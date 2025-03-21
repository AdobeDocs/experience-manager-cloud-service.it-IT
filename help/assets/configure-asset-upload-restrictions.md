---
title: Configurare le restrizioni di caricamento delle risorse
description: Configura Adobe Experience Manager Assets per limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME. Aiuta a prevenire caricamenti accidentali di formato indesiderato e file dannosi.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
feature: Upload, Asset Ingestion
role: User, Admin, Developer
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 16%

---

# Configurare le restrizioni di caricamento delle risorse {#configure-asset-upload-restrictions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Puoi configurare Adobe Experience Manager Assets in modo da limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME.

>[!IMPORTANT]
>
>Per impostazione predefinita, Experience Manager Assets consente agli utenti di caricare risorse di tutti i tipi MIME. Tuttavia, puoi configurare le impostazioni in modo da limitare gli utenti al caricamento solo di file di tipi MIME specifici.

## Prerequisiti {#prerequisites-asset-upload-restrictions}

Per configurare le restrizioni di caricamento delle risorse è necessario disporre dei privilegi di amministratore.

## Applicare restrizioni per il caricamento delle risorse {#apply-restrictions-asset-uploadsssssss}

Per configurare [!DNL Experience Manager] in modo da limitare gli utenti al caricamento di file di tipi MIME specifici:

1. Passa a **[!UICONTROL Strumenti > Assets > Configurazioni Assets]**.

1. Fai clic su **[!UICONTROL Limitazioni di caricamento]**.

1. Fai clic su **[!UICONTROL Aggiungi]** per definire i tipi MIME consentiti.

1. Specificare il tipo MIME nella casella di testo. È possibile fare di nuovo clic su **[!UICONTROL Aggiungi]** per specificare altri tipi MIME consentiti. Puoi anche fare clic su ![icona Elimina](assets/delete-icon.svg) per eliminare qualsiasi tipo MIME dall&#39;elenco.

1. Fai clic su **[!UICONTROL Salva]**.

**Esempio 1: consenti il caricamento di tutte le immagini e dei file PDF in Experience Manager Assets**

Per consentire il caricamento di immagini in tutti i formati e di file PDF in Experience Manager Assets, effettuare le seguenti operazioni:

![Restrizioni al caricamento delle risorse](assets/asset-upload-restrictions.png)

`image/*` come tipo MIME consente il caricamento di immagini in tutti i formati. `application/pdf` come tipo MIME consente il caricamento di file PDF in Experience Manager Assets.

Se tenti di caricare un file non incluso nell’elenco dei tipi MIME consentiti, Experience Manager Assets visualizza il seguente messaggio di errore:

![File con restrizioni](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` fa riferimento a un nome di file non incluso nei tipi MIME consentiti.

**Esempio 2: consenti il caricamento di formati immagine specifici in Experience Manager Assets**

Per aggiungere formati immagine specifici ai tipi MIME consentiti e limitare il caricamento di tutti gli altri formati di risorse, effettua le seguenti impostazioni:

![Restrizioni risorse](assets/asset-restrictions.png)

In base alle impostazioni illustrate nell&#39;immagine, è possibile caricare in Experience Manager Assets immagini nei formati .JPG, .PNG e .GIF.

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
