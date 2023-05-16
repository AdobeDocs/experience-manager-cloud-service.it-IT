---
title: Distribuire e condividere risorse, cartelle e raccolte
description: Distribuisci le risorse digitali utilizzando metodi come condivisione come collegamento, download e tramite [!DNL Brand Portal], [!DNL desktop app]e [!DNL Asset Link].
contentOwner: Vishabh Gupta
feature: Asset Management, Collaboration, Asset Distribution
role: User, Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 4%

---

# Condividere e distribuire le risorse gestite in [!DNL Experience Manager] {#share-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte con i membri dell’organizzazione ed entità esterne, inclusi partner e fornitori. Utilizza i seguenti metodi per condividere le risorse da [!DNL Experience Manager Assets] come [!DNL Cloud Service]:

* [Condividi come collegamento](#sharelink).
* [Scaricare le risorse](/help/assets/download-assets-from-aem.md) e condividere separatamente.
* Condividi utilizzando [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it).
* Condividi utilizzando [[!DNL Adobe Asset Link]](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html).
* Condividi utilizzando [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## Condividere le risorse come collegamento {#sharelink}

La condivisione di risorse tramite un collegamento è un modo conveniente per rendere le risorse disponibili a soggetti esterni, esperti di marketing e altri [!DNL Experience Manager] utenti. La funzionalità consente agli utenti anonimi di accedere e scaricare le risorse condivise con loro. Quando si scaricano risorse da un collegamento condiviso, [!DNL Experience Manager Assets] utilizza un servizio asincrono che offre un download più rapido e ininterrotto. Le risorse da scaricare vengono accodate in background in archivi ZIP di dimensioni file gestibili. Per i download di grandi dimensioni, il download viene raggruppato in più file di 100 GB per dimensione del file.

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* È necessario modificare l&#39;autorizzazione ACL sulla cartella o sulla risorsa che si desidera condividere come collegamento.
>* [Abilitare le e-mail in uscita](/help/implementing/developing/introduction/development-guidelines.md#sending-email) prima di condividere un collegamento con gli utenti.


Esistono due modi per condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti:

1. Generare un collegamento condiviso, [copiare e condividere il collegamento alla risorsa](#copy-and-share-assets-link) con altri utenti. La scadenza predefinita del collegamento è di un giorno. Non puoi modificare l’ora di scadenza quando condividi il collegamento copiato con altri utenti.

1. Generare un collegamento condiviso e [condividere il collegamento della risorsa tramite e-mail](#share-assets-link-through-email). In questo caso, puoi modificare i valori predefiniti, ad esempio la data e l’ora di scadenza, e consentire il download delle risorse originali e dei relativi rendering. Puoi inviare e-mail a più utenti aggiungendo i loro indirizzi e-mail.

![Finestra di dialogo Condivisione collegamenti](assets/link-sharing-dialog.png)

### Copiare e condividere il collegamento alla risorsa{#copy-and-share-asset-link}

Per condividere le risorse come URL pubblico:

1. Accedi a [!DNL Experience Manager Assets] e passa a **[!UICONTROL File]**.
1. Seleziona le risorse o la cartella contenente le risorse. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]**.
1. La **[!UICONTROL Condivisione collegamenti]** viene visualizzata una finestra di dialogo contenente un collegamento di risorsa generato automaticamente nel **[!UICONTROL Condividi collegamento]** campo .
1. Copia il collegamento della risorsa e condividetelo con gli utenti.

### Condividi collegamento risorse tramite notifica e-mail {#share-assets-link-through-email}

Per condividere le risorse tramite e-mail:

1. Seleziona le risorse o la cartella contenente le risorse. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]**.
1. La **[!UICONTROL Condivisione collegamenti]** viene visualizzata una finestra di dialogo contenente un collegamento di risorsa generato automaticamente nel **[!UICONTROL Condividi collegamento]** campo .

   * Nella casella Indirizzo e-mail, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Puoi condividere il collegamento con più utenti. Se l’utente è membro dell’organizzazione, seleziona il proprio ID e-mail dai suggerimenti visualizzati nell’elenco a discesa. Se l’utente è esterno, digita l’ID e-mail completo e premi **[!UICONTROL Invio]**; l’ID e-mail viene aggiunto all’elenco degli utenti.

   * In **[!UICONTROL Oggetto]** digitare un oggetto per specificare lo scopo delle risorse condivise.
   * In **[!UICONTROL Messaggio]** digitare un messaggio se necessario.
   * In **[!UICONTROL Scadenza]** utilizza il selettore data per specificare una data e un’ora di scadenza per il collegamento.
   * Abilita la **[!UICONTROL Consenti download del file originale]** casella di controllo per consentire ai destinatari di scaricare il rendering originale.

1. Fai clic su **[!UICONTROL Condividi]**. Un messaggio conferma che il collegamento è condiviso con gli utenti. Gli utenti ricevono un’e-mail contenente il collegamento condiviso.

![E-mail di condivisione dei collegamenti](assets/link-sharing-email-notification.png)

### Scaricare le risorse tramite il collegamento alla risorsa

Qualsiasi utente con accesso al collegamento della risorsa condivisa può scaricare le risorse bundle in una cartella zip. Il processo di download è lo stesso, sia che un utente acceda al collegamento della risorsa copiato, sia che utilizzi il collegamento della risorsa condiviso tramite e-mail.

* Fai clic sul collegamento della risorsa o incolla l’URL nel browser. La [!UICONTROL Condivisione collegamenti] si apre l&#39;interfaccia in cui è possibile passare alla [!UICONTROL Vista a schede] o [!UICONTROL Vista a elenco].

* In [!UICONTROL Vista a schede], puoi passare il cursore del mouse sulla risorsa condivisa o sulla cartella di risorse condivise per selezionarle o accodarle per il download.

* Per impostazione predefinita, l’interfaccia utente mostra **[!UICONTROL Scarica casella in entrata]** opzione . Riflette l&#39;elenco di tutte le risorse o cartelle condivise in coda per il download e il loro stato.

* Quando selezioni le risorse o la cartella, un **[!UICONTROL Download della coda]** sullo schermo viene visualizzata l’opzione . Fai clic sul pulsante **[!UICONTROL Download della coda]** per avviare il processo di download.

   ![Download della coda](assets/queue-download.png)

* Durante la preparazione del file di download, fai clic sul pulsante **[!UICONTROL Scarica casella in entrata]** per visualizzare lo stato del download. Per i download di grandi dimensioni, fai clic sul pulsante **[!UICONTROL Aggiorna]** per aggiornare lo stato.

   ![Scarica casella in entrata](assets/link-sharing-download-inbox.png)

* Al termine dell’elaborazione, fai clic sul pulsante **[!UICONTROL Scarica]** per scaricare il file zip.

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>Se una risorsa condivisa viene spostata in una posizione diversa, il relativo collegamento smette di funzionare. Ricrea il collegamento e condividi nuovamente con gli utenti.


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

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

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

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
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Scaricare le risorse e condividerle separatamente {#download-and-share-assets}

Gli utenti possono scaricare le risorse richieste e condividerle al di fuori di [!DNL Experience Manager]. Per ulteriori informazioni, consulta [come cercare le risorse](/help/assets/search-assets.md), [come scaricare le risorse](/help/assets/download-assets-from-aem.md)e [come scaricare le raccolte](manage-collections.md#download-a-collection)

## Condividere risorse con i creativi {#share-with-creatives}

Gli addetti al marketing e gli utenti della linea di business possono condividere facilmente le risorse approvate con i loro creativi professionisti che utilizzano,

* **app desktop Experience Manager**: L’app funziona su Windows e Mac. Vedi [panoramica dell’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it). Per sapere in che modo qualsiasi utente desktop autorizzato può accedere facilmente alle risorse condivise, consulta [sfogliare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Gli utenti desktop possono creare risorse e condividerle nuovamente con i loro colleghi utenti di Experience Manager, ad esempio caricando nuove immagini. Vedi [caricare risorse utilizzando l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: I creativi professionisti possono cercare e utilizzare le risorse direttamente da [!DNL Adobe InDesign], [!DNL Adobe Illustrator]e [!DNL Adobe Photoshop].

## Configurare la condivisione delle risorse {#configure-sharing}

Le diverse opzioni per la condivisione delle risorse richiedono una configurazione specifica e dispongono di prerequisiti specifici.

### Configurare la condivisione dei collegamenti delle risorse {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Per generare l’URL per le risorse che desideri condividere con gli utenti, utilizza la finestra di dialogo Condivisione collegamenti . Utenti con privilegi di amministratore o con autorizzazioni di lettura all&#39;indirizzo `/var/dam/share` la posizione consente di visualizzare i collegamenti condivisi con i due. La condivisione delle risorse tramite un collegamento è un modo conveniente per rendere le risorse disponibili a soggetti esterni senza che debbano prima accedere a [!DNL Assets].

>[!NOTE]
>
>Se desideri condividere collegamenti dall’istanza di authoring a entità esterne, accertati di esporre solo i seguenti URL per `GET` richieste. Blocca altri URL per garantire la protezione dell’istanza di authoring.
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
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

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Abilitare le azioni desktop da utilizzare con l’app desktop {#desktop-actions}

Da all’interno di [!DNL Assets] interfaccia utente in un browser, puoi esplorare le posizioni delle risorse o estrarre e aprire la risorsa per la modifica nell’applicazione desktop. Queste opzioni sono denominate azioni desktop e per abilitarle consulta [abilita azioni desktop in [!DNL Assets] interfaccia web](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Abilita le azioni desktop da utilizzare come scelte rapide durante l’utilizzo con l’app desktop](assets/enable_desktop_actions.png)

### Configurazioni da utilizzare [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe Asset Link semplifica la collaborazione tra creativi e addetti al marketing nel processo di creazione dei contenuti. Si connette [!DNL Adobe Experience Manager Assets] con [!DNL Creative Cloud] app desktop [!DNL Adobe InDesign], [!DNL Adobe Photoshop]e [!DNL Adobe Illustrator]. La [!DNL Adobe Asset Link] consente ai creativi di accedere e modificare il contenuto memorizzato in [!DNL Assets] senza lasciare le app creative che hanno più familiarità con.

Vedi [come configurare [!DNL Assets] per utilizzarlo con [!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).

## Procedure consigliate e risoluzione dei problemi {#bestpractices}

* Le cartelle o le raccolte di risorse che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, controlla con il tuo amministratore di Experience Manager quali sono i limiti di download. Il valore predefinito è 100 MB.
* Affinché un utente possa visualizzare in anteprima un video condiviso tramite la condivisione dei collegamenti, il video deve avere una rappresentazione video statica disponibile in `/jcr:content/renditions` nel nodo del video nell’archivio. L’anteprima non dipende dalla disponibilità di un [!DNL Dynamic Media] rendering.
* Quando si scarica una risorsa video tramite la condivisione dei collegamenti, la [!DNL Dynamic Media] le rappresentazioni non sono incluse nell&#39;archivio scaricato.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
