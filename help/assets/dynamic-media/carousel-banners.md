---
title: Banner a carosello
description: Scopri come utilizzare i banner carosello in Dynamic Media.
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '4535'
ht-degree: 1%

---

# Banner a carosello{#carousel-banners}

I banner a carosello consentono agli addetti al marketing di guidare la conversione creando facilmente contenuti promozionali interattivi rotanti e consegnandoli a qualsiasi schermo.

La creazione e la modifica dei contenuti contenuti contenuti nei banner promozionali può richiedere molto tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o renderli più mirati. I banner a carosello consentono di creare o modificare rapidamente i banner rotanti e di aggiungere interattività come il collegamento di punti attivi ai dettagli del prodotto o alle risorse correlate. È possibile distribuirli su qualsiasi schermo, consentendo di immettere nuovi contenuti promozionali sul mercato più rapidamente.

I banner a carosello sono contrassegnati da un banner con la parola **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Sul sito web, un banner a carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui puoi navigare tra le immagini selezionando i numeri. Inoltre, le diapositive ruotano automaticamente in base a un intervallo di tempo personalizzabile. Le immagini in un banner carosello supportano sia punti attivi che mappe immagine. Gli utenti possono selezionare o passare a un collegamento ipertestuale o accedere a una finestra Quickview.

In questo esempio, un utente ha selezionato una mappa immagine e ha effettuato l&#39;accesso alla finestra Quickview per i guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Guarda come vengono creati i banner a carosello {#watch-how-carousel-banners-are-created}

Guarda una procedura dettagliata su [creazione dei banner a carosello](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (Durata: 10 minuti e 33 secondi). Scopri anche come visualizzare in anteprima, modificare e distribuire banner a carosello.

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **d[!UICONTROL utenti]** gruppo.

## Avvio rapido: Banner a carosello {#quick-start-carousel-banners}

Per farti iniziare a lavorare velocemente:

1. [Identificare le variabili dei punti attivi e delle mappe immagine](#identifying-hotspot-and-image-map-variables) (solo per i clienti che utilizzano Adobe Experience Manager Assets + Dynamic Media)

   Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione della visualizzazione rapida esistente. In questo modo puoi inserire correttamente gli hotspot e i dati della mappa immagine durante il processo di creazione del banner carosello in Experience Manager Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/dynamic-media/managing-viewer-presets.md).

   Gli amministratori possono personalizzare il comportamento e l’aspetto del carosello creando un proprio predefinito per visualizzatori Carosello. Il vantaggio principale è che è possibile riutilizzare questo predefinito visualizzatore personalizzato per più caroselli. Tuttavia, se lo desideri, gli utenti possono personalizzare direttamente il comportamento e l’aspetto del carosello durante la creazione del carosello. Questo approccio è da preferire quando si desidera una progettazione specifica per un determinato carosello.

1. [Caricare un banner immagine](#uploading-image-banners).

   Carica i banner immagine che desideri rendere interattivi.

1. [Creare un set carosello](#creating-carousel-sets).

   In Set caroselli, gli utenti navigano tra le immagini dei banner e selezionano punti attivi o mappe immagine per accedere ai contenuti pertinenti.

   Per creare un set carosello in Assets, seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello]**. Aggiungi risorse alle diapositive e seleziona **[!UICONTROL Salva]**. Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).

   Aggiungi uno o più punti attivi o mappe immagine a un banner immagine. Quindi, associa ciascuno di essi a un’azione come un collegamento, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto punti attivi o mappe immagine, finisci questa attività pubblicando il set carosello. La pubblicazione crea il codice di incorporamento che puoi utilizzare per copiare e applicare alla pagina di destinazione del tuo sito web.

   Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del set carosello e verificarne l’interattività.

1. [Pubblicare banner a carosello](#publishing-carousel-banners).

   Puoi pubblicare un set carosello come faresti con una risorsa. In Assets, individua il set carosello, selezionalo e selezionalo **[!UICONTROL Pubblica]**. La pubblicazione di un set carosello attiva l’URL e la stringa di incorporamento.

1. Effettua una delle operazioni seguenti:

   * [Aggiungere un banner carosello alla pagina del sito web](#adding-a-carousel-banner-to-your-website-page)Puoi aggiungere l’URL del banner carosello o il codice di incorporamento copiato nella pagina del sito web.

      * [Integrare il banner carosello con una visualizzazione rapida esistente](#integrating-the-carousel-banner-with-an-existing-quickview). Se utilizzi un sistema di gestione dei contenuti web di terze parti, devi integrare il nuovo banner carosello con l’implementazione della visualizzazione rapida esistente sul sito web.
   * [Aggiungi un banner carosello al sito web in Experience Manager](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). Se sei un cliente di Experience Manager Sites, puoi aggiungere il set carosello direttamente alla pagina utilizzando il componente File multimediali interattivi .


Se è necessario modificare i set carosello, consulta [Modifica set carosello](#editing-carousel-sets). Inoltre, puoi visualizzare e modificare [Proprietà del set carosello](/help/assets/manage-digital-assets.md#editing-properties).

## Identificare le variabili di punti attivi e mappe immagine {#identifying-hotspot-and-image-map-variables}

Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione della visualizzazione rapida esistente. Questo metodo consente di inserire correttamente i dati di hotspot o mappe immagine durante il processo di creazione del set carosello in Experience Manager Assets.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine del banner, assegni un SKU (Stock Keeping Unit). Puoi anche assegnare variabili aggiuntive facoltative a ogni punto attivo o mappa immagine. Tali variabili vengono utilizzate in seguito per far coincidere punti attivi o mappe immagine con il contenuto della visualizzazione rapida.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

È importante identificare in modo appropriato il numero e il tipo di variabili da associare ai dati del punto attivo o della mappa immagine. Ogni punto attivo o mappa immagine aggiunta a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo non ambiguo il prodotto nel sistema back-end esistente. Allo stesso tempo, assicurati che ogni punto attivo o mappa immagine non includa più dati del necessario. Questo perché renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione continua dei punti attivi o delle mappe immagine più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti attivi o delle mappe immagine.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview esistente. È probabile che sappiano qual è il set minimo di dati per identificare la visualizzazione rapida nel sistema. Tuttavia, è possibile semplicemente analizzare il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, selezionando un **[!UICONTROL Quickview]** pulsante .
* Il sito web invia una richiesta Ajax al back-end per caricare i dati o il contenuto di Quickview, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end esegue il rendering visivo di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Quindi attiva la visualizzazione rapida e acquisisci l’URL Ajax inviato dalla pagina web per il caricamento dei dati o del contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser web moderni dispongono di ispettori web che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser web che includono ispettori web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 (Windows®) o Comando-Opzione-I (Mac) per aprire il pannello degli strumenti per sviluppatori. Selezionare la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows®) o Comando-Opzione-I (Mac). Utilizzare la relativa scheda Rete oppure utilizzare lo strumento integrato Inspector e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida nella pagina.

Ora trova l&#39;URL Ajax della visualizzazione rapida nel registro di rete e copia l&#39;URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione rapida sono presenti numerose richieste inviate al server. In genere, l’URL Ajax Quickview è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di stringa di query complessa e il relativo tipo MIME di risposta è `text/html`, `text/xml`oppure `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie di prodotti e tipi. Il motivo è che gli URL di visualizzazione rapida hanno parti comuni per una determinata categoria di siti web, ma cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l’unico elemento dati necessario per aggiungere punti attivi o mappe immagine all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta diversi elementi oltre all’SKU. Alcuni di questi elementi includono ID categoria, codice colore, codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto attivo o della mappa immagine nella funzione del banner carosello.

Prendi in considerazione i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti attivi o mappe immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>SKU singolo, trovato nella stringa query.</td>
   <td><p>Gli URL registrati della visualizzazione rapida includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile nell’URL è il valore della variabile <code>productId=</code> parametro della stringa query, ed è chiaramente un valore SKU. Pertanto, gli hotspot o le mappe immagine richiedono solo campi SKU popolati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU singolo, trovato nel percorso URL.</td>
   <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU delle hotspot/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa query.</td>
   <td><p>Gli URL registrati della visualizzazione rapida includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. La SKU viene memorizzata nel <code>prodId</code> e l'ID della categoria viene memorizzato nella variabile <code>category=</code>parametro .</p> <p>Di conseguenza, le definizioni dei punti attivi e delle mappe immagine sono coppie. Cioè, un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>SKU <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>SKU <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carica banner immagine {#uploading-image-banners}

Se hai già caricato le immagini da utilizzare, passa al passaggio successivo, [Crea set carosello](#creating-carousel-sets). Le immagini utilizzate nel carosello devono essere caricate dopo l’abilitazione di Dynamic Media.

Per caricare i banner immagine, vedi [Caricare le risorse](/help/assets/manage-digital-assets.md).

## Crea set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **[!UICONTROL utenti dam]** gruppo.

**Per creare dei set carosello:**

1. In Assets, individua la cartella in cui vuoi creare il set carosello e vai a **[!UICONTROL Crea > Set carosello]**.
1. Nella pagina Editor banner carosello, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]** per selezionare l&#39;immagine per la prima diapositiva.

   Nella pagina Editor banner carosello, effettuare una delle seguenti operazioni:

   * Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Aggiungi diapositiva]** icona.

   * Vicino al centro della pagina, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]**.
   Seleziona per selezionare le risorse da includere nel set carosello. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine della procedura, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e selezionando **[!UICONTROL Ritorno]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e quindi seleziona la **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** oppure **[!UICONTROL Vista a elenco]**.

   Vedi [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md) per ulteriori informazioni.

1. Continua ad aggiungere diapositive finché non avrai aggiunto tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Se necessario, trascinate le diapositive per riordinare le immagini nell’elenco del set.
   * Per eliminare un’immagine, selezionala e seleziona **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.

   * Per applicare un predefinito, vicino all’angolo superiore destro della pagina, seleziona l’elenco a discesa dei predefiniti , quindi seleziona un predefinito da applicare al set contemporaneamente.
   Per eliminare una diapositiva, selezionarla. Sulla barra degli strumenti, seleziona **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti. Per spostare una diapositiva, selezionate l&#39;icona di riordino e spostatevi nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, puoi aggiungere un punto attivo, una mappa immagine o entrambi all’immagine. Vedi [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
1. È possibile modificare la progettazione visiva e il comportamento dei set carosello. Seleziona la **[!UICONTROL Comportamento]** e **[!UICONTROL Aspetto]** schede per modificare l’aspetto del banner carosello o il comportamento di componenti specifici. Vedi [Gestire i predefiniti per visualizzatori](/help/assets/dynamic-media/viewer-presets.md) per ulteriori informazioni su come utilizzare l’editor per visualizzatori.

   >[!NOTE]
   >
   >Per i banner a carosello, è possibile regolare quanto segue:
   >
   >* Durata visualizzata da un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >* Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. È possibile passare a una transizione diapositiva.
   >* Stile dei pulsanti. Gli utenti possono ruotare attraverso i banner selezionando ogni punto o numero. È possibile modificare la posizione in cui vengono visualizzati i pulsanti degli indicatori impostati (e se si tratta di uno stile numerico o punteggiato) e la loro dimensione.
   >* Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per gli hotspot.
   >* Prima di modificare un predefinito visualizzatore, scegli lo stile su cui desideri basare il predefinito. Se non scegli uno stile, quando inizi a modificare il predefinito visualizzatore, perderai tutte le modifiche se modifichi un predefinito diverso.


   È inoltre possibile visualizzare in anteprima l’aspetto del banner carosello. Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]** una volta finito.

## Aggiungere punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Puoi aggiungere punti attivi o mappe immagine a un banner utilizzando l’editor per set carosello.

Quando aggiungi punti attivi o mappe immagine, puoi definirli come una visualizzazione a comparsa Visualizzazione rapida, come collegamento ipertestuale o come frammento esperienza.

Vedi [Frammento esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorpori il visualizzatore in un Frammento esperienza.
>
>Per risolvere questo problema, puoi utilizzare o creare predefiniti visualizzatore privi di strumenti di condivisione social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine, ricorda di salvare il tuo lavoro. Le opzioni Annulla e Ripristina, situate nell’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, puoi facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner carosello per i clienti.

Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Quando aggiungi punti attivi a un banner immagine, le informazioni relative al punto attivo vengono memorizzate nella stessa posizione di metadati, in relazione alla posizione dell&#39;immagine. Questo punto è vero indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai relativi dati definiti per i punti attivi, in entrambi i visualizzatori.
Tenere tuttavia presente che i caroselli banner supportano mappe immagine su immagini che possono contenere anche punti attivi; un&#39;immagine interattiva non lo è. Tieni presente questo suggerimento se intendi creare un’immagine interattiva o un banner carosello che utilizza la stessa immagine. Considera la creazione di immagini interattive e di banner carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Per aggiungere punti attivi o mappe immagine a un banner immagine:**

1. Da Risorse, accedi al set carosello che desideri rendere interattivo.
1. Seleziona il set carosello e fai clic su **[!UICONTROL Modifica]**. Viene aperto l’Editor visualizzatore carosello.
1. Selezionare la diapositiva da rendere interattiva.
1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine]**.
1. Effettua una delle seguenti operazioni:

   * Per gli hotspot: Nell’immagine, seleziona la posizione in cui vuoi visualizzare il punto attivo.
   * Per le mappe immagine: Nell’immagine, trascina dall’alto a sinistra verso l’alto a destra per creare l’area della mappa immagine. È possibile regolare le dimensioni della mappa immagine trascinando gli angoli.

   Se necessario, trascina il punto attivo o la mappa immagine in una nuova posizione. In alternativa, utilizza i tasti freccia della tastiera per controllare la posizione di un punto attivo selezionato. Se necessario, aggiungi altri punti attivi o mappe immagine.

   Per eliminare un punto attivo o una mappa immagine, seleziona la **[!UICONTROL Azioni]** scheda . Sotto la **[!UICONTROL Mappe e punti attivi]** a partire dal **[!UICONTROL Tipo selezionato]** dall’elenco a discesa, seleziona il nome del punto attivo o della mappa immagine da rimuovere. Seleziona la **[!UICONTROL Cestino]** accanto al menu , quindi seleziona **[!UICONTROL Elimina]**.

1. Nel campo di testo Nome , digita il nome del punto attivo o della mappa immagine. Questo nome viene visualizzato anche nel **[!UICONTROL Mappe e punti attivi]** elenco a discesa. Se specifichi un nome, identifica facilmente il punto attivo o la mappa immagine se decidi di modificarlo in futuro.
1. Effettua una delle seguenti operazioni nel **[!UICONTROL Azioni]** scheda:

   * Seleziona **[!UICONTROL Quickview]**.

      * Se siete un Experience Manager Sites <!-- and Ecommerce--> cliente, seleziona l’icona Selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto . Per tornare all’Editor banner carosello, seleziona il prodotto da utilizzare, quindi seleziona il segno di spunta nell’angolo in alto a destra della pagina.
      * Se non sei un Experience Manager Sites <!-- or Ecommerce --> cliente:

         * Definisci le variabili. Vedi [Identificare le variabili dei punti di attivazione](#identifying-hotspot-and-image-map-variables).
         * Quindi, inserisci manualmente il valore SKU. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU inserito popola automaticamente la parte variabile del modello di visualizzazione rapida. Il sistema ora è in grado di associare il punto attivo selezionato a una particolare visualizzazione rapida SKU.
         * (Facoltativo) Se nella Vista rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, selezionare **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Vedi [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md) per ulteriori informazioni.
   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente Experience Manager Sites, seleziona l’icona Selettore sito (cartella) per passare a un URL.

         >[!NOTE]
         Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.

      * Se si è un cliente autonomo, nel campo di testo href specificare il percorso completo dell&#39;URL di una pagina web collegata.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Vedi [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md) per ulteriori informazioni.

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza . Per tornare alla pagina Gestione punti attivi, seleziona il frammento esperienza da utilizzare, quindi seleziona nell’angolo in alto a destra della pagina **[!UICONTROL Seleziona]**.
Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Specifica la larghezza e l’altezza del frammento esperienza così come viene visualizzato sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorpori il visualizzatore in un Frammento esperienza.
         Per aggirare questo problema, puoi utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   È inoltre possibile visualizzare in anteprima l’aspetto del banner carosello. Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]**.
1. Pubblica il set carosello. La pubblicazione crea il codice di incorporamento o l’URL che puoi utilizzare sulla pagina del tuo sito web. Se sei un cliente Experience Manager Sites, aggiungi il set carosello direttamente alla pagina web.

   Vedi [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Vedi [Aggiungere un set carosello alla pagina di destinazione del sito web](#adding-a-carousel-banner-to-your-website-page)

## Modifica set carosello {#editing-carousel-sets}

>[!NOTE]
Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **[!UICONTROL utenti dam]** gruppo.

È possibile eseguire varie attività di modifica sui set carosello, ad esempio:

* Aggiungi le diapositive a un set carosello. Vedi anche [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Elimina le risorse nel set carosello.
* Applica un predefinito visualizzatore.
* Elimina il set carosello.
* Aggiungi o modifica punti attivi e mappe immagine. Vedi anche [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

**Per modificare i set carosello:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa Set carosello, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona sulla barra degli strumenti **[!UICONTROL Modifica]**.

   * Seleziona una risorsa Set carosello, quindi nell’angolo in alto a sinistra della pagina seleziona **[!UICONTROL Modifica]** (icona a forma di matita).

1. Per modificare il set carosello, effettuate una delle seguenti operazioni:

   * Per aggiungere una diapositiva, seleziona la **[!UICONTROL Aggiungi diapositiva]** icona. Passa alla risorsa da aggiungere alla diapositiva, quindi seleziona il segno di spunta.
   * Per riordinare le diapositive, trascinate una diapositiva in una nuova posizione (selezionate l&#39;icona di riordino per spostare gli elementi).
   * Per aggiungere un punto attivo o una mappa immagine, seleziona le icone del punto attivo o della mappa immagine e vedi [Aggiungere punti attivi e mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Per modificare l’aspetto o il comportamento del set carosello, seleziona la **[!UICONTROL Aspetto]** scheda o **[!UICONTROL Comportamento]** , quindi imposta le opzioni desiderate.
   * Per modificare punti attivi o mappe immagine, nella diapositiva appropriata seleziona un punto attivo o una mappa immagine. Sotto la **[!UICONTROL Azioni]** , apporta le modifiche desiderate.
   * Per eliminare una diapositiva, selezionala, quindi seleziona **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti.
   * Per applicare un predefinito, seleziona la **[!UICONTROL Predefinito]** dall’elenco a discesa, quindi seleziona un predefinito visualizzatore.
   * Per eliminare un intero set carosello, passare al set carosello, selezionarlo, quindi selezionare **[!UICONTROL Elimina]**.

   >[!NOTE]
   Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

## (Facoltativo) Anteprima banner carosello {#optional-previewing-carousel-banners}

È possibile utilizzare Anteprima per vedere come viene visualizzato il banner carosello ai clienti. L’opzione Anteprima consente inoltre di testare gli hotspot e le mappe immagine del banner carosello per garantirne il funzionamento come previsto.

Quando sei soddisfatto del banner carosello, puoi pubblicarlo.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).
Vedi [Collegare gli URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.
Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Puoi visualizzare in anteprima i banner carosello dall’Editor carosello (metodo preferito) o dal **[!UICONTROL Visualizzatori]** elenco.

**Per visualizzare in anteprima facoltativamente i banner carosello:**

1. In **[!UICONTROL Risorse]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona **[!UICONTROL Modifica]**.
1. Nell’elenco dei predefiniti visualizzatore nell’angolo a destra della barra degli strumenti, seleziona un visualizzatore per visualizzare l’anteprima del banner carosello.

   ![experience_fragment-carouselbanner-riquadro a discesa](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Seleziona **[!UICONTROL Anteprima]**.
1. Per testare le azioni associate, seleziona gli hotspot o le mappe immagine sull&#39;immagine.

**Per visualizzare in anteprima i banner a carosello dall’elenco Visualizzatori:**

1. In **[!UICONTROL Risorse]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Nell’angolo in alto a sinistra della pagina Anteprima, seleziona l’icona Contenuto .
1. In **[!UICONTROL Visualizzatori]** nel pannello a sinistra della pagina, seleziona il nome del predefinito visualizzatore del banner carosello da usare.
1. Per testare le azioni associate, seleziona gli hotspot o le mappe immagine sull&#39;immagine.

## Pubblicare banner a carosello {#publishing-carousel-banners}

Per utilizzare il carosello, devi pubblicarlo. La pubblicazione di un set carosello attiva l’URL e il codice di incorporamento. Pubblica anche il carosello su Dynamic Media cloud, integrato con una rete CDN per una distribuzione scalabile e performante.

>[!NOTE]
Se utilizzi un’immagine interattiva esistente con punti attivi per il banner carosello, devi pubblicare separatamente l’immagine interattiva dopo aver pubblicato il banner carosello.
Inoltre, se modifichi un’immagine interattiva pubblicata precedentemente e utilizzata in un banner carosello, pubblica l’immagine interattiva in modo che tali modifiche si riflettano nel banner carosello.

Vedi [Pubblicare risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni su come pubblicare banner carosello.

## Aggiungere un banner carosello alla pagina del sito web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini del banner per creare un carosello, aggiunto punti attivi o mappe immagine, o entrambe, sul banner. È stato pubblicato il set carosello. Ora puoi aggiungerlo alla pagina del sito web esistente.

>[!NOTE]
Se sei un cliente di Experience Manager Sites, puoi aggiungere il banner carosello direttamente alla pagina trascinando il componente File multimediali interattivi nella pagina. Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Tuttavia, se sei un cliente Experience Manager Assets autonomo puoi aggiungere manualmente il banner carosello alla pagina di destinazione del tuo sito web.

1. Copia il codice di incorporamento del set carosello pubblicato.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungi il codice di incorporamento copiato da Experience Manager Assets alla pagina web.
Il codice di incorporamento copiato è reattivo e si adatta automaticamente all’area di incorporamento della pagina.

## Integrare il banner carosello con una Quickview esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: questo passaggio si applica solo se sei un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo consiste nell’integrare il banner carosello con un’implementazione Quickview esistente sul sito web. Ogni implementazione della visualizzazione rapida è unica ed è necessario un approccio specifico che in genere richiede l&#39;assistenza di un IT front-end.

L&#39;implementazione di Quickview esistente rappresenta normalmente una catena di azioni correlate che avvengono sulla pagina web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL di visualizzazione rapida basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al passaggio 2.
1. La logica back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati di visualizzazione rapida caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo, quando l’utente seleziona un punto attivo o una mappa immagine, il banner carosello sostituisce il passaggio 1 e in parte il passaggio 2, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo o della mappa immagine precedentemente aggiunti.

In un tale gestore di eventi, il codice front-end effettua le seguenti operazioni:

* Ascolta un evento emesso dal banner carosello.
* Crea un URL di visualizzazione rapida basato sui dati del punto attivo o della mappa immagine.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets dispone già di un gestore eventi ready-to-use in posizione, che viene aggiunto un commento.

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la pagina web specifica.

Il processo di costruzione dell&#39;URL di visualizzazione rapida è opposto al processo utilizzato per identificare le variabili dei punti attivi e delle mappe immagine trattate in precedenza.

Vedi [Identificare le variabili dei punti attivi e delle mappe immagine](#identifying-hotspot-and-image-map-variables).

L&#39;ultimo passaggio per attivare l&#39;URL di visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede molto probabilmente l&#39;assistenza di un esperto IT front-end del reparto IT. Essi hanno la conoscenza di sapere come attivare con precisione l&#39;implementazione della visualizzazione rapida dal passaggio appropriato, avendo un URL di visualizzazione rapida pronto all&#39;uso.

## Crea Windows® a comparsa personalizzato utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedi [Crea Windows® a comparsa personalizzato utilizzando Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
