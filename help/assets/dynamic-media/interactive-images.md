---
title: Immagini interattive
description: Scoprite come utilizzare le immagini interattive in Dynamic Media.
translation-type: tm+mt
source-git-commit: ad626d9722f1942249197d96aa5fac3d8f7ed947
workflow-type: tm+mt
source-wordcount: '4246'
ht-degree: 1%

---


# Immagini interattive{#interactive-images}

Potete rendere le immagini statiche ricche di immagini e creare esperienze coinvolgenti per i clienti trascinando e rilasciando punti di attivazione &quot;shoppable&quot; su un’immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o un servizio con una funzionalità &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot; diretta, punto vendita. I clienti possono toccare questi punti di attivazione che si collegano direttamente al prodotto o al servizio, aggiungerlo a un carrello o essere collegati a una pagina Web. Esperienze dirette come queste aumentano il coinvolgimento dei clienti e le conversioni sul sito Web.

Di seguito è riportato un banner acquistabile con una finestra a comparsa Vista rapida. Un utente attiva la vista Rapida toccando il cerchio o il punto di attivazione del modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Consultate [immagini interattive in azione](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) sulla pagina Web visualizzata sopra.

## Scoprite come creare i banner immagine interattivi {#watch-how-interactive-image-banners-are-created}

Guardate la procedura dettagliata di 10 minuti e 33 secondi su [come vengono creati i banner immagine interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Inoltre viene illustrato come visualizzare in anteprima, modificare e distribuire banner immagine interattivi.

## Avvio rapido: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le immagini interattive in  AEM Assets.

Cercare l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di Avvio rapido. Contiene una breve esercitazione basata su un esempio di [pagina Web in cui non sono ancora state aggiunte immagini interattive](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



Questa esercitazione illustra i passaggi necessari per integrare le immagini interattive nel sito Web.

Passaggi Immagini interattive:

1. **(Facoltativo) Identificazione delle variabili** dei punti di attivazione. Se utilizzi Adobe Experience Manager Assets e Dynamic Media standalone, individua le variabili dinamiche utilizzate nell’implementazione esistente della visualizzazione rapida. In questo modo potrete inserire i dati dei punti di attivazione al momento della creazione dell’immagine interattiva. Vedere [(facoltativo) Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables).
Tuttavia, se utilizzi  AEM Sites, AEM eCommerce o entrambi, questo passaggio non è necessario.

1. **(Facoltativo) Creazione di un predefinito** per visualizzatori immagini interattivi. Personalizzate l&#39;immagine grafica utilizzata per rappresentare i punti di attivazione. La creazione di un predefinito per visualizzatori di immagini interattive non è necessaria se intendete utilizzare il predefinito per visualizzatori di immagini interattive preimpostato denominato `Shoppable_Banner`.
Consultate [(facoltativo) Creazione di un predefinito per visualizzatori immagini interattivi](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Caricamento di un banner** immagine. Caricate i banner immagine da rendere interattivi.
Consultate [Caricamento di un banner immagine](#uploading-an-image-banner).

1. **Aggiunta di punti attivi a un banner** immagine. Aggiungete uno o più punti di attivazione a un banner immagine. Associate ciascuna di esse a un&#39;azione come un collegamento ipertestuale, una vista Rapida o un frammento esperienza. Dopo aver aggiunto i punti di attivazione, questa attività verrà completata pubblicando l&#39;immagine interattiva.
Consultate [Aggiunta di punti di attivazione a un banner di immagine](#adding-hotspots-to-an-image-banner).
Consultate [Anteprima delle immagini interattive](#optional-previewing-interactive-images) - Facoltativo. Se necessario, potete visualizzare una rappresentazione del banner acquistabile e verificarne l’interattività.
Consultate [Publishing Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

1. **Aggiunta di un’immagine interattiva al sito Web o al sito Web in  Experience Manager**. Se utilizzate Siti, eCommerce o entrambi, potete aggiungere immagini interattive direttamente a una pagina Web in  Experience Manager. Trascinate il componente Contenuti multimediali interattivi sulla pagina. Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
Se utilizzate Experience ManagerAssets e Dynamic Media standalone, copiate il codice da incorporare sul sito Web. Quindi, integratelo con la vista Rapida esistente. Consultate [Integrazione di un&#39;immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).
Se utilizzate un WCM di terze parti (Web Content Manager), integrate il nuovo video interattivo con la visualizzazione Rapida esistente utilizzata sul sito Web. Consultate [Integrazione di un&#39;immagine interattiva con una visualizzazione rapida esistente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Facoltativo) Identificazione delle variabili dei punti di attivazione {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività all’immagine, attivate la visualizzazione Rapida.
>* L&#39;implementazione di  Experience Manager *non* utilizza un framework di integrazione eCommerce per estrarre i dati di prodotto  Experience Manager da qualsiasi soluzione eCommerce. Tali soluzioni includono IBM WebSphere® Commerce, Elastic Path, hybris o Intershop.

>
>
Se l&#39;implementazione di AEM utilizza eCommerce, puoi saltare questa attività e passare all&#39;attività successiva.

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente della vista Rapida in modo da poter inserire i dati dei punti di attivazione per creare l’immagine interattiva.

Quando aggiungete punti attivi a un&#39;immagine del banner in  risorse di Experience Manager, assegnate un SKU (Stock Keeping Unit). Lo SKU è un identificatore univoco per ciascun prodotto o servizio distinto offerto. Inoltre, aggiungete eventuali variabili facoltative aggiuntive a ciascun punto di attivazione. Tali variabili per i punti di attivazione vengono successivamente utilizzate per far corrispondere i punti di attivazione con il contenuto della vista Rapida.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti di attivazione. Ogni punto di attivazione aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo univoco il prodotto nel sistema di back-end esistente.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti di attivazione.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione della visualizzazione rapida esistente. È probabile che tali utenti siano a conoscenza del set minimo di dati necessario per identificare la visualizzazione rapida nel sistema. Tuttavia, è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni delle viste Rapide utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, facendo clic su un pulsante &quot;Vista rapida&quot;.
* Il sito Web invia una richiesta Ajax al back-end per caricare, se necessario, i dati o il contenuto della visualizzazione rapida.
* I dati della vista Rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web in cui è implementata la funzione di visualizzazione rapida. Quindi attivate la visualizzazione Rapida e acquisite l’URL Ajax inviato dalla pagina Web per caricare i dati o il contenuto della visualizzazione Rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzare la relativa scheda Net. In alternativa, potete utilizzare lo strumento integrato Ispettore e la relativa scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione Rapida sulla pagina.

Ora trova l’URL Ajax della visualizzazione rapida nel registro di rete e copia l’URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione Rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Ciò si verifica in quanto gli URL di visualizzazione rapida possono avere parti comuni per una determinata categoria di siti Web. Tuttavia, vengono modificati solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile nell’URL della visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU è l’unico dato necessario per aggiungere aree sensibili all’immagine del banner.

Tuttavia, in casi complessi, l’URL di visualizzazione rapida presenta elementi diversi oltre allo SKU. Ad esempio, elementi variabili possono includere ID categoria, codice colore e codice dimensione. In tali casi, ogni elemento è una variabile separata nella definizione dei dati del punto di attivazione nella funzione immagine interattiva acquistabile in  risorse di Experience Manager.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti di attivazione:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa di query.</p> </td>
    <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile dell’URL è il valore del parametro della stringa di query productId= ed è chiaramente un valore SKU. Pertanto, i punti di attivazione richiedono solo campi SKU compilati con valori quali <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso dell’URL.</p> </td>
    <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU dei punti di attivazione: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa di query.</p> </td>
    <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel parametro <code>prodId</code> e la categoria ID<code></code> è memorizzata nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni dei punti di attivazione sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

È possibile applicare lo stesso approccio utilizzato nei tre esempi sopra alla pagina Web [demo](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).

La pagina Web demo contiene diverse miniature di prodotto, ognuna delle quali presenta un pulsante di visualizzazione rapida con l&#39;etichetta &quot;Ulteriori informazioni&quot;. Con lo strumento di debug del browser Web ancora attivato, fate clic su ciascun pulsante e prendete nota degli URL di visualizzazione rapida registrati. Dopo aver attivato tutte e quattro le visualizzazioni rapide del prodotto disponibili sulla pagina, è disponibile il seguente elenco di richieste di visualizzazione rapida effettuate sul back-end:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Osservando le chiamate al server, potete vedere che le informazioni specifiche per il prodotto sono presenti solo nel percorso di richiesta. Si noti inoltre che la stringa di query non viene utilizzata e che sono coinvolti due tipi distinti di dati:

* Il primo tipo è Uomo o Donna. Puoi chiamare questa &quot;categoria di prodotti&quot;.
* Il secondo tipo è il nome del prodotto, come CamoPullover, che è probabilmente lo SKU del prodotto.

In base a tali informazioni, l’intero URL della visualizzazione rapida presenta il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, per i punti di attivazione si utilizzerebbero `categoryId` e `SKU`.

È ora possibile caricare un banner immagine e aggiungervi degli hotspot tramite la funzione per immagini interattive acquistabile in  AEM Assets.

## (Facoltativo) Creazione di un predefinito per visualizzatori immagini interattivi {#optional-creating-an-interactive-image-viewer-preset}

Potete scegliere di utilizzare il predefinito per visualizzatori di immagini interattive predefinito, denominato `Shoppable_Banner` fornito con  AEM Assets. Oppure potete creare un predefinito per visualizzatori personalizzato da usare con immagini interattive.

Quando create un predefinito per visualizzatori di immagini interattive personalizzato, potete determinare l’aspetto dei punti attivi nel banner immagine. Come parte della creazione del predefinito per visualizzatori, potete scegliere di usare un elemento grafico per punti di attivazione da una raccolta di immagini predefinite.

Dopo aver salvato il predefinito per visualizzatori, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefiniti visualizzatore  AEM Assets. Questa funzionalità significa che è visibile nel componente Contenuti multimediali interattivi e ogni volta che visualizzate una risorsa. Tuttavia, per *distribuire* un banner interattivo con questo predefinito per visualizzatori, *pubblicate* anche il predefinito per visualizzatori. Questa regola è valida per i predefiniti per visualizzatori personalizzati o predefiniti.

**Per creare un predefinito per visualizzatori immagini interattivi**

1. Nella barra a sinistra, toccate **[!UICONTROL Strumenti > Risorse > Predefiniti visualizzatore]**.
1. Vicino all&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Nuovo predefinito per visualizzatori, digitate un nome per descrivere il predefinito per visualizzatori per banner interattivi.

   Questo titolo viene visualizzato nella pagina dell’elenco Predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva]**.
1. Toccate **[!UICONTROL Crea]**.
1. Nella pagina Modifica predefinito per visualizzatori, toccate la scheda **[!UICONTROL Aspetto]**.
1. Effettua una delle operazioni seguenti:

   * Per caricare un’immagine del punto di attivazione che desiderate usare sulle immagini, toccate l’icona del selettore delle risorse. Nella pagina Seleziona contenuto, individuate l’immagine del punto di attivazione che desiderate usare e selezionatela. Toccate l’icona con il segno di spunta nell’angolo in alto a destra.
   * Per selezionare un&#39;immagine per un punto di attivazione predefinito, toccate l&#39;icona Galleria punti di attivazione. Nella palette Galleria punti di attivazione, toccate l’immagine del punto di attivazione da usare.

1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva]**.

   Accertatevi di pubblicare il nuovo predefinito per visualizzatori.

   Consultate [Predefiniti visualizzatore pubblicazione](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   È ora possibile caricare un banner immagine.

## Caricamento di un banner immagine {#uploading-an-image-banner}

Se avete già caricato le immagini che desiderate usare, passate al passaggio successivo, [Aggiunta di punti di attivazione a un banner di immagine](#adding-hotspots-to-an-image-banner).

**Per caricare un banner immagine**

1. Caricate i banner immagine da rendere interattivi.

   Consultate [Caricamento delle risorse](/help/assets/manage-digital-assets.md#uploading-assets).

   È ora possibile aggiungere punti di attivazione al banner immagine; consulta l’attività successiva di seguito.

## Aggiunta di punti attivi a un banner di immagine {#adding-hotspots-to-an-image-banner}

Potete aggiungere punti di attivazione a un banner di immagini utilizzando l&#39;editor nella pagina Gestione dei punti di attivazione.

Quando aggiungete degli hotspot, potete definirli come una visualizzazione a comparsa della vista Rapida, come un collegamento ipertestuale o un frammento esperienza.

Vedere [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Al contrario, usate o create dei predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell’immagine interattiva, potete usare Anteprima per vedere in che modo l’immagine interattiva viene visualizzata ai clienti.

Consultate [(facoltativo) Anteprima delle immagini interattive](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando aggiungete punti attivi a un’immagine in un’immagine interattiva o in un banner carosello, le informazioni relative ai punti attivi vengono memorizzate nella stessa posizione di metadati. Questa posizione è relativa alla posizione dell’immagine, a prescindere dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzione consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti di attivazione definiti, in entrambi i visualizzatori.
Tenete presente, tuttavia, che i banner carosello supportano le mappe immagine sulle immagini che possono anche contenere punti di attivazione; un’immagine interattiva non lo è. Tenete presente questo concetto se intendete creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. Potete creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
Vedere anche [Carosello Banner](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

**Per aggiungere punti attivi a un banner di immagine**

1. Nella vista Risorse, individuate il banner immagine da rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Passate il puntatore del mouse sull&#39;immagine, quindi toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, toccare **[!UICONTROL Modifica]**.

   * Passa il mouse sull&#39;immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica]**.

   * Per aprirlo nella pagina Visualizzazione dettagli, toccate l’immagine. Nella barra degli strumenti, toccare **[!UICONTROL Modifica]**.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Aggiungi punto attivo]** (icona a forma di dito che tocca) per aprire la pagina Gestione punti attivi.
1. Vicino all&#39;angolo superiore sinistro della pagina, toccare **[!UICONTROL Punto attivo]**.

   1. Vicino all&#39;angolo superiore sinistro della pagina Gestione dei punti attivi, toccare **[!UICONTROL Punto attivo]**.
   1.  Sull’immagine, tocca la posizione in cui vuoi visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione. Oppure, utilizzare i tasti freccia della tastiera per controllare la posizione di un punto sensibile selezionato.
   1. Aggiungere altri punti di attivazione, se necessario, ripetendo i passaggi a e b.
   1. (Facoltativo) Per eliminare un punto di attivazione, selezionatelo sull&#39;immagine, quindi toccate **[!UICONTROL Elimina]** (icona cestino) sotto l&#39;intestazione **[!UICONTROL Punti attivi]**.

1. Nel campo di testo Nome, digitate il nome del punto di attivazione. Questo nome viene visualizzato anche nell&#39;elenco a discesa Area sensibile selezionata.
1. Effettua una delle operazioni seguenti:

   * Toccate **[!UICONTROL Vista rapida]**.

      * Se siete un cliente  AEM Sites o eCommerce, toccate o fate clic sull&#39;icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Selezione prodotto. Toccate il prodotto che desiderate utilizzare, quindi toccate **Seleziona** nell&#39;angolo superiore destro della pagina. Viene nuovamente visualizzata la pagina di gestione dei punti attivi.
      * Se si è *not* un cliente di eCommerce o Siti di Experience Manager 

         * Vedere [Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables); è necessario definire queste variabili.
         * Quindi, immettete manualmente il valore SKU. Nel campo di testo Valore SKU, digitate lo SKU del prodotto. Il valore SKU immesso popola automaticamente la porzione variabile del modello di visualizzazione rapida. Garantisce che il sistema sia in grado di associare il punto di attivazione toccato a una particolare visualizzazione rapida SKU.
         * (Facoltativo) Se nella vista Rapida sono presenti altre variabili utilizzate per identificare ulteriormente un prodotto, toccate **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, `category=Mens` è una variabile aggiunta.
   * Toccate **[!UICONTROL Collegamento ipertestuale]**.

      * Se siete clienti di Siti di Experience Manager , toccate l&#39;icona Selettore sito (cartella). Individuate un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine di siti di Experience Manager .
      * Se siete clienti indipendenti, nel campo HREF specificate il percorso completo dell’URL di una pagina Web collegata.

   Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

   * Toccate **[!UICONTROL Frammento esperienza]**.

      * Se siete un cliente AEM Sites , toccate o fate clic sull’icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Toccate il frammento esperienza da utilizzare. Quindi toccate **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro della pagina. Viene nuovamente visualizzata la pagina di gestione dei punti attivi.
Vedere [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Specificate la larghezza e l&#39;altezza del frammento esperienza come desiderate venga visualizzato sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Al contrario, usate o create dei predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.



1. Toccate **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblicate l’immagine interattiva. La pubblicazione distribuisce il banner nel cloud e genera anche codice da incorporare che consente di effettuare l’integrazione con un sito Web di terze parti.

   Consultate [Pubblicazione di risorse](/help/assets/manage-digital-assets.md#publish-assets).

   Dopo aver aggiunto degli hotspot e pubblicato l’immagine interattiva, potete ora aggiungerla al sito Web esistente.

   Consultate [Integrazione di un&#39;immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima delle immagini interattive {#optional-previewing-interactive-images}

Potete usare Anteprima per vedere una rappresentazione dell’aspetto dell’immagine interattiva per i clienti. Anteprima consente inoltre di verificare i punti attivi dell’immagine per verificarne il funzionamento come previsto.

Una volta ottenuta l’immagine interattiva, potete pubblicarla.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consultate [Collegamento di URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.
Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Per visualizzare in anteprima le immagini interattive**

1. Nella vista Risorse, individuate un’immagine interattiva esistente creata e toccate per aprirla in Anteprima.
1. Nell’angolo in alto a sinistra della pagina Anteprima, nell’elenco a discesa Contenuto, toccate **[!UICONTROL Visualizzatori]**.
1. Nell’elenco Visualizzatori, toccate **[!UICONTROL Shoppable_Banner]** o il nome del predefinito per visualizzatori di immagini interattivo creato.
1. Per verificare le azioni associate dei punti di attivazione, toccate i punti di attivazione sull&#39;immagine.

## Pubblicazione di risorse di immagine interattive {#publishing-interactive-image-assets}

Consultate [Publishing Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

## Integrazione di un&#39;immagine interattiva con il sito Web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, vi potete aggiungere altri punti attivi e pubblicare l&#39;immagine interattiva, potete aggiungerla alla pagina del sito Web.

Se siete un cliente AEM Sites , potete aggiungere l’immagine interattiva trascinando il componente Supporto interattivo sulla pagina. Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Se siete clienti indipendenti  AEM Assets, potete aggiungere manualmente l’immagine interattiva al sito Web come descritto in questa sezione.

1. Copiate il codice da incorporare dell’immagine interattiva pubblicata.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungete il codice da incorporare copiato nella posizione desiderata all’interno della pagina Web.
Il codice da incorporare copiato è impostato per un ambiente reattivo in modo che si adatti automaticamente all&#39;area assegnata.

**Esempio**

Utilizzando il sito Web [demo come esempio](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html), si noti che l&#39;immagine dei tre uomini è un tag statico `IMG`:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L&#39;integrazione è semplice come rimuovere il tag `IMG` e sostituirlo con il codice da incorporare copiato da  AEM Assets. Come potete vedere, il risultato [mostra l&#39;immagine interattiva acquistabile sulla pagina con tre punti di attivazione cerchio](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
A questo punto, i punti di attivazione sull&#39;immagine interattiva acquistabile del sito Web demo sono solo a scopo di visualizzazione. Non sono ancora integrati con le viste Rapide esistenti.

Per applicare un &quot;ritaglio&quot; a un&#39;immagine interattiva acquistabile per un ambiente reattivo, includete l&#39;attributo di configurazione Immagine interattiva `ZoomView.iscommand` al percorso. In questo caso, viene chiamato il componente `ZoomView` e `iscommand` è il comando di trasmissione delle immagini &quot;ritaglia&quot; applicato.

Vedere [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) attributo di configurazione.

Vedere [ritaglio](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) comando di gestione delle immagini.

È ora possibile integrare l’immagine interattiva con una vista Rapida esistente sul sito Web.

## Integrazione di un&#39;immagine interattiva con una vista Rapida esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Questa attività si applica solo se siete clienti  AEM Assets indipendenti.

L’ultimo passaggio di questo processo consiste nell’integrare l’immagine interattiva con un’implementazione esistente della visualizzazione rapida sul sito Web. Non esiste una soluzione all&#39;integrazione che funzioni per tutti i casi. Ogni implementazione della visualizzazione rapida è univoca ed è necessario un approccio specifico. In quanto tale, è utile coinvolgere l&#39;assistenza di un utente IT front-end.

L’implementazione della visualizzazione rapida esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL di visualizzazione rapida basato sull’elemento dell’interfaccia utente attivato al punto 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al punto 2.
1. La logica di back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati della vista rapida caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate non rappresentano necessariamente chiamate API pubbliche indipendenti richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Quando l’immagine interattiva acquistabile sostituisce il passaggio 1 e in parte il passaggio 2, un utente tocca un punto di attivazione all’interno dell’immagine acquistabile. Tale interazione utente viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati del punto attivo precedentemente aggiunti a  AEM Assets.

In un tale gestore di eventi, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dall&#39;immagine interattiva acquistabile.
* Crea un URL di visualizzazione rapida basato sui dati del punto di attivazione.
* Attiva il processo di caricamento della vista Rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice da incorporare restituito da Risorse  Experience Manager dispone di un gestore eventi pronto all’uso, commentato, come mostrato nel frammento di codice evidenziato seguente:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo fittizio del gestore con il codice specifico per la pagina Web specifica.

Il processo di creazione dell’URL di visualizzazione rapida è opposto a quello utilizzato per identificare le variabili dei punti di attivazione trattate in precedenza.

Vedere [Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables).

Utilizzando i precedenti esempi di URL della visualizzazione rapida, potete vedere negli esempi seguenti, in che modo l’URL della visualizzazione rapida viene costruito in ogni caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU singolo, trovato nella stringa di query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU singolo, trovato nel percorso URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID categoria nella stringa di query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

L’ultimo passaggio per attivare l’URL della visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede l’assistenza di un esperto IT front-end dell’azienda. Essi hanno la certezza di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio appropriato, avendo un URL di visualizzazione rapida pronto all’uso.

Potete vedere come questi passaggi vengono applicati al sito Web dimostrativo per integrare completamente un’immagine interattiva acquistabile con il codice della visualizzazione rapida. In precedenza, la struttura dell’URL della visualizzazione rapida era identificata come segue:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire questo URL all&#39;interno del gestore `quickViewActivate`, è possibile utilizzare i campi `categoryId` e `SKU`. Questi campi sono disponibili nell&#39;oggetto `inData` passato al gestore dal codice del visualizzatore:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo attiva la finestra di dialogo di visualizzazione rapida utilizzando una semplice chiamata di funzione `loadQuickView()`. Questa funzione richiede un solo argomento, ovvero l&#39;URL dei dati della visualizzazione rapida. Come tale, l&#39;ultimo passaggio per integrare l&#39;immagine interattiva acquistabile è aggiungere la seguente riga di codice al gestore `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

Di seguito è riportato il codice sorgente completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

Il sito Web [demo finale con l&#39;immagine interattiva completamente integrata](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html).

## Uso delle viste rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

Vedere [Uso delle viste rapide per creare finestre a comparsa personalizzate](/help/assets/dynamic-media/custom-pop-ups.md).
