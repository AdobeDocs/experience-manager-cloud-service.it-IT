---
title: Condivisione di risorse, cartelle e raccolte come collegamento
description: Questo articolo descrive come condividere risorse, cartelle e raccolte in Experience Manager Assets come collegamento ipertestuale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Condivisione e distribuzione delle risorse gestite in Experience Manager {#share-assets-from-aem}

Risorse Adobe Experience Manager (AEM) consente di condividere risorse, cartelle e raccolte con membri dell’organizzazione ed entità esterne, inclusi partner e fornitori. Utilizzate i seguenti metodi per condividere le risorse da Experience Manager Assets come servizio Cloud:

* Condividi come collegamento.
* Scaricate le risorse e condividetele separatamente.
* Condividi tramite l&#39;app desktop AEM.
* Condividi tramite Adobe Asset Link.
* (Prossima funzionalità) Condividete tramite Brand Portal.

## Condividere le risorse come collegamento {#sharelink}

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti. La condivisione di risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili a soggetti esterni senza dover prima accedere a Risorse AEM.

>[!NOTE]
>
>* È necessario disporre dell’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.
>* Prima di condividere un collegamento con gli utenti, assicurarsi che Day CQ Mail Service sia configurato. In caso contrario, si verifica un errore.


1. Nell’interfaccia utente Risorse, seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Condividi collegamento]**. Nel campo **[!UICONTROL Condividi collegamento]** viene creato automaticamente un collegamento a una risorsa. Copiate questo collegamento e condividetelo con gli utenti. Il tempo di scadenza predefinito per il collegamento è un giorno.

   >[!NOTE]
   >
   >Se una risorsa condivisa viene spostata in un percorso diverso, il collegamento non funziona più. Crea di nuovo il collegamento e condividi nuovamente con gli utenti.

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Scaricare e condividere le risorse {#download-and-share-assets}

Gli utenti possono scaricare alcune risorse e condividerle al di fuori di Experience Manager. Per ulteriori informazioni, consultate [come cercare risorse](/help/assets/search-assets.md), [scaricare risorse](/help/assets/download-assets-from-aem.md)e [scaricare raccolte](manage-collections.md#download-a-collection)

## Condivisione di risorse con creativi professionisti {#share-with-creatives}

Gli addetti al marketing e gli utenti della linea di business possono condividere facilmente le risorse approvate con i loro creativi professionisti che utilizzano,

* **App** desktop AEM: L&#39;app funziona su Windows e Mac. Consultate Panoramica delle app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html). Per sapere in che modo qualsiasi utente desktop autorizzato può accedere facilmente alle risorse condivise, consultate [sfogliare, cercare e visualizzare in anteprima le risorse](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Gli utenti desktop possono creare risorse e condividerle con colleghi utenti di AEM, ad esempio caricando nuove immagini. Consultate [Caricare le risorse tramite l’app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)desktop.

* **Collegamento** risorse Adobe: I creativi professionisti possono cercare e utilizzare le risorse direttamente da Adobe InDesign, Adobe Illustrator e Adobe Photoshop.

## Configurare la condivisione delle risorse {#configure-sharing}

Le diverse opzioni per condividere le risorse richiedono una configurazione specifica e dispongono di prerequisiti specifici.

### Configurare la condivisione dei collegamenti delle risorse {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti. La condivisione di risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili a soggetti esterni senza dover prima accedere a Risorse AEM.

>[!NOTE]
>
>Se desiderate condividere i collegamenti dall&#39;istanza di AEM Author a entità esterne, accertatevi di esporre solo i seguenti URL per `GET` le richieste. Bloccate altri URL per garantire la protezione dell&#39;istanza di AEM Author.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

### Configurare la dimensione massima dei dati {#maxdatasize}

Quando scaricate le risorse dal collegamento condiviso mediante la funzione Condivisione collegamenti, AEM comprime la gerarchia delle risorse dall’archivio e quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che possono essere compressi in un file ZIP, enormi quantità di dati sono soggetti a compressione, il che causa errori di memoria insufficiente in JVM. Per proteggere il sistema da un potenziale attacco di negazione del servizio a causa di questa situazione, potete configurare la dimensione massima dei file scaricati. Se le dimensioni non compresse della risorsa superano il valore configurato, le richieste di download delle risorse vengono rifiutate. Il valore predefinito è 100 MB.

1. Tocca o fai clic sul logo AEM, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Dalla console Web, individua la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** .
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Salva le modifiche.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Abilitare le azioni desktop da utilizzare con l&#39;app desktop {#desktop-actions}

Dall’interfaccia utente di Risorse in un browser, puoi esplorare le posizioni delle risorse o estrarne e aprire la risorsa per la modifica nell’applicazione desktop. Queste opzioni sono denominate azioni desktop e per attivarle, consultate [Attivare le azioni desktop nell’interfaccia](https://docs.adobe.com/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)Web di AEM.

![Abilitare le azioni desktop a essere utilizzate come scelte rapide quando si lavora con l&#39;app desktop](assets/enable_desktop_actions.png)

### Configurazioni per l’utilizzo di Adobe Asset Link {#configure-asset-link}

Adobe Asset Link semplifica la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti. Collega le risorse Adobe Experience Manager (AEM) con le app desktop Creative Cloud Adobe InDesign, Adobe Photoshop e Adobe Illustrator. Il pannello Collegamento risorse di Adobe consente ai creativi di accedere e modificare i contenuti memorizzati in Risorse AEM senza uscire dalle app creative che conoscono maggiormente.

Scopri [come configurare AEM per l’utilizzo con Adobe Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).

## Best practices and troubleshooting {#bestpractices}

* Le cartelle di risorse o le raccolte che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verificate con il vostro amministratore AEM i limiti [di](#maxdatasize) download.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!--
Add content or link about how to share using Brand Portal when it is available on Cloud Service.
-->
