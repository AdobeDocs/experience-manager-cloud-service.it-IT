---
title: Collegamento di URL all’applicazione web
description: Come collegare gli URL all’applicazione Web in contenuti multimediali dinamici
translation-type: tm+mt
source-git-commit: c240f9aa465b019fa77cc471f865db1f4ab45532
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 11%

---


# Collegamento di URL all’applicazione web {#linking-urls-to-your-web-application}

I siti Web e le applicazioni accedono ai servizi di Dynamic Media mediante chiamate URL. Dopo la pubblicazione di una risorsa, Dynamic Media attiva una stringa URL che fa riferimento alla risorsa. Potete incollare questi URL in un browser Web per sottoporli a test.

Potete impostare un collegamento agli URL solo se *non* utilizzate AEM come WCM. Il collegamento e l’incorporamento vengono utilizzati per distribuire un lettore video come finestra a comparsa o modale. Se usate AEM come WCM, [potete aggiungere le risorse direttamente sulla pagina.](adding-dynamic-media-assets-to-pages.md)

Per inserire queste stringhe URL nelle pagine Web e nelle applicazioni, copiatele da Contenuti multimediali dinamici.

>[!NOTE]
>
>Le stringhe URL sono disponibili solo per le rappresentazioni dinamiche delle risorse. Al momento non sono disponibili per le risorse statiche che risiedono in DAM e non nel server per contenuti multimediali dinamici. Il pulsante URL non viene visualizzato per le rappresentazioni statiche.

See also [Embedding the Video or Image Viewer on a Web Page](embed-code.md).

See also [Linking YouTube URLs to your Web Application](video.md).

See also [Delivering Optimized Images for a Responsive Site](responsive-site.md).

See also [Uploading Assets](/help/assets/manage-digital-assets.md#uploading-assets).

## Ottenimento di un URL per una risorsa {#obtaining-a-url-for-an-asset}

Potete ottenere una stringa URL generata da un predefinito per immagini o un predefinito per visualizzatori. Dopo aver copiato l’URL, questo viene inserito negli Appunti ed è quindi possibile incollarlo nelle pagine del sito Web o dell’applicazione.

>[!NOTE]
>
>L’URL può essere copiato solo dopo la pubblicazione della risorsa selezionata. Dovete inoltre pubblicare il predefinito per visualizzatori o per immagini.
>
>Consultate [Pubblicazione delle risorse](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

Esistono diversi modi per ottenere una stringa URL. Tuttavia, i passaggi seguenti mostrano un solo metodo che è possibile utilizzare.

**Per ottenere un URL per una risorsa**

1. Andate alla risorsa *pubblicata* il cui URL predefinito per immagini o l’URL del predefinito per visualizzatori che desiderate copiare e toccate la risorsa per aprirla.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consultate [Pubblicazione delle risorse](publishing-dynamicmedia-assets.md).

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. In base alla risorsa selezionata, effettuate una delle seguenti operazioni:

   * Se hai selezionato un’immagine, tocca **[!UICONTROL Rappresentazioni]** dal menu a discesa.

      Sotto l’intestazione **[!UICONTROL Dinamico]** , toccate un nome predefinito per visualizzarne la rappresentazione nel fotogramma destro. Potrebbe essere necessario scorrere l&#39;elenco Rappresentazioni per visualizzare l&#39;intestazione Dinamica.

      Nella parte inferiore della barra a sinistra, toccate **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se nel menu a discesa avete selezionato un set 360 gradi, un set di immagini, un set di caroselli o un video, toccate **[!UICONTROL Visualizzatori]**.

      Nella barra a sinistra, toccate il nome di un predefinito per visualizzatori. Un&#39;anteprima del set o del video viene aperta in una pagina separata.

      Nella barra a sinistra, nella parte inferiore, toccate **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Selezionate e copiate il testo nel browser Web per visualizzare l’anteprima della risorsa o per aggiungerlo alla pagina del contenuto Web.

   Per uscire dalla finestra URL, toccate la **[!UICONTROL X]** o toccate **[!UICONTROL Chiudi]**.

## Ottenimento di un URL per una risorsa statica {#obtaining-a-url-for-a-static-asset}

Dynamic Media supporta la distribuzione di risorse statiche, che sono risorse aggiuntive oltre alle sole immagini e ai video. I formati di risorse statiche supportati per la distribuzione includono:

* File 3D
* GIF animata
* File audio
* CSS
* JavaScript (se la società è configurata con un proprio dominio)
* PDF
* SVG
* XML
* ZIP

**Per ottenere un URL per una risorsa statica**

1. Andate alla risorsa *pubblicata *statica di cui desiderate copiare l&#39;URL e toccate la risorsa per aprirla.

   Remember that URLs are only available to copy *after* you have first *published* the static asset.

   Consultate [Pubblicazione delle risorse](publishing-dynamicmedia-assets.md).

1. Per ottenere l’URL della risorsa statica pubblicata, usate uno dei seguenti metodi:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Esempio, `https://aem.com/is/content/adobe/image.gif`.
   * Toccate **[!UICONTROL Risorsa > Rappresentazioni]** dinamiche, quindi toccate una rappresentazione dinamica della risorsa statica e copiate l’URL.

      Modificate l’URL copiato in modo che venga utilizzato `is/content` nel percorso anziché `is/image/`.


## Ottenimento di un URL video per una rappresentazione video pubblicata {#obtaining-a-video-url-for-a-published-video-rendition}

1. In AEM, accedi a **[!UICONTROL Strumenti > Distribuzione > Cloud > Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all’intestazione **[!UICONTROL Servizi cloud per elementi multimediali dinamici]**, quindi tocca **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, tocca il nome della configurazione desiderata.

1. Nella pagina Impostazioni **[!UICONTROL di]** Dynamic Media Cloud, in URL **[!UICONTROL del servizio]** video, copiate l’intero percorso dell’URL. Sarà necessario che il percorso dell’URL copiato venga completato più avanti nei passaggi descritti.

   Ad esempio, il percorso dell’URL potrebbe essere simile al seguente:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (il percorso precedente è solo a scopo illustrativo; non è il percorso effettivo che copiate.)

1. In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID.

   Ad esempio, se l’ID di registrazione era `87654321|MyCompany`, il nome del cliente sarebbe `MyCompany`.

1. Nell’angolo in alto a sinistra della pagina, toccate **[!UICONTROL Cloud Services]**, quindi toccate l’icona AEM e selezionate **[!UICONTROL Generale > CRXDE Lite]**.
1. Copiate l’intero percorso di rappresentazione video dal JCR (Java Content Repository).

   Ad esempio, il percorso di rappresentazione del video potrebbe essere simile al seguente:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (il percorso precedente è solo a scopo illustrativo; non è il percorso effettivo che copiate.)

1. Disporre le informazioni copiate nel seguente ordine in modo da formare un percorso URL completo:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Ad esempio, utilizzando i percorsi di esempio e il nome cliente di esempio dai passaggi precedenti, il percorso completo viene visualizzato come segue:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Questo è l’URL video completo per una rappresentazione video pubblicata.

## Ottenimento di un URL video per lo streaming adattivo (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. In AEM, accedi a **[!UICONTROL Strumenti > Distribuzione > Cloud > Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all’intestazione **[!UICONTROL Servizi cloud per elementi multimediali dinamici]**, quindi tocca **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, tocca il nome della configurazione desiderata.
1. Nella pagina Impostazioni **[!UICONTROL Cloud Services di file multimediali]** dinamici, effettuate le seguenti operazioni:

   * In URL **[!UICONTROL del servizio]** video, copiate l’intero percorso dell’URL. Successivamente, in questi passaggi, sarà necessario copiare il percorso URL. Ad esempio, il percorso dell’URL potrebbe essere simile al seguente:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (il percorso precedente è solo a scopo illustrativo; non è il percorso effettivo che copiate.)

   * In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID. Il nome del cliente così copiato sarà necessario nei passaggi seguenti.

      Ad esempio, se l’ID di registrazione era `87654321|demoCo`il nome cliente copiato sarebbe `demoCo`.


1. In base al protocollo di distribuzione video in uso, copiate il rispettivo selettore di protocollo. Sarà necessario il selettore di protocollo copiato più avanti in questi passaggi.

   <table>
    <tbody>
      <tr>
      <td><strong>Protocollo di distribuzione video utilizzato</strong></td>
      <td><strong>Selettore di protocollo da usare</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>Se utilizzate HTTP (distribuzione video non protetta), accertatevi di passare <code>https</code> al valore URL del servizio video <code>http</code> precedentemente copiato.</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. Copiate il percorso completo della risorsa video in AEM, come elaborato da Contenuti multimediali dinamici. Questo percorso di risorse video copiato sarà necessario più avanti nei seguenti passaggi.

   Esempio:

   `/content/dam/marketing/MyVideo.mp4`

1. Combinate tutti i pezzi precedentemente copiati per creare una stringa nell’ordine seguente:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Utilizzando, ad esempio, le informazioni copiate dagli esempi riportati di seguito, la stringa verrà visualizzata come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Completate l’URL aggiungendo `.m3u8` alla fine della stringa. Ad esempio, aggiungendo `.m3u8` alla stringa del passaggio precedente, il percorso completo dell’URL apparirà come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Utilizzo di HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, migliorando la risposta e i tempi di caricamento.

Per informazioni dettagliate sull’utilizzo di HTTP/2 con l’account per contenuti multimediali dinamici, consultate Consegna di contenuti [](http2faq.md) HTTP2.
