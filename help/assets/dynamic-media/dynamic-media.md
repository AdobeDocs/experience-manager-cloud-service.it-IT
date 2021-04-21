---
title: Utilizzo di Dynamic Media
description: Scopri come utilizzare Dynamic Media per distribuire risorse da utilizzare sui siti web, mobili e social.
role: Administrator,Business Practitioner
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 14%

---

# Utilizzo di Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) permette di fornire on-demand risorse visive di marketing e merchandising, ridimensionandole automaticamente per siti web, dispositivi mobili e piattaforme social. Utilizzando un set di risorse primarie, Dynamic Media genera e distribuisce più varianti di contenuti avanzati in tempo reale attraverso la sua rete globale, scalabile e ottimizzata per le prestazioni.

Dynamic Media offre esperienze di visualizzazione interattive, tra cui zoom, rotazione a 360° e video. Dynamic Media integra in modo esclusivo i flussi di lavoro della soluzione Adobe Experience Manager per la gestione delle risorse digitali (Assets) per semplificare e semplificare il processo di gestione delle campagne digitali.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Operazioni possibili con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media consente di gestire le risorse prima di pubblicarle. Come lavorare con le risorse in generale viene descritto in dettaglio in [Utilizzo di risorse digitali](/help/assets/manage-digital-assets.md). Gli argomenti generali includono il caricamento, il download, la modifica e la pubblicazione delle risorse; visualizzazione e modifica delle proprietà e ricerca delle risorse.

Le funzioni solo per Dynamic Media includono quanto segue:

* [Banner a carosello](carousel-banners.md)
* [Set di immagini](image-sets.md)
* [Immagini interattive](interactive-images.md)
* [Video interattivi](interactive-videos.md)
* [Set di file multimediali diversi](mixed-media-sets.md)
* [Immagini panoramiche](panoramic-images.md)

* [Set 360 gradi](spin-sets.md)
* [Video](video.md)
* [Distribuzione di risorse Dynamic Media](delivering-dynamic-media-assets.md)
* [Gestione delle risorse](managing-assets.md)
* [Utilizzo delle visualizzazioni rapide per creare finestre pop-up personalizzate](custom-pop-ups.md)

Vedere anche [Configurazione di Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media abilitato e Dynamic Media disabilitato {#dynamic-media-on-versus-dynamic-media-off}

È possibile verificare se Dynamic Media è abilitato (attivato) in base alle seguenti caratteristiche:

* Le rappresentazioni dinamiche sono disponibili quando si scaricano o visualizzano in anteprima le risorse.
* Sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.
* Vengono create rappresentazioni PTIFF.

Quando fai clic su una risorsa immagine, la visualizzazione della risorsa è diversa con Dynamic Media abilitato. Dynamic Media utilizza i visualizzatori HTML5 on-demand.

### Rendering dinamici {#dynamic-renditions}

Le rappresentazioni dinamiche come i predefiniti per immagini e visualizzatori (in **[!UICONTROL Dynamic]**) sono disponibili quando Dynamic Media è abilitato.

![chlimage_1-358](assets/chlimage_1-358.png)

### Set di immagini, set 360 gradi, set di file multimediali diversi {#image-sets-spins-sets-mixed-media-sets}

Se Dynamic Media è abilitato, sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rendering PTIFF {#ptiff-renditions}

Le risorse abilitate per Dynamic Media includono `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modifica delle visualizzazioni delle risorse {#asset-views-change}

Con Dynamic Media abilitato, è possibile ingrandire e ridurre facendo clic sui pulsanti `+` e `-`. Puoi anche fare clic o toccare per ingrandire una determinata area. Ripristina la versione originale consente di visualizzare l’immagine a schermo intero facendo clic sulle frecce diagonali. Dynamic Media abilitato si presenta così:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media disattivato è possibile ingrandire e ridurre e ripristinare le dimensioni originali:

![chlimage_1-362](assets/chlimage_1-362.png)
