---
title: Immagini interattive
description: Scopri come utilizzare le immagini interattive in Dynamic Media.
contentOwner: Rick Brough
feature: Interactive Images
role: User
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '4072'
ht-degree: 1%

---

# Immagini interattive{#interactive-images}

Puoi arricchire facilmente le immagini statiche e coinvolgerle con i clienti trascinando gli hotspot &quot;shoppable&quot; su un&#39;immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o un servizio con una funzionalità diretta per i punti vendita &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot;. I clienti possono selezionare questi hotspot che si collegano direttamente al prodotto o al servizio, aggiungerlo al carrello o essere collegati a una pagina web. Esperienze dirette come queste aumentano il coinvolgimento dei clienti e le conversioni sul tuo sito web.

Di seguito è riportato un banner acquistabile con una finestra popup Quickview. L&#39;utente attiva la Quickview toccando il cerchio o il &quot;punto attivo&quot; sul modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Vedi [immagini interattive in azione](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=it) nella pagina Web illustrata sopra.

## Guarda come vengono creati i banner interattivi per le immagini {#watch-how-interactive-image-banners-are-created}

Segui la procedura dettagliata per [la creazione dei banner interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10 minuti e 33 secondi). Scopri anche come visualizzare in anteprima, modificare e distribuire banner interattivi.

## Guida introduttiva: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le immagini interattive in Adobe Experience Manager Assets.

Cerca l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di avvio rapido. Contiene una breve esercitazione basata su un esempio di [pagina Web a cui non sono ancora state aggiunte immagini interattive](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=it).



Il tutorial illustra i passaggi necessari per integrare le immagini interattive nel sito web.

Passaggi delle immagini interattive:

1. **(Facoltativo) Identificare le variabili hotspot**. Se utilizzi Adobe Experience Manager Assets e Dynamic Media in modalità standalone, identifica le variabili dinamiche utilizzate nell’implementazione Quickview esistente. In questo modo è possibile inserire i dati dei punti attivi durante la creazione dell&#39;immagine interattiva. Vedere [(Facoltativo) Identificazione delle variabili hotspot](#optional-identifying-hotspot-variables).
Tuttavia, se utilizzi Experience Manager Sites, o Experience Manager eCommerce, o entrambi, questo passaggio non è necessario.

1. **(Facoltativo) Crea un predefinito visualizzatore di immagini interattivo**. Personalizzare l&#39;immagine grafica utilizzata per rappresentare i punti attivi. Non è necessario creare un predefinito visualizzatore di immagini interattive se si intende utilizzare il predefinito visualizzatore di immagini interattive predefinito `Shoppable_Banner`.
Vedere [(facoltativo) Creazione di un predefinito visualizzatore di immagini interattivo](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Carica un banner immagine**. Carica i banner immagine da rendere interattivi.
Vedi [Caricamento di un banner immagine](#uploading-an-image-banner).

1. **Aggiungi punti attivi a un banner immagine**. Aggiungi uno o più punti attivi a un banner immagine. Associa ciascuno di essi a un’azione, ad esempio un collegamento ipertestuale, una visualizzazione rapida o un frammento di esperienza. Dopo aver aggiunto gli hotspot, terminerai questa attività pubblicando l’immagine interattiva.
Vedi [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).
Vedi [Anteprima delle immagini interattive](#optional-previewing-interactive-images) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del banner acquistabile e testarne l’interattività.
Per informazioni dettagliate su come pubblicare risorse immagine interattive, consulta [Pubblicazione di Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. **Aggiungi un&#39;immagine interattiva al tuo sito Web o al tuo sito Web in Experience Manager**. Se utilizzi Sites, eCommerce o entrambi, puoi aggiungere immagini interattive direttamente a una pagina web in Experience Manager. Trascina il componente File multimediali interattivi sulla pagina. Consulta [Aggiunta di Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Se utilizzi Experience Manager Assets e Dynamic Media in modo indipendente, copia il codice da incorporare sul tuo sito web. Quindi, integrarlo con Quickview esistente. Consulta [Integrazione di un&#39;immagine interattiva con il tuo sito Web](#integrating-an-interactive-image-with-your-website).
Se si utilizza un modulo WCM (Web Content Manager) di terze parti, integrare il nuovo video interattivo con il Quickview esistente utilizzato sul sito Web. Vedi [Integrazione di un&#39;immagine interattiva con un Quickview esistente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Facoltativo) Identificare le variabili dei punti attivi {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se:
>
>* Per aggiungere interattività all’immagine, attiva le Visualizzazioni rapide.
>* L&#39;implementazione di Experience Manager *non* utilizza un framework di integrazione eCommerce per estrarre i dati di prodotto in Experience Manager da qualsiasi soluzione eCommerce. Tali soluzioni includono IBM® WebSphere® Commerce, Elastic Path, SAP Hybris o Intershop.
>
>Se l’implementazione di Experience Manager utilizza l’eCommerce, puoi saltare questa attività e passare a quella successiva.

Inizia identificando le variabili dinamiche utilizzate dall’implementazione Quickview esistente in modo da poter immettere i dati dei punti attivi per creare l’immagine interattiva.

Quando aggiungi punti attivi a un&#39;immagine del banner in Experience Manager Assets, assegna uno SKU (Stock Keeping Unit). Lo SKU è un identificatore univoco per ciascun prodotto o servizio offerto. Inoltre, aggiungi eventuali variabili facoltative aggiuntive a ciascun hotspot. Tali variabili di punti attivi vengono utilizzate in un secondo momento per far corrispondere i punti attivi con il contenuto Quickview.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti attivi. Ogni punto attivo aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo univoco il prodotto nel sistema back-end esistente.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti attivi.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione Quickview esistente. Queste persone probabilmente sanno qual è il set minimo di dati necessari per identificare Quickview nel sistema. Tuttavia, è anche possibile semplicemente analizzare il comportamento esistente del codice front-end.

La maggior parte delle implementazioni Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, selezionando un pulsante &quot;Quickview&quot;.
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto Quickview, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end riproduce visivamente tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Quindi attiva Quickview e acquisisci l’URL Ajax inviato dalla pagina web per caricare i dati o il contenuto Quickview.

In genere non è necessario utilizzare strumenti di debug specifici. I browser web moderni dispongono di web inspector che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono i controlli Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premi F12 per aprire il pannello Strumenti di sviluppo e quindi seleziona la scheda Rete.
In un Mac, premi Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi seleziona la scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzando la relativa scheda Net. In alternativa, è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.
In un Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi selezionare la scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attiva Quickview sulla pagina.

Ora trova l’URL Ajax di Quickview nel registro di rete e copia l’URL registrato per l’analisi futura. Di solito, quando si attiva Quickview, vengono inviate numerose richieste al server. In genere, l’URL Ajax di Quickview è uno dei primi dell’elenco. Ha una porzione o un percorso di stringa di query complesso e il relativo tipo MIME di risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL Quickview possono avere parti comuni per una determinata categoria di siti Web. Tuttavia, cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL di Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l&#39;unico dato necessario per aggiungere punti attivi all&#39;immagine del banner.

Tuttavia, in casi complessi, oltre allo SKU l&#39;URL Quickview presenta diversi elementi variabili. Ad esempio, elementi diversi possono includere l’ID categoria, il codice colore e il codice dimensione. In questi casi, ogni elemento è una variabile separata nella definizione dei dati dei punti attivi nella funzione per immagini interattive acquistabili di Experience Manager Assets.

Prendi in considerazione i seguenti esempi di URL Quickview e le variabili hotspot risultanti:

<table>
  <tbody>
  <tr>
    <td><p>Singolo SKU, trovato nella stringa di query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile nell’URL è il valore del parametro della stringa query productId=, che è chiaramente un valore SKU. Pertanto, gli hotspot richiedono solo campi SKU compilati con valori come <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>Singolo SKU, trovato nel percorso URL.</p> </td>
    <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell'ultima parte del percorso e diventa il valore SKU dei punti attivi: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è archiviato nel parametro <code>prodId</code> e l'ID categoria <code></code> nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni dei punti attivi sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>Lo SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>Lo SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>Lo SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Puoi applicare lo stesso approccio utilizzato nei tre esempi precedenti alla [pagina web demo](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=it).

La pagina web demo presenta diverse miniature di prodotto, ciascuna con un pulsante Quickview etichettato &quot;See More&quot; (Vedi altro). Con lo strumento di debug del browser ancora attivato, seleziona ogni pulsante e annota gli URL registrati di Quickview. Dopo aver attivato tutte e quattro le visualizzazioni rapide del prodotto disponibili nella pagina, viene visualizzato il seguente elenco di richieste Quickview effettuate al backend:

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

Osservando le chiamate al server, puoi vedere che le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Inoltre, la stringa di query non viene utilizzata e sono presenti due tipi distinti di parti di dati:

* Il primo tipo è Maschio o Femmina. Puoi chiamare questa &quot;categoria di prodotto&quot;.
* Il secondo tipo è il nome del prodotto, come CamoPullover, che è probabilmente lo SKU del prodotto.

Considerate queste informazioni, l&#39;intero URL Quickview ha il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, utilizzerai `categoryId` e `SKU` per gli hotspot.

Ora puoi caricare un banner immagine e aggiungervi punti attivi utilizzando la funzione per immagini interattive acquistabili in Experience Manager Assets.

## (Facoltativo) Crea un predefinito visualizzatore di immagini interattivo {#optional-creating-an-interactive-image-viewer-preset}

È possibile scegliere di utilizzare il predefinito visualizzatore predefinito di immagini interattive denominato `Shoppable_Banner` fornito con Experience Manager Assets. Oppure puoi creare un predefinito visualizzatore personalizzato da utilizzare con le immagini interattive.

Quando crei un predefinito visualizzatore immagine interattiva personalizzato, puoi determinare l&#39;aspetto dei punti attivi sul banner dell&#39;immagine. Come parte della creazione del predefinito visualizzatore, puoi scegliere di utilizzare un elemento grafico a punti attivi da una galleria di immagini predefinite.

Dopo aver salvato il predefinito visualizzatore, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefinito visualizzatore di Experience Manager Assets. Questa funzionalità indica che è visibile nel componente File multimediali interattivi e ogni volta che visualizzi una risorsa. Tuttavia, per *consegnare* un banner interattivo con questo predefinito visualizzatore, *pubblicare* anche il tuo predefinito visualizzatore. Questa regola è valida per i predefiniti visualizzatore personalizzati o predefiniti.

**Per creare un predefinito visualizzatore immagini interattivo:**

1. Nella barra a sinistra, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Seleziona **[!UICONTROL Crea]** nell&#39;angolo superiore destro della pagina.
1. Nella finestra di dialogo Nuovo predefinito visualizzatore, digita un nome per descrivere il predefinito visualizzatore banner interattivo.

   Questo titolo viene visualizzato nella pagina Elenco predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva]**.
1. Seleziona **[!UICONTROL Crea]**.
1. Nella pagina Modifica predefinito visualizzatore, seleziona la scheda **[!UICONTROL Aspetto]**.
1. Effettua una delle seguenti operazioni:

   * Per caricare la tua immagine del punto attivo da utilizzare sulle immagini, seleziona l’icona Selettore risorse. Nella pagina Seleziona contenuto, individua l’immagine del punto attivo che desideri utilizzare e selezionala. Seleziona l’icona a forma di segno di spunta nell’angolo in alto a destra.
   * Per selezionare un&#39;immagine punto attivo predefinita, selezionate l&#39;icona Raccolta punti attivi. Nella tavolozza della galleria di punti attivi, selezionare l&#39;immagine che si desidera utilizzare.

1. Seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina.

   Assicurati di pubblicare il nuovo predefinito visualizzatore.

   Consulta [Predefiniti visualizzatore pubblicazione](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   Ora puoi caricare un banner immagine.

## Carica un banner immagine {#uploading-an-image-banner}

Se hai già caricato le immagini che desideri utilizzare, passa al passaggio successivo, [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).

**Per caricare un banner immagine:**

1. Carica i banner immagine da rendere interattivi.

   Consulta [Caricamento risorse](/help/assets/manage-digital-assets.md#uploading-assets).

   Ora puoi aggiungere punti attivi al banner dell&#39;immagine; vedi l&#39;attività successiva qui sotto.

## Aggiunta di punti attivi a un banner immagine {#adding-hotspots-to-an-image-banner}

Puoi aggiungere punti attivi a un banner immagine utilizzando l&#39;editor nella pagina Gestione punti attivi.

Quando aggiungi punti attivi, puoi definirli come una visualizzazione a comparsa Quickview, un collegamento ipertestuale o un frammento di esperienza.

Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!NOTE]
>
>Gli strumenti per la condivisione di social media nell’immagine interattiva non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza. Puoi invece utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione tramite social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

Le opzioni Annulla e Ripristina, posizionate nell&#39;angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell&#39;immagine interattiva, è possibile utilizzare Anteprima per visualizzare una rappresentazione dell&#39;aspetto dell&#39;immagine interattiva per i clienti.

Vedi [(facoltativo) Anteprima immagini interattive](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando aggiungi punti attivi a un&#39;immagine in un&#39;immagine interattiva o in un banner carosello, le informazioni sui punti attivi vengono memorizzate nella stessa posizione di metadati. Questa posizione è relativa alla posizione dell&#39;immagine, indipendentemente dal fatto che si tratti di un&#39;immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti attivi definiti, in entrambi i visualizzatori.
>
>Tieni presente, tuttavia, che i banner a carosello supportano le mappe immagine sulle immagini che possono anche contenere punti attivi, diversamente da un’immagine interattiva. Tieni presente questo pensiero se intendi creare un’immagine interattiva o un banner a carosello che utilizza la stessa immagine. È invece possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
>
>Vedi anche [Banner a carosello](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
>
>Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, questi vengono rimossi.

**Per aggiungere punti attivi a un banner immagine:**

1. Nella vista Assets, individua il banner immagine da rendere interattivo.
1. Effettua una delle seguenti operazioni:

   * Passa il mouse sull&#39;immagine, quindi seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, selezionare **[!UICONTROL Modifica]**.

   * Passa il mouse sull&#39;immagine, quindi seleziona **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica]**.

   * Per aprirla nella pagina Vista dettaglio, selezionare l&#39;immagine. Nella barra degli strumenti, seleziona **[!UICONTROL Modifica]**.

1. Nell&#39;angolo superiore sinistro della pagina, selezionare **[!UICONTROL Aggiungi punto attivo]** (icona di selezione del dito) per aprire la pagina Gestione punti attivi.
1. Seleziona **[!UICONTROL Punto attivo]** nell&#39;angolo superiore sinistro della pagina.

   1. Selezionare **[!UICONTROL Punto attivo]** nell&#39;angolo superiore sinistro della pagina Gestione punti attivi.
   1. Sull&#39;immagine, selezionare la posizione in cui si desidera visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione. In alternativa, utilizzare i tasti freccia della tastiera per controllare la posizione di un&#39;area sensibile selezionata.
   1. Se necessario, aggiungi altri punti attivi ripetendo i passaggi a e b.
   1. (Facoltativo) Per eliminare un punto attivo, selezionalo nell&#39;immagine, quindi seleziona **[!UICONTROL Elimina]** (icona cestino) sotto l&#39;intestazione **[!UICONTROL Punti attivi]**.

1. Nel campo di testo Nome digitare il nome del punto attivo. Questo nome viene visualizzato anche nell&#39;elenco a discesa Punto attivo selezionato.
1. Effettua una delle seguenti operazioni:

   * Selezionare **[!UICONTROL Quickview]**.

      * Se sei un cliente Experience Manager Sites o eCommerce, seleziona l’icona del selettore prodotti (lente di ingrandimento) per aprire la pagina Seleziona prodotto. Seleziona il prodotto da utilizzare, quindi fai clic su **Seleziona** nell&#39;angolo superiore destro della pagina. Viene visualizzata di nuovo la pagina Gestione punti attivi.
      * Se *non* sei un cliente Experience Manager Sites o eCommerce

         * Vedere [Identificazione delle variabili hotspot](#optional-identifying-hotspot-variables). È necessario definire queste variabili.
         * Quindi, immetti manualmente il valore SKU. Nel campo di testo Valore SKU, digita lo SKU del prodotto. Il valore SKU immesso popola automaticamente la parte variabile del modello Quickview. In questo modo il sistema è in grado di associare il punto attivo toccato a Quickview di una particolare SKU.
         * (Facoltativo) Se in Quickview sono presenti altre variabili utilizzate per identificare ulteriormente un prodotto, selezionare **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. `category=Mens` è ad esempio una variabile aggiunta.

   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Selettore siti (cartella). Passa a un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
      * Se si è clienti autonomi, specificare il percorso URL completo di una pagina Web collegata nel campo di testo HREF.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Seleziona il frammento di esperienza da utilizzare. Quindi seleziona **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro della pagina. Viene visualizzata di nuovo la pagina Gestione punti attivi.
Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md).

      * Specifica la larghezza e l’altezza del frammento di esperienza da visualizzare sul banner.

        >[!NOTE]
        >
        >Gli strumenti per la condivisione di social media nell’immagine interattiva non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza. Puoi invece utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione tramite social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

1. Seleziona **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblica l’immagine interattiva. La pubblicazione distribuisce il banner attraverso il cloud e genera anche codice di incorporamento che consente l’integrazione con un sito web di terze parti.

   Consulta [Pubblicare risorse](/help/assets/manage-digital-assets.md#publish-assets).

   Dopo aver aggiunto gli hotspot e pubblicato l&#39;immagine interattiva, puoi aggiungerla al sito Web esistente.

   Vedi [Integrare un&#39;immagine interattiva con il tuo sito Web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima di immagini interattive {#optional-previewing-interactive-images}

Puoi utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto dell’immagine interattiva ai clienti. L&#39;anteprima consente inoltre di verificare gli hotspot dell&#39;immagine per verificarne il comportamento previsto.

Quando sei soddisfatto dell’immagine interattiva, puoi pubblicarla.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consulta [Collegare gli URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Consulta [Aggiungere Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Per visualizzare in anteprima le immagini interattive:**

1. Nella vista Assets, individua un’immagine interattiva esistente creata e seleziona per aprirla in Anteprima.
1. Selezionare **[!UICONTROL Visualizzatori]** nell&#39;elenco a discesa Contenuto nell&#39;angolo superiore sinistro della pagina Anteprima.
1. Nell&#39;elenco Visualizzatori selezionare **[!UICONTROL Shoppable_Banner]** o il nome del predefinito visualizzatore di immagini interattivo creato.
1. Per verificare le azioni associate ai punti attivi, seleziona i punti attivi sull’immagine.

## Pubblicare risorse di immagini interattive {#publishing-interactive-image-assets}

Per informazioni dettagliate su come pubblicare risorse immagine interattive, consulta [Pubblica Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Integrare un’immagine interattiva con il sito web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, aggiunto punti attivi e pubblicato l&#39;immagine interattiva, puoi aggiungerla alla pagina del sito Web.

I clienti di Experience Manager Sites possono aggiungere l’immagine interattiva trascinando il componente File multimediali interattivi nella pagina. Consulta [Aggiungere Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Se sei un cliente Experience Manager Assets indipendente, puoi aggiungere manualmente l’immagine interattiva al sito web come descritto in questa sezione.

1. Copia il codice di incorporamento dell&#39;immagine interattiva pubblicata.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).

1. Aggiungi il codice da incorporare copiato nella posizione desiderata all’interno della pagina web.
Il codice di incorporamento copiato è impostato per un ambiente reattivo in modo che si adatti automaticamente all’area assegnata.

**Esempio**

Utilizzando il sito Web [demo come esempio](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=it), l&#39;immagine dei tre singoli utenti è un tag `IMG` statico:

```xml {.line-numbers}
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L&#39;integrazione è semplice come rimuovere il tag `IMG` e sostituirlo con il codice da incorporare copiato da Experience Manager Assets. Il risultato [mostra l&#39;immagine interattiva acquistabile nella pagina con tre punti attivi circolari](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=it).

>[!NOTE]
>
>A questo punto, gli hotspot sull’immagine interattiva acquistabile del sito web demo sono solo a scopo di visualizzazione. Non sono ancora integrate con le visualizzazioni rapide esistenti.

Per applicare un ritaglio a un&#39;immagine interattiva acquistabile per un ambiente reattivo, includere nel percorso l&#39;attributo di configurazione dell&#39;immagine interattiva `ZoomView.iscommand`. In questo caso, viene chiamato il componente `ZoomView` e `iscommand` è il comando di server immagini &quot;ritagliate&quot; applicato.

Vedere l&#39;attributo di configurazione [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html?lang=it).

Vedere il comando [crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html?lang=it) image serving.

Ora puoi integrare l’immagine interattiva con un Quickview esistente sul tuo sito web.

## Integrare un&#39;immagine interattiva con un Quickview esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Questa attività si applica solo se sei un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo è l’integrazione dell’immagine interattiva con un’implementazione Quickview esistente sul sito web. Non esiste una soluzione all’integrazione che funzioni per tutti i casi. Ogni implementazione Quickview è unica ed è necessario un approccio specifico. Di conseguenza, è utile coinvolgere l’assistenza di un responsabile IT front-end.

L’implementazione Quickview esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina web nell’ordine seguente:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto nel passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente.

Queste chiamate non rappresentano necessariamente chiamate API pubbliche indipendenti che vengono chiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo è nascosto nell’ultima fase (callback) del passaggio precedente.

Quando l’immagine interattiva acquistabile sostituisce il passaggio 1 e parzialmente il passaggio 2, l’utente tocca un punto attivo all’interno dell’immagine acquistabile. Tale interazione con l’utente viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati dei punti attivi aggiunti in precedenza a Experience Manager Assets.

In un gestore eventi di questo tipo, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dall’immagine interattiva acquistabile.
* Costruisce un URL Quickview in base ai dati del punto attivo.
* Attiva il processo di caricamento di Quickview dal backend e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets include un gestore eventi pronto all’uso e commentato, come mostrato nel seguente snippet di codice evidenziato:

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
                    //To pass other parameter from the hotspot, add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //See your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Pertanto, è necessario solo rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la particolare pagina web.

Il processo di costruzione dell’URL Quickview è opposto a quello utilizzato per identificare le variabili hotspot trattate in precedenza.

Vedi [Identificare le variabili hotspot](#optional-identifying-hotspot-variables).

Utilizzando i precedenti esempi di URL di Quickview, è possibile vedere come viene costruito l&#39;URL di Quickview in ogni caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU singola, trovata nella stringa di query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
   <td><p>SKU singola, trovata nel percorso URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/product/" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID categoria nella stringa query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
 </tbody>
</table>

L’ultimo passaggio per attivare l’URL Quickview e il pannello Quickview richiede l’assistenza di un IT front-end dal tuo lavoro. Possiedono le conoscenze necessarie per sapere come attivare con precisione l’implementazione Quickview dal passaggio corretto, avendo un URL Quickview pronto all’uso.

Puoi vedere come questi passaggi vengono applicati al sito web demo per integrare completamente un’immagine interattiva acquistabile con il codice Quickview. In precedenza, la struttura dell’URL Quickview era identificata come segue:

```xml {.line-numbers}
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire l&#39;URL nel gestore `quickViewActivate`, è possibile utilizzare i campi `categoryId` e `SKU`. Questi campi sono disponibili nell&#39;oggetto `inData` passato al gestore dal codice del visualizzatore:

```xml {.line-numbers}
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo sta attivando la finestra di dialogo Quickview utilizzando una semplice chiamata alla funzione `loadQuickView()`. Questa funzione accetta un solo argomento, ovvero l’URL dati Quickview. Di conseguenza, l&#39;ultimo passaggio per integrare l&#39;immagine interattiva acquistabile consiste nell&#39;aggiungere la seguente riga di codice al gestore `quickViewActivate`:

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

Il sito Web di dimostrazione [final con l&#39;immagine interattiva completamente integrata](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=it).

## Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedere [Creare finestre popup personalizzate® utilizzando Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
