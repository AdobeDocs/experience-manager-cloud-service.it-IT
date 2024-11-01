---
title: Visualizzare e gestire le rappresentazioni in Experience Manager Assets
description: Scopri come AEM Assets e Dynamic Medie semplificano la gestione efficace delle immagini con rappresentazioni statiche e dinamiche.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Visualizzare e gestire le rappresentazioni in Experience Manager Assets{#renditions}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Le rappresentazioni in Adobe Experience Manager (AEM) sono versioni personalizzate di risorse digitali, come le immagini, progettate per diversi dispositivi e piattaforme per garantire prestazioni ottimali. L’AEM facilita la creazione e la gestione di queste rappresentazioni, migliorando l’esperienza degli utenti. Puoi creare miniature, ottimizzare immagini per il web o per dispositivi mobili, aggiungere filigrane, visualizzare e scaricare rappresentazioni dinamiche o di ritaglio avanzato e fare molto di più.

I predefiniti per le immagini Dynamic Medie e le rappresentazioni Smart Crop promuovono una gestione sistematica delle immagini in linea con gli standard del marchio, massimizzando la coesione del marchio. Questo semplifica il processo di individuazione e utilizzo rapido delle rappresentazioni dinamiche delle immagini in base alle esigenze, senza alcun accesso da parte dell’amministratore.

Le rappresentazioni sono classificate come statiche e dinamiche e ogni tipo presenta caratteristiche e funzionalità univoche che vengono discusse più dettagliatamente.

## Rappresentazioni statiche {#static-renditions}

Le rappresentazioni statiche sono versioni pregenerate delle risorse digitali, in genere create durante l’inserimento o la modifica delle risorse. Questi rendering sono ottimizzati per scopi e piattaforme specifici, come le miniature web, i formati facili da usare sui dispositivi mobili per la progettazione reattiva o le versioni ad alta risoluzione per la stampa, garantendo un’esperienza efficiente e coerente.
Scopri [come visualizzare e scaricare](#view-dynamic-renditions) rappresentazioni statiche in [!DNL Experience Manager Assets].

## Rappresentazioni dinamiche {#dynamic-renditions}

Le rappresentazioni dinamiche sono versioni personalizzate delle risorse create in tempo reale per soddisfare esigenze specifiche, ad esempio per ridimensionare le immagini in base alla risoluzione del dispositivo o per adattarle a proporzioni diverse.
Questi rendering consentono alle organizzazioni di fornire esperienze personalizzate e ottimizzate per soddisfare diverse esigenze di pubblico. È possibile visualizzare e scaricare le rappresentazioni dinamiche in [!DNL Experience Manager Assets].

### Prima di iniziare

* Devi essere un utente con licenza di AEM Dynamic Medie.

* Utilizza [!UICONTROL Visualizzazione amministratore] per configurare:
   * [Profili immagine ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefiniti immagine](/help/assets/dynamic-media/managing-image-presets.md)

  È possibile [cambiare la visualizzazione](/help/assets/assets-view-introduction.md#how-to-access-assets-view) in un secondo momento per visualizzare in anteprima le rappresentazioni dinamiche nella visualizzazione Assets.

### Visualizzare e scaricare le rappresentazioni dinamiche {#view-renditions}

Per visualizzare o scaricare le rappresentazioni dinamiche delle immagini in [!DNL Experience Manager Assets], eseguire la procedura seguente:

1. Vai a **[!UICONTROL Gestione Assets]** > **[!UICONTROL Assets]**.

1. Passa alla cartella delle risorse applicabile.

1. Fai clic sull&#39;immagine da visualizzare e fai clic su **[!UICONTROL Dettagli]**.

1. Nel menu di destra, fai clic su **[!UICONTROL Rappresentazioni]**. <br> Il pannello **[!UICONTROL Rappresentazioni]** si apre con le rappresentazioni disponibili **[!UICONTROL Dinamiche]** e **[!UICONTROL Ritaglio avanzato]**.

   ![rappresentazioni dinamiche](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Fai clic sulla rappresentazione da visualizzare o scaricare.

1. Fai clic sull&#39;icona ![scarica](assets/do-not-localize/download-icon.png) accanto al rendering dinamico da scaricare. <br> In alternativa, è possibile selezionare la rappresentazione dell&#39;immagine e fare clic sull&#39;opzione **[!UICONTROL Scarica rappresentazione]** nella parte inferiore.

   Puoi fare clic sull&#39;icona ![scarica](assets/do-not-localize/download-icon.png) disponibile nella parte superiore della sezione **[!UICONTROL Ritaglio avanzato]** per scaricare tutte le rappresentazioni di Ritaglio avanzato disponibili per tale risorsa.

>[!NOTE]
>
>Le rappresentazioni dinamiche sono visibili solo se le risorse vengono caricate dalla vista Amministratore.
