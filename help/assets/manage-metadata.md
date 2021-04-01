---
title: Gestione dei metadati delle risorse digitali
description: Scopri i tipi di metadati e come  [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] consente di organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.
contentOwner: AG
mini-toc-levels: 1
feature: Gestione risorse, metadati
role: Business Practices, Architetto, Amministratore
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 3%

---


# Gestire i metadati delle risorse digitali {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] conserva i metadati per ogni risorsa. Consente di organizzare e classificare più facilmente le risorse e aiuta le persone che cercano una specifica risorsa. Grazie alla possibilità di estrarre i metadati dai file caricati su [!DNL Experience Manager Assets], la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di mantenere e gestire i metadati con le risorse, puoi organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.

>[!MORELIKETHIS]
>
>* [Metadati XMP](xmp-metadata.md)
>* [Come modificare o aggiungere metadati](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Perché abbiamo bisogno di metadati {#why-metadata}

Metadati significa dati relativi ai dati. A questo proposito, i dati si riferiscono alla risorsa digitale, ad esempio un’immagine. I metadati sono fondamentali per una gestione efficiente delle risorse.

I metadati sono la raccolta di tutti i dati disponibili per una risorsa, ma non necessariamente contenuti in tale immagine. Alcuni esempi di metadati sono:

* Nome della risorsa.
* Ora e data dell’ultima modifica.
* Dimensione della risorsa così come era memorizzata nell’archivio.
* Nome della cartella in cui è contenuta.
* Risorse correlate o tag applicati.

Le proprietà di metadati di base gestite da [!DNL Experience Manager] per le risorse consentono agli utenti di visualizzare tutte le risorse. Ad esempio, ordinare le risorse per data dell’ultima modifica è utile quando si tenta di individuare le risorse aggiunte di recente.

Puoi aggiungere ulteriori dati di alto livello alle risorse digitali, ad esempio:

* Tipo di risorsa (immagine, video, clip audio o documento?).
* Proprietario della risorsa.
* Titolo della risorsa.
* Descrizione della risorsa.
* Tag assegnati a una risorsa.

Ulteriori metadati ti aiutano a categorizzare ulteriormente le risorse ed è utile man mano che la quantità di informazioni digitali cresce. È possibile gestire poche centinaia di file in base solo ai nomi dei file. Tuttavia, questo approccio non è scalabile. Non è sufficiente che il numero di persone coinvolte e il numero di risorse gestite aumentino.

Con l’aggiunta dei metadati, il valore di una risorsa digitale aumenta, perché la risorsa diventa,

* Più accessibile: i sistemi e gli utenti possono trovarlo facilmente.
* Gestione più semplice: puoi trovare più facilmente le risorse con lo stesso set di proprietà e applicarvi le modifiche necessarie.
* Completo : la risorsa contiene ulteriori informazioni e contenuti con più metadati.

Per questi motivi, [!DNL Assets] ti offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Tipi di metadati {#types-of-metadata}

I due tipi di metadati di base sono i metadati tecnici e i metadati descrittivi.

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere mantenuti manualmente. [!DNL Experience Manager Assets] e altri software determinano automaticamente i metadati tecnici e i metadati possono cambiare quando la risorsa viene modificata. I metadati tecnici disponibili di una risorsa dipendono in larga misura dal tipo di file della risorsa. Alcuni esempi di metadati tecnici sono:

* Dimensioni di un file.
* Dimension (altezza e larghezza) di un’immagine.
* Bit rate di un file audio o video.
* Risoluzione (livello di dettaglio) di un&#39;immagine.

I metadati descrittivi sono metadati relativi al dominio dell&#39;applicazione, ad esempio, l&#39;azienda da cui proviene una risorsa. Impossibile determinare automaticamente i metadati descrittivi. Viene creato manualmente o semiautomatico. Ad esempio, una fotocamera con GPS abilitato può tracciare automaticamente la latitudine e la longitudine e aggiungere il geotag all&#39;immagine.

Il costo della creazione manuale di informazioni descrittive sui metadati è elevato. Pertanto, vengono stabiliti degli standard per facilitare lo scambio di metadati tra sistemi software e organizzazioni. [!DNL Experience Manager Assets] supporta tutti gli standard pertinenti per la gestione dei metadati.

## Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. Sono supportati diversi standard di codifica:

* XMP: utilizzato da [!DNL Assets] per memorizzare i metadati estratti all&#39;interno del repository.
* ID3: per file audio e video.
* Exif: per i file di immagine.
* Altro/Legacy: da [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e così via.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) è uno standard aperto utilizzato da  [!DNL Experience Manager Assets] per la gestione di tutti i metadati. Lo standard offre una codifica universale dei metadati che può essere incorporata in tutti i formati di file. Adobe e altre aziende supportano XMP standard in quanto fornisce un modello di contenuti avanzati. Gli utenti di XMP standard e di [!DNL Experience Manager Assets] dispongono di una piattaforma potente su cui basarsi. Per ulteriori informazioni, consulta [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Informazioni aggiuntive sui formati:

* I tag ID3 funzionano nei file MP3 e mp3PRO.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l’implementazione open-source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di assegnazione tag proprietario.

### Exif {#exif}

Il formato Exif (Exchangeable image file format) è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in molti formati di file, come JPEG, TIFF, RIFF e WAV. Exif memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Queste coppie nome-valore-metadati sono anche denominate tag, da non confondere con l’assegnazione tag in [!DNL Experience Manager]. Le moderne fotocamere digitali creano metadati Exif e il software di grafica moderno lo supportano. Il formato Exif è il denominatore più basso per la gestione dei metadata, in particolare per le immagini.

Una limitazione importante di Exif è che alcuni formati di file immagine popolari come BMP, GIF o PNG non lo supportano.

I campi metadati definiti da Exif sono tipicamente di natura tecnica e sono di uso limitato per la gestione dei metadati descrittivi. Per questo motivo, [!DNL Experience Manager Assets] offre la mappatura delle proprietà Exif in [schemi di metadati comuni](metadata-schemas.md) e in XMP.

#### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file includono [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e così via.

## Gestire i metadati delle risorse digitali {#manage-assets-metadata}

Enterprise Manager Assets consente di modificare contemporaneamente i metadati di più risorse, in modo da poter rapidamente propagare le modifiche comuni ai metadati delle risorse in blocco. Utilizza la pagina [!UICONTROL Proprietà] per modificare le proprietà dei metadati in un valore comune o aggiungere o modificare tag. Per personalizzare la pagina Proprietà metadati, ad esempio aggiungere, modificare, eliminare proprietà di metadati, utilizza l’editor schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una cartella o in una raccolta. Per le risorse disponibili nelle cartelle o che corrispondono a un criterio comune, è possibile [aggiornare in blocco i metadati dopo la ricerca](/help/assets/search-assets.md#metadata-updates).

1. Andate alla posizione delle risorse da modificare.
1. Seleziona le risorse per le quali desideri modificare le proprietà comuni.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Proprietà]** per aprire la pagina [!UICONTROL Proprietà] delle risorse selezionate.

   >[!NOTE]
   >
   >Quando selezioni più risorse, per le risorse viene selezionato il modulo principale più basso. In altre parole, la pagina [!UICONTROL Proprietà] visualizza solo i campi di metadati comuni nelle pagine [!UICONTROL Proprietà] di tutte le singole risorse.

1. Modifica le proprietà dei metadati per le risorse selezionate nelle varie schede.
1. Per visualizzare l’editor di metadati per una risorsa specifica, annulla la selezione delle risorse rimanenti nell’elenco. I campi dell’editor di metadati sono compilati con i metadati per la risorsa in questione.

   >[!NOTE]
   >
   >* Nella pagina [!UICONTROL Proprietà], puoi rimuovere le risorse dall’elenco delle risorse annullando la selezione. Per impostazione predefinita, nell’elenco delle risorse sono selezionate tutte le risorse. I metadati per le risorse rimosse dall’elenco non vengono aggiornati.
   >* Nella parte superiore dell’elenco delle risorse, seleziona la casella di controllo accanto a **[!UICONTROL Titolo]** per passare dalla selezione delle risorse alla cancellazione dell’elenco.


1. Per selezionare uno schema di metadati diverso per le risorse, tocca o fai clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti e seleziona lo schema desiderato. Salva le modifiche.
1. Per aggiungere i nuovi metadati a quelli esistenti nei campi che contengono più valori, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Tocca o fai clic su **[!UICONTROL Invia]**.

   >[!CAUTION]
   >
   >Per i campi con valore singolo, i nuovi metadati non vengono aggiunti al valore esistente nel campo, nemmeno se selezioni **[!UICONTROL Modalità di aggiunta]**.

## Metadati personalizzati utilizzando il profilo di elaborazione {#metadata-compute-service}

Le risorse come [!DNL Cloud Service] possono generare metadati personalizzati per una risorsa utilizzando i servizi nativi del cloud. Configura un profilo di elaborazione per generare metadati personalizzati. Vedi [come utilizzare il profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

![Rendering dei metadati nel profilo di elaborazione](assets/processing-profile-metadata.png)

>[!TIP]
>
>A una cartella può essere applicato un solo profilo di elaborazione. Per applicare più elaborazioni alle risorse di una cartella, aggiungi più opzioni a un singolo profilo di elaborazione. Ad esempio, un singolo profilo può generare rappresentazioni, transcodificare risorse, generare metadati personalizzati e così via. Puoi applicare filtri di tipo MIME per ogni attività in modo che venga attivata l’attività appropriata per il formato di file richiesto.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## Schemi di metadati {#metadata-schemata}

Gli schemi di metadati sono insiemi predefiniti di definizioni di proprietà di metadati che possono essere utilizzati in varie applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che le proprietà sono &#39;Info&#39; sulla risorsa.

Puoi anche progettare i tuoi schemi di metadati personalizzati, se non ne esistono alcuno che soddisfi le tue esigenze. Non duplicare le informazioni esistenti. All’interno di un’organizzazione, la separazione degli schemi facilita la condivisione dei metadati. [!DNL Experience Manager] fornisce un elenco predefinito degli schemi di metadati più comuni. L&#39;elenco ti aiuta a rilanciare la strategia dei metadati e a scegliere rapidamente le proprietà di metadati necessarie.

Gli schemi di metadati supportati sono elencati di seguito.

### Metadati standard {#standard-metadata}

* DC - [!DNL Dublin Core] è un set importante e ampiamente utilizzato di metadati.
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` e  `iptc4xmpExt` - International Press Communications Standard contiene molti metadati specifici per il soggetto.
* RDF - Resource Description Framework - per metadati web semantici generici.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Ticketing di base dei processi.

### Metadati specifici dell&#39;applicazione {#application-specific-metadata}

I metadati specifici dell&#39;applicazione includono metadati tecnici e descrittivi. Se si utilizzano tali metadati, altre applicazioni potrebbero non essere in grado di utilizzarli. Ad esempio, un&#39;applicazione diversa per il rendering delle immagini potrebbe non essere in grado di accedere ai metadati [!DNL Adobe Photoshop]. Puoi creare un passaggio del flusso di lavoro che modifica una proprietà specifica di un&#39;applicazione in una proprietà standard.

* ACDSee - Metadati gestiti dal programma [!DNL ACDSee]. Vedere [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Utilizzato da [!DNL Experience Manager Assets].
* DAM - Utilizzato da [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) è una raccolta di strumenti per la gestione di metadati e file per i sistemi operativi Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadati del Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - [Requisiti di pubblicazione per metadati standard di settore](https://www.idealliance.org/prism-metadata).
* PRL - Lingua dei diritti PRISM.
* PUR - Diritti di utilizzo PRISM.
* `xmpPlus` - Integrazione di PLUS con XMP.

### Metadati specifici per la fotografia {#photography-specific-metadata}

* Exif - Informazioni tecniche provenienti dalla fotocamera, inclusa la posizione GPS.
* Schema CRS - [!DNL Camera Raw].
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - Metadati immagine (non solo per le immagini TIFF).

### Metadati specifici per la stampa {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e applicazioni di terze parti.
* PRISM - [Requisiti di pubblicazione per metadati standard di settore](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadati XMP per il testo di paging.

### Metadati multimediali specifici {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestione dei supporti.

## Flussi di lavoro basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l’efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro e, di conseguenza, esegue alcune azioni predefinite. Ad esempio, alcuni dei modi per utilizzare flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha o meno un titolo. In caso contrario, il sistema notifica l’aggiunta di un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente o meno la distribuzione. Pertanto, il sistema invia la risorsa a un server o all’altro.
* Un flusso di lavoro può verificare la presenza di risorse senza metadati obbligatori predefiniti o risorse con metadati *non validi*.
