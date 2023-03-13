---
title: Gestire i documenti PDF in [!DNL Adobe Experience Manager].
description: Gestire i documenti PDF in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 041f0fb62b1bca79cdf4b47f971c060deb77d28f
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Gestire i documenti PDF in Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets si integra perfettamente con Document Cloud PDF Viewer, consentendo di visualizzare in anteprima più pagine di un documento PDF. È inoltre possibile utilizzare funzioni avanzate di visualizzazione di Document Cloud PDF, ad esempio annotazioni, testo da cercare, navigare nel documento di PDF utilizzando segnalibri e miniature e altro ancora nello stesso tetto. Experience Manager Assets consente inoltre di caricare documenti in altri formati supportati e di visualizzarli in anteprima in formato PDF.

Document Cloud PDF Viewer offre i seguenti vantaggi ad AEM Assets:
* [Supporto per i componenti visualizzatore Document Cloud di PDF](#pdf-doc-cloud)
* [Supporto per Anteprima pagine multiple e Annotazioni per PDF Assets](#multi-page)
* [Supporto per l&#39;anteprima di più pagine per documenti in altri formati](#multi-format)

> Suggerimento
> Se non riesci a ottenere l’anteprima di più pagine di un documento PDF caricato in precedenza, seleziona il PDF e fai clic su **![Rielabora](/help/assets/assets/Reprocess.svg) Rielabora risorse**.

## Supporto per i componenti visualizzatore Document Cloud di PDF {#pdf-doc-cloud}

Il visualizzatore nativo di PDF Doc Cloud dispone dei seguenti componenti in AEM Assets:

* **Visualizzatore PDF con miniature di pagina** La visualizzazione Anteprima è una piccola anteprima delle pagine di un documento PDF. Utilizzando le miniature, puoi passare direttamente alla pagina desiderata. È possibile accedere alle miniature del documento PDF selezionato tramite ![miniatura](/help/assets/assets/thumbnail.svg) nel riquadro sinistro.

* **Visualizzatore PDF con segnalibri** Il segnalibro è un collegamento diretto che consente di passare al contenuto del documento. È possibile accedere ai segnalibri del documento PDF selezionato tramite ![segnalibro](/help/assets/assets/bookmark.svg) nel riquadro sinistro.

* **Cerca in PDF** È possibile utilizzare la ricerca ![ricerca](/help/assets/assets/Search.svg) per cercare il testo nel documento di PDF.

* **Pagina su/Pagina giù** Usa pagina su ![Pagina su](/help/assets/assets/ArrowUp.svg) o Page Down ![Pagina giù](/help/assets/assets/ArrowDown.svg) per scorrere il documento.

* **Zoom out/Zoom in** Usa zoom out ![Zoom out](/help/assets/assets/ZoomOut.svg) o Zoom in ![Zoom in](/help/assets/assets/ZoomIn.svg) per creare una serie del documento.

* **Adatta pagina** Utilizzare le dimensioni di larghezza o altezza per adattare il documento alle dimensioni dello schermo.

* **Ancora/Disancora PDF** Con questa opzione puoi ancorare o disancorare i componenti del visualizzatore nativo di PDF.

## Supporto per Anteprima pagine multiple e Annotazioni per PDF Assets {#multi-page}

Adobe Experience Manager Assets consente di visualizzare in anteprima un documento PDF composto da diverse pagine. Per visualizzare in anteprima più pagine di un documento PDF, attenersi alla seguente procedura:

1. Segui i passaggi per [caricare risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfogliare il documento PDF da caricare e visualizzare in anteprima.
1. Aprire il documento.
1. Per impostazione predefinita, il visualizzatore documenti di PDF viene caricato. Potete anche selezionare la rappresentazione PDF nel pannello della rappresentazione.
1. Sotto il menu a discesa Rappresentazioni, seleziona **Tutte le rappresentazioni**.

Puoi anche applicare [annotazioni](#pdf-annotations) al documento PDF in un&#39;anteprima su più pagine.

> NOTA
> La dimensione massima di una risorsa che puoi visualizzare in anteprima è di 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Annotazioni PDF{#pdf-annotations}**

Experience Manager Assets consente di aggiungere commenti a un documento PDF. Un documento PDF può contenere più annotazioni.

Per annotare un documento PDF, effettuare le seguenti operazioni:
1. Passa all’interfaccia Assets e individua il documento PDF a cui desideri aggiungere un’annotazione. Il visualizzatore PDF nativo si apre a destra con l&#39;anteprima del documento PDF selezionato.
1. Clic **Annota** dal menu principale.
Di seguito sono riportate le annotazioni che possono essere applicate a un documento PDF:

<table>
        <tr>
             <th> Annotazione </th>
            <th> Descrizione </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> Commenti </td>
            <td> Seleziona Commento per esprimere un’osservazione. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Casella di testo </td>
            <td> Selezionare Casella di testo per immettere il testo. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Sticky Notes </td>
            <td> Aggiungete un piccolo testo o promemoria che potete aggiungere a una particolare area del PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Evidenziatore testo </td>
            <td> Selezionare il testo da evidenziare con colori diversi. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Sottolineatura testo </td>
            <td> Selezionare il testo che si desidera sottolineare. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Barrato </td>
            <td> Selezionare il testo che si desidera escludere. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> Disegno </td>
            <td> Inserire un'immagine nel PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Cancella disegno </td>
             <td> Rimuovere o annullare il disegno. </td>
        </tr>
    </table>

## Supporto per l&#39;anteprima di più pagine per documenti in altri formati {#multi-format}

Oltre ai documenti PDF, è possibile visualizzare in anteprima più pagine per i documenti in altri tipi di formato. I tipi di formato di documento supportati sono TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX. Experience Manager Assets converte automaticamente questi formati di documento in un formato PDF e li rende disponibili per l&#39;anteprima.

![Anteprima multipagina di documenti in altri formati](/help/assets/assets/multi-page-other-formats.png)

Per l&#39;anteprima di più pagine di altri formati di documento supportati, effettuare le seguenti operazioni:
1. Segui i passaggi per [caricare risorse in AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Sfogliare il documento da caricare e visualizzare in anteprima.
1. Aprire il documento.
1. Seleziona PDF nella sezione statica del pannello a sinistra. Il pannello a destra mostra l’anteprima di più pagine di una risorsa. Seleziona la miniatura dal pannello a sinistra per scegliere la pagina da visualizzare in anteprima.

> NOTA
> * La dimensione massima di una risorsa che puoi visualizzare in anteprima è di 100 MB.
> * La dimensione massima dei file XLS o XLSX da visualizzare in anteprima è di 20 MB.
>

