---
title: Dashboard delle prestazioni CDN
description: Scopri in che modo Cloud Manager valuta le prestazioni della rete CDN (Content Delivery Network) e cosa puoi imparare dal dashboard.
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 4%

---

# Dashboard prestazioni CDN {#cdn-performance}

Scopri in che modo Cloud Manager valuta le prestazioni della rete CDN (Content Delivery Network) e cosa puoi imparare dal dashboard.

## Panoramica {#overview}

Ogni programma Cloud Manager ha un dashboard delle prestazioni CDN. Questa dashboard presenta un punteggio complessivo per le prestazioni CDN, oltre a tendenze, avvisi e suggerimenti per eventuali miglioramenti.

![Dashboard delle prestazioni CDN](assets/cdn-performance-dashboard.png)

## Accedere al dashboard {#accessing}

La dashboard CDN è disponibile nella pagina di panoramica di ogni programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** fare clic sul programma di cui si desidera visualizzare il dashboard CDN.

   ![Pagina Programmi](assets/my-programs.png)

1. Nella pagina **Panoramica programma** del programma, scorri verso il basso sotto le schede **Ambienti** e **Pipeline** per visualizzare la scheda **Prestazioni**.

   ![Prestazioni](assets/cdn-performance-overview.png)

## Utilizzare il dashboard {#using}

La dashboard presenta un punteggio complessivo per le prestazioni CDN, oltre a tendenze, avvisi e suggerimenti per miglioramenti, in base alle esigenze.

![Dashboard delle prestazioni CDN](assets/cdn-performance-dashboard.png)

Per informazioni dettagliate sulle prestazioni CDN e suggerimenti su come migliorarle, fai clic su **Visualizza tendenza**.

![Tendenza delle prestazioni](assets/cdn-performance-trend.png)

Fai clic su **Visualizza** sotto il grafico per modificare l&#39;intervallo di tempo del grafico.

Per suggerimenti su come migliorare le prestazioni CDN, seleziona la scheda **Consigli**.

![Consigli CDN](assets/cdn-performance-recommendations.png)

Fai clic sulla freccia accanto a qualsiasi consiglio nell’elenco per visualizzare i dettagli su quali passi intraprendere per migliorare e la causa del problema.

## Definizione hit cache {#cache-hit}

Il rapporto di hit della cache è una misurazione del numero di richieste di contenuto che una cache può compilare correttamente, rispetto al numero di richieste che riceve. Maggiore è il rapporto cache-hit, migliori sono le prestazioni di una rete CDN.

>[!TIP]
>
>Adobe consiglia agli utenti di puntare a un rapporto di hit della cache del 99%.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Hit** - Dati richiesti dalla cache e trovati.
* **Errore**. Dati richiesti dalla cache non trovati.
* **Passaggio**: i dati vengono richiesti dalla cache e non sono impostati per la memorizzazione in cache di tali dati.
* **Altro** - Tutte le richieste di dati dalla cache che non corrispondono a nessun altro caso.

Le metriche della cache vengono aggiornate ogni 24 ore.

>[!TIP]
>
>Per ulteriori dettagli sull&#39;interazione di Cloud Manager e CDN con Dispatcher, vedere [Memorizzazione in cache in AEM as a Cloud Service](/help/implementing/dispatcher/caching.md).
