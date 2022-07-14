---
title: Configurazione delle pipeline di produzione
description: Scopri come configurare le pipeline di produzione per generare e distribuire il codice agli ambienti di produzione.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# Configurazione di una pipeline di produzione {#configure-production-pipeline}

Scopri come configurare le pipeline di produzione per generare e distribuire il codice agli ambienti di produzione. Una pipeline di produzione distribuisce il codice prima nell’ambiente Stage e dopo l’approvazione distribuisce lo stesso codice all’ambiente di produzione.

Un utente deve avere **[Gestione distribuzione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** ruolo per configurare le pipeline di produzione.

>[!NOTE]
>
>Non è possibile impostare una pipeline di produzione fino al completamento della creazione del programma, un archivio Git dispone di almeno un ramo e viene creato un set di ambienti di produzione e staging.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline dal [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando [!UICONTROL Cloud Manager] Interfaccia utente, puoi aggiungere una pipeline di produzione seguendo questi passaggi.

>[!TIP]
>
>Prima di configurare una pipeline front-end, consulta la sezione [AEM Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per una guida end-to-end attraverso lo strumento di facile utilizzo AEM creazione rapida di siti. Questo percorso consente di semplificare lo sviluppo front-end del sito AEM, consentendo di personalizzare rapidamente il sito senza AEM conoscenza back-end.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e fai clic su **Aggiungi** per selezionare **Aggiungi pipeline di produzione**.

   ![Panoramica sulla scheda Pipelines in Program Manager](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. La **Aggiungi pipeline di produzione** viene visualizzata la finestra di dialogo. Fornisci un **Nome della pipeline** per identificare la pipeline con le seguenti opzioni. Fai clic su **Continua**.

   **Trigger distribuzione** - Quando definisci gli attivatori della distribuzione per avviare la pipeline, sono disponibili le seguenti opzioni.

   * **Manuale** - Utilizzare questa opzione per avviare manualmente la pipeline.
   * **Su modifiche Git** - Questa opzione avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo git configurato. Con questa opzione, potete comunque avviare la pipeline manualmente come necessario.

   **Comportamento di errori di metrica importanti** - Durante la configurazione o la modifica della pipeline, il **Gestione distribuzione** ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei cancelli di qualità. Le opzioni disponibili sono:

   * **Chiedi sempre** - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
   * **Non riuscito immediatamente** - Se selezionata, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.

   ![Configurazione della pipeline di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Sulla **Codice sorgente** scheda è necessario definire la posizione in cui la pipeline deve recuperare il proprio codice e il tipo di codice in cui si trova.

   * **[Codice front-end](#front-end-code)**
   * **[Codice Stack Completo](#full-stack-code)**
   * **[Configurazione a livello web](#web-tier-config)**

I passaggi per completare la creazione della pipeline di produzione variano a seconda dell’opzione per **Codice sorgente** selezionato. Segui i collegamenti sopra riportati per passare alla sezione successiva del documento per completare la configurazione della pipeline.

### Codice front-end {#front-end-code}

Una pipeline di codice front-end implementa build di codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per ulteriori informazioni su questo tipo di pipeline.

Per completare la configurazione della pipeline di produzione del codice front-end, effettua le seguenti operazioni.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.
   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo e la funzione di completamento automatico di questo campo troverà i rami corrispondenti per aiutarti a selezionare.
   * **Posizione codice** - Questa opzione definisce il percorso nel ramo dell’archivio selezionato da cui la pipeline deve recuperare il codice.
   * **Sospendi prima dell’implementazione in produzione** - Questa opzione mette in pausa la pipeline prima dell’implementazione in produzione.

   ![Codice front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Fai clic su **Salva** per salvare la pipeline.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

### Codice Stack Completo {#full-stack-code}

Una pipeline di codice a stack completo distribuisce simultaneamente build di codice back-end e front-end contenenti una o più applicazioni server AEM insieme alla configurazione HTTPD/Dispatcher. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) per ulteriori informazioni su questo tipo di pipeline.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline di codice con stack completo, questa selezione verrà disabilitata.

Per completare la configurazione della pipeline di produzione del codice full-stack, segui questi passaggi.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.
   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo e la funzione di completamento automatico di questo campo troverà i rami corrispondenti per aiutarti a selezionare.
   * **Posizione codice** - Questa opzione definisce il percorso nel ramo dell’archivio selezionato da cui la pipeline deve recuperare il codice.
   * **Sospendi prima dell’implementazione in produzione** - Questa opzione mette in pausa la pipeline prima dell’implementazione in produzione.
   * **Pianificato** - Questa opzione consente all&#39;utente di abilitare la distribuzione di produzione pianificata.

   ![Codice stack completo](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Fai clic su **Continua** per passare al **Audit delle esperienze** scheda in cui puoi definire i percorsi che devono sempre essere inclusi nel Experience Audit.

   ![Aggiungi audit esperienza](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Fornisci un percorso da includere nel Experience Audit.

   * I percorsi delle pagine devono iniziare con `/`.
   * Ad esempio, se desideri includere `https://wknd.site/us/en/about-us.html` in Audit esperienze, immetti il percorso `/us/en/about-us.html`.

   ![Definizione di un percorso per il controllo delle esperienze](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Fai clic su **Aggiungi pagina** e il percorso verrà completato automaticamente con l’indirizzo dell’ambiente e aggiunto alla tabella dei percorsi.

   ![Salvataggio del percorso della tabella](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Continua ad aggiungere i percorsi in base alle necessità ripetendo i due passaggi precedenti.

   * Puoi aggiungere un massimo di 25 percorsi.
   * Se non definisci alcun percorso, per impostazione predefinita la home page del sito verrà inclusa in Experience Audit.

1. Fai clic su **Salva** per salvare la pipeline.

I percorsi configurati per Experience Audit verranno inviati al servizio e valutati in base alle prestazioni, all’accessibilità, all’ottimizzazione SEO (Search Engine Optimization), alle best practice e ai test PWA (Progressive Web App) durante l’esecuzione della pipeline. Fai riferimento a [Risultati di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) per ulteriori dettagli.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

### Configurazione a livello web {#web-tier-config}

Una pipeline di configurazione a livello web distribuisce configurazioni HTTPD/Dispatcher. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) per ulteriori informazioni su questo tipo di pipeline.

Per completare la configurazione della pipeline di produzione del codice full-stack, segui questi passaggi.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.
   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo e la funzione di completamento automatico di questo campo troverà i rami corrispondenti per aiutarti a selezionare.
   * **Posizione codice** - Questa opzione definisce il percorso nel ramo dell’archivio selezionato da cui la pipeline deve recuperare il codice.
      * Per le pipeline di configurazione livello web, in genere si tratta del percorso contenente `conf.d`, `conf.dispatcher.d`e `opt-in` directory.
      * Ad esempio, se la struttura del progetto è stata generata dal [Archetipo AEM progetto,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) il percorso sarebbe `/dispatcher/src`.
   * **Sospendi prima dell’implementazione in produzione** - Questa opzione mette in pausa la pipeline prima dell’implementazione in produzione.
   * **Pianificato** - Questa opzione consente all&#39;utente di abilitare la distribuzione di produzione pianificata.

   ![Codice a livello web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Fai clic su **Salva** per salvare la pipeline.

>[!NOTE]
>
>Se disponi di una pipeline full-stack esistente che viene distribuita in un ambiente, la creazione di una pipeline di configurazione del livello web per lo stesso ambiente comporterà l’eliminazione della configurazione del livello web esistente nella pipeline full-stack.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

## Ignora pacchetti Dispatcher {#skip-dispatcher-packages}

Se desideri che i pacchetti del dispatcher siano generati come parte della pipeline, ma non desideri che vengano pubblicati per creare l’archiviazione, puoi disattivarli, riducendo la durata dell’esecuzione della pipeline.

Per disabilitare la pubblicazione dei pacchetti dispatcher, devi aggiungere la seguente configurazione tramite il tuo progetto `pom.xml` file. Si basa su una variabile di ambiente, che funge da flag impostabile nel contenitore di build di Cloud Manager per definire quando i pacchetti del dispatcher devono essere ignorati.

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
