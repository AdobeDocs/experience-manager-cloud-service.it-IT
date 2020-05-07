---
title: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud
description: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2830c1cb2a9a0c06e6f8a4a765420706f5ceb093
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 9%

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager come servizio Cloud supporta funzionalità di gestione dei contenuti di base — archiviazione, gestione dei metadati online, controllo delle versioni, caricamento, scaricamento e così via — per qualsiasi file binario, indipendentemente dal suo formato. Risorse Adobe Experience Manager supporta un&#39;ampia gamma di formati di file e ogni funzione di prodotto supporta vari formati.

Inoltre, Experience Manager Assets offre un ampio supporto per la generazione di anteprime e rappresentazioni e per l’estrazione di metadati e testo per l’indicizzazione full-text. Questo supporto esteso viene fornito utilizzando i microservizi [delle](asset-microservices-configure-and-use.md)risorse.

I principali elementi di rilievo per la conversione delle risorse mediante i microservizi delle risorse sono:

* Formati [di file](#adobe-formats) Adobe principali prodotti da applicazioni e servizi Adobe, inclusi Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension, Adobe Acrobat o PDF.
* Formati [di file](#image-formats)di imaging chiave.
* [Formati](#camera-raw-formats) di file Camera Raw per un&#39;ampia gamma di telecamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (basati su Adobe Camera Raw).
* Formati [comuni di](#document-formats)documenti, inclusi i formati Microsoft Office e Open Document.
* Ampia gamma di formati [video](#video-formats) e [audio.](#audio-formats)

La legenda seguente descrive il livello di supporto.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Supportato |
| * | Vedere le osservazioni riportate di seguito. |
| - | Non applicabile |

## Formati Adobe {#adobe-formats}

| Formato file | Generazione delle miniature | Estrazione full-text | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| IDEE | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Per [!DNL Adobe InDesign] i file (INDD), la dimensione della rappresentazione è determinata dall&#39;anteprima incorporata nel file INDD. Configura le preferenze in [!DNL InDesign] (**[!UICONTROL Preferenze > Gestione file > Salva sempre immagini di anteprima con documenti, Dimensione]** anteprima) per incorporare una rappresentazione più grande.

## Formati immagine {#image-formats}

| Formato file | Generazione delle miniature | Estrazione di metadati | Larghezza/Altezza | Ritaglia |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## Formati immagine in [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Carica (formato di input) | Creare un predefinito per immagini (formato di output) | Anteprima rappresentazione dinamica | Distribuzione di rappresentazioni dinamiche | Download della rappresentazione dinamica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

† L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da [!DNL Adobe Photoshop] e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere l’immagine effettiva o meno.

I seguenti sottotipi di formati di file immagine raster non supportati in [!DNL Dynamic Media]:

* File PNG con dimensioni blocco IDAT superiori a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Scala di grigio o Bitmap non sono supportati. Gli spazi colore DuoTone, Lab e Indexed non sono supportati.
* File PSD con una profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* file TIFF con spazio colore Lab.

## [!DNL Camera RAW] format {#camera-raw-formats}

| Formato file | Generazione delle miniature | Estrazione di metadati | Larghezza/Altezza |
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

## Formati documento {#document-formats}

I formati dei documenti supportati per le funzioni di gestione delle risorse sono i seguenti.

| Formato file | Generazione delle miniature | Estrazione full-text | Larghezza/Altezza | Gestione dei metadati | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## Formati di documento [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Carica (formato di input) | Creare un predefinito per immagini (formato di output) | Anteprima rappresentazione dinamica | Distribuzione di rappresentazioni dinamiche | Download della rappresentazione dinamica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## Formati video {#video-formats}

| Formato file | Generazione delle miniature | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
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
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formati video in [!DNL Dynamic Media] per la transcodifica {#video-dynamic-media-transcoding}

| Estensione dei file video | Contenitore | Codec video consigliati | Codec video non supportati |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC (tutti i profili) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animazione Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Interferenza A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Video Raw rosso | MJPEG 2000 |  |
| RAM, RM | RealVideo | Non supportato | Real G2 (RV 20), Real 8 (RV 30), Real 10 (RV 40) |
| FLAC | Flac nativo | Codec audio senza perdita di dati |  |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 |  |

## Formati audio {#audio-formats}

Assets as a Cloud Service (Risorse come servizio cloud) fornisce il supporto per l&#39;estrazione dei metadati XMP per i formati audio FIA, ASF, M4A, MP3, WAV e WMA.

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi delle risorse](asset-microservices-overview.md)

