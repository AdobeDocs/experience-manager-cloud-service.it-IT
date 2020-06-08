---
title: Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate
description: La visualizzazione rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Potete attivare il contenuto personalizzato da visualizzare nelle finestre a comparsa.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 1%

---


# Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

La visualizzazione rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Tuttavia, potete attivare il contenuto personalizzato per la visualizzazione nelle finestre a comparsa. A seconda del visualizzatore in uso, questa funzione consente agli utenti di fare clic su un punto di attivazione, una miniatura o una mappa immagine per visualizzare informazioni o contenuti correlati.

Le viste rapide sono supportate dai seguenti visualizzatori in elementi multimediali dinamici:

* Immagini interattive (aree sensibili selezionabili)
* Video interattivo (immagini in miniatura cliccabili durante la riproduzione di un video)
* Banner carosello (aree sensibili selezionabili o mappe immagine)

Sebbene le funzionalità di ciascun visualizzatore siano diverse, il processo di creazione di una visualizzazione rapida è lo stesso per tutti e tre i visualizzatori supportati.

**Per utilizzare le viste rapida per creare finestre a comparsa personalizzate**

1. Create una visualizzazione rapida per una risorsa caricata.

   In genere, potete creare una visualizzazione rapida contemporaneamente a una risorsa da usare con il visualizzatore in uso.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Completate i seguenti passaggi per creare la visualizzazione rapida</strong></td>
    </tr>
    <tr>
    <td>Immagini interattive</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Aggiunta di punti attivi a un banner</a>immagine.</td>
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
    <td><strong>Completate i seguenti passaggi per integrare il visualizzatore con il sito Web</strong></td>
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
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina</a>del sito Web.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore che state utilizzando ora deve essere in grado di utilizzare la visualizzazione rapida.

   A questo scopo, il visualizzatore utilizza un handler denominato `QuickViewActive`.

   **Esempio**: utilizzate il seguente codice da incorporare nella pagina Web per un’immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizzando l&#39;esempio di codice da incorporare riportato sopra, è disponibile il seguente codice:**

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

   Per ulteriori informazioni sul `setHandlers()` metodo, consulta:

   * Visualizzatore immagini interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_sethandlers.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_sethandlers.html)
   * Visualizzatore video interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_sethandlers.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_sethandlers.html)

1. È ora necessario configurare il `quickViewActivate` gestore.

   Il `quickViewActivate` gestore controlla le visualizzazioni rapide nel visualizzatore. Il gestore contiene l&#39;elenco di variabili e le chiamate di funzioni da utilizzare con la visualizzazione rapida. Il codice embed fornisce la mappatura per la variabile SKU impostata in Quickview e per una `loadQuickView` funzione di esempio chiamata.

   **Variabili di mappatura** Mappa della variabile da usare nella pagina Web per il valore SKU e le variabili generiche contenute in Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice da incorporare fornito include un esempio di mappatura per la variabile SKU:

   `var sku=inData.sku`

   Mappate anche altre variabili dalla visualizzazione rapida, come segue:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chiamata** alla funzione Il gestore richiede anche una chiamata alla funzione per il funzionamento di Quickview. Si presume che la funzione sia accessibile dalla pagina host. Il codice embed fornisce un esempio di chiamata di funzione:

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esista e sia accessibile.

   Per ulteriori informazioni sul `quickViewActivate` metodo, consulta:

   * Visualizzatore immagini interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_interactive_image_event_callbacks.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_interactive_image_event_callbacks.html)
   * Visualizzatore video interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_event_callbacks.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_event_callbacks.html)
   * Supporto dei dati interattivi nel visualizzatore video interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_int_data_support.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_int_video_int_data_support.html)

1. Effettua le seguenti operazioni:

   * Rimuovete il commento dalla sezione setHandlers del codice da incorporare.
   * Mappare eventuali ulteriori variabili contenute nella visualizzazione rapida.

      * Aggiorna la `loadQuickView(sku,*var1*,*var2*)` chiamata se stai aggiungendo ulteriori variabili.
   * Create una semplice funzione `loadQuickView` () sulla pagina, all’esterno del visualizzatore.

      Ad esempio, il valore sku riportato di seguito viene scritto nella console del browser:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Caricate una pagina HTML di prova su un server Web e apritela.

      Con le variabili di Quickview mappate e la chiamata della funzione in essere, la console del browser scrive il valore della variabile nella console del browser utilizzando la funzione di esempio fornita.



1. È ora possibile utilizzare una funzione per richiamare una semplice finestra a comparsa nella visualizzazione rapida. Nell&#39;esempio seguente viene utilizzato un `DIV` a comparsa.
1. Stile della finestra a comparsa `DIV` nel modo seguente. Aggiungete il vostro stile aggiuntivo come desiderate.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserite la finestra a comparsa `DIV` nel corpo della pagina HTML.

   Uno degli elementi è impostato con un ID aggiornato con il valore sku quando l&#39;utente richiama una visualizzazione rapida. L’esempio include anche un semplice pulsante per nascondere nuovamente la finestra a comparsa dopo che questa diventa visibile.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Aggiungete una funzione per aggiornare il valore sku nella finestra a comparsa; rendere il pop-up visibile sostituendo la semplice funzione creata al punto 5. con le seguenti caratteristiche:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Caricate una pagina HTML di prova nel server Web e apritela. Il visualizzatore visualizza la finestra a comparsa `DIV` quando un utente richiama una visualizzazione rapida.
1. **Come visualizzare il pop-up personalizzato in modalità a schermo intero**

   Alcuni visualizzatori, come il visualizzatore per video interattivi, supportano la visualizzazione in modalità a schermo intero. Tuttavia, se si utilizza la finestra a comparsa come descritto nei passaggi precedenti, viene visualizzata dietro il visualizzatore in modalità a schermo intero.

   Per visualizzare la visualizzazione a comparsa sia in modalità standard che a schermo intero, allegate la finestra a comparsa al contenitore del visualizzatore. A tal fine, è possibile utilizzare un secondo metodo di gestione, `initComplete`.

   Il `initComplete` gestore viene richiamato dopo che il visualizzatore è stato inizializzato.

   ```xml
   "initComplete":function() { code block }
   ```

   Per ulteriori informazioni sul `init()` metodo, consulta:

   * Visualizzatore immagini interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_init.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_image_viewer_javascriptapiref_init.html)
   * Visualizzatore video interattivo: [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_init.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_aem_int_video_javascriptapiref_init.html)

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

   Nel codice riportato sopra, abbiamo fatto quanto segue:

   * Identificato il nostro pop-up personalizzato.
   * Rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * Associata la finestra a comparsa al contenitore del visualizzatore.

1. Il codice setHandlers deve ora essere simile al seguente (è stato utilizzato il visualizzatore video interattivo):

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

   **Esempio** Questo esempio utilizza il visualizzatore di immagini interattivo.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, accertatevi che l’istanza del visualizzatore venga creata e che i gestori vengano caricati prima che il visualizzatore venga richiamato tramite `init()`.

