---
title: Configurazione delle pipeline di produzione
description: Scopri come configurare le pipeline di produzione per generare e distribuire il codice negli ambienti di produzione.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 98%

---


# Configurazione di una pipeline di produzione {#configure-production-pipeline}

Scopri come configurare le pipeline di produzione per generare e distribuire il codice negli ambienti di produzione. Una pipeline di produzione distribuisce per prima cosa il codice nell’ambiente di staging e, dopo l’approvazione, distribuisce lo stesso codice nell’ambiente di produzione.

Per configurare le pipeline di produzione, l’utente deve avere il ruolo **[Responsabile dell’implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!NOTE]
>
>Non è possibile configurare una pipeline di produzione finché non è stata completata la creazione del programma, non è stato creato almeno un ramo in un archivio Git e non è stato creato un set di ambienti di produzione e di staging.

Prima di iniziare la distribuzione del codice, è necessario configurare le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente che utilizza l’interfaccia utente di [!UICONTROL Cloud Manager], puoi aggiungere una pipeline di produzione seguendo la procedura riportata di seguito.

>[!TIP]
>
>Prima di configurare una pipeline front-end, consulta la sezione [Percorso per la creazione rapida dei siti di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento di AEM per la creazione rapida dei siti. Questo percorso aiuta a semplificare lo sviluppo front-end del sito AEM e consente di personalizzarlo rapidamente senza alcuna conoscenza del back-end di AEM.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e fai clic su **Aggiungi** per selezionare **Aggiungi pipeline di produzione**.

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

1. Nella scheda **Codice sorgente** è necessario definire la posizione da cui la pipeline deve recuperare il relativo codice e il tipo di codice.

   * **[Codice front-end](#front-end-code)**
   * **[Codice full stack](#full-stack-code)**
   * **[Configurazione a livello web](#web-tier-config)**

I passaggi per completare la creazione della pipeline di produzione variano a seconda dell’opzione **Codice sorgente** selezionata. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

### Codice front-end {#front-end-code}

Una pipeline del codice front-end distribuisce le build del codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end).

Per completare la configurazione della pipeline di produzione del codice front-end, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
   * **Sospendi prima della distribuzione in produzione**: sospende la pipeline prima della distribuzione nell’ambiente di produzione.

   ![Codice front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Per salvare la pipeline, fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con la configurazione HTTPD/Dispatcher. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline).

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline del codice full stack, la selezione viene disabilitata.

Per completare la configurazione della pipeline di produzione del codice full stack, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
   * **Sospendi prima della distribuzione in produzione**: sospende la pipeline prima della distribuzione nell’ambiente di produzione.
   * **Pianificato**: consente all’utente di abilitare la pianificazione della distribuzione nell’ambiente di produzione.

   ![Codice full stack](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Per passare alla scheda **Audit dell’esperienza** e definire i percorsi da includere sempre nell’audit dell’esperienza, fai clic su **Continua**.

   ![Aggiunta dell’audit dell’esperienza](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Fornisci un percorso da includere nell’audit dell’esperienza.

   * I percorsi delle pagine devono iniziare con `/`.
   * Ad esempio, se desideri includere `https://wknd.site/us/en/about-us.html` nell’audit dell’esperienza, inserisci il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per l’audit dell’esperienza](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Facendo clic su **Aggiungi pagina**, il percorso viene completato automaticamente con l’indirizzo dell’ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso nella tabella](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Continua ad aggiungere i percorsi che desideri ripetendo i due passaggi precedenti.

   * Puoi aggiungere fino a un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la pagina Home del sito viene inclusa nell’audit dell’esperienza.

1. Per salvare la pipeline, fai clic su **Salva**.

I percorsi configurati per l’audit dell’esperienza vengono inviati al servizio e valutati in termini di prestazioni, accessibilità, SEO (Search Engine Optimization), best practice e test PWA (web app progressiva) durante l’esecuzione della pipeline. Per ulteriori informazioni, consulta la sezione dedicata alla [lettura dei risultati dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md).

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Configurazione a livello web {#web-tier-config}

Una pipeline di configurazione a livello web distribuisce configurazioni HTTPD/Dispatcher. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline).

Per completare la configurazione della pipeline di produzione del codice full stack, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
      * Per le pipeline di configurazione a livello web, in genere si tratta del percorso contenente le directory `conf.d`, `conf.dispatcher.d` e `opt-in`.
      * Ad esempio, se la struttura del progetto è stata generata dall’[archetipo del progetto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) il percorso è `/dispatcher/src`.
   * **Sospendi prima della distribuzione in produzione**: sospende la pipeline prima della distribuzione nell’ambiente di produzione.
   * **Pianificato**: consente all’utente di abilitare la pianificazione della distribuzione nell’ambiente di produzione.

   ![Codice a livello web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Per salvare la pipeline, fai clic su **Salva**.

>[!NOTE]
>
>Se già disponi di una pipeline full stack distribuita in un ambiente, creando una pipeline di configurazione a livello web per lo stesso ambiente la configurazione del livello web esistente nella pipeline full stack verrà ignorata.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

## Sviluppo di Sites con la pipeline front-end {#developing-with-front-end-pipeline}

Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.

Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).

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
