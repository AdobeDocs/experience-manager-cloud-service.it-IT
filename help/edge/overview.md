---
title: Panoramica di Edge Delivery Services
description: Scopri in che modo AEM as a Cloud Service può trarre vantaggio dalle prestazioni e dai punteggi impeccabili di Lighthouse offerti da Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 9829709a4558a2d0fd479c7c0fed979ee43937ea
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 37%

---


# Panoramica di Edge Delivery Services {#edge-delivery-services}

## Cos’è Edge Delivery Services? {#what-is-edge}

Edge Delivery Services è un framework moderno per la distribuzione dei contenuti che reimmagina come vengono creati e distribuiti i siti web, ottimizzandoli per velocità, semplicità e scalabilità. È una parte fondamentale di Adobe Experience Manager e consente esperienze digitali più veloci, rendendo il rendering e la distribuzione più vicini all’utente, alla periferia della rete.

Non sostituisce una rete CDN (Content Delivery Network), ma si integra perfettamente con la tua rete CDN o con la rete CDN [gestita da Adobe inclusa.](/help/implementing/dispatcher/cdn.md)

>[!TIP]
>
>**Desideri metterti subito all’opera?**
>
>Se lo desideri, avvia il tuo progetto Edge Delivery Services con l’authoring di AEM in meno di 30 minuti [consultando il tutorial su aem.live.](https://www.aem.live/developer/ue-tutorial)


## Perché Edge Delivery Services? {#why-edge}

### Maggiore reperibilità e aumento del traffico {#increase-traffic}

I siti web di Edge Delivery sono motori di ricerca ottimizzati (SEO) e motori generativi ottimizzati (GEO) per LLM. In questo modo si garantisce un&#39;elevata visibilità e la possibilità di individuare le fonti di traffico organico esistenti e future. L&#39;architettura **end-to-end basata sulle prestazioni** garantisce una piacevole esperienza del cliente, con un impatto positivo sul coinvolgimento.

### Efficienza degli sviluppatori {#developer-efficientcy}

Andate a vivere in giorni e settimane invece che in mesi e anni! Edge Delivery offre tutti gli strumenti **ai moderni sviluppatori web** piace: GitHub, sviluppo locale con ricaricamento automatico, prestazioni, semplicità e nessuna delle complicazioni: nessuna traspilazione, nessun bundle, nessuna configurazione, nessun sovraccarico.

La semplicità di Edge Delivery non richiede l’utilizzo di framework, strumenti o processi complicati, ideali per la creazione di codice AI. Usa HTML semplice, CSS moderno e Vanilla JavaScript per creare esperienze eccezionali più rapidamente che mai. Concentrarsi sul lavoro e dedicare meno tempo alla formazione e all&#39;apprendimento di nuovi strumenti.

Edge Delivery consente a ogni sviluppatore di ottenere un punteggio di 100 per un faro.

### Supporto per più origini di contenuto {#multiple-content-sources}

I contenuti di varie soluzioni possono essere integrati direttamente con Edge Delivery, **incluse tutte le istanze esistenti di AEM**. Gli autori possono gestire e **pubblicare contenuti da qualsiasi sistema, ad esempio da SharePoint ad Edge Delivery**, per velocizzare l&#39;attività grazie agli strumenti già noti.

### Architettura componibile {#composable-architeture}

Sia headless che headful, puoi fornire il contenuto giusto nel formato giusto e aggiungere la decorazione giusta per renderlo un’esperienza che si distingue in qualsiasi canale.

## Come funziona {#how-does-it-work}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Sostituisce AEM Publish/Dispatcher e il modo tradizionale di creare esperienze con i componenti core di AEM con una soluzione SaaS multi-cloud e un approccio di sviluppo front-end puro.

![Architettura di Edge Delivery](assets/aem-with-eds-architecture.png)

Edge Delivery Services sfrutta GitHub per consentirti di gestire e distribuire il codice direttamente dall’archivio GitHub. Il nuovo contenuto viene subito aggiunto senza che sia necessario eseguire una nuova build.

## Authoring {#authoring}

### Modifica nel contesto {#in-context-editing}

WYSIWYG [Universal Editor](/help/implementing/universal-editor/introduction.md) è una risorsa unica e personalizzabile per la modifica del contenuto in tempo reale e nel contesto con un&#39;anteprima visiva.

* Con l’authoring AEM e l’editor universale, puoi aumentare l’efficienza dell’authoring sia headless che headful.
* Puoi sfruttare le funzionalità complete di gestione dei contenuti di AEM, incluse quelle per flussi di lavoro e governance.
* Puoi sfruttare numerosi punti di estensione per supportare i tuoi processi e integrazioni.
* Le funzionalità del sito possono essere sviluppate utilizzando CSS e JavaScript in GitHub.

![Authoring AEM con l’editor universale](assets/wysiwyg-authoring.png)

### Modifica basata su documento {#document-based-editing}

[Un altro approccio è l&#39;authoring basato su documenti](https://www.aem.live/docs/authoring), in cui il contenuto viene gestito come documento. Microsoft Word è una scelta popolare in quanto molte aziende hanno SharePoint in posizione in cui viene creato il contenuto iniziale. Non è necessario apprendere un nuovo strumento e pubblicare contenuti direttamente da SharePoint e Word elimina il problema di copiare e incollare contenuti in AEM. I clienti senza SharePoint possono anche utilizzare Google Drive come alternativa.

## Telemetria operativa {#telemetry}

Adobe Experience Manager utilizza la [telemetria operativa](https://www.aem.live/docs/operational-telemetry) per raccogliere i dati delle operazioni strettamente necessari per individuare e risolvere i problemi funzionali e di prestazioni sui siti basati su Adobe Experience Manager. I dati di telemetria operativa possono essere utilizzati per diagnosticare problemi di prestazioni e per misurare l&#39;efficacia degli esperimenti. La telemetria operativa preserva la privacy dei visitatori attraverso il [campionamento](https://www.aem.live/docs/operational-telemetry#operational-telemetry-data-is-sampled) (verrà monitorata solo una piccola parte di tutte le visualizzazioni di pagina) e [esclusione giudiziosa di informazioni personali identificabili](https://www.aem.live/docs/operational-telemetry#what-data-is-being-collected) (PII).

## Inizia ad esplorare {#start-exploring}

Introduzione all’authoring in AEM con Universal Editor e Edge Delivery Services:

* Documentazione di Edge Delivery Services [Edge Delivery Services](https://www.aem.live)
* Per una panoramica sull’authoring AEM con l’edito universale, consulta il documento [Authoring con AEM per Edge Delivery Services](https://www.aem.live/docs/aem-authoring) nella documentazione di aem.live.
* Per una panoramica per gli sviluppatori, consulta il documento [Guida introduttiva - Tutorial per sviluppatori di editor universale](https://www.aem.live/developer/ue-tutorial) nella documentazione di aem.live.

## Edge Delivery Services e altri prodotti di Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services fa parte di Adobe Experience Manager. Di conseguenza, Edge Delivery Services e AEM Sites possono coesistere sullo stesso dominio, che rappresenta un caso d’uso comune per i siti web più grandi. Inoltre, le pagine AEM Sites possono utilizzare facilmente i contenuti di Edge Delivery Service e può succedere anche il contrario.

È inoltre possibile utilizzare Edge Delivery Services con [Adobe Target](https://www.aem.live/developer/target-integration) e [Launch.](https://experienceleague.adobe.com/it/docs/experience-platform/tags/home)

## Ottenere assistenza da Adobe {#getting-help}

Adobe fornisce tre livelli per aiutarti con Edge Delivery Services:

* Interazione con le [risorse della community](#community-resources) per rispondere a domande generali.
* Accesso al [canale di collaborazione sui prodotti](#collaboration-channel) per domande specifiche.
* [Registra un ticket di supporto](#support-ticket) per risolvere i problemi principali e critici **all&#39;interno del supporto contrattuale SLA**.

### Accesso alle risorse della community {#community-resources}

Adobe si impegna a fornire il miglior coinvolgimento della community e il miglior supporto per Edge Delivery Services, l’authoring AEM con l’editor universale e l’authoring basato su documenti.

* Aderisci alla [community Experience League](https://adobe.ly/3Q6kTKl) per rivolgere domande, condividere feedback, avviare discussioni, chiedere assistenza da esperti di Adobe e consulenti ed esperti di AEM e connetterti in tempo reale con altri utenti che condividono i tuoi stessi interessi.
* Segui il [canale Discord](https://discord.gg/aem-live), una piattaforma più informale per interazioni in tempo reale e rapidi scambi di idee.

### Registrare un ticket di supporto {#support-ticket}

{{support-ticket}}
