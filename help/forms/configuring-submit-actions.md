---
title: Come si configura un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio integrate o crearne di personalizzate.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 89e61c009890e2052c5db74b38c93fd54e697cd3
workflow-type: tm+mt
source-wordcount: '3395'
ht-degree: 3%

---

# Azione di invio modulo adattivo {#configuring-the-submit-action}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service | Questo articolo |

**Applicabile a**: ✔️ Componenti Di Base Per Moduli Adattivi. ❌ [Componenti core modulo adattivo](/help/forms/configure-submit-actions-core-components.md). L’Adobe consiglia di utilizzare i Componenti core per [aggiungere un Forms adattivo a una pagina AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md) o a [creare un Forms adattivo indipendente](creating-adaptive-form-core-components.md).

Un’azione di invio viene attivata quando un utente fa clic su **[!UICONTROL Invia]** in un modulo adattivo. Forms as a Cloud Service fornisce le seguenti azioni di invio pronte all’uso.

* [Invia all’endpoint REST](#submit-to-rest-endpoint)
* [Invia e-mail](#send-email)
* [Invia usando il modello dati modulo](#submit-using-form-data-model)
* [Richiama un flusso di lavoro AEM](#invoke-an-aem-workflow)
* [Invia a SharePoint](#submit-to-sharedrive)
* [Invia a OneDrive](#submit-to-onedrive)
* [Invia ad Azure Blob Storage](#azure-blob-storage)
* [Invia a Power Automate](#microsoft-power-automate)

È inoltre possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md) per creare un’azione di invio personalizzata.

Puoi configurare un’azione di invio in **[!UICONTROL Invio]** nella barra laterale, nella sezione delle proprietà Contenitore modulo adattivo.

![Configura azione di invio](assets/submission.png)


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

Utilizza il **[!UICONTROL Invia all’endpoint REST]** azione per pubblicare i dati inviati su un URL rest. L’URL può essere interno (il server sul quale viene eseguito il rendering del modulo) o esterno.

Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, /content/restEndPoint. Per tali richieste successive, vengono utilizzate le informazioni di autenticazione della richiesta di invio.

Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell’URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

![Mappatura per i valori dei campi passati come parametri della pagina di ringraziamento](assets/post-enabled-actionconfig.png)

Nell’esempio precedente, l’utente ha inserito le informazioni in `textbox` viene acquisito tramite il parametro `param1`. Sintassi per pubblicare i dati acquisiti tramite `param1` è:

`String data=request.getParameter("param1");`

Analogamente, i parametri utilizzati per la registrazione di dati e allegati XML sono `dataXml` e `attachments`.

Ad esempio, questi due parametri vengono utilizzati nello script per analizzare i dati in un punto finale rest. Utilizza la sintassi seguente per archiviare e analizzare i dati:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

In questo esempio, `data` memorizza i dati XML e `att` memorizza i dati dell&#39;allegato.

Il **[!UICONTROL Invia all’endpoint REST]** Azione di invio invia i dati compilati nel modulo a una pagina di conferma configurata come parte della richiesta HTTP GET. Puoi aggiungere il nome dei campi da richiedere. Il formato della richiesta è:

`{fieldName}={request parameter name}`

Come mostrato nell&#39;immagine seguente, `param1` e `param2` vengono passati come parametri con valori copiati da **casella di testo** e **numericbox** campi per l’azione successiva.

![Configurazione dell’azione di invio endpoint REST](assets/action-config.png)

È inoltre possibile **[!UICONTROL Abilita richiesta POST]** e fornisci un URL per pubblicare la richiesta. Per inviare i dati al server AEM che ospita il modulo, utilizzare un percorso relativo corrispondente al percorso radice del server AEM. Esempio: `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

>[!NOTE]
>
>Per passare i campi come parametri in un URL REST, tutti i campi devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi.

## Invia e-mail {#send-email}

È possibile utilizzare **[!UICONTROL Invia e-mail]** Azione di invio per inviare un’e-mail a uno o più destinatari in seguito all’invio corretto del modulo. L’e-mail generata può contenere dati del modulo in un formato predefinito. Ad esempio, nel modello seguente, il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviati.

    &quot;
    
    Ciao ${customer_Name},
    
    Di seguito è riportato l&#39;indirizzo di spedizione predefinito:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Cordiali saluti
    WKND
    
    &quot;

>[!NOTE]
>
> * Tutti i campi modulo devono avere nomi di elementi diversi, anche se i campi sono posizionati su pannelli diversi di un modulo adattivo.
> * AEM as a Cloud Service richiede la crittografia della posta in uscita. Per impostazione predefinita, l’e-mail in uscita è disabilitata. Per attivarlo, invia un ticket di supporto a [Richiesta di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

Puoi anche includere nell’e-mail allegati e un documento di record (DoR). Per abilitare **[!UICONTROL Allega documento record]** , configura il modulo adattivo per generare un documento di record (DoR). Puoi abilitare l’opzione per generare un documento di record dalle proprietà del modulo adattivo.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Invia usando il modello dati modulo {#submit-using-form-data-model}

Il **[!UICONTROL Invia utilizzando il modello dati modulo]** L’azione di invio scrive i dati del modulo adattivo inviati per l’oggetto modello dati specificato in un modello dati modulo nella relativa origine dati. Durante la configurazione dell’azione di invio, puoi scegliere un oggetto modello dati di cui desideri riscrivere i dati inviati nella relativa origine dati.

È inoltre possibile inviare un allegato del modulo all&#39;origine dati utilizzando un modello dati modulo e un documento di record (DoR). Per informazioni sul modello dati del modulo, consulta [[!DNL AEM Forms] Integrazione dei dati](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Richiama un flusso di lavoro AEM {#invoke-an-aem-workflow}

Il **[!UICONTROL Richiama un flusso di lavoro AEM]** Azione di invio associa un modulo adattivo a un [Flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). Quando un modulo viene inviato, il flusso di lavoro associato viene avviato automaticamente nell’istanza Autore. Puoi salvare il file di dati, gli allegati e il documento di record nella posizione di payload del flusso di lavoro o in una variabile. Se il flusso di lavoro è contrassegnato per l’archiviazione dati esterna e configurato per un’archiviazione dati esterna, è disponibile solo l’opzione della variabile. Puoi effettuare una selezione dall’elenco di variabili disponibili per il modello di flusso di lavoro. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni in una fase successiva e non al momento della creazione del flusso di lavoro, assicurati che siano presenti le configurazioni di variabili richieste.

L’azione di invio inserisce quanto segue nella posizione di payload del flusso di lavoro, o nella variabile se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni:

* **File di dati**: contiene i dati inviati al modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso file di dati]** per specificare il nome del file e il percorso del file relativo al payload. Ad esempio, il `/addresschange/data.xml` percorso crea una cartella denominata `addresschange` e lo posiziona in relazione al payload. È inoltre possibile specificare solo `data.xml` per inviare solo i dati inviati senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

* **Allegati**: puoi utilizzare la **[!UICONTROL Percorso allegato]** per specificare il nome della cartella in cui archiviare gli allegati caricati nel modulo adattivo. La cartella viene creata in relazione al payload. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

* **Documento record**: contiene il documento di record generato per il modulo adattivo. È possibile utilizzare **[!UICONTROL Percorso del documento record]** per specificare il nome del file del documento di record e il percorso del file relativo al payload. Ad esempio, il `/addresschange/DoR.pdf` percorso crea una cartella denominata `addresschange` relativo al payload e posiziona il `DoR.pdf` relativo al payload. È inoltre possibile specificare solo `DoR.pdf` per salvare solo un documento di record senza creare una gerarchia di cartelle. Se il flusso di lavoro è contrassegnato per l’archiviazione di dati esterni, utilizza l’opzione della variabile e seleziona la variabile dall’elenco di variabili disponibili per il modello di flusso di lavoro.

Prima di utilizzare **[!UICONTROL Richiama un flusso di lavoro AEM]** Azione di invio configura quanto segue per **[!UICONTROL Servizio impostazioni Servizi di dominio AEM]** configurazione:

* **[!UICONTROL Elaborazione URL server]**: il server di elaborazione è il server in cui viene attivato il flusso di lavoro Forms o AEM. Può essere uguale all’URL dell’istanza di authoring AEM o di un altro server.

* **[!UICONTROL Nome utente server di elaborazione]**: nome utente dell’utente del flusso di lavoro

* **[!UICONTROL Password server di elaborazione]**: password dell&#39;utente del flusso di lavoro

## Invia a SharePoint {#submit-to-sharedrive}

Il **[!UICONTROL Invia a SharePoint]** L’azione di invio collega un modulo adattivo a un archivio Microsoft® SharePoint. È possibile inviare il file di dati del modulo, gli allegati o il documento di record all&#39;archivio di Microsoft® Sharepoint connesso. Per utilizzare **[!UICONTROL Invia a SharePoint]** Azione di invio in un modulo adattivo:

1. [Creare una configurazione SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): collega AEM Forms all’archiviazione Microsoft® Sharepoint.
2. [Utilizzare l’azione Invia a SharePoint in un modulo adattivo](#use-sharepoint-configuartion-in-af): collega il modulo adattivo a Microsoft® SharePoint configurato.

### Creare una configurazione SharePoint {#create-sharepoint-configuration}

Per collegare AEM Forms al tuo Microsoft® Sharepoint Storage:

1. Vai al tuo **Autore AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Dopo aver selezionato **[!UICONTROL Microsoft® SharePoint]**, viene reindirizzato a **[!UICONTROL Browser SharePoint]**.
1. Seleziona un **Contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Clic **[!UICONTROL Crea]** > **[!UICONTROL Raccolta documenti di SharePoint]** dall’elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.

![Configurazione SharePoint](/help/forms/assets/sharepoint_configuration.png)
1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l’ID client, il segreto client e l’ID tenant per l’URL OAuth, consulta [Documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * È possibile recuperare `Client ID` e `Client Secret` dell’app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungi l’URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l’URL dell’istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` per fornire autorizzazioni di lettura/scrittura.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell’app dal portale Microsoft® Azure.

   >[!NOTE]
   >
   > Il **segreto client** Il campo è obbligatorio o facoltativo dipende dalla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Clic **[!UICONTROL Connetti]**. In caso di connessione riuscita, il `Connection Successful` viene visualizzato il messaggio.

1. Ora, seleziona **Sito SharePoint** > **Raccolta documenti** > **Cartella SharePoint**, per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel sito SharePoint selezionato.
   >* Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente nel `Documents` libreria del sito SharePoint selezionato facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di SharePoint Sites per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione SharePoint in un modulo adattivo {#use-sharepoint-configuartion-in-af}

Puoi utilizzare la configurazione SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella SharePoint. Per utilizzare una configurazione di archiviazione SharePoint in un modulo adattivo, effettua le seguenti operazioni:

1. Creare un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo storage SharePoint.
   > * In caso negativo [!UICONTROL Contenitore configurazione] è selezionato, quindi il [!UICONTROL Configurazione archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell&#39;azione di invio.

1. Seleziona **Azione di invio** as **[!UICONTROL Invia a SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Seleziona la **[!UICONTROL Configurazione archiviazione]**, dove desideri salvare i dati.
1. Clic **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio di Microsoft® Sharepoint specificato.
La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Invia a OneDrive {#submit-to-onedrive}

Il **[!UICONTROL Invia a OneDrive]** L&#39;azione di invio collega un modulo adattivo a Microsoft® OneDrive. È possibile inviare i dati del modulo, i file, gli allegati o il documento di record all&#39;archivio Microsoft® OneDrive collegato. Per utilizzare [!UICONTROL Invia a OneDrive] Azione di invio in un modulo adattivo:

1. [Crea una configurazione OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): collega AEM Forms allo storage Microsoft® OneDrive.
2. [Utilizzare l&#39;azione Invia a OneDrive in un modulo adattivo](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): collega il modulo adattivo a Microsoft® OneDrive configurato.

### Crea una configurazione OneDrive {#create-onedrice-configuration}

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

Per collegare AEM Forms allo storage Microsoft® OneDrive:

1. Vai al tuo **Autore AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. Dopo aver selezionato **[!UICONTROL Microsoft® OneDrive]**, viene reindirizzato a **[!UICONTROL Browser OneDrive]**.
1. Seleziona un **Contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Verrà visualizzata la configurazione guidata di OneDrive.

   ![Schermata Configurazione OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l’ID client, il segreto client e l’ID tenant per l’URL OAuth, consulta [Documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * È possibile recuperare `Client ID` e `Client Secret` dell’app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungi l’URI di reindirizzamento come `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l’URL dell’istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Files.ReadWrite.All` per fornire autorizzazioni di lettura/scrittura.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell’app dal portale Microsoft® Azure.

   >[!NOTE]
   >
   > Il **segreto client** Il campo è obbligatorio o facoltativo dipende dalla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Clic **[!UICONTROL Connetti]**. In caso di connessione riuscita, il `Connection Successful` viene visualizzato il messaggio.

1. Ora, seleziona **[!UICONTROL Contenitore OneDrive]** > **[Cartella OneDrive]**  per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel contenitore OneDrive.
   > * Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di archiviazione OneDrive per l&#39;azione di invio in un modulo adattivo.

### Usa configurazione OneDrive in un modulo adattivo {#use-onedrive-configuartion-in-af}

È possibile utilizzare la configurazione di archiviazione di OneDrive creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella di OneDrive. Per utilizzare la configurazione di archiviazione OneDrive in un modulo adattivo, effettua le seguenti operazioni:
1. Creare un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo storage OneDrive.
   > * In caso negativo [!UICONTROL Contenitore configurazione] è selezionato, quindi il [!UICONTROL Configurazione archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell&#39;azione di invio.

1. Seleziona **Azione di invio** as **[!UICONTROL Invia a OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
1. Seleziona la **[!UICONTROL Configurazione archiviazione]**, dove desideri salvare i dati.
1. Clic **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio Microsoft® OneDrive specificato.
La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Invia ad Azure Blob Storage {#submit-to-azure-blob-storage}

Il **[!UICONTROL Invia ad Azure Blob Storage]**  L’azione di invio collega un modulo adattivo a un portale Microsoft® Azure. È possibile inviare i dati del modulo, il file, gli allegati o il documento record ai contenitori di archiviazione di Azure connessi. Per utilizzare l’azione Invia per l’archiviazione BLOB di Azure:

1. [Creare un contenitore di archiviazione BLOB di Azure](#create-a-azure-blob-storage-container-create-azure-configuration): connette AEM Forms ai contenitori di archiviazione Azure.
2. [Utilizzare la configurazione di archiviazione Azure in un modulo adattivo](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): collega il modulo adattivo ai contenitori di archiviazione Azure configurati.

### Creare un contenitore di archiviazione BLOB di Azure {#create-azure-configuration}

Per connettere AEM Forms ai contenitori di archiviazione Azure:
1. Vai al tuo **Autore AEM Forms** istanza > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Archiviazione Azure]**.
1. Dopo aver selezionato **[!UICONTROL Archiviazione Azure]**, viene reindirizzato a **[!UICONTROL Browser archiviazione Azure]**.
1. Seleziona un **Contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la procedura guidata Crea configurazione di archiviazione Azure.

   ![Configurazione archiviazione Azure](/help/forms/assets/azure-storage-configuration.png)

1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]**.

   * Puoi recuperare `Azure Storage Account` nome e `Azure Access key` dagli account di archiviazione nel portale Microsoft® Azure.

1. Fai clic su **[!UICONTROL Salva]**.

Ora puoi utilizzare questa configurazione del contenitore di archiviazione Azure per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione di archiviazione Azure in un modulo adattivo {#use-azure-storage-configuartion-in-af}

Puoi utilizzare la configurazione del contenitore di archiviazione Azure creata in un modulo adattivo per salvare dati o documenti di record generati nel contenitore di archiviazione Azure. Per utilizzare la configurazione del contenitore di archiviazione Azure in un modulo adattivo, effettua le seguenti operazioni:
1. Creare un [Modulo adattivo](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stato creato lo storage OneDrive.
   > * In caso negativo [!UICONTROL Contenitore configurazione] è selezionato, quindi il [!UICONTROL Configurazione archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell&#39;azione di invio.

1. Seleziona **Azione di invio** as **[!UICONTROL Invia ad Azure Blob Storage]**.
   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

1. Seleziona la **[!UICONTROL Configurazione archiviazione]**, dove desideri salvare i dati.
1. Clic **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nella configurazione del contenitore di archiviazione Azure specificata.
La struttura di cartelle per il salvataggio dei dati è `/configuration_container/form_name/year/month/date/submission_id/data`.

Per impostare i valori di una configurazione: [Generare configurazioni OSGi utilizzando l’SDK per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all’istanza di Cloud Service.


## Invia a Power Automate {#microsoft-power-automate}

È possibile configurare un modulo adattivo per eseguire un flusso cloud di Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business sulla base dei dati acquisiti e automatizzare i flussi di lavoro dei clienti. Di seguito sono riportati alcuni esempi di cosa è possibile fare dopo l’integrazione di un modulo adattivo con Microsoft® Power Automate:

* Utilizzare dati Forms adattivi in processi aziendali Power Automate
* Utilizza Power Automate per inviare i dati acquisiti a più di 500 origini dati o a qualsiasi API disponibile pubblicamente
* Eseguire calcoli complessi sui dati acquisiti
* Salvataggio dei dati Adaptive Forms sui sistemi di storage secondo una pianificazione predefinita

L’editor di Forms adattivo fornisce **Richiama un flusso Microsoft® Power Automate** l’azione di invio per inviare i dati dei moduli adattivi, gli allegati e il documento di record viene inviata a Power Automate Cloud Flow. Per utilizzare l&#39;azione Invia per inviare i dati acquisiti a Microsoft® Power Automate, [Collegare l&#39;istanza Forms as a Cloud Service con Microsoft® Power Automate](forms-microsoft-power-automate-integration.md)

Dopo una configurazione corretta, utilizza [Richiama un flusso Microsoft® Power Automate](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) azione di invio per inviare dati a un flusso Power Automate.

## Utilizzare l’invio sincrono o asincrono {#use-synchronous-or-asynchronous-submission}

Un’azione di invio può utilizzare l’invio sincrono o asincrono.

**Invio sincrono**: in genere, i moduli web sono configurati per l’invio sincrono. In un invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento oppure, se l’invio non riesce, a una pagina di errore. È possibile selezionare **[!UICONTROL Utilizzare l’invio asincrono]** per reindirizzare gli utenti a una pagina web o mostrare un messaggio all’invio.

![Configura azione di invio](assets/thank-you-setting.png)

**Invio asincrono**: le moderne esperienze web, come le applicazioni a pagina singola, stanno guadagnando popolarità: la pagina web rimane statica, mentre l’interazione client-server avviene in background. Ora puoi fornire questa esperienza con Adaptive Forms tramite [configurazione dell’invio asincrono](asynchronous-submissions-adaptive-forms.md).

## Riconvalida lato server in modulo adattivo {#server-side-revalidation-in-adaptive-form}

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole di business. Tuttavia, nei browser moderni, gli utenti finali possono ignorare tali convalide ed effettuare manualmente gli invii utilizzando varie tecniche, ad esempio la Console per la creazione di strumenti di browser Web. Tali tecniche sono valide anche per Adaptive Forms. Uno sviluppatore di moduli può creare diverse logiche di convalida, ma tecnicamente gli utenti finali possono ignorarle e inviare dati non validi al server. I dati non validi violano le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente inoltre di eseguire le convalide fornite da un autore di Forms adattivo durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromissione dell’invio dei dati e delle violazioni delle regole aziendali rappresentate in termini di convalide dei moduli.

### Cosa convalidare su Server? {#what-to-validate-on-server-br}

Tutte le convalide di campo pronte all’uso di un modulo adattivo che vengono rieseguite sul server sono:

* Obbligatorio
* Clausola di convalida immagine
* Espressione di convalida

### Abilitazione della convalida lato server {#enabling-server-side-validation-br}

Utilizza il **[!UICONTROL Riconvalida sul server]** in Contenitore modulo adattivo nella barra laterale per abilitare o disabilitare la convalida lato server per il modulo corrente.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

Abilitazione della convalida lato server

Se l&#39;utente finale ignora tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida non riesce alla fine del server, la transazione di invio viene interrotta. All’utente finale viene nuovamente presentato il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
>
>La convalida lato server convalida il modello del modulo. Ti consigliamo di creare una libreria client separata per le convalide e di non combinarla con altri elementi come lo stile di HTML e la manipolazione DOM nella stessa libreria client.

### Supporto di funzioni personalizzate nelle espressioni di convalida {#supporting-custom-functions-in-validation-expressions-br}

A volte, se ci sono **regole di convalida complesse**, lo script di convalida esatto risiede nelle funzioni personalizzate e l’autore chiama tali funzioni personalizzate dall’espressione di convalida del campo. Per rendere nota e disponibile questa libreria di funzioni personalizzata durante l’esecuzione delle convalide lato server, l’autore del modulo può configurare il nome della libreria client AEM in **[!UICONTROL Base]** delle proprietà del Contenitore modulo adattivo, come illustrato di seguito.

![Supporto di funzioni personalizzate nelle espressioni di convalida](assets/clientlib-cat.png)

Supporto di funzioni personalizzate nelle espressioni di convalida

L’autore può configurare una libreria JavaScript personalizzata per modulo adattivo. Nella libreria, mantieni solo le funzioni riutilizzabili, che hanno dipendenza da librerie di terze parti jquery e underscore.js.

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida sulla sicurezza e l’irrigidimento dell’AEM, configura pagine di errore personalizzate come 400.jsp, 404.jsp e 500.jsp. Questi gestori vengono chiamati quando all’invio di un modulo vengono visualizzati errori 400, 404 o 500. Gli handler vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish. Puoi anche creare pagine JSP per altri codici di errore HTTP.

Quando si precompila un modello di dati modulo o un modulo adattivo basato su schema con un reclamo di dati XML o JSON per uno schema che non contiene dati `<afData>`, `<afBoundData>`, e `</afUnboundData>` , i dati dei campi non limitati del modulo adattivo andranno persi. Lo schema può essere uno schema XML, uno schema JSON o un modello dati modulo. I campi non limitati sono campi modulo adattivo senza `bindref` proprietà.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
