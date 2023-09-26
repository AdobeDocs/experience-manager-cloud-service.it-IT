---
title: Introduzione ad Assets as a [!DNL Cloud Service]
description: Novità e vantaggi di Experience Manager Assets as a [!DNL Cloud Service]. Una soluzione PaaS nativa per il cloud per le aziende.
contentOwner: AK
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: a4601d95076d37ed5df79b7c9dabb8beab8353d0
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 88%

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

* **Vista Amministratore**: l’interfaccia utente esistente di Assets as a Cloud Service. Utilizza la vista Amministratore per tutte le funzionalità avanzate di gestione risorse, tra cui integrazioni, flussi di lavoro, automazione dei contenuti, pubblicazione e altro ancora.

* **Vista Risorse**: esperienza Adobe leggera di gestione delle risorse per archiviare, gestire, scoprire e utilizzare le risorse digitali. Interfaccia utente semplificata con funzionalità essenziali per la gestione delle risorse. Progettata per gli utenti di DAM leggeri con particolare attenzione al caricamento, alla gestione dei metadati, alla ricerca, al download e alla condivisione.

Gli utenti con accesso alla vista Amministratore possono accedere anche alla vista Risorse. L’interfaccia utente semplificata di vista Risorse agevola la gestione, l’individuazione e la distribuzione delle risorse digitali. Un ampio insieme di utenti con diverse funzioni, compresi i team creativi, di marketing e line-of-business, possono collaborare alle risorse e accedere alle risorse approvate, quando e dove ne hanno bisogno. Molti utenti di DAM occasionali preferiscono la vista Risorse perché contiene solo un sottoinsieme di funzioni. L’esperienza è destinata ai creativi, a chi utilizza le risorse di sola lettura e agli utenti di DAM più leggeri.

Librerie, sviluppatori e utenti con privilegi avanzati DAM possono continuare a utilizzare la vista Amministratore o passare da un’interfaccia utente all’altra, in base alle esigenze. Puoi selezionare l’esperienza che funziona meglio per il tuo ruolo.

![add-tags](assets/newui-overview.svg)

Per informazioni su come accedere alla vista Risorse e su alcune delle semplificazioni offerte rispetto alla vista Amministratore, consulta [Introduzione alla vista Risorse](/help/assets/assets-view-introduction.md).

## Integrazione con l’authoring basato su documenti per i Edge Delivery Services {#integrate-doc-authoring-edge-and-assets}

Edge Delivery consente di creare siti web veloci e coinvolgenti in cui gli autori possono aggiornare e pubblicare rapidamente i contenuti e nuovi siti possono essere avviati rapidamente.

Integra AEM Assets con l’authoring basato su documenti per Edge Delivery Services per consentire agli autori di siti web di utilizzare le immagini disponibili negli archivi AEM Assets durante l’authoring di documenti nei documenti Microsoft Word o Google. Per ulteriori informazioni, consulta [Integrare AEM Assets con l’authoring basato su documenti](/help/edge/using.md#integrate-assets-edge).

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
