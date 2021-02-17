---
title: Banner a carosello
description: Scoprite come utilizzare i banner carosello in Dynamic Media.
translation-type: tm+mt
source-git-commit: f5627a6e885a556700fbf56c4c63f0f4d6a89da0
workflow-type: tm+mt
source-wordcount: '4576'
ht-degree: 3%

---


# Banner a carosello{#carousel-banners}

I banner carosello consentono agli esperti di marketing di promuovere la conversione creando facilmente contenuti promozionali interattivi a rotazione e distribuendoli su qualsiasi schermo.

La creazione e la modifica dei contenuti contenuti contenuti nei banner promozionali può richiedere molto tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o rendendoli più mirati. I banner carosello consentono di creare o modificare rapidamente i banner a rotazione e di aggiungere interattività, ad esempio punti di attivazione collegati ai dettagli del prodotto o alle risorse correlate. Puoi distribuirli su qualsiasi schermo, per introdurre più rapidamente nuovi contenuti promozionali sul mercato.

I banner carosello sono contrassegnati da un banner con la parola **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Nel sito Web, un banner carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui puoi scorrere le immagini facendo clic sui numeri. Inoltre, le diapositive vengono ruotate automaticamente in base a un intervallo di tempo personalizzabile. Le immagini aggiunte nel banner carosello supportano sia punti attivi che mappe immagine. Gli utenti possono toccare o passare a un collegamento ipertestuale o accedere a una finestra di visualizzazione rapida.

In questo esempio, un utente ha toccato o fatto clic su una mappa immagine per accedere alla finestra di visualizzazione rapida dei guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Scoprite come creare i banner carosello {#watch-how-carousel-banners-are-created}

Guardate la procedura dettagliata di 10 minuti e 33 secondi sulla [modalità di creazione dei banner carosello](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Inoltre viene illustrato come visualizzare in anteprima, modificare e distribuire i banner carosello.

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al gruppo **[!UICONTROL dam-users]** per poter creare o modificare i banner del carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema, che può aggiungere l&#39;utente al gruppo **d[!UICONTROL am-users]**.

## Avvio rapido: Banner carosello {#quick-start-carousel-banners}

Per iniziare subito a lavorare:

1. [Identificare le variabili](#identifying-hotspot-and-image-map-variables)  dei punti di attivazione e delle mappe immagine (solo per i clienti che utilizzano Adobe Experience Manager Assets + Dynamic Media)

   Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente della visualizzazione rapida. In questo modo potete inserire correttamente i punti di attivazione e i dati delle mappe immagine durante il processo di creazione dei banner carosello in  risorse Experience Manager.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an AEM Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an AEM Assets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/dynamic-media/managing-viewer-presets.md).

   Gli amministratori possono personalizzare il comportamento e l’aspetto del carosello creando un proprio predefinito per visualizzatori Carosello. Il vantaggio principale è che potete riutilizzare questo predefinito per visualizzatori personalizzati per più caroselli. Tuttavia, gli utenti possono personalizzare il comportamento e l’aspetto del carosello direttamente durante la creazione del carosello. Questo approccio è preferibile se si desidera una progettazione specifica per un determinato carosello.

1. [Caricate un banner](#uploading-image-banners) immagine.

   Caricate i banner immagine da rendere interattivi.

1. [Create un set](#creating-carousel-sets) carosello.

   In Set caroselli, gli utenti si spostano tra le immagini dei banner e toccano i punti attivi o le mappe immagine per accedere ai contenuti pertinenti.

   Per creare un set carosello all’interno di Assets, tocca **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello]**. Aggiungi le risorse alle diapositive e tocca **[!UICONTROL Salva]**. Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungete punti di attivazione o mappe immagine a un banner immagine.](#adding-hotspots-or-image-maps-to-an-image-banner)

   Aggiungete uno o più punti di attivazione o mappe immagine a un banner immagine. Quindi, associateli a un’azione come un collegamento, una vista Rapida o un frammento esperienza. Dopo aver aggiunto punti di attivazione o mappe immagine, potete completare questa attività pubblicando il set di caroselli. Con la pubblicazione viene creato il codice da incorporare da copiare e applicare alla pagina di destinazione del sito Web.

   Consultate [(Facoltativo) Anteprima dei banner carosello.](#optional-previewing-carousel-banners) - Facoltativo. Se necessario, potete visualizzare una rappresentazione del set carosello e verificarne l’interattività.

1. [Pubblicare Banner](#publishing-carousel-banners) Carosello.

   Potete pubblicare un set di caroselli come qualsiasi altra risorsa. In Risorse, andate al set carosello e selezionatelo, quindi toccate **[!UICONTROL Pubblica]**. Quando si pubblica un set carosello, vengono attivati l’URL e la stringa da incorporare.

1. Effettua una delle operazioni seguenti:

   * [Aggiungete un banner carosello alla ](#adding-a-carousel-banner-to-your-website-page)pagina del sito WebPotete aggiungere nella pagina del sito Web l’URL del banner carosello o il codice da incorporare che avete copiato.

      * [Integrare il banner del carosello con una vista](#integrating-the-carousel-banner-with-an-existing-quickview) Rapida esistente. Se utilizzate un sistema di gestione dei contenuti Web di terze parti, dovete integrare il nuovo banner carosello con l’implementazione esistente della visualizzazione rapida sul sito Web.
   * [Aggiungi un banner carosello al tuo sito Web in Experience ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md) ManagerSe sei un cliente di Siti di Experience Manager  puoi aggiungere il set di carosello direttamente alla pagina in  Experience Manager utilizzando il componente Supporto interattivo.


Se è necessario modificare i set di caroselli, consultate [modifica dei set di caroselli.](#editing-carousel-sets) Inoltre, potete visualizzare e modificare le proprietà [ del set ](/help/assets/manage-digital-assets.md#editing-properties)carosello.

## Identificazione delle variabili dei punti di attivazione e delle mappe immagine {#identifying-hotspot-and-image-map-variables}

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente della visualizzazione rapida. Questo consente di inserire correttamente i punti di attivazione o i dati delle mappe immagine durante il processo di creazione dei set carosello in  risorse Experience Manager.

Quando aggiungete punti di attivazione o mappe immagine a un&#39;immagine del banner, potete assegnare un SKU e variabili aggiuntive facoltative a ogni punto di attivazione o mappa immagine. Tali variabili vengono utilizzate successivamente per far corrispondere punti attivi o mappe immagine con il contenuto della visualizzazione rapida.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an AEM Sites and/or AEM Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an AEM Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

È importante identificare in modo appropriato il numero e il tipo di variabili da associare ai dati dei punti di attivazione o delle mappe immagine. Ogni punto sensibile o mappa immagine aggiunta a un&#39;immagine banner deve contenere informazioni sufficienti per identificare in modo chiaro il prodotto nel sistema back-end esistente. Allo stesso tempo, accertatevi che ogni punto di attivazione o mappa immagine non includa più dati del necessario. Questo perché renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione continua dei punti attivi o delle mappe immagine più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati di aree sensibili o mappe immagine.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione della visualizzazione rapida esistente. È probabile che sappiano qual è il set minimo di dati per identificare la visualizzazione rapida nel sistema. Tuttavia, è possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni delle viste Rapide utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, questo accade quando tocca un pulsante **[!UICONTROL Quick View (Visualizzazione rapida)]**.
* Il sito Web invia una richiesta Ajax al back-end per caricare, se necessario, i dati o il contenuto della visualizzazione rapida.
* I dati della vista Rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web in cui è implementata la funzione di visualizzazione rapida. Quindi attivate la vista Rapida e acquisite l’URL Ajax inviato dalla pagina Web per caricare i dati o il contenuto della vista Rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premete F12 (Windows) o Comando-Opzione-I (Mac) per aprire il pannello degli strumenti per sviluppatori. Toccate la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows) o Comando-Opzione-I (Mac). Utilizzare la scheda Rete oppure utilizzare lo strumento integrato Ispettore e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione Rapida sulla pagina.

Ora trova l’URL Ajax della visualizzazione rapida nel registro di rete e copia l’URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione Rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida hanno parti comuni per una determinata categoria di siti Web, ma cambiano solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile nell’URL della visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU è l’unico dato necessario per aggiungere aree sensibili o mappe immagine all’immagine del banner.

Tuttavia, in casi complessi, l’URL di visualizzazione rapida presenta elementi diversi oltre allo SKU, come ID categoria, codice colore, codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto di attivazione o della mappa immagine nella funzione del banner del carosello.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di aree sensibili o mappe immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>SKU singolo, trovato nella stringa di query.</td>
   <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L'unica parte variabile dell'URL è il valore del parametro della stringa di query <code>productId=</code>, che è chiaramente un valore SKU. Pertanto, i punti di attivazione o le mappe immagine richiedono solo campi SKU compilati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU singolo, trovato nel percorso dell’URL.</td>
   <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell'ultima parte del percorso e diventa il valore SKU delle aree sensibili/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa di query.</td>
   <td><p>Gli URL registrati per la visualizzazione rapida includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel parametro <code>prodId</code> e l'ID categoria è memorizzato nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni di aree sensibili e mappe immagine sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Caricamento dei banner immagine {#uploading-image-banners}

Se avete già caricato le immagini che desiderate usare, passate al passaggio successivo, [Creazione di set di carosello](#creating-carousel-sets). Le immagini utilizzate nel carosello devono essere caricate dopo l’attivazione di Dynamic Media.

Per caricare i banner immagine, consultate [Caricamento delle risorse](/help/assets/manage-digital-assets.md).

## Creazione di set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al gruppo **[!UICONTROL dam-users]** per poter creare o modificare i banner del carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema, che può aggiungere l&#39;utente al gruppo **[!UICONTROL dam-users]**.

**Per creare un set carosello**

1. In Risorse, andate alla cartella in cui desiderate creare il set carosello e toccate **[!UICONTROL Crea > Set carosello]**.
1. Nella pagina Editor banner carosello toccate **[!UICONTROL Toccate per aprire Selettore risorsa]** per selezionare l&#39;immagine per la prima diapositiva.

   Nella pagina Editor banner carosello, effettuate una delle seguenti operazioni:

   * Vicino all&#39;angolo superiore sinistro della pagina, toccare l&#39;icona **[!UICONTROL Aggiungi diapositiva]**.

   * Vicino al centro della pagina, toccate **[!UICONTROL Toccate per aprire Selettore risorsa]**.
   Tocca per selezionare le risorse da includere nel Set carosello. Sulle risorse selezionate è presente un’icona con il segno di spunta. Al termine, nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Selezionate il filtro e toccate l&#39;icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

1. Continuate ad aggiungere diapositive finché non avrete aggiunto tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Se necessario, trascinate le diapositive per riordinare le immagini nell’elenco.
   * Per eliminare un&#39;immagine, selezionate l&#39;immagine, quindi toccate **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.

   * Per applicare un predefinito, toccate l’elenco a discesa dei predefiniti accanto all’angolo superiore destro della pagina, quindi selezionate un predefinito da applicare al set contemporaneamente.
   Per eliminare una diapositiva, toccate o fate clic sulla diapositiva e toccate o fate clic su **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti. Per spostare una diapositiva, toccate l’icona di riordinamento e tenete premuto e spostatevi nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, potete aggiungere un punto di attivazione, una mappa immagine o entrambi all’immagine. Vedere [aggiunta di punti di attivazione o mappe immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Per modificare la progettazione visiva e il comportamento dei set carosello, toccate o fate clic sulle schede Comportamento e Aspetto e regolate l’aspetto del banner del carosello o il funzionamento di componenti specifici. Consultate [Gestione dei predefiniti per visualizzatori](/help/assets/dynamic-media/viewer-presets.md) per ulteriori informazioni sull&#39;utilizzo dell&#39;editor per visualizzatori.

   >[!NOTE]
   >
   >Per i banner carosello, potete regolare quanto segue:
   >    * Durata della visualizzazione di un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >    * Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. È possibile modificare questa impostazione in una transizione diapositiva.
   >    * Stile dei pulsanti. Gli utenti possono ruotare i banner toccando ogni punto o numero. È possibile modificare la posizione in cui appaiono i pulsanti degli indicatori di set (e se si tratta di uno stile numerico o punteggiato) e le loro dimensioni.
   >    * Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per i punti di attivazione.
   >    * Prima di modificare un predefinito per visualizzatori, scegliete lo stile su cui basare il predefinito. Se non scegliete uno stile, quando iniziate a modificare il predefinito per visualizzatori perdete tutte le modifiche se decidete di passare a un altro predefinito.


   Potete anche visualizzare l’anteprima dell’aspetto del banner del carosello. Consultate [(facoltativo) Anteprima dei banner carosello](#optional-previewing-carousel-banners).

1. Toccate **[!UICONTROL Save]** al termine.

## Aggiunta di punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Potete aggiungere punti attivi o mappe immagine a un banner utilizzando l&#39;editor di set carosello.

Quando aggiungete aree sensibili o mappe immagine, potete definirle come una visualizzazione a comparsa della vista Rapida, come un collegamento ipertestuale o un frammento esperienza.

Vedere [Frammento esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorporate il visualizzatore in un frammento esperienza.
>
>Per risolvere questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

Quando aggiungete punti di attivazione o mappe immagine a un’immagine, ricordate di salvare il lavoro. Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, potete facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner carosello per i clienti.

Vedere [(facoltativo) Anteprima dei banner carosello.](#optional-previewing-carousel-banners)

>[!NOTE]
>
>Quando aggiungete punti di attivazione a un&#39;immagine in un [Immagine interattiva](/help/assets/dynamic-media/interactive-images.md) o in un banner carosello, le informazioni relative ai punti di attivazione vengono memorizzate nella stessa posizione di metadati, relativa alla posizione dell&#39;immagine. Questo punto è vero a prescindere dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti di attivazione definiti, in entrambi i visualizzatori.
Tenete presente, tuttavia, che i banner carosello supportano le mappe immagine sulle immagini che possono anche contenere punti di attivazione; un’immagine interattiva non lo è. Tenete presente questo suggerimento se intendete creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. Provate a creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Per aggiungere punti attivi o mappe immagine a un banner immagine**

1. Da Risorse, andate al set di caroselli da rendere interattivo.
1. Selezionare il set carosello e toccare **[!UICONTROL Modifica]**. Viene aperto l’Editor visualizzatore carosello.
1. Selezionate la diapositiva da rendere interattiva.
1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine]**.
1. Effettuate una delle seguenti operazioni:

   * Per i punti attivi: Sull&#39;immagine, toccate la posizione in cui desiderate visualizzare il punto di attivazione.
   * Per le mappe immagine: Sull’immagine, fate clic, quindi trascinate dall’angolo in alto a sinistra verso l’angolo in basso a destra per creare l’area della mappa immagine. Per regolare le dimensioni della mappa immagine, trascinatene gli angoli.

   Se necessario, trascinate il punto di attivazione o la mappa immagine in una nuova posizione. Oppure, utilizzare i tasti freccia della tastiera per controllare la posizione di un punto di attivazione selezionato. Aggiungete altri punti di attivazione o mappe immagine secondo necessità.

   Per eliminare un punto attivo o una mappa immagine, tocca la scheda **[!UICONTROL Azioni]**. Nell&#39;intestazione **[!UICONTROL Mappe e punti attivi]**, dall&#39;elenco a discesa **[!UICONTROL Tipo selezionato]**, selezionare il nome del punto di attivazione o della mappa immagine da rimuovere. Tocca l’icona **[!UICONTROL Cestino]** accanto al menu, quindi seleziona **[!UICONTROL Elimina]**.

1. Nel campo di testo Nome, digitate il nome del punto di attivazione o della mappa immagine. Questo nome viene visualizzato anche nell&#39;elenco a discesa **[!UICONTROL Mappe &amp; Hotspot]**. Fornendo un nome è facile identificare il punto di attivazione o la mappa immagine se si decide di modificarla in futuro.
1. Effettuare una delle seguenti operazioni nella scheda **[!UICONTROL Azioni]**:

   * Toccate **[!UICONTROL Vista rapida]**.

      * Se siete un cliente di Siti di Experience Manager  <!-- and Ecommerce-->, toccate l&#39;icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Selezione prodotto. Per tornare all’Editor banner carosello, toccate il prodotto da utilizzare, quindi toccate il segno di spunta nell’angolo superiore destro della pagina.
      * Se non siete un cliente di Siti di Experience Manager  <!-- or Ecommerce -->:

         * Definire le variabili. Vedere [Identificazione delle variabili dei punti di attivazione](#identifying-hotspot-and-image-map-variables).
         * Quindi, immettete manualmente il valore SKU. Nel campo di testo Valore SKU, digitare lo SKU del prodotto (Stock Keeping Unit), che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU immesso popola automaticamente la porzione variabile del modello di visualizzazione rapida in modo che il sistema sappia associare il punto attivo toccato a una particolare vista Rapida dello SKU.
         * (Facoltativo) Se nella vista Rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, toccare **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).
   * Toccate **[!UICONTROL Collegamento ipertestuale]**.

      * Se siete clienti AEM Sites , toccate l&#39;icona Selettore sito (cartella) per passare a un URL.

         >[!NOTE]
         Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.

      * Se siete clienti indipendenti, nel campo di testo href specificate il percorso completo dell’URL di una pagina Web collegata.

   Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

   * Toccate **[!UICONTROL Frammento esperienza]**.

      * Se siete un cliente AEM Sites , toccate l’icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Per tornare alla pagina di gestione dei punti attivi, tocca o fai clic sul frammento esperienza da utilizzare, quindi tocca Seleziona nell’angolo superiore destro della pagina.
Vedere [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Specificate la larghezza e l&#39;altezza del frammento esperienza così come viene visualizzato sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorporate il visualizzatore in un frammento esperienza.
         Per aggirare questo punto, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Potete anche visualizzare l’anteprima dell’aspetto del banner del carosello. Consultate [(facoltativo) Anteprima dei banner carosello](#optional-previewing-carousel-banners).

1. Toccate **[!UICONTROL Salva]**.
1. Pubblicate il set carosello. La pubblicazione crea il codice da incorporare o l’URL che potete utilizzare nella pagina del sito Web. Se siete clienti di Siti di Experience Manager , aggiungete il set di carosello direttamente alla pagina Web.

   Consultate [Pubblicazione di risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Vedere [Aggiunta di un set carosello alla pagina di destinazione del sito Web](#adding-a-carousel-banner-to-your-website-page)

## Modifica dei set di caroselli {#editing-carousel-sets}

>[!NOTE]
Gli utenti non amministrativi devono essere aggiunti al gruppo **[!UICONTROL dam-users]** per poter creare o modificare i banner del carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema, che può aggiungere l&#39;utente al gruppo **[!UICONTROL dam-users]**.

Potete eseguire diverse attività di modifica su Set carosello, ad esempio:

* Aggiungete le diapositive a un set carosello. Vedere anche [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Eliminate le risorse nel set carosello.
* Applicate un predefinito per visualizzatori.
* Eliminate il set di caroselli.
* Aggiungere o modificare punti di attivazione e mappe immagine. Vedere anche [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

**Per modificare un set di caroselli**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa Set carosello, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa Set carosello, toccate **[!UICONTROL Seleziona]** (icona con il segno di spunta), quindi toccate **[!UICONTROL Modifica]** nella barra degli strumenti.

   * Toccate una risorsa Set carosello, quindi nell’angolo in alto a sinistra della pagina toccate **[!UICONTROL Modifica]** (icona matita).

1. Per modificare il set di caroselli, effettuate una delle seguenti operazioni:

   * Per aggiungere una diapositiva, toccate l&#39;icona **[!UICONTROL Aggiungi diapositiva]**, quindi individuate la risorsa da aggiungere alla diapositiva e toccate o fate clic sul segno di spunta.
   * Per riordinare le diapositive, trascinate una diapositiva in una nuova posizione (selezionate l’icona di riordinamento per spostare gli elementi).
   * Per aggiungere un punto di attivazione o una mappa immagine, fai clic sulle icone del punto di attivazione o della mappa immagine e vedi [aggiunta di punti di attivazione e mappe immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Per modificare l&#39;aspetto o il comportamento del set carosello, toccare la scheda **[!UICONTROL Aspetto]** o **[!UICONTROL Comportamento]**, quindi impostare le opzioni desiderate.
   * Per modificare punti di attivazione o mappe immagine, nella diapositiva appropriata selezionate un punto di attivazione o una mappa immagine. Nella scheda **[!UICONTROL Actions]** (Azioni), apportate le modifiche necessarie.
   * Per eliminare una diapositiva, selezionatela, quindi toccate **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.
   * Per applicare un predefinito, nell’angolo superiore destro della pagina toccate l’elenco a discesa **[!UICONTROL Preset]**, quindi selezionate un predefinito per visualizzatori.
   * Per eliminare un intero set carosello, passate al set carosello, selezionatelo, quindi toccate **[!UICONTROL Elimina]**.

   >[!NOTE]
   Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

## (Facoltativo) Anteprima dei banner carosello {#optional-previewing-carousel-banners}

Potete utilizzare Anteprima per vedere l’aspetto del banner carosello per i clienti e per testare i punti di attivazione e le mappe immagine dei banner carosello per assicurarvi che si comportino come previsto.

Una volta ottenuto il risultato desiderato, potete pubblicarlo.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consultate [Collegamento di URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.
Vedere [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Potete visualizzare in anteprima i banner carosello dall&#39;Editor carosello (metodo preferito) o dall&#39;elenco **[!UICONTROL Visualizzatori]**.

**Per visualizzare in anteprima i banner del carosello**

1. In **[!UICONTROL Risorse]**, andate a un banner carosello esistente creato e toccate per aprirlo.
1. Toccate **[!UICONTROL Modifica]**.
1. Nell’elenco dei predefiniti per visualizzatori nell’angolo destro della barra degli strumenti, selezionate un visualizzatore per l’anteprima del banner carosello.

   ![experience_fragment-carouselbanner-viewermenu a discesa](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Toccate **[!UICONTROL Anteprima]**.
1. Per verificare le azioni associate, toccate i punti di attivazione o le mappe immagine sull’immagine.

**Per visualizzare in anteprima i banner del carosello dall&#39;elenco Visualizzatori**

1. In **[!UICONTROL Risorse]**, andate a un banner carosello esistente creato e toccate per aprirlo.
1. Nell’angolo in alto a sinistra della pagina Anteprima, fate clic sull’icona Contenuto.
1. Nell’elenco **[!UICONTROL Visualizzatori]** nel pannello a sinistra della pagina, toccate il nome del predefinito per visualizzatori di banner carosello che desiderate usare.
1. Per verificare le azioni associate, toccate i punti di attivazione o le mappe immagine sull’immagine.

## Pubblicazione dei banner carosello {#publishing-carousel-banners}

Pubblicate il carosello per utilizzarlo. Quando si pubblica un set carosello, vengono attivati l’URL e il codice da incorporare. Il carosello viene anche pubblicato su Dynamic Media cloud, integrato con un CDN per la distribuzione scalabile e performante.

>[!NOTE]
Se utilizzate un&#39;immagine interattiva esistente con punti di attivazione per il banner del carosello, dopo aver pubblicato il banner del carosello dovete pubblicare separatamente l&#39;immagine interattiva.
Inoltre, se modificate un&#39;immagine interattiva già pubblicata che state utilizzando in un banner carosello, è necessario pubblicare l&#39;immagine interattiva prima che tali modifiche si riflettano nel banner del carosello.

Consultate [Pubblicazione di Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni su come pubblicare i banner del carosello.

## Aggiunta di un banner carosello alla pagina del sito Web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini dei banner per creare un carosello, sono stati aggiunti punti di attivazione o mappe immagine, oppure entrambe, nel banner. Pubblicato il set carosello. È ora possibile aggiungerlo alla pagina del sito Web esistente.

>[!NOTE]
Se siete un cliente AEM Sites , potete aggiungere il banner del carosello direttamente alla pagina trascinando il componente Supporto interattivo sulla pagina. Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Tuttavia, se siete clienti indipendenti di Risorse per  Experience Manager, potete aggiungere manualmente il banner carosello alla pagina di destinazione del sito Web, come descritto in questo argomento.

1. Copiate il codice da incorporare del set carosello pubblicato.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungete alla pagina Web il codice da incorporare copiato da  risorse Experience Manager.
Il codice da incorporare copiato è reattivo e si adatta automaticamente all&#39;area di incorporamento della pagina.

## Integrazione del banner carosello con una vista Rapida esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: questo passaggio si applica solo se sei un cliente  AEM Assets indipendente.

L’ultimo passaggio di questo processo consiste nell’integrare il banner del carosello con un’implementazione esistente della visualizzazione rapida sul sito Web. Ogni implementazione della visualizzazione rapida è univoca ed è necessario un approccio specifico, che in genere richiede l&#39;assistenza di una persona IT front-end.

L’implementazione della visualizzazione rapida esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL di visualizzazione rapida basato sull’elemento dell’interfaccia utente attivato al punto 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al punto 2.
1. La logica back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati della vista rapida caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Contemporaneamente alla sostituzione del passaggio 1 e in parte del passaggio 2 da parte del banner carosello, quando un utente fa clic su un punto di attivazione o una mappa immagine all’interno del banner carosello, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati di aree sensibili o mappe immagine precedentemente aggiunti.

In un tale gestore di eventi, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dal banner del carosello.
* Crea un URL di visualizzazione rapida basato sui dati del punto di attivazione o della mappa immagine.
* Attiva il processo di caricamento della vista Rapida dall&#39;estremità posteriore e di rendering sullo schermo per la visualizzazione.

Il codice da incorporare restituito da  AEM Assets dispone già di un gestore eventi ready-to-use impostato come commento.

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo fittizio del gestore con il codice specifico per la pagina Web specifica.

Il processo di creazione dell’URL di visualizzazione rapida è opposto a quello utilizzato per identificare le variabili dei punti di attivazione e delle mappe immagine precedentemente descritte.

Vedere [Identificazione delle variabili dei punti di attivazione e delle mappe immagine](#identifying-hotspot-and-image-map-variables).

L’ultimo passaggio per attivare l’URL della visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un esperto IT front-end del reparto IT. Essi hanno la certezza di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio appropriato, avendo un URL di visualizzazione rapida pronto all’uso.

## Uso delle viste rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

Vedere [Uso delle viste rapide per creare finestre a comparsa personalizzate](/help/assets/dynamic-media/custom-pop-ups.md).