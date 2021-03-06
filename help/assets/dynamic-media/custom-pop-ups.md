---
title: Creare pop-up personalizzati utilizzando Quickview
description: '"Scopri come viene utilizzata la visualizzazione rapida predefinita nelle esperienze di e-commerce in cui viene visualizzata una finestra a comparsa con informazioni sul prodotto per promuovere un acquisto. Puoi attivare il contenuto personalizzato da visualizzare nella finestra a comparsa."'
feature: Interactive Images,Interactive Videos,Carousel Banners
role: Admin,User
exl-id: c2bc6ec8-d46e-4681-ac3e-3337b9e6ae5c
source-git-commit: 462ce45d24cf8bcad6963011d2d57d9d7da45550
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

La visualizzazione rapida predefinita viene utilizzata nelle esperienze e-commerce in cui viene visualizzato un pop-up con le informazioni sul prodotto per promuovere un acquisto. Tuttavia, puoi attivare il contenuto personalizzato da visualizzare nei pop-up. A seconda del visualizzatore utilizzato, i clienti possono selezionare un punto attivo, un&#39;immagine in miniatura o una mappa immagine per visualizzare le informazioni o il contenuto correlato.

Quickview √® supportato dai seguenti visualizzatori in Dynamic Media:

* Immagini interattive (hotspot selezionabili)
* Video interattivo (immagini in miniatura selezionabili durante la riproduzione del video)
* Banner a carosello (punti attivi selezionabili o mappe immagine)

Sebbene le funzionalit√† di ciascun visualizzatore siano diverse, il processo di creazione di una visualizzazione rapida √® lo stesso in tutti e tre i visualizzatori supportati.

**Per creare pop-up personalizzati utilizzando Quickview:**

1. Crea una visualizzazione rapida per una risorsa caricata.

   In genere, quando si modifica una risorsa da utilizzare con il visualizzatore in uso, viene creata una visualizzazione rapida.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Per creare la visualizzazione rapida, completa questi passaggi</strong></td>
    </tr>
    <tr>
    <td>Immagini interattive</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Aggiunta di punti attivi a un banner immagine</a>.</td>
    </tr>
    <tr>
    <td>Video interattivi</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Aggiunta di interattivit√† al video</a>.</td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Aggiunta di punti attivi o mappe immagine a un banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Ottieni il codice di incorporamento del visualizzatore per integrare il visualizzatore all‚Äôinterno del tuo sito web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong><br /> </td>
    <td><strong>Per integrare il visualizzatore con il sito web, completa questi passaggi</strong></td>
    </tr>
    <tr>
    <td>Immagine interattiva</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrazione di un‚Äôimmagine interattiva con il sito web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Video interattivo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrazione di un video interattivo con il sito web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina del sito web</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore utilizzato deve sapere come utilizzare la visualizzazione rapida.

   Il visualizzatore utilizza un gestore chiamato `QuickViewActive`.

   **Esempio**
Supponiamo che tu stia utilizzando il seguente codice di incorporamento sulla tua pagina web per un&#39;immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizzando l&#39;esempio di codice di incorporamento di esempio riportato sopra, si dispone del seguente codice:**

   ```xml {.line-numbers}
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Ulteriori informazioni `setHandlers()` metodo nel modo seguente:

   * Visualizzatore immagini interattivo - [armatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizzatore video interattivo - [armatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Ora configura la `quickViewActivate` handler.

   La `quickViewActivate` Il gestore controlla la visualizzazione rapida nel visualizzatore. Il gestore contiene l&#39;elenco di variabili e le chiamate di funzioni da utilizzare con Quickview. Il codice di incorporamento fornisce la mappatura per la variabile SKU impostata in Quickview. Fa anche un campione `loadQuickView` chiamata della funzione.

   **Mappatura variabile**
Mappa le variabili da utilizzare nella pagina web al valore SKU e alle variabili generiche contenute in Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice di incorporamento fornito ha una mappatura di esempio per la variabile SKU:

   `var sku=inData.sku`

   Mappa anche altre variabili dalla visualizzazione rapida, come illustrato di seguito:

   ```xml {.line-numbers}
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chiamata funzione**
Il gestore richiede anche una chiamata di funzione per il funzionamento di Quickview. Si presume che la funzione sia accessibile dalla pagina host. Il codice di incorporamento fornisce un esempio di chiamata della funzione :

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esiste ed √® accessibile.

   Ulteriori informazioni `quickViewActivate` metodo nel modo seguente:

   * Visualizzatore immagini interattivo - [Callback degli eventi](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizzatore video interattivo - [Callback degli eventi](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Supporto dei dati interattivi nel visualizzatore video interattivo - [Supporto dei dati interattivi](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Effettua le seguenti operazioni:

   * Rimuovi il commento alla sezione setHandlers del codice di incorporamento.
   * Mappa eventuali variabili aggiuntive contenute nella visualizzazione rapida.

      * Aggiorna `loadQuickView(sku,*var1*,*var2*)` chiama se aggiungi altre variabili.
   * Crea un semplice `loadQuickView` () funziona a pagina, all‚Äôesterno del visualizzatore.

      Ad esempio, il seguente scrive il valore di SKU nella console del browser:

   ```xml {.line-numbers}
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carica una pagina HTML di test su un server web e apri.

      Le variabili della visualizzazione rapida sono mappate. La chiamata della funzione √® attiva. E la console del browser scrive il valore della variabile nella console del browser. Lo fa utilizzando la funzione di esempio fornita.



1. √ą ora possibile utilizzare una funzione per richiamare un semplice pop-up in Quickview. Nell&#39;esempio seguente viene utilizzato un `DIV` per una finestra a comparsa.
1. Personalizzare lo stile della finestra a comparsa `DIV` nel modo seguente. Aggiungi lo stile extra desiderato.

   ```xml {.line-numbers}
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Posiziona la finestra a comparsa `DIV` nel corpo della pagina HTML.

   Uno degli elementi viene impostato con un ID aggiornato con il valore SKU quando l‚Äôutente richiama un Quickview. L‚Äôesempio include anche un semplice pulsante per nascondere nuovamente la finestra a comparsa quando diventa visibile.

   ```xml {.line-numbers}
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Per aggiornare il valore SKU nella finestra a comparsa, aggiungi una funzione. Rendere visibile la finestra a comparsa sostituendo la funzione semplice creata al punto 5 con la seguente:

   ```xml {.line-numbers}
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carica una pagina HTML di test sul server web e apri. Il visualizzatore visualizza la finestra a comparsa `DIV` quando un utente richiama un Quickview.
1. **Come visualizzare la finestra pop-up personalizzata in modalit√† a schermo intero**

   Alcuni visualizzatori, come il visualizzatore video interattivo, supportano la visualizzazione in modalit√† a schermo intero. Tuttavia, se si utilizza il pop-up come descritto nei passaggi precedenti, questo viene visualizzato dietro il visualizzatore in modalit√† a schermo intero.

   Per visualizzare la finestra a comparsa nelle modalit√† standard e a schermo intero, allegare la finestra a comparsa al contenitore del visualizzatore. In questo caso, utilizza un secondo metodo handler, `initComplete`.

   La `initComplete` viene richiamato dopo l&#39;inizializzazione del visualizzatore.

   ```xml {.line-numbers}
   "initComplete":function() { code block }
   ```

   Ulteriori informazioni `init()` metodo nel modo seguente:

   * Visualizzatore immagini interattivo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizzatore video interattivo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Per allegare al visualizzatore il pop-up (descritto nei passaggi precedenti), utilizza il seguente codice:

   ```xml {.line-numbers}
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   Nel codice precedente, hai fatto quanto segue:

   * Identificata la finestra pop-up personalizzata.
   * √ą stato rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * √ą stato allegato il pop-up al contenitore del visualizzatore.

1. L‚Äôintero codice setHandlers √® simile al seguente (√® stato utilizzato il visualizzatore video interattivo):

   ```xml {.line-numbers}
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. Dopo il caricamento dei gestori, inizializza il visualizzatore:

   `*viewerInstance.*init()`

   **Esempio**
In questo esempio viene utilizzato il visualizzatore di immagini interattivo.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, assicurati che l‚Äôistanza del visualizzatore sia stata creata. Inoltre, assicurati che i gestori vengano caricati prima che il visualizzatore venga richiamato utilizzando `init()`.
