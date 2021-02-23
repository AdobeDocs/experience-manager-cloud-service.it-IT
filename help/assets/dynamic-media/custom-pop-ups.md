---
title: Utilizzo delle viste rapide per creare finestre a comparsa personalizzate
description: La visualizzazione Rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Potete attivare il contenuto personalizzato da visualizzare nelle finestre a comparsa.
translation-type: tm+mt
source-git-commit: ad626d9722f1942249197d96aa5fac3d8f7ed947
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 1%

---


# Uso delle viste rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

La visualizzazione Rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Tuttavia, potete attivare il contenuto personalizzato per la visualizzazione nelle finestre a comparsa. A seconda del visualizzatore in uso, i clienti possono toccare un punto sensibile, un’immagine in miniatura o una mappa immagine per visualizzare informazioni o contenuti correlati.

Le viste rapide sono supportate dai seguenti visualizzatori in Dynamic Media:

* Immagini interattive (aree sensibili selezionabili)
* Video interattivo (immagini in miniatura cliccabili durante la riproduzione di un video)
* Banner carosello (aree sensibili selezionabili o mappe immagine)

Sebbene le funzionalità di ciascun visualizzatore differiscano, il processo di creazione di una visualizzazione rapida è lo stesso per tutti e tre i visualizzatori supportati.

**Per utilizzare le viste rapide per creare finestre a comparsa personalizzate**

1. Create una visualizzazione rapida per una risorsa caricata.

   In genere, potete creare una visualizzazione Rapida contemporaneamente a una risorsa da usare con il visualizzatore in uso.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Per creare la vista Rapida, completare i seguenti passaggi</strong></td>
    </tr>
    <tr>
    <td>Immagini interattive</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Aggiunta di punti attivi a un banner</a> immagine.</td>
    </tr>
    <tr>
    <td>Video interattivi</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Aggiunta di interattività al video</a>.</td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Aggiunta di punti attivi o mappe immagine a un banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Ottenete il codice da incorporare del visualizzatore per integrare il visualizzatore nel vostro sito Web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong><br /> </td>
    <td><strong>Per integrare il visualizzatore con il sito Web, effettuate le seguenti operazioni</strong></td>
    </tr>
    <tr>
    <td>Immagine interattiva</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrazione di un’immagine interattiva con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Video interattivo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrazione di un video interattivo con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner carosello</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina</a> del sito Web.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore utilizzato deve essere in grado di utilizzare la vista Rapida.

   Il visualizzatore utilizza un gestore denominato `QuickViewActive`.

   **Esempio:**
Supponete di usare il seguente codice da incorporare nella pagina Web per un’immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizzando l’esempio di codice da incorporare riportato sopra, si ottiene il seguente codice:**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Per ulteriori informazioni sul metodo `setHandlers()`, consulta:

   * Visualizzatore immagini interattivo: [palmari](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizzatore video interattivo: [palmari](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Configurate ora il gestore `quickViewActivate`.

   Il gestore `quickViewActivate` controlla le viste Rapide nel visualizzatore. Il gestore contiene l&#39;elenco di variabili e le chiamate di funzioni da utilizzare con la vista Rapida. Il codice da incorporare fornisce la mappatura della variabile SKU impostata nella vista Rapida. Esegue inoltre una chiamata di funzione `loadQuickView` di esempio.

   **Variabili**
mappingMappa per l’utilizzo nella pagina Web in base al valore SKU e alle variabili generiche contenute nella visualizzazione Rapida:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice da incorporare fornito include un esempio di mappatura per la variabile SKU:

   `var sku=inData.sku`

   Mappare anche altre variabili dalla vista Rapida, come illustrato di seguito:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Funzione**
callIl gestore richiede anche una chiamata di funzione per il funzionamento della visualizzazione Rapida. Si presume che la funzione sia accessibile dalla pagina host. Il codice embed fornisce un esempio di chiamata di funzione:

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esista e sia accessibile.

   Per ulteriori informazioni sul metodo `quickViewActivate`, consulta:

   * Visualizzatore immagini interattivo - [callback evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizzatore video interattivo - [callback evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Supporto dei dati interattivi nel visualizzatore video interattivo - [Supporto dei dati interattivi](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Effettua le seguenti operazioni:

   * Rimuovete il commento dalla sezione setHandlers del codice da incorporare.
   * Mappare eventuali variabili aggiuntive contenute nella vista Rapida.

      * Aggiorna la chiamata `loadQuickView(sku,*var1*,*var2*)` se aggiungi altre variabili.
   * Create una semplice funzione `loadQuickView` () sulla pagina, all&#39;esterno del visualizzatore.

      Ad esempio, il valore SKU viene scritto nella console del browser come segue:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Caricate una pagina HTML di prova su un server Web e apritela.

      Le variabili della vista Rapida sono mappate. La chiamata della funzione è attiva. La console del browser scrive il valore della variabile nella console del browser. A tal fine, utilizza la funzione di esempio fornita.



1. È ora possibile utilizzare una funzione per richiamare una semplice finestra a comparsa nella vista Rapida. Nell&#39;esempio seguente viene utilizzato un `DIV` per un popup.
1. Formattare la finestra a comparsa `DIV` nel modo seguente. Se necessario, potete aggiungere altri stili.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserite il pop-up `DIV` nel corpo della pagina HTML.

   Uno degli elementi è impostato con un ID aggiornato con il valore SKU quando l’utente richiama una vista Rapida. L’esempio include anche un semplice pulsante per nascondere nuovamente la finestra a comparsa dopo che questa diventa visibile.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Per aggiornare il valore SKU nella finestra a comparsa, aggiungere una funzione. Rendete visibile la finestra a comparsa sostituendo la semplice funzione creata al punto 5 con la seguente:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Caricate una pagina HTML di prova nel server Web e apritela. Il visualizzatore visualizza la finestra a comparsa `DIV` quando un utente richiama una visualizzazione rapida.
1. **Come visualizzare la finestra a comparsa personalizzata in modalità a schermo intero**

   Alcuni visualizzatori, come il visualizzatore per video interattivi, supportano la visualizzazione in modalità a schermo intero. Tuttavia, se si utilizza la finestra a comparsa come descritto nei passaggi precedenti, viene visualizzata dietro il visualizzatore in modalità a schermo intero.

   Per visualizzare la finestra a comparsa nelle modalità standard e a schermo intero, allegate la finestra a comparsa al contenitore del visualizzatore. In questo caso, utilizzare un secondo metodo del gestore, `initComplete`.

   Il gestore `initComplete` viene richiamato dopo l&#39;inizializzazione del visualizzatore.

   ```xml
   "initComplete":function() { code block }
   ```

   Per ulteriori informazioni sul metodo `init()`, consulta:

   * Visualizzatore immagini interattivo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizzatore video interattivo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Per allegare al visualizzatore la finestra a comparsa (descritta nei passaggi precedenti), usate il seguente codice:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   Nel codice precedente, avete eseguito le seguenti operazioni:

   * Identificata la finestra a comparsa personalizzata.
   * Rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * Associata la finestra a comparsa al contenitore del visualizzatore.

1. L’intero codice setHandlers è simile al seguente (è stato utilizzato il visualizzatore video interattivo):

   ```xml
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

1. Dopo aver caricato i gestori, inizializzate il visualizzatore:

   `*viewerInstance.*init()`

   ****
Esempio: in questo esempio viene utilizzato il visualizzatore di immagini interattivo.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, accertatevi che sia stata creata l’istanza del visualizzatore. Inoltre, verificate che i gestori vengano caricati prima che il visualizzatore venga richiamato utilizzando `init()`.

