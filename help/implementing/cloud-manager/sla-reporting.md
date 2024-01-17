---
title: Generazione rapporti SLA
description: Scopri come visualizzare le prestazioni dell’ambiente di produzione AEM relative al contratto del livello di servizio (SLA) sottoscritto.
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 88%

---


# Generazione rapporti SLA {#sla-reporting}

Scopri come visualizzare le prestazioni dell’ambiente di produzione AEM relative al contratto del livello di servizio (SLA) sottoscritto.

## Introduzione {#introduction}

I dati della generazione rapporti SLA sono disponibili per ogni programma di produzione tramite la scheda **Rapporti**. Per accedere, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** selezionare il programma.

1. Dalla pagina **Panoramica**, accedi alla scheda **Rapporti**.

1. Fai clic sull’anno desiderato per visualizzare i dati SLA riportati nel grafico.

![Esempio di grafico SLA](assets/sla-reporting-1.png)

Sposta il cursore su un punto dati per visualizzarne i valori specifici.

![Visualizzazione dei dati dettagliati](assets/sla-reporting-b.png)

## Metriche SLA {#sla-metrics}

Il grafico dell’anno selezionato include diversi set di dati.

* **Livello di pubblicazione da contratto**: si tratta dello SLA definito nel contratto con Adobe per il livello di pubblicazione.

* **Livello di pubblicazione effettivo**: si tratta del tempo di attività misurato relativo al livello di pubblicazione della produzione, che tiene conto dei problemi attribuibili a Adobe o ai relativi produttori.

* **Livello di creazione da contratto**: si tratta dello SLA definito nel contratto con Adobe per il livello di creazione.

* **Livello di creazione effettivo**: si tratta del tempo di attività misurato relativo al livello di creazione della produzione, che tiene conto dei problemi attribuibili a Adobe o ai relativi produttori.

## Analisi degli eventi {#event-analysis}

La sezione **Analisi degli eventi** sotto il grafico mostra i problemi relativi al programma che si sono verificati durante l’anno selezionato.

Ogni problema presenta un intervallo di tempo, una causa e una serie di commenti.

![Esempio di analisi degli eventi](assets/sla-reporting-c.png)
