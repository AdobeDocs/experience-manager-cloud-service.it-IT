---
title: Percorso Dynamic Media, Parte I
description: Il Percorso Dynamic Media tratta le nozioni di base di Dynamic Media, il suo funzionamento, ciò che può fare per te e il valore che apporta al tuo lavoro e ai tuoi clienti.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3615'
ht-degree: 0%

---

# Percorso Dynamic Media: Nozioni Di Base, Parte I {#dm-journey-part1}

{{see-also-dm}}

Benvenuto nel Percorso Dynamic Media.

Questo percorso descrive le nozioni di base di Dynamic Media, il suo funzionamento, il suo potenziale vantaggio e il valore che apporta al tuo lavoro e ai tuoi clienti.

**_Prerequisiti_**

* Conoscenza di base dei formati immagine e video
* Comprensione di base di HTML e CSS
* Comprensione di base degli strumenti di progettazione come Adobe Illustrator, Adobe Photoshop, Adobe XD
* L’accesso a Dynamic Media su Experience Manager è utile, ma non obbligatorio

**_Informazioni utili_**

_Parte I_

* Cos’è Dynamic Media e come può esserti utile?
* Casi d’uso per Dynamic Media
* Flusso di una risorsa attraverso il sistema Dynamic Media

_Parte II_

* Anatomia di un URL di Dynamic Media e modo in cui Dynamic Media distribuisce i contenuti
* Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse
* Set di immagini, set 360 gradi e set di file multimediali diversi

**_Pubblico_**
I tipi di pubblico più adatti ai lettori di questo percorso sono i seguenti, che hanno poca esperienza con Dynamic Media su Experience Manager:

* Amministratore
* Analista aziendale
* Architetto dei contenuti
* Autore del contenuto
* Designer
* Sviluppatore
* Marketing
* Product Manager/Proprietario

>[!TIP]
>
>Per ottenere risultati ottimali, Adobe consiglia di leggere e visualizzare questo Percorso Dynamic Media su un computer desktop.

## Cos’è Dynamic Media e come può esserti utile? {#dm-journey-a}

Dynamic Media ti consente di fornire risorse visive avanzate di merchandising e marketing on-demand. Consente inoltre di creare e distribuire esperienze di visualizzazione interattive, tra cui zoom, 360 gradi in rotazione e video. Le risorse vengono scalate in modo dinamico per l’utilizzo su siti web, mobili e social network. Utilizzando un set di risorse di origine primarie, come immagini, video e 3D, Dynamic Media genera e distribuisce più varianti di questo rich content in tempo reale attraverso la sua rete CDN (Content Delivery Network) globale, scalabile e ottimizzata per le prestazioni.

Dynamic Media incorpora i flussi di lavoro della soluzione Adobe Experience Manager Assets per la gestione delle risorse digitali per semplificare e semplificare il processo di gestione delle campagne digitali.

### Un file con infinite possibilità

Uno dei punti principali da comprendere su Dynamic Media è il concetto di _Un file di risorsa principale con infinite possibilità_.

Per comprendere meglio questo concetto, pensa al modo in cui tradizionalmente si lavora con una singola risorsa, ad esempio un’immagine o un video. In genere si crea una risorsa principale. Quindi, crei manualmente le versioni di quella stessa risorsa per ogni esperienza, ogni dispositivo necessario, ogni pagina web e ogni proprietà in cui viene utilizzata. Con il tempo, quella singola risorsa può crescere fino a 20, 30 o più versioni, senza alcuna cronologia delle versioni associata. Ora, immaginate di farlo per ogni immagine o video che avete. Il numero di versioni delle risorse diventerebbe rapidamente enorme da mantenere e aggiornare, per non parlare dell&#39;aumento dei costi di storage.

Dynamic Media, tuttavia, è fondamentalmente diverso da altri sistemi perché lo si utilizza per distribuire i contenuti multimediali _in modo dinamico_ da singole risorse primarie e da chiamate URL. I percorsi URL di Dynamic Media richiesti includono istruzioni che indicano al server di pubblicazione di Adobe come visualizzare la risorsa quando viene consegnata alla schermata di un cliente. Ad esempio, utilizzando la stessa risorsa principale, è possibile consegnarla immediatamente in un numero illimitato di copie trasformate, cambiando dimensione, formato, risoluzione, peso, colore, ritaglio ed effetti, come una visualizzazione zoom.

Questo metodo di distribuzione univoco garantisce che esperienze di qualità coerenti vengano inviate a qualsiasi schermo, indipendentemente dalle dimensioni o dalla larghezza di banda. I video a schermo intero sono ottimizzati anche per tutti i tipi di schermo e vengono trasmessi in streaming adattivo per garantire un’esperienza utente coerente e di qualità.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media fornisce la stessa immagine primaria a supporti diversi in formati e dimensioni diversi](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media garantisce che le esperienze di qualità e coerenza vengano distribuite a qualsiasi schermo, indipendentemente dalle dimensioni o dalla larghezza di banda._

Continuando a leggere, imparerai di più sul perché questo concetto di &quot;un file di risorse principale, infinite possibilità&quot; è importante.

### La rete per la distribuzione dei contenuti

Quando sei pronto per andare live con una risorsa di immagine o una risorsa video, è supportato dalla spina dorsale di Dynamic Media, costituita da una potente rete di consegna di primo livello. La rete serve centinaia di clienti in tutto il mondo ogni giorno. Le risorse sono distribuite sulla rete per la distribuzione dei contenuti (CDN) in hosting presso Akamai. La rete CDN è un sistema di servizi informatici collegati in rete che cooperano in modo trasparente per fornire contenuti, soprattutto rich media di grandi dimensioni, agli utenti finali.

Nel sistema CDN, il contenuto web viene memorizzato nelle cache web su Internet. Quindi viene distribuito dalla cache web agli utenti finali per velocizzare la consegna. Pertanto, la prima volta che qualcuno scarica una pagina web, le risorse visualizzate vengono inviate a una cache CDN. Vengono archiviati sul server in modo che, al successivo accesso alla pagina Web da parte di un utente nella stessa area, lo stesso contenuto memorizzato nella cache venga distribuito più rapidamente. Il contenuto viene distribuito più rapidamente perché si trova più vicino all’utente. Una rete CDN consente una visualizzazione più rapida delle pagine Web, ma riduce i requisiti di larghezza di banda del server centrale, in quanto i contenuti vengono distribuiti da una rete cache e non da un server centrale in ogni istanza. Questo flusso ottimizzato garantisce una migliore esperienza d&#39;uso, con un conseguente aumento delle vendite.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Storicamente, la rete CDN distribuisce ogni mese 3,5 petabyte di traffico ai clienti. Il sistema è in grado di fornire 52 miliardi di asset in un singolo giorno. Questo numero equivale a 864.000 immagini e video distribuiti correttamente ai clienti, _ogni secondo_.

### Imaging avanzato

Dynamic Media già ottimizza le risorse e assicura che ogni risorsa venga caricata rapidamente sui sistemi mobili e desktop tramite la rete CDN. Per realizzare questo obiettivo, in Dynamic Media vengono utilizzati predefiniti per le immagini per definire la qualità dell’immagine. Inoltre, definiscono il tipo di immagine che stai inviando, la sua nitidezza e altri elementi per varie parti delle esperienze o delle pagine.

Tuttavia, per aggiungere ulteriore valore a Dynamic Media oltre ai predefiniti immagine, è disponibile _Smart Imaging_.

La tecnologia Smart Imaging migliora ulteriormente le prestazioni di consegna delle immagini ottimizzando automaticamente il formato e le dimensioni dei file in base alle funzionalità del browser del cliente. Funziona con i predefiniti immagine esistenti (i predefiniti immagine sono descritti nella Parte II di questo percorso) e utilizza l&#39;intelligenza al momento della consegna.

Questa tecnologia riduce ulteriormente le dimensioni dei file di immagine in base alla velocità del browser e della connessione di rete. Poiché le risorse di immagini rappresentano la maggior parte del tempo di caricamento di una pagina, il miglioramento delle prestazioni può avere un impatto completo sugli indicatori aziendali chiave, ad esempio:

* Conversione più elevata
* Tempo trascorso sul sito
* Riduci la frequenza di rimbalzo del sito

Nel complesso, con la tecnologia Smart Imaging, le prestazioni delle network camere migliorano del 22-47% in base alle impostazioni predefinite e alle caratteristiche specifiche dell&#39;utente finale. Il tutto mantenendo la qualità delle immagini come se non fossero mai state toccate.

![Imaging avanzato](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Smart Imaging ottimizza automaticamente il formato e le dimensioni dei file di un&#39;immagine in base alla capacità del browser e alla velocità di rete del cliente._

L’imaging avanzato non è attivato per impostazione predefinita perché richiede uno sforzo coordinato tra l’utente e il supporto tecnico di Adobe Dynamic Media. Inoltre, l’abilitazione di Smart Imaging richiede la cancellazione completa della cache CDN, che viene quindi riempita con il tempo. Se ti interessa utilizzare Smart Imaging, puoi lavorare con Adobe per attivarlo inviando un ticket di supporto tecnico. Il supporto tecnico fornisce quindi un parametro URL che consente di provare, in anticipo, l’imaging intelligente. Puoi provarlo su qualsiasi pagina web o immagine in modo da vedere le prestazioni che ottieni e i risparmi. È quindi possibile attivare la tecnologia Smart Imaging per l&#39;intero sito.

### Set video adattivi

Quando in una pagina è presente un video o una pagina principale, i clienti tendono a interagire più a lungo con tale contenuto e a rimanere sulla pagina più a lungo, il che è in genere una buona cosa. Questo comportamento viene mostrato attraverso le analisi eseguite da Adobe. Tuttavia, il video può essere complesso. Per prima cosa, spesso hai un file principale di grandi dimensioni. È complicato determinare come ridimensionare e distribuire il video, il tutto per garantire un&#39;esperienza fluida indipendentemente dal dispositivo su cui viene visualizzata e dalla larghezza di banda.

Per risolvere questo problema, Dynamic Media consente di creare _set di video adattivi_.

Un set di video adattivi raggruppa le versioni dello stesso video che sono codificate in bit rate e formati diversi.

Inizia con il tuo video originale principale, che carichi nel sistema. Dynamic Media ridimensiona automaticamente o _trascodifica_ il video in più video. Quindi, al momento della consegna, determina in modo intelligente quale schermo video, quale qualità e quale formato utilizzare e lo distribuisce al telefono, al tablet o al computer desktop.

Ad esempio, su un dispositivo mobile iOS rileva una larghezza di banda come 4G, 5G o Wi-Fi. Quindi seleziona automaticamente il video codificato giusto tra i vari bit rate video all’interno del set video adattivo. Il video viene inviato in streaming a dispositivi mobili, tablet o computer desktop.

Inoltre, la qualità video viene automaticamente commutata in caso di cambiamento delle condizioni della rete. Inoltre, se un cliente entra in modalità a tutto schermo su un desktop, il set video adattivo risponde con una risoluzione migliore, migliorando l’esperienza di visualizzazione del cliente.

L’utilizzo di set video adattivi offre una riproduzione fluida e di alta qualità per i clienti che riproducono video Dynamic Media su più schermi e dispositivi. Riduce davvero la complessità del video.

## Casi d’uso per Dynamic Media {#dm-journey-b}

Di seguito sono riportati i problemi comuni relativi ai casi d’uso e le soluzioni che Dynamic Media può aiutarti a gestire per favorire il coinvolgimento positivo dei clienti, la fidelizzazione, la conversione e l’aumento del ROI.

### Caso d’uso: approccio basato su file primario

Uno dei casi d’uso più importanti per Dynamic Media è anche uno dei più ovvi. In altre parole, riducendo il peso delle pagine e delle esperienze e le dimensioni del contenuto, che si tratti di un’immagine o di un video in fase di distribuzione.

Di seguito è riportata un’esperienza o una pagina web tipica. Circa il 90% di una pagina è costituito da rich media, come immagini e video, che sono comunemente file molto più pesanti.

![Spessore pagina contenuto](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Peso pagina contenuto di una pagina Web tipica._

Il restante 10% è costituito da HTML, codice CSS e tag specifici. Desideri ottimizzare il peso del 90% della pagina; Dynamic Media ti aiuterà in questo compito. In precedenza, hai letto del concetto di _un file di risorse principale con infinite possibilità_. Questo approccio è importante per ridurre il peso complessivo delle pagine. La possibilità di prendere una risorsa principale e utilizzarla in una pagina di dettaglio del prodotto, in una pagina di miniature, nel carrello e nella griglia di ricerca ti consente di risparmiare tempo. Inoltre, assicura la coerenza tra le diverse esperienze.

![Approccio file primario](/help/assets/dynamic-media/assets/dm-onefile.png)
_L&#39;orologio è un file di risorse principale, ma con più copie trasformate, non copie, create al volo._

Osserviamo più da vicino i problemi che Dynamic Media sta risolvendo con l’unico file e alcune delle soluzioni a tale approccio.

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Crea e archivia ogni risorsa. | Utilizza un singolo file di immagine, creando automaticamente le rappresentazioni richieste solo al momento della consegna. |
| Costi di storage elevati. | Elimina la necessità di creare e archiviare più copie di una risorsa. |
| Difficoltà a mantenere la catena di custodia. | Garantisce la distribuzione di esperienze coerenti e ottimizzate per i dispositivi. |
| Nessuna cronologia delle versioni. | |
| Esperienze del brand non coerenti tra i dispositivi. | |
| Costi non necessari per la creazione di risorse duplicate. | |

Quando pensi a un file, crei una risorsa per ogni tipo di esperienza. Potreste avere un&#39;immagine di partenza, e poi dovreste creare 20, 30, o 40 varianti di quell&#39;immagine, che alla fine dovete archiviare e pagare per quell&#39;archiviazione.

Poi devi assicurarti che venga utilizzata l’immagine giusta, che potrebbe influire sulla tua capacità di mantenere coerenza tra i vari marchi. E se non riesci a trovare un’immagine, devi tornare indietro e duplicare quelle risorse.

Dynamic Media consente di creare al volo varianti di immagini a partire da quella immagine iniziale. Ti consente di essere creativo con quella risorsa principale e di non dover andare avanti e indietro con il tuo artista di design grafico o studio fotografico per creare contenuti aggiuntivi. Ed è risparmiando tempo e denaro.

Con l’approccio basato su un file, puoi utilizzare un singolo file principale. Quindi crea le versioni o le rappresentazioni necessarie per i vari siti, proprietà ed esperienze, solo nel momento in cui vengono consegnate o visualizzate da un cliente. Questa efficienza può ridurre notevolmente la quantità di storage necessario per le risorse e la complessità complessiva del flusso di lavoro. Grazie al sistema di distribuzione di Dynamic Media, ogni immagine e video è ottimizzato, caricato rapidamente e ha un aspetto eccezionale su tutti gli schermi e i dispositivi.

### Caso d’uso: video

Un altro caso d’uso che Dynamic Media risolve per è il video. Il video è complesso. È difficile da gestire. I file video sono difficili da archiviare e spostare a causa delle loro dimensioni intrinseche.

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| È difficile gestire e distribuire video ottimizzati per vari dispositivi. | Utilizza un singolo video che ridimensiona automaticamente tutti i dispositivi. |
| I video si interrompono o vengono riprodotti in bassa qualità a causa della larghezza di banda disponibile dell&#39;utente. | Distribuisci il video tramite un lettore HTML che rileva automaticamente la larghezza di banda disponibile e si adatta alla qualità per garantire un&#39;alta fedeltà e una riproduzione fluida. |
| Non è possibile creare manualmente tutte le versioni di un video in modo da garantirne una buona visualizzazione e riproduzione su tutti i dispositivi. | Eliminazione di ore di noiosa attività di transcodifica con un flusso di lavoro semplificato. |
| | Libera il tempo per un lavoro di maggior valore. |

I clienti arrivano a Dynamic Media con i seguenti problemi che sperano di risolvere:

&quot;_La mia azienda ha il video e il reparto ha speso una grande quantità di denaro per crearlo, ma ha evitato di metterlo sulle pagine o consegnarlo. Il motivo era che, a causa dei test, la qualità del video non poteva essere garantita, o anche se stava per essere riprodotto davvero. E in ultima analisi, questo influisce sul marchio dell&#39;azienda e potenzialmente sul suo ruolo nella conversione._&quot;

La soluzione di Dynamic Media è quella di prendere quell&#39;unico file video principale e lasciare che Dynamic Media ne faccia tutte le dimensioni attraverso il suo processo di transcodifica. Quindi, aggiungilo al lettore video intelligente di Dynamic Media. Questo flusso di lavoro garantisce che il video venga utilizzato nella pagina di destinazione principale, in una categoria o in una pagina di dettaglio del prodotto e sia sempre coerente e di alta qualità.

Di seguito sono riportati diversi altri casi d’uso da considerare.

### Caso d’uso: un’unica fonte di verità

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Risorse digitali distribuite in tutta l’organizzazione, in silos in diversi team o business unit. | Archivia e gestisci tutte le risorse digitali da una posizione centrale. |
| I membri del team scaricano e creano versioni locali. | I membri del team utilizzano un singolo file principale per creare _e_ per distribuire tutte le versioni necessarie su schermi e dispositivi di varie dimensioni. |
| Risorse monouso create per ogni esperienza e dispositivo. | Elimina le risorse monouso, risparmiando tempo e denaro. |

### Caso di utilizzo: ritaglio avanzato basato sull’intelligenza artificiale per rich media

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Disegnare, misurare e tagliare manualmente immagini o video per evidenziare il punto focale e visualizzarli in modo appropriato su tutti i dispositivi e le dimensioni dello schermo richiede molto tempo e lavoro. | Utilizza il ritaglio avanzato in Dynamic Media, una funzionalità di intelligenza artificiale di Adobe Sensei, per rilevare automaticamente il punto focale in qualsiasi immagine o video e ritagliarlo per mantenerlo. |
| Tempo perso che potrebbe essere impiegato meglio per creare esperienze ad alto impatto. | Acquisisce il punto di interesse desiderato indipendentemente dalle dimensioni dello schermo. |
| Risorse monouso create per ogni esperienza e dispositivo. | Elimina le attività manuali noiose e fornisce immagini e video di alta qualità e a caricamento rapido che si presentano correttamente su qualsiasi dispositivo o schermo. |

### Caso di utilizzo: authoring di contenuti multimediali interattivi

| **Problema** | **Soluzione Dynamic Media** |
|---|---|
| Esperienze cliente piatte e statiche che non coinvolgono, generano fedeltà o stimolano la conversione. | Consente agli utenti non tecnici di aggiungere facilmente e senza problemi elementi interattivi come punti attivi, caroselli e set 360 gradi per esperienze più dinamiche e coinvolgenti. |
| Ritorno limitato sull’investimento dalle risorse digitali e customer experience poco brillanti. | Promuove la conversione e il ritorno sull&#39;investimento dalle esperienze rich media. |

## Flusso di una risorsa attraverso il sistema Dynamic Media {#dm-journey-c}

Di seguito è riportato un flusso di lavoro tipico per Dynamic Media.

![Flusso di lavoro per elementi multimediali dinamici](/help/assets/dynamic-media/assets/dm-workflow.png)
_Flusso di una risorsa attraverso il sistema Dynamic Media._

Inizia con la fase di creazione con l’obiettivo principale di avere la risorsa principale alla fine. Queste risorse primarie potrebbero provenire da servizi fotografici, da fornitori video o da alcuni file audio che hai creato. Puoi utilizzare le applicazioni Creative Suite di Adobe, come Adobe InDesign, Adobe Photoshop e Adobe Illustrator, per aiutarti a elaborare i contenuti.

Al termine della creazione, la risorsa viene inserita nella soluzione di authoring caricandola in Dynamic Media. All’interno di Dynamic Media, assicurati di disporre dei giusti predefiniti per immagini e visualizzatori allineati per le varie pagine web del sito.

Infine, ottimizzate tutti i contenuti e pubblicateli sui server Dynamic Media in modo che siano disponibili per web, stampa, e-mail, desktop e dispositivi mobili.

### Caricamento di risorse in Dynamic Media

Al termine della creazione, la risorsa principale viene caricata in Dynamic Media. Il tipo di file caricato, il formato e le dimensioni del file sono attributi importanti di Dynamic Media. È al momento del caricamento che desideri assicurarti di ottenere il valore massimo dal supporto di un file.

Ad esempio, l&#39;immagine dell&#39;orologio qui sotto è di 4560 x 3020 pixel. E anche se non si può mai usare un&#39;immagine di quelle dimensioni, è comunque possibile caricarla. Più grande è l’immagine, migliore è la qualità offerta da Dynamic Media, fino alla rappresentazione di miniature. Ricorda: puoi _diminuire_ facilmente la risoluzione di un&#39;immagine esistente. Ma se tenti di _aumentare_ la risoluzione di un&#39;immagine, il risultato potrebbe essere insoddisfacente.

![Formati consigliati per il caricamento in Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Considerazioni per il caricamento delle risorse._

Adobe consiglia di caricare le risorse in un formato senza perdite. In genere, è meglio evitare JPEG perché quando distribuisci JPEG o continui a salvare JPEG, la qualità delle immagini si perde nel tempo. Si desidera iniziare con le immagini con la massima risoluzione in un formato senza perdita di dati. Tale formato è in genere un file TIFF o PNG.

Per quanto riguarda lo spazio colore, quando si pensa a un canale digitale o a una visualizzazione web, in genere si pensa a RGB (rosso, verde, blu).

La maggior parte non penserebbe mai a consegnare qualcosa in CMYK o perché si potrebbe anche volere consegnare in CMYK. Il motivo è che lo spazio colore viene utilizzato più spesso per la consegna di articoli stampati. Tuttavia, Dynamic Media può distribuire in entrambi gli spazi di colore.

Ci sono molti clienti che ancora stampano, come i club all&#39;ingrosso di magazzino. E ci sono negozi di alimentari che stampano spesso volantini su base settimanale. Tali clienti richiedono che le loro immagini siano in entrambi gli spazi di colore. In genere, questo richiedeva due immagini diverse: una in RGB e una in CMYK. Tuttavia, puoi caricare le risorse CMYK direttamente in Dynamic Media, e far sì che Dynamic Media distribuisca automaticamente le risorse RGB tramite un predefinito immagine o un profilo colore. Non è necessario creare più versioni di un file, mantenendo così il concetto di _un file di risorsa principale con infinite possibilità_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Pubblicare e visualizzare in anteprima le risorse

Dopo aver caricato le risorse in Dynamic Media, è consigliabile _pubblicarle_ selezionando le risorse e facendo clic su **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]** in Dynamic Media. La pubblicazione delle risorse è necessaria se intendi utilizzarle in qualsiasi esperienza. Una volta pubblicate, le risorse possono essere incluse in una pagina web utilizzando un URL generato da Dynamic Media e copiato oppure incorporando codice nella pagina.

Oltre a pubblicare manualmente le risorse, puoi configurare Dynamic Media in modo da pubblicare immediatamente le risorse al momento del caricamento, senza alcun intervento da parte dell’utente.

Dopo il caricamento, esistono diversi modi per visualizzare in anteprima le rappresentazioni di una risorsa in Dynamic Media. L’anteprima delle rappresentazioni può essere utile per avere un’idea di ciò che vede un cliente. Un metodo di anteprima comune consiste nel selezionare una risorsa e quindi visualizzarne le rappresentazioni selezionando un _predefinito immagine_ come illustrato di seguito.

![Anteprima del rendering di una risorsa in base al predefinito per immagine grande](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Anteprima del rendering di una risorsa in base al predefinito immagine &quot;Large&quot; selezionato. È stato fatto clic sul pulsante URL. Il percorso URL risultante contiene il nome del predefinito immagine &quot;Large&quot; e può essere utilizzato in una pagina Web._

L&#39;URL qui sopra è live! [Prova](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}.

Un altro metodo per visualizzare in anteprima una risorsa consiste nel selezionare la risorsa immagine e quindi selezionare un predefinito di _Visualizzatori_ come illustrato di seguito.

![Anteprima di una risorsa in base al predefinito visualizzatore Zoom Vertical Light](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Anteprima di una risorsa in base al predefinito visualizzatore &quot;ZoomVertical_light&quot; selezionato. Il puntatore del mouse (`+`) è stato spostato sull&#39;orologio per ingrandire. Osservare i pulsanti URL e Incorpora._

La rappresentazione qui sopra è live! [Prova](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&config=jpearldemo/ZoomVertical_light){target="_blank"}.

## Facoltativo - Ulteriori informazioni

La parte I di questo percorso tratta le nozioni di base su vari argomenti di Dynamic Media. Se desideri saperne di più su ciò che leggi, utilizza i materiali seguenti per esplorare i concetti in modo più dettagliato. In caso contrario, è possibile continuare con la Parte II del percorso. Vedi [Le prossime novità di questo Percorso Dynamic Media](#whats-next).

<!--
_Dynamic Media Help topics_

* [Work with Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [About Smart Imaging](/help/assets/dynamic-media/imaging-faq.md)
* [How to create Adaptive Video Sets](/help/assets/dynamic-media/video.md)
* [Best practices for optimizing the quality of your images](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [How to upload assets](/help/assets/add-assets.md#upload-assets)
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to deliver Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [How to publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Work with Selective Publish in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md) -->

_Esercitazioni Dynamic Media_

* [Utilizza Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it)
* [Libreria contenuti Adobe Experience Manager](https://experienceleague.adobe.com/it?lang=en#recommended/solutions/experience-manager) (ricerca in _Dynamic Media_)

_Visualizzatori Dynamic Media_

* [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) di ogni visualizzatore

## Novità di questo Percorso Dynamic Media {#whats-next}

Nella parte II di questo percorso, esamini attentamente gli URL di Dynamic Media per capire meglio cosa succede quando viene consegnata una risorsa. Scopri anche le nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse, nonché di set di immagini, set 360 gradi e set di file multimediali diversi e come vengono creati.

Vai a [Percorso Dynamic Media: nozioni di base, parte II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->