---
title: Anteprima delle risorse 3D
description: Scopri come visualizzare in anteprima le risorse 3D in Experience Manager.
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: d00e1f49438ad36339a09f8914496faeda3d4de6
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 6%

---

# Visualizzare in anteprima le risorse 3D in Adobe Experience Manager{#previewing-3d-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Experience Manager Assets supporta l’acquisizione, la gestione, l’anteprima e la distribuzione di risorse 3D.

Puoi visualizzare in anteprima le risorse 3D con le rappresentazioni delle miniature generate automaticamente o con il visualizzatore 3D interattivo. Il visualizzatore 3D interattivo è disponibile dalla pagina dei dettagli della risorsa in Experience Manager. Il visualizzatore include, tra le altre cose, una raccolta di controlli interattivi della fotocamera che consentono di ruotare, ingrandire ed eseguire una panoramica intorno alla scena 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Formati supportati per l’anteprima delle miniature nell’Experience Manager{#supported-thumbnail-previewing-assets}

L&#39;Experience Manager genera le miniature per i seguenti formati di file per impostazione predefinita:

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| 3DS | Modello 3D Studio | application/x-3ds |  |
| USDz | Descrizione scena universale | model/vnd.usdz+zip |  |

## Formati supportati per l’anteprima 3D interattiva in Experience Manager{#supported-3d-previewing-assets}

L&#39;Experience Manager supporta l&#39;anteprima 3D interattiva per i seguenti formati di file in modalità nativa:

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary |  |
| GLTF | Formato di trasmissione GL | model/gltf+json | Consulta la **Nota** di seguito. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>Se i materiali non vengono riprodotti nell&#39;anteprima di un modello gLTF, assicurarsi che siano denominati correttamente e in un `textures` cartella nella stessa cartella principale del modello, simile alla seguente:

    Risorsa (cartella)
    model.gltf
    model.bin
    texture (cartella)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considerazioni sulle prestazioni quando si visualizza l’anteprima delle risorse 3D in Experience Manager{#performance-3d-previewing-assets}

Il tempo necessario per aprire una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa dipende da diversi fattori, quali la larghezza di banda, la complessità delle immagini e le latenze per il server.

Inoltre, le funzionalità del computer client, ad esempio una workstation, un notebook o un dispositivo touch mobile, sono importanti quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l&#39;esperienza di visualizzazione 3D interattiva più fluida e più favorevole.

**Per visualizzare in anteprima le risorse 3D in Experience Manager:**

1. Assicurati di aver caricato risorse 3D in Experience Manager.
Consulta [Formati supportati per l’anteprima 3D](#supported-3d-previewing-assets) e [Caricare le risorse](/help/assets/manage-digital-assets.md#uploading-assets).
1. Da Experience Manager, il **[!UICONTROL Navigazione]** pagina, vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.

   ![Pagina di navigazione](/help/assets/dynamic-media/assets/navigation-assets.png)

1. Dall’elenco a discesa Visualizza posto nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Vista a schede]**, quindi individua la risorsa 3D da visualizzare in anteprima.

   ![Selezione della scheda 3D](/help/assets/dynamic-media/assets/3d-card-select.png)
   _In Vista a schede, seleziona la scheda della risorsa 3D da visualizzare in anteprima._

1. Seleziona la scheda della risorsa 3D.

   ![Anteprima 3D interattiva](/help/assets/dynamic-media/assets/3d-preview.png)
   _Anteprima interattiva di una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa._
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta la fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fai clic con il pulsante destro del mouse e trascina con il mouse. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Ricentro fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |   |   |

1. Al termine, vicino all’angolo superiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
