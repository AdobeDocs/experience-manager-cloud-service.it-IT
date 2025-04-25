---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: Come collegare la raccolta documenti di SharePoint per un modulo adattivo, Inviare a SharePoint, Creare una configurazione della raccolta documenti di SharePoint, Utilizzare l’azione Invia a SharePoint per un modulo adattivo, Libreria documenti di AEM Forms Data Model SharePoint, Libreria documenti di Forms Data Model SharePoint, Integrare il modello dati di Forms nella raccolta documenti di SharePoint
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: a00b4a93-2324-4c2a-824f-49146dc057b0
source-git-commit: 1dddba99c5871d01bf51c335747363af1889738d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Collegare un modulo adattivo alla raccolta documenti di Microsoft® SharePoint {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

Per utilizzare l&#39;azione di invio **[!UICONTROL Invia a raccolta documenti di SharePoint]** in un modulo adattivo:

1. [Crea una configurazione della libreria di documenti di SharePoint](#1-create-a-sharepoint-document-library-configuration): connette AEM Forms all&#39;archiviazione di Microsoft® Sharepoint.
2. [Utilizzare l&#39;azione Invia a SharePoint in un modulo adattivo](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form): il modulo adattivo viene collegato a Microsoft® SharePoint configurato.

## 1. Creare una configurazione di SharePoint Document Library

Per collegare AEM Forms all&#39;archivio della raccolta documenti di Microsoft® Sharepoint:

1. Vai alla tua istanza di **AEM Forms Author** > **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Dopo aver selezionato **[!UICONTROL Microsoft® SharePoint]**, sei reindirizzato a **[!UICONTROL SharePoint Browser]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Libreria documenti di SharePoint]** dall&#39;elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.

   ![Configurazione Sharepoint](/help/forms/assets/sharepoint_configuration.png)

1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l&#39;ID client, il segreto client e l&#39;ID tenant per l&#39;URL OAuth, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Puoi recuperare `Client ID` e `Client Secret` dell&#39;app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungere l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` per fornire le autorizzazioni di lettura/scrittura. `Sites.Manage.All` è un ambito di autorizzazione nell&#39;API Graph di Microsoft che consente a un&#39;applicazione di gestire tutti gli aspetti dei siti SharePoint, ad esempio l&#39;eliminazione o la modifica di siti.

     >[!NOTE]
     >
     > È inoltre possibile [configurare SharePoint Sites con accesso limitato](/help/forms/configure-sharepoint-site-limited-access.md) utilizzando l&#39;ambito di autorizzazione `Sites.Selected` nell&#39;API Graph di Microsoft. `Sites.Selected` è un ambito di autorizzazione nell&#39;API Graph di Microsoft che consente un accesso più granulare e limitato ai siti SharePoint.

   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

     >[!NOTE]
     >
     > Il campo **segreto client** è obbligatorio oppure facoltativo in base alla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Ambito di autorizzazione `offline_access Sites.Selected` nell&#39;API Graph di Microsoft che consente un accesso più granulare e limitato ai siti SharePoint. Ambito di autorizzazione `offline_access Sites.Manage.All` nell&#39;API Graph di Microsoft che consente l&#39;accesso completo ai siti SharePoint.
1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.

1. Selezionare **Sito SharePoint** > **Raccolta documenti** > **Cartella SharePoint** per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel sito SharePoint selezionato.
   >* Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente nella raccolta `Documents` del sito SharePoint selezionato facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di SharePoint Sites per l’azione di invio in un modulo adattivo.

### 2. Utilizzare la configurazione della raccolta documenti di SharePoint in un modulo adattivo

È possibile utilizzare la configurazione della raccolta documenti di SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella di SharePoint. Per utilizzare una configurazione di archiviazione SharePoint Document Library in un modulo adattivo, effettua le seguenti operazioni:

1. Crea un [modulo adattivo](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Selezionare lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stata creata l&#39;archiviazione della raccolta documenti di SharePoint.
   > * Se non è selezionato alcun contenitore di configurazione [!UICONTROL Contenitore di configurazione], nella finestra delle proprietà dell&#39;azione di invio vengono visualizzate le cartelle globali [!UICONTROL Configurazione archiviazione].

1. Seleziona **Invia azione** come **[!UICONTROL Invia a SharePoint]**.
   ![GIF Sharepoint](/help/forms/assets/sharedrive-video.gif)
1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

>[!NOTE]
>
> Quando si invia il modulo, i dati vengono salvati nell&#39;archivio della raccolta documenti di Microsoft® Sharepoint specificato. La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

>[!NOTE]
>
> Gli allegati vengono archiviati anche nella directory `/folder_name/form_name/year/month/date/submission_id/data`. Tuttavia, se si seleziona **Salva allegati con nome originale**, gli allegati vengono archiviati nella cartella utilizzando i nomi di file originali.
> ![image](/help/forms/assets/sp-doc-attachment-af2.png){height=50%,width=50%}

## Articoli correlati

{{af-submit-action}}
