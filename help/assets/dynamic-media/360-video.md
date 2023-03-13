---
title: Video 360/VR
description: Scopri come utilizzare il 360 e il video VR (Virtual Reality) in Dynamic Media.
contentOwner: Rick Brough
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# Video 360/VR {#vr-video}

I video a 360° registrano una vista in ogni direzione contemporaneamente. Le riprese vengono effettuate utilizzando una telecamera omnidirezionale o una serie di telecamere. Durante la riproduzione, su uno schermo piatto, l&#39;utente ha il controllo dell&#39;angolo di visualizzazione; la riproduzione su dispositivi mobili applica di solito i controlli giroscopici incorporati.

Dynamic Media include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Puoi distribuire video 360 utilizzando le estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

È possibile utilizzare il visualizzatore video 360/VR per eseguire il rendering di video equirettangolari. Il risultato è un&#39;esperienza visiva coinvolgente di una stanza, una proprietà, una posizione, un paesaggio, una procedura medica e così via.

L&#39;audio spaziale non è attualmente supportato; se l&#39;audio è mixato in stereo, il bilanciamento (L/R) non cambia quando il cliente cambia l&#39;angolo di visualizzazione della telecamera.

Consulta [Utilizzo di video Dynamic Media 360 e miniatura video personalizzata con AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Vedi anche [Gestione dei predefiniti per i visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md).

## Video in azione a 360° {#video-in-action}

Seleziona [Stazione spaziale 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) per aprire una finestra del browser e guardare un video a 360°. Durante la riproduzione di un video, trascinare il puntatore in una nuova posizione per modificare l&#39;angolo di visualizzazione.

![Fotogramma video da Space Station 360](assets/6_5_360videoiss_simplified.png)
*Fotogramma video da Space Station 360*

## Video e Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

È possibile utilizzare Adobe Premier Pro per visualizzare e modificare il metraggio 360/VR. Ad esempio, potete inserire correttamente loghi e testo in una scena e applicare effetti e transizioni progettati appositamente per gli elementi multimediali equirettangolari.

Consulta [Modifica video 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Carica le risorse da utilizzare con il visualizzatore video 360 {#uploading-assets-for-use-with-the-video-viewer}

360 risorse video caricate in [!DNL Experience Manager] sono etichettati come **Multimedia** su una pagina di risorse, come una normale risorsa video.

![Una risorsa video 360 caricata visualizzata nella vista a schede](assets/6_5_360video-selecttopreview.png)
*Una risorsa video 360 caricata visualizzata nella vista a schede. La risorsa è etichettata come Multimedia.*

**Carica le risorse da utilizzare con il visualizzatore video 360:**

1. È stata creata una cartella dedicata alla risorsa video 360.
1. [Applicare un profilo video adattivo alla cartella](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   Il rendering di contenuti video a 360° richiede requisiti più elevati per la risoluzione del video sorgente e delle rappresentazioni codificate rispetto ai contenuti video standard non a 360°.

   Puoi utilizzare il profilo video adattivo fornito con Dynamic Media. Tuttavia, risulta in una qualità video 360-inferiore rispetto a quella che si otterrebbe per un video non 360 codificato con le stesse impostazioni sottoposte a rendering con un visualizzatore video non 360. Pertanto, se è richiesta una qualità video 360 elevata, effettuare le seguenti operazioni:

   * Idealmente, il contenuto video originale a 360 ha una delle seguenti risoluzioni:

      * 1080p - 1920 x 1080, risoluzione Full HD o FHD oppure
      * 2160p - 3840 x 2160, nota come risoluzione 4k, UHD o HD Ultra. Questa risoluzione elevata del display si trova più spesso su televisori e monitor per computer di alta qualità. La risoluzione 2160p è spesso chiamata &quot;4k&quot; perché la larghezza è vicina a 4000 pixel. In altre parole, offre quattro volte i pixel di 1080p.
   * [Creare un profilo video adattivo personalizzato](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) con rappresentazioni di qualità superiore. Ad esempio, puoi creare un profilo video adattivo contenente le tre impostazioni seguenti:

      * Larghezza=auto; Altezza=720; Bit rate=2500 kbps
      * Larghezza=auto; Altezza=1080; Bit rate=5000 kbps
      * Larghezza=auto; Altezza=1440; Bit rate=6600 kbps
   * Elabora contenuti video 360 in una cartella dedicata esclusivamente alle risorse video 360.

   Questo approccio aumenta le esigenze della rete e della CPU dell&#39;utente finale.

1. [Carica il video nella cartella](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## Anteprima video 360 {#previewing-video}

È possibile utilizzare Anteprima per vedere in che modo il video 360 viene visualizzato ai clienti e assicurarsi che si comporti come previsto.

Vedi anche [Modifica dei predefiniti per i visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

Quando sei soddisfatto del video 360, puoi pubblicarlo.

Consulta [Incorporazione di un visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).
Consulta [Collegamento di URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a [!DNL Experience Manager Sites] pagine.
Consulta [Aggiunta di risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Per visualizzare in anteprima 360 video:**

1. In entrata **[!UICONTROL Risorse]**, passa a un video 360 esistente creato. Per aprirlo in modalità anteprima, seleziona la risorsa Video 360.

   ![Schermata di una risorsa video 360 caricata, come mostrato nella vista a schede di Experience Manager.](assets/6_5_360video-selecttopreview-1.png)

   Per visualizzare l’anteprima del video, seleziona la risorsa video 360.

1. Nella pagina di anteprima, nell’angolo superiore sinistro della pagina, seleziona l’elenco a discesa, quindi fai clic su **[!UICONTROL Visualizzatori]**.

   ![Schermata di selezione dei visualizzatori per visualizzare l’elenco dei visualizzatori video disponibili.](assets/6_5_360video-preview-viewers.png)

   Dall’elenco Visualizzatori, seleziona **[!UICONTROL Video360_social]**, quindi eseguire una delle operazioni seguenti:

   * Per modificare l&#39;angolo di visualizzazione della scena statica, trascinate il puntatore sul video.
   * Per iniziare la riproduzione, seleziona il **[!UICONTROL Play]** pulsante. Durante la riproduzione del video, trascinare il puntatore sul video per modificare l&#39;angolo di visualizzazione.

   ![Schermata di un utente che seleziona il visualizzatore Video360_Social per visualizzare l’anteprima di un video a 360 gradi.](assets/6_5_360video-preview-video360-social.png)*Una schermata di 360 video.*

   * Dall’elenco Visualizzatori, seleziona **[!UICONTROL Video360VR]**.

      Il video VR (Virtual Reality) è un video coinvolgente a cui si accede utilizzando cuffie per realtà virtuale. Come per i video ordinari, puoi creare video VR all’inizio quando un video viene registrato o catturato utilizzando videocamere a 360°.
   ![Schermata di un utente che passa il puntatore del mouse sull&#39;opzione Visualizzatore Video360VR.](assets/6_5_360video-preview-video360vr.png)
   *Una schermata video 360 VR.*

1. Nella parte superiore destra della pagina di anteprima, seleziona **[!UICONTROL Chiudi]**.

## Pubblicazione di video 360 {#publishing-video}

Per utilizzare il video 360, è necessario pubblicarlo. La pubblicazione di un video 360 attiva l’URL e il codice di incorporamento. Pubblica inoltre il video 360 sul cloud Dynamic Media, integrato con una rete CDN per una distribuzione scalabile e performante.

Consulta [Pubblicazione di risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare video a 360°.
Vedi anche [Incorporazione di un visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).
Vedi anche [Collegamento di URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a [!DNL Experience Manager Sites] pagine.
Vedi anche [Aggiunta di risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
