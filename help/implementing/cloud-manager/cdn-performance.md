---
title: Dashboard delle prestazioni CDN
description: Scopri in che modo Cloud Manager valuta le prestazioni della rete di distribuzione dei contenuti (CDN) e cosa puoi imparare dal dashboard.
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 4%

---

# Dashboard delle prestazioni CDN {#cdn-performance}

Scopri in che modo Cloud Manager valuta le prestazioni della rete di distribuzione dei contenuti (CDN) e cosa puoi imparare dal dashboard.

## Panoramica {#overview}

Ogni programma di Cloud Manager ha una dashboard delle prestazioni CDN. Questa dashboard presenta un punteggio complessivo per le prestazioni CDN, oltre a tendenze, avvisi e suggerimenti per eventuali miglioramenti.

![Dashboard delle prestazioni CDN](assets/cdn-performance-dashboard.png)

## Accesso al dashboard {#accessing}

La dashboard CDN è disponibile nella pagina di panoramica di ogni programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** , tocca o fai clic sul programma di cui desideri visualizzare il dashboard CDN.

   ![Pagina I miei programmi](assets/my-programs.png)

1. Il giorno **Panoramica del programma** del programma, scorri verso il basso sotto la **Ambienti** e **Pipeline** schede per visualizzare **Prestazioni** Card.

   ![Prestazioni](assets/cdn-performance-overview.png)

## Utilizzo del dashboard {#using}

La dashboard presenta un punteggio complessivo per le prestazioni CDN, oltre a tendenze, avvisi e suggerimenti per miglioramenti, in base alle esigenze.

![Dashboard delle prestazioni CDN](assets/cdn-performance-dashboard.png)

Per informazioni dettagliate sulle prestazioni CDN e per suggerimenti su come migliorarle, tocca o fai clic su **Visualizza tendenza**.

![Tendenza delle prestazioni](assets/cdn-performance-trend.png)

Tocca o fai clic su **Visualizza** sotto il grafico per modificare l&#39;intervallo di tempo del grafico.

Per suggerimenti su come migliorare le prestazioni CDN, seleziona la **Recommendations** scheda.

![Consigli CDN](assets/cdn-performance-recommendations.png)

Tocca o fai clic sulla freccia accanto a qualsiasi consiglio nell’elenco per visualizzare i dettagli sui passaggi da intraprendere per migliorare e la causa del problema.

## Definizione hit cache {#cache-hit}

Il rapporto di hit della cache è una misurazione del numero di richieste di contenuto che una cache può compilare correttamente, rispetto al numero di richieste che riceve. Maggiore è il rapporto cache-hit, migliori sono le prestazioni di una rete CDN.

>[!TIP]
>
>L’Adobe consiglia agli utenti di puntare a un rapporto di hit della cache del 99%.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Hit** : i dati vengono richiesti dalla cache e trovati.
* **Signorina** : i dati vengono richiesti dalla cache e non vengono trovati.
* **Superato** - I dati vengono richiesti dalla cache ed è impostato per non memorizzarli in cache in nessun caso.
* **Altro** : tutte le richieste di dati dalla cache che non corrispondono a nessun altro caso.

Le metriche della cache vengono aggiornate ogni 24 ore.

>[!TIP]
>
>Per ulteriori dettagli su come Cloud Manager e la rete CDN interagiscono con Dispatcher, consulta il documento [Memorizzazione in cache in AEM as a Cloud Service.](/help/implementing/dispatcher/caching.md)
