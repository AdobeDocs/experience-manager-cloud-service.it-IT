---
title: Gestisci i tuoi documenti PDF in [!DNL Adobe Experience Manager].
description: Gestisci documenti PDF in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 1652df9e774d8212b1bcc2898ca5d57e2a0d13bc
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 6%

---

# Gestire i documenti PDF in Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets si integra perfettamente con Document Cloud PDF Viewer, consentendo di visualizzare in anteprima più pagine di un documento PDF. Inoltre, è possibile utilizzare funzioni avanzate del visualizzatore PDF di Document Cloud, quali annotazioni, testo da cercare, navigare nel documento PDF utilizzando segnalibri e miniature e altro ancora nello stesso tetto. Experience Manager Assets consente inoltre di caricare documenti in altri formati supportati e di visualizzarli in anteprima in un formato PDF.

Il visualizzatore PDF di Document Cloud offre ad AEM Assets i seguenti vantaggi:

* [Supporto per i componenti visualizzatore Document Cloud di PDF](#pdf-doc-cloud)
* [Supporto per l’anteprima di più pagine e le annotazioni per la risorsa PDF](#multi-page)
* [Supporto per l&#39;anteprima di più pagine per documenti in altri formati](#multi-format)

>[!TIP]
>
> Se non riesci a ottenere l&#39;anteprima di più pagine di un documento PDF caricato in precedenza, seleziona il PDF e fai clic su ![Rielabora](/help/assets/assets/Reprocess.svg) **Rielabora Assets**.

## Supporto per i componenti visualizzatore Document Cloud di PDF {#pdf-doc-cloud}

Il visualizzatore nativo di PDF Doc Cloud dispone dei seguenti componenti in AEM Assets:

* **Il visualizzatore PDF che utilizza le miniature di pagina** La visualizzazione delle miniature è una piccola anteprima delle pagine di un documento PDF. Utilizzando le miniature, puoi passare direttamente alla pagina desiderata. Puoi accedere alle miniature del documento PDF selezionato tramite ![miniatura](/help/assets/assets/thumbnail.svg) nel riquadro a sinistra.

* **Il visualizzatore PDF che utilizza i segnalibri** Bookmark è un collegamento diretto che consente di passare al contenuto del documento. Puoi accedere ai segnalibri del documento PDF selezionato tramite ![segnalibro](/help/assets/assets/bookmark.svg) nel riquadro a sinistra.

* **Cerca in PDF** Puoi utilizzare la ricerca ![cerca](/help/assets/assets/Search.svg) per cercare il testo nel documento di PDF.

* **Pagina su/Pagina giù** Utilizzare Pagina su ![Pagina su](/help/assets/assets/ArrowUp.svg) o Pagina giù ![Pagina giù](/help/assets/assets/ArrowDown.svg) per scorrere il documento.

* **Zoom indietro/Zoom avanti** Utilizza Zoom indietro ![Zoom indietro](/help/assets/assets/Zoom-out.svg) o Zoom avanti ![Zoom avanti](/help/assets/assets/zoom-in.svg) per applicare una visualizzazione in sequenza al documento.

* **Adatta pagina** Utilizzare le dimensioni di larghezza e altezza per adattare il documento alle dimensioni dello schermo.

* **Ancorare/Disinserire PDF** Utilizzando questa opzione è possibile ancorare o disancorare i componenti del visualizzatore nativo di PDF.

## Supporto per l’anteprima di più pagine e le annotazioni per la risorsa PDF {#multi-page}

Adobe Experience Manager Assets consente di visualizzare in anteprima un documento PDF costituito da diverse pagine. Per visualizzare in anteprima più pagine di un documento PDF, attenersi alla seguente procedura:

1. Segui i passaggi per [caricare le risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfogliare il documento PDF da caricare e visualizzare in anteprima.
1. Aprire il documento.
1. Il visualizzatore documenti di PDF viene caricato per impostazione predefinita. Potete anche selezionare la rappresentazione PDF nel pannello della rappresentazione.
1. Nel menu a discesa Rappresentazioni selezionare **Tutte le rappresentazioni**.

Puoi anche applicare [annotazioni](#pdf-annotations) al documento PDF in un&#39;anteprima su più pagine.

>[!NOTE]
>
> La dimensione massima di una risorsa che puoi visualizzare in anteprima è di 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Annotazioni PDF{#pdf-annotations}**

Experience Manager Assets consente di aggiungere commenti a un documento PDF. Un documento PDF può contenere più annotazioni.

Per annotare un documento PDF, effettuare le seguenti operazioni:

1. Vai all’interfaccia di Assets e individua il documento PDF a cui desideri aggiungere un’annotazione. Il visualizzatore PDF nativo si apre a destra con l&#39;anteprima del documento PDF selezionato.
1. Fai clic su **Annota** nel menu principale.
Di seguito sono riportate le annotazioni che possono essere applicate a un documento di PDF:

<table>
        <tr>
             <th> Annotazione </th>
            <th> Descrizione </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> commento </td>
            <td> Seleziona Commento per esprimere un’osservazione. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> casella di testo </td>
            <td> Selezionare Casella di testo per immettere il testo. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Sticky Notes </td>
            <td> Aggiungete un piccolo testo o promemoria che potete aggiungere a una particolare area del PDF. </td>
        </tr>
        <tr>
            <td> Evidenziatore di testo <img src="/help/assets/assets/Comment.svg"> </td>
            <td> Selezionare il testo da evidenziare con colori diversi. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Sottolineatura testo </td>
            <td> Selezionare il testo che si desidera sottolineare. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> barrato </td>
            <td> Selezionare il testo che si desidera escludere. </td>
        </tr>
        <tr>
            <td> Disegno <img src="/help/assets/assets/Draw.svg"> </td>
            <td> Inserisce un'immagine visiva in PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Cancella disegno </td>
             <td> Rimuovere o annullare il disegno. </td>
        </tr>
    </table>

>[!NOTE]
>
>Le annotazioni aggiunte al documento PDF sono disponibili in modalità anteprima. Tuttavia, le annotazioni non vengono visualizzate quando si scarica o si stampa il documento PDF.

## Supporto per l&#39;anteprima di più pagine per documenti in altri formati {#multi-format}

Oltre ai documenti di PDF, è possibile visualizzare in anteprima più pagine per i documenti in altri tipi di formato. I tipi di formato di documento supportati sono TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX. Experience Manager Assets converte automaticamente questi formati di documento in un formato PDF e li rende disponibili per l&#39;anteprima.

![Anteprima multipagina di documenti in altri formati](/help/assets/assets/multi-page-other-formats.png)

Per l&#39;anteprima di più pagine di altri formati di documento supportati, effettuare le seguenti operazioni:

1. Segui i passaggi per [caricare le risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfogliare il documento da caricare e visualizzare in anteprima.
1. Aprire il documento.
1. Seleziona PDF nella sezione statica del pannello a sinistra. Il pannello a destra mostra l’anteprima di più pagine di una risorsa. Seleziona la miniatura dal pannello a sinistra per scegliere la pagina da visualizzare in anteprima.

>[!NOTE]
>
> * La dimensione massima di una risorsa che puoi visualizzare in anteprima è di 100 MB.
> * La dimensione massima dei file XLS o XLSX da visualizzare in anteprima è di 20 MB.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
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
