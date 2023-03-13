---
title: Introduzione ad Assets as a [!DNL Cloud Service]
description: Novità di Assets as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 100%

---

# Introduzione ad Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] offre una soluzione PaaS nativa per il cloud, che consente alle aziende di eseguire le operazioni di gestione delle risorse digitali ed elementi multimediali dinamici in modo rapido ed efficace, ma anche di utilizzare funzionalità avanzate di nuova generazione, come AI/ML, dall’interno di un sistema sempre attuale, disponibile e in grado di apprendere.

L’assimilazione simultanea di più risorse o risorse complesse è un’attività ad alta intensità di risorse per un’istanza di authoring di Experience Manager. L’istanza primaria consuma notevoli risorse di CPU, memoria e I/O quando le risorse vengono aggiunte, elaborate o persino migrate. Tali problemi di prestazioni influiscono sull’esperienza di authoring e navigazione degli utenti finali.

Le aziende richiedono il supporto di un’ampia varietà di formati di file e risoluzioni di contenuti per casi d’uso multi-dispositivo, diversi ambienti geografici e multilingue. I requisiti di elaborazione e archiviazione delle risorse richiedono risorse e funzionalità che possono sovraccaricare una soluzione tradizionale. Talvolta, le limitazioni tecniche dell’elaborazione delle risorse non producono i risultati desiderati e in altri casi il costo di archiviazione rappresenta un ostacolo ai margini di profitto.

Per cominciare, comprendi i [vantaggi di un’offerta nativa per il cloud](#solution-benefits). Dai un’occhiata alle importanti [modifiche ad Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) che hanno anche avuto un impatto su Experience Manager Assets e che ha fatto seguito alle importanti [modifiche ad Assets](/help/assets/assets-cloud-changes.md).

Continua a leggere per conoscere i [dettagli delle nuove funzionalità di Assets](#whats-new-assets) e i [problemi noti](/help/release-notes/known-issues.md). Visualizza l’elenco delle [funzionalità obsolete o rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato rimosso in questa versione e l’[elenco delle funzionalità in arrivo](/help/release-notes/known-issues.md#upcoming-assets-capabilities) per sapere cosa verrà rilasciato. Infine, comprendi i termini di Experience Manager con l’aiuto di questo [glossario](/help/overview/terminology.md).

## Vantaggi della soluzione {#solution-benefits}

Di seguito sono riportati i vantaggi principali di Assets as a [!DNL Cloud Service]. Per ulteriori informazioni, consulta la [panoramica di Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Servizi cloud moderni per l’elaborazione delle risorse**: i nuovi microservizi per le risorse sono un’attività di elaborazione delle risorse basato su cloud, scalabile, affidabile e privo di problemi.
* **Altamente scalabile**: scalabilità elastica in tutti i tipi di implementazioni. Risorse praticamente illimitate disponibili on-demand, in base alle esigenze. Risparmia il costo del design eccessivo rispetto a un sistema tradizionale.
* **Software più recente**: sempre aggiornato. Tutti gli utenti dispongono solo del software più recente con tutte le patch, le funzioni, la sicurezza e le correzioni di bug disponibili. Sviluppatori e integratori lavorano con l’ultimo set di API senza problemi di supporto per più versioni.
* **Sempre online**: zero tempi di inattività (0dt), grazie all’istanza implementata in un cluster con backup e ridondanza. Anche gli aggiornamenti sono 0dt.
* **Monitoraggio costante**: il monitoraggio del sistema è automatizzato e i controlli e trigger integrati contribuiscono a mantenere le prestazioni, la disponibilità e la robustezza complessiva.
* **Implementazioni senza problemi**: le operazioni Experience Manager nel Cloud sono completamente automatizzate e non richiedono alcun intervento manuale. Per le distribuzioni automatizzate, il componente Cloud Manager (CM) automatizza la generazione di immagini Docker distribuibili contenenti il codice personalizzato.

## Nuove funzionalità di Assets {#whats-new-assets}

Le nuove funzionalità principali sono:

* [Microservizi per le risorse](/help/assets/asset-microservices-overview.md)
* [Metodi di caricamento delle risorse](/help/assets/add-assets.md)
