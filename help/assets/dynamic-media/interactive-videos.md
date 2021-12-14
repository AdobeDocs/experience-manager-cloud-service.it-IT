---
title: Video interattivi
description: Scopri come lavorare con video interattivi e video acquistabili in Dynamic Media.
feature: Interactive Videos
role: User
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: ba752888601413dd4725a7a137f8b468b92ad5c7
workflow-type: tm+mt
source-wordcount: '5966'
ht-degree: 3%

---

# Video interattivi{#interactive-videos}

Puoi creare facilmente video interattivi - noti anche come video acquistabili - che guidano la conversione direttamente dal video. Il coinvolgimento dei clienti con il video si svolge in un pannello accanto al lettore video, dove vengono visualizzate informazioni o miniature relative a servizi, prodotti in base alle funzioni presenti nel video. I clienti possono selezionare la miniatura ed essere collegati direttamente al servizio oppure aggiungere l’articolo a un carrello per un acquisto immediato, oppure essere collegati a una pagina web per ulteriori informazioni.

Al termine del video, viene visualizzato un riepilogo visivo di tutte le offerte per attivare una chiamata all’azione. I clienti hanno un&#39;altra opportunità per selezionare l&#39;elemento desiderato. Esperienze fruibili e specifiche, come queste, aumentano il coinvolgimento e le conversioni dei clienti.

Vedi anche [Immagini interattive](/help/assets/dynamic-media/interactive-images.md).

## Video interattivo in azione {#interactive-video-in-action}

Per visualizzare un video interattivo e acquistabile in azione, seleziona [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), scorri fino a **[!UICONTROL Media acquistabili]** nella pagina, quindi seleziona il video acquistabile per iniziare la riproduzione.

* Durante la riproduzione, quando i prodotti vengono utilizzati nel video, il prodotto identico viene visualizzato a destra come immagine in miniatura.

* Per mettere in pausa il video e aprire la visualizzazione rapida del prodotto, seleziona la miniatura. Ad esempio, selezionare l&#39;immagine in miniatura di KitchenAid nel video per vedere una rotazione a 360° del mixer, oppure ingrandirla per vedere i dettagli del mixer.

Vedi anche [Utilizzare i video interattivi con Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader selected the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>Se crei un video interattivo per avviare una pagina web quando un utente seleziona un&#39;immagine in miniatura, alcuni dispositivi impediscono l&#39;apertura della pagina web a comparsa. In questi casi, modifica l&#39;impostazione di blocco dei popup sul dispositivo. Ad esempio, su un Apple iPhone 6, vai a **[!UICONTROL Impostazioni]** > **[!UICONTROL Safari]** > **[!UICONTROL Blocca popup]** quindi far scorrere il controllo su **[!UICONTROL Disattivato]**. Ora, quando si riproduce un video interattivo e si seleziona una miniatura, viene richiesto se si desidera aprire il pop-up. Se si accetta, viene visualizzata la pagina web.

### Guarda come vengono creati i video interattivi {#watch-how-interactive-videos-are-created}

Guarda una procedura dettagliata su [creazione dei video interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)(7 minuti e 30 secondi).
Anche se la procedura dettagliata per i video è contrassegnata con il marchio Assets on Demand, i principi e i passaggi illustrati restano applicabili ai video interattivi in Adobe Experience Manager Assets.

### Adobe webinar sul successo del cliente {#adobe-customer-success-webinar}

La [Utilizzo di video interattivi, condivisione dei collegamenti e condivisione YouTube in Experience Manager Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/) Il webinar illustra come utilizzare i video interattivi e altre funzioni per collegare gli eventi basati sulla conversione ai contenuti di marketing video.

## Avvio rapido: Video interattivi {#quick-start-interactive-videos}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare i video interattivi in Dynamic Media.

Cerca la **Esempio** intestazione all&#39;interno di alcune delle attività di avvio rapido. Contiene una breve esercitazione basata su [pagina web demo iniziale *non* hanno ancora aggiunto l’interattività](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html).

Gli **esempi** illustrano i passaggi necessari per integrare i video interattivi nel sito web.

Al termine dell’esercitazione nell’ultima sezione Esempio, [la pagina web demo finale con il video interattivo completamente integrato viene visualizzata in questo modo](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html).

Passaggi video interattivi:

1. **(Facoltativo) Identifica le variabili Quickview** - Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione di Quickview esistente. Puoi utilizzare le variabili per mappare le miniature dei prodotti sulla visualizzazione rapida del prodotto corrispondente al momento della creazione del video interattivo. Vedi [(Facoltativo) Identificazione delle variabili Quickview](#optional-identifying-quickview-variables).
   **Questo passaggio è necessario solo se sono soddisfatte tutte le seguenti condizioni:**
・ Per aggiungere interattività al video, attivare le visualizzazioni rapide.
・ L&#39;implementazione di Experience Manager 
*not* utilizza un framework di integrazione eCommerce per estrarre i dati dei prodotti in Experience Manager da qualsiasi soluzione eCommerce come IBM® WebSphere® Commerce, Elastic Path, SAP Hybris o Intershop.

1. **(Facoltativo) Crea un predefinito visualizzatore video interattivo.** - Personalizza l’aspetto e il comportamento dei vari componenti che compongono il lettore, come lo scorrimento video e le miniature interattive.
La creazione di un predefinito per visualizzatori video interattivi non è necessaria se si intende utilizzare i predefiniti per visualizzatori video interattivi predefiniti `Shoppable_Video_Light` o `Shoppable_Video_Dark` invece.
Vedi [Creare un predefinito per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) (facoltativo) e [Considerazioni speciali per la creazione di un predefinito visualizzatore interattivo](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **Caricare un video e le relative risorse di immagine associate** - Carica un video e le immagini associate che desideri rendere interattive.
Vedi [Caricare un video e le relative risorse di miniatura associate](#uploading-a-video-and-its-associated-thumbnail-assets).

   >[!NOTE]
   >
   >Il formato video MXF non è ancora supportato per l&#39;utilizzo con video interattivi in Dynamic Media.

1. **Aggiungi interattività al video** - Aggiungi uno o più segmenti di tempo al video. Quindi, associa le miniature delle immagini all’interno di tali segmenti di tempo. Assegna a ciascuna miniatura immagine un’azione come un collegamento ipertestuale, una visualizzazione rapida o un frammento esperienza.
(Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con pagine Experience Manager Sites.)
Per terminare, pubblica le risorse video interattive. La pubblicazione crea il codice di incorporamento o l’URL da copiare e applicare alla pagina di destinazione del sito web. Vedi [Aggiungi interattività al video](#adding-interactivity-to-your-video).
Vedi [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. **Aggiungi un video interattivo al tuo sito web o al tuo sito web, ad Experience Manager** - Se utilizzi Experience Manager Sites o eCommerce, o entrambi, aggiungi il video interattivo a una pagina web nell’Experience Manager. Trascina il componente File multimediali interattivi sulla pagina. Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Utilizza il codice di incorporamento o l’URL per integrare il video interattivo con le esperienze del sito web. Vedi [Integrare un video interattivo con il sito web](#integrating-an-interactive-video-with-your-website).
Se utilizzi un WCM di terze parti (Web Content Manager), devi integrare il nuovo video interattivo con l’implementazione Quickview esistente utilizzata sul sito web. Vedi [Integrare un video interattivo con una Quickview esistente](#integrating-an-interactive-video-with-an-existing-quickview).
   [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## (Facoltativo) Identifica le variabili Quickview {#optional-identifying-quickview-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività al video, attiva le visualizzazioni rapide.
>* La tua implementazione di Experience Manager *not* utilizza un framework di integrazione eCommerce per estrarre i dati dei prodotti in Experience Manager da qualsiasi soluzione eCommerce come IBM® WebSphere® Commerce, Elastic Path, SAP Hybris o Intershop. <!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->

>
>Se l’implementazione di Experience Manager utilizza eCommerce, puoi saltare questa attività e passare all’attività successiva.

Per iniziare, identifica le variabili dinamiche utilizzate dall’implementazione di Quickview esistente in modo da poter mappare le miniature dei prodotti sul prodotto corrispondente Quickview durante il processo di creazione di video interattivo.

Quando aggiungi segmenti di tempo a un video, assegni un SKU (Stock Keeping Unit) e qualsiasi variabile aggiuntiva a ogni miniatura che aggiungi a un segmento. Tali variabili vengono utilizzate in seguito per visualizzare il prodotto Quickview corretto.

È importante identificare correttamente le variabili necessarie per attivare in modo univoco una visualizzazione rapida del prodotto.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview esistente. È probabile che conoscano il set minimo di dati che identifica Quickview nel sistema. Tuttavia, è possibile semplicemente analizzare il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, selezionando un pulsante &quot;Quickview&quot;.
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end esegue il rendering visivo di tali contenuti sullo schermo.

L’approccio, quindi, consiste nel visitare diverse aree del sito web esistente in cui è implementato Quickview. Quindi attiva la visualizzazione rapida e acquisisci l’URL Ajax inviato dalla pagina web per il caricamento dei dati o del contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser web moderni dispongono di ispettori web che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser web che includono ispettori web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premi **F12** (Windows®) o **Comando+Opzioni+I** (Mac) per aprire il pannello Strumenti per sviluppatori, quindi selezionare il **Rete** scheda .

* In Firefox, è possibile attivare il plug-in Firebug premendo **F12** (Windows®) o **Comando+Opzione+I** (Mac) e utilizza i relativi **[!UICONTROL Netto]** oppure è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.

* In Internet Explorer, attivare lo strumento di debug premendo **F12**.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida nella pagina.

Ora trova l&#39;URL Ajax Quickview nel registro di rete e copia l&#39;URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione rapida sono presenti numerose richieste inviate al server. In genere, l’URL Ajax Quickview è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di stringa di query complessa e il relativo tipo MIME di risposta è `text/html`, `text/xml`oppure `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie di prodotti e tipi. Il motivo è che gli URL di visualizzazione rapida hanno parti comuni per una determinata categoria di siti web, ma cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL Quickview è lo SKU del prodotto. In questo caso, il valore SKU del prodotto è l’unico elemento dati necessario per aggiungere miniature a un segmento di tempo nel video interattivo di Experience Manager.

Tuttavia, in casi complessi, l’URL Quickview presenta diversi elementi diversi oltre all’SKU del prodotto, come ID categoria e codice colore. In tali casi, ogni elemento di questo tipo diventa una variabile separata nella definizione dei dati delle miniature di Experience Manager.

Prendi in considerazione i seguenti esempi di URL di Quickview e le relative variabili di miniatura risultanti:

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
    </ul> <p>L’unica parte variabile nell’URL è il valore della variabile <code>productId=</code> parametro della stringa query, ed è chiaramente un valore SKU. Pertanto, le miniature richiedono solo campi SKU compilati con valori come <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso URL.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU delle miniature di Experience Manager: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. La SKU viene memorizzata nel <code>prodId</code> e l'ID della categoria viene memorizzato nella variabile <code>category=</code> parametro .</p> <p>Di conseguenza, le definizioni delle miniature sono coppie. Cioè, un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li>SKU <code>305466</code> e <code>categoryId</code> è <code>1100004</code></li>
      <li>SKU <code>310181</code> e <code>categoryId</code> è <code>1100004</code></li>
      <li>SKU <code>308706</code> e <code>categoryId</code> è <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Quando l&#39;approccio di cui sopra viene applicato al sito web Example, hai una pagina web con diverse miniature di prodotto, ognuna con un pulsante &quot;SEE MORE&quot;:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Dopo aver attivato tutte le visualizzazioni rapide del prodotto disponibili sulla pagina, ottieni il seguente elenco di richieste Quickview effettuate al backend:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

Osservando le chiamate al server, le informazioni specifiche per prodotto sono presenti solo nel percorso della richiesta. Noterai inoltre che la stringa di query non viene utilizzata e che sono coinvolti due tipi distinti di elementi di dati:

* Il primo tipo è candele, cuscini, mobili e oggetti di vetro. Puoi chiamare questa &quot;categoria di prodotto&quot;.
* Il secondo tipo è il codice del prodotto, ad esempio 233916597. Si può presumere che sia &quot;SKU prodotto&quot;.

Considerate queste informazioni, l&#39;intero URL della visualizzazione rapida ha il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, si conclude che per le miniature è possibile utilizzare le due variabili seguenti: `categoryId` e `SKU`.

Ora puoi caricare un video e le relative risorse di miniatura associate.

## (Facoltativo) Crea un predefinito visualizzatore video interattivo. {#optional-creating-an-interactive-video-viewer-preset}

Puoi saltare questa attività e passare all’attività successiva se vuoi utilizzare uno dei tipi predefiniti per visualizzatori video interattivi predefiniti `Shoppable_Video_dark` o `Shoppable_Video_light`.

Quando nell’ambiente di authoring viene selezionata una miniatura, viene visualizzata un’anteprima della finestra di dialogo Quickview.

![chlimage_1-21](assets/chlimage_1-127.png)

Facoltativamente, puoi creare il tuo predefinito visualizzatore video interattivo personalizzato. È possibile determinare, tra l’altro, lo stile del lettore video, le miniature interattive e la vista a griglia delle miniature visualizzata alla fine del video.

Un predefinito per visualizzatori video interattivi esegue correttamente il rendering del video e di tutti i segmenti della timeline aggiunti. Utilizza anche un esempio di Quickview predefinito quando selezioni una miniatura di prodotto in modalità Anteprima in modo da poterne testare l’interattività prima della pubblicazione.

Dopo aver salvato il predefinito visualizzatore, lo stato relativo viene impostato automaticamente su **On **nella pagina Predefiniti visualizzatore. Lo stato indica che è visibile nel componente Dynamic Media e ogni volta che lo si utilizza per visualizzare l’anteprima di un video. Accertati anche di pubblicare manualmente il nuovo predefinito visualizzatore.

Vedi [Creare un predefinito per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) per creare un proprio predefinito visualizzatore video interattivo.

## Caricare un video e le relative risorse di miniatura associate {#uploading-a-video-and-its-associated-thumbnail-assets}

Se hai già caricato il video e le risorse miniature, procedi a [Aggiungi interattività al video](#adding-interactivity-to-your-video).

>[!NOTE]
>
>Il formato video MXF non è ancora supportato per l&#39;utilizzo con video interattivi in Dynamic Media.

Se hai caricato i video o le immagini errati o desideri eliminare i video o le immagini caricati di cui non hai più bisogno, consulta [Eliminare le risorse](/help/assets/manage-digital-assets.md#delete-assets).

Per caricare un video e le relative risorse di miniatura associate:

1. Carica il video e le relative miniature nella cartella o nelle cartelle desiderate.

   Vedi [Caricare le risorse](/help/assets/manage-digital-assets.md).
Vedi [Caricare risorse tramite la pianificazione dei processi FTP](/help/assets/manage-digital-assets.md).

   Aggiungi ora l’interattività al video.

## Aggiungi interattività al video {#adding-interactivity-to-your-video}

Puoi aggiungere segmenti della timeline a un video utilizzando l’editor visivo nella posizione nella pagina Crea video interattivo.

Dopo aver aggiunto i segmenti della timeline, aggiungi immagini in miniatura all’interno di ciascun segmento. Per ogni miniatura aggiunta, applichi un’azione ad essa. Ad esempio, puoi applicare una visualizzazione rapida alla miniatura, oppure assegnare un collegamento ipertestuale ad essa o un frammento esperienza.

Vedi [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media nei video interattivi non sono supportati quando si incorpora il visualizzatore in un frammento esperienza. È invece possibile utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.

>[!NOTE]
>
>Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.

Le opzioni Annulla e Ripristina, situate nell’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Dopo aver salvato il video interattivo, il video viene immediatamente aperto in Anteprima. Da qui, puoi selezionare un predefinito visualizzatore video interattivo e riprodurre il video per vedere una rappresentazione approssimativa di come appare ai clienti.

**Per aggiungere interattività al video:**

1. Nella vista Risorse, individua il video caricato e vuoi renderlo interattivo.
1. Effettua una delle operazioni seguenti:

   * Passa il puntatore sull&#39;immagine, quindi seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, seleziona **[!UICONTROL Modifica]**.

   * Passa il puntatore sull&#39;immagine, quindi seleziona **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica]**.

   * Per aprirlo nella pagina Vista dettagli, seleziona l’immagine. Sulla barra degli strumenti, seleziona **[!UICONTROL Modifica]**.

1. Nella pagina Crea video interattivo, effettua una delle seguenti operazioni:

   * Per iniziare a riprodurre il video, seleziona la **[!UICONTROL Play]** pulsante . Quando un particolare prodotto, servizio o dettaglio da evidenziare viene visualizzato, seleziona **[!UICONTROL Aggiungi segmento]** sulla barra degli strumenti. Ripetere l&#39;operazione fino a quando non si raggiunge la fine del video.

      Per ogni segmento di tempo aggiunto, puoi assegnare una o più immagini in miniatura. Puoi quindi collegare queste miniature alle pagine di prodotto Quickview che i clienti possono acquistare o alle pagine web per ulteriori informazioni.

   * Per iniziare a riprodurre il video, seleziona la **[!UICONTROL Play]** pulsante . Quando un particolare prodotto, servizio o dettaglio da evidenziare viene visualizzato, seleziona **[!UICONTROL Pausa]**. Seleziona **[!UICONTROL Aggiungi segmento]**.

      Continua a riprodurre e mettere in pausa il video nei punti della timeline in cui desideri aggiungere un segmento fino alla fine del video.

1. (Facoltativo) Trascina la barra **[!UICONTROL Cursore scala timeline]** da sinistra a destra per ingrandire o da sinistra per ridurre. Questa azione ti consente di controllare quanti dettagli vengono visualizzati dei segmenti aggiunti.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   A seconda della lunghezza del video, l’impostazione predefinita della Durata del segmento è la seguente:

   <table>
      <tbody>
        <tr>
        <td><strong>Se la lunghezza del video è...</strong></td>
        <td><strong>Per impostazione predefinita, l’impostazione Durata segmento è impostata su...</strong></td>
        </tr>
        <tr>
        <td>3 minuti o più</td>
        <td>60 secondi</td>
        </tr>
        <tr>
        <td>2-3 minuti</td>
        <td>30 secondi</td>
        </tr>
        <tr>
        <td>1-2 minuti</td>
        <td>20 secondi<br /> </td>
        </tr>
        <tr>
        <td>30-60 secondi</td>
        <td>10 secondi</td>
        </tr>
        <tr>
        <td>30 secondi o meno</td>
        <td>5 secondi</td>
        </tr>
      </tbody>
    </table>

   La timeline del video utilizza la stessa quantità di spazio disponibile sullo schermo. Di conseguenza, quando ridimensiona il browser, i segmenti aggiunti mantengono la larghezza corretta.

   Ad esempio, le tre schermate seguenti stanno utilizzando lo stesso video. La larghezza di ciascun segmento varia a seconda dell’impostazione Scala timeline.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Schermata A

   La schermata A precedente mostra la visualizzazione predefinita di un video prodotto di 29 secondi. La scala timeline è impostata sul valore predefinito di 5 secondi.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Schermata B

   Nella schermata B precedente, il cursore Scala timeline è stato trascinato dal valore predefinito di 5 secondi a 3 secondi. I singoli timestamp della scala timeline sono ora tutti impostati a intervalli di 3 secondi.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Schermata C

   Nella schermata C precedente, l&#39;impostazione Scala timeline è stata spostata a 8 secondi. I segmenti che contengono miniature di prodotto si sono ridotti. Questa funzione è utile se si dispone di un video lungo e si desidera visualizzare una panoramica di più segmenti che normalmente si adattano alla larghezza della pagina.

1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Per regolare l’ora di inizio e di fine di un segmento.

      Seleziona un segmento, quindi trascina l’ovale blu iniziale o finale per regolare rispettivamente l’ora di inizio e di fine. Il fotogramma video visualizzato si sposta al tempo appropriato nel video, in base alle tue regolazioni. Lo spostamento del segmento della timeline è limitato in base a eventuali segmenti adiacenti nella timeline. Il tempo minimo consentito per i segmenti è di un secondo.

      Utilizza le seguenti scelte rapide per la navigazione per controllare e ottimizzare rapidamente i segmenti video:

      * Per cercare il video direttamente all’inizio di quel segmento, selezionate l’ovale blu iniziale.
      * Per cercare il video direttamente alla fine di quel segmento, seleziona l’ovale blu finale.
      * Per ripristinare la riproduzione video all’inizio di quel segmento, seleziona l’intero segmento.

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Riposizionamento della fine di un segmento della timeline

   * Eliminazione di un segmento

      Seleziona l’ultimo segmento nella timeline, quindi nella barra degli strumenti seleziona **[!UICONTROL Elimina segmento]**. Se sono selezionati due o più segmenti, la funzione Elimina segmento è disabilitata.

      Puoi eliminare solo l’ultimo segmento. Ad esempio, se desideri eliminare tutti i segmenti dalla timeline, devi sempre selezionare l’ultimo, quindi selezionare **[!UICONTROL Elimina segmento]**.


1. Seleziona un segmento di tempo a cui associare una o più immagini in miniatura.
1. A destra del video, seleziona la **[!UICONTROL Contenuto]** scheda .
1. Nella scheda Contenuto , seleziona **[!UICONTROL Seleziona risorse]**, quindi sfoglia e seleziona tutte le risorse di immagine che desideri utilizzare con il video. Le risorse selezionate vengono aggiunte al pannello Selettore risorse della scheda Contenuto .

1. Nel selettore delle risorse sotto la scheda Contenuto, effettua una delle seguenti operazioni:

   <table>
      <tbody>
        <tr>
        <td>Per associare una miniatura al segmento della timeline selezionato</td>
        <td><p>Seleziona l’immagine nel pannello del selettore risorse a destra.</p> <p>Puoi aggiungere tutte le miniature desiderate in un segmento della timeline. Per ogni immagine selezionata, un segno di spunta compare sull’immagine nel selettore delle risorse.</p> </td>
        </tr>
        <tr>
        <td>Rimozione di una miniatura dal segmento della timeline selezionato</td>
        <td><p>Effettua una delle operazioni seguenti:</p>
          <ul>
          <li>Nel pannello del selettore delle risorse, seleziona un’immagine con un segno di spunta per deselezionarla. La risorsa immagine viene rimossa dal segmento della timeline.<br /> </li>
          <li>Nel segmento della timeline selezionato, seleziona un’immagine, quindi nella barra degli strumenti seleziona <strong>Elimina prodotto</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Selettore risorse](assets/chlimage_1-133.png)

   Quando si seleziona un’immagine nel pannello del selettore delle risorse, questa viene aggiunta al segmento della timeline selezionato.

1. Seleziona una singola miniatura all’interno di uno dei segmenti della timeline, quindi seleziona la **[!UICONTROL Azioni]** scheda .
1. Effettua una delle operazioni seguenti:
   <table> 
    <tbody> 
      <tr> 
      <td>Per associare l’immagine di miniatura selezionata a una visualizzazione rapida</td> 
      <td><p>In Tipo di azione, seleziona <strong>Quickview</strong>.</p> <p>Se sei un cliente Experience Manager Sites ed e-commerce:</p> 
       <ul> 
       <li>Il campo di testo Valore SKU è precompilato con lo SKU (Stock Keeping Unit) del prodotto selezionato. Lo SKU è un identificatore univoco per ogni prodotto o servizio distinto offerto. Questo campo viene popolato automaticamente quando l’immagine è associata a un prodotto in Experience Manager Commerce.</li> 
       <li>Se lo SKU prepopolato non è corretto, seleziona l’icona Selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto . Seleziona il prodotto da utilizzare, quindi seleziona il segno di spunta nell’angolo in alto a destra della pagina. Viene nuovamente visualizzato l’Editor video interattivo.</li> 
       </ul> <p> Se sei <em>not</em> un cliente Experience Manager Sites o Ecommerce</p> 
       <ul> 
       <li>Vedi <a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identificazione delle variabili dei punti attivi</a>. Queste variabili devono essere definite.</li> 
       <li>Per impostazione predefinita, questo campo SKU utilizza il nome file della risorsa immagine senza estensione. Se segui una convenzione di denominazione standard per i file basati su SKU, in genere questo campo non richiede alcuna modifica aggiuntiva. </li> 
       <li>In caso contrario, modifica il valore predefinito e inserisci il valore SKU corretto. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU inserito popola automaticamente la parte variabile del modello Quickview in modo che il sistema sappia associare l'immagine selezionata a una particolare visualizzazione rapida SKU.</li> 
       </ul> <p>(Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili da utilizzare per identificare ulteriormente un prodotto, seleziona <strong>Aggiungi variabile generica</strong>. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio: <code>category=Womens</code> è una variabile aggiunta.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Per associare l’immagine di miniatura selezionata a un collegamento ipertestuale</td> 
      <td><p>In Tipo di azione, seleziona <strong>Collegamento ipertestuale</strong>, quindi effettua una delle seguenti operazioni:</p> 
       <ul> 
       <li>Se sei un cliente Experience Manager Sites, seleziona l’icona Selettore sito (cartella) per passare a una pagina web. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.</li> 
       <li>Se si è un cliente Dynamic Media autonomo, nel campo di testo HREF specificare il percorso completo dell'URL di una pagina Web collegata.</li> 
       </ul> <p>Assicurati di specificare se aprire il collegamento in una nuova scheda del browser o nella scheda corrente.</p> </td> 
      </tr> 
      <tr> 
      <td>Per associare l’immagine in miniatura selezionata a un frammento esperienza</td> 
      <td><p>In Tipo di azione, seleziona <strong>Frammento esperienza</strong>, quindi procedi come segue:<p> 
       <ul> 
       <li>Se sei un cliente Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza . Seleziona il frammento esperienza da utilizzare, quindi seleziona <strong>Per tornare al pannello Azioni della pagina precedente, seleziona </strong>nell’angolo superiore destro della pagina.<br /> Vedi <a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">Frammenti esperienza</a>.</li> 
      </ul> 
       <ul> 
       <li>Specifica la larghezza e l’altezza del frammento esperienza così come viene visualizzato sul video.</li>
       </ul><strong>Nota</strong>: Gli strumenti di condivisione social media in Video interattivo non sono supportati quando si incorpora il visualizzatore in un frammento esperienza. È invece possibile utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.</p></tr>&lt; 
      <tr> 
      <td>Per modificare un’azione già assegnata a un’immagine miniatura</td> 
      <td>All’interno di un segmento della timeline, seleziona una miniatura con un collegamento a catena a destra dell’etichetta di testo. Il collegamento a catena indica che è stata assegnata un’azione. Per apportare le modifiche, seleziona la <strong>Azioni</strong> scheda .</td> 
      </tr> 
      <tr> 
      <td>Per modificare l’etichetta di testo di un’immagine miniatura</td> 
      <td><p>Per impostazione predefinita, l’etichetta di testo utilizza l’immagine della miniatura <code>Title</code> campo metadati. Se <code>Title</code> non è presente, viene invece utilizzato il nome del file dell'immagine miniatura, ma senza l'estensione .</p> <p>Per modificare l’etichetta di testo di un’immagine miniatura, sotto la sezione <strong>Azioni </strong>Inserisci il testo desiderato direttamente sotto la risorsa immagine visualizzata. Vedi l'immagine seguente.</p> <p>La nuova etichetta di testo viene utilizzata solo dal lettore video stesso e il testo in miniatura visualizzato nel segmento della timeline. La modifica dell’etichetta non influisce sul campo dei metadati Titolo dell’immagine miniatura né sul relativo nome file.</p> </td> 
      </tr> 
      <tr> 
      <td>Ripristino di una modifica</td> 
      <td>Nell’angolo in alto a destra della pagina, seleziona <strong>Annulla</strong> o <strong>Ripeti</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   All’immagine miniatura viene aggiunta una nuova etichetta di testo.

1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 6-11 per aggiungere altre immagini in miniatura ai segmenti della timeline nel video.
   * Procedi al passaggio facoltativo 13.

1. (Facoltativo) Effettua una delle seguenti operazioni:

   * **[!UICONTROL Unisci segmento]** - Puoi combinare due segmenti adiacenti (con o senza l’assegnazione di miniature di prodotto) in un unico segmento.

      Nella timeline, seleziona due o più segmenti contigui da unire in uno. Nell’immagine seguente non sono presenti maniglie di trascinamento ovali blu sui due segmenti selezionati.

      Seleziona **[!UICONTROL Unisci segmento]** sulla barra degli strumenti.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Unione di due segmenti selezionati di cinque secondi in un segmento di dieci secondi.

   * **[!UICONTROL Segmento diviso]** - Puoi dividere un singolo segmento in due segmenti con tempo uguale. Se al segmento sono già assegnate miniature di prodotto, queste vengono combinate nel segmento a sinistra.

      Nella timeline, seleziona un segmento da dividere in due, quindi seleziona **[!UICONTROL Segmento diviso]** sulla barra degli strumenti.

      Selezionando due o più segmenti, disattiva la **[!UICONTROL Segmento diviso]** funzionalità.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   Suddivisione di un segmento selezionato di dieci secondi in due segmenti di cinque secondi ciascuno.

1. Vicino all&#39;angolo superiore destro del **[!UICONTROL Crea video interattivo]** viene visualizzato il nome del predefinito visualizzatore attualmente selezionato utilizzato con il video. Per selezionare un predefinito visualizzatore diverso, seleziona il nome.

   Ad esempio, il `Shoppable_Video_light` il predefinito per visualizzatori consente di riprodurre il video con un’area di visualizzazione bianca accanto al video. L&#39;area di visualizzazione è quella in cui vengono visualizzate le miniature selezionabili durante la riproduzione. La `Shoppable_Video_dark` il predefinito per visualizzatori consente di riprodurre il video con un’area di visualizzazione nera accanto al video.

   Se hai creato il tuo predefinito per visualizzatori video interattivi, puoi visualizzarlo nell’elenco dei predefiniti tra i quali puoi scegliere.

   Al termine, seleziona **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Quando salvi il video interattivo, con esso viene salvato automaticamente un file associato `.vtt`. La `.vtt` viene salvato nel `_VTT` nella directory principale di **[!UICONTROL Risorse]**. Il file e la cartella sono necessari affinché il video interattivo possa essere riprodotto correttamente sul sito web. Non spostare, modificare o eliminare la cartella `_VTT` o il relativo contenuto.

1. Pubblica il video interattivo. La pubblicazione crea il codice di incorporamento o l’URL da copiare e incollare nelle esperienze del sito web.

   Se hai aggiunto interattività con le visualizzazioni rapide, utilizza solo il codice di incorporamento; se hai aggiunto l’interattività con le pagine web con collegamenti ipertestuali, puoi anche utilizzare l’URL pubblicato. Tuttavia, il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con pagine Experience Manager Sites.

   Vedi [Pubblicare le risorse](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   >
   >Per pubblicare un video acquistabile con visualizzazioni rapide, accertati anche di pubblicare separatamente dall’area di e-commerce ciascuna delle risorse immagine correlate al video.

   Dopo aver aggiunto i segmenti della timeline e pubblicato il video interattivo, puoi aggiungerlo alla pagina di destinazione del sito web esistente. Vedi [Integrare un video interattivo con il sito web](#integrating-an-interactive-video-with-your-website).

## Pubblicare risorse video interattive {#publishing-interactive-video-assets}

Vedi [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare le risorse video interattive.

## Integrare un video interattivo con il sito web {#integrating-an-interactive-video-with-your-website}

Dopo aver caricato un video, aggiunto dei segmenti della timeline e pubblicato il video interattivo, puoi aggiungerlo al sito web esistente.

Se sei un cliente di Experience Manager Sites, puoi aggiungere il video interattivo trascinando il componente File multimediali interattivi nella pagina. Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Se sei un cliente Experience Manager Assets indipendente, puoi aggiungere manualmente il video interattivo al tuo sito web come descritto in questa sezione.

1. Copia il codice di incorporamento o l’URL del video interattivo pubblicato.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md).
Se hai aggiunto interattività con le visualizzazioni rapide, utilizza solo il codice di incorporamento; se hai aggiunto l’interattività con le pagine web con collegamenti ipertestuali, puoi anche utilizzare l’URL pubblicato. Tuttavia, il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con pagine Experience Manager Sites.

1. Nel codice della pagina web del target, identifica dove si trova il video statico.
1. Rimuovi il video statico e sostituisci il codice con il codice di incorporamento o l’URL copiato da Experience Manager Assets, così come è.
Il codice da incorporare copiato è impostato per un ambiente reattivo in modo che si adatti automaticamente all’area precedentemente occupata dal video statico.

>[!NOTE]
>
>A questo punto, se hai aggiunto l’interattività solo con pagine web collegate ipertestuale, puoi farlo.
>
>Tuttavia, se hai aggiunto interattività per attivare una visualizzazione rapida, le miniature accanto al video interattivo sono solo a scopo di visualizzazione; non sono ancora integrati con le visualizzazioni rapide esistenti. In tal caso, è necessario integrare il video interattivo con le visualizzazioni rapide esistenti sul sito web.

**Esempio**

Utilizzo del sito web demo come esempio:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Il codice di incorporamento video è standard:

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

L&#39;integrazione è semplice come rimuovere il codice di incorporamento video e sostituirlo con il codice di incorporamento video interattivo da Experience Manager. Puoi vedere il risultato al seguente URL. Mentre mostra un video interattivo presente sulla pagina, non è ancora integrato con le visualizzazioni rapide esistenti:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## Integrare un video interattivo con una Quickview esistente {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
>
>Questa attività si applica solo se sei un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo consiste nell’integrare il video interattivo con un’implementazione Quickview esistente utilizzata sul sito web. Non esiste una soluzione all’integrazione che funzioni per tutti i casi. Ogni implementazione di Quickview è univoca. Di conseguenza, è necessario un approccio specifico che implichi l&#39;assistenza di una persona IT front-end.

L&#39;implementazione di Quickview esistente rappresenta normalmente una catena di azioni correlate che avvengono sulla pagina web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta AJAX utilizzando l’URL ottenuto al passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto di Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo, quando un utente seleziona una miniatura all’interno del video interattivo, il visualizzatore gestisce l’interazione dell’utente sostituendo il passaggio 1 e in parte il passaggio 2. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati delle miniature precedentemente aggiunti all’Experience Manager.

In un tale gestore di eventi, il codice front-end effettua le seguenti operazioni:

* Ascolta un evento emesso dal video interattivo.
* Crea un URL Quickview basato sui dati delle miniature.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Inoltre, il visualizzatore video interattivo supporta la modalità di funzionamento a schermo intero. L’utente finale attiva le visualizzazioni rapide selezionando una miniatura senza uscire dalla schermata completa. Per ottenere questa funzionalità, devi modificare il codice front-end in modo che la finestra di dialogo modale Quickview sia collegata al contenitore del visualizzatore. Non aggiungere il BODY del documento o altri elementi di pagina web non disponibili quando il visualizzatore è in modalità a schermo intero. Il codice che esegue questo lavoro ascolta un altro callback del visualizzatore inviato dopo il caricamento del visualizzatore sulla pagina.

Il codice di incorporamento restituito da Experience Manager dispone già di un gestore eventi ready-to-use. Viene commentato come visto nel seguente frammento di codice evidenziato:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

Pertanto, è solo necessario rimuovere il commento dallo snippet di codice evidenziato sopra e sostituire il corpo dei gestori fittizi con codice specifico per la particolare pagina web.

Nel codice di incorporamento standard sono presenti due gestori di callback predefiniti: `quickViewActivate` e `initComplete`. La `quickViewActivate` viene attivato quando una miniatura viene selezionata nel visualizzatore. Utilizzalo per integrare il visualizzatore con la logica di attivazione Quickview. La `initComplete` Il gestore viene attivato solo una volta quando il visualizzatore viene caricato nella pagina. Questo gestore viene utilizzato per regolare la posizione della finestra di dialogo Quickview nel DOM della pagina Web.

Il processo di costruzione dell’URL di visualizzazione rapida è opposto al processo di identificazione delle variabili di miniatura descritte in precedenza in questo argomento. Utilizzando gli esempi di URL Quickview precedentemente identificati, puoi vedere come viene costruito l’URL Quickview in ogni caso:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>SKU singolo, trovato nel percorso URL</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

L&#39;ultimo passaggio per attivare l&#39;URL Quickview e attivare il pannello Quickview richiede molto probabilmente l&#39;assistenza di un esperto IT front-end del reparto IT. Hanno la conoscenza di sapere come attivare con precisione l&#39;implementazione di Quickview dal passaggio appropriato, avendo un URL di Quickview pronto all&#39;uso.

Puoi vedere come questi passaggi vengono applicati al sito web dimostrativo per integrare completamente un video interattivo con il codice Quickview. In precedenza, in questo argomento, la struttura dell’URL di visualizzazione rapida era identificata come segue:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

È facile ricostruire questo URL all’interno del `quickViewActivate` handler che utilizza `categoryId` e `sku` campi disponibili nel `inData` oggetto passato al gestore tramite il codice del visualizzatore, come illustrato di seguito:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo sta attivando la finestra di dialogo Quickview utilizzando un semplice `loadQuickView()` chiamata della funzione. Questa funzione accetta un solo argomento, ovvero l’URL dei dati Quickview. Quindi l&#39;ultimo passo per integrare il video interattivo è quello di aggiungere la seguente riga di codice al `quickViewActivate` handler:

```xml
loadQuickView(quickViewUrl);
```

Infine, accertati che la finestra di dialogo Quickview sia associata all’elemento contenitore del visualizzatore. Il codice di incorporamento predefinito fornisce alcuni passaggi di esempio per ottenere questa funzionalità. Per ottenere un riferimento all’elemento contenitore del visualizzatore, puoi utilizzare le seguenti righe di codice:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Dove `inner_container` è un riferimento a un `DIV` gestito dal visualizzatore. La finestra di dialogo deve essere un elemento secondario di tale `DIV`.

I passaggi per individuare effettivamente l’elemento della finestra di dialogo modale e allegarlo al contenitore di cui sopra sono specifici per casi specifici. Anche in questo caso, puoi chiedere aiuto allo sviluppatore front-end che abbia familiarità con l’implementazione Quickview necessaria.

Per il sito Web di esempio, la finestra di dialogo modale Quickview viene implementata come `DIV` con l’ID quickview-modale collegato direttamente al documento `BODY`. Pertanto, il codice per spostare tale finestra di dialogo nel contenitore del visualizzatore è altrettanto semplice:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

Il codice sorgente completo è il seguente:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

Il sito web demo finale con il video interattivo completamente integrato viene visualizzato come segue:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## Crea Windows® a comparsa personalizzato utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedi [Crea Windows® a comparsa personalizzato utilizzando Quickview](/help/assets/dynamic-media/custom-pop-ups.md). —>
