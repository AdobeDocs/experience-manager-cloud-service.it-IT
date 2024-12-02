---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Come connettere l'elenco di SharePoint per un modulo adattivo?, Come connettere la raccolta documenti di SharePoint per un modulo adattivo, Inviare a SharePoint, Creare una configurazione della raccolta documenti di SharePoint, Utilizzare l'azione Invia a SharePoint in un modulo adattivo, Connettere un modulo adattivo a Microsoft&reg; Elenco SharePoint.
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: 5e1d08e82cafc3a8a715653727f42ce0048f2b1f
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Collegare un modulo adattivo a Microsoft® SharePoint

L&#39;azione di invio **[!UICONTROL Invia a SharePoint]** consente di collegare facilmente il modulo adattivo a un archivio Microsoft® SharePoint. Dopo l’invio del modulo, i dati del modulo vengono inviati all’archiviazione SharePoint desiderata.

AEM as a Cloud Service offre diverse azioni di invio pronte all’uso per la gestione degli invii di moduli. Ulteriori informazioni su queste opzioni sono disponibili nell&#39;articolo [Azione di invio modulo adattivo](/help/forms/configure-submit-actions-core-components.md).

## Vantaggi

Alcuni dei vantaggi dell’invio di dati da un modulo adattivo all’archiviazione SharePoint sono:

* Semplifica l&#39;invio diretto dei dati dei moduli a SharePoint, fornendo una posizione centralizzata per l&#39;archiviazione e la gestione delle informazioni.
* Applicando le funzioni di controllo degli accessi e delle autorizzazioni di SharePoint, questo garantisce che solo le persone autorizzate possano visualizzare o modificare i dati inviati.

Utilizzando **[!UICONTROL Invia a SharePoint]**, è possibile:

* [Collegare un modulo adattivo alla raccolta documenti di SharePoint](#connect-af-sharepoint-doc-library)
* [Collegare un modulo adattivo a elenco SharePoint](#connect-af-sharepoint-list)

## Collegare un modulo adattivo alla raccolta documenti di SharePoint {#connect-af-sharepoint-doc-library}

Per utilizzare l&#39;azione di invio **[!UICONTROL Invia a raccolta documenti di SharePoint]** in un modulo adattivo:

1. [Crea una configurazione della libreria di documenti di SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): connette AEM Forms all&#39;archiviazione di Microsoft® Sharepoint.
2. [Utilizzare l&#39;azione Invia a SharePoint in un modulo adattivo](#use-sharepoint-configuartion-in-af): il modulo adattivo viene collegato a Microsoft® SharePoint configurato.

### Creare una configurazione di SharePoint Document Library {#create-sharepoint-configuration}

Per collegare AEM Forms all&#39;archivio della raccolta documenti di Microsoft® Sharepoint:

1. Vai all&#39;istanza di **AEM Forms Author** > **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
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

1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.

1. Selezionare **Sito SharePoint** > **Raccolta documenti** > **Cartella SharePoint** per salvare i dati.

   >[!NOTE]
   >
   >* Per impostazione predefinita, `forms-ootb-storage-adaptive-forms-submission` è presente nel sito SharePoint selezionato.
   >* Creare una cartella come `forms-ootb-storage-adaptive-forms-submission`, se non già presente nella raccolta `Documents` del sito SharePoint selezionato facendo clic su **Crea cartella**.

Ora puoi utilizzare questa configurazione di SharePoint Sites per l’azione di invio in un modulo adattivo.

### Utilizzare la configurazione della raccolta documenti di SharePoint in un modulo adattivo {#use-sharepoint-configuartion-in-af}

È possibile utilizzare la configurazione della raccolta documenti di SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in una cartella di SharePoint. Per utilizzare una configurazione di archiviazione SharePoint Document Library in un modulo adattivo, effettua le seguenti operazioni:

1. Crea un [modulo adattivo](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Selezionare lo stesso [!UICONTROL Contenitore configurazione] per un modulo adattivo, in cui è stata creata l&#39;archiviazione della raccolta documenti di SharePoint.
   > * Se non è selezionato alcun contenitore di configurazione [!UICONTROL Contenitore di configurazione], nella finestra delle proprietà dell&#39;azione di invio vengono visualizzate le cartelle globali [!UICONTROL Configurazione archiviazione].

1. Seleziona **Invia azione** come **[!UICONTROL Invia a SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Selezionare la **[!UICONTROL configurazione archiviazione]**, in cui si desidera salvare i dati.
1. Fai clic su **[!UICONTROL Salva]** per salvare le impostazioni di invio.

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio della raccolta documenti di Microsoft® Sharepoint specificato.
La struttura di cartelle per il salvataggio dei dati è `/folder_name/form_name/year/month/date/submission_id/data`.

## Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Per utilizzare l&#39;azione di invio [!UICONTROL Invia a elenco SharePoint] in un modulo adattivo:

1. [Crea una configurazione elenco SharePoint](#create-sharepoint-list-configuration): connette AEM Forms all&#39;archiviazione elenco Microsoft® Sharepoint.
1. [Utilizzare l&#39;invio utilizzando il modello dati del modulo (FDM) in un modulo adattivo](#use-submit-using-fdm): collega il modulo adattivo a Microsoft® SharePoint configurato.

### Creare una configurazione dell’elenco SharePoint {#create-sharepoint-list-configuration}

Per collegare AEM Forms all’elenco di Microsoft® Sharepoint:

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Seleziona un **contenitore configurazione**. La configurazione viene archiviata nel Contenitore configurazione selezionato.
1. Fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa. Viene visualizzata la procedura guidata di configurazione di SharePoint.
1. Specifica il **[!UICONTROL Titolo]**, **[!UICONTROL ID client]**, **[!UICONTROL Segreto client]** e **[!UICONTROL URL OAuth]**. Per informazioni su come recuperare l&#39;ID client, il segreto client e l&#39;ID tenant per l&#39;URL OAuth, consulta la [documentazione di Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Puoi recuperare `Client ID` e `Client Secret` dell&#39;app dal portale Microsoft® Azure.
   * Nel portale Microsoft® Azure, aggiungere l&#39;URI di reindirizzamento come `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Sostituisci `[author-instance]` con l&#39;URL dell&#39;istanza di authoring.
   * Aggiungere le autorizzazioni API `offline_access` e `Sites.Manage.All` nella scheda **Microsoft® Graph** per fornire le autorizzazioni di lettura/scrittura. Aggiungere l&#39;autorizzazione `AllSites.Manage` nella scheda **Sharepoint** per interagire in remoto con i dati di SharePoint.
   * Usa URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Sostituisci `<tenant-id>` con `tenant-id` dell&#39;app dal portale di Microsoft® Azure.

     >[!NOTE]
     >
     > Il campo **segreto client** è obbligatorio oppure facoltativo in base alla configurazione dell&#39;applicazione Azure Active Directory. Se l’applicazione è configurata per l’utilizzo di un segreto client, è obbligatorio fornire il segreto client.

1. Fai clic su **[!UICONTROL Connetti]**. Se la connessione ha esito positivo, viene visualizzato il messaggio `Connection Successful`.
1. Selezionare **[!UICONTROL Sito SharePoint]** e **[!UICONTROL Elenco SharePoint]** dall&#39;elenco a discesa.
1. Selezionare **[!UICONTROL Crea]** per creare la configurazione cloud per Microsoft® SharePointList.


### Utilizzare l’invio utilizzando il modello dati modulo (FDM) in un modulo adattivo {#use-submit-using-fdm}

È possibile utilizzare la configurazione dell’elenco SharePoint creata in un modulo adattivo per salvare dati o documenti di record generati in un elenco SharePoint. Per utilizzare un elenco SharePoint in un modulo adattivo come, effettua le seguenti operazioni:

1. [Creare un modello dati modulo (FDM) tramite Microsoft](/help/forms/create-form-data-models.md)
1. [Configurare il modello dati modulo (FDM) per recuperare e inviare dati](/help/forms/work-with-form-data-model.md#configure-services)
1. [Creare un modulo adattivo](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurare l’azione di invio utilizzando un modello di dati del modulo (FDM)](/help/forms/using-form-data-model.md)

Quando si invia il modulo, i dati vengono salvati nell&#39;archivio elenco di Microsoft® Sharepoint specificato.

>[!NOTE]
>
> In Microsoft® SharePoint List non sono supportati i seguenti tipi di colonna:
> * colonna immagine
> * colonna metadati
> * colonna persona
> * colonna di dati esterni

## Articoli correlati

{{af-submit-action}}
