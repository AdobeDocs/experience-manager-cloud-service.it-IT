---
title: Utilizzo di Dynamic Media
description: Scopri come utilizzare Dynamic Medie per distribuire risorse da utilizzare su siti web, mobili e social network.
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 8%

---

# Utilizzo di Dynamic Media {#working-with-dynamic-media}

[Dynamic Medie](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) consente di fornire risorse di marketing e merchandising visive avanzate su richiesta, scalabili automaticamente per l&#39;utilizzo su siti Web, mobili e social network. Utilizzando un set di risorse di origine principale, Dynamic Medie genera e distribuisce in tempo reale più varianti di rich content attraverso la sua rete globale, scalabile e ottimizzata per le prestazioni.

Dynamic Medie offre esperienze di visualizzazione interattiva, tra cui zoom, 360° rotazione e video. Dynamic Medie incorpora in modo esclusivo i flussi di lavoro della soluzione Adobe Experience Manager di gestione delle risorse digitali (Assets) per semplificare e semplificare il processo di gestione delle campagne digitali.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Operazioni possibili con Dynamic Medie {#what-you-can-do-with-dynamic-media}

Dynamic Medie consente di gestire le risorse prima di pubblicarle. Le modalità di utilizzo delle risorse in generale sono descritte in dettaglio in [Utilizzo di Digital Assets](/help/assets/manage-digital-assets.md). Gli argomenti generali includono il caricamento, il download, la modifica e la pubblicazione delle risorse, la visualizzazione e la modifica delle proprietà e la ricerca delle risorse.

Le funzioni disponibili solo in Dynamic Medie includono:

* [Banner a carosello](carousel-banners.md)
* [Set di immagini](image-sets.md)
* [Immagini interattive](interactive-images.md)
* [Video interattivi](interactive-videos.md)
* [Set di file multimediali diversi](mixed-media-sets.md)
* [Immagini panoramiche](panoramic-images.md)

* [Set 360 gradi](spin-sets.md)
* [Video](video.md)
* [Distribuzione di Dynamic Medie Assets](delivering-dynamic-media-assets.md)
* [Gestione di Assets](managing-assets.md)
* [Utilizzo delle visualizzazioni rapide per creare finestre popup personalizzate](custom-pop-ups.md)

Vedere anche [Configurazione di Dynamic Medie](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Medie abilitato e Dynamic Medie disabilitato {#dynamic-media-on-versus-dynamic-media-off}

È possibile verificare se Dynamic Medie è abilitato (attivato) in base alle seguenti caratteristiche:

* Le rappresentazioni dinamiche sono disponibili quando si scaricano o si visualizzano in anteprima le risorse.
* Sono disponibili set di immagini, set 360 gradi, set di file multimediali diversi.
* Vengono creati rendering PTIFF.

Quando fai clic su una risorsa di immagine, la visualizzazione della risorsa cambia quando è attivato Dynamic Medie. Dynamic Medie utilizza i visualizzatori HTML5 on-demand.

### Rappresentazioni dinamiche {#dynamic-renditions}

Le rappresentazioni dinamiche, come i predefiniti immagine e visualizzatore (in **[!UICONTROL Dinamico]**), sono disponibili quando Dynamic Medie è abilitato.

![chlimage_1-358](assets/chlimage_1-358.png)

### Set di immagini, set 360 gradi, set di file multimediali diversi {#image-sets-spins-sets-mixed-media-sets}

Se Dynamic Medie è abilitato, sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rappresentazioni PTIFF {#ptiff-renditions}

Le risorse abilitate per Dynamic Medie includono `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modifica visualizzazioni risorse {#asset-views-change}

Se Dynamic Medie è abilitato, è possibile ingrandire e ridurre facendo clic sui pulsanti `+` e `-`. È inoltre possibile selezionare di eseguire lo zoom in un&#39;area specifica. Ripristina consente di tornare alla versione originale e di visualizzare l&#39;immagine a schermo intero facendo clic sulle frecce diagonali. Dynamic Medie abilitato viene visualizzato come segue:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Medie disabilitato puoi ingrandire e ridurre e ripristinare le dimensioni originali:

![chlimage_1-362](assets/chlimage_1-362.png)
