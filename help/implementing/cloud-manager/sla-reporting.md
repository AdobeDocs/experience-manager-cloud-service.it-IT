---
title: Generazione rapporti SLA
description: Scopri come visualizzare le prestazioni dell’ambiente di produzione AEM rispetto al contratto di assistenza a livello di contratto (SLA).
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Generazione rapporti SLA {#sla-reporting}

Scopri come visualizzare le prestazioni dell’ambiente di produzione AEM rispetto al contratto di assistenza a livello di contratto (SLA).

## Introduzione {#introduction}

I dati di reporting SLA sono disponibili per ogni programma di produzione tramite **Rapporti** scheda . Segui questi passaggi per accedere.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Rapporti** dalla scheda **Panoramica** pagina.

1. Fai clic sull’anno desiderato per visualizzare i dati SLA sotto forma di grafico.

![Esempio di grafico SLA](assets/sla-reporting-1.png)

Sposta il cursore su un punto dati per visualizzare i valori specifici di quel punto.

![Visualizzazione di dati dettagliati](assets/sla-reporting-b.png)

## Metriche SLA {#sla-metrics}

Il grafico dell’anno selezionato include una serie di set di dati.

* **Pubblica contratto livello** - Questo è lo SLA definito nel contratto con l’Adobe per il livello di pubblicazione.

* **Livello di pubblicazione effettivo** - Si tratta del tempo di attività misurato degli incidenti di factoring del livello di pubblicazione della produzione causati da fornitori di Adobi o Adobi.

* **Contratto livello autore** - Questo è lo SLA definito nel contratto con Adobe per il livello di authoring.

* **Livello autore effettivo** - Si tratta del tempo di attività misurato degli incidenti di factoring del livello di authoring di produzione causati da fornitori di Adobi o Adobi.

## Analisi degli eventi {#event-analysis}

La **Analisi degli eventi** la sezione sotto il grafico mostra l&#39;insieme di incidenti verificatisi per il programma durante l&#39;anno selezionato.

Ogni incidente ha un intervallo di tempo, una causa e una serie di commenti.

![Esempio di analisi degli eventi](assets/sla-reporting-c.png)
