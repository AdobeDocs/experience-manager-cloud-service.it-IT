---
title: Flusso di lavoro incentrato su Forms su OSGi
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Utilizzo [!DNL AEM Forms] Flusso di lavoro per automatizzare e creare rapidamente revisioni e approvazioni, per avviare document services
seo-description: Use [!DNL AEM Forms] Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 1%

---


# Flusso di lavoro incentrato su Forms su OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

Le aziende raccolgono dati da centinaia e migliaia di moduli, da diversi sistemi back-end e da fonti di dati online o offline. Hanno anche un set dinamico di utenti per prendere decisioni sui dati, il che implica processi di revisione e approvazione iterativi.

Oltre ai flussi di lavoro di revisione e approvazione per il pubblico interno ed esterno, le grandi organizzazioni e aziende hanno attività ripetitive. Ad esempio, la conversione di un documento PDF in un altro formato. Una volta eseguite manualmente, queste attività richiedono molto tempo e risorse. Le aziende hanno inoltre i requisiti legali necessari per firmare digitalmente un documento e archiviare i dati del modulo in modo da utilizzarli in formati predefiniti.

## Introduzione al flusso di lavoro Forms-centric su OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puoi utilizzare flussi di lavoro AEM per creare rapidamente flussi di lavoro basati su Forms adattivi. Questi flussi di lavoro possono essere utilizzati per la revisione e le approvazioni, per i flussi dei processi aziendali, per avviare document services, per l’integrazione con il flusso di lavoro della firma Adobe Sign e per operazioni simili. Ad esempio, l&#39;elaborazione delle applicazioni con carta di credito, il dipendente lascia i flussi di lavoro di approvazione, salvando un modulo come documento PDF. Inoltre, questi flussi di lavoro possono essere utilizzati all&#39;interno di un&#39;organizzazione o attraverso un firewall di rete.

Con il flusso di lavoro Forms-centric su OSGi, puoi creare e distribuire rapidamente flussi di lavoro per varie attività sullo stack OSGi, senza dover installare la funzionalità di Process Management completa sullo stack JEE. Lo sviluppo e la gestione dei flussi di lavoro utilizzano le funzionalità familiari AEM Workflow e AEM Inbox. I flussi di lavoro costituiscono la base per automatizzare i processi aziendali reali che si estendono su più sistemi software, reti, reparti e persino organizzazioni.

Una volta configurati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o eseguiti a livello di programmazione quando gli utenti inviano un modulo <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

Workflow Forms-centric su OSGi estende [Casella in entrata AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) e fornisce componenti aggiuntivi (passaggi) per AEM editor di flussi di lavoro per aggiungere supporto per [!DNL AEM Forms]Flussi di lavoro incentrati. <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

Tutto [!DNL AEM Forms] i passaggi del flusso di lavoro supportano l’utilizzo di variabili. Le variabili consentono ai passaggi del flusso di lavoro di conservare e trasmettere i metadati tra i passaggi in fase di runtime. Puoi creare diversi tipi di variabili per memorizzare diversi tipi di dati. È inoltre possibile creare raccolte di variabili (array) per memorizzare più istanze di dati correlati con lo stesso tipo. In genere, si utilizza una variabile o una raccolta di variabili quando è necessario prendere una decisione in base al valore che contiene o per memorizzare le informazioni necessarie in un secondo momento in un processo. Per ulteriori informazioni sull’utilizzo delle variabili nei componenti del flusso di lavoro incentrati su Forms (passaggi), consulta [Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato](aem-forms-workflow-step-reference.md). Per informazioni sulla creazione e la gestione delle variabili, consulta [Variabili nei flussi di lavoro AEM](variable-in-aem-workflows.md).

Il diagramma seguente illustra la procedura end-to-end per creare, eseguire e monitorare un flusso di lavoro incentrato su Forms su OSGi.

![introduzione ad aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Prima di iniziare {#before-you-start}

* Un flusso di lavoro è una rappresentazione di un processo aziendale reale. Prepara il tuo processo aziendale e l&#39;elenco dei partecipanti al processo aziendale. Inoltre, tieni il materiale collaterale (Forms adattivo, documenti PDF e altro ancora) pronto prima di iniziare a creare un flusso di lavoro.
* Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM e consentono di segnalare l’avanzamento del flusso di lavoro. Dividi il tuo processo aziendale in fasi logiche.
* Puoi configurare la fase di assegnazione dell’attività dei flussi di lavoro AEM per inviare notifiche e-mail agli utenti o agli assegnatari. Quindi, [abilitare le notifiche e-mail](#configure-email-service).
* Un flusso di lavoro può inoltre utilizzare il segno Adobe per le firme digitali. Se prevedi di utilizzare Adobe Sign in un flusso di lavoro, la [configurare Adobe Sign per [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) prima di utilizzarlo in un flusso di lavoro.

## Creare un modello di flusso di lavoro {#create-a-workflow-model}

Un modello di flusso di lavoro è costituito dalla logica e dal flusso di un processo aziendale. È costituito da una serie di passi. Questi passaggi sono componenti AEM. Puoi estendere i passaggi del flusso di lavoro con parametri e script per fornire ulteriori funzionalità e controlli, a seconda delle necessità. [!DNL AEM Forms] fornisce alcuni passaggi oltre a AEM passaggi disponibili. Per un elenco dettagliato dei AEM e [!DNL AEM Forms] passaggi, vedi [Riferimento dettagliato sui flussi di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) e [Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato](aem-forms-workflow.md).

AEM fornisce un’interfaccia utente intuitiva per creare un modello di flusso di lavoro utilizzando i passaggi del flusso di lavoro forniti. Per istruzioni dettagliate sulla creazione di un modello di flusso di lavoro, consulta [Creazione di modelli di flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows). L&#39;esempio seguente fornisce istruzioni passo passo per creare un modello di flusso di lavoro per un flusso di lavoro di approvazione e revisione:

>[!NOTE]
>
>Per creare o modificare un modello di flusso di lavoro, devi essere membro del gruppo editor-flussi di lavoro.

### Creare un modello per un flusso di lavoro di approvazione e revisione {#create-a-model-for-an-approval-and-review-workflow}

Il flusso di lavoro di approvazione e revisione riguarda i compiti che richiedono l&#39;intervento umano per prendere decisioni. Nell&#39;esempio seguente viene creato un modello di flusso di lavoro per un&#39;applicazione di mutui ipotecari che deve essere compilata da un agente bancario di front-office. Una volta compilata, la domanda viene inviata per l&#39;approvazione. Successivamente, la domanda approvata viene inviata al richiedente la firma elettronica utilizzando Adobe Sign.

L’esempio è disponibile come pacchetto allegato di seguito. Importa e installa l&#39;esempio utilizzando il gestore di pacchetti. Puoi anche eseguire i seguenti passaggi per creare manualmente il modello di flusso di lavoro per l’applicazione:

Nell&#39;esempio viene creato un modello di flusso di lavoro un&#39;applicazione mutuo che deve essere compilata da un agente bancario front-office. Una volta compilata la domanda viene inviata per l&#39;approvazione. Successivamente, l&#39;applicazione approvata viene inviata al cliente per le firme elettroniche che utilizzano Adobe Sign. Puoi importare e installare l’esempio utilizzando il gestore dei pacchetti.

[Ottieni file](assets/example-mortgage-loan-application.zip)

1. Apri la console Modelli di flusso di lavoro . L’URL predefinito è `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Seleziona **Crea**, quindi **Crea modello**. Viene visualizzata la finestra di dialogo Aggiungi modello flusso di lavoro.
1. Inserisci il **Titolo** e **Nome** (facoltativo). Ad esempio, un&#39;applicazione ipotecaria. Toccate **Chiudi**.
1. Seleziona il modello di flusso di lavoro appena creato e tocca **Modifica**. Ora puoi aggiungere passaggi del flusso di lavoro per creare una logica di business. Quando crei un modello di flusso di lavoro per la prima volta, questo contiene:

   * I passaggi: Inizio flusso e Fine flusso. Questi passaggi rappresentano l’inizio e la fine del flusso di lavoro. Questi passaggi sono obbligatori e non possono essere modificati o rimossi.
   * Esempio di passaggio partecipante denominato Passaggio 1. Questo passaggio è configurato per assegnare un elemento di lavoro all’utente amministratore. Rimuovi questo passaggio.

1. Abilitare le notifiche e-mail. Puoi configurare un flusso di lavoro Forms-centric su OSGi per inviare notifiche e-mail agli utenti o agli assegnatari. Esegui le seguenti configurazioni per abilitare le notifiche e-mail:

   1. Vai a AEM gestione della configurazione all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
   1. Apri **[!UICONTROL Servizio e-mail Day CQ]** configurazione. Specifica un valore per **[!UICONTROL Nome host server SMTP]**, **[!UICONTROL porta server SMTP,]** e **[!UICONTROL Indirizzo &quot;Da&quot;]** campi. Fai clic su **[!UICONTROL Salva]**.
   1. Apri **[!UICONTROL Day CQ Link Externalizer]** configurazione. In **[!UICONTROL Domini]** Specifica l’indirizzo IP o nome host effettivo e il numero di porta per le istanze locali, di authoring e di pubblicazione. Fai clic su **[!UICONTROL Salva]**.

1. Crea fasi del flusso di lavoro. Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM e segnalano l’avanzamento del flusso di lavoro.

   Per definire un’area di visualizzazione, tocca ![info-cerchio](assets/info-circle.png) per aprire le proprietà del modello di flusso di lavoro, apri **Fasi** scheda , aggiungi aree di visualizzazione per il modello di flusso di lavoro e tocca **Salva e chiudi**. Per l&#39;esempio di applicazione ipotecaria, creare le fasi: richiesta di prestito, stato della richiesta di prestito, documenti da firmare e documento di prestito firmato.

1. Trascina e rilascia la **Assegna attività** passa il browser al modello di flusso di lavoro. Impostalo come primo passo del modello.

   Il componente Assegnazione attività assegna l’attività, creata dal flusso di lavoro, a un utente o a un gruppo. Oltre ad assegnare l’attività, è possibile utilizzare il componente per specificare un Modulo adattivo o un PDF non interattivo per l’attività. Il Modulo adattivo è necessario per accettare l’input degli utenti e PDF non interattivo o un Modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di revisione.

   È inoltre possibile utilizzare il passaggio per controllare il comportamento dell’attività. Ad esempio, per creare un documento di record automatico, assegnare l&#39;attività a un utente o a un gruppo specifico, il percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Per informazioni dettagliate sulle opzioni della fase di assegnazione delle attività, vedere [Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato](aem-forms-workflow.md) documento.

   ![editor di workflow](assets/workflow-editor.png)

   Per l’esempio di applicazione del mutuo, configurare il passaggio dell’attività di assegnazione in modo da utilizzare un modulo adattivo di sola lettura e visualizzare un documento PDF una volta completata l’attività. Inoltre, selezionare il gruppo utenti autorizzato ad approvare la richiesta di prestito. Sulla **Azioni** disabilita **Invia** opzione . Crea un **actionTaken** variabile del tipo di dati String e specifica la variabile come **Variabile di percorso**. Ad esempio, actionTaken. Inoltre, aggiungere le route Approva e Rifiuta. Le route vengono visualizzate come azioni separate (pulsanti) nella casella in entrata AEM. Il flusso di lavoro seleziona un ramo in base all’azione (pulsante) che un utente tocca.

   È possibile importare il pacchetto di esempio, disponibile per il download all&#39;inizio della sezione, per l&#39;insieme completo di valori di tutti i campi della fase di assegnazione delle attività configurate, ad esempio l&#39;applicazione mutuo.

1. Trascina il componente O diviso dal browser dei passaggi al modello di flusso di lavoro. La divisione OR crea una suddivisione nel flusso di lavoro, dopodiché è attivo un solo ramo. Questo passaggio ti consente di introdurre i percorsi di elaborazione condizionale nel flusso di lavoro. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle tue esigenze.

   È possibile definire l&#39;espressione di indirizzamento per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

   Utilizzare l&#39;editor espressioni per creare espressioni di indirizzamento per Branch 1 e Branch 2. Queste espressioni di indirizzamento consentono di scegliere un ramo in base all&#39;azione dell&#39;utente in AEM casella in entrata.

   **Espressione di routing per il ramo 1**

   Quando un utente tocca **Approva** in AEM casella in entrata viene attivato il ramo 1.

   ![Esempio di divisione OR](assets/orsplit_branch1_active_new.png)

   **Espressione di routing per il ramo 2**

   Quando un utente tocca **Rifiuta** in AEM casella in entrata viene attivato il ramo 2.

   ![Esempio di divisione OR](assets/orsplit_branch2_active_new.png)

   Per informazioni sulla creazione di espressioni di indirizzamento utilizzando le variabili, consulta [Variabili in [!DNL AEM Forms] workflow](variable-in-aem-workflows.md).

1. Aggiungi altri passaggi del flusso di lavoro per generare la logica di business.

   Per l&#39;esempio di ipoteca, aggiungere un documento generato di record, due fasi di task di assegnazione e un passo documento di segno al ramo 1 del modello, come illustrato nell&#39;immagine seguente. Una fase dell&#39;attività di assegnazione consiste nel visualizzare e inviare **da firmare al richiedente** e un altro componente dell’attività di assegnazione è **visualizzazione di documenti firmati**. Inoltre, aggiungi un componente task assegnato al ramo 2. Viene attivato quando un utente tocca Rifiuta nella casella in entrata AEM.

   Per l&#39;insieme completo di valori di tutti i campi dei passaggi dell&#39;attività di assegnazione, del passaggio Documento di record e del passaggio del documento di firma configurato per esempio applicazione di ipoteca, importare il pacchetto di esempio, disponibile per il download all&#39;inizio di questa sezione.

   Il modello di flusso di lavoro è pronto. Puoi avviare il flusso di lavoro attraverso vari metodi. Per maggiori dettagli, vedi [Avvia un flusso di lavoro incentrato su Forms su OSGi](#launch).

   ![workflow-editor-mutui](assets/workflow-editor-mortgage.png)

## Creare un’applicazione per flussi di lavoro incentrata su Forms {#create-a-forms-centric-workflow-application}

L’applicazione è il Modulo adattivo associato al flusso di lavoro. Quando un&#39;applicazione viene inviata tramite Posta in arrivo, avvia il flusso di lavoro associato. Per rendere disponibile un flusso di lavoro Forms come applicazione in AEM Posta in arrivo e [!DNL AEM Forms] Per creare un’applicazione di flusso di lavoro, procedi come segue:

>[!NOTE]
>
>È necessario essere membri del gruppo fd-administrator per poter creare e gestire le applicazioni del flusso di lavoro.

1. Nell’istanza di authoring di AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gestisci applicazione flusso di lavoro]** e tocco **[!UICONTROL Crea]**.
1. Nella finestra Crea applicazione flusso di lavoro, fornisci gli input per i campi seguenti e tocca **Crea**. Viene creata una nuova applicazione ed è elencata nella schermata Applicazioni flusso di lavoro .

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Il titolo è visibile AEM casella in entrata e consente agli utenti di scegliere un’applicazione. Tenetela descrittiva. Ad esempio, Salvataggio dell'applicazione di apertura dell'account.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Specifica il nome dell'applicazione. Tutti i caratteri diversi da alfabeti, numeri, trattini e caratteri di sottolineatura vengono sostituiti con trattini. </td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>La descrizione è visibile AEM casella in entrata. Fornisci informazioni dettagliate sull’applicazione nei campi di descrizione. Ad esempio, Scopo dell'applicazione.<br /> </td>
  </tr>
  <tr>
   <td>Modulo adattivo</td>
   <td><p>Specifica il percorso di un modulo adattivo. Quando un utente avvia un'applicazione, viene visualizzato il modulo adattivo specificato.</p> <p><strong>Nota</strong>: Le applicazioni per flussi di lavoro non supportano moduli e documenti PDF che hanno più pagine o richiedono lo scorrimento su Apple iPad. Quando un’applicazione viene aperta in Apple iPad e il modulo adattivo o il documento PDF è più lungo di una pagina, i campi modulo e il contenuto della seconda pagina vengono persi.</p> </td>
  </tr>
  <tr>
   <td>Gruppo di accesso</td>
   <td><p>Seleziona un gruppo. L'applicazione è visibile AEM casella in entrata solo ai membri del gruppo selezionato. L'opzione gruppo di accesso rende tutti i gruppi del [!DNL workflow-users] gruppo disponibile per la selezione. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servizio preriempimento</td>
   <td>Seleziona una <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servizio di precompilazione</a> per il modulo adattivo.<br /> </td>
  </tr>
  <tr>
   <td>Modello flusso di lavoro</td>
   <td>Seleziona una <a href="aem-forms-workflow.md#create-a-workflow-model">modello di flusso di lavoro</a> per la domanda. Un modello di flusso di lavoro è costituito dalla logica e dal flusso del processo aziendale. </td>
  </tr>
  <tr>
   <td>Percorso del file di dati</td>
   <td>Specifica il percorso del file di dati in crx-repository. Il percorso è relativo al payload del modulo adattivo e contiene il nome del file di dati. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso allegato</td>
   <td>Specifica il percorso della cartella degli allegati in crx-repository. Il percorso allegato è relativo alla posizione del payload. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso del documento record</td>
   <td>Specifica il percorso del file del documento di record in crx-repository. Il percorso è relativo alla posizione del payload del modulo adattivo. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Avvia un flusso di lavoro incentrato su Forms su OSGi {#launch}

Puoi avviare o attivare un flusso di lavoro incentrato su Forms:

* [Invio di un’applicazione da AEM casella in entrata](#inbox)
* [Invio di una domanda da [!DNL AEM Forms] App](#afa)

* [Invio di un modulo adattivo](#af)
* [Utilizzo della cartella controllata](#watched)

* [Invio di una comunicazione interattiva o di una lettera](#letter)

### Invio di un’applicazione da AEM casella in entrata {#inbox}

L’applicazione del flusso di lavoro creata è disponibile come applicazione nella casella in entrata. Utenti membri di [!DNL workflow-users] può compilare e inviare l’applicazione che attiva il flusso di lavoro associato. Per informazioni sull&#39;utilizzo di AEM Posta in arrivo per inviare le applicazioni e gestire le attività, vedere [Gestione di applicazioni e attività Forms nella casella in entrata AEM](manage-applications-inbox.md).

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and allows you to make changes to the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### Invio di un modulo adattivo {#af}

È possibile configurare le azioni di invio di un modulo adattivo per avviare un flusso di lavoro all’invio del modulo adattivo. La funzione Forms adattiva fornisce **Richiamare un flusso di lavoro AEM** Invia azione per avviare un flusso di lavoro dopo l’invio di un modulo adattivo. Per informazioni dettagliate sull’azione di invio, vedere [Configurazione dell’azione Invia](configuring-submit-actions.md). Invio di un modulo adattivo tramite [!DNL AEM Forms] app, abilita Sincronizza con [!DNL AEM Forms] App nelle proprietà del modulo adattivo.

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Tap **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

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

1. Tap **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

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
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### Eliminare le istanze del flusso di lavoro {#purge-workflow-instances}

Minimizzare il numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione. Per informazioni dettagliate, consulta [Rimozione regolare delle istanze del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html) eliminazione delle istanze del flusso di lavoro
