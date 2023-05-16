---
title: Scaricare le risorse
description: Scaricare le risorse da [!DNL Adobe Experience Manager Assets] e abilitare o disabilitare la funzionalità di download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 6%

---

# Scaricare le risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Puoi scaricare le risorse, compresi i rendering statici e dinamici. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono raggruppate in un file ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Non è possibile scaricare i seguenti tipi di risorse: Set di immagini, set 360 gradi, set di file multimediali diversi e set carosello.

Puoi scaricare risorse da Experience Manager utilizzando i seguenti metodi:

<!-- * [Link Share](#link-share-download) -->

* [Interfaccia utente di Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Scaricare le risorse utilizzando [!DNL Experience Manager] interfaccia {#download-assets}

Experience Manager ottimizza l’esperienza di download in base alla quantità e alle dimensioni della risorsa. I file più piccoli vengono scaricati dall’interfaccia utente in tempo reale. [!DNL Experience Manager] scarica direttamente le richieste di risorse singole per il file originale anziché racchiudere singole risorse in un archivio ZIP per velocizzarne il download. Experience Manager supporta download di grandi dimensioni con richieste asincrone. Le richieste di download di dimensioni superiori a 100 GB sono suddivise in più archivi ZIP con una dimensione massima di 100 GB ciascuno.

Per impostazione predefinita, [!DNL Experience Manager] attiva una notifica nel [[!DNL Experience Manager] Inbox](/help/sites-cloud/authoring/getting-started/inbox.md) alla generazione di un archivio di download.

![Notifica casella in entrata](assets/inbox-notification-for-large-downloads.png)


### Abilita notifiche e-mail per download di grandi dimensioni {#enable-emails-for-large-downloads}

I download asincroni vengono attivati in uno dei seguenti casi:

* Se ci sono più di dieci risorse
* Se la dimensione del download è superiore a 100 MB
* Se il download richiede più di 30 secondi per prepararsi

Mentre il download asincrono viene eseguito sul backend , l’utente può continuare a esplorare e lavorare ulteriormente in Experience Manager. Oltre alle notifiche della casella in entrata di Experience Manager, Experience Manager può inviare e-mail per informare l’utente al termine del processo di download. Per abilitare questa funzione, gli amministratori possono configurare il servizio e-mail tramite [configurazione di una connessione server SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Una volta configurato il servizio e-mail, gli amministratori e gli utenti possono abilitare le notifiche e-mail dall’interfaccia di Experience Manager.

Per abilitare le notifiche e-mail:

1. Accedi a [!DNL Experience Manager Assets].
1. Fai clic sull’icona utente nell’angolo in alto a destra, quindi fai clic su **[!UICONTROL Preferenze]** per aprire la finestra Preferenze utente.
1. Seleziona la **[!UICONTROL Notifiche e-mail per il download delle risorse]** seleziona e fai clic su **[!UICONTROL Accetta]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Per scaricare le risorse, effettua le seguenti operazioni:

1. In [!DNL Experience Manager] interfaccia utente, fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa alle risorse da scaricare. Seleziona la cartella o seleziona una o più risorse all’interno della cartella. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.

   ![Opzioni disponibili durante il download delle risorse da [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Nella finestra di dialogo scarica selezionare le opzioni di download desiderate.

   | Opzione di download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per creare una cartella per ogni risorsa contenente tutte le rappresentazioni scaricate per la risorsa. Se questa opzione non è selezionata, ogni risorsa (e le relative rappresentazioni se selezionate per il download) saranno contenute nella cartella principale dell’archivio generato. |
   | **[!UICONTROL E-mail]** | Seleziona questa opzione per inviare una notifica e-mail (contenente un collegamento al download) a un altro utente. L&#39;utente destinatario deve essere membro del gruppo `dam-users` gruppo. I modelli e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>È possibile archiviare modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nel modulo originale.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale include risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Un rendering è la rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere diverse rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata dall’interno di [!DNL Experience Manager]. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni di ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Seleziona questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezioni questa opzione, selezioni anche le rappresentazioni che desideri creare in modo dinamico selezionando dalla [Predefinito immagine](/help/assets/dynamic-media/image-presets.md) elenco. <br>È inoltre possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l&#39;inversione dell&#39;immagine. L’opzione è disponibile solo se è disponibile [!DNL Dynamic Media] abilitato. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

   Se la notifica e-mail è abilitata per i download di grandi dimensioni, nella casella in entrata viene visualizzato un messaggio e-mail contenente l’URL di download della cartella zip archiviata. Fai clic sul collegamento di download dall&#39;e-mail per scaricare l&#39;archivio zip.

   ![e-mail-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   Puoi anche visualizzare la notifica nel tuo [!DNL Experience Manager] Casella in entrata.

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Scaricare le risorse condivise tramite la condivisione dei collegamenti {#link-share-download}

La condivisione di risorse tramite un collegamento è un modo conveniente per renderle disponibili alle persone interessate senza che queste debbano accedere a [!DNL Assets]. Vedi [Funzionalità Condivisione collegamenti](/help/assets/share-assets.md#sharelink).

Quando gli utenti scaricano risorse dai collegamenti condivisi, [!DNL Assets] utilizza un servizio asincrono che offre download più rapidi e ininterrotti. Le risorse da scaricare vengono messe in coda in background in una casella in entrata in archivi ZIP di dimensioni file gestibili. Per i download più grandi, il download viene suddiviso in file da 100 GB.

La [!UICONTROL Scarica casella in entrata] visualizza lo stato di elaborazione di ciascun archivio. Una volta completata l’elaborazione, puoi scaricare gli archivi dalla casella in entrata.

![Scarica casella in entrata](assets/link-sharing-download-inbox.png)

## Abilita il servlet di download delle risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni per creare file ZIP di risorse. La preparazione del download può avere implicazioni di prestazioni o può anche sovraccaricare il server e la rete. Per attenuare tali rischi potenziali simili a quelli di DoS causati da questa funzione, `AssetDownloadServlet` Il componente OSGi è disabilitato per le istanze di pubblicazione. Se non hai bisogno della funzione di download sulle istanze dell&#39;autore, disattiva il servlet sull&#39;autore.

Per consentire il download delle risorse dal tuo DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione del download consentito il più possibile bassa senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Crea una cartella con una convenzione di denominazione per la modalità di esecuzione di pubblicazione, ovvero `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, crea un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti caratteristiche. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattiva il servlet di download delle risorse {#disable-asset-download-servlet}

Se non hai bisogno della funzionalità di download, disattiva il servlet per evitare rischi simili a quelli di DoS. La `Asset Download Servlet` può essere disabilitato su un [!DNL Experience Manager] crea e pubblica le istanze aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download delle risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione del dispatcher, modifica la `dispatcher.any` e aggiungi una nuova regola al [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Suggerimenti e limitazioni {#tips-limitations}

* se si scarica una cartella vuota, [!DNL Experience Manager] trasmette un messaggio di operazione riuscita della creazione di un archivio ZIP, ma l’archivio non viene creato.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
>* [Scaricare risorse utilizzando l’app desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Scaricare le risorse utilizzando il collegamento Risorse di Adobe dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)

