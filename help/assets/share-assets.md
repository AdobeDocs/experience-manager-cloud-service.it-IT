---
title: Distribuire e condividere risorse, cartelle e raccolte
description: Distribuisci le risorse digitali utilizzando metodi come share as a link, download e via [!DNL Brand Portal], [!DNL desktop app], and [!DNL Asset Link].
feature: Asset Management, Collaboration, Asset Distribution
role: Admin, User
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1875'
ht-degree: 4%

---

# Condividi e distribuisci le risorse gestite in [!DNL Experience Manager] {#share-assets-from-aem}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte con membri dell&#39;organizzazione ed entità esterne, inclusi partner e fornitori. Utilizzare i metodi seguenti per condividere risorse da [!DNL Experience Manager Assets] come [!DNL Cloud Service]:

* [Condividi come collegamento](#sharelink).
* [Scarica le risorse](/help/assets/download-assets-from-aem.md) e condividile separatamente.
* Condividi con [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it).
* Condividi con [[!DNL Adobe Asset Link]](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html).
* Condividi con [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## Prerequisiti {#prerequisites}

Sono necessari privilegi di amministratore per [configurare le impostazioni per la condivisione di risorse come collegamento](#config-link-share-settings).

## Configurare le impostazioni di condivisione dei collegamenti {#config-link-share-settings}

[!DNL Experience Manager Assets] consente di configurare le impostazioni predefinite della condivisione di collegamenti.

1. Fai clic sul logo [!DNL Experience Manager], quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Configurazione Assets]** > **[!UICONTROL Condivisione collegamenti]**.
1. Impostazioni iniziali:

   * **Includi originali:**

      * Selezionare `Select Include Originals` per selezionare l&#39;opzione `Include Originals` per impostazione predefinita nella finestra di dialogo di condivisione del collegamento.
      * Selezionare la modalità di presentazione dell&#39;opzione `Include Originals` nella finestra di dialogo Condivisione collegamenti. [!UICONTROL Modificabile] consente all&#39;utente di modificare le impostazioni qui definite nelle impostazioni iniziali. Con `Read-only` l&#39;impostazione viene visualizzata ma non può essere modificata. `Hidden` nasconde l&#39;impostazione e utilizza il valore configurato qui nelle impostazioni iniziali.
   * **Includi rappresentazioni:**
      * Selezionare l&#39;opzione `Select Include Renditions` per selezionare l&#39;opzione `Include Renditions` per impostazione predefinita nella finestra di dialogo Condivisione collegamento.
      * Selezionare la modalità di presentazione dell&#39;opzione `Include Renditions` nella finestra di dialogo Condivisione collegamenti. [!UICONTROL Modificabile] consente all&#39;utente di modificare le impostazioni qui definite nelle impostazioni iniziali. Con `Read-only` l&#39;impostazione viene visualizzata ma non può essere modificata. `Hidden` nasconde l&#39;impostazione e utilizza il valore configurato qui nelle impostazioni iniziali.

1. Specificare il periodo di validità predefinito per il collegamento nel campo `Validity Period` della sezione `Expiration date`.

1. Pulsante **[!UICONTROL Condivisione collegamento]** nella barra delle azioni:
   * Tutti gli utenti con autorizzazioni `jcr:modifyAccessControl` possono visualizzare l&#39;opzione [!UICONTROL Condivisione collegamenti]. Per impostazione predefinita, è visibile a tutti gli amministratori. Per impostazione predefinita, il pulsante [!UICONTROL Condivisione collegamento] è visibile a tutti. È possibile configurare per visualizzare questa opzione solo per i gruppi definiti oppure negarla a gruppi specifici. Selezionare `Allow only for groups` per consentire a gruppi specifici di visualizzare l&#39;opzione `Share Link`. Selezionare `Deny from groups` per negare l&#39;opzione `Share Link` da gruppi specifici. Dopo aver selezionato una di queste opzioni, specificare i nomi dei gruppi utilizzando il campo `Select Groups` per aggiungere i nomi dei gruppi da consentire o negare.

Per le impostazioni relative alla configurazione e-mail, visita la [documentazione del servizio e-mail](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/email-service.html)

![Configura servizio e-mail](/help/assets/assets/config-email-service.png)

## Condividere le risorse come collegamento {#sharelink}

La condivisione delle risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili a parti esterne, addetti al marketing e altri utenti di [!DNL Experience Manager]. Questa funzionalità consente agli utenti anonimi di accedere e scaricare le risorse condivise con loro. Quando si scaricano risorse da un collegamento condiviso, [!DNL Experience Manager Assets] utilizza un servizio asincrono che offre un download più rapido e ininterrotto. Le risorse da scaricare vengono accodate in background in archivi ZIP di dimensioni file gestibili. Per i download di grandi dimensioni, il download è raggruppato in più file di 100 GB per file di dimensioni.

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* È necessario disporre dell’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.
>* [Abilita le e-mail in uscita](/help/implementing/developing/introduction/development-guidelines.md#sending-email) prima di condividere un collegamento con gli utenti.

Esistono due modi per condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti:

1. Genera un collegamento condiviso, [copia e condividi il collegamento della risorsa](#copy-and-share-assets-link) con altri utenti.
1. Genera un collegamento condiviso e [condividi il collegamento della risorsa tramite e-mail](#share-assets-link-through-email). Puoi modificare i valori predefiniti, ad esempio data e ora di scadenza, e consentire di scaricare le risorse originali e le relative rappresentazioni. Puoi inviare e-mail a più utenti aggiungendo i loro indirizzi e-mail.

   ![Finestra di dialogo Condivisione collegamenti](assets/share-link.png)

In entrambi i casi, puoi modificare i valori predefiniti, ad esempio data e ora di scadenza, e consentire il download delle risorse originali e delle relative rappresentazioni.

### Copiare e condividere il collegamento della risorsa{#copy-and-share-asset-link}

Per condividere le risorse come URL pubblico:

1. Accedere a [!DNL Experience Manager Assets] e passare a **[!UICONTROL File]**.
1. Seleziona le risorse o la cartella contenente le risorse. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]**.
1. Viene visualizzata la finestra di dialogo **[!UICONTROL Condivisione collegamenti]** che contiene un collegamento di risorsa generato automaticamente nel campo **[!UICONTROL Condividi collegamento]**.
1. Imposta la data di scadenza del collegamento condiviso come richiesto.
1. In **[!UICONTROL Impostazioni collegamento]**, selezionare o deselezionare `Include Originals` o `Include Renditions` per includere o escludere uno dei due. È obbligatorio scegliere almeno l’opzione.
1. I nomi dell&#39;Assets selezionato vengono visualizzati nella colonna di destra della finestra di dialogo [!DNL Share Link].
1. Copia il collegamento della risorsa e condividilo con gli utenti.

### Condividere il collegamento delle risorse tramite notifica e-mail {#share-assets-link-through-email}

Per condividere le risorse tramite e-mail:

1. Seleziona le risorse o la cartella contenente le risorse. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]**.
1. Viene visualizzata la finestra di dialogo **[!UICONTROL Condivisione collegamenti]** che contiene un collegamento di risorsa generato automaticamente nel campo **[!UICONTROL Condividi collegamento]**.

   * Nella casella dell’indirizzo e-mail digita l’indirizzo e-mail dell’utente con cui vuoi condividere il collegamento. Puoi condividere il collegamento con più utenti. Se l’utente è membro dell’organizzazione, seleziona il proprio indirizzo e-mail dai suggerimenti visualizzati nell’elenco a discesa. Nel campo di testo dell&#39;indirizzo di posta elettronica digitare l&#39;indirizzo di posta elettronica dell&#39;utente con cui si desidera condividere il collegamento e fare clic su [!UICONTROL Invio]. Puoi condividere il collegamento con più utenti.

   * Nella casella **[!UICONTROL Oggetto]** digitare un oggetto per specificare lo scopo delle risorse condivise.
   * Nella casella **[!UICONTROL Messaggio]** digitare un messaggio, se necessario.
   * Nel campo **[!UICONTROL Scadenza]**, utilizza il selettore data per specificare una data e un&#39;ora di scadenza per il collegamento.
   * Abilitare la casella di controllo **[!UICONTROL Consenti download del file originale]** per consentire ai destinatari di scaricare la copia trasformata originale.

1. Fai clic su **[!UICONTROL Condividi]**. Un messaggio conferma che il collegamento è condiviso con gli utenti. Gli utenti ricevono un messaggio e-mail contenente il collegamento condiviso.

   ![E-mail condivisione collegamenti](assets/link-sharing-email-notification.png)

### Personalizza modello e-mail {#customize-email-template}

Un modello ben progettato trasmette professionalità e competenza, migliorando la credibilità del messaggio e della tua organizzazione. [!DNL Adobe Experience Manager] ti consente di personalizzare il modello di e-mail, che viene inviato ai destinatari che ricevono l&#39;e-mail contenente il collegamento condiviso. Inoltre, i modelli e-mail personalizzati consentono di personalizzare il contenuto delle e-mail rivolgendosi ai destinatari con il nome e facendo riferimento a dettagli specifici pertinenti. Questo contatto personale può far sentire apprezzato il destinatario e aumentarne il coinvolgimento. Inoltre, un modello personalizzato garantisce che le e-mail siano coerenti con la tua identità del brand, inclusi logo, colori e font. La coerenza rafforza il riconoscimento del brand e la fiducia tra i destinatari.

#### Formato di un modello e-mail personalizzato {#format-of-custom-email-template}

Il modello e-mail può essere personalizzato utilizzando testo normale o HTML. Il collegamento predefinito al modello modificabile si trova in `/libs/settings/dam/adhocassetshare/en.txt`. È possibile sostituire il modello creando il file `/apps/settings/dam/adhocassetshare/en.txt`. Puoi modificare il modello e-mail il numero di volte necessario.

| Segnaposto | Descrizione |
|---|-----|
| `${emailSubject}` | Oggetto di un messaggio e-mail |
| `${emailInitiator}` | ID e-mail dell’utente che ha creato l’e-mail |
| `${emailMessage}` | Corpo dell’e-mail |
| `${pagePath}` | URL del collegamento condiviso |
| `${linkExpiry}` | Data di scadenza del collegamento condiviso |

<!--| `${host.prefix}` | Origin of the [!DNL Experience Manager] instance, for example `http://www.adobe.com"` |-->

#### Esempio di modello e-mail personalizzato {#custom-email-template-example}

```
subject: ${emailSubject}

<!DOCTYPE html>
<html><body>
<p><strong>${emailInitiator}</strong> invited you to review assets.</p>
<p>${emailMessage}</p>
<p>The shared link will be available until ${linkExpiry}.
<p>
    <a href="${pagePath}" target="_blank"><strong>Open</strong></a>
</p>

</body></html>
```

<!--Sent from instance: ${host.prefix}-->

### Scaricare le risorse utilizzando il collegamento alle risorse {#download-assets-using-asset-link}

Qualsiasi utente che abbia accesso al collegamento della risorsa condivisa può scaricare le risorse incluse in una cartella zip. Il processo di download è lo stesso, sia che un utente acceda al collegamento della risorsa copiato, sia che utilizzi il collegamento della risorsa condiviso tramite l’e-mail.

* Fai clic sul collegamento della risorsa o incolla l’URL nel browser. Viene aperta l&#39;interfaccia [!UICONTROL Condivisione collegamenti] in cui è possibile passare alla [!UICONTROL Vista a schede] o alla [!UICONTROL Vista a elenco].

* Nella [!UICONTROL Vista a schede], puoi passare il cursore del mouse sulla cartella delle risorse condivise o sulla cartella delle risorse condivise per selezionare le risorse o metterle in coda per il download.

* Per impostazione predefinita, nell&#39;interfaccia utente viene visualizzata l&#39;opzione **[!UICONTROL Scarica cartella Posta in arrivo]**. Riflette l’elenco di tutte le risorse o cartelle condivise che sono in coda per il download e il loro stato.

* Quando selezioni le risorse o la cartella, sullo schermo viene visualizzata l&#39;opzione **[!UICONTROL Download coda]**. Fare clic sull&#39;opzione **[!UICONTROL Download coda]** per avviare il processo di download.

  ![Download coda](assets/queue-download.png)

* Durante la preparazione del file di download, fare clic sull&#39;opzione **[!UICONTROL Scarica cartella Posta in arrivo]** per visualizzare lo stato del download. Per i download di grandi dimensioni, fare clic sul pulsante **[!UICONTROL Aggiorna]** per aggiornare lo stato.

  ![Scarica casella in entrata](assets/link-sharing-download-inbox.png)

* Al termine dell&#39;elaborazione, fare clic sul pulsante **[!UICONTROL Scarica]** per scaricare il file zip.

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>Se una risorsa condivisa viene spostata in una posizione diversa, il relativo collegamento non funziona più. Ricrea il collegamento e condividilo nuovamente con gli utenti.


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

Gli utenti possono scaricare le risorse richieste e condividerle all&#39;esterno di [!DNL Experience Manager]. Per ulteriori informazioni, consulta [come cercare le risorse](/help/assets/search-assets.md), [come scaricare le risorse](/help/assets/download-assets-from-aem.md) e [come scaricare le raccolte](manage-collections.md#download-a-collection)

## Condividere risorse con i professionisti della creatività {#share-with-creatives}

Gli addetti al marketing e gli utenti del settore possono condividere con facilità le risorse approvate con i loro creativi utilizzando,

* **App desktop Experience Manager**: l&#39;app funziona su Windows e Mac. Vedi [Panoramica dell&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it). Per sapere in che modo un utente desktop autorizzato può accedere facilmente alle risorse condivise, consulta [Sfogliare, cercare e visualizzare in anteprima le risorse](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Gli utenti desktop possono creare risorse e condividerle nuovamente con le controparti che sono utenti di Experience Manager, ad esempio, caricando nuove immagini. Consulta [caricare risorse tramite un&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: i professionisti della creatività possono cercare e utilizzare le risorse direttamente da [!DNL Adobe InDesign], [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop].

## Configurare la condivisione delle risorse {#configure-sharing}

Le diverse opzioni per la condivisione delle risorse richiedono una configurazione specifica e prerequisiti specifici.

### Configurare la condivisione dei collegamenti delle risorse {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Per generare l’URL per le risorse da condividere con gli utenti, utilizza la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura nel percorso `/var/dam/share` possono visualizzare i collegamenti condivisi con loro. La condivisione delle risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili alle parti esterne senza dover prima accedere a [!DNL Assets].

>[!NOTE]
>
>Se desideri condividere i collegamenti dall&#39;istanza di authoring alle entità esterne, accertati di esporre solo i seguenti URL per le richieste `GET`. Blocca altri URL per garantire la protezione dell’istanza di authoring.
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`

<!--
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password
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

### Abilita le azioni desktop da utilizzare con l’app desktop {#desktop-actions}

Dall&#39;interfaccia utente di [!DNL Assets] in un browser, puoi esplorare i percorsi delle risorse o estrarle e aprire la risorsa per la modifica nell&#39;applicazione desktop. Queste opzioni sono denominate azioni desktop e per abilitarle, vedi [abilitare le azioni desktop nell&#39;interfaccia Web [!DNL Assets] 2}.](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)

![Abilita le azioni desktop da utilizzare come collegamento quando si lavora con l&#39;app desktop](assets/enable_desktop_actions.png)

### Configurazioni da utilizzare [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe Asset Link semplifica la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti. Connette [!DNL Adobe Experience Manager Assets] con [!DNL Creative Cloud] app desktop, [!DNL Adobe InDesign], [!DNL Adobe Photoshop] e [!DNL Adobe Illustrator]. Il pannello [!DNL Adobe Asset Link] consente ai creativi di accedere e modificare il contenuto archiviato in [!DNL Assets] senza uscire dalle app creative che hanno più familiarità con.

Consulta [come configurare [!DNL Assets] per utilizzarlo con [!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html).

## Best practice e risoluzione dei problemi {#bestpractices}

* Le cartelle o le raccolte di risorse il cui nome contiene uno spazio vuoto potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verifica con il tuo amministratore Experience Manager quali sono i limiti di download. Il valore predefinito è 100 MB.
* Per consentire a un utente di visualizzare in anteprima un video condiviso tramite la condivisione di collegamenti, è necessario che nel video sia disponibile una rappresentazione video statica nella posizione `/jcr:content/renditions` nel nodo del video nell&#39;archivio. L&#39;anteprima non dipende dalla disponibilità di una rappresentazione [!DNL Dynamic Media].
* Quando si scarica una risorsa video tramite condivisione collegamenti, le rappresentazioni [!DNL Dynamic Media] non vengono incluse nell&#39;archivio scaricato.

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
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

