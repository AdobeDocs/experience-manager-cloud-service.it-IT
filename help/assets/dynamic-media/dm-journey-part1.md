---
title: percorso Dynamic Media, parte I
description: Il Percorso Dynamic Media illustra le nozioni di base di Dynamic Media, il suo funzionamento, le sue funzioni e il suo valore per il tuo lavoro e per i tuoi clienti.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: aea668753222e981a7f2c8bd71bc6c790aa32a15
workflow-type: tm+mt
source-wordcount: '3710'
ht-degree: 1%

---

# percorso Dynamic Media: Nozioni di base, parte I {#dm-journey-part1}

Benvenuto nel Percorso Dynamic Media.

Questo percorso illustra le nozioni di base di Dynamic Media, il suo funzionamento, le sue funzioni e il suo valore per il tuo lavoro e per i tuoi clienti.

**_Prerequisiti_**

* Informazioni di base sui formati immagine e video
* Comprensione di base di HTML e CSS
* Nozioni di base sugli strumenti di progettazione come Adobe Illustrator, Adobe Photoshop, Adobe XD
* L’accesso a Dynamic Media all’Experience Manager è utile, ma non obbligatorio

**_Cosa ti aspetti di imparare_**

_Parte I_

* Cos’è Dynamic Media e come può aiutarti?
* Casi di utilizzo per Dynamic Media
* Flusso di una risorsa attraverso il sistema Dynamic Media

_Parte II_

* Anatomia di un URL Dynamic Media e modalità di distribuzione dei contenuti da parte di Dynamic Media
* Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse
* Set di immagini, set 360 gradi e set di file multimediali diversi

**_Pubblico_**
Il pubblico più adatto ai lettori di questo percorso sono i seguenti, nuovi utenti di Dynamic Media all&#39;Experience Manager:

* Administrator
* Analista aziendale
* Architetto dei contenuti
* Autore del contenuto
* Designer
* Sviluppatore
* Marketing
* Responsabile/Proprietario del prodotto

>[!TIP]
>
>Per ottenere risultati ottimali, Adobe consiglia di leggere e visualizzare questo Percorso Dynamic Media su un computer desktop.

## Cos’è Dynamic Media e come può aiutarti? {#dm-journey-a}

Dynamic Media ti consente di fornire su richiesta risorse visive di marketing e merchandising. Consente inoltre di creare e distribuire esperienze di visualizzazione interattive, tra cui zoom, rotazione a 360 gradi e video. Le risorse vengono ridimensionate in modo dinamico per essere utilizzate su siti web, mobili e social. Utilizzando un set di risorse di origine primaria (come immagini, video e 3D), Dynamic Media genera e distribuisce più varianti di questi contenuti avanzati in tempo reale tramite la rete CDN (Content Delivery Network) globale, scalabile e ottimizzata per le prestazioni.

Dynamic Media integra i flussi di lavoro della soluzione di gestione delle risorse digitali Adobe Experience Manager Assets per semplificare e semplificare il processo di gestione delle campagne digitali.

### Un file con infinite possibilità

Uno dei punti principali da comprendere su Dynamic Media è il concetto di _Un file di risorse principali con infinite possibilità_.

Per comprendere meglio questo concetto, pensa al modo in cui tradizionalmente si lavora con una singola risorsa, ad esempio un’immagine o un video. In genere viene creata una risorsa principale. Poi, crei manualmente versioni della stessa risorsa per ogni esperienza, ogni dispositivo necessario, ogni pagina web e ogni proprietà in cui viene utilizzato. Con il tempo, tale singola risorsa può crescere fino a 20, 30 o più versioni, senza alcuna cronologia delle versioni ad esse associata. Immaginate di farlo per ogni immagine o video che avete. Il numero di versioni delle risorse diventerebbe rapidamente eccessivo per la manutenzione e l&#39;aggiornamento, per non parlare dell&#39;aumento dei costi di storage.

Dynamic Media, tuttavia, è fondamentalmente diverso dagli altri sistemi perché lo si utilizza per distribuire i contenuti multimediali _dinamicamente_ da risorse singole primarie e da chiamate URL. I percorsi URL di Dynamic Media richiesti includono istruzioni che spiegano al server di pubblicazione di Adobe come visualizzare la risorsa quando viene consegnata alla schermata di un cliente. Ad esempio, utilizzando la stessa singola risorsa primaria, è possibile che venga distribuita istantaneamente in rappresentazioni illimitate, modificando dimensioni, formato, risoluzione, peso, colore, ritaglio ed effetti come la visualizzazione zoom.

Questo metodo di consegna esclusivo assicura che le esperienze di qualità vengano inviate a qualsiasi schermo, indipendentemente dalle dimensioni o dalla larghezza di banda. I video full-size sono ottimizzati anche per tutti i tipi di schermo e trasmessi in streaming adattivo per garantire un&#39;esperienza utente coerente e di qualità.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media offre la stessa immagine primaria a diversi supporti in diverse dimensioni e formati.](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media garantisce esperienze di qualità e coerenza a qualsiasi schermo, indipendentemente dalle dimensioni o dalla larghezza di banda._

Continuando a leggere, imparerai perché questo concetto di &quot;un file di risorsa principale, infinite possibilità&quot; è importante.

### La rete di distribuzione dei contenuti

Quando sei pronto per essere live con una risorsa immagine o video, è supportato dalla spina dorsale di Dynamic Media costituita da una potente rete di distribuzione di livello superiore. La rete serve centinaia di clienti in tutto il mondo ogni giorno. Le risorse vengono distribuite sulla rete di distribuzione dei contenuti (o CDN) ospitata da Akamai. La rete CDN è un sistema di servizi informatici collegati in rete che cooperano in modo trasparente per fornire agli utenti finali contenuti, in particolare contenuti rich media di grandi dimensioni.

Nel sistema CDN, il contenuto web viene memorizzato in cache web su Internet. Poi viene consegnato dalla cache web agli utenti finali per rendere la consegna più veloce. Quindi, la prima volta che un utente scarica una pagina web, le risorse che vede vengono consegnate a una cache CDN. Vengono memorizzati sul server in modo che la prossima volta che un utente nella stessa area accede alla pagina web, lo stesso contenuto della cache viene consegnato più velocemente. Il contenuto viene distribuito più rapidamente perché si trova più vicino all’utente finale. Una rete CDN fornisce display di pagine web più veloci, ma riduce le richieste di larghezza di banda sul server centrale perché il contenuto viene distribuito da una rete di cache, non da un server centrale in ogni istanza. Questo flusso ottimizzato significa una migliore esperienza utente, che porta ad un aumento delle vendite.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Storicamente, la rete CDN fornisce 3,5 petabyte di traffico ai clienti, ogni mese. Il sistema può fornire 52 miliardi di asset in un solo giorno. Tale numero equivale a 864.000 immagini e video consegnati con successo ai clienti, _ogni secondo_.

### Imaging avanzato

Dynamic Media ottimizza già le risorse e garantisce che ogni risorsa venga caricata rapidamente sui sistemi mobili e desktop tramite la rete CDN. Per ottenere questo risultato, in Dynamic Media vengono utilizzati i predefiniti per immagini per definire la qualità dell’immagine. Definiscono anche il tipo di immagine che stai inviando, la relativa nitidezza e altri pezzi per varie parti delle tue esperienze o pagine.

Ma per aggiungere ulteriore valore a Dynamic Media oltre ai predefiniti per immagini, esiste _Imaging avanzato_.

La funzione Smart imaging fornisce prestazioni ancora migliori nella distribuzione delle risorse di immagini ottimizzando automaticamente il formato e le dimensioni dei file di un&#39;immagine in base alla funzionalità del browser del cliente. Funziona con i predefiniti per immagini esistenti (i predefiniti per immagini sono descritti nella parte II di questo percorso) e utilizza l’intelligenza durante la distribuzione.

Questa intelligenza riduce ulteriormente le dimensioni dei file immagine in base al browser e alla velocità di connessione di rete. Poiché le risorse immagine rappresentano la maggior parte del tempo di caricamento di una pagina, il miglioramento delle prestazioni può avere un impatto approfondito su indicatori aziendali chiave, come:

* Conversione più elevata
* Tempo trascorso sul sito
* Frequenza rimbalzo sito inferiore

Nel complesso, grazie all&#39;imaging intelligente, le prestazioni variano dal 22% al 47% a seconda delle impostazioni di preimpostazione dell&#39;immagine e delle caratteristiche specifiche dell&#39;utente finale. Mantenendo al contempo la qualità delle immagini come se non fosse mai stata toccata.

![Imaging avanzato](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_La funzione Smart imaging ottimizza automaticamente il formato e le dimensioni del file dell&#39;immagine in base alla capacità del browser e alla velocità di rete del cliente._

Per impostazione predefinita, la funzione Smart imaging non è attivata perché richiede uno sforzo coordinato tra l’utente e il supporto tecnico Adobe Dynamic Media. Inoltre, l&#39;abilitazione di Smart imaging richiede una cancellazione completa della cache CDN, che viene poi riempita di tempo. Se sei interessato a utilizzare Smart imaging, puoi lavorare con Adobe per attivarlo inviando un ticket di assistenza tecnica. Il supporto tecnico fornisce quindi un parametro URL che consente di provare in anticipo l’imaging intelligente. Puoi provarlo su qualsiasi pagina web o immagine in modo da vedere le prestazioni che ottieni e i risparmi. È quindi possibile attivare l&#39;imaging intelligente per il sito completo.

### Set video adattivi

In presenza di un video su una pagina o su una pagina principale, i clienti tendono a interagire con tale contenuto più a lungo e a rimanere sulla pagina più a lungo, il che è tipicamente positivo. Questo comportamento è stato esposto attraverso le analisi che Adobe ha fatto. Tuttavia, i video possono essere complessi. Per una cosa, spesso si ha un file primario di grandi dimensioni. È complicato determinare le dimensioni e la distribuzione dei video, il tutto per garantire che l&#39;esperienza funzioni senza problemi indipendentemente dal dispositivo su cui viene visualizzata e dalla larghezza di banda.

Per risolvere questo problema, Dynamic Media consente di creare _Set video adattivi_.

![Set video adattivo](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Un Adaptive Video Set raggruppa le versioni dello stesso video codificate con diversi bit rate e formati._

Si inizia con il video originale principale, che si carica nel sistema. Dynamic Media ridimensiona automaticamente, oppure _transcodifica_, questo video in più video. Quindi, al momento della distribuzione, determina in modo intelligente quale schermo video, quale qualità e quale formato utilizzare, e lo consegna al telefono, tablet o computer desktop.

Ad esempio, su un dispositivo mobile iOS, rileva una larghezza di banda come 4G, 5G o Wi-Fi. Quindi, seleziona automaticamente il video codificato a destra tra i vari bit rate video all&#39;interno del set video adattivo. Il video viene inviato in streaming a dispositivi mobili, tablet o computer desktop.

Inoltre, la qualità video viene commutata in modo dinamico automaticamente in caso di cambiamento delle condizioni della rete. Inoltre, se un cliente entra in modalità a schermo intero su un desktop, il set video adattivo risponde utilizzando una risoluzione migliore, migliorando l’esperienza di visualizzazione del cliente.

L&#39;utilizzo di Adaptive Video Sets fornisce una riproduzione fluida e di alta qualità per i clienti che riproducono video Dynamic Media su schermi e dispositivi multipli. Toglie davvero la complessità dal video.

## Casi di utilizzo per Dynamic Media {#dm-journey-b}

Di seguito sono riportati i problemi e le soluzioni comuni per i casi d’uso con cui Dynamic Media può aiutarti a incrementare il coinvolgimento positivo dei clienti, la fidelizzazione, la conversione e il ROI.

### Caso di utilizzo: Approccio principale dei file

Uno dei casi d’uso più importanti per Dynamic Media è anche uno dei più ovvi. In altre parole, riducendo il peso delle pagine e delle esperienze e la dimensione del contenuto, che si tratti di un&#39;immagine o di un video, che viene distribuito.

Di seguito viene illustrata un’esperienza o una pagina web tipica. Circa il 90% di una pagina è costituito da contenuti multimediali avanzati, come immagini e video, che sono solitamente file molto più pesanti.

![Spessore pagina contenuto](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Peso della pagina del contenuto di una tipica pagina web._

Il restante 10% è costituito da HTML, codice CSS e tag specifici. Vuoi ottimizzare il peso del 90% di quella pagina e Dynamic Media ti aiuta a farlo. In precedenza, avete letto del concetto di _un file di risorse principali con infinite possibilità_. Questo approccio è significativo per ridurre il peso complessivo della pagina. La possibilità di prendere una risorsa principale e utilizzarla in una pagina di dettaglio del prodotto, una pagina in miniatura, il carrello e la griglia di ricerca è un ottimo risparmio di tempo. E garantisce coerenza anche tra le esperienze.

![Approccio principale dei file](/help/assets/dynamic-media/assets/dm-onefile.png)
_L’orologio è un file risorsa principale, ma con più rappresentazioni di esso, non copie, create al volo._

Esaminiamo più da vicino i problemi che Dynamic Media sta risolvendo con l&#39;unico file e alcune delle soluzioni a tale approccio.

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Crea e archivia ogni risorsa. | Utilizza un singolo file di immagine, creando automaticamente le rappresentazioni richieste solo al momento della consegna. |
| Costi elevati di storage. | Elimina la necessità di creare e memorizzare più copie di una risorsa. |
| Difficoltà a mantenere la catena di custodia. | Garantisce la distribuzione di esperienze coerenti e ottimizzate per i dispositivi. |
| Nessuna cronologia delle versioni. |  |
| Esperienze di marchio incoerenti tra i dispositivi. |  |
| Costo non necessario per la creazione di risorse duplicate. |  |

Quando pensi a un file, stai creando una risorsa per ogni tipo di esperienza. Si potrebbe avere un&#39;immagine di partenza, e poi si devono creare 20, 30 o 40 varianti di quell&#39;immagine, che alla fine è necessario archiviare e pagare per la memorizzazione.

Quindi devi accertarti che l&#39;immagine corretta sia utilizzata e che ciò possa influire sulla tua capacità di avere coerenza tra i tuoi marchi. Inoltre, se non riesci a trovare un&#39;immagine, devi tornare indietro e duplicare quelle risorse.

Dynamic Media consente di creare al volo varianti di immagini provenienti da quell’immagine iniziale. Ti consente di essere creativo con quella risorsa primaria e di non dover andare avanti e indietro con il tuo graphic design artista o studio fotografico per creare contenuti aggiuntivi. Ed è denaro e tempo risparmiati.

Con l’approccio a un file, si utilizza un singolo file primario. Quindi crea le versioni o le rappresentazioni necessarie nei tuoi siti, proprietà ed esperienze, solo nel momento in cui vengono consegnate o visualizzate da un cliente. Tale efficienza può ridurre notevolmente la quantità di storage necessaria per le risorse e la complessità complessiva del flusso di lavoro. Inoltre, grazie al sistema di distribuzione di Dynamic Media, è possibile ottimizzare tutte le immagini e i video, caricarli rapidamente e ottimizzare l&#39;aspetto su tutti gli schermi e i dispositivi.

### Caso di utilizzo: Video

Un altro caso d’uso che Dynamic Media risolve per è il video. Il video è complesso. È difficile da gestire. I file video sono difficili da archiviare e spostarsi a causa delle loro dimensioni intrinseche di file.

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Difficile gestire e distribuire video ottimizzati per vari dispositivi. | Utilizza un singolo video che si ridimensiona automaticamente per tutti i dispositivi. |
| I video si bloccano o riproducono in bassa qualità a causa della larghezza di banda disponibile per l&#39;utente finale. | Fornire video attraverso un lettore HTML che rileva automaticamente la larghezza di banda disponibile e adatta la qualità per garantire alta fedeltà e una riproduzione fluida. |
| La creazione manuale di tutte le versioni di un video non è fattibile e richiede molto tempo per garantire una corretta visualizzazione e riproduzione su dispositivi diversi. | Elimina le ore di lavoro di transcodifica tediosa con un flusso di lavoro semplificato. |
|  | Libera il tempo per un lavoro di maggior valore. |

I clienti arrivano a Dynamic Media con il seguente problema che sperano di risolvere:

&quot;_Abbiamo il video e abbiamo speso molti soldi per crearlo. Ma abbiamo evitato di posizionarlo sulle pagine, o di consegnarlo, perché dai nostri test, non possiamo davvero garantire la qualità del video, o se lo farà davvero. E alla fine, questo influisce sui nostri marchi e potenzialmente sul nostro ruolo anche nella conversione._&quot;

La soluzione di Dynamic Media è quella di prendere quel file video principale e lasciare che Dynamic Media faccia tutte le dimensioni attraverso il suo processo di transcodifica. Poi, associalo al lettore video intelligente di Dynamic Media. Questo flusso di lavoro garantisce che l’utilizzo di quel video sulla pagina di destinazione principale, o su una pagina di dettaglio di una categoria o di un prodotto, sia coerente e fornito con un’elevata qualità.

Di seguito sono riportati altri casi d’uso da considerare.

### Caso di utilizzo: Unica fonte di verità

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Le risorse digitali sono sparse nell’organizzazione, archiviate in team o unità aziendali diversi. | Archivia e gestisci tutte le risorse digitali in una posizione centrale. |
| I membri del team scaricano e creano versioni locali. | I membri del team utilizzano un singolo file primario per creare _e_ fornire tutte le versioni necessarie su vari schermi e dispositivi. |
| Risorse monouso create per ogni esperienza e dispositivo. | Elimina le risorse a uso singolo, risparmiando tempo e denaro per crearle. |

### Caso di utilizzo: Ritaglio avanzato basato sull’intelligenza artificiale per contenuti multimediali avanzati

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Disegnare, misurare e tagliare manualmente immagini o video in modo da evidenziare il punto focale e visualizzarli in modo appropriato su tutti gli schermi e i dispositivi richiede molto tempo e molta manodopera. | Utilizza Smart Crop in Dynamic Media, una funzionalità di Adobe Sensei AI, per rilevare automaticamente il punto focale in qualsiasi immagine o video e ritagliarlo per mantenerlo. |
| Il tempo perso che potrebbe essere meglio impiegato nella creazione di esperienze ad alto impatto. | Acquisisce il punto di interesse desiderato indipendentemente dalle dimensioni dello schermo. |
| Risorse monouso create per ogni esperienza e dispositivo. | Elimina le noiose attività manuali e offre immagini e video di alta qualità e a caricamento rapido che risultano perfetti su qualsiasi dispositivo o schermo. |

### Caso di utilizzo: Authoring di contenuti multimediali interattivi

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Esperienze cliente semplici e statiche che non coinvolgono, generano fidelizzazione o guidano la conversione. | Consente agli utenti non tecnici di aggiungere facilmente e senza problemi elementi interattivi quali punti critici, caroselli e set 360 gradi per esperienze più dinamiche e coinvolgenti. |
| Ritorno limitato sugli investimenti provenienti da risorse digitali e esperienze cliente lente. | Conversione e ritorno dell&#39;investimento grazie alle esperienze multimediali. |

## Flusso di una risorsa attraverso il sistema Dynamic Media {#dm-journey-c}

Di seguito viene illustrato un flusso di lavoro tipico per Dynamic Media.

![Flusso di lavoro Dynamic Media](/help/assets/dynamic-media/assets/dm-workflow.png)
_Flusso di una risorsa attraverso il sistema Dynamic Media._

Inizia con la fase di creazione con l’obiettivo principale di avere la risorsa principale alla fine. Queste risorse primarie potrebbero provenire da riprese di foto, da fornitori di video, o potrebbero essere alcuni file audio che hai creato. Puoi utilizzare applicazioni Adobe Creative Suite come Adobe InDesign, Adobe Photoshop, Adobe Illustrator per elaborare i contenuti.

Al termine della creazione, inserisci la risorsa nella soluzione Authoring caricandola in Dynamic Media. All’interno di Dynamic Media, assicurati di disporre dei predefiniti per immagini e dei visualizzatori giusti in linea per le varie pagine web del tuo sito.

Infine, è possibile ottimizzare tutti i contenuti e pubblicarli sui server Dynamic Media in modo che siano disponibili per web, stampa, e-mail, desktop e dispositivi mobili.

### Caricamento delle risorse in Dynamic Media

Al termine della creazione di una risorsa primaria, caricala in Dynamic Media. Il tipo di file caricato, il formato e le dimensioni del file sono attributi importanti per Dynamic Media. Al momento del caricamento, assicurati di ottenere il valore massimo dal supporto di un file.

Ad esempio, l’immagine dell’orologio seguente è 4560 x 3020 pixel. E anche se non si può mai utilizzare un&#39;immagine di quelle dimensioni, è comunque possibile caricarla. Più grande è l&#39;immagine, migliore è la qualità che Dynamic Media può offrire, anche fino a una rappresentazione in miniatura. Ricorda: è possibile _diminuzione_ la risoluzione di un&#39;immagine esistente. Ma se provi a _aumentare_ la risoluzione di un&#39;immagine, il risultato, probabilmente, sarà insoddisfacente.

![Formati consigliati da caricare in Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Considerazioni sul caricamento delle risorse._

Adobe consiglia di caricare le risorse in un formato senza perdita di dati. In genere, è meglio evitare JPEG perché, quando si distribuisce JPEG o se si continua a salvare JPEG, la qualità dell’immagine si perde nel tempo. Si desidera iniziare con le immagini con la risoluzione più elevata in un formato senza perdita di dati. Tale formato è in genere un file TIFF o PNG.

Per quanto riguarda lo spazio colore, quando si pensa a un canale digitale o a una visualizzazione web, in genere si pensa a RGB (Rosso, Verde, Blu).

La maggior parte non penserebbe mai di consegnare qualcosa in CMYK o perché potresti voler consegnare in CMYK. Il motivo è che lo spazio colore viene utilizzato più spesso per la consegna di articoli stampati. Ma Dynamic Media può offrire in entrambi gli spazi di colore.

Ci sono molti clienti che ancora fanno la stampa, come i club all&#39;ingrosso del magazzino. E ci sono negozi di alimentari che spesso stampano volantini su base settimanale. Tali clienti richiedono che le loro immagini siano in entrambi gli spazi colore. Tradizionalmente, questo richiederebbe due immagini diverse: uno in RGB e uno in CMYK. Tuttavia, puoi caricare le risorse CMYK direttamente in Dynamic Media e far sì che Dynamic Media distribuisca automaticamente le risorse RGB tramite un predefinito per immagini o tramite un profilo colore. Non è necessario creare più versioni di un file, mantenendo così il concetto di _un file di risorse principali con infinite possibilità_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Pubblicare e visualizzare in anteprima le risorse

Dopo aver caricato le risorse in Dynamic Media, è buona prassi effettuare le operazioni seguenti: _pubblicare_ selezionando le risorse e facendo clic su **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]** in Dynamic Media. La pubblicazione delle risorse è necessaria se desideri utilizzarle in qualsiasi esperienza. Dopo la pubblicazione, le risorse sono disponibili per l’inclusione in una pagina web utilizzando un URL generato da Dynamic Media che copia oppure tramite l’incorporazione di codice nella pagina.

Oltre a pubblicare manualmente le risorse, puoi configurare Dynamic Media in modo da pubblicare istantaneamente le risorse, senza alcun intervento dell’utente, al momento del caricamento.

Dopo il caricamento, in Dynamic Media sono disponibili diversi modi per visualizzare in anteprima le rappresentazioni di una risorsa. L’anteprima delle rappresentazioni può aiutarti a fornire un’idea di ciò che vede un cliente. Un metodo di anteprima comune consiste nel selezionare una risorsa e quindi visualizzarne le rappresentazioni selezionando un _predefinito immagine_ come illustrato di seguito.

![Anteprima di un rendering di una risorsa basato sul predefinito per immagini Grandi](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Anteprima di un rendering di una risorsa basato sul predefinito immagine &quot;Grande&quot; selezionato. È stato fatto clic sul pulsante URL. Il percorso URL risultante contiene il nome del predefinito immagine &quot;Grande&quot; e può essere utilizzato in una pagina web._

L&#39;URL di cui sopra è attivo! [Provate](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$).

Un altro metodo per visualizzare in anteprima una risorsa è quello di selezionare la risorsa immagine e quindi selezionare un _Visualizzatori_ come illustrato di seguito.

![Anteprima di una risorsa in base al predefinito visualizzatore Zoom verticale light](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Anteprima di una risorsa in base al predefinito visualizzatore ZoomVertical_light selezionato. Puntatore del mouse (`+`) è stato spostato sull&#39;orologio per ingrandire. Osserva i pulsanti URL e Incorpora ._

Il rendering di cui sopra è live! [Provate](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target=&quot;_blank&quot;}.

## Facoltativo - Ulteriori informazioni

La prima parte di questo percorso ha trattato le basi di una serie di argomenti relativi a Dynamic Media. Per saperne di più su ciò che hai appena letto, utilizza i materiali qui sotto per esplorare i concetti in modo più dettagliato. In caso contrario, puoi continuare con la Parte II del tuo percorso. Vedi [Ulteriori informazioni in questo Percorso Dynamic Media](#whats-next).

_Argomenti dell’Aiuto di Dynamic Media_

* [Utilizzare Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [Informazioni sull’imaging intelligente](/help/assets/dynamic-media/imaging-faq.md)
* [Come creare set video adattivi](/help/assets/dynamic-media/video.md)
* [Best practice per ottimizzare la qualità delle immagini](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [Come caricare le risorse](/help/assets/add-assets.md#upload-assets)
* [Come visualizzare in anteprima le risorse](/help/assets/dynamic-media/previewing-assets.md)
* [Come visualizzare in anteprima le risorse 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Come distribuire Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [Come pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)

_Tutorial su Dynamic Media_

* [Utilizzare Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it)
* [Libreria dei contenuti di Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (ricerca su _Dynamic Media_)

_Visualizzatori Dynamic Media_

* [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) di ciascun visualizzatore

## Ulteriori informazioni in questo Percorso Dynamic Media {#whats-next}

Nella parte II di questo percorso, esaminerai gli URL Dynamic Media un po&#39; più vicini per comprendere meglio cosa succede quando una risorsa viene consegnata. Ulteriori informazioni sui fondamenti della creazione di predefiniti per immagini per il rendering delle risorse, sui set di immagini, sui set 360 gradi e sui set di file multimediali diversi e sulla relativa creazione.

Portami a [percorso Dynamic Media: Nozioni di base, parte II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->