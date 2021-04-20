---
title: Formati di file e tipi MIME supportati
description: Formati di file e tipi MIME supportati da [!DNL Experience Manager Assets] come a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: Business Practitioner,Administrator
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 10%

---

# [!DNL Assets] formati di file supportati  {#supported-file-formats}

[!DNL Adobe Experience Manager] as a  [!DNL Cloud Service] supporta funzionalità di base per la gestione dei contenuti - archiviazione, gestione dei metadati online, controllo delle versioni, caricamento e download e così via - per qualsiasi file binario, indipendentemente dal formato. [!DNL Adobe Experience Manager Assets] supporta un’ampia gamma di formati di file e ogni funzionalità di prodotto supporta diversi formati.

Inoltre, [!DNL Experience Manager Assets] offre un esteso supporto per generare anteprime e rappresentazioni ed estrarre metadati e testo per l’indicizzazione full-text. Questo supporto esteso viene fornito utilizzando i [microservizi per le risorse](asset-microservices-configure-and-use.md).

Gli elementi di rilievo per la conversione delle risorse tramite i microservizi per le risorse includono:

* I formati di file di Adobe [prodotti da applicazioni e servizi Adobe, inclusi [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] e [!DNL Adobe Acrobat] o PDF, sono ](#adobe-formats).
* Chiave [formati di file immagine](#image-formats).
* [Formati di file Camera Raw ](#camera-raw-formats) per una vasta gamma di telecamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (alimentati da Adobe Camera Raw).
* Formati di documenti [comuni](#document-formats), inclusi i formati Microsoft Office e Open Document.
* Ampia gamma di formati [video](#video-formats) e [audio.](#audio-formats)

La legenda seguente descrive il livello di supporto per ciascun formato.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| . | Supportata |
| * | Vedere le osservazioni sotto la tabella |
| - | Non applicabile |

## Formati di Adobe {#adobe-formats}

| Formato file | Generazione di miniature | Estrazione full-text | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | . | - | . | . |
| COLLABORAZIONE | - | - | . | - |
| DN | . | - | . | . |
| IDEE | - | - | . | - |
| INDD | . | - | . | * |
| INDT | - | - | . | - |
| PDF | . | . | . | . |
| PROTO | - | - | . | - |
| PSB | . | - | . | . |
| PSD | . | - | . | . |
| XD | . | - | . | . |

\* Per i file [!DNL Adobe InDesign] (INDD), la dimensione del rendering è determinata dall&#39;anteprima incorporata nel file INDD. Configura le preferenze in [!DNL InDesign] (**[!UICONTROL Preferenze > Gestione file > Salva sempre anteprima immagini con documenti, Dimensione anteprima]**) per incorporare una rappresentazione più grande.

## Formati immagine {#image-formats}

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza | Ritaglia |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | . | - | . | . |
| EPS | - | . | - | - |
| GIF | . | . | . | . |
| JPEG | . | . | . | . |
| PNG | . | . | . | . |
| RGB | . | . | . | . |
| RGBA | . | . | . | . |
| SGI | . | . | . | . |
| SVG | . | - | . | . |
| TIFF | . | . | . | - |

## Formati immagine in [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito per immagini (formato di output) | Anteprima del rendering dinamico | Distribuzione di rendering dinamico | Scaricare il rendering dinamico |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | . | - | - | - | - |
| EPS | . | . | . | . | . |
| GIF | . | . | . | . | . |
| JPEG | . | . | . | . | . |
| PICT | . | - | - | - | - |
| PNG | . | . | . | . | . |
| PSD   infinito | . | - | - | - | - |
| TIFF | . | . | . | . | . |

† L&#39;immagine unita viene estratta dal file PSD. Si tratta di un’immagine generata da [!DNL Adobe Photoshop] e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere o meno l’immagine effettiva.

I seguenti sottotipi di formati di file immagine raster non supportati in [!DNL Dynamic Media]:

* File PNG con una dimensione del blocco IDAT superiore a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Scala di grigio o Bitmap non sono supportati. Gli spazi colore DuoTone, Lab e Indexed non sono supportati.
* File PSD con una profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* File TIFF con spazio colore Lab.

## Formati 3D {#support-3d-formats}

Sono supportati i seguenti formati 3D.

Consulta anche [Utilizzo di risorse 3D in Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo dell&#39;accesso | Anteprima miniature | Anteprima 3D | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | . | . | . | - | . | . | - | - |
| gLB | . | . | . | . | . | - | . | . |
| gLTF | . | . | . | - | . | - | . | - |
| OBJ | . | . | . | . | . | - | . | . |
| STL | . | . | . | . | . | - | . | . |
| USDz | . | . | . | . | . | - | - | . |

## [!DNL Camera RAW] formati  {#camera-raw-formats}

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | . | . | . |
| FRECCIA | . | . | . |
| CR2 | . | . | . |
| CR3 | . | . | . |
| CRW | . | . | . |
| DCR | . | . | . |
| DNG | . | . | . |
| ERF | . | . | . |
| FFF | . | . | . |
| RGPD | . | . | . |
| IIQ | . | . | . |
| KDC | . | . | . |
| MEF | . | . | . |
| MFW | . | . | . |
| MOS | . | . | . |
| MRW | . | . | . |
| NEF | . | . | . |
| NRW | . | . | . |
| ORF | . | . | . |
| PEF | . | . | . |
| RAF | . | . | . |
| RAZZA | . | . | . |
| RW2 | . | . | . |
| RWL | . | . | . |
| SRF | . | . | . |
| SRW | . | . | . |
| X3F | . | . | . |

## Formati di documenti {#document-formats}

I formati di documento supportati per le funzioni di gestione delle risorse sono i seguenti.

| Formato file | Generazione di miniature | Estrazione full-text | Larghezza/Altezza | Gestione dei metadati | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | . | . |
| DOCX | . | . | . | . | . |
| EPUB | - | . | - | - | - |
| HTML | - | . | - | . | . |
| ODF | . | . | . | - | - |
| ODM | . | . | . | - | - |
| ODP | . | . | . | - | - |
| ODS | . | . | . | - | - |
| ODT | . | . | . | . | . |
| UFG | . | . | . | - | - |
| PDF | . | . | . | . | . |
| PPT | - | - | - | . | . |
| PPTX | . | . | . | . | . |
| PS | - | - | . | - | - |
| RTF | - | . | - | . | . |
| TXT | - | . | - | . | . |
| XLS | - | - | - | . | . |
| XLSX | . | . | . | . | . |
| XML | - | . | - | - | - |

## Formati di documenti in [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito per immagini (formato di output) | Anteprima del rendering dinamico | Distribuzione di rendering dinamico | Scaricare il rendering dinamico |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | . | - | - | - | - |
| INDD | . | - | - | - | - |
| PDF | . | . | . | . | . |

## Formati video {#video-formats}

| Formato file | Generazione di miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | . | - |
| 3GP | - | . | - |
| AVI | . | . | . |
| DIVX | . | - | . |
| F4V | . | . | . |
| FLV | . | . | . |
| M2T | . | - | . |
| M2TS | . | - | . |
| M2V | . | - | . |
| M4V | . | . | . |
| MKV | . | - | . |
| MOV | . | . | . |
| MP4 | . | . | . |
| MPEG | . | . | . |
| MPG | . | . | . |
| MTS | . | - | . |
| MXF | . | - | . |
| OGV | . | - | . |
| QT | . | - | . |
| R3D | - | . | . |
| SWF | . | - | . |
| WebM | . | - | . |
| WMV | . | . | . |

## Formati video in [!DNL Dynamic Media] per la transcodifica {#video-dynamic-media-transcoding}

| Estensione file video | Contenitore | Codec video consigliati | Codec video non supportati |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC (tutti i profili) | - |
| MOV, QT | QuickTime Apple | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animazione Apple |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | Interleave A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Video a barre rosse | MJPEG 2000 | - |
| RAM, RM | Video reale | Non supportato | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flac nativo | Codec audio senza perdita | - |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 | - |

## Formati audio {#audio-formats}

[!DNL Assets] as a  [!DNL Cloud Service] fornisce supporto per l’estrazione dei metadati XMP per i formati audio AIF, ASF, M4A, MP3, WAV e WMA.

## Suggerimenti e limitazioni {#limitations-and-tips}

* Attualmente, il limite di dimensione del file per l’estrazione dei metadati è di circa 10 GB. Quando si caricano risorse di grandi dimensioni, a volte l’operazione di estrazione dei metadati non riesce.

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi per le risorse](asset-microservices-overview.md)
>* [Formati di file supportati per l’assegnazione di tag avanzati alle risorse basate su testo](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

