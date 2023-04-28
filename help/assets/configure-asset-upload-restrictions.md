---
title: Configurare le restrizioni di caricamento delle risorse
description: Configura risorse Adobe Experience Manager per limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME. Consente di evitare caricamenti accidentali di formati indesiderati e file dannosi.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 9%

---

# Configurare le restrizioni di caricamento delle risorse {#configure-asset-upload-restrictions}

Puoi configurare Risorse Adobe Experience Manager per limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME.

>[!IMPORTANT]
>
>Per impostazione predefinita, Experience Manager Assets consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare le impostazioni per limitare gli utenti a caricare solo file di tipi MIME specifici.

## Prerequisiti {#prerequisites-asset-upload-restrictions}

Per configurare le restrizioni di caricamento delle risorse, devi disporre dei privilegi di amministratore.

## Applica restrizioni per il caricamento delle risorse {#apply-restrictions-asset-uploadsssssss}

Per configurare [!DNL Experience Manager] per limitare gli utenti al caricamento di file di tipi MIME specifici:

1. Passa a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Fai clic su **[!UICONTROL Restrizioni al caricamento]**.

1. Fai clic su **[!UICONTROL Aggiungi]** per definire i tipi MIME consentiti.

1. Specifica il tipo MIME nella casella di testo. Puoi fare clic su **[!UICONTROL Aggiungi]** per specificare altri tipi MIME consentiti. Puoi anche fare clic su ![icona Elimina](assets/delete-icon.svg) per eliminare qualsiasi tipo MIME dall’elenco.

1. Fai clic su **[!UICONTROL Salva]**.

**Esempio 1: Consenti il caricamento di tutte le immagini e dei file PDF in Experience Manager Assets**

Per consentire il caricamento di immagini in tutti i formati e file PDF in Experience Manager Assets, effettua le seguenti impostazioni:

![Restrizioni al caricamento delle risorse](assets/asset-upload-restrictions.png)

`image/*` come il tipo MIME consente il caricamento di immagini in tutti i formati. `application/pdf` poiché il tipo MIME consente il caricamento di file PDF in Experience Manager Assets.

Se tenti di caricare un file non incluso nell’elenco dei tipi MIME consentiti, Experience Manager Assets visualizza il seguente messaggio di errore:

![File limitati](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` fa riferimento a un nome di file non incluso nei tipi MIME consentiti.

**Esempio 2: Consenti caricamento di formati immagine specifici in Experience Manager Assets**

Per aggiungere formati immagine specifici ai tipi MIME consentiti e per limitare il caricamento di tutti gli altri formati di risorse, procedi come segue:

![Restrizioni alle risorse](assets/asset-restrictions.png)

In base alle impostazioni illustrate nell’immagine, puoi caricare le immagini nei formati .JPG, .PNG e .GIF in Experience Manager Assets.

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
