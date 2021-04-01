---
title: Condividere risorse, cartelle e raccolte come collegamento
description: Questo articolo descrive come condividere risorse, cartelle e raccolte all'interno di [!DNL Experience Manager Assets] come collegamento ipertestuale.
contentOwner: AG
feature: Gestione risorse, collaborazione, distribuzione delle risorse
role: Business Practices, Amministratore
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---


# Condividere e distribuire le risorse gestite in [!DNL Experience Manager] {#share-assets-from-aem}

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte con i membri dell’organizzazione ed entità esterne, inclusi partner e fornitori. Utilizza i seguenti metodi per condividere risorse da [!DNL Experience Manager Assets] come [!DNL Cloud Service]:

* Condividi come collegamento.
* Scarica le risorse e condividi separatamente.
* Condividi tramite app desktop AEM.
* Condividi tramite Adobe Asset Link.
* (Funzionalità in arrivo) Condividi tramite Brand Portal.

## Condividere le risorse come collegamento {#sharelink}

Per generare l’URL per le risorse che desideri condividere con gli utenti, utilizza la finestra di dialogo Condivisione collegamenti . Gli utenti con privilegi di amministratore o con autorizzazioni di lettura nel percorso `/var/dam/share` possono visualizzare i collegamenti condivisi con loro. La condivisione di risorse tramite un collegamento è un modo conveniente per rendere le risorse disponibili a soggetti esterni senza che debbano prima accedere a [!DNL Assets].

>[!NOTE]
>
>* È necessario modificare l&#39;autorizzazione ACL sulla cartella o sulla risorsa che si desidera condividere come collegamento.
>* Prima di condividere un collegamento con gli utenti, accertati che [e-mail in uscita sia abilitata](/help/implementing/developing/introduction/development-guidelines.md#sending-email). In caso contrario, si verifica un errore.


1. Nell’interfaccia utente di [!DNL Assets] , seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]**. Un collegamento a una risorsa viene creato automaticamente nel campo **[!UICONTROL Condividi collegamento]** . Copia questo collegamento e condividilo con gli utenti. Il tempo di scadenza predefinito per il collegamento è un giorno.

   >[!NOTE]
   >
   >Se una risorsa condivisa viene spostata in una posizione diversa, il relativo collegamento smette di funzionare. Ricrea il collegamento e condividi nuovamente con gli utenti.

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

## Scaricare e condividere risorse {#download-and-share-assets}

Gli utenti possono scaricare le risorse richieste e condividerle al di fuori di [!DNL Experience Manager]. Per ulteriori informazioni, consulta [come cercare le risorse](/help/assets/search-assets.md), [come scaricare le risorse](/help/assets/download-assets-from-aem.md) e [come scaricare le raccolte](manage-collections.md#download-a-collection)

## Condividere risorse con i creativi {#share-with-creatives}

Gli addetti al marketing e gli utenti della linea di business possono condividere facilmente le risorse approvate con i loro creativi professionisti che utilizzano,

* **Experience Manager di app** desktop: L’app funziona su Windows e Mac. Consulta [panoramica dell’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). Per sapere in che modo qualsiasi utente desktop autorizzato può accedere facilmente alle risorse condivise, consulta [sfogliare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Gli utenti desktop possono creare risorse e condividerle nuovamente con i loro colleghi che sono utenti AEM, ad esempio, caricando nuove immagini. Consulta [caricare le risorse utilizzando l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: I professionisti creativi possono cercare e utilizzare le risorse direttamente da  [!DNL Adobe InDesign],  [!DNL Adobe Illustrator] e  [!DNL Adobe Photoshop].

## Configurare la condivisione delle risorse {#configure-sharing}

Le diverse opzioni per la condivisione delle risorse richiedono una configurazione specifica e dispongono di prerequisiti specifici.

### Configurare la condivisione dei collegamenti alle risorse {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Per generare l’URL per le risorse che desideri condividere con gli utenti, utilizza la finestra di dialogo Condivisione collegamenti . Gli utenti con privilegi di amministratore o con autorizzazioni di lettura nel percorso `/var/dam/share` possono visualizzare i collegamenti condivisi con loro. La condivisione di risorse tramite un collegamento è un modo conveniente per rendere le risorse disponibili a soggetti esterni senza che debbano prima accedere a [!DNL Assets].

>[!NOTE]
>
>Se desideri condividere collegamenti dall’istanza di authoring a entità esterne, assicurati di esporre solo i seguenti URL per le richieste `GET` . Blocca altri URL per garantire la protezione dell’istanza di authoring.
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

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, AEM compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the AEM logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Abilitare le azioni desktop da utilizzare con l’app desktop {#desktop-actions}

Dall’interno dell’interfaccia utente di [!DNL Assets] in un browser, puoi esplorare le posizioni delle risorse o estrarre e aprire la risorsa per la modifica nell’applicazione desktop. Queste opzioni sono denominate azioni desktop e per abilitarle, consulta [abilitare le azioni desktop in [!DNL Assets] interfaccia web](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Abilita le azioni desktop da utilizzare come scelte rapide durante l’utilizzo con l’app desktop](assets/enable_desktop_actions.png)

### Configurazioni da utilizzare [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe Asset Link semplifica la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. Connette [!DNL Adobe Experience Manager Assets] con [!DNL Creative Cloud] app desktop [!DNL Adobe InDesign], [!DNL Adobe Photoshop] e [!DNL Adobe Illustrator]. Il pannello [!DNL Adobe Asset Link] consente ai creativi di accedere e modificare i contenuti memorizzati in [!DNL Assets] senza lasciare le app creative con cui hanno più familiarità.

Vedi [come configurare [!DNL Assets] per utilizzarlo con [!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).

## Procedure consigliate e risoluzione dei problemi {#bestpractices}

* Le cartelle o le raccolte di risorse che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verifica con l&#39;amministratore AEM quali sono i limiti di download [a1/>.](#maxdatasize)
* Affinché un utente possa visualizzare in anteprima un video condiviso tramite la condivisione dei collegamenti, è necessario che il video disponga di un rendering video statico disponibile nella posizione `/jcr:content/renditions` nel nodo del video nell’archivio. L’anteprima non dipende dalla disponibilità di un rendering [!DNL Dynamic Media].
* Quando si scarica una risorsa video tramite la condivisione dei collegamenti, le rappresentazioni [!DNL Dynamic Media] non sono incluse nell’archivio scaricato.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->
