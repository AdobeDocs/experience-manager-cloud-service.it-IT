---
title: Visualizzare e gestire le rappresentazioni in Experience Manager Assets
description: Scopri come AEM Assets e Dynamic Medie semplificano la gestione efficace delle immagini con rappresentazioni statiche e dinamiche.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
source-git-commit: 4627eb00ba910d1ad2920db15a87761bd7e4a0c0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Visualizzare e gestire le rappresentazioni in Experience Manager Assets{#renditions}

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

* Utilizzare [!UICONTROL Visualizzazione amministratore] per impostare:
   * [Profili immagine ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Predefiniti immagine](/help/assets/dynamic-media/managing-image-presets.md)

  È possibile [cambiare visualizzazione](/help/assets/assets-view-introduction.md#how-to-access-assets-view) per visualizzare in anteprima le rappresentazioni dinamiche nella vista Risorse.

### Visualizzare e scaricare le rappresentazioni dinamiche {#view-renditions}

Per visualizzare o scaricare rappresentazioni dinamiche di immagini in [!DNL Experience Manager Assets], effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Gestione risorse]** > **[!UICONTROL Risorse]**.

1. Passa alla cartella delle risorse applicabile.

1. Fai clic sull’immagine da visualizzare e fai clic su **[!UICONTROL Dettagli]**.

1. Nel menu di destra, fai clic su **[!UICONTROL Rappresentazioni]**. <br> Il **[!UICONTROL Rappresentazioni]** viene aperto con il **[!UICONTROL Dinamico]** e **[!UICONTROL Ritaglio avanzato]** copie trasformate.

   ![rappresentazioni dinamiche](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Fai clic sulla rappresentazione da visualizzare o scaricare.

1. Fai clic su ![icona di download](assets/do-not-localize/download-icon.png) accanto alla rappresentazione dinamica da scaricare. <br> In alternativa, è possibile selezionare la rappresentazione dell&#39;immagine e fare clic su **[!UICONTROL Scarica rappresentazione]** nella parte inferiore.

   Puoi fare clic su ![icona di download](assets/do-not-localize/download-icon.png) icona disponibile nella parte superiore di **[!UICONTROL Ritaglio avanzato]** per scaricare tutte le rappresentazioni di ritaglio avanzato disponibili per tale risorsa.

>[!NOTE]
>
>Le rappresentazioni dinamiche sono visibili solo se le risorse vengono caricate dalla vista Amministratore.
