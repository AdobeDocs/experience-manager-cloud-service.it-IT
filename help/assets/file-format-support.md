---
title: Formati di file e tipi MIME supportati
description: Formati di file e tipi MIME supportati da [!DNL Experience Manager Assets] come [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 10%

---

# [!DNL Assets] formati di file supportati {#supported-file-formats}

[!DNL Adobe Experience Manager] come [!DNL Cloud Service] supporta funzionalità di gestione dei contenuti di base, quali archiviazione, gestione dei metadati online, controllo delle versioni, caricamento e download, e così via, per qualsiasi file binario, indipendentemente dal formato. [!DNL Adobe Experience Manager Assets] supporta un’ampia gamma di formati di file e ogni funzionalità di prodotto supporta diversi formati.

Inoltre, [!DNL Experience Manager Assets] fornisce un supporto esteso per generare anteprime e rappresentazioni ed estrarre metadati e testo per l’indicizzazione full-text. Questo supporto esteso viene fornito utilizzando [microservizi per le risorse](asset-microservices-configure-and-use.md).

Gli elementi di rilievo per la conversione delle risorse tramite i microservizi per le risorse includono:

* Chiave [Adobe di formati di file](#adobe-formats) prodotti da applicazioni e servizi di Adobe, compresi [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]e [!DNL Adobe Acrobat] o PDF.
* Chiave [formati di file immagine](#image-formats).
* [Formati di file Camera Raw](#camera-raw-formats) per una vasta gamma di telecamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (alimentati da Adobe Camera Raw).
* Comune [formati documento](#document-formats), inclusi i formati Microsoft Office e Open Document.
* Ampia gamma di formati [video](#video-formats) e [audio.](#audio-formats)

La legenda seguente descrive il livello di supporto per ciascun formato.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Funzione supportata |
| * | Vedere le osservazioni sotto la tabella |
| - | Non applicabile |

## Formati di Adobe {#adobe-formats}

| Formato file | Generazione di miniature | Estrazione full-text | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLABORAZIONE | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| IDEE | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Per [!DNL Adobe InDesign] file (INDD), la dimensione del rendering è determinata dall’anteprima incorporata nel file INDD. Configura le preferenze in [!DNL InDesign] (**[!UICONTROL Preferenze > Gestione file > Salva sempre immagini di anteprima con documenti, Dimensione anteprima]**) per incorporare rappresentazioni di dimensioni maggiori.

## Formati immagine {#image-formats}

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza | Ritaglia |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## Formati 3D {#support-3d-formats}

Sono supportati i seguenti formati 3D.

Vedi anche [Utilizzare le risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Archiviazione | Controllo delle versioni | Flusso di lavoro | Pubblicazione | Controllo dell&#39;accesso | Anteprima miniature | Anteprima 3D | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] formati {#camera-raw-formats}

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| FRECCIA | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| RGPD | ✓ | ✓ | ✓ |
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
| RAZZA | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formati documento {#document-formats}

I formati di documento supportati per le funzioni di gestione delle risorse sono i seguenti.

| Formato file | Generazione di miniature | Estrazione full-text | Larghezza/Altezza | Gestione dei metadati | [Risorse collegate](use-assets-across-connected-assets-instances.md) | Anteprima documento completa |
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
| UFG | ✓ | ✓ | ✓ | - | - | - |
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

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formati audio {#audio-formats}

[!DNL Assets] come [!DNL Cloud Service] fornisce supporto per l’estrazione dei metadati XMP per i formati audio AIF, ASF, M4A, MP3, WAV e WMA.

## Formati di ingresso supportati per la trascrizione audio e video {#audio-video-transcription-formats}

* FLV (con codec H.264 e AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Windows Media Video (WMV)/ASF (.wmv, .asf)
* AVI (8 bit non compressi/10 bit) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Registrazione video digitale Microsoft (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Suggerimenti e limitazioni {#limitations-and-tips}

* Attualmente, il limite di dimensione del file per l’estrazione dei metadati è di circa 15 GB. Quando si caricano risorse di grandi dimensioni, a volte l’operazione di estrazione dei metadati non riesce.

## Dynamic Media - Formati video di ingresso supportati per la transcodifica {#video-dynamic-media-transcoding}

| Estensione file video | Contenitore | Codec video consigliati | Codec video non supportati |
| --- | --- | --- | --- |
| AVI | Interleave A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | QuickTime di Apple | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animazione Apple |
| MP4 | MPEG-4 | H264/AVC (tutti i profili) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Schermo Microsoft (MSS2), Microsoft Photo Story (WVP2) |

† Questo formato video non è ancora supportato per l&#39;uso con video interattivi in Dynamic Media o per l&#39;uso con Annotation in Experience Manager Assets.

## Dynamic Media - Formati di documenti supportati {#document-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito per immagini (formato di output) | Anteprima del rendering dinamico | Distribuzione di rendering dinamico | Scaricare il rendering dinamico |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (vedi la nota di seguito) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Per i PDF protetti, è supportato solo il caricamento .

## Dynamic Media - Formati immagine raster supportati {#image-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito per immagini (formato di output) | Anteprima del rendering dinamico | Distribuzione di rendering dinamico | Scaricare il rendering dinamico | Imposta i tipi che supportano questo formato |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)e [Centrifuga](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)e [Centrifuga](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)e [Centrifuga](/help/assets/dynamic-media/spin-sets.md) |
| PSD | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/dynamic-media/image-sets.md), [File multimediali diversi](/help/assets/dynamic-media/mixed-media-sets.md)e [Centrifuga](/help/assets/dynamic-media/spin-sets.md) |

† L&#39;immagine unita viene estratta dal file PSD. È un’immagine generata da [!DNL Adobe Photoshop] ed è incluso nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere o meno l’immagine effettiva.

## Dynamic Media - Formati immagine raster non supportati {#unsupported-raster-image-formats-dm}

I seguenti sottotipi di formati di file immagine raster *not* supportato in [!DNL Dynamic Media]:

* File PNG con una dimensione del blocco IDAT superiore a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Scala di grigio o Bitmap non sono supportati. Gli spazi colore DuoTone, Lab e Indexed non sono supportati.
* File PSD con una profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* File TIFF con spazio colore Lab.

## Dynamic Media - Formati di file 3D supportati {#support-3d-formats-dynamic-media}

Vedi anche [Formati 3D supportati](/help/assets/file-format-support.md#support-3d-formats)

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | *Sostegno solo all&#39;acquisizione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modalità nativa da Safari o iOS. |

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi per le risorse](asset-microservices-overview.md)
>* [Formati di file supportati per l’assegnazione di tag avanzati alle risorse basate su testo](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

