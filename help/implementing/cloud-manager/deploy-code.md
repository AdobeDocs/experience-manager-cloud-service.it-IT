---
title: Distribuisci il tuo codice - Cloud Services
description: Distribuisci il tuo codice - Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 782035708467693ec7648b1fd701c329a0b5f7c8
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# Implementazione del codice {#deploy-your-code}

## Distribuzione di codice con Cloud Manager in AEM come Cloud Service {#deploying-code-with-cloud-manager}

Dopo aver configurato la pipeline di produzione (archivio, ambiente e ambiente di test), è possibile distribuire il codice.

1. Fai clic su **Distribuisci** da Cloud Manager per avviare il processo di distribuzione.

   ![](assets/deploy-code1.png)


1. Viene visualizzata la schermata **Esecuzione pipeline** .

   Fai clic su **Genera** per avviare il processo.

   ![](assets/deploy-code2.png)

1. Il processo di compilazione completo distribuisce il codice.

   Nel processo di creazione sono coinvolte le seguenti fasi:

   1. Implementazione fase
   1. Test della fase
   1. Distribuzione di produzione

   >[!NOTE]
   >
   >Inoltre, puoi rivedere i passaggi dei vari processi di distribuzione visualizzando i registri o rivedendo i risultati per i criteri di test.

   La **distribuzione della fase** prevede i seguenti passaggi:

   * Convalida: Questo passaggio assicura che la pipeline sia configurata per utilizzare le risorse attualmente disponibili, ad esempio che il ramo configurato esista, che gli ambienti siano disponibili.
   * Build &amp; Unit Testing: Questo passaggio esegue un processo di compilazione containerizzato. Per informazioni dettagliate sull’ambiente di compilazione, consulta [Generazione di dettagli ambiente](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md) .
   * Scansione del codice: Questo passaggio valuta la qualità del codice dell&#39;applicazione. Per informazioni dettagliate sul processo di test, consulta [Test della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) .
   * Crea immagini: Questo passaggio include un file di registro dal processo utilizzato per creare le immagini. Questo processo è responsabile della trasformazione dei pacchetti di contenuti e dispatcher prodotti dalla fase di creazione in immagini Docker e configurazione Kubernetes.
   * Distribuisci su Stage

      ![](assets/stage-deployment.png)
   La **prova della fase** prevede i seguenti passaggi:

   * **Test** funzionale del prodotto: Le esecuzioni della pipeline di Cloud Manager supporteranno l’esecuzione di test eseguiti sull’ambiente stage.
Per ulteriori informazioni, consulta [Test funzionale del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) .

   * **Test** funzionali personalizzati: Questo passaggio nella pipeline è sempre presente e non può essere ignorato. Tuttavia, se la build non produce JAR di test, il test viene superato per impostazione predefinita.\
      Per ulteriori informazioni, consulta [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) .

   * **Test** interfaccia utente personalizzati: Questo passaggio è una funzione opzionale che consente ai nostri clienti di creare ed eseguire automaticamente i test dell’interfaccia utente per le loro applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium).
Per ulteriori informazioni, consulta [Test personalizzati dell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=en#custom-ui-testing) .


   * **Audit** esperienza: Questo passaggio nella pipeline è sempre presente e non può essere ignorato. Quando viene eseguita una pipeline di produzione, viene incluso un passaggio di controllo dell’esperienza dopo un test funzionale personalizzato che eseguirà i controlli. Le pagine configurate verranno inviate al servizio e valutate. I risultati sono informativi e consentono all’utente di visualizzare i punteggi e il cambiamento tra il punteggio corrente e quello precedente. Questa informazione è utile per determinare se vi è una regressione che verrà introdotta con la distribuzione corrente.
Per ulteriori informazioni, consulta [Informazioni sui risultati di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) .

      ![](assets/stage-testing.png)





## Processo di distribuzione {#deployment-process}

La sezione seguente descrive come i pacchetti AEM e dispatcher vengono distribuiti nella fase di stage e nella fase di produzione.

Cloud Manager carica tutti i file target/*.zip prodotti dal processo di compilazione in una posizione di archiviazione.  Questi artefatti vengono recuperati da questa posizione durante le fasi di distribuzione della pipeline.

Quando Cloud Manager viene implementato in topologie non di produzione, l’obiettivo è quello di completare l’implementazione il più rapidamente possibile e, pertanto, gli artefatti vengono distribuiti simultaneamente su tutti i nodi come segue:

1. Cloud Manager determina se ogni artefatto è un pacchetto AEM o dispatcher.
1. Cloud Manager rimuove tutti i dispatcher dal Load Balancer per isolare l’ambiente durante la distribuzione.

   A meno che non sia configurato diversamente, è possibile saltare le modifiche del Load Balancer nelle implementazioni di sviluppo e stage, ovvero scollegare e allegare i passaggi sia nelle pipeline non di produzione, per gli ambienti di sviluppo e nella pipeline di produzione, per gli ambienti di stage.

   >[!NOTE]
   >
   >Questa funzione dovrebbe essere utilizzata principalmente da 1-1-1 clienti.

1. Ciascun artefatto AEM viene distribuito a ogni istanza AEM tramite API di Gestione pacchetti, con dipendenze dei pacchetti che determinano l’ordine di distribuzione.

   Per ulteriori informazioni su come utilizzare i pacchetti per installare nuove funzionalità, trasferire contenuti tra le istanze e eseguire il backup del contenuto dell’archivio, consulta Come utilizzare i pacchetti.

   >[!NOTE]
   >
   >Tutti gli artefatti AEM vengono distribuiti sia all’autore che agli editori. Le modalità di esecuzione devono essere utilizzate quando sono necessarie configurazioni specifiche per il nodo. Per ulteriori informazioni su come le modalità di esecuzione ti consentono di regolare la tua istanza AEM per uno scopo specifico, fai riferimento alle modalità di esecuzione.

1. L’artefatto del dispatcher viene distribuito a ciascun dispatcher come segue:

   1. Le configurazioni correnti vengono sottoposte a backup e copiate in una posizione temporanea
   1. Tutte le configurazioni vengono eliminate tranne i file immutabili. Per ulteriori informazioni, consulta Gestire le configurazioni del Dispatcher . Questo cancella le directory per garantire che non vengano lasciati indietro i file orfani.
   1. L’artefatto viene estratto nella directory `httpd`.  I file immutabili non vengono sovrascritti. Eventuali modifiche apportate ai file immutabili nell’archivio Git verranno ignorate al momento della distribuzione.  Questi file sono di base del framework del dispatcher AMS e non possono essere modificati.
   1. Apache esegue un test di configurazione. Se non viene rilevato alcun errore, il servizio viene ricaricato. Se si verifica un errore, le configurazioni vengono ripristinate dal backup, il servizio viene ricaricato e l&#39;errore viene riportato a Cloud Manager.
   1. Ogni percorso specificato nella configurazione della pipeline viene invalidato o scaricato dalla cache del dispatcher.

   >[!NOTE]
   >
   >Cloud Manager prevede che l’artefatto del dispatcher contenga l’intero set di file.  Tutti i file di configurazione del dispatcher devono essere presenti nell’archivio Git. File o cartelle mancanti causeranno un errore di distribuzione.

1. Dopo la corretta distribuzione di tutti i pacchetti AEM e dispatcher a tutti i nodi, i dispatcher vengono aggiunti nuovamente al load balancer e la distribuzione è completa.

   >[!NOTE]
   >
   >È possibile saltare le modifiche al load balancer nelle distribuzioni di sviluppo e stage, ovvero scollegare e allegare i passaggi sia nelle pipeline non di produzione, per gli ambienti di sviluppo e nella pipeline di produzione, per gli ambienti di stage.

### Fase di distribuzione alla produzione {#deployment-production-phase}

Il processo di distribuzione nelle topologie di produzione è leggermente diverso per ridurre al minimo l’impatto sui visitatori AEM sito.

Le distribuzioni di produzione seguono generalmente gli stessi passaggi indicati in precedenza, ma in modo continuo:

1. Distribuisci pacchetti AEM per l’authoring.
1. Scollega dispatcher1 dal load balancer.
1. Distribuisci pacchetti AEM a publish1 e il pacchetto dispatcher a dispatcher1, svuota la cache del dispatcher.
1. Rimetti dispatcher1 nel load balancer.
1. Una volta che dispatcher1 è tornato in servizio, scollega dispatcher2 dal load balancer.
1. Distribuisci pacchetti AEM a publish2 e il pacchetto dispatcher a dispatcher2, svuota la cache del dispatcher.
1. Rimetti dispatcher2 nel load balancer.
Questo processo continua fino a quando la distribuzione non raggiunge tutti gli editori e i dispatcher nella topologia.
