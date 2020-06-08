---
title: Immagini interattive
description: Scopri come lavorare con le immagini interattive in Dynamic Media
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '4238'
ht-degree: 2%

---


# Immagini interattive{#interactive-images}

Potete rendere le immagini statiche ricche di immagini e creare esperienze coinvolgenti per i clienti trascinando e rilasciando punti di attivazione &quot;shoppable&quot; su un’immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o un servizio con una funzionalità &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot; diretta, punto vendita. I clienti possono toccare o fare clic su questi punti di attivazione ed essere collegati direttamente al prodotto o al servizio, aggiungerli a un carrello o essere collegati a una pagina Web. Esperienze dirette come queste aumentano il coinvolgimento e la conversione dei clienti sul sito Web.

Di seguito è riportato un banner acquistabile con una finestra a comparsa Quickview. Un utente attiva la visualizzazione rapida toccando il cerchio o il punto di attivazione del modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Consultate le immagini [interattive](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) nella pagina Web nella quale sono riportate le immagini.

## Guardate come vengono creati i banner immagine interattivi {#watch-how-interactive-image-banners-are-created}

Watch a 10 minute and 33 second walkthrough on [how interactive image banners are created](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Inoltre verrà illustrato come visualizzare in anteprima, modificare e distribuire i banner immagine interattivi.

## Avvio rapido: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le immagini interattive in Risorse AEM.

Cercare l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di Avvio rapido. Contiene una breve esercitazione basata su un esempio di pagina [Web in cui non sono ancora state aggiunte immagini interattive](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



Questa esercitazione illustra i passaggi necessari per integrare le immagini interattive nel sito Web.

Passaggi Immagini interattive:

1. **(Facoltativo) Identificazione delle variabili** per i punti di attivazione - Se utilizzate Risorse AEM e Contenuti multimediali dinamici standalone, iniziate identificando le variabili dinamiche utilizzate nell’implementazione esistente di Quickview in modo da poter inserire i dati per i punti di attivazione al momento della creazione dell’immagine interattiva. Consultate [(Facoltativo) Identificazione delle variabili](#optional-identifying-hotspot-variables)dei punti di attivazione.
Tuttavia, se utilizzi AEM Sites, AEM eCommerce o entrambi, questo passaggio non è necessario.

1. **(Facoltativo) Creazione di un predefinito** per visualizzatori di immagini interattive - Personalizzare l’immagine grafica utilizzata per rappresentare i punti attivi. La creazione di un predefinito per visualizzatori di immagini interattive non è necessaria se intendete usare il predefinito per visualizzatori di immagini interattive fornito con il nome `Shoppable_Banner` .
Consultate [(Facoltativo) Creazione di un predefinito](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset)per visualizzatori immagini interattivi.

1. **Caricamento di un banner** immagine - Caricamento dei banner immagine da rendere interattivi.
Consultate [Caricamento di un banner](#uploading-an-image-banner)immagine.

1. **Aggiunta di punti attivi a un banner** di immagini - Aggiungete uno o più punti attivi a un banner di immagini e associateli a un’azione come un collegamento ipertestuale, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto i punti di attivazione, questa attività verrà completata pubblicando l&#39;immagine interattiva.
Consultate [Aggiunta di punti attivi a un banner](#adding-hotspots-to-an-image-banner)immagine.
Consultate [Anteprima delle immagini](#optional-previewing-interactive-images) interattive - Facoltativo. Se necessario, potete visualizzare una rappresentazione del banner acquistabile e verificarne l’interattività.
Consultate [Pubblicazione di risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

1. **Aggiunta di un’immagine interattiva al sito Web o al sito Web in AEM** Se utilizzate AEM Sites, AEM eCommerce o entrambi, potete aggiungere l’immagine interattiva direttamente a una pagina Web in AEM trascinando il componente Supporto interattivo sulla pagina. See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
Se utilizzi Risorse AEM e Contenuti multimediali dinamici autonomamente, devi copiare il codice da incorporare nel tuo sito Web e quindi integrarlo con la visualizzazione rapida esistente. Consultate [Integrazione di un’immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).
Se utilizzate un WCM di terze parti (Web Content Manager), dovete integrare il nuovo video interattivo con l’implementazione esistente di Quickview utilizzata sul vostro sito Web. Consultate [Integrazione di un’immagine interattiva con una visualizzazione rapida](#integrating-an-interactive-image-with-an-existing-quickview)esistente.

## (Facoltativo) Identificazione delle variabili dei punti di attivazione {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività all’immagine, attivate l’opzione Visualizzazioni rapide.
>* L’implementazione di AEM *non* utilizza un framework di integrazione eCommerce per estrarre i dati di prodotto in AEM da soluzioni di eCommerce come IBM Websfera Commerce, Elastic Path, hybris o Intershop.

>
>
Se l’implementazione di AEM utilizza eCommerce, puoi saltare questa attività e passare all’attività successiva.

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente di Quickview in modo da poter inserire i dati dei punti di attivazione per creare l’immagine interattiva.

Quando aggiungi punti attivi a un&#39;immagine banner in Risorse AEM, devi assegnare un SKU (Stock Keeping Unit); un identificatore univoco per ciascun prodotto o servizio distinto offerto) e variabili aggiuntive facoltative per ciascun punto di attivazione. Tali variabili per i punti di attivazione vengono successivamente utilizzate per far corrispondere i punti di attivazione con il contenuto della visualizzazione rapida.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti di attivazione. Ogni punto di attivazione aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo univoco il prodotto nel sistema di back-end esistente.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti di attivazione.

A volte può essere sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview, in quanto è probabile che sappiano quale sia il set minimo di dati necessario per identificare Quickview nel sistema. Tuttavia, nella maggior parte dei casi è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, facendo clic su un pulsante &quot;Quickview&quot;.
* Il sito Web invia una richiesta Ajax al back-end per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati della visualizzazione rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web esistente in cui è implementata la funzione Quickview, attivare la visualizzazione rapida e acquisire l’URL Ajax inviato dalla pagina Web per caricare i dati o il contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzare la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Ispettore e la relativa scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attivare la visualizzazione rapida sulla pagina.

Ora trova l’URL Ajax di Quickview nel registro di rete e copia l’URL registrato per l’analisi futura. Nella maggior parte dei casi, quando si attiva la visualizzazione rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi nell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml`o `text/javascript`.

Durante questo processo è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida possono avere parti comuni per una determinata categoria di sito Web, ma possono essere modificati solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile dell’URL di visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU è l’unico dato necessario per aggiungere aree sensibili all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta elementi diversi oltre allo SKU, come ID categoria, codice colore, codice dimensione e così via. In tali casi, ogni elemento è una variabile separata nella definizione dei dati del punto di attivazione nella funzione di immagine interattiva acquistabile in Risorse AEM.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti di attivazione:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa di query.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile dell’URL è il valore del parametro della stringa di query productId= ed è chiaramente un valore SKU. Pertanto, i nostri punti di attivazione richiedono solo campi SKU popolati con valori quali <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso dell’URL.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU dei punti di attivazione: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa di query.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel <code>prodId</code> parametro e l'ID<code></code> categoria è memorizzato nel <code>category=</code> parametro.</p> <p>Di conseguenza, le definizioni dei punti di attivazione sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>SKU è <strong><code>305466</code></strong> ed <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>SKU è <strong><code>310181</code></strong> ed <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU è <strong><code>308706</code></strong> ed <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Potete applicare lo stesso approccio utilizzato nei tre esempi riportati sopra alla pagina [Web della](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)demo.

La pagina Web demo contiene diverse miniature di prodotto, ognuna delle quali contiene un pulsante di visualizzazione rapida con l&#39;etichetta &quot;Ulteriori informazioni&quot;. Con lo strumento di debug del browser Web ancora attivato, fate clic su ciascun pulsante e prendete nota degli URL di visualizzazione rapida registrati. Dopo aver attivato tutte e quattro le quickview del prodotto disponibili sulla pagina, è disponibile il seguente elenco di richieste Quickview effettuate sul back-end:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Osservando queste chiamate al server, le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Si noti inoltre che la stringa di query non viene utilizzata e che sono coinvolti due tipi distinti di dati:

* Il primo tipo è Uomo o Donna. Puoi chiamare questa &quot;categoria di prodotti&quot;.
* Il secondo tipo è il nome del prodotto, ad esempio CamoPullover. Potete presumere che questo sia lo SKU del prodotto.

Considerate queste informazioni, l’intero URL di Quickview presenta il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, si utilizzerebbero `categoryId` e `SKU` per i punti di attivazione.

È ora possibile caricare un banner immagine e aggiungervi degli hotspot tramite la funzione per immagini interattive acquistabile in Risorse AEM.

## (Facoltativo) Creazione di un predefinito per visualizzatori immagini interattivi {#optional-creating-an-interactive-image-viewer-preset}

Potete scegliere di utilizzare il predefinito per visualizzatori di immagini interattive predefinito, denominato `Shoppable_Banner` che include Risorse AEM. Oppure potete creare un predefinito per visualizzatori personalizzato da usare con immagini interattive.

Quando create un predefinito per visualizzatori di immagini interattive personalizzato, potete determinare l’aspetto dei punti attivi nel banner immagine. Come parte della creazione del predefinito per visualizzatori, potete scegliere di usare un elemento grafico per punti di attivazione da una raccolta di immagini predefinite.

Dopo aver salvato il predefinito per visualizzatori, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefiniti visualizzatore di Risorse AEM. Questa funzionalità significa che è visibile nel componente Contenuti multimediali interattivi e ogni volta che visualizzate una risorsa. Tuttavia, per *fornire *un banner interattivo con questo predefinito per visualizzatori, dovete anche *pubblicare *il predefinito per visualizzatori (vale per i predefiniti per visualizzatori personalizzati o forniti con Scene7).

**Per creare un predefinito per visualizzatori immagini interattivi**

1. Nella barra a sinistra, toccate **[!UICONTROL Strumenti > Risorse > Predefiniti]** visualizzatore.
1. Near the upper-right corner of the page, tap **[!UICONTROL Create]**.
1. Nella finestra di dialogo Nuovo predefinito per visualizzatori, digitate un nome per descrivere il predefinito per visualizzatori per banner interattivi.

   Titolo che verrà visualizzato nella pagina dell’elenco Predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva]**.
1. Toccate **[!UICONTROL Crea]**.
1. On the Edit Viewer Preset page, tap the **[!UICONTROL Appearance]** tab.
1. Effettua una delle operazioni seguenti:

   * Per caricare un’immagine del punto di attivazione che desiderate usare sulle immagini, toccate l’icona del selettore delle risorse. Nella pagina Seleziona contenuto, individuate l’immagine del punto di attivazione da usare, selezionatela, quindi toccate l’icona con il segno di spunta nell’angolo superiore destro.
   * Per selezionare un&#39;immagine per un punto di attivazione predefinito, toccate l&#39;icona Galleria punti di attivazione. Nella palette della galleria del punto di attivazione, toccate l’immagine del punto di attivazione che desiderate usare.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**.

   Accertatevi di pubblicare il nuovo predefinito per visualizzatori.

   See [Publishing Viewer Presets](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   È ora possibile caricare un banner immagine.

## Caricamento di un banner immagine {#uploading-an-image-banner}

Se avete già caricato le immagini da usare, passate al passaggio successivo e [Aggiungete punti attivi a un banner](#adding-hotspots-to-an-image-banner)di immagine.

**Per caricare un banner immagine**

1. Caricate i banner immagine da rendere interattivi.

   See [Uploading assets](/help/assets/manage-digital-assets.md#uploading-assets).

   È ora possibile aggiungere punti di attivazione al banner immagine; consulta l’attività successiva di seguito.

## Aggiunta di punti attivi a un banner di immagine {#adding-hotspots-to-an-image-banner}

Potete aggiungere punti attivi a un banner di immagini utilizzando l&#39;editor nella pagina Gestione dei punti attivi.

Quando aggiungete degli hotspot, potete definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Consulta Frammenti [](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)esperienza.

>[!NOTE]
>
>Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza.  Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell’immagine interattiva, potete usare Anteprima per vedere in che modo l’immagine interattiva verrà visualizzata ai clienti.

Consultate [(Facoltativo) Anteprima delle immagini](#optional-previewing-interactive-images)interattive.

>[!NOTE]
>
>Quando aggiungete punti di attivazione a un’immagine in un’immagine interattiva o in un banner carosello, le informazioni relative ai punti di attivazione vengono memorizzate nella stessa posizione di metadati, relativa alla posizione dell’immagine, indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti di attivazione definiti, in entrambi i visualizzatori.

>Tenete presente, tuttavia, che i banner carosello supportano le mappe immagine sulle immagini che possono anche contenere punti di attivazione; un’immagine interattiva non lo è. Tenete presente questo aspetto se intendete creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. È possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
>
>Consultate anche Banner [carosello](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
>
>Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

**Per aggiungere punti attivi a un banner di immagine**

1. Nella vista Risorse, individuate il banner immagine da rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). Sulla barra degli strumenti, toccate **[!UICONTROL Modifica]**.

   * Passa il mouse sull’immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica]**.

   * Toccate l’immagine per aprirla nella pagina Visualizzazione dettagli. Sulla barra degli strumenti, toccate **[!UICONTROL Modifica]**.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Aggiungi punto attivo]** (icona a forma di dito che tocca) per aprire la pagina Gestione punti attivi.
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot]**.

1. Nell’angolo in alto a sinistra della pagina Gestione dei punti attivi, toccate **[!UICONTROL Area sensibile]**.
1.  Sull’immagine, tocca la posizione in cui vuoi visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione.
1. Se necessario, potete aggiungere altri punti di attivazione ripetendo i passaggi a e b.
1. (Facoltativo) Per eliminare un punto di attivazione, selezionatelo sull&#39;immagine, quindi toccate **[!UICONTROL Elimina]** (icona cestino) sotto l&#39;intestazione **[!UICONTROL Punti attivi]** .

1. Nel campo di testo Nome, digitate il nome del punto di attivazione. Questo nome viene visualizzato anche nell&#39;elenco a discesa Area sensibile selezionata.
1. Effettua una delle operazioni seguenti:

   * Toccate **[!UICONTROL Visualizzazione rapida]**.

      * Se siete clienti AEM Sites o eCommerce, toccate o fate clic sull&#39;icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Selezione prodotto. Toccate o fate clic sul prodotto che desiderate utilizzare, quindi toccate **Select ** nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dei punti attivi.
      * Se *non* sei un cliente AEM Sites o eCommerce

         * Consultate [Identificazione delle variabili](#optional-identifying-hotspot-variables)dei punti di attivazione; sarà necessario definire queste variabili.
         * Quindi, immettete manualmente il valore SKU. Nel campo di testo Valore SKU, digitare lo SKU del prodotto (Stock Keeping Unit), che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU immesso popola automaticamente la porzione variabile del modello Quickview, in modo che il sistema sia in grado di associare il punto attivo toccato a una particolare visualizzazione Quickview dello SKU.
         * (Facoltativo) Se all’interno della visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, toccate **[!UICONTROL Aggiungi variabile]** generica. Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, `category=Mens` è una variabile aggiunta.
   * Toccate **[!UICONTROL Collegamento ipertestuale]**.

      * Se siete clienti di AEM Sites, toccate o fate clic sull&#39;icona Selettore sito (cartella) per passare a un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine AEM Sites.
      * Se siete clienti indipendenti, nel campo HREF specificate il percorso completo dell’URL di una pagina Web collegata.

   Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, consulta [Uso dei selettori](/help/assets/dynamic-media/working-with-selectors.md) .

   * Tap **[!UICONTROL Experience Fragment]**.

      * Se siete clienti di AEM Sites, toccate o fate clic sull&#39;icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Toccate o fate clic sul frammento esperienza che desiderate utilizzare, quindi toccate Seleziona nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dell&#39;area sensibile.
Consulta Frammenti [](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)esperienza.

      * Specificate la larghezza e l&#39;altezza del frammento esperienza così come apparirà sul banner.

         >[!NOTE]
         >
         >Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza.  Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.



1. Toccate **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblicate l’immagine interattiva. La pubblicazione consente la distribuzione del banner tramite cloud e la generazione del codice da incorporare se è necessario effettuare l’integrazione con un sito Web di terze parti.

   Consultate [Pubblicazione delle risorse](/help/assets/manage-digital-assets.md#publish-assets).

   Dopo aver aggiunto degli hotspot e pubblicato l’immagine interattiva, potete ora aggiungerla al sito Web esistente.

   Consultate [Integrazione di un’immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima delle immagini interattive {#optional-previewing-interactive-images}

Potete usare Anteprima per vedere l’aspetto dell’immagine interattiva per i clienti e per verificare i punti di attivazione dell’immagine in modo che si comportino come previsto.

Una volta ottenuta l’immagine interattiva, potete pubblicarla.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).
See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine AEM Sites.
See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Per visualizzare in anteprima le immagini interattive**

1. Nella vista Risorse, individuate un’immagine interattiva esistente creata e toccate per aprirla in Anteprima.
1. Nell’angolo in alto a sinistra della pagina Anteprima, toccate **[!UICONTROL Visualizzatori]** dall’elenco a discesa Contenuto.
1. Nell’elenco Visualizzatori, toccate **[!UICONTROL Shoppable_Banner]** o il nome del predefinito per visualizzatori di immagini interattivo creato.
1. Toccate i punti di attivazione sull&#39;immagine per verificare le azioni associate.

## Pubblicazione di risorse di immagine interattive {#publishing-interactive-image-assets}

Consultate [Pubblicazione di risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

## Integrazione di un’immagine interattiva con il sito Web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, aggiunto dei punti di attivazione all&#39;immagine e pubblicato l&#39;immagine interattiva, potete ora aggiungerla alla pagina del sito Web.

Se siete clienti di AEM Sites, potete aggiungere l’immagine interattiva trascinando il componente Supporto interattivo sulla pagina. See [Adding Dynamic Media Assets to Pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Se sei un cliente autonomo di Risorse AEM, puoi aggiungere manualmente l’immagine interattiva al tuo sito Web come descritto in questa sezione.

1. Copiate il codice da incorporare dell’immagine interattiva pubblicata.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/dynamic-media/embed-code.md).

1. Aggiungete il codice da incorporare copiato nella posizione desiderata all’interno della pagina Web.
Il codice da incorporare copiato è impostato per un ambiente reattivo e dovrebbe quindi adattarsi automaticamente all&#39;area assegnata.

**Esempio**

Utilizzando il sito Web [demo come esempio](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html), si noti che l&#39;immagine dei tre uomini è un `IMG` tag statico:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L’integrazione è semplice come rimuovere il `IMG` tag e sostituirlo con il codice da incorporare copiato da AEM Assets. Potete vedere il risultato [che mostra l&#39;immagine interattiva acquistabile sulla pagina con tre punti di attivazione](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)circolari.

>[!NOTE]
>
>A questo punto, i punti di attivazione sull&#39;immagine interattiva acquistabile del sito Web demo sono solo a scopo di visualizzazione; non sono ancora integrati con le viste Quickview esistenti.

Per applicare un &quot;ritaglio&quot; a un’immagine interattiva acquistabile per un ambiente reattivo, potete includere l’attributo di configurazione Immagine interattiva `ZoomView.iscommand` nel percorso, dove `ZoomView` è il componente da chiamare ed `iscommand` è il comando di gestione delle immagini &quot;ritaglia&quot; applicato.

Consultate Attributo di configurazione [ZoomView.iscommand](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) .

Consultate [Ritagliare](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) le immagini, comando di gestione.

È ora possibile integrare l’immagine interattiva con una visualizzazione rapida esistente sul sito Web.

## Integrazione di un’immagine interattiva con una visualizzazione rapida esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Questa attività è valida solo se sei un cliente autonomo di Risorse AEM.

L’ultimo passaggio di questo processo consiste nell’integrare l’immagine interattiva con un’implementazione esistente di Quickview sul sito Web. Non esiste una soluzione all&#39;integrazione che funzioni per tutti i casi. Ogni implementazione di Quickview è univoca ed è necessario un approccio specifico che molto probabilmente coinvolga l&#39;assistenza di una persona IT front-end.

L’implementazione esistente di Quickview rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al punto 2.
1. La logica di back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate potrebbero non rappresentare chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Contemporaneamente alla sostituzione dell’immagine interattiva acquistabile con il passaggio 1 e in parte il passaggio 2, quando un utente fa clic su un punto di attivazione all’interno dell’immagine acquistabile, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati dei punti di attivazione precedentemente aggiunti a Risorse AEM.

In un tale gestore di eventi, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dall&#39;immagine interattiva acquistabile.
* Crea un URL di visualizzazione rapida basato sui dati del punto di attivazione.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering della visualizzazione sullo schermo.

Il codice da incorporare restituito da Risorse AEM dispone già di un gestore di eventi pronto all’uso, commentato, come mostrato nel frammento di codice evidenziato seguente:

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

Il processo di creazione dell’URL di visualizzazione rapida è sostanzialmente opposto a quello utilizzato per identificare le variabili dei punti di attivazione trattate in precedenza.

Consultate [Identificazione delle variabili](#optional-identifying-hotspot-variables)dei punti di attivazione.

Utilizzando i nostri precedenti esempi di URL di Quickview, potete vedere negli esempi seguenti in che modo l’URL di Quickview è costruito in ogni caso:

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

L’ultimo passaggio per attivare l’URL di visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un esperto IT front-end del reparto IT. Essi hanno la capacità di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio corretto, avendo un URL Quickview pronto all’uso.

Potete vedere come questi passaggi vengono applicati al sito Web dimostrativo per integrare completamente un’immagine interattiva acquistabile con il codice Quickview. In precedenza, la struttura dell’URL di Quickview era identificata come segue:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire questo URL all&#39;interno del `quickViewActivate` gestore, potete utilizzare i campi `categoryId` e `SKU` disponibili nell&#39; `inData` oggetto passato al gestore dal codice del visualizzatore:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo attiva la finestra di dialogo Quickview utilizzando una semplice chiamata `loadQuickView()` di funzione. Questa funzione richiede un solo argomento, ovvero l&#39;URL dei dati di Quickview. Come tale, l&#39;ultimo passaggio necessario per integrare l&#39;immagine interattiva acquistabile è quello di aggiungere la seguente riga di codice al `quickViewActivate` gestore:

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

Il sito Web dimostrativo [finale con l&#39;immagine](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)interattiva completamente integrata.

## Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/dynamic-media/custom-pop-ups.md).