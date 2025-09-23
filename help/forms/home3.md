---
title: AEM Forms as a Cloud Service - Piattaforma modulo digitale
description: Crea, integra e ottimizza i moduli digitali con componenti modulari. Scegli tra moduli adattivi, connettori dati, automazione del flusso di lavoro, strumenti di analisi e gestione per creare esperienze di moduli efficaci.
landing-page-description: Piattaforma modulare per moduli digitali con componenti indipendenti per la creazione di moduli, l’integrazione di dati, l’automazione dei processi, l’analisi e la governance.
keywords: AEM Forms, moduli digitali, generatore di moduli, moduli adattivi, integrazione di moduli, automazione dei flussi di lavoro, analisi dei moduli, servizi documentali
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
source-git-commit: 51d9fed937ea5f12544ed476974d2812843fb457
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 1%

---


# AEM Forms as a Cloud Service {#aem-forms-platform}

Crea, integra e ottimizza i moduli digitali con componenti modulari. AEM Forms fornisce prodotti indipendenti che lavorano insieme o in modo indipendente per creare esperienze di moduli efficaci per qualsiasi esigenza aziendale.

Scegli i componenti necessari: dalla semplice creazione di moduli ai flussi di lavoro complessi per documenti, all’integrazione di dati e all’analisi avanzata.

## Novità {#whats-new}

**Elementi di rilievo della versione più recente:**

- **Componente input data e ora** - Input utente avanzato con interfaccia calendario e orologio
- **Sicurezza avanzata caricamento file** - Convalida automatica e controllo del tipo di contenuto
- **È stata migliorata la gestione degli errori** - È stato migliorato il debug con codici di errore specifici per le azioni di invio personalizzate
- **Miglioramenti al documento record** - Opzione per escludere i campi nascosti per una generazione di documenti più pulita

**Funzioni Pre-Release:**

- **Supporto per il formato AFP** - Funzionalità di stampa di livello Enterprise con API di comunicazione
- **Miglioramenti all&#39;editor di regole** - Supporto moderno di JavaScript e variabili dinamiche
- **Metodi di convalida migliorati** - Miglioramenti alla convalida a livello di pannello, campo e modulo

[Visualizzare le note sulla versione complete →](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Programma di accesso in anteprima {#early-access}

Accesso esclusivo alle innovazioni AEM Forms all’avanguardia:

- **🤖AEM Forms AI Assistant** - IA generativa per la creazione e l&#39;ottimizzazione automatizzate dei moduli
- **✍️componente firma scarabocchio** - Acquisizione diretta della firma nei moduli
- Integrazione diretta API **🔗** - Connessione alle API senza configurazione del modello dati modulo
- **📊Ottimizzazione Forms** - Miglioramenti all&#39;analisi delle prestazioni e alla conversione basati su IA

[Richiedi accesso →](mailto:aem-forms-ea@adobe.com) | [Ulteriori informazioni →](/help/forms/early-access-ea-features.md)

## Creazione e authoring di 📋 moduli {#form-creation}

Crea moduli utilizzando l’approccio di authoring più adatto alle tue esigenze e ai tuoi requisiti tecnici.

### Componente core Forms {#core-components}

| **Componente core Forms** |
|---|
| Creazione di moduli moderni e reattivi con gli standard web più recenti. Crea moduli adattivi che funzionano automaticamente tra dispositivi diversi e producono moduli headless per la distribuzione basata su API. |
| **Funzionamento:** Generatore di moduli con funzionalità di trascinamento della selezione con componenti moderni, progettazione reattiva automatica e funzionalità di accessibilità incorporate. |
| **Quando utilizzare:** nuovi progetti, esperienze Web moderne, distribuzione di moduli headless, progettazione basata su dispositivi mobili. |
| ✅ Progettazione reattiva ✅ Conformità all&#39;accessibilità ✅ Funzionalità headless ✅ Componenti dell&#39;interfaccia utente moderni |
| [Introduzione ai componenti core →](/help/forms/creating-adaptive-form-core-components.md) |

### Forms del componente Foundation {#foundation-components}

| **Componente Foundation Forms** |
|---|
| Approccio consolidato per la creazione di moduli per i progetti esistenti e le integrazioni legacy. Componenti collaudati con ampie opzioni di personalizzazione. |
| **Funzionamento:** creazione di moduli adattivi tradizionali con una libreria di componenti completa e ampie funzionalità di personalizzazione. |
| **Quando utilizzare:** progetti esistenti, integrazione di sistema legacy, requisiti di personalizzazione specifici, flussi di lavoro stabiliti. |
| ✅ Libreria estesa di componenti ✅ Personalizzazione approfondita ✅ Compatibilità legacy ✅ Stabilità comprovata |
| [Introduzione ai componenti Foundation →](/help/forms/creating-adaptive-form.md) |

### Edge Delivery Forms {#edge-delivery}

| **Edge Delivery Forms** |
|---|
| Creazione di moduli ad alte prestazioni tramite strumenti familiari come Microsoft Excel. Raggiungere velocità di carico eccezionali e prestazioni SEO. |
| **Funzionamento:** creare moduli utilizzando fogli di calcolo Excel, pubblicare su reti di consegna Edge ad alte prestazioni con punteggi ottimali di Google Lighthouse. |
| **Quando utilizzare:** applicazioni critiche dal punto di vista delle prestazioni, progetti incentrati sull&#39;ottimizzazione SEO, creazione di moduli basati sull&#39;autore di contenuto e distribuzione globale dei contenuti. |
| ⚡ Authoring basato su Excel ⚡ Caricamento rapido ⚡ SEO ottimale ⚡ Consegna CDN globale |
| [Introduzione ad Edge Delivery →](/help/edge/docs/forms/overview.md) |

### Moduli HTML5 {#html5-forms}

| **Moduli HTML5** |
|---|
| Rendering di moduli basati su XFA come HTML5 per dispositivi mobili e browser legacy. Mantenere la logica dei moduli fornendo al tempo stesso un’esperienza mobile nativa. |
| **Funzionamento:** convertire i modelli di modulo XFA in moduli HTML5 con esperienza mobile nativa e compatibilità tra browser diversi. |
| **Quando utilizzare:** modernizzazione moduli XFA, ottimizzazione mobile, supporto browser legacy, investimenti XDP esistenti. |
| 📱 Compatibilità XFA 📱 Ottimizzazione mobile 📱 Supporto cross-browser 📱 Nessun requisito plug-in |
| [Introduzione a HTML5 Forms →](/help/forms/introductionhtml5.md) |

### Comunicazioni interattive {#interactive-communications}

| **Comunicazioni interattive** |
|---|
| Creare comunicazioni incentrate sui documenti, ad esempio istruzioni, fatture e avvisi, utilizzando un editor visivo con l&#39;integrazione di dati dinamici. |
| **Funzionamento:** progettare comunicazioni personalizzate che combinano contenuti statici con dati dinamici per canali di stampa e digitali. |
| **Quando utilizzare:** Rendiconti cliente, fatture, avvisi, comunicazioni personalizzate, flussi di lavoro basati su documenti. |
| 📄 Progettazione documento visivo 📄 Integrazione dati dinamici 📄 Output multicanale 📄 Personalization |
| [Introduzione alle comunicazioni interattive →](/help/forms/introduction-to-interactive-communication.md) |

## Dati e integrazione 🔗 {#data-integration}

Collegare i moduli ai sistemi back-end e alle origini dati per un flusso di informazioni senza soluzione di continuità e uno scambio di dati in tempo reale.

### Modello dati modulo {#form-data-model}

| **Modello dati modulo** |
|---|
| Interfaccia unificata a più origini di dati con funzionalità di precompilazione, convalida e invio. Complessità astratta dell’integrazione alla base di un modello coerente. |
| **Funzionamento:** creare un livello dati unificato che colleghi i moduli a più sistemi back-end con interfaccia e gestione coerente del flusso di dati. |
| **Quando utilizzare:** integrazione di più origini dati, relazioni dati complesse, requisiti di pre-popolamento, convalida con dati live. |
| 🔄 Integrazione multi-source 🔄 Modellazione dati 🔄 Pre-popolamento 🔄 Regole di convalida 🔄 Interfaccia unificata |
| [Introduzione al modello dati del modulo →](/help/forms/create-form-data-models.md) |

### Connettori RESTful {#restful-connectors}

| **Connettori RESTful** |
|---|
| Integrazione diretta con qualsiasi servizio accessibile tramite web tramite API RESTful. Connettersi a API e servizi web personalizzati. |
| **Funzionamento:** abilitare le chiamate API dirette dai moduli tramite azioni di invio o l&#39;integrazione dei dati per la connettività in tempo reale ai servizi Web. |
| **Quando utilizzare:** integrazione API personalizzata, connettività del servizio Web, scambio di dati in tempo reale, integrazione del servizio di terze parti. |
| 🌐 chiamate API dirette 🌐 Connettività in tempo reale 🌐 Integrazione flessibile 🌐 Supporto del servizio personalizzato |
| [Configura endpoint REST →](/help/forms/configure-submit-action-restpoint.md) \| [Configurazione integrazione dati →](/help/forms/data-integration.md) |

### Connettore Salesforce {#salesforce-connector}

| **Connettore Salesforce** |
|---|
| Integrazione nativa con Salesforce CRM per la gestione dei lead, la sincronizzazione dei dati dei clienti e l&#39;automazione dei processi di vendita. |
| **Funzionamento:** connettore predefinito per Salesforce con sincronizzazione dei dati dei moduli, creazione di lead e gestione dei record cliente. |
| **Quando utilizzare:** integrazione di Salesforce CRM, moduli di generazione dei lead, gestione dei dati cliente, automazione dei processi di vendita. |
| 🏢 Connettore predefinito 🏢 Gestione lead 🏢 Sincronizzazione dati 🏢 Automazione vendite |
| [Configura integrazione Salesforce →](/help/forms/configure-salesforce.md) |

### Connettore Microsoft Dynamics {#dynamics-connector}

| **Connettore Microsoft Dynamics** |
|---|
| Integrazione aziendale con Microsoft Dynamics per la connettività ERP e CRM con supporto completo dei processi aziendali. |
| **Funzionamento:** connettere i moduli a Microsoft Dynamics per la gestione dei clienti, l&#39;integrazione dei processi aziendali e il flusso di dati aziendali. |
| **Quando utilizzare:** integrazione Microsoft Dynamics, flussi di lavoro aziendali, gestione clienti, automazione dei processi aziendali. |
| 🏭 Connettività Enterprise 🏭 Integrazione dei processi aziendali 🏭 Gestione clienti 🏭 Sincronizzazione dei dati |
| [Configura integrazione Dynamics →](/help/forms/configure-msdynamics.md) |

### Connettore SharePoint {#sharepoint-connector}

| **Connettore SharePoint** |
|---|
| Integrazione di Document Management con SharePoint per l&#39;archiviazione di file, la collaborazione e l&#39;automazione del flusso di lavoro dei documenti. |
| **Funzionamento:** Archiviare gli invii di moduli e i documenti generati in SharePoint con funzionalità di collaborazione e gestione automatizzata dei documenti. |
| **Quando utilizzare:** Gestione documenti, collaborazione team, archiviazione file, flussi di lavoro basati su SharePoint. |
| 📁 Archiviazione documenti 📁 Caratteristiche Collaboration 📁 Flussi di lavoro automatizzati 📁 Integrazione SharePoint |
| [Configura integrazione SharePoint →](/help/forms/connect-forms-to-sharepoint-document-library.md) |

## Processo e flusso di lavoro {#process-workflow}

Automatizza i processi aziendali, le approvazioni e la generazione di documenti con funzionalità complete di workflow ed elaborazione.

### Flussi di lavoro AEM {#aem-workflows}

Automazione dei processi aziendali con approvazioni in più passaggi, assegnazioni di attività e orchestrazione dei processi per flussi di lavoro complessi basati su moduli.

**Funzionamento:** creazione di processi aziendali automatizzati con catene di approvazione, instradamento delle attività e monitoraggio dei processi per l&#39;invio di moduli.

**Quando utilizzare:** processi di approvazione, automazione aziendale, gestione attività, flussi di lavoro complessi, orchestrazione processi.

**Funzioni chiave:** automazione dei processi, catene di approvazione, routing delle attività, monitoraggio dei processi, regole aziendali.

[Introduzione ai flussi di lavoro di AEM →](/help/forms/aem-forms-workflow.md)

### Integrazione di Adobe Sign {#adobe-sign}

Flussi di lavoro per la firma elettronica con firme digitali legalmente vincolanti integrati direttamente nelle esperienze del modulo per processi di firma fluidi.

**Funzionamento:** abilitare le firme digitali nei moduli con funzionalità di firma elettronica legalmente vincolanti e flussi di lavoro di firma automatica.

**Quando utilizzare:** Firma del contratto, documenti legali, flussi di lavoro di approvazione, requisiti di conformità, automazione della firma.

**Caratteristiche principali:** firme elettroniche legali, flussi di lavoro di firma, supporto per la conformità, processi automatizzati.

[Configurare Adobe Sign →](/help/forms/working-with-adobe-sign.md)

### Azioni di invio {#submit-actions}

Gestione dell’invio dei moduli con più opzioni di elaborazione, tra cui e-mail, archiviazione del database, trigger del flusso di lavoro ed elaborazione personalizzata.

**Funzionamento:** Definire l&#39;invio dei moduli da parte degli utenti: indirizzare i dati a e-mail, database, flussi di lavoro o sistemi esterni.

**Quando utilizzare:** elaborazione invio modulo, routing dati, sistemi di notifica, attivatori integrazione.

**Funzioni chiave:** più opzioni di invio, routing dei dati, sistemi di notifica, trigger di integrazione.

[Configurare le azioni di invio →](/help/forms/configure-submit-actions-core-components.md)

### API di comunicazione {#communication-apis}

Generazione, manipolazione e sicurezza dei documenti a livello di programmazione con API RESTful per l’elaborazione e l’automazione di documenti a volume elevato.

**Funzionamento:** Generare, manipolare e proteggere i documenti a livello di programmazione con API per la creazione di PDF, l&#39;assemblaggio di documenti e l&#39;elaborazione batch.

**Quando utilizzare:** automazione documenti, elaborazione di volumi elevati, generazione programmatica, assembly documenti, operazioni batch.

**Funzioni chiave:** generazione di documenti, elaborazione batch, controllo programmatico, sicurezza dei documenti, automazione API.

[Guida introduttiva alle API di comunicazione →](/help/forms/aem-forms-cloud-service-communications-introduction.md)

## Analisi e ottimizzazione {#analytics-optimization}

Monitora le prestazioni dei moduli, comprendi il comportamento degli utenti e ottimizza i tassi di conversione con funzionalità complete di analisi e test.

### Integrazione di Adobe Analytics {#adobe-analytics}

Tracciamento delle prestazioni dei moduli con analisi dettagliate su tassi di completamento, modelli di abbandono e comportamento degli utenti per l’ottimizzazione basata sui dati.

**Funzionamento:** tieni traccia di interazioni modulo, tassi di completamento, analisi a livello di campo e modelli di comportamento degli utenti con reporting completo.

**Quando utilizzare:** Monitoraggio delle prestazioni, ottimizzazione della conversione, analisi del comportamento degli utenti e miglioramenti basati sui dati.

**Funzioni chiave:** tracciamento delle prestazioni, analisi del comportamento degli utenti, metriche di conversione, reporting dettagliato.

[Configurare i → di integrazione di Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

### Rapporti sulle transazioni {#transaction-reports}

Monitoraggio dell’utilizzo e trasparenza della fatturazione con rapporti dettagliati sulle chiamate API, generazione di documenti e transazioni fatturabili nell’implementazione.

**Funzionamento:** monitorare l&#39;utilizzo delle API, i volumi di generazione dei documenti e le transazioni fatturabili con report dettagliati sul consumo e registrazione dei costi.

**Quando utilizzare:** monitoraggio dell&#39;utilizzo, registrazione dei costi, pianificazione della capacità, creazione di report sulla conformità, ottimizzazione delle risorse.

**Funzioni chiave:** monitoraggio dell&#39;utilizzo, monitoraggio dei costi, pianificazione della capacità, reporting sulla conformità.

[Visualizzare i rapporti sulle transazioni →](/help/forms/transaction-reports-billable-apis.md)

### Integrazione test A/B {#ab-testing}

Ottimizzazione dei moduli mediante test di layout, disposizioni sul campo e flussi di utenti diversi con analisi statistica per il miglioramento della conversione.

**Funzionamento:** testare diverse varianti di modulo per identificare gli approcci più efficaci per i diversi segmenti utente e casi d&#39;uso.

**Quando utilizzare:** ottimizzazione della conversione, test dell&#39;esperienza utente, miglioramento delle prestazioni, decisioni di progettazione basate sui dati.

**Funzioni chiave:** test dei moduli, analisi statistica, ottimizzazione della conversione, confronto delle prestazioni.

[Scopri le → di ottimizzazione dei moduli](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Gestione e governance {#management-governance}

Gestione centralizzata dei moduli, controllo dell&#39;accesso degli utenti e funzionalità di governance per l&#39;implementazione di moduli su scala aziendale.

### Portale moduli {#forms-portal}

Archivio di moduli centralizzato con funzionalità di ricerca, categorizzazione dei moduli, gestione delle bozze e monitoraggio dell’invio in un’interfaccia unificata.

**Funzionamento:** creare archivi di moduli centralizzati in cui gli utenti possono individuare, accedere, gestire le bozze e tenere traccia degli invii tramite ricerca e categorizzazione.

**Quando utilizzare:** individuazione moduli, gestione centralizzata, self-service utenti, gestione bozze, monitoraggio invio.

**Funzioni chiave:** individuazione moduli, funzionalità di ricerca, gestione bozze, tracciamento invio, interfaccia utente.

[Configurare Forms Portal →](/help/forms/configure-forms-portal.md)

### User Management {#user-management}

Controllo dell’accesso basato sui ruoli con autorizzazioni granulari per la creazione, la modifica, la pubblicazione e l’amministrazione dei moduli all’interno dell’organizzazione.

**Funzionamento:** definizione di ruoli utente e autorizzazioni per diversi aspetti della gestione dei moduli con controllo di accesso e sicurezza granulari.

**Quando utilizzare:** Controllo degli accessi, gestione della sicurezza, definizione dei ruoli, gestione delle autorizzazioni, governance organizzativa.

**Funzioni chiave:** accesso basato su ruoli, gestione delle autorizzazioni, controllo della sicurezza, governance organizzativa.

[Configurare le → di gestione utenti](/help/forms/forms-groups-privileges-tasks.md)

### Controllo della versione {#version-control}

Gestione del ciclo di vita dei moduli con rilevamento delle versioni, cronologia delle modifiche, funzionalità di rollback e audit trail per conformità e governance.

**Funzionamento:** tenere traccia delle versioni dei moduli, gestire la cronologia delle modifiche, abilitare i rollback e fornire audit trail per i requisiti di conformità e governance.

**Quando utilizzare:** Gestione delle modifiche, requisiti di conformità, audit trail, verifica delle versioni, processi di governance.

**Funzioni chiave:** Tracciamento delle versioni, cronologia delle modifiche, funzionalità di rollback, audit trail, supporto della conformità.

[Informazioni sulle → di controllo delle versioni](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## Guida introduttiva per prodotto {#getting-started}

Scegli il tuo punto di partenza in base alle tue esigenze immediate e ai tuoi requisiti tecnici.

### Guida introduttiva alla creazione di moduli {#form-creation-start}

**Per i progetti moderni:** Inizia con [Componente core Forms](/help/forms/creating-adaptive-form-core-components.md)

**Per prestazioni elevate:** Inizia con [Edge Delivery Forms](/help/edge/docs/forms/overview.md)

**Per i progetti esistenti:** Inizia con [Componente di base Forms](/help/forms/creating-adaptive-form.md)

**Per la modernizzazione XFA:** Inizia con [HTML5 Forms](/help/forms/introductionhtml5.md)

**Per le comunicazioni documenti:** Inizia con [Comunicazioni interattive](/help/forms/introduction-to-interactive-communication.md)

### Guida rapida all’integrazione dei dati {#integration-start}

**Per più origini dati:** Inizia con [Modello dati modulo](/help/forms/create-form-data-models.md)

**Per Salesforce CRM:** Inizia con [Connettore Salesforce](/help/forms/configure-salesforce.md)

**Per Microsoft Dynamics:** Inizia con [Dynamics Connector](/help/forms/configure-msdynamics.md)

**Per le API personalizzate:** Inizia con [Connettori RESTful](/help/forms/configure-submit-action-restpoint.md)

**Per l&#39;archiviazione dei documenti:** Inizia con [Connettore SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md)

### Guida introduttiva all&#39;automazione dei processi {#workflow-start}

**Per i processi di approvazione:** Inizia con [Flussi di lavoro AEM](/help/forms/aem-forms-workflow.md)

**Per le firme elettroniche:** Inizia con [Integrazione Adobe Sign](/help/forms/working-with-adobe-sign.md)

**Per la gestione dell&#39;invio:** Inizia con [Azioni di invio](/help/forms/configure-submit-actions-core-components.md)

**Per la generazione di documenti:** Inizia con [API di comunicazione](/help/forms/aem-forms-cloud-service-communications-introduction.md)

### Guida introduttiva di Analytics {#analytics-start}

**Per il tracciamento delle prestazioni:** Inizia con [Integrazione Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

**Per il monitoraggio della sintassi:** Inizia con [Report transazioni](/help/forms/transaction-reports-billable-apis.md)

**Per informazioni sull&#39;ottimizzazione:** inizia con [Rapporti di Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

### Guida introduttiva alla gestione {#management-start}

**Per l&#39;individuazione dei moduli:** Inizia con [Forms Portal](/help/forms/configure-forms-portal.md)

**Per il controllo degli accessi:** Inizia con [Gestione utenti](/help/forms/forms-groups-privileges-tasks.md)

**Per il rilevamento delle modifiche:** Inizia con [Controllo versione](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## Architettura e implementazione {#architecture}

Per orientamenti completi sull&#39;implementazione:

- **[Esaminare i modelli dell&#39;architettura](/help/forms/aem-forms-cloud-service-architecture.md)** per la distribuzione scalabile
- **[Imposta l&#39;ambiente di sviluppo](/help/forms/setup-local-development-environment.md)** per la collaborazione team
- **[Pianificare le strategie di migrazione](/help/forms/migrate-to-forms-as-a-cloud-service.md)** dai sistemi esistenti

## Supporto e risorse {#support}

- **Centro assistenza** - Assistenza per l&#39;implementazione e la risoluzione dei problemi
- **Forum della community** - Entra in contatto con altri utenti ed esperti di AEM Forms
- **Servizi professionali** - Consulenza Adobe per le implementazioni Enterprise
- **Formazione e certificazione** - Sviluppa le competenze nelle funzionalità di AEM Forms

*Scegli i componenti necessari per creare esperienze modulo efficaci. Ogni prodotto funziona in modo indipendente o si combina con altri per creare soluzioni complete per i requisiti aziendali.*
