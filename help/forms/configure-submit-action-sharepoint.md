---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Come connettere un elenco di SharePoint per un modulo adattivo?, Come connettere una raccolta documenti di SharePoint per un modulo adattivo, Inviare a SharePoint, Creare una configurazione della raccolta documenti di SharePoint, Utilizzare l’azione Invia a SharePoint in un modulo adattivo, Connettere un modulo adattivo a Microsoft&reg; Elenco SharePoint.
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# Collegare un modulo adattivo a Microsoft® SharePoint

Il **[!UICONTROL Invia a SharePoint]** L’azione di invio consente di collegare facilmente il Modulo adattivo a un archivio Microsoft® SharePoint. Dopo l’invio del modulo, i dati del modulo vengono inviati all’archiviazione SharePoint desiderata.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione delle richieste di moduli. Per ulteriori informazioni su queste opzioni, consulta [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md)  articolo.

## Vantaggi

Alcuni dei vantaggi dell’invio di dati da un modulo adattivo all’archiviazione SharePoint sono:

* Semplifica l&#39;invio diretto dei dati dei moduli a SharePoint, fornendo una posizione centralizzata per l&#39;archiviazione e la gestione delle informazioni.
* Applicando le funzioni di controllo degli accessi e delle autorizzazioni di SharePoint, questo garantisce che solo le persone autorizzate possano visualizzare o modificare i dati inviati.

Utilizzo di **[!UICONTROL Invia a SharePoint]**, è possibile:

* [Collegare un modulo adattivo alla raccolta documenti di SharePoint](#connect-af-sharepoint-doc-library)
* [Collegare un modulo adattivo a elenco SharePoint](#connect-af-sharepoint-list)

## Collegare un modulo adattivo alla raccolta documenti di SharePoint {#connect-af-sharepoint-doc-library}

Per utilizzare **[!UICONTROL Invia a raccolta documenti di SharePoint]** Azione di invio in un modulo adattivo:

1. [Creare una configurazione di SharePoint Document Library](#create-a-sharepoint-configuration-create-sharepoint-configuration): collega AEM Forms all’archiviazione Microsoft® Sharepoint.
2. [Utilizzare l’azione Invia a SharePoint in un modulo adattivo](#use-sharepoint-configuartion-in-af): collega il modulo adattivo a Microsoft® SharePoint configurato.

### Creare una configurazione di SharePoint Document Library {#create-sharepoint-configuration}

Per collegare AEM Forms all&#39;archivio della raccolta documenti di Microsoft® Sharepoint:

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

### Utilizzare la configurazione della raccolta documenti di SharePoint in un modulo adattivo {#use-sharepoint-configuartion-in-af}

È possibile utilizzare la configurazione della raccolta documenti di SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella di SharePoint. Per utilizzare una configurazione di archiviazione SharePoint Document Library in un modulo adattivo, effettua le seguenti operazioni:

1. Creare un [Modulo adattivo](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Seleziona lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stata creata l’archiviazione della raccolta documenti di SharePoint.
   > * In caso negativo [!UICONTROL Contenitore configurazione] è selezionato, quindi il [!UICONTROL Configurazione archiviazione] Le cartelle vengono visualizzate nella finestra delle proprietà dell&#39;azione di invio.

1. Seleziona **Azione di invio** as **[!UICONTROL Invia a SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Seleziona la **[!UICONTROL Configurazione archiviazione]**, dove desideri salvare i dati.
1. Clic **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio della raccolta documenti di Microsoft® Sharepoint specificato.
La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Per utilizzare [!UICONTROL Invia a elenco SharePoint] Azione di invio in un modulo adattivo:

1. [Creare una configurazione dell’elenco SharePoint](#create-sharepoint-list-configuration): collega AEM Forms all’archivio degli elenchi Microsoft® Sharepoint.
1. [Utilizzare l’invio utilizzando il modello dati del modulo in un modulo adattivo](#use-submit-using-fdm): collega il modulo adattivo a Microsoft® SharePoint configurato.

### Creare una configurazione dell’elenco SharePoint {#create-sharepoint-list-configuration}

Per collegare AEM Forms all’elenco di Microsoft® Sharepoint:

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Seleziona un **Contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Clic **[!UICONTROL Crea]** > **[!UICONTROL Elenco SharePoint]** dall’elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.
1. Specifica la **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l’ID client, il segreto client e l’ID tenant per l’URL OAuth, consulta [Documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * È possibile recuperare `Client ID` e `Client Secret` dell’app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungi l’URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l’URL dell’istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` nel **Grafico Microsoft®** per fornire autorizzazioni di lettura/scrittura. Aggiungi `AllSites.Manage` autorizzazione in **Sharepoint** per interagire in remoto con i dati di SharePoint.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell’app dal portale Microsoft® Azure.

     >[!NOTE]
     >
     > Il **segreto client** Il campo è obbligatorio o facoltativo dipende dalla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Clic **[!UICONTROL Connetti]**. In caso di connessione riuscita, il `Connection Successful` viene visualizzato il messaggio.
1. Seleziona **[!UICONTROL Sito SharePoint]** e **[!UICONTROL Elenco SharePoint]** dall’elenco a discesa.
1. Seleziona **[!UICONTROL Crea]** per creare la configurazione cloud per Microsoft® SharePointList.


### Utilizzare l’invio utilizzando il modello dati del modulo in un modulo adattivo {#use-submit-using-fdm}

È possibile utilizzare la configurazione dell’elenco SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in un elenco SharePoint. Per utilizzare un elenco SharePoint in un modulo adattivo come, effettua le seguenti operazioni:

1. [Creare un modello di dati modulo con Microsoft](/help/forms/create-form-data-models.md)
1. [Configurare il modello dati modulo per recuperare e inviare dati](/help/forms/work-with-form-data-model.md#configure-services)
1. [Creare un modulo adattivo](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurare l’azione di invio utilizzando un modello dati modulo](/help/forms/using-form-data-model.md)

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio elenco di Microsoft® Sharepoint specificato.

>[!NOTE]
>
> In Microsoft® SharePoint List non sono supportati i seguenti tipi di colonna:
* colonna immagine
* colonna metadati
* colonna persona
* colonna di dati esterni

## Articoli correlati

{{af-submit-action}}