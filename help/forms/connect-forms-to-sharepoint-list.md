---
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: Come connettere l’elenco di SharePoint per un modulo adattivo?, Invia a SharePoint, Crea configurazione elenco SharePoint, Utilizza l’azione di invio Invia a SharePoint in un modulo adattivo, Connetti un modulo adattivo a Microsoft&reg; Elenco SharePoint.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

Per utilizzare l&#39;azione di invio [!UICONTROL Invia a elenco SharePoint] in un modulo adattivo:

1. [Crea una configurazione elenco SharePoint](#1-create-a-sharepoint-list-configuration): connette AEM Forms all&#39;archiviazione elenco Microsoft® Sharepoint.
1. [Utilizzare l&#39;invio utilizzando il modello dati del modulo (FDM) in un modulo adattivo](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): collega il modulo adattivo a Microsoft® SharePoint configurato.

## &#x200B;1. Creare una configurazione dell’elenco SharePoint

Per collegare AEM Forms all’elenco di Microsoft® Sharepoint:

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Microsoft® SharePoint]**.
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


## &#x200B;2. Utilizzare l’opzione Sottometti con modello dati modulo (FDM) in un modulo adattivo {#use-submit-using-fdm}

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
