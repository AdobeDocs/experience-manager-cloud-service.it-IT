---
title: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud
description: Formati di file e tipi MIME supportati da Experience Manager Assets come servizio Cloud.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Formati di file supportati per le risorse {#supported-file-formats}

Adobe Experience Manager come servizio Cloud supporta funzionalità di base per la gestione dei contenuti - archiviazione, gestione dei metadati online, controllo delle versioni, caricamento e download e così via - per qualsiasi file binario, indipendentemente dal suo formato. Inoltre, per i formati di file comunemente utilizzati, come immagini, documenti di proprietà Adobe e video, offre un supporto esteso per la generazione di anteprime e rappresentazioni e l’estrazione di metadati e testo per l’indicizzazione full-text. Questo supporto esteso viene fornito utilizzando i microservizi [delle](asset-microservices-configure-and-use.md)risorse.

Alcuni esempi di formati di file con supporto esteso:

* Formati [di file](#adobe-formats) Adobe principali prodotti da applicazioni e servizi Adobe, inclusi Adobe Photoshop, InDesign, Illustrator, XD, Dimension e Acrobat / PDF.
* Formati di file [di imaging chiave](#image-formats)
* [Formati](#camera-raw-formats) di file Camera Raw per un&#39;ampia gamma di telecamere, tra cui Canon, Nikon, Fujifilm, Olympus e altri produttori (con tecnologia Adobe Camera Raw)
* Formati [comuni di](#document-formats)documenti, inclusi i formati [Microsoft Office](#microsoft-office-formats) (Word, Excel, PowerPoint) e [Open Document](#opendocument-formats)
* Ampia gamma di formati [video](#video-formats) e [audio](#audio-formats)

## Legenda per informazioni dettagliate sul supporto {#legend-for-detailed-support-information}

La legenda seguente descrive il livello di supporto per una funzione:

| Livello di supporto | Descrizione |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | Supportato |
| * | Vedere le osservazioni sotto la tabella |
| - | Non applicabile |

Le colonne delle tabelle di supporto forniscono le seguenti informazioni:

| Colonna | Descrizione |
| ------------ | --------------------------------------------------------------- |
| Formato | Formato file (estensione file) del binario originale della risorsa |
| GIF | Formato GIF per la generazione di rappresentazioni |
| JPEG | Formato JPEG per la generazione di rappresentazioni |
| PNG | Formato PNG per la generazione di rappresentazioni |
| XMP | Estrazione di metadati dal binario originale |
| TXT | Estrazione di testo da un documento per l&#39;indicizzazione |
| Larghezza/Altezza | Supporto per la definizione di larghezza e altezza di una rappresentazione (pixel) |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Formati Adobe {#adobe-formats}

| Formato file | GIF | JPEG | PNG | TXT | XMP | Larghezza/Altezza |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| COLLAGE | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| IDEE | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* Per i file INDD (InDesign), la dimensione della rappresentazione è determinata dall&#39;anteprima incorporata nel file INDD. Configurate le preferenze in InDesign (**[!UICONTROL Preferenze > Gestione file > Salva sempre immagini di anteprima con documenti, Dimensione]** anteprima) per incorporare una rappresentazione più grande.

## Formati immagine {#image-formats}

| Formato file | GIF | JPEG | PNG | XMP | Larghezza/Altezza |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Formati RAW della telecamera {#camera-raw-formats}

| Formato file | GIF | JPEG | PNG | XMP | Larghezza/Altezza |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formati documento {#document-formats}

| Formato file | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| TESTO | ✓ | - |
| XML | ✓ | - |

## Formati di Microsoft Office {#microsoft-office-formats}

| Formato file | GIF | JPEG | PNG | TESTO | Larghezza/Altezza |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formati OpenDocument {#opendocument-formats}

| Formato file | GIF | JPEG | PNG | TESTO | Altezza |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formati video {#video-formats}

| Formato file | GIF | JPEG | PNG | XMP | Larghezza/Altezza |
| ----------- | --- | ---- | --- | --- | ------------ |
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

## Formati audio {#audio-formats}

Assets as a Cloud Service offre il supporto XMP per i seguenti formati audio: AIF, ASF, M4A, MP3, WAV e WMA.

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [Elaborazione delle risorse tramite i microservizi delle risorse](asset-microservices-overview.md)

