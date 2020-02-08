---
title: Gestione dei metadati per le risorse digitali
description: Scopri i tipi di metadati e come Risorse AEM consente di gestire i metadati per le risorse per facilitarne la categorizzazione e l’organizzazione. Grazie alla possibilità di gestire e mantenere con le risorse metadati arbitrari, Risorse AEM consente di organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Gestione dei metadati delle risorse digitali {#managing-metadata-for-digital-assets}

Risorse Adobe Experience Manager (AEM) conserva i metadati per ogni risorsa. Questo semplifica la categorizzazione e l’organizzazione delle risorse e aiuta le persone che cercano una risorsa specifica. Grazie alla possibilità di estrarre i metadati dai file caricati in Risorse AEM, la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di gestire e mantenere con le risorse metadati arbitrari, Risorse AEM consente di organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.

>[!MORELIKETHIS]
>
>* [Metadati XMP](xmp-metadata.md)
>* [Come modificare o aggiungere metadati](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Perché i metadati {#why-metadata}

Metadati significa dati sui dati. A questo proposito, i dati si riferiscono alla risorsa con cui hai a che fare, ad esempio un’immagine. I metadati sono importanti perché consentono agli utenti di gestire le risorse in modo più efficiente.

I metadati sono la raccolta di tutti i dati disponibili per questa immagine, ma non necessariamente contenuti in tale immagine, ad esempio:

* il nome della risorsa
* l&#39;ora e la data dell&#39;ultima modifica
* le dimensioni dell’immagine così come è stata memorizzata nella directory archivio
* il nome della cartella in cui si trova

Queste sono le proprietà di metadati di base che AEM può gestire per le risorse, che consentono agli utenti di visualizzare tutte le risorse, ad esempio, ordinate in base alla data dell’ultima modifica, utile quando cercano di scoprire quali risorse sono state aggiunte di recente alla directory archivio.

Puoi aggiungere più dati di alto livello alle risorse digitali, ad esempio:

* il tipo di risorsa (è un&#39;immagine, un video, una clip audio o un documento?)
* proprietario della risorsa
* titolo della risorsa
* la descrizione del bene
* i tag assegnati a una risorsa

Più metadati consentono di classificare ulteriormente le risorse ed è utile man mano che cresce la quantità di informazioni digitali. Anche se è possibile per una singola persona gestire un elenco di poche centinaia di file semplicemente in base ai loro nomi di file, questo approccio è inferiore quando il numero di persone coinvolte e il numero di risorse gestite aumenta.

Man mano che i metadati vengono aggiunti alle risorse, il valore della risorsa aumenta, perché la risorsa diventa

* più accessibile - la gente può trovare molto più facile
* gestione più semplice: è possibile trovare risorse con lo stesso set di proprietà in modo più semplice e apportare modifiche
* più complesso: più metadati sono stati aggiunti a una risorsa, più importante sarà la gestione dei metadati

Per questi motivi, Risorse AEM offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Nozioni di base sui metadati {#metadata-basics}

I metadati vengono estratti dalle risorse al momento dell’importazione (assimilazione). Inoltre, l’aggiunta di metadati facilita ulteriormente la classificazione delle risorse.

Questa sezione descrive i tipi di metadati e gli standard di codifica.

### Metadati tecnici {#technical-metadata}

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere mantenuti manualmente. I metadati tecnici possono essere determinati automaticamente da Risorse AEM e altri software e possono essere modificati al momento della modifica della risorsa. I metadati tecnici disponibili per una risorsa dipendono in larga misura dal tipo di file della risorsa. Di seguito sono riportati alcuni esempi di metadati tecnici:

* le dimensioni di un file
* le dimensioni (altezza e larghezza) di un’immagine
* bitrate di un file audio o video
* la risoluzione (livello di dettaglio) di un&#39;immagine

### Metadati descrittivi {#descriptive-metadata}

I metadati descrittivi sono metadati relativi al dominio applicazione, ad esempio l’azienda da cui proviene una risorsa. I metadati descrittivi non possono essere determinati automaticamente. Deve essere creato manualmente o semi-automaticamente. Ad esempio, una videocamera GPS può tracciare automaticamente latitudine e longitudine dell&#39;immagine e aggiungere queste informazioni ai metadati dell&#39;immagine.

A causa dell&#39;alto costo del lavoro manuale necessario per creare informazioni descrittive sui metadati, sono stati definiti standard per facilitare lo scambio di metadati tra i sistemi software e le organizzazioni.

AEM Assets supporta tutti gli standard pertinenti per la gestione dei metadati.

Data l&#39;importanza dei metadata e l&#39;elevato coinvolgimento manuale necessario per creare i metadata, sono stati definiti standard che semplificano lo scambio.

### Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. Sono supportati alcuni standard di codifica:

* XMP: utilizzato da Risorse AEM per archiviare i metadati estratti nella directory archivio.
* ID3: per i file audio e video.
* EXIF: per i file di immagine.
* Altro/Legacy: da Microsoft Word, PowerPoint, Excel e così via.

#### XMP {#xmp}

XMP è la piattaforma di metadati estensibile e lo standard di metadati utilizzato da AEM Assets per la gestione di tutti i metadati. Oltre a offrire una codifica di metadati universale che può essere incorporata in tutti i formati di file, XMP fornisce un modello di contenuto avanzato ed è supportato da Adobe e da altre aziende, in modo che gli utenti di XMP in combinazione con Risorse AEM possano sfruttare una piattaforma potente.

#### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Ulteriori informazioni sui formati:

* I tag ID3 funzionano nei file MP3 e MP3pro.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l&#39;implementazione open source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore OGG.
* AAC utilizza un formato di tag proprietario.

#### EXIF {#exif}

EXIF significa formato di file di immagine sostituibile ed è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in diversi formati di file, come

* JPEG
* TIFF
* RIFF
* WAV

Una limitazione importante di EXIF è che non è supportato da altri formati di file immagine popolari come BMP, GIF o PNG.

EXIF memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Queste coppie nome-valore di metadati sono anche denominate tag, da non confondere con i tag in AEM.

Poiché l&#39;EXIF viene creata automaticamente dalle moderne telecamere digitali e supportata dai moderni software grafici, può essere considerata il denominatore più basso per la gestione dei metadata.

La maggior parte dei campi di metadati definiti da EXIF sono di natura altamente tecnica e di utilizzo limitato per la gestione dei metadati descrittivi. Per questo motivo, AEM Assets offre la mappatura delle proprietà EXIF negli schemi [di metadati](metadata-schemas.md) comuni e in [XMP](xmp-metadata.md), il potente formato di metadati utilizzato da Risorse AEM per la gestione dei metadati.

#### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file sono Microsoft Word, PowerPoint, Excel e così via.

## Gestione dei metadati delle risorse digitali {#manage-assets-metadata}

Risorse Enterprise Manager consente di modificare i metadati di più risorse contemporaneamente, in modo da poter rapidamente estendere le comuni modifiche ai metadati alle risorse in gruppo. Utilizzare la pagina [!UICONTROL Proprietà] per modificare le proprietà dei metadati impostando un valore comune o per aggiungere o modificare i tag. Per personalizzare la pagina Proprietà metadati, ad esempio aggiungere, modificare, eliminare proprietà di metadati, utilizzare l&#39;Editor schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una cartella o in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è possibile aggiornare [in massa i metadati dopo la ricerca](/help/assets/search-assets.md#metadataupdates).

1. Andate alla posizione delle risorse che desiderate modificare.
1. Selezionate le risorse per le quali desiderate modificare le proprietà comuni.
1. Dalla barra degli strumenti, toccate o fate clic su **[!UICONTROL Proprietà]** per aprire la pagina [!UICONTROL Proprietà] delle risorse selezionate.

   >[!NOTE]
   >
   >Quando selezionate più risorse, per le risorse viene selezionato il modulo padre più basso comune. In altre parole, nella pagina [!UICONTROL Proprietà] sono visualizzati solo i campi di metadati comuni nelle pagine [!UICONTROL Proprietà] di tutte le singole risorse.

1. Modificate le proprietà dei metadati per le risorse selezionate nelle varie schede.
1. Per visualizzare l’editor di metadati per una risorsa specifica, deselezionate le risorse rimanenti nell’elenco. I campi dell’editor di metadati vengono compilati con i metadati della risorsa in questione.

   >[!NOTE]
   >
   >* Nella pagina [!UICONTROL Proprietà] , potete rimuovere le risorse dall’elenco delle risorse deselezionandole. Per impostazione predefinita, nell’elenco delle risorse sono selezionate tutte le risorse. I metadati delle risorse rimosse dall’elenco non vengono aggiornati.
   >* Nella parte superiore dell’elenco delle risorse, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle risorse e la cancellazione dell’elenco.


1. Per selezionare uno schema di metadati diverso per le risorse, toccate o fate clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti, quindi selezionate lo schema desiderato. Salva le modifiche.
1. Per aggiungere i nuovi metadati ai metadati esistenti nei campi contenenti più valori, selezionate **[!UICONTROL Aggiungi modalità]**. Se non selezionate questa opzione, i nuovi metadati sostituiranno quelli esistenti nei campi. Toccate o fate clic su **[!UICONTROL Invia]**.

   >[!CAUTION]
   >
   >Per i campi con valore singolo, i nuovi metadati non vengono aggiunti al valore esistente nel campo, anche se selezionate la modalità **** Aggiungi.

## Configurare il limite per l&#39;aggiornamento in massa dei metadati {#configlimit}

Per evitare situazioni simili a DOS, AEM limita il numero di parametri supportati in una richiesta Sling. Quando aggiornate i metadati di molte risorse in una sola volta, potete raggiungere il limite massimo e i metadati non vengono aggiornati per altre risorse. AEM genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Per modificare il limite, accedete alla console Web ( **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web) e modificate il valore dei parametri **[!UICONTROL POST]** massimi nella configurazione **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi.

## Schemata metadati {#metadata-schemata}

Gli schemi di metadati sono insiemi predefiniti di definizioni di proprietà di metadati che possono essere utilizzati in un’ampia gamma di applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che le proprietà sono &quot;informazioni sulla risorsa&quot;.

Potete anche progettare i vostri schemi di metadati personali se non ne esistono alcuno che soddisfi le vostre esigenze (prestate attenzione, tuttavia, a non duplicare elementi già esistenti). La separazione degli schemi all&#39;interno di un&#39;organizzazione semplifica la condivisione dei metadati tra le organizzazioni.

AEM fornisce un elenco completo degli schemi di metadati più comuni, che consente di avviare rapidamente la strategia per i metadati e di scegliere le proprietà di metadati necessarie da uno schema già definito.

Gli schemi di metadati supportati sono elencati nella sezione seguente.

### Metadati standard {#standard-metadata}

* dc - Dublin Core - il set di metadati più importante e ampiamente utilizzato
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - un sacco di metdata specifici per oggetto
* rdf - Resource Description Framework per metadati Web semantici generici
* xmp - Extensible Metadata Platform
* xmpBJ - Job Ticketing di base

### Metadati specifici per l’applicazione {#application-specific-metadata}

>[!NOTE]
>
>I metadati specifici per le applicazioni includono metadati tecnici e descrittivi. Se utilizzate queste opzioni, altre applicazioni potrebbero non essere in grado di utilizzare i metadati. Ad esempio, se disponete di una risorsa con metadati Adobe Photoshop e un’altra applicazione per il rendering delle immagini tenta di accedere ai metadati, potrebbe non essere in grado di accedervi.
>
>Se nelle risorse sono presenti molti metadati specifici per l’applicazione, potete creare un passaggio del flusso di lavoro che modifica la proprietà specifica dell’applicazione in uno standard.

* acdsee - metadati gestiti dal programma ACDSee [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - utilizzato da Risorse AEM
* dam utilizzato da AEM Assets
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* Microsoft Photo e MP - Microsoft Photo
* pdf e pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadati per Digital Rights Management {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* più - Sistema universale di gestione delle immagini - https://www.useplus.com/
* prisma - https://www.idealliance.org/prism-metadata di pubblicazione per metadati standard di settore
* prl - Prism
* pur - Diritti di utilizzo Prism
* xmpPlus - integrazione di PLUS con XMP

### Metadati specifici per la fotografia {#photography-specific-metadata}

* exif - molte informazioni tecniche dalla telecamera, inclusa la posizione GPS
* crs - photoshop camera raw
* Iptc4xmpCore e iptc4xmpExt
* TIFF - Metadati immagine (non solo per le immagini TIFF)

### Metadati specifici per la stampa {#print-specific-metadata}

* pdf e pdfx - Adobe PDF e applicazioni di terze parti
* prisma - [www.prismstandard.org](https://www.prismstandard.org) di pubblicazione DPS per metadati standard di settore
* XMP
* xmpPG - xmp per il testo in pagine

### Metadati multimediali specifici {#multimedia-specific-metadata}

* xmpDM - Contenuti multimediali dinamici
* xmpMM - Gestione dei supporti

## Flussi di lavoro basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l&#39;efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro ed esegue quindi alcune azioni predefinite.

Ad esempio, potete usare alcuni dei flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha un titolo. In caso contrario, il sistema avvisa un utente specifico di aggiungere un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente la distribuzione. In caso contrario, il sistema invia la risorsa a un server. In caso contrario, il sistema invia la risorsa a un altro server.
