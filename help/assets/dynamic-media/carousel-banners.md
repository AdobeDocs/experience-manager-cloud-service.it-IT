---
title: Banner a carosello
description: Scopri come utilizzare i banner carosello in Dynamic Media.
contentOwner: Rick Brough
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '4492'
ht-degree: 1%

---

# Banner a carosello{#carousel-banners}

I banner carosello consentono agli addetti al marketing di promuovere la conversione dei contenuti creando facilmente contenuti promozionali a rotazione interattivi e distribuendoli a qualsiasi schermo.

La creazione e la modifica dei contenuti visualizzati nei banner promozionali può richiedere tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o renderli più mirati. I banner a carosello consentono di creare o modificare rapidamente i banner rotanti e di aggiungere interattività, ad esempio il collegamento di punti attivi ai dettagli del prodotto o a risorse correlate. e possono essere distribuiti su qualsiasi schermo per velocizzare le operazioni di marketing.

I banner a carosello sono indicati da un banner con la parola **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Sul sito web, un banner a carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui puoi navigare tra le immagini selezionando i numeri. Inoltre, le diapositive ruotano automaticamente in base a un intervallo di tempo personalizzabile. Le immagini contenute in un banner carosello supportano sia gli hotspot che le mappe immagine. Gli utenti possono selezionare o passare a un collegamento ipertestuale o accedere a una finestra Quickview.

In questo esempio, un utente ha selezionato una mappa immagine e ha effettuato l&#39;accesso alla finestra Quickview per i guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Guarda come vengono creati i banner a carosello {#watch-how-carousel-banners-are-created}

Guarda una procedura dettagliata sulla [creazione dei banner a carosello](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner) (durata: 10 minuti e 33 secondi). Scopri anche come visualizzare in anteprima, modificare e distribuire i banner carosello.

>[!NOTE]
>
>Per poter creare o modificare i banner a carosello, è necessario aggiungere gli utenti non amministratori al gruppo **[!UICONTROL dam-users]**. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema che potrà aggiungerti al gruppo **d[!UICONTROL am-users]**.

## Guida introduttiva: Banner a carosello {#quick-start-carousel-banners}

Per iniziare subito a utilizzare il prodotto:

1. [Identificare le variabili del punto attivo e della mappa immagine](#identifying-hotspot-and-image-map-variables) (solo per i clienti che utilizzano Adobe Experience Manager Assets + Dynamic Media)

   Per prima cosa, identifica le variabili dinamiche utilizzate dall’implementazione della visualizzazione rapida esistente. In questo modo puoi inserire correttamente gli hotspot e i dati della mappa immagine durante il processo di creazione del banner a carosello in Experience Manager Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/dynamic-media/managing-viewer-presets.md).

   Se sei un amministratore, puoi personalizzare il comportamento e l’aspetto del carosello creando un predefinito visualizzatore Carosello personalizzato. Il vantaggio principale è che puoi riutilizzare questo predefinito visualizzatore personalizzato per più caroselli di immagini. Tuttavia, gli utenti possono personalizzare facoltativamente il comportamento e l’aspetto del carosello direttamente durante la creazione dello stesso. Questo approccio è da preferirsi quando si desidera un design specifico per un determinato carosello.

1. [Carica un banner immagine](#uploading-image-banners).

   Carica i banner immagine da rendere interattivi.

1. [Crea un set carosello](#creating-carousel-sets).

   In Set caroselli di immagini, gli utenti possono navigare tra le immagini dei banner e selezionare punti attivi o mappe immagine per accedere al contenuto pertinente.

   Per creare un set carosello in Assets, seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello]**. Aggiungi le risorse alle diapositive e seleziona **[!UICONTROL Salva]**. Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungi punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).

   Aggiungi uno o più punti attivi o mappe immagine a un banner immagine. Quindi, associa ciascuna di esse a un’azione, ad esempio un collegamento, una visualizzazione rapida o un frammento di esperienza. Dopo aver aggiunto punti attivi o mappe immagine, completa questa attività pubblicando il set carosello. La pubblicazione crea il codice da incorporare che puoi utilizzare per copiare e applicare alla pagina di destinazione del sito web.

   Vedere [(Facoltativo) Anteprima Banner Carosello](#optional-previewing-carousel-banners) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del set carosello e testarne l’interattività.

1. [Pubblica banner carosello](#publishing-carousel-banners).

   Pubblichi un set carosello come faresti con una risorsa. In Assets, passa al set carosello e selezionalo, quindi seleziona **[!UICONTROL Pubblica]**. La pubblicazione di un set carosello attiva l’URL e la stringa di incorporamento.

1. Effettua una delle seguenti operazioni:

   * [Aggiungi un banner carosello alla pagina del tuo sito Web](#adding-a-carousel-banner-to-your-website-page)Puoi aggiungere l&#39;URL del banner o il codice da incorporare copiato nella pagina del sito Web.

      * [Integrare il banner del carosello con una visualizzazione rapida esistente](#integrating-the-carousel-banner-with-an-existing-quickview). Se utilizzi un sistema di gestione dei contenuti web di terze parti, devi integrare il nuovo banner a carosello con l’implementazione Quick view esistente sul tuo sito web.

   * [Aggiungi un banner carosello al tuo sito Web in Experience Manager](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). Se sei un cliente di Experience Manager Sites, puoi aggiungere il set carosello direttamente alla pagina utilizzando il componente File multimediali interattivi.

Se devi modificare i set carosello, vedi [Modifica set carosello](#editing-carousel-sets). Inoltre, puoi visualizzare e modificare [le proprietà del set carosello](/help/assets/manage-digital-assets.md#editing-properties).

## Identificare i punti attivi e le variabili della mappa immagine {#identifying-hotspot-and-image-map-variables}

Per prima cosa, identifica le variabili dinamiche utilizzate dall’implementazione della visualizzazione rapida esistente. Questo metodo consente di immettere correttamente i punti attivi o i dati della mappa immagine durante il processo di creazione del set carosello in Experience Manager Assets.

Quando aggiungete punti attivi o mappe immagine a un&#39;immagine del banner, assegnate uno SKU (Stock Keeping Unit). Puoi anche assegnare ulteriori variabili facoltative a ciascun punto attivo o mappa immagine. Tali variabili vengono utilizzate in un secondo momento per far corrispondere i punti attivi o le mappe immagine con il contenuto della Visualizzazione rapida.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati del punto attivo o della mappa immagine. Ogni punto attivo o mappa immagine aggiunta a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo inequivocabile il prodotto nel sistema back-end esistente. Allo stesso tempo, assicurati che ogni punto attivo o mappa immagine non includa più dati del necessario. Il motivo è che questo renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione dei punti attivi o delle mappe immagine in corso più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati del punto attivo o della mappa immagine.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione Quickview esistente. È probabile che sappiano qual è il set minimo di dati per identificare la Visualizzazione rapida nel sistema. Tuttavia, è possibile semplicemente analizzare il comportamento esistente del codice front-end.

La maggior parte delle implementazioni Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, selezionando un pulsante **[!UICONTROL Quickview]**.
* Il sito web invia una richiesta Ajax al back-end per caricare i dati o il contenuto Quickview, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end riproduce visivamente tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Quindi attiva Quickview e acquisisci l’URL Ajax inviato dalla pagina web per caricare i dati o il contenuto Quickview.

In genere non è necessario utilizzare strumenti di debug specifici. I browser web moderni dispongono di web inspector che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono i controlli Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premi F12 (Windows®) o Comando-Opzione-I (Mac) per aprire il pannello dello strumento Sviluppatore. Selezionare la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows®) o Command-Option-I (Mac). Utilizzare la relativa scheda Rete oppure lo strumento integrato Ispettore e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva Quickview sulla pagina.

Ora puoi trovare l’URL Ajax della visualizzazione rapida nel registro di rete e copiare l’URL registrato per l’analisi futura. Di solito, quando si attiva Quickview, vengono inviate numerose richieste al server. In genere, l’URL Ajax di Quickview è uno dei primi dell’elenco. Ha una porzione o un percorso di stringa di query complesso e il relativo tipo MIME di risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida hanno parti comuni per una determinata categoria di siti web, ma cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL di Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l&#39;unico dato necessario per aggiungere punti attivi o mappe immagine all&#39;immagine del banner.

Tuttavia, in casi complessi, oltre allo SKU l&#39;URL Quickview presenta diversi elementi variabili. Alcuni di questi elementi includono l’ID categoria, il codice colore, il codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione del punto attivo o della mappa immagine nella funzione del banner del carosello.

Prendi in considerazione i seguenti esempi di URL Quickview e le variabili hotspot o mappa immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>Singolo SKU, trovato nella stringa di query.</td>
   <td><p>Gli URL di visualizzazione rapida registrati includono:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&source=100</code></p> </li>
    </ul> <p>L'unica parte variabile nell'URL è il valore del parametro della stringa di query <code>productId=</code> ed è chiaramente un valore SKU. Pertanto, i punti attivi o le mappe immagine richiedono solo campi SKU compilati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>Singolo SKU, trovato nel percorso URL.</td>
   <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell'ultima parte del percorso e diventa il valore SKU dei punti attivi/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa query.</td>
   <td><p>Gli URL di visualizzazione rapida registrati includono:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è archiviato nel parametro <code>prodId</code> e l'ID categoria nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni del punto attivo/mappa immagine sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>Lo SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>Lo SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>Lo SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carica banner immagine {#uploading-image-banners}

Se hai già caricato le immagini che desideri utilizzare, passa al passaggio successivo, [Crea set carosello](#creating-carousel-sets). Le immagini utilizzate nel carosello devono essere caricate dopo l’abilitazione di Dynamic Media.

Per caricare i banner immagine, consulta [Caricare le risorse](/help/assets/manage-digital-assets.md).

## Creare set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Per poter creare o modificare i banner a carosello, è necessario aggiungere gli utenti non amministratori al gruppo **[!UICONTROL dam-users]**. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema che potrà aggiungerti al gruppo **[!UICONTROL dam-users]**.

**Per creare set carosello:**

1. In Assets, passa alla cartella in cui desideri creare il set carosello e vai a **[!UICONTROL Crea > Set carosello]**.
1. Nella pagina Editor banner carosello, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]** e selezionare l&#39;immagine per la prima diapositiva.

   Nella pagina Editor banner carosello eseguire una delle operazioni seguenti:

   * Nell&#39;angolo superiore sinistro della pagina, selezionare l&#39;icona **[!UICONTROL Aggiungi diapositiva]**.

   * Nella parte centrale della pagina, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]**.

   Seleziona per selezionare le risorse da includere nel set carosello. Le risorse selezionate presentano un’icona a forma di segno di spunta. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e selezionando **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Selezionare il filtro e quindi l&#39;icona **[!UICONTROL Filtro]** nella barra degli strumenti. Modificare la visualizzazione selezionando l&#39;icona Visualizza e selezionando **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

1. Continuate ad aggiungere diapositive fino ad aggiungere tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Se necessario, trascinare la diapositiva per riordinare le immagini nell&#39;elenco.
   * Per eliminare un&#39;immagine, selezionarla, quindi selezionare **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.

   * Per applicare un predefinito, seleziona l’elenco a discesa dei predefiniti nell’angolo superiore destro della pagina, quindi seleziona un predefinito da applicare al set contemporaneamente.

   Per eliminare una diapositiva, selezionarla. Sulla barra degli strumenti, selezionare **[!UICONTROL Elimina diapositiva]**. Per spostare una diapositiva, selezionate l&#39;icona Riordina (Reorder) e spostatela nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, è possibile aggiungere un punto attivo, una mappa immagine o entrambi all&#39;immagine. Consulta [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Puoi modificare la progettazione visiva e il comportamento dei set carosello. Seleziona le schede **[!UICONTROL Comportamento]** e **[!UICONTROL Aspetto]** per modificare l&#39;aspetto del banner del carosello o il comportamento di componenti specifici. Per ulteriori informazioni sull&#39;utilizzo dell&#39;editor visualizzatore, vedere [Gestione predefiniti visualizzatore](/help/assets/dynamic-media/viewer-presets.md).

   >[!NOTE]
   >
   >Per i banner a carosello, puoi regolare quanto segue:
   >
   >* Durata di visualizzazione di un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >* Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. Potete cambiare questa transizione in una diapositiva.
   >* Stile dei pulsanti. Gli utenti possono ruotare tra i banner selezionando ogni punto o numero. È possibile modificare la posizione e le dimensioni dei pulsanti degli indicatori impostati (e se sono numerici o con uno stile punteggiato).
   >* Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per gli hotspot.
   >* Prima di modificare un predefinito visualizzatore, scegliete lo stile su cui basare il predefinito. Se non scegliete uno stile, quando iniziate a modificare il predefinito visualizzatore, tutte le modifiche andranno perse se passate a un predefinito diverso.

   Puoi anche visualizzare in anteprima l’aspetto del banner del carosello. Vedi [(Facoltativo) Anteprima Banner Carosello](#optional-previewing-carousel-banners).

1. Al termine, seleziona **[!UICONTROL Salva]**.

## Aggiunta di punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Puoi aggiungere punti attivi o mappe immagine a un banner utilizzando l’editor di set carosello.

Quando aggiungi punti attivi o mappe immagine, puoi definirli come una visualizzazione a comparsa della Visualizzazione rapida, come collegamento ipertestuale o frammento di esperienza.

Vedi [Frammento esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione dei social media nel banner Carosello non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza.
>
>Per risolvere questo problema, puoi utilizzare o creare predefiniti visualizzatore che non dispongono di strumenti per la condivisione sui social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine, ricorda di salvare i tuoi dati. Le opzioni Annulla e Ripristina, posizionate nell&#39;angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, puoi facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner ai clienti.

Vedi [(Facoltativo) Anteprima Banner Carosello](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Quando aggiungete punti attivi a un banner immagine, le informazioni sui punti attivi vengono memorizzate nella stessa posizione di metadati, relativa alla posizione dell&#39;immagine. Questo punto è valido indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti attivi definiti, in entrambi i visualizzatori.
>
>Tieni presente, tuttavia, che i banner a carosello supportano le mappe immagine sulle immagini che possono anche contenere punti attivi, diversamente da un’immagine interattiva. Tieni presente questo suggerimento se intendi creare un’immagine interattiva o un banner a carosello che utilizza la stessa immagine. In alternativa, puoi creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
>
>Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, questi vengono rimossi.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Per aggiungere punti attivi o mappe immagine a un banner immagine:**

1. Da Assets, individua il set carosello che desideri rendere interattivo.
1. Seleziona il set carosello e seleziona **[!UICONTROL Modifica]**. Viene aperto l’Editor visualizzatore carosello.
1. Selezionare la diapositiva da rendere interattiva.
1. Nell&#39;angolo superiore sinistro della pagina, selezionare **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine]**.
1. Effettuare una delle seguenti operazioni:

   * Per punti attivi: sull&#39;immagine, seleziona la posizione in cui desideri visualizzare il punto attivo.
   * Per le mappe immagine: Sull’immagine, trascina dall’alto a sinistra all’basso a destra per creare l’area della mappa immagine. È possibile regolare le dimensioni della mappa immagine trascinando gli angoli.

   Se necessario, trascina il punto attivo o la mappa immagine in una nuova posizione. In alternativa, utilizzare i tasti freccia della tastiera per controllare la posizione di un punto attivo selezionato. Aggiungi altri punti attivi o mappe immagine in base alle esigenze.

   Per eliminare un punto attivo o una mappa immagine, seleziona la scheda **[!UICONTROL Azioni]**. Nell&#39;intestazione **[!UICONTROL Mappe e punti attivi]**, dall&#39;elenco a discesa **[!UICONTROL Tipo selezionato]**, selezionare il nome del punto attivo o della mappa immagine da rimuovere. Seleziona l&#39;icona **[!UICONTROL Elimina]** accanto al menu, quindi seleziona **[!UICONTROL Elimina]**.

1. Nel campo di testo Nome digitare il nome del punto attivo o della mappa immagine. Questo nome viene visualizzato anche nell&#39;elenco a discesa **[!UICONTROL Mappe e punto attivo]**. Specificando un nome è facile identificare il punto attivo o la mappa immagine se si decide di modificarlo in futuro.
1. Effettua una delle seguenti operazioni nella scheda **[!UICONTROL Azioni]**:

   * Selezionare **[!UICONTROL Quickview]**.

      * Se sei un cliente di Experience Manager Sites <!-- and Ecommerce-->, seleziona l&#39;icona del selettore prodotti (lente di ingrandimento) per aprire la pagina Seleziona prodotto. Per tornare all’Editor banner carosello, seleziona il prodotto da utilizzare, quindi fai clic sul segno di spunta nell’angolo superiore destro della pagina.
      * Se non sei un cliente di Experience Manager Sites <!-- or Ecommerce -->:

         * Definisci le variabili. Vedi [Identificare le variabili hotspot](#identifying-hotspot-and-image-map-variables).
         * Quindi, immetti manualmente il valore SKU. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che rappresenta un identificatore univoco per ogni prodotto o servizio specifico offerto. Il valore SKU inserito popola automaticamente la parte variabile del modello di visualizzazione rapida. Il sistema ora è in grado di associare il punto attivo selezionato alla visualizzazione rapida di una particolare SKU.
         * (Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, selezionare **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Selettore siti (cartella) per passare a un URL.

        >[!NOTE]
        >
        >Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.

      * Se sei un cliente autonomo, specifica il percorso URL completo di una pagina web collegata nel campo di testo href.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Per tornare alla pagina Gestione punti attivi, seleziona il frammento di esperienza che desideri utilizzare, quindi nell&#39;angolo superiore destro della pagina seleziona **[!UICONTROL Seleziona]**.
Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md).

      * Specifica la larghezza e l&#39;altezza del frammento di esperienza così come viene visualizzato sul banner.

        >[!NOTE]
        >
        >Gli strumenti di condivisione dei social media nel banner Carosello non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza.
        >
        >Per ovviare a questo problema, puoi utilizzare o creare predefiniti visualizzatore che non dispongono di strumenti per la condivisione tramite social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Puoi anche visualizzare in anteprima l’aspetto del banner del carosello. Vedi [(Facoltativo) Anteprima Banner Carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]**.
1. Pubblica il set carosello. La pubblicazione crea il codice o l’URL da incorporare che puoi utilizzare nella pagina del sito web. Se sei un cliente di Experience Manager Sites, aggiungi il set carosello direttamente alla pagina web.

   Consulta [Pubblicare risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Consulta [Aggiungere un set carosello alla pagina di destinazione del tuo sito Web](#adding-a-carousel-banner-to-your-website-page)

## Modifica set carosello {#editing-carousel-sets}

>[!NOTE]
>
>Per poter creare o modificare i banner a carosello, è necessario aggiungere gli utenti non amministratori al gruppo **[!UICONTROL dam-users]**. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema che potrà aggiungerti al gruppo **[!UICONTROL dam-users]**.

Puoi eseguire varie attività di modifica sui set carosello, come le seguenti:

* Aggiungere diapositive a un set carosello. Vedi anche [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Elimina le risorse nel set carosello.
* Applica un predefinito visualizzatore.
* Elimina il set carosello.
* Aggiungi o modifica gli hotspot e le mappe immagine. Vedi anche [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

**Per modificare i set carosello:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa Set carosello, seleziona **[!UICONTROL Seleziona]** (icona del segno di spunta), quindi seleziona **[!UICONTROL Modifica]** nella barra degli strumenti.

   * Seleziona una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) nell&#39;angolo superiore sinistro della pagina.

1. Per modificare il set carosello, effettuate una delle seguenti operazioni:

   * Per aggiungere una diapositiva, selezionare l&#39;icona **[!UICONTROL Aggiungi diapositiva]**. Passa alla risorsa da aggiungere alla diapositiva, quindi seleziona il segno di spunta.
   * Per riordinare le diapositive, trascinare una diapositiva in una nuova posizione (selezionare l&#39;icona Riordina per spostare gli elementi).
   * Per aggiungere un punto attivo o una mappa immagine, seleziona le icone del punto attivo o della mappa immagine e vedi [Aggiungere punti attivi e mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Per modificare l&#39;aspetto o il comportamento del set carosello, selezionare la scheda **[!UICONTROL Aspetto]** o **[!UICONTROL Comportamento]**, quindi impostare le opzioni desiderate.
   * Per modificare punti attivi o mappe immagine, nella diapositiva appropriata, seleziona un punto attivo o una mappa immagine. Nella scheda **[!UICONTROL Azioni]**, apporta le modifiche.
   * Per eliminare una diapositiva, selezionarla, quindi selezionare **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.
   * Per applicare un predefinito, seleziona l&#39;elenco a discesa **[!UICONTROL Predefinito]** nell&#39;angolo superiore destro della pagina, quindi seleziona un predefinito visualizzatore.
   * Per eliminare un intero set carosello, passare al set carosello, selezionarlo, quindi selezionare **[!UICONTROL Elimina]**.

   >[!NOTE]
   >
   >Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, questi vengono rimossi.

## (Facoltativo) Anteprima banner carosello {#optional-previewing-carousel-banners}

Puoi utilizzare Anteprima per vedere come il banner del carosello viene visualizzato ai clienti. L’utilizzo di Anteprima consente inoltre di testare gli hotspot e le mappe immagine del banner carosello per verificare che si comportino come previsto.

Quando sei soddisfatto del banner del carosello, puoi pubblicarlo.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consulta [Collegare gli URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Consulta [Aggiungere Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Puoi visualizzare in anteprima i banner carosello dall&#39;Editor carosello (metodo preferito) o dall&#39;elenco **[!UICONTROL Visualizzatori]**.

**Per visualizzare facoltativamente l&#39;anteprima dei banner del carosello:**

1. In **[!UICONTROL Assets]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona **[!UICONTROL Modifica]**.
1. Nell’elenco dei predefiniti visualizzatore nell’angolo destro della barra degli strumenti, seleziona un visualizzatore per visualizzare in anteprima il banner del carosello.

   ![elenco a discesa experience_fragment-carouselbanner-viewer](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Selezionare **[!UICONTROL Anteprima]**.
1. Per verificare le azioni associate, seleziona gli hotspot o le mappe immagine sull’immagine.

**Per visualizzare in anteprima i banner a carosello dall&#39;elenco dei visualizzatori:**

1. In **[!UICONTROL Assets]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona l’icona Contenuto nell’angolo in alto a sinistra della pagina Anteprima.
1. Nell&#39;elenco **[!UICONTROL Visualizzatori]** nel pannello a sinistra della pagina, seleziona il nome del predefinito visualizzatore banner a carosello che desideri utilizzare.
1. Per verificare le azioni associate, seleziona gli hotspot o le mappe immagine sull’immagine.

## Pubblica banner a carosello {#publishing-carousel-banners}

Per utilizzare il carosello, è necessario pubblicarlo. La pubblicazione di un set carosello attiva l’URL e il codice di incorporamento. Pubblica inoltre il carosello sul cloud Dynamic Media, integrato con una rete CDN per una distribuzione scalabile e performante.

>[!NOTE]
>
>Se utilizzi un’immagine interattiva esistente con punti attivi per il banner carosello, devi pubblicarla separatamente dopo aver pubblicato il banner.
>
>Inoltre, se modifichi un’immagine interattiva pubblicata preesistente utilizzata in un banner carosello, pubblica l’immagine interattiva in modo che tali modifiche vengano riportate nel banner del carosello.

Consulta [Pubblicare Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni su come pubblicare i banner a carosello.

## Aggiungere un banner carosello alla pagina del sito Web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini del banner per creare un carosello, sono stati aggiunti punti attivi, mappe immagine o entrambi. Pubblicato il set carosello. Ora puoi aggiungerlo alla pagina del tuo sito web esistente.

>[!NOTE]
>
>Se sei un cliente di Experience Manager Sites, puoi aggiungere il banner del carosello direttamente alla pagina trascinando il componente File multimediali interattivi nella pagina. Consulta [Aggiungere Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Tuttavia, se sei un cliente Experience Manager Assets indipendente, puoi aggiungere manualmente il banner a carosello alla pagina di destinazione del sito web.

1. Copia il codice di incorporamento del set carosello pubblicato.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungi alla pagina web il codice da incorporare copiato da Experience Manager Assets.
Il codice di incorporamento copiato è reattivo e si adatta automaticamente all’area di incorporamento della pagina.

## Integrare il banner Carosello con una Quickview esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: questo passaggio si applica solo se si è un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo è l’integrazione del banner a carosello con un’implementazione Quickview esistente sul sito web. Ogni implementazione Quick view è unica ed è necessario un approccio specifico che solitamente richiede l’assistenza di un responsabile IT front-end.

L’implementazione Quickview esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina web nell’ordine seguente:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL di visualizzazione rapida basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto nel passaggio 2.
1. La logica back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondente al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati della visualizzazione rapida caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere chiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo è nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo in cui il banner del carosello sostituisce il passaggio 1 e parzialmente il passaggio 2, quando un utente seleziona un punto attivo o una mappa immagine, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo o della mappa immagine aggiunti in precedenza.

In un gestore eventi di questo tipo, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dal banner del carosello.
* Costruisce un URL di visualizzazione rapida in base ai dati del punto attivo o della mappa immagine.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets contiene già un gestore di eventi pronto all’uso ed è stato aggiunto un commento.

Pertanto, è necessario solo rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la particolare pagina web.

Il processo di costruzione dell’URL della visualizzazione rapida è opposto al processo utilizzato per identificare il punto attivo e le variabili della mappa immagine trattati in precedenza.

Consulta [Identificare le variabili del punto attivo e della mappa immagine](#identifying-hotspot-and-image-map-variables).

L’ultimo passaggio per attivare l’URL di visualizzazione rapida e il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un responsabile IT front-end del reparto IT. Possiedono le conoscenze necessarie per sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio corretto, avendo un URL di visualizzazione rapida pronto all’uso.

## Creare finestre popup personalizzate® utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedere [Creare finestre popup personalizzate® utilizzando Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
