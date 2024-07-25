---
title: Configurazione delle pipeline di produzione
description: Scopri come configurare le pipeline di produzione per generare e distribuire il codice negli ambienti di produzione.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 68%

---


# Configurazione di una pipeline di produzione {#configure-production-pipeline}

Scopri come configurare le pipeline di produzione per generare e distribuire il codice negli ambienti di produzione. Una pipeline di produzione distribuisce prima il codice nell’ambiente di staging e, dopo l’approvazione, distribuisce lo stesso codice nell’ambiente di produzione.

Per configurare le pipeline di produzione, l’utente deve avere il ruolo **[Responsabile dell’implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!NOTE]
>
>Non è possibile impostare una pipeline di produzione finché non viene completata la creazione del programma, un archivio Git non dispone di almeno un ramo e non viene creato un set di ambienti di produzione e di staging.

Prima di iniziare la distribuzione del codice, è necessario configurare le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente che utilizza l’interfaccia utente di [!UICONTROL Cloud Manager], puoi aggiungere una pipeline di produzione seguendo la procedura riportata di seguito.

>[!TIP]
>
>Prima di configurare una pipeline front-end, consulta la sezione [Percorso per la creazione rapida dei siti di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento di AEM per la creazione rapida dei siti. Questo percorso aiuta a semplificare lo sviluppo front-end del sito AEM e consente di personalizzarlo rapidamente senza alcuna conoscenza del back-end di AEM.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma** e fai clic su **Aggiungi** per selezionare **Aggiungi pipeline di produzione**.

   ![Scheda Pipeline nella panoramica del responsabile del programma](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Viene visualizzata la finestra di dialogo **Aggiungi pipeline di produzione**. Per identificare la pipeline, fornisci un **nome della pipeline** con le seguenti opzioni. Fai clic su **Continua**.

   **Trigger distribuzione**: quando si definiscono i trigger della distribuzione per avviare la pipeline, le opzioni disponibili sono le seguenti.

   * **Manuale**: per avviare la pipeline manualmente.
   * **Alla modifica Git**: per avviare la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione è comunque possibile avviare la pipeline manualmente secondo necessità.

   **Comportamento in caso di errori relativi a metriche importanti**: durante la configurazione o la modifica della pipeline, l’utente con il ruolo **Responsabile dell’implementazione** può definire il comportamento della pipeline in caso di errore importante rilevato da un gate di qualità. Opzioni disponibili:

   * **Chiedi ogni volta**: impostazione predefinita che richiede l’intervento manuale per tutti gli errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, quest’opzione simula un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente**: selezionando questa opzione, la pipeline avanza automaticamente ogni volta che si verifica un errore importante. In sostanza, quest’opzione simula un utente che approva manualmente ogni errore.

   ![Configurazione della pipeline di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Nella scheda **Codice Source** è necessario selezionare il tipo di codice che deve essere elaborato dalla pipeline.

   * **[Codice full stack](#full-stack-code)**
   * **[Distribuzione di destinazione](#targeted-deployment)**

Per ulteriori informazioni sui tipi di pipeline, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

I passaggi per completare la creazione della pipeline di produzione variano a seconda del tipo di codice sorgente selezionato. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

### Codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server AEM con la configurazione HTTPD/Dispatcher.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline del codice full stack, la selezione viene disabilitata.

Per completare la configurazione della pipeline di produzione del codice full stack, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Ignora configurazione a livello web**: se questa opzione è selezionata, la pipeline non distribuisce la configurazione a livello web.
   * **Sospendi prima della distribuzione in produzione**: sospende la pipeline prima della distribuzione nell’ambiente di produzione.
   * **Pianificato**: consente all’utente di abilitare la pianificazione della distribuzione nell’ambiente di produzione.

   ![Codice full stack](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Tocca o fai clic su **Continua** per passare alla scheda **Audit dell&#39;esperienza** in cui puoi definire i percorsi da includere sempre nell&#39;audit dell&#39;esperienza.

   ![Aggiunta dell’audit dell’esperienza](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Fornisci percorsi da includere nell’audit dell’esperienza.

   * Per informazioni dettagliate, consulta il documento [Test di audit dell&#39;esperienza](/help/implementing/cloud-manager/experience-audit-testing.md#configuration).

1. Per salvare la pipeline, fai clic su **Salva**.

I percorsi configurati per l’audit dell’esperienza vengono inviati al servizio e valutati in termini di prestazioni, accessibilità, SEO (Search Engine Optimization), best practice e test PWA (web app progressiva) durante l’esecuzione della pipeline. Per ulteriori informazioni, consulta la sezione dedicata alla [lettura dei risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md).

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Distribuzione mirata {#targeted-deployment}

Una distribuzione mirata distribuisce il codice solo per parti selezionate dell’applicazione AEM. In tale distribuzione è possibile scegliere di **Includere** uno dei seguenti tipi di codice:

* **Configurazione** - Configura le impostazioni per varie funzionalità nell&#39;ambiente AEM.
   * Consulta l&#39;articolo [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md) per un elenco delle configurazioni supportate, che include l&#39;inoltro del registro, le attività di manutenzione correlate all&#39;eliminazione e varie configurazioni CDN, e per gestirle nel tuo archivio in modo che vengano distribuite correttamente.
   * Quando si esegue una pipeline di distribuzione di destinazione, le configurazioni vengono distribuite, purché vengano salvate nell’ambiente, nell’archivio e nel ramo definiti nella pipeline.
   * In qualsiasi momento può essere presente una sola pipeline di configurazione per ogni ambiente.
* **Codice front-end**: configura JavaScript e CSS per il front-end dell&#39;applicazione AEM.
   * Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.
   * Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
* **Configurazione a livello web**: configura le proprietà del dispatcher per archiviare, elaborare e consegnare le pagine web al client.
   * Per ulteriori dettagli, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Se esiste una pipeline del codice a livello web per l’ambiente selezionato, questa selezione è disabilitata.
   * Se già disponi di una pipeline full stack distribuita in un ambiente, creando una pipeline di configurazione a livello web per lo stesso ambiente la configurazione del livello web esistente nella pipeline full stack verrà ignorata.

>[!NOTE]
>
>Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per dettagli e un elenco completo delle limitazioni, consulta [Aggiunta di archivi privati in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

I passaggi per completare la creazione della pipeline di distribuzione di produzione con targeting sono gli stessi quando scegli un tipo di distribuzione.

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
   * **Pianificato** - Questa opzione consente all&#39;utente di abilitare la distribuzione di produzione pianificata. Disponibile solo per le distribuzioni mirate a livello web.

   ![Pipeline di configurazione](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

## Ignorare i pacchetti Dispatcher {#skip-dispatcher-packages}

Se desideri che i pacchetti dispatcher vengano generati come parte della pipeline, ma non che vengano pubblicati nell’archivio della build, puoi disabilitare la pubblicazione riducendo in tal modo la durata dell’esecuzione della pipeline.

Per disabilitare la pubblicazione dei pacchetti dispatcher, aggiungi la seguente configurazione tramite il file di progetto `pom.xml`. Si basa su una variabile di ambiente che funge da flag impostabile nel contenitore della build di Cloud Manager per definire quando ignorare i pacchetti dispatcher.

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
