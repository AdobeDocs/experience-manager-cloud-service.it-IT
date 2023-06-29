---
title: Introduzione ad Assets as a [!DNL Cloud Service]
description: Novità di Assets as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: d0deca8acbf6049d5be6c27275eedf9b52b27658
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 68%

---

# Introduzione ad Assets as a [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] offre una soluzione PaaS nativa per il cloud, che consente alle aziende di eseguire le operazioni di gestione delle risorse digitali ed elementi multimediali dinamici in modo rapido ed efficace, ma anche di utilizzare funzionalità avanzate di nuova generazione, come AI/ML, dall’interno di un sistema sempre attuale, disponibile e in grado di apprendere.

L’assimilazione simultanea di più risorse o risorse complesse è un’attività ad alta intensità di risorse per un’istanza di authoring di Experience Manager. L’istanza primaria consuma notevoli risorse di CPU, memoria e I/O quando le risorse vengono aggiunte, elaborate o persino migrate. Tali problemi di prestazioni influiscono sull’esperienza di authoring e navigazione degli utenti finali.

Le aziende richiedono il supporto di un’ampia varietà di formati di file e risoluzioni di contenuti per casi d’uso multi-dispositivo, diversi ambienti geografici e multilingue. I requisiti di elaborazione e archiviazione delle risorse richiedono risorse e funzionalità che possono sovraccaricare una soluzione tradizionale. Talvolta, le limitazioni tecniche dell’elaborazione delle risorse non producono i risultati desiderati e in altri casi il costo di archiviazione rappresenta un ostacolo ai margini di profitto.

Per cominciare, comprendi i [vantaggi di un’offerta nativa per il cloud](#solution-benefits). Dai un’occhiata alle importanti [modifiche ad Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) che hanno anche avuto un impatto su Experience Manager Assets e che ha fatto seguito alle importanti [modifiche ad Assets](/help/assets/assets-cloud-changes.md).

Continua a leggere per conoscere i [dettagli delle nuove funzionalità di Assets](#whats-new-assets) e i [problemi noti](/help/release-notes/maintenance/latest.md). Visualizza un elenco di [funzionalità obsolete o rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato rimosso in questa versione. Infine, comprendi i termini di Experience Manager con l’aiuto di questo [glossario](/help/overview/terminology.md).

## Vantaggi della soluzione {#solution-benefits}

Di seguito sono riportati i vantaggi principali di Assets as a [!DNL Cloud Service]. Per ulteriori informazioni, consulta la [panoramica di Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Servizi cloud moderni per l’elaborazione delle risorse**: i nuovi microservizi per le risorse sono un’attività di elaborazione delle risorse basato su cloud, scalabile, affidabile e privo di problemi.
* **Altamente scalabile**: scalabilità elastica in tutti i tipi di implementazioni. Risorse praticamente illimitate disponibili on-demand, in base alle esigenze. Risparmia il costo del design eccessivo rispetto a un sistema tradizionale.
* **Software più recente**: sempre aggiornato. Tutti gli utenti dispongono solo del software più recente con tutte le patch, le funzioni, la sicurezza e le correzioni di bug disponibili. Sviluppatori e integratori lavorano con l’ultimo set di API senza problemi di supporto per più versioni.
* **Sempre online**: zero tempi di inattività (0dt), grazie all’istanza implementata in un cluster con backup e ridondanza. Anche gli aggiornamenti sono 0dt.
* **Monitoraggio costante**: il monitoraggio del sistema è automatizzato e i controlli e trigger integrati contribuiscono a mantenere le prestazioni, la disponibilità e la robustezza complessiva.
* **Implementazioni senza problemi**: le operazioni Experience Manager nel Cloud sono completamente automatizzate e non richiedono alcun intervento manuale. Per le distribuzioni automatizzate, il componente Cloud Manager (CM) automatizza la generazione di immagini Docker distribuibili contenenti il codice personalizzato.

## Esperienze disponibili basate su utenti tipo {#persona-based-experiences}

Adobe offre una solida soluzione di gestione delle risorse digitali (DAM) che consente di ottenere il massimo dalle risorse digitali. Adobe Experience Manager Assets dispone di due esperienze separate che utilizzano lo stesso archivio Cloud Services:

* **Visualizzazione amministratore**: interfaccia utente esistente di Assets as a Cloud Service. Utilizza la Vista amministratore per tutte le funzionalità avanzate di gestione delle risorse, inclusi integrazioni, flussi di lavoro, automazione dei contenuti, pubblicazione e altro ancora.

* **Visualizzazione risorse**: esperienza di gestione delle risorse leggera di Adobe per archiviare, gestire, individuare e utilizzare le risorse digitali. Interfaccia utente semplificata con funzionalità essenziali per la gestione delle risorse. Progettato per gli utenti DAM leggeri con particolare attenzione a caricamento, gestione dei metadati, ricerca, download e condivisione.

Gli utenti con accesso alla vista Amministratore possono accedere anche alla vista Risorse. La visualizzazione Assets offre un’interfaccia utente semplificata per gestire, individuare e distribuire facilmente le risorse digitali. Un’ampia gamma di utenti con diverse funzioni, tra cui creativi, team di marketing e line-of-business possono collaborare alle risorse e accedere alle risorse approvate, quando e dove ne hanno bisogno. Molti utenti DAM occasionali preferiscono la vista Risorse perché contiene solo un sottoinsieme di funzioni. L’esperienza è destinata ai creativi, ai consumatori di risorse di sola lettura e agli utenti DAM più leggeri.

Librerie DAM, sviluppatori e utenti con privilegi avanzati possono continuare a utilizzare la visualizzazione Amministratore o passare da un’interfaccia utente all’altra, in base alle esigenze. Puoi selezionare l’esperienza che funziona meglio per il tuo ruolo.

![add-tags](assets/newui-overview.svg)

Per informazioni su come accedere alla vista Risorse e su alcune delle semplificazioni offerte rispetto alla vista Amministrazione, consulta [Introduzione alla vista Risorse](/help/assets/assets-view-introduction.md).

## Nuove funzionalità di Assets {#whats-new-assets}

Le nuove funzionalità principali sono:

* [Microservizi per le risorse](/help/assets/asset-microservices-overview.md)
* [Metodi di caricamento delle risorse](/help/assets/add-assets.md)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
