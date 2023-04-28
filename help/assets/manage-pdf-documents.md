---
title: Gestire i documenti PDF in [!DNL Adobe Experience Manager].
description: Gestire i documenti PDF in [!DNL Adobe Experience Manager] come [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 3%

---

# Gestione dei documenti PDF in Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets si integra perfettamente con Document Cloud PDF Viewer, che consente di visualizzare in anteprima più pagine di un documento PDF. Inoltre, è possibile utilizzare funzioni avanzate del visualizzatore di Document Cloud PDF, ad esempio annotazioni, testo di ricerca, navigazione nel documento PDF tramite segnalibri e miniature e altro ancora sotto lo stesso tetto. Experience Manager Assets consente inoltre di caricare documenti in altri formati supportati e di visualizzarli in anteprima in un formato PDF.

Il visualizzatore Document Cloud PDF offre i seguenti vantaggi ad AEM Assets:
* [Supporto per i componenti visualizzatore di Document Cloud PDF](#pdf-doc-cloud)
* [Supporto per l’anteprima di più pagine e le annotazioni per PDF Asset](#multi-page)
* [Supporto per l’anteprima di più pagine per i documenti in altri formati](#multi-format)

> Suggerimento
> Se non riesci a ottenere l’anteprima di più pagine di un documento PDF caricato in precedenza, seleziona il PDF e fai clic su **![Rielaborazione](/help/assets/assets/Reprocess.svg) Rielaborazione delle risorse**.

## Supporto per i componenti visualizzatore di Document Cloud PDF {#pdf-doc-cloud}

Il visualizzatore PDF Doc Cloud nativo dispone dei seguenti componenti in AEM Assets:

* **Visualizzatore PDF con miniature di pagina** La visualizzazione miniatura è una piccola anteprima delle pagine di un documento PDF. Con le miniature è possibile passare direttamente alla pagina desiderata. È possibile accedere alle miniature del documento PDF selezionato tramite ![miniatura](/help/assets/assets/thumbnail.svg) nel riquadro a sinistra.

* **Visualizzatore PDF con segnalibri** Il segnalibro è un collegamento diretto che consente di passare al contenuto del documento. È possibile accedere ai segnalibri del documento PDF selezionato tramite ![segnalibro](/help/assets/assets/bookmark.svg) nel riquadro a sinistra.

* **Ricerca in PDF** Puoi utilizzare la ricerca ![ricerca](/help/assets/assets/Search.svg) per cercare il testo nel documento di PDF.

* **Pagina su/Pagina giù** Usa pagina su ![Pagina su](/help/assets/assets/ArrowUp.svg) o Pagina giù ![Pagina giù](/help/assets/assets/ArrowDown.svg) per scorrere il documento.

* **Zoom out/Zoom avanti** Usa zoom out ![Zoom out](/help/assets/assets/ZoomOut.svg) o Zoom in ![Zoom in](/help/assets/assets/ZoomIn.svg) per inviare in streaming il documento.

* **Adatta a pagina** Utilizzare dimensioni di larghezza o altezza per adattare il documento in base alle dimensioni dello schermo.

* **Dock/Sdock PDF** È possibile ancorare o sganciare i componenti del visualizzatore PDF nativo utilizzando questa opzione.

## Supporto per l’anteprima di più pagine e le annotazioni per PDF Asset {#multi-page}

Risorse Adobe Experience Manager consente di visualizzare in anteprima il documento di PDF composto da più pagine. Per visualizzare in anteprima più pagine di un documento PDF, attenersi alla seguente procedura:

1. Segui i passaggi per [caricare le risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfoglia il documento PDF da caricare e visualizzare in anteprima.
1. Apri il documento.
1. Il visualizzatore di documenti PDF viene caricato per impostazione predefinita. Puoi anche selezionare il rendering di PDF nel pannello rendering.
1. Nel menu a discesa Rendering , seleziona **Tutte le rappresentazioni**.

È inoltre possibile applicare [annotazioni](#pdf-annotations) al documento PDF in un’anteprima con più pagine.

> NOTA
> La dimensione massima di una risorsa che puoi visualizzare in anteprima è fino a 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Annotazioni PDF{#pdf-annotations}**

Experience Manager Assets consente di aggiungere commenti a un documento di PDF. Un documento PDF può contenere più annotazioni.

Per annotare un documento PDF, eseguire le operazioni seguenti:
1. Passa all’interfaccia di Assets e individua il documento PDF di cui desideri effettuare l’annotazione. Il visualizzatore PDF nativo si apre a destra e mostra l’anteprima del documento PDF selezionato.
1. Fai clic su **Annota** dal menu principale.
Di seguito sono riportate le annotazioni che è possibile applicare a un documento PDF:

<table>
        <tr>
             <th> Annotazione </th>
            <th> Descrizione </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> Commenti </td>
            <td> Selezionare Commento per esprimere un'osservazione. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Textbox </td>
            <td> Selezionare Casella di testo per immettere il testo. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Note adesive </td>
            <td> Aggiungere un testo o un promemoria di piccole dimensioni da aggiungere a una particolare area in PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Evidenziatore testo </td>
            <td> Selezionare il testo da evidenziare in diversi colori. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Sottolineatore di testo </td>
            <td> Selezionare il testo da sottolineare. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Barrato </td>
            <td> Selezionare il testo che si desidera barrare. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> Disegno </td>
            <td> Inserisce un’arte visiva in PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Cancella disegno </td>
             <td> Rimuovere o annullare il disegno. </td>
        </tr>
    </table>

## Supporto per l’anteprima di più pagine per i documenti in altri formati {#multi-format}

Oltre ai documenti PDF, è anche possibile visualizzare in anteprima più pagine per documenti in altri formati. I tipi di formato di documento supportati sono TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX. Experience Manager Assets converte automaticamente questi formati di documento in un formato PDF e li rende disponibili per l’anteprima.

![Anteprima multipagina di documenti in altri formati](/help/assets/assets/multi-page-other-formats.png)

Per visualizzare in anteprima più pagine di altri formati di documento supportati, eseguire le operazioni seguenti:
1. Segui i passaggi per [caricare le risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfoglia il documento da caricare e visualizzare in anteprima.
1. Apri il documento.
1. Seleziona PDF sotto la sezione statica nel pannello a sinistra. Il pannello di destra mostra l’anteprima su più pagine di una risorsa. Seleziona la miniatura dal pannello a sinistra per scegliere la pagina da visualizzare in anteprima.

> NOTA
> * La dimensione massima di una risorsa che puoi visualizzare in anteprima è fino a 100 MB.
> * La dimensione massima dei file XLS o XLSX da visualizzare in anteprima è di 20 MB.
>


**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
