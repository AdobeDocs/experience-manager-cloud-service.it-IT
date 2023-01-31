---
title: Immagini interattive
description: Scopri come utilizzare le immagini interattive in Dynamic Media.
contentOwner: Rick Brough
feature: Interactive Images
role: User
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '4176'
ht-degree: 2%

---

# Immagini interattive{#interactive-images}

È possibile rendere le immagini statiche ricche di esperienze coinvolgenti per i clienti trascinando e rilasciando punti attivi &quot;shoppable&quot; su un&#39;immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o servizio con una funzionalità diretta, punto vendita &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot;. I clienti possono toccare questi hotspot che si collegano direttamente al prodotto o al servizio, aggiungerli a un carrello o essere collegati a una pagina web. Esperienze dirette come queste aumentano il coinvolgimento dei clienti e le conversioni sul tuo sito web.

Di seguito è riportato un banner acquistabile con una finestra a comparsa Quickview. Un utente attiva la visualizzazione rapida toccando il cerchio o il &quot;punto attivo&quot; sul modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Vedi [immagini interattive in azione](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) nella pagina web qui sopra.

## Guarda come vengono creati i banner immagine interattivi {#watch-how-interactive-image-banners-are-created}

Guarda una procedura dettagliata su [creazione di banner immagine interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10 minuti e 33 secondi). Inoltre, viene illustrato come visualizzare in anteprima, modificare e distribuire banner immagine interattivi.

## Avvio rapido: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le immagini interattive in Adobe Experience Manager Assets.

Cerca la **Esempio** intestazione all&#39;interno di alcune delle attività di avvio rapido. Contiene una breve esercitazione basata su [esempio di pagina web per cui non sono ancora state aggiunte immagini interattive](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html).



L’esercitazione illustra i passaggi necessari per integrare le immagini interattive nel sito web.

Passaggi per le immagini interattive:

1. **(Facoltativo) Identifica le variabili dei punti attivi**. Se utilizzi Adobe Experience Manager Assets e Dynamic Media standalone, identifica le variabili dinamiche utilizzate nell’implementazione Quickview esistente. In questo modo è possibile inserire i dati dei punti attivi durante la creazione dell’immagine interattiva. Vedi [(Facoltativo) Identificazione delle variabili dei punti attivi](#optional-identifying-hotspot-variables).
Tuttavia, se utilizzi Experience Manager Sites, Experience Manager eCommerce o entrambi, questo passaggio non è necessario.

1. **(Facoltativo) Crea un predefinito visualizzatore di immagini interattive**. Personalizza l&#39;immagine grafica utilizzata per rappresentare gli hotspot. La creazione di un predefinito per visualizzatori di immagini interattive non è necessaria se si intende utilizzare il predefinito visualizzatore di immagini interattive preconfigurato denominato `Shoppable_Banner` invece.
Vedi [(Facoltativo) Creazione di un predefinito visualizzatore di immagini interattive](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Caricare un banner immagine**. Carica i banner immagine che desideri rendere interattivi.
Vedi [Caricamento di un banner immagine](#uploading-an-image-banner).

1. **Aggiungere punti attivi a un banner immagine**. Aggiungi uno o più punti attivi a un banner immagine. Associare ciascuno di essi a un&#39;azione come un collegamento ipertestuale, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto gli hotspot, finirai questa attività pubblicando l&#39;immagine interattiva.
Vedi [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).
Vedi [Anteprima delle immagini interattive](#optional-previewing-interactive-images) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del banner acquistabile e verificarne l’interattività.
Vedi [Pubblicazione delle risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare le risorse immagine interattive.

1. **Aggiungi un’immagine interattiva al tuo sito web o al tuo sito web in Experience Manager**. Se utilizzi Sites, eCommerce o entrambi, puoi aggiungere immagini interattive direttamente a una pagina web in un Experience Manager. Trascina il componente File multimediali interattivi sulla pagina. Vedi [Aggiunta di risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Se utilizzi Experience ManagerAssets e Dynamic Media standalone, copia il codice di incorporamento sul tuo sito web. Quindi, integralo con la visualizzazione rapida esistente. Vedi [Integrazione di un’immagine interattiva con il sito web](#integrating-an-interactive-image-with-your-website).
Se utilizzi un WCM di terze parti (Web Content Manager), integra il nuovo video interattivo con la Quickview esistente utilizzata sul sito web. Vedi [Integrazione di un’immagine interattiva con una Quickview esistente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Facoltativo) Identifica le variabili dei punti attivi {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività all’immagine, attiva le visualizzazioni rapide.
>* La tua implementazione di Experience Manager *not* utilizza un framework di integrazione eCommerce per estrarre i dati dei prodotti in Experience Manager da qualsiasi soluzione eCommerce. Tali soluzioni includono IBM® WebSphere® Commerce, Elastic Path, SAP Hybris o Intershop.
>
Se l’implementazione di Experience Manager utilizza eCommerce, puoi saltare questa attività e passare all’attività successiva.

Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione di Quickview esistente in modo da poter inserire i dati dei punti attivi per creare l&#39;immagine interattiva.

Quando aggiungi punti attivi a un&#39;immagine del banner in Experience Manager Assets, assegna un SKU (Stock Keeping Unit). Lo SKU è un identificatore univoco per ogni prodotto o servizio distinto offerto. Inoltre, aggiungi eventuali variabili facoltative aggiuntive a ogni punto attivo. Tali variabili dei punti attivi vengono utilizzate in seguito per far corrispondere gli hotspot con il contenuto di Quickview.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti attivi. Ogni punto attivo aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo non ambiguo il prodotto nel sistema di back-end esistente.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti attivi.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview esistente. Tali persone probabilmente sapranno qual è il set minimo di dati necessari per identificare Quickview nel sistema. Tuttavia, è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, selezionando un pulsante &quot;Quickview&quot;.
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end esegue il rendering visivo di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Quindi attiva la visualizzazione rapida e acquisisci l’URL Ajax inviato dalla pagina web per caricare i dati o il contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser web moderni dispongono di ispettori web che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser web che includono ispettori web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 per aprire il pannello Strumenti per sviluppatori, quindi selezionare la scheda Rete.
In un Mac, premere Comando+Opzione+I per aprire il pannello Strumenti di sviluppo, quindi selezionare la scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzando la relativa scheda Net. In alternativa, è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.
In un Mac, premere Comando+Opzione+I per aprire il pannello Strumenti di sviluppo, quindi selezionare la scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida nella pagina.

Ora trova l&#39;URL Ajax Quickview nel registro di rete e copia l&#39;URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione rapida sono presenti numerose richieste inviate al server. In genere, l’URL Ajax Quickview è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di stringa di query complessa e il relativo tipo MIME di risposta è `text/html`, `text/xml`oppure `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie di prodotti e tipi. Il motivo è che gli URL Quickview possono avere parti comuni per una determinata categoria di siti web. Tuttavia, cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l’unico elemento dati necessario per aggiungere punti attivi all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta diversi elementi oltre all’SKU. Ad esempio, gli elementi variabili possono includere ID categoria, codice colore e codice dimensione. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto attivo nella funzione immagine interattiva acquistabile in Experience Manager Assets.

Prendi in considerazione i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti attivi risultanti:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile nell’URL è il valore del parametro della stringa query productId= ed è chiaramente un valore SKU. Pertanto, gli hotspot richiedono solo campi SKU compilati con valori come <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso URL.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU degli hotspot: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. La SKU viene memorizzata nel <code>prodId</code> e l'ID categoria<code></code> è memorizzato in <code>category=</code> parametro .</p> <p>Di conseguenza, le definizioni dei punti attivi sono coppie. Cioè, un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>SKU <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>SKU <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

È possibile applicare lo stesso approccio utilizzato nei tre esempi precedenti al [pagina web demo](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html).

La pagina web demo ha diverse miniature di prodotto, ognuna con un pulsante Quickview con etichetta &quot;See More&quot; (Vedi altro). Con lo strumento di debug del browser Web ancora attivato, seleziona ogni pulsante e osserva gli URL registrati di Quickview. Dopo aver attivato tutti e quattro i prodotti Visualizzazioni rapide disponibili sulla pagina, si dispone del seguente elenco di richieste Quickview effettuate al backend:

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

Osservando le chiamate al server, puoi vedere che le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Noterai inoltre che la stringa di query non viene utilizzata e che sono presenti due tipi distinti di parti di dati:

* Il primo tipo è Maschio o Femmina. Puoi chiamare questa &quot;categoria di prodotto&quot;.
* Il secondo tipo è il nome del prodotto, come CamoPullover, che è probabilmente il prodotto SKU.

Considerate queste informazioni, l&#39;intero URL della visualizzazione rapida ha il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, puoi utilizzare `categoryId` e `SKU` per hotspot.

Ora puoi caricare un banner immagine e aggiungervi hotspot utilizzando la funzione di immagine interattiva acquistabile in Experience Manager Assets.

## (Facoltativo) Crea un predefinito visualizzatore di immagini interattive {#optional-creating-an-interactive-image-viewer-preset}

Puoi scegliere di utilizzare il predefinito visualizzatore di immagini interattive predefinito denominato `Shoppable_Banner` questo viene fornito con Experience Manager Assets. Oppure puoi creare un predefinito visualizzatore personalizzato da usare con le immagini interattive.

Quando crei un predefinito visualizzatore di immagini interattive personalizzato, puoi determinare l’aspetto degli hotspot sul banner immagine. Come parte della creazione del predefinito visualizzatore, puoi scegliere di utilizzare un grafico per punti attivi da una raccolta di immagini predefinite.

Dopo aver salvato il predefinito visualizzatore, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefiniti visualizzatore in Experience Manager Assets. Questa funzionalità significa che è visibile nel componente File multimediali interattivi e ogni volta che visualizzi una risorsa. Tuttavia, *distribuire* un banner interattivo con questo predefinito visualizzatore, *pubblicare* anche il predefinito per visualizzatori. Questa regola è valida per i predefiniti visualizzatore personalizzati o predefiniti.

**Per creare un predefinito visualizzatore di immagini interattive:**

1. Nella barra a sinistra, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Nuovo predefinito visualizzatore , digita un nome per descrivere il predefinito visualizzatore banner interattivo.

   Questo titolo viene visualizzato nella pagina dell’elenco Predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva]**.
1. Seleziona **[!UICONTROL Crea]**.
1. Nella pagina Modifica predefinito visualizzatore, tocca il pulsante **[!UICONTROL Aspetto]** scheda .
1. Effettua una delle operazioni seguenti:

   * Per caricare un’immagine del tuo punto attivo da utilizzare sulle immagini, tocca l’icona Selettore risorse . Nella pagina Seleziona contenuto , individua l’immagine del punto attivo che desideri utilizzare e selezionala. Seleziona l’icona con il segno di spunta nell’angolo in alto a destra.
   * Per selezionare un’immagine hotspot predefinita, tocca l’icona Raccolta punti attivi . Nella palette galleria punti attivi, tocca l’immagine del punto attivo che desideri utilizzare.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva]**.

   Assicurati di pubblicare il nuovo predefinito visualizzatore.

   Vedi [Pubblicare i predefiniti per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   Ora puoi caricare un banner immagine.

## Caricare un banner immagine {#uploading-an-image-banner}

Se hai già caricato le immagini da utilizzare, passa al passaggio successivo, [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).

**Per caricare un banner immagine:**

1. Carica i banner immagine che desideri rendere interattivi.

   Vedi [Caricamento delle risorse](/help/assets/manage-digital-assets.md#uploading-assets).

   Ora puoi aggiungere punti attivi al banner immagine; consulta l’attività successiva di seguito.

## Aggiungere punti attivi a un banner immagine {#adding-hotspots-to-an-image-banner}

Puoi aggiungere punti attivi a un banner immagine utilizzando l’editor nella pagina Gestione dei punti attivi.

Quando aggiungi degli hotspot, puoi definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando si incorpora il visualizzatore in un frammento esperienza. Al contrario, utilizza o crea predefiniti visualizzatore che non dispongono di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.

Le opzioni Annulla e Ripristina, situate nell’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell’immagine interattiva, puoi utilizzare Anteprima per vedere come l’immagine interattiva viene visualizzata dai clienti.

Vedi [(Facoltativo) Anteprima delle immagini interattive](#optional-previewing-interactive-images).

>[!NOTE]
Quando aggiungi punti attivi a un&#39;immagine in un&#39;immagine interattiva o in un banner carosello, le informazioni relative ai punti attivi vengono memorizzate nella stessa posizione di metadati. Questa posizione è relativa alla posizione dell’immagine, indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai relativi dati definiti per i punti attivi, in entrambi i visualizzatori.
Tenere tuttavia presente che i caroselli banner supportano mappe immagine su immagini che possono contenere anche punti attivi; un&#39;immagine interattiva non lo è. Tieni presente questo aspetto se vuoi creare un’immagine interattiva o un banner carosello che utilizza la stessa immagine. È invece possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
Vedi anche [Banner a carosello](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

**Per aggiungere punti attivi a un banner immagine:**

1. Nella vista Risorse, individua il banner immagine che desideri rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Passa il puntatore sull’immagine, quindi tocca **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, tocca **[!UICONTROL Modifica]**.

   * Passa il puntatore sull’immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica]**.

   * Per aprirlo nella pagina Vista dettagli, tocca l’immagine. Nella barra degli strumenti, tocca **[!UICONTROL Modifica]**.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Aggiungi punto attivo]** (icona a forma di dito che tocca) per aprire la pagina Gestione punti attivi.
1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Punto attivo]**.

   1. Nell’angolo in alto a sinistra della pagina Gestione punti attivi, tocca **[!UICONTROL Punto attivo]**.
   1.  Sull’immagine, tocca la posizione in cui vuoi visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione. In alternativa, utilizzare i tasti freccia della tastiera per controllare la posizione di un punto attivo selezionato.
   1. Aggiungi altri punti attivi, se necessario, ripetendo i passaggi a e b.
   1. (Facoltativo) Per eliminare un punto attivo, selezionalo sull’immagine, quindi tocca **[!UICONTROL Elimina]** (icona cestino) sotto il **[!UICONTROL Punti attivi]** intestazione.

1. Nel campo di testo Nome, digitare il nome del punto attivo. Questo nome viene visualizzato anche nell’elenco a discesa Punto attivo selezionato .
1. Effettua una delle operazioni seguenti:

   * Seleziona **[!UICONTROL Quickview]**.

      * Se sei un cliente Experience Manager Sites o eCommerce, seleziona l’icona Selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto . Seleziona il prodotto da utilizzare, quindi tocca **Seleziona** nell’angolo superiore destro della pagina. Viene visualizzata nuovamente la pagina Gestione punti attivi.
      * Se sei *not* un cliente Experience Manager Sites o eCommerce

         * Vedi [Identificazione delle variabili dei punti attivi](#optional-identifying-hotspot-variables); devi definire queste variabili.
         * Quindi, inserisci manualmente il valore SKU. Nel campo di testo Valore SKU, digita lo SKU del prodotto. Il valore SKU inserito popola automaticamente la parte variabile del modello Quickview. In questo modo il sistema è in grado di associare il punto attivo toccato a una particolare visualizzazione rapida SKU.
         * (Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili utilizzate per identificare ulteriormente un prodotto, tocca **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio: `category=Mens` è una variabile aggiunta.
   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente Experience Manager Sites, tocca l’icona Selettore sito (cartella). Passa a un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.
      * Se si è un cliente autonomo, nel campo di testo HREF specificare il percorso completo dell&#39;URL di una pagina Web collegata.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Vedi [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md) per ulteriori informazioni.

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza . Seleziona il frammento esperienza da utilizzare. Quindi tocca **[!UICONTROL Seleziona]** nell’angolo superiore destro della pagina. Viene visualizzata nuovamente la pagina Gestione punti attivi.
Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Specifica la larghezza e l’altezza del frammento esperienza come desideri che appaia sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando si incorpora il visualizzatore in un frammento esperienza. Al contrario, utilizza o crea predefiniti visualizzatore che non dispongono di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.



1. Seleziona **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblica l’immagine interattiva. La pubblicazione distribuisce il banner attraverso il cloud e genera anche codice di incorporamento che consente l’integrazione con un sito web di terze parti.

   Vedi [Pubblicare le risorse](/help/assets/manage-digital-assets.md#publish-assets).

   Dopo aver aggiunto gli hotspot e pubblicato l&#39;immagine interattiva, ora puoi aggiungerla al tuo sito web esistente.

   Vedi [Integrare un’immagine interattiva con il sito web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Se modifichi immagini interattive con punti attivi e ritagli l’immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima delle immagini interattive {#optional-previewing-interactive-images}

È possibile utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto dell’immagine interattiva per i clienti. L’anteprima consente inoltre di testare gli hotspot dell’immagine per verificarne il funzionamento come previsto.

Una volta ottenuta l’immagine interattiva, puoi pubblicarla.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).
Vedi [Collegare gli URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.
Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Per visualizzare in anteprima le immagini interattive:**

1. Nella vista Risorse, individua un’immagine interattiva esistente creata e tocca per aprirla in Anteprima.
1. Nell’elenco a discesa Contenuto, nell’angolo in alto a sinistra della pagina Anteprima, tocca **[!UICONTROL Visualizzatori]**.
1. Nell’elenco Visualizzatori, tocca **[!UICONTROL Banner_Shoppable]** o il nome del predefinito per visualizzatori di immagini interattivi che hai creato.
1. Per testare le azioni associate dei punti attivi, tocca i punti attivi sull’immagine.

## Pubblicare risorse di immagini interattive {#publishing-interactive-image-assets}

Vedi [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare le risorse immagine interattive.

## Integrare un’immagine interattiva con il sito web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, aggiunto degli hotspot ad essa e pubblicato l&#39;immagine interattiva, puoi aggiungerla alla pagina del tuo sito web.

Se sei un cliente di Experience Manager Sites, puoi aggiungere l’immagine interattiva trascinando il componente File multimediali interattivi sulla pagina. Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Se sei un cliente Experience Manager Assets indipendente, puoi aggiungere manualmente l’immagine interattiva al tuo sito web come descritto in questa sezione.

1. Copia il codice di incorporamento dell’immagine interattiva pubblicata.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungi il codice di incorporamento copiato nella posizione desiderata all’interno della pagina web.
Il codice di incorporamento copiato è impostato per un ambiente reattivo in modo che si adatti automaticamente all’area assegnata.

**Esempio**

Utilizzo della [sito web dimostrativo come esempio](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html), notare che l&#39;immagine dei tre individui è statica `IMG` tag:

```xml {.line-numbers}
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L&#39;integrazione è semplice come rimuovere `IMG` e sostituirlo con il codice di incorporamento copiato da Experience Manager Assets. Il risultato [mostra l&#39;immagine interattiva acquistabile sulla pagina con tre punti di attivazione cerchio](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
Come questo punto, gli hotspot sull&#39;immagine interattiva acquistabile del sito web demo sono solo a scopo di visualizzazione. Non sono ancora integrati con le visualizzazioni rapide esistenti.

Per applicare un &quot;ritaglio&quot; a un’immagine interattiva acquistabile per un ambiente dinamico, includi l’attributo di configurazione Immagine interattiva `ZoomView.iscommand` al percorso. In questo caso, il `ZoomView` viene chiamato e `iscommand` è il comando di servizio immagine &quot;ritaglia&quot; applicato.

Vedi [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) attributo di configurazione.

Vedi [coltura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) comando di servizio delle immagini.

È ora possibile integrare l’immagine interattiva con una Quickview esistente sul sito web.

## Integrare un’immagine interattiva con una Quickview esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Questa attività si applica solo se sei un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo consiste nell’integrazione dell’immagine interattiva con un’implementazione Quickview esistente sul sito web. Non esiste una soluzione all’integrazione che funzioni per tutti i casi. Ogni implementazione di Quickview è univoca ed è necessario un approccio specifico. In quanto tale, è utile coinvolgere l&#39;assistenza di una persona IT front-end.

L&#39;implementazione di Quickview esistente rappresenta normalmente una catena di azioni correlate che avvengono sulla pagina web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto di Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate non rappresentano necessariamente chiamate API pubbliche indipendenti richiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Quando l&#39;immagine interattiva acquistabile sostituisce il passaggio 1 e in parte il passaggio 2, un utente tocca un punto attivo all&#39;interno dell&#39;immagine acquistabile. Tale interazione dell’utente viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo precedentemente aggiunti a Experience Manager Assets.

In un tale gestore di eventi, il codice front-end effettua le seguenti operazioni:

* Ascolta un evento emesso dall&#39;immagine interattiva acquistabile.
* Crea un URL di visualizzazione rapida basato sui dati del punto attivo.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets ha un gestore di eventi ready-to-use che viene commentato, come visto nel seguente frammento di codice evidenziato:

```xml {.line-numbers}
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

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la pagina web specifica.

Il processo di costruzione dell’URL di visualizzazione rapida è opposto al processo utilizzato per identificare le variabili dei punti attivi trattate in precedenza.

Vedi [Identificare le variabili dei punti di attivazione](#optional-identifying-hotspot-variables).

Utilizzando i precedenti esempi di URL di Quickview, puoi vedere negli esempi seguenti come viene costruito l’URL di Quickview in ogni caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU singolo, trovato nella stringa query</p> </td>
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
   <td><p>SKU e ID categoria nella stringa query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

L’ultimo passaggio per attivare l’URL di visualizzazione rapida e attivare il pannello Quickview richiede l’assistenza di una persona IT front-end dal proprio lavoro. Hanno la conoscenza di sapere come attivare con precisione l&#39;implementazione di Quickview dal passaggio appropriato, avendo un URL di Quickview pronto all&#39;uso.

Puoi vedere come questi passaggi vengono applicati al sito web demo per integrare completamente un’immagine interattiva acquistabile con il codice Quickview. In precedenza, la struttura dell’URL di visualizzazione rapida era identificata come segue:

```xml {.line-numbers}
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire questo URL all’interno di `quickViewActivate` handler, puoi utilizzare `categoryId` e `SKU` campi. Questi campi sono disponibili nella `inData` oggetto passato al gestore dal codice del visualizzatore:

```xml {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo sta attivando la finestra di dialogo Quickview utilizzando un semplice `loadQuickView()` chiamata della funzione. Questa funzione accetta un solo argomento, ovvero l’URL dei dati Quickview. Come tale, l&#39;ultimo passo per integrare l&#39;immagine interattiva acquistabile è quello di aggiungere la seguente riga di codice al `quickViewActivate` handler:

```xml {.line-numbers}
loadQuickView(quickViewUrl);
```

Di seguito è riportato il codice sorgente completo:

```xml {.line-numbers}
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

La [sito web demo finale con immagine interattiva completamente integrata](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html).

## Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedi [Crea Windows® a comparsa personalizzato utilizzando Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
