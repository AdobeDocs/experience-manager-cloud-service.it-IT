---
title: Aggiungere una pipeline di produzione
description: Scopri come aggiungere una pipeline di produzione per generare e distribuire il codice negli ambienti di produzione.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 34%

---


# Aggiungere una pipeline di produzione {#configure-production-pipeline}

Scopri come configurare le pipeline di produzione per generare e distribuire il codice negli ambienti di produzione. Una pipeline di produzione distribuisce prima il codice nell’ambiente di staging. Dopo l’approvazione, distribuisce lo stesso codice nell’ambiente di produzione.

Per configurare le pipeline di produzione, l’utente deve avere il ruolo **[Responsabile dell’implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!NOTE]
>
>Non è possibile impostare una pipeline di produzione finché non si verifica quanto segue:
>
>* Il programma viene creato.
>* L’archivio Git dispone di almeno un ramo.
>* Vengono creati gli ambienti di produzione e di staging.

Prima di iniziare la distribuzione del codice, configura le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiungere una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente che utilizza l&#39;interfaccia utente di [!UICONTROL Cloud Manager], puoi aggiungere una pipeline di produzione seguendo la procedura riportata di seguito.

>[!TIP]
>
>Prima di configurare una pipeline front-end, consulta [Percorso per la creazione rapida dei siti di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento AEM per la creazione rapida dei siti. Questo percorso può aiutarti a semplificare lo sviluppo front-end del tuo sito AEM, consentendoti di personalizzare rapidamente il tuo sito senza alcuna conoscenza del back-end di AEM.

1. Accedi a Cloud Manager all&#39;indirizzo [experiece.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale sinistro fare clic su **Cloud Manager**.
1. Selezionare un&#39;organizzazione desiderata.
1. Nella console **Programmi** fare clic su un programma.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma** e fai clic su **Aggiungi** per selezionare **Aggiungi pipeline di produzione**.

   ![Scheda Pipeline nella panoramica del responsabile del programma](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Viene visualizzata la finestra di dialogo **Aggiungi pipeline di produzione**. Per identificare la pipeline, fornisci un **nome della pipeline** con le seguenti opzioni. Fai clic su **Continua**.

   **Trigger distribuzione**: quando si definiscono i trigger della distribuzione per avviare la pipeline, le opzioni disponibili sono le seguenti.

   * **Manuale** - Avvia la pipeline manualmente.
   * **Su modifiche Git** - Avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione è comunque possibile avviare la pipeline manualmente secondo necessità.

   **Comportamento in caso di errori relativi a metriche importanti**: durante la configurazione o la modifica della pipeline, l’utente con il ruolo **Responsabile dell’implementazione** può definire il comportamento della pipeline in caso di errore importante rilevato da un gate di qualità. Opzioni disponibili:

   * **Chiedi ogni volta** - Impostazione predefinita. Richiede l&#39;intervento manuale in caso di errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, questo processo simula un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo processo simula un utente che approva manualmente ogni errore.

   ![Configurazione della pipeline di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Nella scheda **Codice Source**, seleziona il tipo di codice da elaborare con la pipeline.

   * **[Configurare una pipeline del codice full stack](#full-stack-code)**
   * **[Configurare una pipeline di distribuzione di destinazione](#targeted-deployment)**

Per ulteriori informazioni sui tipi di pipeline, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

I passaggi per completare la creazione della pipeline di produzione variano a seconda del tipo di codice sorgente selezionato. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

### Configurare una pipeline del codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con la configurazione HTTPD/Dispatcher.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline del codice full stack, la selezione viene disabilitata.

**Per configurare una pipeline del codice full stack:**

1. Nella scheda **Codice Source**, definisci le opzioni seguenti.

   * **Archivio**: definisce l&#39;archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Consulta [Aggiungere e gestire archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Definisce da quale ramo la pipeline selezionata deve recuperare il codice.
Inserisci i primi caratteri del nome del ramo e la funzione di completamento automatico di questo campo trova i rami corrispondenti per aiutarti a selezionare.
   * **Ignora configurazione a livello web**: se questa opzione è selezionata, la pipeline non distribuisce la configurazione a livello web.
   * **Sospendi prima della distribuzione nell&#39;ambiente di produzione** - Sospende la pipeline prima della distribuzione nell&#39;ambiente di produzione.
   * **Pianificato** - Consente all&#39;utente di abilitare la distribuzione di produzione pianificata.

   ![Codice full stack](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Per passare alla scheda **Audit dell’esperienza** e definire i percorsi da includere sempre nell’audit dell’esperienza, fai clic su **Continua**.

   ![Aggiunta dell’audit dell’esperienza](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Fornisci percorsi da includere nell’audit dell’esperienza.

   * Per ulteriori informazioni, vedere [Test di verifica dell&#39;esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration).

1. Per salvare la pipeline, fai clic su **Salva**.

Durante l’esecuzione della pipeline, i percorsi configurati per l’audit dell’esperienza vengono inviati e valutati in base a prestazioni, accessibilità, SEO, best practice e test di PWA. Per ulteriori dettagli, vedere [Informazioni sui risultati dell&#39;audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md).

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Configurare una pipeline di distribuzione di destinazione {#targeted-deployment}

Una distribuzione mirata distribuisce il codice solo per parti selezionate dell’applicazione AEM. In tale distribuzione, puoi scegliere di **Includere** uno dei seguenti tipi di codice:

* **Configurazione** - Configura le impostazioni per varie funzioni nell&#39;ambiente AEM.
   * Consulta [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md) per un elenco delle configurazioni supportate, tra cui inoltro log, attività di manutenzione correlate all&#39;eliminazione e varie configurazioni CDN, e per gestirle nel tuo archivio in modo che vengano distribuite correttamente.
   * Quando si esegue una pipeline di distribuzione di destinazione, le configurazioni vengono distribuite, purché vengano salvate nell’ambiente, nell’archivio e nel ramo definiti nella pipeline.
   * In qualsiasi momento può essere presente una sola pipeline di configurazione per ogni ambiente.
* **Configura pipeline di configurazione di Edge Delivery Services** - Le pipeline di configurazione di Edge Delivery non dispongono di ambienti di sviluppo, staging e produzione separati. In AEM as a Cloud Service, le modifiche passano attraverso i livelli di sviluppo, stage e produzione. Al contrario, una pipeline di configurazione di Edge Delivery applica la propria configurazione direttamente a tutti i domini di Edge Delivery Sites registrati in Cloud Manager. Per ulteriori informazioni, consulta [Aggiungere una pipeline di Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
* **Codice front-end**: configura JavaScript e CSS per il front-end dell&#39;applicazione AEM.
   * Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.
   * Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
* **Configurazione a livello web**: configura le proprietà di Dispatcher per archiviare, elaborare e inviare pagine Web al client.
   * Per ulteriori dettagli, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Se esiste una pipeline del codice a livello web per l’ambiente selezionato, questa selezione è disabilitata.
   * Se crei una pipeline di configurazione a livello web per un ambiente con una pipeline full stack esistente, la configurazione a livello web nella pipeline full stack viene ignorata. Questa modifica influisce solo sulla configurazione a livello web in tale ambiente.

>[!NOTE]
>
>Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per informazioni dettagliate e l&#39;elenco completo delle limitazioni, vedere [Aggiunta di archivi privati in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

**Per configurare una pipeline di distribuzione di destinazione:**

1. Scegliere il tipo di distribuzione desiderato.

![Opzioni di distribuzione di destinazione](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Definisci gli **ambienti di distribuzione idonei**.

   * Se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.

1. In **Codice Source**, definire le opzioni seguenti:

   * **Archivio**: questa opzione definisce da quale archivio Git la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git**: questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo: la funzione di completamento automatico di questo campo. trova i rami corrispondenti che puoi selezionare.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
   * **Sospendi prima della distribuzione in produzione**: sospende la pipeline prima della distribuzione nell’ambiente di produzione.
   * **Pianificato** - Consente all&#39;utente di abilitare la distribuzione di produzione pianificata. Disponibile solo per le distribuzioni mirate a livello web.

   ![Pipeline di configurazione](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

## Ignora pacchetti Dispatcher {#skip-dispatcher-packages}

Per creare pacchetti Dispatcher nella pipeline senza pubblicarli nell’archiviazione della build, puoi disabilitare l’opzione di pubblicazione. Questa operazione può contribuire a ridurre il tempo di esecuzione della pipeline.

Per disabilitare la pubblicazione dei pacchetti dispatcher, aggiungi la seguente configurazione tramite il file di progetto `pom.xml`. Una variabile di ambiente funge da flag impostato nel contenitore della build di Cloud Manager per determinare quando ignorare i pacchetti Dispatcher.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
