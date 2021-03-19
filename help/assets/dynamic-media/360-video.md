---
title: Video 360/VR
description: Scopri come lavorare con i video 360 e Virtual Reality (VR) in Dynamic Media.
feature: Video VR a 360°
topic: Professionista
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---


# Video 360/VR {#vr-video}

I video a 360 gradi registrano contemporaneamente una visualizzazione in ogni direzione. Le riprese vengono effettuate con una telecamera omnidirezionale o con una serie di telecamere. Durante la riproduzione, su un display piatto, l&#39;utente ha il controllo dell&#39;angolo di visione; la riproduzione su dispositivi mobili di solito applica i loro controlli giroscopici incorporati.

Dynamic Media include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. È possibile distribuire video 360 utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

Puoi usare il visualizzatore video 360/VR per riprodurre video equirettangolari. Il risultato è un&#39;esperienza di visione immersiva di una stanza, proprietà, posizione, paesaggio, procedura medica e così via.

L&#39;audio spaziale non è attualmente supportato; se l&#39;audio è mixato in stereo, il bilanciamento (L/R) non cambia quando il cliente cambia l&#39;angolo di visione della telecamera.

Consulta [Utilizzo di video Dynamic Media 360 e miniatura video personalizzata con AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Consulta anche [Gestione dei predefiniti per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Video in azione {#video-in-action}

Toccare [Stazione Spaziale 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) per aprire una finestra del browser e guardare un video a 360 gradi. Durante la riproduzione del video, trascinare il puntatore in una nuova posizione per modificare l’angolo di visualizzazione.

![360 Video ](assets/6_5_360videoiss_simplified.png)
*campioneFrame video da Space Station 360*

## Video e Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

È possibile utilizzare Adobe Premier Pro per visualizzare e modificare le riprese a 360/VR. Ad esempio, è possibile inserire correttamente loghi e testo in una scena e applicare effetti e transizioni progettati appositamente per i supporti equirettangolari.

Vedi [Modifica video 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Caricamento delle risorse da utilizzare con il visualizzatore video 360 {#uploading-assets-for-use-with-the-video-viewer}

360 risorse video caricate in Experience Manager sono etichettate come **Multimedia** in una pagina delle risorse, in modo simile alla normale risorsa video.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selecttopreviewUna risorsa video 360 caricata visualizzata nella vista a schede. La risorsa è etichettata come Multimedia.*

**Per caricare le risorse da utilizzare con il visualizzatore video 360:**

1. È stata creata una cartella dedicata alla risorsa video 360.
1. [Applica un profilo video adattivo alla cartella](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   Il rendering di contenuti video a 360° richiede una risoluzione video sorgente e una risoluzione delle rappresentazioni codificate superiori a quella dei contenuti video standard non a 360°.

   Puoi utilizzare il profilo video adattivo predefinito già fornito con Dynamic Media. Tuttavia, si ottiene una qualità video di 360 notevolmente inferiore rispetto a quella dei video non-360 codificati con le stesse impostazioni renderizzate con un visualizzatore video non-360. Pertanto, se è necessario un video di alta qualità 360, procedi come segue:

   * Idealmente, il contenuto video 360 originale ha una delle seguenti risoluzioni:

      * 1080p - 1920 x 1080, noto come risoluzione Full HD o FHD o,
      * 2160p - 3840 x 2160, noto come risoluzione 4K, UHD o HD Ultra. Questa grande risoluzione del display si trova più spesso su televisori e monitor per computer premium. La risoluzione 2160p viene spesso chiamata &quot;4K&quot; perché la larghezza è vicina a 4000 pixel. In altre parole, offre quattro volte i pixel di 1080p.
   * [Crea un ](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) profilo video adattivo personalizzato con rappresentazioni di qualità superiore. Ad esempio, puoi creare un profilo video adattivo contenente le tre impostazioni seguenti:

      * Width=auto; Altezza=720; Bit rate=2500 kbps
      * Width=auto; Height=1080; Bit rate=5000 kbps
      * Width=auto; Height=1440; Bit rate=6600 kbps
   * Elabora 360 contenuti video in una cartella dedicata esclusivamente a 360 risorse video.

   Questo approccio pone maggiori richieste sulla rete e sulla CPU dell&#39;utente finale.

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

## Anteprima dei video 360 {#previewing-video}

Puoi usare Anteprima per vedere come si presenta ai clienti il tuo video 360 e assicurarti che funzioni come previsto.

Consulta anche [Modifica dei predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

Quando sei soddisfatto del video 360, puoi pubblicarlo.

Consulta [Incorporamento del visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consulta [Collegamento di URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine di Experience Manager Sites.
Consulta [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Per visualizzare in anteprima 360 video**

1. In **[!UICONTROL Risorse]**, individua un video 360 esistente creato. Per aprirla in modalità anteprima, tocca la risorsa video 360.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Per visualizzare l’anteprima del video, tocca la risorsa video 360.

1. Nella pagina di anteprima, nell’angolo in alto a sinistra della pagina, tocca l’elenco a discesa, quindi seleziona **[!UICONTROL Visualizzatori]**.

   ![6_5_360visualizzatori di anteprima video](assets/6_5_360video-preview-viewers.png)

   Dall’elenco Visualizzatori, tocca **[!UICONTROL Video360_social]**, quindi effettua una delle seguenti operazioni:

   * Per modificare l’angolo di visualizzazione della scena statica, trascinare il puntatore sul video.
   * Per iniziare la riproduzione, toccare il pulsante **[!UICONTROL Play]** del video. Durante la riproduzione del video, trascinate il puntatore sull’angolo di visualizzazione per modificarlo.

   ![Schermata video 6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360.*

   * Dall’elenco Visualizzatori, tocca **[!UICONTROL Video360VR]**.

      Il video Virtual Reality (VR) è un video coinvolgente a cui è possibile accedere utilizzando cuffie per realtà virtuale. Come per i video comuni, è possibile creare video VR all&#39;inizio quando un video viene registrato o catturato utilizzando videocamere a 360 gradi.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Schermata video VR a 360°.*

1. Vicino alla parte superiore destra della pagina di anteprima, tocca **[!UICONTROL Chiudi]**.

## Pubblicazione di video 360 {#publishing-video}

Per utilizzare il video 360, è necessario pubblicarlo. La pubblicazione di un video 360 attiva l’URL e il codice di incorporamento. Pubblica anche il video 360 sul cloud Dynamic Media, integrato con una rete CDN per una distribuzione scalabile e performante.

Per informazioni dettagliate su come pubblicare video 360, consulta [Pubblicazione di risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .
Vedere anche [Incorporamento del visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consulta anche [Collegamento di URL all&#39;applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine di Experience Manager Sites.
Consulta anche [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
