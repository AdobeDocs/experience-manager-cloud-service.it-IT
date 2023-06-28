---
title: Formati di file supportati
description: Formati di file supportati per i vari casi d’uso di [!DNL Assets view]
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: bc44e98d-446e-41ff-b5b4-9dc324834630
source-git-commit: 6cb30ffda6c0de04e5cb3d01341b59c9ee75b335
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 96%

---

# Supporto dei formati di file in [!DNL Assets view] {#file-format-support}

[!DNL Assets view] supporta un’ampia gamma di formati di file e ogni funzionalità supporta diversi tipi di file.

* ![icona per file immagine](assets/image-icon.svg) Immagini: JPG, PNG, GIF, TIFF e altri
* ![icona creative cloud](assets/creative-cloud-files.svg) File Creative Cloud: PSD, AI e INDD
* ![icona per file da fotocamera](assets/camera-icon.svg) File Camera Raw: CR2/CR3, NEF, SRW/SRF e altri
* ![icona per file documento](assets/document-icon.svg) Documenti: DOCX, PDF, PPTX e XLSX
* ![icona per file video](assets/video-icon.svg) Video: MP4

[!DNL Assets view] supporta qualsiasi formato di file binario con servizi di base quali archiviazione, caricamento, copia, spostamento, eliminazione e aggiunta di metadati.

[!DNL Assets view] supporta anche i file Camera Raw di una vasta gamma di produttori di fotocamere, tra cui Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF) e altri, grazie ad Adobe Camera Raw.

I vari tipi di file sono supportati per diversi casi d’uso e funzioni, come riepilogato di seguito. La legenda seguente indica i diversi livelli di supporto.

| Livello di supporto | Descrizione |
|-------------------|-------------------------|
| ✓ | Funzione supportata |
| ✓ ‡ | Funzione supportata a determinate condizioni |
| − | Non applicabile |

## Aggiungere, caricare e visualizzare le risorse {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tipo risorsa | [Sfogliare](/help/assets/navigate-assets-view.md) | Copiare | [Caricare](/help/assets/add-delete-assets-view.md) | Creare | [Eliminare](/help/assets/add-delete-assets-view.md#delete-assets) | Dettagli | Zoom immagine | [Visualizzato di recente](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Immagini raster | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| File non elaborati | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Cartelle | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| Video MP4 | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD, AI e INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| Altri file binari | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Cercare, utilizzare e modificare le risorse {#support-to-search-use-edit}

| Tipo risorsa | [Download](/help/assets/manage-organize-assets-view.md#download) | Inserimento tramite trascinamento | [Editor immagine](/help/assets/edit-images-assets-view.md) | [Ricerca](/help/assets/search-assets-view.md) | [Tag avanzati](/help/assets/metadata-assets-view.md#tags) | [Rinomina](/help/assets/manage-organize-assets-view.md) | [Versioni](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Immagini raster | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| File non elaborati | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| Cartelle | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Video | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| CC Libraries | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| AI e INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Altri file binari | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## Rivedere le risorse e collaborare {#support-to-review-collaborate}

| Tipo risorsa | Annotazioni | Commenti | Creazione di attività e revisione |
|---------------|----------|----------|-------------------------|
| Immagini raster | ✓ | ✓ | ✓ |
| File non elaborati | ✓ | ✓ | ✓ |
| Cartelle | − | − | − |
| Video | − | ✓ | ✓ |
| CC Libraries | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD, AI e INDD | − | ✓ | ✓ |
| Altri file binari | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## Altre attività di gestione risorse {#support-to-manage-assets}

| Tipo risorsa | [Metadati](/help/assets/metadata-assets-view.md) | [Rappresentazioni](/help/assets/add-delete-assets-view.md#renditions) | [Eliminare](/help/assets/add-delete-assets-view.md#delete-assets) | Copiare | Spostare |
|---------------|-------------------|------------|----------|----------|----------|
| Immagini raster | ✓ | ✓ | ✓ | ✓ | ✓ |
| File non elaborati | ✓ | ✓ | ✓ | ✓ | ✓ |
| Cartelle | ✓ | − | ✓ | ✓ | ✓ |
| Video | ✓ | − | ✓ | ✓ | ✓ |
| CC Libraries | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| PSD, AI e INDD | ✓ | − | ✓ | ✓ | ✓ |
| Altri file binari | ✓ | − | ✓ | ✓ | ✓ |

Gli utenti di [!DNL Adobe Asset Link] possono caricare e consegnare (caricare una nuova versione) i file nell’archivio di [!DNL Assets view] dalle applicazioni desktop [!DNL Adobe Creative Cloud] supportate.

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Passaggi successivi {#next-steps}

* Fornire feedback sul prodotto utilizzando [!UICONTROL Feedback] opzione disponibile nell’interfaccia utente di visualizzazione delle risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support)
