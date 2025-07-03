---
title: Formati di file supportati e tipi MIME
description: Formati di file e tipi MIME supportati da [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management, Renditions
role: User, Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 0129bf13301a208b777b61f65623222cdf2b4b18
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 10%

---

# [!DNL Assets] formati di file supportati {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] supporta funzionalità di base per la gestione dei contenuti, quali archiviazione, gestione dei metadati online, controllo delle versioni, caricamento e download e così via, per qualsiasi file binario, indipendentemente dal formato. [!DNL Adobe Experience Manager Assets] supporta un&#39;ampia gamma di formati di file e ogni funzionalità del prodotto supporta diversi formati.

Inoltre, [!DNL Experience Manager Assets] fornisce supporto esteso per generare anteprime e rendering ed estrarre metadati e testo per l&#39;indicizzazione full-text. Questo supporto esteso viene fornito utilizzando [microservizi per risorse](asset-microservices-configure-and-use.md).

Gli elementi di rilievo per la conversione delle risorse tramite i microservizi per le risorse includono:

* [Formati di file Adobe](#adobe-formats) chiave prodotti dalle applicazioni e dai servizi Adobe, inclusi [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] e [!DNL Adobe Acrobat] o PDF.
* [formati di file di imaging](#image-formats) chiave.
* [Formati di file Camera Raw](#camera-raw-formats) per un&#39;ampia gamma di fotocamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (con tecnologia Adobe Camera Raw).
* [formati di documento](#document-formats) comuni, inclusi i formati di Microsoft® Office e Open Document.
* Ampio intervallo di formati [video](#video-formats) e [audio](#audio-formats).

La legenda seguente descrive il livello di supporto per ciascun formato.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Funzione supportata |
| * | Vedi le osservazioni sotto la tabella |
| - | Non applicabile |

>[!IMPORTANT]
>
>[!DNL Adobe Experience Manager Assets] supporta solo i formati di file elencati in questo articolo.
>&#x200B;>Alcune funzionalità potrebbero funzionare con altri formati, ma questi formati non sono ufficialmente supportati. I risultati potrebbero essere incoerenti e le funzioni potrebbero non funzionare come previsto.
>&#x200B;>Per garantire risultati coerenti e affidabili, utilizza solo i formati supportati.

## Formati Adobe {#adobe-formats}

| Formato file | Generazione miniature | Estrazione full-text | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| SBSAR | ✓ | - | ✓ | ✓ |
| IDEE | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓* |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| BOZZA | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Per [!DNL Adobe InDesign] file (INDD), le dimensioni delle rappresentazioni sono determinate dall&#39;anteprima incorporata nel file INDD. Configura le preferenze in [!DNL InDesign] (**[!UICONTROL Preferenze > Gestione file > Salva sempre immagini di anteprima con documenti, Dimensione anteprima]**) in modo da poter incorporare rappresentazioni più grandi.

## Formati immagine {#image-formats}

| Formato file | Generazione miniature | Estrazione di metadati | Larghezza/Altezza | Ritaglia |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI™ | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## Formati 3D {#support-3d-formats}

Sono supportati i seguenti formati 3D.

Vedi anche [Utilizzare risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Archiviazione | Controllo delle versioni | Flusso di lavoro | Pubblicazione | Controllo degli accessi | Anteprima miniatura | Anteprima 3D | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw] formati {#camera-raw-formats}

| Formato file | Generazione miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formati dei documenti {#document-formats}

I formati di documento supportati per le funzioni di gestione delle risorse sono i seguenti.

| Formato file | Generazione miniature | Estrazione full-text | Larghezza/Altezza | Gestione dei metadati | [Risorse collegate](use-assets-across-connected-assets-instances.md) | Anteprima documento completa |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ | - |
| ODF | ✓ | ✓ | ✓ | - | - | - |
| ODM | ✓ | ✓ | ✓ | - | - | - |
| ODP | ✓ | ✓ | ✓ | - | - | - |
| ODS | ✓ | ✓ | ✓ | - | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| OFG | ✓ | ✓ | ✓ | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - | - |
| RTF | - | ✓ | - | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - | - |

## Formati video {#video-formats}

| Formato file | Generazione miniature | Estrazione di metadati | Larghezza/Altezza | Anteprima | Output |
| ----------- | -------------------- | ------------------- | ------------ | ------- | ------- |
| 3G2 | - | ✓ | - | - | - |
| 3GP | - | ✓ | - | - | - |
| AVI | ✓ | ✓ | ✓ | ✓ | - |
| DIVX | ✓ | - | ✓ | ✓ | - |
| F4V | ✓ | ✓ | ✓ | ✓ | - |
| FLV | ✓ | ✓ | ✓ | ✓ | - |
| M2T | ✓ | - | ✓ | ✓ | - |
| M2TS | ✓ | - | ✓ | ✓ | - |
| M2V | ✓ | - | ✓ | ✓ | - |
| M4V | ✓ | ✓ | ✓ | ✓ | - |
| MKV | ✓ | - | ✓ | ✓ | - |
| MOV | ✓ | ✓ | ✓ | ✓ | - |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | - |
| MPG | ✓ | ✓ | ✓ | ✓ | - |
| MTS | ✓ | - | ✓ | ✓ | - |
| MXF | ✓ | - | ✓ | ✓ | - |
| OGV | ✓ | - | ✓ | ✓ | - |
| QT | ✓ | - | ✓ | ✓ | - |
| R3D | - | ✓ | ✓ | ✓ | - |
| SWF | ✓ | - | ✓ | ✓ | - |
| WebM | ✓ | - | ✓ | ✓ | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | - |

## Formati audio {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] fornisce il supporto per l&#39;estrazione dei metadati XMP per i formati audio AIF, ASF, M4A, MP3, WAV e WMA.

## Formati di ingresso supportati per la trascrizione audio e video {#audio-video-transcription-formats}

* FLV (con codec H.264 e AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Windows Media Video (WMV)/ASF (.wmv, .asf)
* AVI (non compresso 8 bit/10 bit) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Registrazione video digitale Microsoft® (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Suggerimenti e limitazioni {#limitations-and-tips}

* Attualmente, il limite di dimensione del file per l’estrazione dei metadati è di circa 15 GB. Quando si caricano risorse di grandi dimensioni, a volte l’operazione di estrazione dei metadati non riesce.

## Dynamic Media: formati video di ingresso supportati per la transcodifica {#video-dynamic-media-transcoding}

| Estensione file video | Contenitore | Codec video consigliati | Codec video non supportati |
| --- | --- | --- | --- |
| AVI | Interfoliazione A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, animazione Apple |
| MP4 | MPEG-4 | H264/AVC (tutti i profili) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| ‡ MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | OGG | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Schermo Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

‡ Questo formato video non è ancora supportato per l’utilizzo con video interattivi in Dynamic Media o con Annotation in Experience Manager Assets.

## Dynamic Media - Formati di documenti supportati {#document-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito immagine (formato di output) | Anteprima rappresentazione dinamica | Distribuzione di una rappresentazione dinamica | Scarica rappresentazione dinamica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (vedi la nota seguente) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Per i PDF protetti, è supportato solo il caricamento.

## Dynamic Media - Formati supportati per le immagini raster {#image-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito immagine (formato di output) | Anteprima rappresentazione dinamica | Distribuzione di una rappresentazione dinamica | Scarica rappresentazione dinamica | Imposta i tipi che supportano questo formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md) e [Rotazione](/help/assets/dynamic-media/spin-sets.md) |
| [EPS](/help/assets/dynamic-media/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md) e [Rotazione](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md) e [Rotazione](/help/assets/dynamic-media/spin-sets.md) |
| ‡ PSD | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md) e [Rotazione](/help/assets/dynamic-media/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da [!DNL Adobe Photoshop] e inclusa nel file PSD. A seconda delle impostazioni, l&#39;immagine unita potrebbe essere o meno l&#39;immagine effettiva.

## Dynamic Media - Formati immagine raster non supportati {#unsupported-raster-image-formats-dm}

I seguenti sottotipi di formati di file immagine raster *non* sono supportati in [!DNL Dynamic Media]:

* File PNG con dimensioni del blocco IDAT superiori a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Gradazioni di grigio o Bitmap non sono supportati. DuoTone, Lab e gli spazi colore indicizzati non sono supportati.
* File PSD con profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* File TIFF con spazio colore Lab.

## Dynamic Media - Formati di file 3D supportati {#support-3d-formats-dynamic-media}

Vedi anche [Formati 3D supportati](/help/assets/file-format-support.md#support-3d-formats)

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary | Include i materiali e le texture come un&#39;unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif | |
| STL | Stereolitografia | application/vnd.ms-pki.stl | |
| USDZ | Universal Scene Description Archivio zip | model/vnd.usdz+zip | *Supporto per l&#39;acquisizione e la generazione di miniature; anteprime 3D non ancora supportate.* USDZ è un formato 3D che può essere visualizzato in modalità nativa da Safari o iOS. |

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi per le risorse](asset-microservices-overview.md).
>* [Formati di file supportati per l&#39;assegnazione di tag avanzati di risorse basate su testo](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
