---
title: Distribuisci il tuo codice - Cloud Services
description: Distribuisci il tuo codice - Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 64023bbdccd8d173b15e3984d0af5bb59a2c1447
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

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

Tutte le distribuzioni di Cloud Service seguono un processo continuo per garantire tempi di inattività pari a zero. Per ulteriori informazioni, consulta [Come funzionano le implementazioni continue](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#how-rolling-deployments-work) .

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
