---
title: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud
description: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4729f0bdd3cf7e2c6fc80e52bf2f70d689956296

---


# Assets supported file formats {#supported-file-formats}

Adobe Experience Manager come servizio Cloud supporta funzionalità di gestione dei contenuti di base — archiviazione, gestione dei metadati online, controllo delle versioni, caricamento, scaricamento e così via — per qualsiasi file binario, indipendentemente dal suo formato. Risorse Adobe Experience Manager supporta un&#39;ampia gamma di formati di file e ogni funzione di prodotto supporta vari formati.

Inoltre, Experience Manager Assets offre un ampio supporto per la generazione di anteprime e rappresentazioni e per l’estrazione di metadati e testo per l’indicizzazione full-text. Questo supporto esteso viene fornito utilizzando i microservizi [delle](asset-microservices-configure-and-use.md)risorse.

La legenda seguente descrive il livello di supporto.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Supportato |
| * | Vedere le osservazioni riportate di seguito. |
| - | Non applicabile |

## Conversione delle risorse tramite i microservizi delle risorse {#asset-microservices-supported-formats}

Le caratteristiche principali sono:

* Formati [di file](#adobe-formats) Adobe principali prodotti da applicazioni e servizi Adobe, inclusi Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension, Adobe Acrobat o PDF.
* Formati [di file](#image-formats)di imaging chiave.
* [Formati](#camera-raw-formats) di file Camera Raw per un&#39;ampia gamma di telecamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (basati su Adobe Camera Raw).
* Formati [comuni di](#document-formats)documenti, inclusi i formati Microsoft Office e Open Document.
* Ampia gamma di formati [video](#video-formats) e [audio.](#audio-formats)

Le colonne delle seguenti tabelle forniscono le seguenti informazioni:

| Colonna | Descrizione |
| ------------ | --------------------------------------------------------------- |
| Formato | Formato file (estensione file) del binario originale della risorsa. |
| GIF | Formato GIF per la generazione di rappresentazioni. |
| JPEG | Formato JPEG per la generazione di rappresentazioni. |
| PNG | Formato PNG per la generazione della rappresentazione. |
| Larghezza/Altezza | Supporto per definire la larghezza e l’altezza di una rappresentazione in pixel. |

### Formati Adobe {#adobe-formats}

| Formato file | GIF | JPEG | PNG | Estrazione full-text | TIFF | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------- | -------- | -------- | ------------------- | -------- | ------------------- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| COLLAGE | - | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | ✓ |
| IDEE | - | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓* |
| INDT | - | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ |

\* Per i file INDD (InDesign), la dimensione della rappresentazione è determinata dall&#39;anteprima incorporata nel file INDD. Configurate le preferenze in InDesign (**[!UICONTROL Preferenze > Gestione file > Salva sempre immagini di anteprima con documenti, Dimensione]** anteprima) per incorporare una rappresentazione più grande.

### Formati immagine {#image-formats}

| Formato file | GIF | JPEG | PNG | TIFF | Estrazione di metadati | Larghezza/Altezza | Ritaglia |
| ----------- | -------- | -------- | -------- | -------- | ------------------- | ------------ | -------- |
| BMP | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| EPS | - | - | - | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - |

### Formati RAW della telecamera {#camera-raw-formats}

| Formato file | GIF | JPEG | PNG | TIFF | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------- | -------- | -------- | -------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

### Formati documento {#document-formats}

I formati dei documenti supportati per le funzioni di gestione delle risorse sono i seguenti.

|  | GIF | JPEG | PNG | Estrazione full-text | TIFF | Larghezza/Altezza | Gestione dei metadati | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
| ---- | -------- | -------- | -------- | ------------------- | -------- | ------------ | ------------------- | ------------------------------------------------------------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | - | - | ✓ | - | - | - | - |
| HTML | - | - | - | ✓ | - | - | ✓ | ✓ |
| PS | - | - | - | - | - | ✓ | - | - |
| RTF | - | - | - | ✓ | - | - | ✓ | ✓ |
| TXT | - | - | - | ✓ | - | - | ✓ | ✓ |
| XML | - | - | - | ✓ | - | - | - | - |

### Formati video {#video-formats}

| Formato file | GIF | JPEG | PNG | Estrazione di metadati | Larghezza/Altezza |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

### Formati audio {#audio-formats}

Assets as a Cloud Service (Risorse come servizio cloud) fornisce il supporto per l&#39;estrazione dei metadati XMP per i formati audio FIA, ASF, M4A, MP3, WAV e WMA.

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi delle risorse](asset-microservices-overview.md)

