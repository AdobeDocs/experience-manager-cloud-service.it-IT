---
title: Come configurare un’azione di invio per un modulo adattivo
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. È possibile utilizzare le azioni di invio integrate o crearne una personalizzata.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 6a124b476b4dd18ea38d35438866a07958918461
workflow-type: tm+mt
source-wordcount: '3131'
ht-degree: 1%

---

# Azione di invio di moduli adattivi {#configuring-the-submit-action}

Un’azione di invio viene attivata quando un utente fa clic sul pulsante **[!UICONTROL Invia]** su un modulo adattivo. Adaptive Forms fornisce alcune azioni di invio pronte all&#39;uso. Le azioni di invio disponibili sono:

* [Invia all’endpoint REST](#submit-to-rest-endpoint)
* [Invia e-mail](#send-email)
* [Invia usando il modello dati modulo](#submit-using-form-data-model)
* [Richiamare un flusso di lavoro AEM](#invoke-an-aem-workflow)
* [Invia a SharePoint](#submit-to-sharedrive)
* [Invia a OneDrive](#submit-to-onedrive)
* [Invia ad Azure Blob Storage](#azure-blob-storage)

È inoltre possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un’azione di invio personalizzata.

Puoi configurare un’azione di invio nella **[!UICONTROL Invio]** della sezione delle proprietà del contenitore di moduli adattivi, nella barra laterale.

![Configurare l’azione Invia](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.


-->

## Invia all’endpoint REST {#submit-to-rest-endpoint}

Utilizza la **[!UICONTROL Invia a endpoint REST]** per inviare i dati inviati a un URL rimanente. L’URL può essere di un server interno (il server su cui viene eseguito il rendering del modulo) o di un server esterno.

Per inviare dati a un server interno, fornisci il percorso della risorsa. I dati vengono inviati nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste post, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per inviare dati a un server esterno, specifica un URL. Il formato dell’URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mappatura dei valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell’esempio precedente, l’utente ha immesso informazioni in `textbox` viene acquisito utilizzando il parametro `param1`. Sintassi per la registrazione dei dati acquisiti tramite `param1` è:

`String data=request.getParameter("param1");`

Analogamente, i parametri utilizzati per la registrazione di dati XML e allegati sono `dataXml` e `attachments`.

Ad esempio, è possibile utilizzare questi due parametri nello script per analizzare i dati in un punto finale residuo. Utilizza la sintassi seguente per memorizzare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio, `data` memorizza i dati XML e `att` memorizza i dati degli allegati.

La **[!UICONTROL Invia all’endpoint REST]** Invia azione invia i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con i valori copiati dal **casella di testo** e **casella numerica** campi per l’azione successiva.

![Configurazione dell&#39;azione di invio dell&#39;endpoint rimanente](assets/action-config.png)

È inoltre possibile **[!UICONTROL Abilita richiesta POST]** e fornire un URL per inviare la richiesta. Per inviare dati al server AEM che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso principale del server AEM. Esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare un percorso assoluto.

>[!NOTE]
>
>Per trasmettere i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

## Invia e-mail {#send-email}

È possibile utilizzare **[!UICONTROL Invia e-mail]** Invia azione per inviare un’e-mail a uno o più destinatari dopo l’invio corretto del modulo. L’e-mail generata può contenere dati del modulo in un formato predefinito. Ad esempio, nel modello seguente, il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviati.

    &quot;
    
    Hi ${customer_Name},
    
    Il seguente è impostato come indirizzo di spedizione predefinito:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Cordiali saluti,
    WKND
    
    &quot;

>[!NOTE]
>
> * Tutti i campi del modulo devono avere nomi di elementi diversi, anche se si trovano su pannelli diversi di un modulo adattivo.
> * AEM as a Cloud Service richiede che la posta in uscita sia crittografata. Per impostazione predefinita, le e-mail in uscita sono disabilitate. Per attivarlo, invia un ticket di supporto a [Richiesta di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


È inoltre possibile includere allegati e un documento di record (DoR) nell’e-mail. Per abilitare **[!UICONTROL Allega documento di registrazione]** configurare il modulo adattivo per generare un documento di record (DoR). È possibile abilitare l’opzione per generare un documento di record dalle proprietà Modulo adattivo.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Invia usando il modello dati modulo {#submit-using-form-data-model}

La **[!UICONTROL Invia utilizzando il modello dati del modulo]** L’azione di invio scrive i dati del modulo adattivo inviati per l’oggetto modello dati specificato in un modello dati modulo nella relativa origine dati. Durante la configurazione dell’azione di invio, è possibile scegliere un oggetto modello dati di cui si desidera riscrivere i dati inviati nella relativa origine dati.

Inoltre, è possibile inviare all’origine dati un allegato del modulo utilizzando un modello dati modulo e un documento di record. Per informazioni sul modello dati del modulo, consultare [[!DNL AEM Forms] Integrazione dei dati](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Richiamare un flusso di lavoro AEM {#invoke-an-aem-workflow}

La **[!UICONTROL Richiamare un flusso di lavoro AEM]** Invia azione associa un modulo adattivo a un [Flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza di authoring. È possibile salvare il file di dati, gli allegati e il documento di record nella posizione di payload del flusso di lavoro o in una variabile. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni e configurato per un archivio dati esterno, è disponibile solo l’opzione variabile . Puoi selezionare dall’elenco delle variabili disponibili per il modello di flusso di lavoro. Se il flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni in una fase successiva e non al momento della creazione del flusso di lavoro, assicurati che siano presenti le configurazioni delle variabili richieste.

L’azione Invia inserisce quanto segue nel percorso di payload del flusso di lavoro o nella variabile se il flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni:

* **File di dati**: Contiene i dati inviati al modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso file dati]** per specificare il nome del file e il percorso del file relativo al payload. Ad esempio, il `/addresschange/data.xml` crea una cartella denominata `addresschange` e lo posiziona rispetto al carico utile. Puoi anche specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni, utilizza l’opzione variabile e seleziona la variabile dall’elenco delle variabili disponibili per il modello di flusso di lavoro.

* **Allegati**: È possibile utilizzare **[!UICONTROL Percorso allegato]** opzione per specificare il nome della cartella in cui memorizzare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni, utilizza l’opzione variabile e seleziona la variabile dall’elenco delle variabili disponibili per il modello di flusso di lavoro.

* **Documento di registrazione**: Contiene il documento di record generato per il modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso del documento di registrazione]** per specificare il nome del file del documento di record e il percorso del file relativo al payload. Ad esempio, il `/addresschange/DoR.pdf` crea una cartella denominata `addresschange` relativo al payload e inserisce il `DoR.pdf` relativo al payload. Puoi anche specificare solo `DoR.pdf` per salvare solo il documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione dei dati esterni, utilizza l’opzione variabile e seleziona la variabile dall’elenco delle variabili disponibili per il modello di flusso di lavoro.

Prima di utilizzare **[!UICONTROL Richiamare un flusso di lavoro AEM]** Invia azione configura quanto segue per **[!UICONTROL Servizio impostazioni di DS AEM]** configurazione:

* **[!UICONTROL URL server di elaborazione]**: Il server di elaborazione è il server in cui viene attivato il flusso di lavoro Forms o AEM. Può essere lo stesso dell’URL dell’istanza di authoring AEM o di un altro server.

* **[!UICONTROL Nome utente del server di elaborazione]**: Nome utente dell’utente del flusso di lavoro

* **[!UICONTROL Password server di elaborazione]**: Password utente del flusso di lavoro

## Invia a SharePoint {#submit-to-sharedrive}

La **[!UICONTROL Invia a SharePoint]** L’azione di invio collega un modulo adattivo a un archivio Microsoft SharePoint. È possibile inviare il file di dati del modulo, gli allegati o il documento di record alla Microsoft Sharepoint Storage connessa. Per utilizzare **[!UICONTROL Invia a SharePoint]** Invia azione in un modulo adattivo:

1. [Creare una configurazione SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): Collega AEM Forms al tuo Microsoft Sharepoint Storage.
2. [Utilizzare l’azione Invia a SharePoint in un modulo adattivo](#use-sharepoint-configuartion-in-af): Collega il modulo adattivo a Microsoft SharePoint configurato.

### Creare una configurazione SharePoint {#create-sharepoint-configuration}

Per collegare AEM Forms al tuo Microsoft Sharepoint Storage:

1. Vai al tuo **Autore di AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft SharePoint]**.
1. Una volta selezionato il **[!UICONTROL Microsoft SharePoint]**, viene reindirizzato a **[!UICONTROL Browser SharePoint]**.
1. Seleziona una **Contenitore di configurazione**. La configurazione viene memorizzata nel contenitore di configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata di configurazione di SharePoint.
   ![Configurazione di Sharepoint](/help/forms/assets/sharepoint_configuration.png)
1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l’ID client, il segreto client e l’ID tenant per l’URL OAuth, consulta [Documentazione di Microsoft](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * È possibile recuperare `Client ID` e `Client Secret` dell’app dal portale Microsoft Azure.
   * Nel portale Microsoft Azure, aggiungi l’URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l’URL dell’istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` per fornire autorizzazioni di lettura/scrittura.
   * Utilizza URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell’app dal portale Microsoft Azure.

   >[!NOTE]
   >
   > La **segreto client** Il campo è obbligatorio o facoltativo dipende dalla configurazione dell’applicazione Azure Active Directory. Se l&#39;applicazione configurata per l&#39;utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. In caso di connessione riuscita, il `Connection Successful` viene visualizzato un messaggio.

1. Ora, seleziona **Sito SharePoint** > **Raccolta documenti** > **Cartella SharePoint**, per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel sito SharePoint selezionato.
   >* Crea una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente nel `Documents` libreria del sito SharePoint selezionato facendo clic su **Crea cartella**.


Ora è possibile utilizzare questa configurazione di SharePoint Sites per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione SharePoint in un modulo adattivo {#use-sharepoint-configuartion-in-af}

È possibile utilizzare la configurazione SharePoint creata in un modulo adattivo per salvare i dati o il documento di record generato in una cartella SharePoint. Esegui i seguenti passaggi per utilizzare una configurazione di archiviazione SharePoint in un modulo adattivo come:
1. Crea un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore di configurazione] per un modulo adattivo, in cui è stato creato lo storage SharePoint.
   > * Se no [!UICONTROL Contenitore di configurazione] viene selezionato, quindi il valore globale [!UICONTROL Configurazione dell&#39;archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell’azione di invio.


1. Seleziona **Invia azione** come **[!UICONTROL Invia a SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Seleziona la **[!UICONTROL Configurazione dell&#39;archiviazione]**, in cui salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell’archivio Microsoft Sharepoint specificato.
La struttura della cartella per salvare i dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Invia a OneDrive {#submit-to-onedrive}

La **[!UICONTROL Invia a OneDrive]** L’azione di invio collega un modulo adattivo a Microsoft OneDrive. È possibile inviare i dati del modulo, i file, gli allegati o il documento di record all&#39;archivio Microsoft OneDrive collegato. Per utilizzare [!UICONTROL Invia a OneDrive] Invia azione in un modulo adattivo:

1. [Creare una configurazione OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): Collega AEM Forms al tuo Microsoft OneDrive Storage.
2. [Utilizzare l’azione Invia a OneDrive in un modulo adattivo](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Collega il modulo adattivo a Microsoft OneDrive configurato.

### Creare una configurazione OneDrive {#create-onedrice-configuration}

Per collegare AEM Forms al tuo Microsoft OneDrive Storage:

1. Vai al tuo **Autore di AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft OneDrive]**.
1. Una volta selezionato il **[!UICONTROL Microsoft OneDrive]**, viene reindirizzato a **[!UICONTROL Browser OneDrive]**.
1. Seleziona una **Contenitore di configurazione**. La configurazione viene memorizzata nel contenitore di configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata di configurazione di OneDrive.

   ![Schermata Configurazione di OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l’ID client, il segreto client e l’ID tenant per l’URL OAuth, consulta [Documentazione di Microsoft](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * È possibile recuperare `Client ID` e `Client Secret` dell’app dal portale Microsoft Azure.
   * Nel portale Microsoft Azure, aggiungi l’URI di reindirizzamento come `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l’URL dell’istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Files.ReadWrite.All` per fornire autorizzazioni di lettura/scrittura.
   * Utilizza URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell’app dal portale Microsoft Azure.

   >[!NOTE]
   >
   > La **segreto client** Il campo è obbligatorio o facoltativo dipende dalla configurazione dell’applicazione Azure Active Directory. Se l&#39;applicazione configurata per l&#39;utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. In caso di connessione riuscita, il `Connection Successful` viene visualizzato un messaggio.

1. Ora, seleziona **[!UICONTROL Contenitore OneDrive]** > **[Cartella OneDrive]**  per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente in Contenitore OneDrive.
   > * Crea una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non è già presente facendo clic su **Crea cartella**.


Ora è possibile utilizzare questa configurazione di archiviazione OneDrive per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione di OneDrive in un modulo adattivo {#use-onedrive-configuartion-in-af}

È possibile utilizzare la configurazione di archiviazione OneDrive creata in un modulo adattivo per salvare i dati o il documento di record generato in una cartella OneDrive. Esegui i seguenti passaggi per utilizzare la configurazione di archiviazione OneDrive in un modulo adattivo come:
1. Crea un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore di configurazione] per un modulo adattivo, in cui è stato creato l&#39;archivio OneDrive.
   > * Se no [!UICONTROL Contenitore di configurazione] viene selezionato, quindi il valore globale [!UICONTROL Configurazione dell&#39;archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell’azione di invio.


1. Seleziona **Invia azione** come **[!UICONTROL Invia a OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. Seleziona la **[!UICONTROL Configurazione dell&#39;archiviazione]**, in cui salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio Microsoft OneDrive specificato.
La struttura della cartella per salvare i dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Invia ad Azure Blob Storage {#submit-to-azure-blob-storage}

La **[!UICONTROL Invia ad Azure Blob Storage]**  L’azione Invia collega un modulo adattivo a un portale Microsoft Azure. È possibile inviare i dati del modulo, il file, gli allegati o il documento di record ai contenitori Archiviazione di Azure collegati. Per utilizzare l’azione Invia per Azure Blob Storage:

1. [Creare un contenitore di archiviazione BLOB di Azure](#create-a-azure-blob-storage-container-create-azure-configuration): Collega AEM Forms ai contenitori di archiviazione di Azure.
2. [Utilizzare la configurazione di archiviazione di Azure in un modulo adattivo ](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): Collega il modulo adattivo ai contenitori di archiviazione di Azure configurati.

### Creare un contenitore di archiviazione BLOB di Azure {#create-azure-configuration}

Per collegare AEM Forms ai contenitori di archiviazione di Azure:
1. Vai al tuo **Autore di AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Archiviazione di Azure]**.
1. Una volta selezionato il **[!UICONTROL Archiviazione di Azure]**, viene reindirizzato a **[!UICONTROL Browser di archiviazione di Azure]**.
1. Seleziona una **Contenitore di configurazione**. La configurazione viene memorizzata nel contenitore di configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata Crea configurazione di archiviazione di Azure.

   ![Configurazione archiviazione Azure](/help/forms/assets/azure-storage-configuration.png)

1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL Account di archiviazione di Azure]** e **[!UICONTROL Chiave di accesso di Azure]**.

   * È possibile recuperare `Azure Storage Account` nome e `Azure Access key` dagli account di archiviazione nel portale Microsoft Azure.

1. Fai clic su **[!UICONTROL Salva]**.

Ora è possibile utilizzare questa configurazione del contenitore di archiviazione di Azure per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione di archiviazione di Azure in un modulo adattivo {#use-azure-storage-configuartion-in-af}

È possibile utilizzare la configurazione del contenitore Archiviazione di Azure creata in un modulo adattivo per salvare i dati o il documento di record generato nel contenitore Archiviazione di Azure. Esegui i seguenti passaggi per utilizzare la configurazione del contenitore di archiviazione di Azure in un modulo adattivo come:
1. Crea un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore di configurazione] per un modulo adattivo, in cui è stato creato l&#39;archivio OneDrive.
   > * Se no [!UICONTROL Contenitore di configurazione] viene selezionato, quindi il valore globale [!UICONTROL Configurazione dell&#39;archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell’azione di invio.


1. Seleziona **Invia azione** come **[!UICONTROL Invia ad Azure Blob Storage]**.
   ![GIF archiviazione BLOB di Azure](/help/forms/assets/azure-submit-video.gif)

1. Seleziona la **[!UICONTROL Configurazione dell&#39;archiviazione]**, in cui salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione di Azure specificata.
La struttura della cartella per salvare i dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

Per impostare i valori di una configurazione, [Generare configurazioni OSGi utilizzando l’SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all&#39;istanza di Cloud Service.

## Utilizzare l’invio sincrono o asincrono {#use-synchronous-or-asynchronous-submission}

Un’azione di invio può utilizzare l’invio sincrono o asincrono.

**Invio sincrono**: In genere, i moduli web sono configurati per l’invio in modo sincrono. In un invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento o in caso di errore di invio, a una pagina di errore. È possibile selezionare la **[!UICONTROL Utilizzare l’invio asincrono]** per reindirizzare gli utenti a una pagina web o mostrare un messaggio all’invio.

![Configurare l’azione Invia](assets/thank-you-setting.png)

**Invio asincrono**: Le esperienze web moderne, come le applicazioni a pagina singola, stanno guadagnando popolarità laddove la pagina web rimane statica mentre l&#39;interazione client-server avviene in background. È ora possibile fornire questa esperienza con Adaptive Forms tramite [configurazione dell’invio asincrono](asynchronous-submissions-adaptive-forms.md).

## Rivalutazione lato server in forma adattiva {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole business. Ma nei browser moderni, gli utenti finali hanno modo di bypassare tali convalide e fare manualmente gli invii utilizzando varie tecniche, come ad esempio Web Browser DevTools Console. Tali tecniche sono valide anche per Adaptive Forms. Uno sviluppatore di moduli può creare diversi logici di convalida, ma tecnicamente, gli utenti finali possono ignorare tali logici di convalida e inviare dati non validi al server. Dati non validi potrebbero interrompere le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente di eseguire anche le convalide fornite da un autore di Forms adattivo durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromesso tra l’invio dei dati e le violazioni delle regole aziendali rappresentate in termini di convalida dei moduli.

### Cosa convalidare sul server? {#what-to-validate-on-server-br}

Tutte le convalide predefinite (OOTB) di un modulo adattivo che vengono ripetute sul server sono:

* Obbligatorio
* Clausola di convalida dell&#39;immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Utilizza la **[!UICONTROL Rivelare sul server]** in Contenitore di moduli adattivi nella barra laterale per abilitare o disabilitare la convalida lato server per il modulo corrente.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l’utente finale bypassa tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida ha esito negativo al server, la transazione di invio viene arrestata. All’utente finale viene presentato nuovamente il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
>
>La convalida lato server convalida il modello di modulo. È consigliabile creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile di HTML e la manipolazione DOM nella stessa libreria client.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

A volte, se **regole di convalida complesse**, lo script di convalida esatto risiede in funzioni personalizzate e l’autore chiama queste funzioni personalizzate dall’espressione di convalida del campo. Per rendere questa libreria di funzioni personalizzate nota e disponibile durante l’esecuzione di convalide lato server, l’autore del modulo può configurare il nome di AEM libreria client nella sezione **[!UICONTROL Base]** scheda delle proprietà del contenitore di moduli adattivi come mostrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per modulo adattivo. Nella libreria , mantieni solo le funzioni riutilizzabili, che dipendono dalle librerie di terze parti jquery e underscore.js.

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida per la protezione e l’indurimento AEM, configura pagine di errore personalizzate come 400.jsp, 404.jsp e 500.jsp. Quando si invia un modulo 400, 404 o 500 vengono visualizzati errori di questi gestori. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish . Puoi anche creare pagine JSP per altri codici di errore HTTP.

Quando si precompila un modello dati del modulo o un modulo adattivo basato su schema con dati XML o JSON in uno schema che non contiene dati `<afData>`, `<afBoundData>`e `</afUnboundData>` quindi i dati dei campi non associati del modulo adattivo vengono persi. Lo schema può essere uno schema XML, uno schema JSON o un modello dati modulo. I campi non collegati sono campi Modulo adattivo senza `bindref` proprietà.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
