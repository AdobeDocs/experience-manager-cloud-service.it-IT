---
title: Come utilizzare AEM Forms per l'automazione dei processi aziendali (BPM, Business Process Automation)?
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Utilizza AEM Forms Workflow per automatizzare e creare rapidamente flussi di lavoro per i processi aziendali. Ad esempio, revisione e approvazione, Generazione di PDF, Flussi di lavoro di Adobe Sign.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f0fec4a9-b214-4931-bf09-5898b082481e
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2489'
ht-degree: 1%

---

# Flusso di lavoro incentrato su Forms su OSGi {#forms-centric-workflow-on-osgi}

![Immagine protagonista](do-not-localize/header.png)

Le aziende raccolgono dati da centinaia e migliaia di moduli, da vari sistemi back-end e da origini dati online o offline. Hanno anche un set dinamico di utenti per prendere decisioni sui dati, che comporta processi iterativi di revisione e approvazione.

Oltre ai flussi di lavoro di revisione e approvazione per il pubblico interno ed esterno, le grandi organizzazioni e le aziende hanno attività ripetitive. Ad esempio, la conversione di un documento PDF in un altro formato. Se eseguite manualmente, queste attività richiedono molto tempo e risorse. Le aziende hanno anche l&#39;obbligo legale di firmare digitalmente un documento e archiviare i dati dei moduli per un successivo utilizzo in formati predefiniti.

## Introduzione al flusso di lavoro incentrato su Forms su OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puoi utilizzare Flussi di lavoro di AEM per creare rapidamente flussi di lavoro basati su Forms adattivi. Questi flussi di lavoro possono essere utilizzati per la revisione e l’approvazione, per i flussi di processo aziendali, per avviare i servizi documentali, per l’integrazione con il flusso di lavoro della firma di Adobe Sign e per operazioni simili. Ad esempio, l&#39;elaborazione della richiesta della carta di credito, il dipendente lascia i flussi di lavoro di approvazione, salvando un modulo come documento PDF. Inoltre, questi flussi di lavoro possono essere utilizzati all’interno di un’organizzazione o attraverso un firewall di rete.

Con un flusso di lavoro incentrato su Forms su OSGi, puoi creare e distribuire rapidamente flussi di lavoro per varie attività sullo stack OSGi, senza dover installare la funzionalità completa di gestione dei processi sullo stack JEE. Lo sviluppo e la gestione dei flussi di lavoro utilizzano le familiari funzionalità di AEM Workflow e Casella in entrata di AEM. I flussi di lavoro costituiscono la base per automatizzare i processi aziendali reali che si estendono su più sistemi software, reti, reparti e persino organizzazioni.

Una volta configurati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o essere eseguiti a livello di programmazione quando gli utenti inviano un modulo <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

Il flusso di lavoro incentrato su Forms su OSGi estende la cartella Posta in arrivo di [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) e fornisce componenti aggiuntivi (passaggi) che consentono all&#39;editor di flussi di lavoro AEM di aggiungere supporto per i flussi di lavoro incentrati su [!DNL AEM Forms]. <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

Tutti i [!DNL AEM Forms] passaggi del flusso di lavoro supportano l&#39;utilizzo di variabili. Le variabili consentono ai passaggi del flusso di lavoro di conservare e trasmettere metadati tra i passaggi in fase di esecuzione. Puoi creare diversi tipi di variabili per memorizzare diversi tipi di dati. Puoi anche creare raccolte di variabili (array) per memorizzare più istanze di dati correlati dello stesso tipo. In genere, si utilizza una variabile o una raccolta di variabili quando è necessario prendere una decisione in base al valore in essa contenuto o per memorizzare le informazioni necessarie in un secondo momento di un processo. Per ulteriori informazioni sull&#39;utilizzo delle variabili in questi componenti del flusso di lavoro incentrati su Forms (passaggi), vedi [Flusso di lavoro incentrato su Forms in OSGi - Riferimento passaggio](aem-forms-workflow-step-reference.md). Per informazioni sulla creazione e la gestione delle variabili, consulta [Variabili nei flussi di lavoro di AEM](variable-in-aem-workflows.md).

Il diagramma seguente illustra la procedura end-to-end per creare, eseguire e monitorare un flusso di lavoro incentrato su Forms su OSGi.

![introduzione-ad-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Applicabilità e casi d’uso

### Assicurazione

## AEM Forms supporta i flussi di lavoro di approvazione delle assicurazioni?

Sì. AEM Forms supporta le revisioni e le approvazioni basate sul flusso di lavoro, consentendo la revisione dei revisori, l’approvazione dei manager e i cicli di rilavorazione come parte dei processi assicurativi.

## AEM Forms supporta i processi di maker-checker per il settore assicurativo?

Sì. I flussi di lavoro di AEM Forms possono essere configurati per supportare i modelli di maker-checker, garantendo la separazione dei compiti tra i ruoli di immissione dati e approvazione.

## AEM Forms può tenere traccia dello stato delle richieste di risarcimento o delle domande di risarcimento?

Sì. I flussi di lavoro di AEM Forms consentono agli assicuratori di tenere traccia dell’invio dei moduli e dello stato di elaborazione in diverse fasi del processo aziendale.

## AEM Forms supporta i flussi di lavoro di sottoscrizione?

Sì, con flussi di lavoro e integrazioni. AEM Forms supporta processi basati sul flusso di lavoro e integrazioni back-end che consentono il flusso dei dati delle applicazioni nei sistemi di sottoscrizione e decisioning.

## AEM Forms supporta audit trail per i processi assicurativi?

Sì. AEM Forms supporta la verificabilità attraverso la cronologia dei flussi di lavoro, i controlli di accesso e i registri di sistema, che consentono alle compagnie di assicurazione di soddisfare le esigenze di audit interno ed esterno.

## Prima di iniziare {#before-you-start}

* Un flusso di lavoro è una rappresentazione di un processo aziendale reale. Tenere pronto il processo aziendale reale e l&#39;elenco dei partecipanti al processo aziendale. Inoltre, tieni il materiale collaterale (Forms adattivo, documenti PDF e altro) pronto prima di iniziare a creare un flusso di lavoro.
* Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata di AEM e aiutano a segnalare l’avanzamento del flusso di lavoro. Dividere il processo aziendale in fasi logiche.
* Puoi configurare il passaggio di assegnazione delle attività dei flussi di lavoro AEM per inviare notifiche e-mail agli utenti o agli assegnatari. Pertanto, [abilita notifiche e-mail](#configure-email-service).
* Un flusso di lavoro può utilizzare anche Adobe sign per le firme digitali. Se prevedi di utilizzare Adobe Sign in un flusso di lavoro, [configura Adobe Sign per [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) prima di utilizzarlo in un flusso di lavoro.

## Creare un modello di flusso di lavoro {#create-a-workflow-model}

Un modello di flusso di lavoro è costituito dalla logica e dal flusso di un processo aziendale. È costituito da una serie di passaggi. Questi passaggi sono relativi ai componenti di AEM. Puoi estendere i passaggi del flusso di lavoro con parametri e script per fornire più funzionalità e controllo, in base alle esigenze. [!DNL AEM Forms] fornisce alcuni passaggi in aggiunta ai passaggi predefiniti di AEM. Per un elenco dettagliato dei passaggi di AEM e di [!DNL AEM Forms], consulta [Riferimento passaggio flusso di lavoro di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) e [Flusso di lavoro incentrato su Forms in OSGi - Riferimento passaggio](aem-forms-workflow.md).

AEM fornisce un’interfaccia utente intuitiva per creare un modello di flusso di lavoro utilizzando i passaggi di flusso di lavoro forniti. Per istruzioni dettagliate sulla creazione di un modello di flusso di lavoro, vedere [Creazione di modelli di flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows). L’esempio seguente fornisce istruzioni dettagliate per creare un modello di flusso di lavoro per un flusso di lavoro di approvazione e revisione:

>[!NOTE]
>
>Per creare o modificare un modello di flusso di lavoro è necessario essere membri del gruppo editor flusso di lavoro.

### Creare un modello per un flusso di lavoro di approvazione e revisione {#create-a-model-for-an-approval-and-review-workflow}

I flussi di lavoro di approvazione e revisione sono per le attività che richiedono l’intervento umano per prendere decisioni. L’esempio seguente crea un modello di flusso di lavoro per una richiesta di prestito ipotecario che deve essere compilata da un agente bancario di front-office. Una volta compilata, la domanda viene inviata per l’approvazione. Successivamente, la domanda approvata viene inviata al richiedente per le firme elettroniche utilizzando Adobe Sign.

L’esempio è disponibile come pacchetto allegato di seguito. Importa e installa l’esempio utilizzando Gestione pacchetti. Per creare manualmente il modello di flusso di lavoro per l&#39;applicazione, è inoltre possibile effettuare le operazioni riportate di seguito.

Nell&#39;esempio viene creato un modello di flusso di lavoro per una richiesta di mutuo che deve essere compilata da un agente bancario di front-office. Una volta compilata, la domanda viene inviata per l&#39;approvazione. Successivamente, l’applicazione approvata viene inviata al cliente per le firme elettroniche utilizzando Adobe Sign. Puoi importare e installare l’esempio utilizzando Gestione pacchetti.

[Ottieni il file](assets/example-mortgage-loan-application.zip)

1. Apri la console Modelli di flusso di lavoro. URL predefinito: `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Seleziona **Crea**, quindi **Crea modello**. Viene visualizzata la finestra di dialogo Aggiungi modello flusso di lavoro.
1. Immetti **Titolo** e **Nome** (facoltativo). Ad esempio, una richiesta di ipoteca. Seleziona **Fine**.
1. Seleziona il modello di flusso di lavoro creato e seleziona **Modifica**. Ora è possibile aggiungere passaggi del flusso di lavoro per creare una logica di business. La prima volta che crei un modello di flusso di lavoro, contiene:

   * I passaggi: Inizio flusso e Fine flusso. Questi passaggi rappresentano l’inizio e la fine del flusso di lavoro. Questi passaggi sono necessari e non possono essere modificati o rimossi.
   * Un esempio di passaggio Partecipante denominato Passaggio 1. Questo passaggio è configurato per assegnare un elemento di lavoro all’utente amministratore. Rimuovi questo passaggio.

1. Abilita le notifiche e-mail. Puoi configurare il flusso di lavoro incentrato su Forms su OSGi per inviare notifiche e-mail agli utenti o agli assegnatari. Per abilitare le notifiche e-mail, effettua le seguenti configurazioni:

   1. Passare a Gestione configurazione di AEM all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
   1. Apri la configurazione del servizio di posta CQ **[!UICONTROL Day]**. Specificare un valore per i campi **[!UICONTROL Nome host server SMTP]**, **[!UICONTROL Porta server SMTP]** e **[!UICONTROL &quot;Da&quot; indirizzo]**. Fai clic su **[!UICONTROL Salva]**.
   1. Apri la configurazione di **[!UICONTROL Day CQ Link Externalizer]**. Nel campo **[!UICONTROL Domini]**, specifica il nome host/indirizzo IP effettivo e il numero di porta per le istanze locali, di authoring e di pubblicazione. Fai clic su **[!UICONTROL Salva]**.

1. Creare fasi del flusso di lavoro. Un flusso di lavoro può avere più fasi. Questi passaggi vengono visualizzati nella casella in entrata di AEM e segnalano l’avanzamento del flusso di lavoro.

   Per definire una fase, seleziona l&#39;icona ![info-circle](assets/info-circle.png) per aprire le proprietà del modello di flusso di lavoro, apri la scheda **Fasi**, aggiungi le fasi per il modello di flusso di lavoro e seleziona **Salva e chiudi**. Nell&#39;esempio di richiesta di mutuo, creare fasi: richiesta di prestito, stato della richiesta di prestito, documenti da firmare e documento di prestito firmato.

1. Trascina e rilascia il browser passaggi **Assegna attività** al modello di flusso di lavoro. Rendete il primo passo del modello.

   Il componente Assegna attività assegna l’attività, creata da un flusso di lavoro, a un utente o a un gruppo. Oltre ad assegnare l’attività, puoi utilizzare il componente per specificare un Modulo adattivo o un PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e PDF non interattivo oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

   È inoltre possibile utilizzare il passaggio per controllare il comportamento dell&#39;attività. Ad esempio, la creazione di un documento di record automatico, l’assegnazione dell’attività a un utente o gruppo specifico, il percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Per informazioni dettagliate sulle opzioni del passaggio Assegna attività, consulta [Flusso di lavoro incentrato su Forms nel documento OSGi - Riferimento passaggio](aem-forms-workflow.md).

   ![workflow-editor](assets/workflow-editor.png)

   Per l’esempio di applicazione ipotecaria, configura la fase Assegna attività in modo che utilizzi un modulo adattivo di sola lettura e visualizzi il documento PDF una volta completata l’attività. Inoltre, seleziona un gruppo di utenti autorizzato ad approvare la richiesta di prestito. Nella scheda **Azioni**, disabilita l&#39;opzione **Invia**. Crea una variabile **actionTaken** di tipo di dati String e specifica la variabile come **Variabile route**. Ad esempio, actionTaken. Aggiungere inoltre le route di approvazione e rifiuto. I percorsi vengono visualizzati come azioni separate (pulsanti) nella casella in entrata di AEM. Il flusso di lavoro seleziona un ramo in base all’azione (pulsante) toccata da un utente.

   Puoi importare il pacchetto di esempio, disponibile per il download all’inizio della sezione, per il set completo di valori di tutti i campi della fase assegna attività configurata, ad esempio, applicazione ipotecaria.

1. Trascina il componente Divisione OR dal browser dei passaggi al modello di flusso di lavoro. La suddivisione OR crea una suddivisione nel flusso di lavoro, dopo la quale è attivo un solo ramo. Questo passaggio ti consente di introdurre nel flusso di lavoro i percorsi di elaborazione condizionale. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle esigenze.

   È possibile definire un&#39;espressione di indirizzamento per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

   Utilizza l’editor espressioni per creare espressioni di indirizzamento per Ramo 1 e Ramo 2. Queste espressioni di indirizzamento aiutano a scegliere un ramo in base all’azione dell’utente nella casella in entrata di AEM.

   **Espressione di routing per il ramo 1**

   Quando un utente tocca **Approva** nella casella in entrata di AEM, viene attivato il ramo 1.

   ![O Dividi esempio](assets/orsplit_branch1_active_new.png)

   **Espressione di routing per il ramo 2**

   Quando un utente tocca **Rifiuta** nella casella in entrata di AEM, viene attivato il Ramo 2.

   ![O Dividi esempio](assets/orsplit_branch2_active_new.png)

   Per informazioni sulla creazione di espressioni di routing tramite variabili, vedere [Variabili in [!DNL AEM Forms] flussi di lavoro](variable-in-aem-workflows.md).

1. Aggiungi altri passaggi del flusso di lavoro per creare la logica di business.

   Per l&#39;esempio del mutuo, aggiungere un documento di record di generazione, due passaggi dell&#39;attività di assegnazione e un passaggio del documento di firma al ramo 1 del modello, come illustrato nell&#39;immagine seguente. Un passaggio dell&#39;attività di assegnazione consiste nel visualizzare e inviare **documenti di prestito da firmare al candidato** e un altro componente dell&#39;attività di assegnazione è **per visualizzare documenti firmati**. Aggiungete inoltre un componente Assegna attività al ramo 2. Viene attivato quando un utente tocca Rifiuta nella casella in entrata di AEM.

   Per il set completo di valori di tutti i campi dei passaggi dell’attività di assegnazione, del passaggio del documento record e del passaggio del documento di firma configurati, ad esempio, per l’applicazione di un mutuo, importa il pacchetto di esempio, disponibile per il download all’inizio di questa sezione.

   Il modello di flusso di lavoro è pronto. Puoi avviare il flusso di lavoro attraverso vari metodi. Per ulteriori dettagli, vedere [Avviare un flusso di lavoro incentrato su Forms in OSGi](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## Creazione di un&#39;applicazione per flussi di lavoro incentrata su Forms {#create-a-forms-centric-workflow-application}

L’applicazione è il modulo adattivo associato al flusso di lavoro. Quando un’applicazione viene inviata tramite Casella in entrata, avvia il flusso di lavoro associato. Per rendere un flusso di lavoro Forms disponibile come applicazione nella Posta in arrivo di AEM e nell&#39;app [!DNL AEM Forms], eseguire le operazioni seguenti per creare un&#39;applicazione flusso di lavoro:

>[!NOTE]
>
>Per poter creare e gestire le applicazioni del flusso di lavoro è necessario essere membri del gruppo fd-administrator.

1. Nell&#39;istanza Autore AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gestisci applicazione flusso di lavoro]** e tocca **[!UICONTROL Crea]**.
1. Nella finestra Crea applicazione flusso di lavoro, fornisci gli input per i campi seguenti e tocca **Crea**. Viene creata una nuova applicazione, che viene elencata nella schermata Applicazioni flusso di lavoro.

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Il titolo è visibile nella casella in entrata di AEM e consente agli utenti di scegliere un’applicazione. Tienilo descrittivo. Ad esempio, l'applicazione di apertura dell'account di risparmio.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Specificare il nome dell'applicazione. Tutti i caratteri diversi da lettere, numeri, trattini e caratteri di sottolineatura vengono sostituiti da trattini. </td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>La descrizione è visibile nella casella in entrata di AEM. Fornisci informazioni dettagliate sull’applicazione nei campi di descrizione. Ad esempio, Scopo dell'applicazione.<br /> </td>
  </tr>
  <tr>
   <td>Modulo adattivo</td>
   <td><p>Specifica il percorso di un modulo adattivo. Quando un utente avvia un’applicazione, viene visualizzato il modulo adattivo specificato.</p> <p><strong>Nota</strong>: le applicazioni del flusso di lavoro non supportano moduli e documenti PDF di lunghezza superiore a una pagina o che richiedono lo scorrimento in Apple iPad. Quando un’applicazione viene aperta su Apple iPad e il modulo adattivo o il documento PDF è più lungo di una pagina, i campi modulo e il contenuto della seconda pagina vengono persi.</p> </td>
  </tr>
  <tr>
   <td>Gruppo di accesso</td>
   <td><p>Selezionare un gruppo. L’applicazione è visibile nella casella in entrata di AEM solo per i membri del gruppo selezionato. L'opzione gruppo di accesso rende disponibili per la selezione tutti i gruppi del gruppo [!DNL workflow-users]. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servizio preriempimento</td>
   <td>Seleziona un <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servizio di precompilazione</a> per il modulo adattivo.<br /> </td>
  </tr>
  <tr>
   <td>Modello flusso di lavoro</td>
   <td>Selezionare un <a href="aem-forms-workflow.md#create-a-workflow-model">modello flusso di lavoro</a> per l'applicazione. Un modello di flusso di lavoro è costituito dalla logica e dal flusso del processo aziendale. </td>
  </tr>
  <tr>
   <td>Percorso del file di dati</td>
   <td>Specifica il percorso del file di dati in crx-repository. Il percorso è relativo al payload del modulo adattivo e contiene il nome del file di dati. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso allegato</td>
   <td>Specifica il percorso della cartella degli allegati in crx-repository. Il percorso dell'allegato è relativo alla posizione del payload. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso del documento record</td>
   <td>Specifica il percorso del file del documento record nell’archivio crx. Il percorso è relativo alla posizione del payload del modulo adattivo. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Avviare un flusso di lavoro incentrato su Forms su OSGi {#launch}

Puoi avviare o attivare un flusso di lavoro incentrato su Forms:

* [Invio di un’applicazione dalla casella in entrata di AEM](#inbox)
* [Invio di un&#39;applicazione da [!DNL AEM Forms] App](#afa)

* [Invio di un modulo adattivo](#af)
* [Utilizzo della cartella controllata](#watched)

* [Invio di una comunicazione interattiva o di una lettera](#letter)

### Invio di un’applicazione dalla casella in entrata di AEM {#inbox}

L&#39;applicazione del flusso di lavoro creata è disponibile come applicazione nella cartella Posta in arrivo. Gli utenti membri del gruppo [!DNL workflow-users] possono compilare e inviare l&#39;applicazione che attiva il flusso di lavoro associato.

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and lets you change the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### Invio di un modulo adattivo {#af}

Puoi configurare le azioni di invio di un modulo adattivo in modo da avviare un flusso di lavoro al momento dell’invio del modulo adattivo. Forms adattivo fornisce l&#39;azione di invio **Richiama un flusso di lavoro AEM** per avviare un flusso di lavoro all&#39;invio di un modulo adattivo. Per informazioni dettagliate sull&#39;azione Invia, vedere [Configurazione dell&#39;azione Invia](configuring-submit-actions.md). Per inviare un modulo adattivo tramite l&#39;app [!DNL AEM Forms], abilita l&#39;app Sincronizza con [!DNL AEM Forms] nelle proprietà del modulo adattivo.

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Select **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Select **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### Rimuovi istanze flusso di lavoro {#purge-workflow-instances}

La riduzione al minimo del numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione. Per informazioni dettagliate, vedi [Rimozione regolare delle istanze del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=it) eliminazione delle istanze del flusso di lavoro
