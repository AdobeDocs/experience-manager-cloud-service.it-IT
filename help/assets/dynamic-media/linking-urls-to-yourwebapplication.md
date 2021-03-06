---
title: Collegamento degli URL all’applicazione Web
description: Scopri come collegare gli URL alla tua applicazione web in Dynamic Media.
role: User
exl-id: 3cd3f4d5-ebf0-4318-9a0d-1ea69453d57b
source-git-commit: 1d42305b6a597dc95bff8b34eee8279eb0e511f3
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 6%

---

# Collegamento degli URL all’applicazione Web {#linking-urls-to-your-web-application}

I siti web e le applicazioni accedono ai servizi Dynamic Media tramite chiamate URL. Dopo la pubblicazione di una risorsa, Dynamic Media attiva una stringa URL che fa riferimento a tale risorsa. You can paste these URLs into a web browser for testing.

Ti colleghi agli URL solo se lo sei *not* utilizzo di Adobe Experience Manager come WCM. Linking – versus embedding – is used when you want to deliver a video player as a pop-up or modal window. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente sulla pagina.](adding-dynamic-media-assets-to-pages.md)

To place these URL strings in your web pages and applications, copy them from Dynamic Media.

>[!NOTE]
>
>Le stringhe URL sono disponibili solo per le rappresentazioni dinamiche delle risorse. Al momento non sono disponibili per le risorse statiche che risiedono in DAM e non nel server Dynamic Media. Il pulsante URL non viene visualizzato per le rappresentazioni statiche.

Vedi anche [Incorporare il visualizzatore di video o immagini in una pagina web](embed-code.md).

Vedi anche [Collegare gli URL di YouTube all’applicazione web](video.md).

Vedi anche [Fornire immagini ottimizzate per un sito reattivo](responsive-site.md).

Vedi anche [Caricare risorse](/help/assets/manage-digital-assets.md#uploading-assets).

## Ottenere un URL per una risorsa {#obtaining-a-url-for-an-asset}

Puoi ottenere una stringa URL generata da un predefinito per immagini o da un predefinito per visualizzatori. Dopo aver copiato l’URL, questo viene inserito negli Appunti in modo da poterlo incollare come necessario nelle pagine del sito web o dell’applicazione.

>[!NOTE]
>
>L’URL può essere copiato solo dopo la pubblicazione della risorsa selezionata. Inoltre, devi pubblicare il predefinito visualizzatore o il predefinito immagine.
>
>Vedi [Pubblicare le risorse](publishing-dynamicmedia-assets.md).
>
>Vedi [Pubblicare i predefiniti per visualizzatori](managing-viewer-presets.md#publishing-viewer-presets).
>
>Vedi [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

Esistono diversi modi per ottenere una stringa URL. Tuttavia, i passaggi seguenti mostrano un solo metodo possibile.

**Per ottenere un URL per una risorsa:**

1. Navigate to the *published* asset whose image preset URL or viewer preset URL you want to copy, and select the asset to open it.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Vedi [Pubblicare le risorse](publishing-dynamicmedia-assets.md).

   See [Publish Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   Vedi [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. In base alla risorsa selezionata, effettua una delle seguenti operazioni:

   * Se hai selezionato un’immagine, seleziona dal menu a discesa **[!UICONTROL Rendering]**.

      Under the **[!UICONTROL Dynamic]** heading, select a preset name to view its rendition in the right frame. Se necessario, scorri l’elenco Rendering per visualizzare l’intestazione Dinamica .

      Nella parte inferiore della barra a sinistra, seleziona **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se hai selezionato un set 360 gradi, un set di immagini, un set carosello o un video nel menu a discesa, seleziona **[!UICONTROL Visualizzatori]**.

      Nella barra a sinistra, seleziona un nome di predefinito visualizzatore. A preview of the set or video is opened in a separate page.

      Nella barra a sinistra, nella parte inferiore, seleziona **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Per visualizzare l’anteprima della risorsa o per aggiungerla alla pagina del contenuto web, seleziona e copia il testo nel browser web.

   Per uscire dalla finestra URL, seleziona la **[!UICONTROL X]** o seleziona **[!UICONTROL Chiudi]**.

## Ottenere un URL per una risorsa statica {#obtaining-a-url-for-a-static-asset}

Dynamic Media supporta la distribuzione di risorse statiche, che sono altre risorse oltre alle sole immagini e ai video. I formati di risorse statiche supportati per la distribuzione includono:

* 3D files
* GIF animato
* File audio
* CSS
* JavaScript (when your company is configured with its own domain)
* PDF
* SVG
* XML
* ZIP

**Per ottenere un URL per una risorsa statica:**

1. Passa a *pubblicato* risorsa statica di cui desideri copiare l’URL e seleziona la risorsa per aprirla.

   Gli URL sono disponibili solo per la copia *dopo* hai il primo *pubblicato* la risorsa statica.

   Vedi [Pubblicazione delle risorse](publishing-dynamicmedia-assets.md).

1. Use any of the following methods to obtain the URL of the published static asset:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Esempio, `https://aem.com/is/content/adobe/image.gif`.
   * Seleziona **[!UICONTROL Risorsa]** > **[!UICONTROL Rendering dinamici]**, quindi seleziona un rendering dinamico della risorsa statica e copia l’URL.

      Modificare l’URL copiato da utilizzare `is/content` nel percorso invece di `is/image/`.


## Ottenere un URL video per un rendering video pubblicato {#obtaining-a-video-url-for-a-published-video-rendition}

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. Sulla **[!UICONTROL Cloud Services]** , scorri verso il basso fino a **[!UICONTROL Cloud Services Dynamic Media]** intestazione, quindi selezionare **[!UICONTROL Mostra configurazioni]**.
1. Sotto **[!UICONTROL Configurazioni disponibili]**, seleziona il nome della configurazione desiderata.

1. Sulla **[!UICONTROL Impostazioni di Dynamic Media Cloud]** pagina, sotto **[!UICONTROL URL del servizio video]**, copia l’intero percorso URL. Il percorso dell’URL copiato deve essere visualizzato più avanti nei passaggi descritti.

   For example, the URL path could appear similar to the following:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (Il percorso di cui sopra è solo a scopo esplicativo; non è il percorso effettivo copiato.)

1. In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID.

   For example, if the registration ID was `87654321|MyCompany`, the customer name would be `MyCompany`.

1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Cloud Services]**, quindi seleziona l’icona Experience Manager e vai a **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Copia l’intero percorso di rendering video dal JCR (Java™ Content Repository).

   Ad esempio, il percorso di rendering del video potrebbe essere simile al seguente:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (Il percorso di cui sopra è solo a scopo esplicativo; non è il percorso effettivo copiato.)

1. Per creare un percorso URL completo, disporre le informazioni copiate nel seguente ordine:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Ad esempio, utilizzando i percorsi di esempio e il nome del cliente di esempio dei passaggi precedenti, il percorso completo viene visualizzato come segue:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Questo percorso è l’URL video completo per un rendering video pubblicato.

## Ottenere un URL video per lo streaming adattivo (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. Ad Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. Sulla **[!UICONTROL Cloud Services]** , scorri verso il basso fino a **[!UICONTROL Cloud Services Dynamic Media]** intestazione, quindi selezionare **[!UICONTROL Mostra configurazioni]**.
1. Sotto **[!UICONTROL Configurazioni disponibili]**, seleziona il nome della configurazione desiderata.
1. Sulla **[!UICONTROL Impostazioni Cloud Services Dynamic Media]** , procedi come segue:

   * Sotto **[!UICONTROL URL del servizio video]**, copia l’intero percorso URL. Successivamente, segui il percorso dell’URL copiato in questi passaggi. For example, the URL path could appear similar to the following:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (Il percorso di cui sopra è solo a scopo esplicativo; non è il percorso effettivo copiato.)

   * In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID. You need the copied customer name later in these steps.

      Ad esempio, se l&#39;ID di registrazione era `87654321|demoCo`, il nome del cliente copiato sarà `demoCo`.


1. In base al protocollo di consegna video utilizzato, copia il rispettivo selettore di protocollo. Successivamente, è necessario utilizzare il selettore di protocollo copiato in questi passaggi.

   <table>
    <tbody>
      <tr>
      <td><strong>Protocollo di distribuzione video utilizzato</strong></td>
      <td><strong>Selettore di protocollo da utilizzare</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>If you are using HTTP (non-secure video delivery), be sure you change <code>https</code> to <code>http</code> in the Video Service URL value you copied earlier.</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. Copia il percorso completo della risorsa video in Experience Manager, come elaborato da Dynamic Media. In seguito, segui questi passaggi per trovare il percorso della risorsa video copiata.

   Ad esempio:

   `/content/dam/marketing/MyVideo.mp4`

1. Combina tutti gli elementi copiati in precedenza per creare una stringa nell&#39;ordine seguente:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Ad esempio, utilizzando le informazioni copiate dagli esempi descritti in questi passaggi, la stringa verrà visualizzata come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Complete the URL by appending `.m3u8` to the end of the string. Ad esempio, aggiunta `.m3u8` alla stringa del passaggio precedente, il percorso URL completo apparirà come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Utilizza HTTP/2 per distribuire le tue risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. It provides faster transfer of information and reduces the amount of processing power that is needed. La distribuzione delle risorse Dynamic Media può ora avvenire tramite HTTP/2, garantendo tempi di risposta e caricamento migliori.

Vedi [Distribuzione di contenuti HTTP2](http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media.
