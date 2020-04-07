---
title: Scaricare risorse da AEM
description: Scoprite come scaricare risorse da AEM e abilitare o disabilitare la funzionalità di download.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Scaricare risorse da AEM {#download-assets-from-aem}

Potete scaricare le risorse incluse le rappresentazioni statiche e dinamiche. Le risorse scaricate vengono raggruppate in un file ZIP. Il file ZIP compresso ha una dimensione massima di 1 GB per il processo di esportazione. È consentito un massimo di 500 risorse totali per processo di esportazione.

>[!NOTE]
>
>Per poter scaricare le risorse, i membri devono disporre delle autorizzazioni necessarie per avviare flussi di lavoro che attivano il download delle risorse.

Per scaricare le risorse, individuate una risorsa, selezionatela, quindi toccate o fate clic sull’icona **[!UICONTROL Scarica]** dalla barra degli strumenti. Nella finestra di dialogo risultante, specificate le opzioni di download.

Impossibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set file multimediali diversi e Set caroselli.

![Opzioni disponibili quando si scaricano le risorse da Risorse](assets/asset_download_dialog.png)*di AEM: Opzioni disponibili quando si scaricano le risorse da Risorse AEM*

Di seguito sono riportate le opzioni di esportazione/download. Le rappresentazioni dinamiche sono univoche per gli elementi multimediali dinamici e consentono di generare rapidamente rappresentazioni oltre alla risorsa selezionata. Tale opzione è disponibile solo se è stata attivata l’opzione per gli elementi multimediali dinamici.

| Opzioni di esportazione o download | Descrizioni |
|---|---|
| [!UICONTROL Assets] | Selezionate questa opzione per scaricare la risorsa nel modulo originale senza alcuna rappresentazione. |
| [!UICONTROL Rappresentazioni] | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, potete selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
| [!UICONTROL Rendering dinamici] | Una rappresentazione dinamica genera al volo altre rappresentazioni. Quando selezionate questa opzione, potete anche selezionare i rendering da creare in modo dinamico selezionando dall’elenco dei predefiniti per immagini. Potete inoltre selezionare le dimensioni e l’unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine (ad esempio per invertire l’immagine) |
| [!UICONTROL Crea una cartella separata per ogni risorsa] | Selezionate questa opzione per mantenere la gerarchia delle cartelle durante il download delle risorse. Per impostazione predefinita, la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del sistema locale. |

L’opzione di rappresentazione dell’opzione è disponibile se la risorsa dispone di rappresentazioni. L’opzione Risorse secondarie è disponibile se la risorsa include risorse secondarie.

Quando selezionate una cartella da scaricare, viene scaricata l’intera gerarchia di risorse sotto la cartella. Per includere ciascuna risorsa scaricata (incluse le risorse nelle cartelle figlie nidificate sotto la cartella principale) in una singola cartella, selezionate **[!UICONTROL Crea cartella separata per ciascuna risorsa]**.

## Abilita servlet download risorse {#enable-asset-download-servlet}

Il servlet predefinito in AEM consente agli utenti autenticati di emettere richieste di download simultanei di grandi dimensioni per la creazione di file ZIP di risorse visibili agli utenti che possono sovraccaricare il server e la rete. Per attenuare i potenziali rischi DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione.

Per consentire il download delle risorse da DAM, ad esempio quando si utilizza un sistema simile a Asset Share Commons o ad altre implementazioni di tipo portale, è necessario abilitare manualmente il servlet tramite una configurazione OSGi. Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Create una cartella con una convenzione di denominazione per la modalità di esecuzione della pubblicazione, vale a dire `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, create un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Compilate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti opzioni. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattivazione del servlet di download delle risorse {#disable-asset-download-servlet}

È `Asset Download Servlet` possibile disabilitare il dispatcher in un&#39;istanza di AEM Publish aggiornando la configurazione del dispatcher per bloccare qualsiasi richiesta di download di risorse. Il servlet può anche essere disattivato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione dispatcher, modifica la `dispatcher.any` configurazione e aggiungi una nuova regola alla sezione [](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtro.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
>* [Scaricare risorse dall’app desktop AEM su Windows o Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Scaricare risorse tramite il collegamento Adobe Assets dall&#39;interno delle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)


<!-- FULL ARTICLE ARCHIVE IS BELOW 

You can download assets including static and dynamic renditions. Alternatively, you can send emails with links to assets directly from AEM Assets. Downloaded assets are bundled in a ZIP file. The compressed ZIP file has a maximum file size of 1 GB for the export job. You are allowed a maximum of 500 total assets per export job.

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.

To download assets, navigate to an asset, select the asset, and tap/click the **[!UICONTROL Download]** icon from the toolbar. In the resulting dialog, specify your download options.

The asset types Image Sets, Spin Sets, Mixed Media Sets, and Carousel Sets cannot be downloaded.

![Available options when downloading assets from AEM Assets](assets/asset_download_dialog.png)
*Figure: Available options when downloading assets from AEM Assets*

The following are the Export/Download options. Dynamic renditions are unique to Dynamic Media and let you generate renditions on-the-fly in addition to the asset you selected - that option is only available if you have Dynamic Media enabled.

|Export or download options|Descriptions|
|---|---|
| [!UICONTROL Assets]| Select this to download the asset in its original form without any renditions.|
| [!UICONTROL Renditions] |A rendition is the binary representation of an asset. Assets have a primary representation - that of the uploaded file. They can have any number of representations. <br> With this option, you can select the renditions you want downloaded. The renditions available depend on the asset you select.|
| [!UICONTROL Dynamic Renditions] |A dynamic rendition generates other renditions on-the-fly. When you select this option, you also select the renditions you want to create dynamically by selecting from the image presets list. In addition, you can select the size and unit of measurement, format, color space, resolution, and any image modifiers (for example to invert the image)|
| [!UICONTROL Email] |An email notification is sent to the user. Standard emails templates are available at the following locations:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Templates that you customize during deployment should be present at these locations: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>You can store tenant-specific custom templates at these locations:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>|
| [!UICONTROL Create separate folder for each asset] |Select this to preserve the folder hierarchy while downloading assets. By default, the folder hierarchy is ignored and all assets are downloaded in one folder in your local system.|

The option renditions option is available if the asset has any renditions. The subassets option is available if the asset includes subassets.

When you select a folder to download, the complete asset hierarchy under the folder is downloaded. To include each asset you download (including assets in child folders nested under the parent folder) in an individual folder, select **[!UICONTROL Create separate folder for each asset]**.

## Enable asset download servlet {#enable-asset-download-servlet}

The default servlet in AEM allows authenticated users to issue arbitrarily-large, concurrent download requests for creating ZIP files of assets visible to them that can overload the server and the network. To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

To allow downloading assets from your DAM, say when using something like Asset Share Commons or other portal-like implementation, manually enable the servlet via an OSGi configuration. Adobe recommends setting the permissible download size as low as possible without affecting the day-to-day download requirements. A high value may impact performance.

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Sets a maximum size (in bytes) for the download as value of `asset.download.prezip.maxcontentsize`. The below sample configures the maximum size of the ZIP download to not exceed 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. The servlet can also be manually disabled via the OSGi console directly.

1. To block asset download requests via a dispatcher configuration edit the `dispatcher.any` configuration and add a new rule to the [filter section](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Download DRM protected assets](drm.md)
>* [Download assets using AEM desktop app on Win or Mac desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Download assets using Adobe Assets Link from within the supported Adobe Creative Cloud apps](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


-->