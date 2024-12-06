---
title: Visualizzare e gestire le rappresentazioni in Experience Manager Assets
description: Scopri come AEM Assets e Dynamic Media semplificano la gestione efficace delle immagini con rappresentazioni statiche e dinamiche.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: eb5886b5ed6a6f5b52303b4fccf5c266178b36f8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Visualizzare e gestire le rappresentazioni in Experience Manager Assets{#renditions}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Le rappresentazioni in Adobe Experience Manager (AEM) sono versioni personalizzate di risorse digitali, come le immagini, progettate per diversi dispositivi e piattaforme per garantire prestazioni ottimali. L’AEM facilita la creazione e la gestione di queste rappresentazioni, migliorando l’esperienza di utilizzo. Puoi creare miniature, ottimizzare immagini per il web o per dispositivi mobili, aggiungere filigrane, visualizzare e scaricare rappresentazioni dinamiche o ritaglio avanzato e fare molto di più.

I predefiniti per le immagini Dynamic Media e le rappresentazioni Smart Crop promuovono una gestione sistematica delle immagini in linea con gli standard del marchio, massimizzando la coesione del marchio. Questo semplifica il processo di individuazione e utilizzo rapido delle rappresentazioni dinamiche delle immagini in base alle esigenze, senza alcun accesso da parte dell’amministratore.

Le rappresentazioni sono classificate come statiche e dinamiche e ogni tipo presenta caratteristiche e funzionalità univoche che vengono discusse più dettagliatamente.

## Rappresentazioni statiche {#static-renditions}

Le rappresentazioni statiche sono versioni pregenerate delle risorse digitali, in genere create durante l’inserimento o la modifica delle risorse. Questi rendering sono ottimizzati per scopi e piattaforme specifici, come le miniature web, i formati facili da usare sui dispositivi mobili per la progettazione reattiva o le versioni ad alta risoluzione per la stampa, garantendo un’esperienza efficiente e coerente.
Scopri come [visualizzare e scaricare le rappresentazioni statiche](#view-and-download-static-renditions) in Experience Manager Assets.

### Visualizzare e scaricare le rappresentazioni statiche{#view-and-download-static-renditions}

Per visualizzare le rappresentazioni delle risorse e scaricarle, effettua le seguenti operazioni:

1. Nella visualizzazione Assets, fai clic su **Assets**, accedi a una cartella, seleziona una risorsa e fai clic su **Dettagli**.
1. Fai clic sull’icona della rappresentazione disponibile nel riquadro a destra.
1. Seleziona una copia trasformata per visualizzarne l&#39;anteprima e fai clic sull&#39;icona ![scarica](/help/assets/assets/download-icon.svg) per scaricarla.

   ![Visualizza e scarica rappresentazioni dinamiche](/help/assets/assets/view-download-static-rendition.png)

## Rappresentazioni dinamiche {#dynamic-renditions}

Le rappresentazioni dinamiche sono versioni personalizzate delle risorse create in tempo reale per soddisfare esigenze specifiche, ad esempio per ridimensionare le immagini in base alla risoluzione del dispositivo o per adattarle a proporzioni diverse.
Questi rendering consentono alle organizzazioni di fornire esperienze personalizzate e ottimizzate per soddisfare diverse esigenze di pubblico. Puoi visualizzare e scaricare le rappresentazioni dinamiche in Experience Manager Assets.

## Rappresentazioni Dynamic Media {#dynamic-media-renditions}

### Prima di iniziare

* Devi essere un utente con licenza di AEM Dynamic Media.
* Utilizza la [!UICONTROL visualizzazione Amministratore] per configurare:
   * [Profili immagine ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefiniti immagine](/help/assets/dynamic-media/managing-image-presets.md)

  È possibile [cambiare la visualizzazione](/help/assets/assets-view-introduction.md#how-to-access-assets-view) in un secondo momento per visualizzare in anteprima le rappresentazioni dinamiche nella visualizzazione Assets.
* da Publish a Dynamic Media per rendere disponibili le rappresentazioni di Dynamic Media nella vista Assets. Per ulteriori informazioni, vedere [Publish da Assets a AEM e Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm).


### Visualizzare e scaricare le rappresentazioni di Dynamic Media {#view-download-dm-renditions}

Per visualizzare o scaricare le rappresentazioni dinamiche delle immagini in Experience Manager Assets, effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Gestione Assets]** > **[!UICONTROL Assets]**.

1. Passa alla cartella delle risorse applicabile.

1. Fai clic sulla risorsa da visualizzare e fai clic su **[!UICONTROL Dettagli]**.

1. Nel menu di destra, fai clic sull&#39;icona **[!UICONTROL Dynamic Media]**. Nel pannello **[!UICONTROL Dynamic Media]** sono visualizzate le rappresentazioni di Dynamic Media e Ritaglio avanzato.

   ![rappresentazioni dinamiche](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Seleziona la rappresentazione da visualizzare in anteprima e fai clic su **Copia URL** per copiare l&#39;URL della rappresentazione selezionata. Fai clic su **Scarica rappresentazione** per scaricare le rappresentazioni delle risorse immagine.
1. Seleziona la rappresentazione con ritaglio avanzato da visualizzare in anteprima e fai clic su **Copia URL** per copiare l&#39;URL della rappresentazione selezionata.
1. Fai clic sull&#39;![icona di download](assets/do-not-localize/download-icon.png) per scaricare tutte le rappresentazioni di ritaglio avanzato disponibili come un unico file zip.
   ![icona di download](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >Queste rappresentazioni sono disponibili solo per le risorse immagine.

## Dynamic Media con rappresentazioni delle funzionalità OpenAPI {#dm-with-openapi-renditions}

### Prima di iniziare

* Devi essere un utente con licenza di AEM Dynamic Media.
* Per visualizzare Dynamic Media con le funzionalità OpenAPI è necessario approvare Assets. Per ulteriori informazioni, consulta [Approvare le risorse in Experience Manager](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* Dynamic Media con funzionalità OpenAPI deve essere abilitato nell’istanza AEM as a Cloud Service.

### Visualizza rappresentazioni di Dynamic Media con funzionalità OpenAPI {#view-download-dm-with-openapi-renditions}

1. Seleziona la risorsa e fai clic su **Dettagli**.
1. Fai clic sull’icona Dynamic Media disponibile nel riquadro a destra. Il pannello Dynamic Media visualizza il rendering Dynamic Media con funzionalità OpenAPI per tutti i tipi di risorse.
   ![icona di download](/help/assets/assets/dm-with-open-api-copy-url.png)
1. Seleziona l&#39;opzione **Dynamic Media con OpenAPI**, quindi fai clic su **Copia URL** per copiare l&#39;URL di consegna della risorsa.


