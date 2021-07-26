---
title: Scaricare le risorse
description: Scarica le risorse da  [!DNL Adobe Experience Manager Assets] e abilita o disabilita la funzionalità di download.
contentOwner: AG
feature: Gestione risorse
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 2f9e8c00674979c4a245d410b68fd99c60eccfb4
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---

# Scaricare risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puoi scaricare le risorse, compresi i rendering statici e dinamici. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono raggruppate in un file ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

>[!NOTE]
>
>I destinatari delle e-mail devono essere membri del gruppo `dam-users` per accedere al collegamento di download ZIP nel messaggio e-mail. Per poter scaricare le risorse, i membri devono disporre delle autorizzazioni per avviare flussi di lavoro che attivano il download delle risorse.

Non è possibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

Per scaricare le risorse di Experience Manager, utilizza i seguenti metodi:

<!-- * [Link Share](#link-share-download) -->

* [Interfaccia utente di Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Scaricare le risorse utilizzando l’interfaccia [!DNL Experience Manager] {#download-assets}

Il servizio di download asincrono fornisce un framework per il download senza soluzione di continuità delle risorse di grandi dimensioni. I file più piccoli vengono scaricati dall’interfaccia utente in tempo reale. [!DNL Experience Manager] non archivia i download di singole risorse in cui viene scaricato il file originale. Questa funzionalità consente download più veloci. I file di grandi dimensioni vengono scaricati in modo asincrono e [!DNL Experience Manager] notifica il completamento tramite notifiche nella casella in entrata. Consultare [Comprendere [!DNL Experience Manager] Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md).

![Notifica di download](assets/download-notification.png)

*Figura: Scarica la notifica tramite  [!DNL Experience Manager] Casella in entrata.*

I download asincroni vengono attivati in uno dei seguenti casi:

* Se sono presenti più di 10 risorse o più di 100 MB da scaricare.
* Se il download richiede più di 30 secondi per la preparazione.

Per scaricare le risorse, effettua le seguenti operazioni:

1. Nell&#39;interfaccia utente [!DNL Experience Manager] fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa alle risorse da scaricare. Seleziona la cartella o seleziona una o più risorse all’interno della cartella. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.

   ![Opzioni disponibili durante il download delle risorse da  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Figura: Opzioni della finestra di dialogo Scarica.*

1. Nella finestra di dialogo scarica selezionare le opzioni di download desiderate.

   | Opzione di download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per includere ogni risorsa scaricata, incluse le risorse in cartelle secondarie nidificate sotto la cartella padre della risorsa, in un’unica cartella sul computer locale. Quando questa opzione è *not* , seleziona, per impostazione predefinita, la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del computer locale. |
   | **[!UICONTROL E-mail]** | Seleziona questa opzione per far sì che al destinatario venga inviata una notifica e-mail. I modelli e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>È possibile archiviare modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nel modulo originale senza rendering.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale include risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere diverse rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata dall’interno di [!DNL Experience Manager]. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni di ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Seleziona questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezioni questa opzione, selezioni anche i rendering che desideri creare in modo dinamico selezionando dall&#39;elenco [Predefinito immagine](/help/assets/dynamic-media/image-presets.md). <br>È inoltre possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l&#39;inversione dell&#39;immagine. L’opzione è disponibile solo se è stato abilitato [!DNL Dynamic Media] . |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

## Scaricare le risorse condivise tramite la condivisione dei collegamenti {#link-share-download}

>[!NOTE]
>
>Questa funzionalità è disponibile nel canale prerelease di Experience Manager.

La condivisione di risorse tramite un collegamento è un modo conveniente per renderle disponibili alle persone interessate senza che queste debbano prima accedere a [!DNL Assets]. Per generare un URL per la condivisione delle risorse, utilizza la funzionalità [Condivisione collegamenti](/help/assets/share-assets.md#sharelink).

Quando gli utenti scaricano le risorse dai collegamenti condivisi, [!DNL Assets] utilizza un servizio asincrono che offre download più rapidi e ininterrotti. Le risorse da scaricare vengono messe in coda in background in una casella in entrata in archivi ZIP di dimensioni file gestibili. Per i download di grandi dimensioni, il download viene suddiviso in file di dimensioni pari a 100 GB.

Nella casella in entrata viene visualizzato lo stato di elaborazione di ciascun archivio. Una volta completata l’elaborazione, puoi scaricare gli archivi dalla casella in entrata.

![Scarica casella in entrata](assets/download-inbox.png)

## Abilita il servlet di download delle risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni arbitrarie per creare file ZIP di risorse. La preparazione del download può avere implicazioni di prestazioni o può anche sovraccaricare il server e la rete. Per attenuare i rischi simili a DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per le istanze di pubblicazione. Se non hai bisogno della funzione di download sulle istanze dell&#39;autore, disattiva il servlet sull&#39;autore.

Per consentire il download delle risorse dal tuo DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione del download consentito il più possibile bassa senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Crea una cartella con una convenzione di denominazione che esegue il targeting della modalità di esecuzione di pubblicazione, ovvero `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, crea un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Compila `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con quanto segue. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP in modo che non superi 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattiva il servlet di download delle risorse {#disable-asset-download-servlet}

Se non hai bisogno della funzionalità di download, disattiva il servlet per evitare rischi simili a quelli di DoS. È possibile disabilitare `Asset Download Servlet` in un’istanza di authoring e pubblicazione [!DNL Experience Manager] aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download delle risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione del dispatcher, modifica la configurazione `dispatcher.any` e aggiungi una nuova regola alla sezione [filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
* [Scaricare risorse utilizzando l’app desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
* [Scaricare le risorse utilizzando il collegamento Risorse di Adobe dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)

