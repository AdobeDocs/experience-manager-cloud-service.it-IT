---
title: Introduzione ad AEM Forms as a Cloud Service
description: Scopri le funzionalità di AEM Forms per la creazione di moduli adattivi, l’automazione dei flussi di lavoro e la gestione dei documenti digitali. Piattaforma completa per processi aziendali basati su moduli.
landing-page-description: Scopri come utilizzare AEM Forms as a Cloud Service per creare moduli adattivi, elaborare documenti e automatizzare i flussi di lavoro aziendali.
keywords: AEM Forms, moduli adattivi, generatore di moduli, moduli digitali, automazione del flusso di lavoro, servizi documentali, modello per dati modulo
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# Introduzione ad AEM Forms as a Cloud Service {#introduction}



Adobe Experience Manager Forms as a Cloud Service fornisce una piattaforma completa per la creazione, la gestione e l’ottimizzazione delle esperienze di moduli digitali. Le organizzazioni utilizzano AEM Forms per digitalizzare i processi basati su carta, creare moduli web dinamici, automatizzare i flussi di lavoro dei documenti e distribuire comunicazioni personalizzate su larga scala.

La piattaforma combina le funzionalità di authoring dei moduli con servizi di back-end affidabili, consentendo di creare qualsiasi cosa, dai semplici moduli di contatto alle complesse applicazioni aziendali in più fasi. Grazie all&#39;architettura nativa per il cloud, è possibile ottenere aggiornamenti automatici, scalabilità elastica e sicurezza di livello enterprise senza dover gestire l&#39;infrastruttura.

Questa guida presenta le funzionalità di base organizzate per l’intero ciclo di vita dei moduli, dalla progettazione iniziale fino all’ottimizzazione continua.

## Novità di AEM Forms {#whats-new}

**Elementi di rilievo della versione più recente:**

- **Componente input data e ora** - Input utente avanzato con interfaccia calendario e orologio per una selezione precisa di data e ora
- **Sicurezza avanzata caricamento file** - Convalida automatica e controllo del tipo di contenuto per evitare formati di file non supportati
- **È stata migliorata la gestione degli errori** - È stato migliorato il debug con codici di errore specifici per le azioni di invio personalizzate
- **Miglioramenti al documento record** - Opzione per escludere i campi nascosti per una generazione di documenti più pulita

**Funzioni Pre-Release:**

- **Supporto per il formato AFP** - Funzionalità di stampa di livello Enterprise con API di comunicazione
- **Miglioramenti all&#39;editor di regole** - Supporto moderno di JavaScript, variabili dinamiche e regole del pannello in base al contesto
- **Metodi di convalida migliorati** - Convalida a livello di pannello, campo e modulo con maggiore flessibilità

[Visualizzare le note sulla versione complete →](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Programma di accesso in anteprima {#early-access}

Ottieni accesso esclusivo alle innovazioni AEM Forms all’avanguardia prima che siano generalmente disponibili.

**Funzioni di accesso anticipato correnti:**

- **Assistente AEM Forms AI** - IA generativa per la creazione automatica di moduli, la generazione di pannelli e i consigli per l&#39;ottimizzazione
- **Componente firma scarabocchio** - Acquisizione diretta della firma nei moduli tramite mouse, stilo o touchscreen
- **Integrazione API diretta** - Connettersi alle API nell&#39;editor di regole senza richiedere la configurazione del modello dati modulo
- **Ottimizzazione Forms** - Suggerimenti per l&#39;analisi delle prestazioni e il miglioramento del tasso di conversione basati sull&#39;intelligenza artificiale

**Partecipa al programma:**
Sii tra i primi ad accedere alle innovazioni e contribuire a modellare il futuro di AEM Forms.

[Richiedi accesso →](mailto:aem-forms-ea@adobe.com) | [Ulteriori informazioni →](/help/forms/early-access-ea-features.md)


## Funzionalità di base {#core-capabilities}

AEM Forms supporta il percorso completo di moduli digitali, dalla creazione iniziale fino all’ottimizzazione continua. Ogni fase si basa sulla precedente, creando una piattaforma completa per i processi aziendali basati su moduli.

**Percorso di flussi di lavoro AEM Forms:**

    CREA → GESTISCI → PUBBLICA → ACQUISISCI → PROCESSO → INTEGRA → TRACK → ARCHIVIO → MIGLIORARE
    ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    Progettazione   Revisione   Distribuisci   Raccogli   Maniglia   Connetti   Archivio monitor   Ottimizza
    ↑                                                                              ↓
    ←←←←←←←←←←←←←←← Ciclo continuo di miglioramento ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←

### Creazione: Progettazione e sviluppo di moduli {#create}

Crea moduli adattivi utilizzando più approcci di authoring personalizzati in base a esigenze e requisiti tecnici diversi.

**Generatore di moduli visivi**
Progetta moduli reattivi tramite interfacce di trascinamento utilizzando [Componenti core](/help/forms/creating-adaptive-form-core-components.md), [Componenti Foundation](/help/forms/creating-adaptive-form.md) o [Edge Delivery Services](/help/edge/docs/forms/overview.md). L’editor visivo fornisce un feedback immediato, mantenendo al contempo un markup semantico e pulito che funziona tra dispositivi e tecnologie per l’accessibilità.

**Authoring basato su documenti**
Crea moduli utilizzando strumenti familiari come Microsoft Excel tramite [Edge Delivery Services](/help/edge/docs/forms/overview.md). Questo approccio consente agli autori di contenuti di creare moduli ad alte prestazioni senza competenze tecniche, ottenendo allo stesso tempo punteggi eccezionali in Google Lighthouse.

**Modelli e temi**
Accelera la creazione di moduli utilizzando [modelli](/help/forms/template-editor-core-components.md) predefiniti che definiscono la struttura e il contenuto iniziale. Applica un branding coerente con [temi](/help/forms/using-themes-in-core-components.md) che controllano lo stile visivo in più moduli, garantendo la coerenza della progettazione e riducendo i tempi di sviluppo.

**Integrazioni dati**
Collegare i moduli ai sistemi back-end durante la fase di progettazione. Il [modello dati modulo](/help/forms/create-form-data-models.md) fornisce un&#39;interfaccia unificata a più origini dati, abilitando [precompilazione](/help/forms/prepopulate-adaptive-form-fields.md), [regole di convalida](/help/forms/rule-editor-core-components.md) e un flusso di dati continuo tra moduli e sistemi aziendali.

**Convalide e logica condizionale**
Implementa [logica condizionale](/help/forms/rule-editor-core-components.md), divulgazione progressiva e convalida adattiva per guidare gli utenti attraverso processi complessi. [La funzionalità Salva e riprendi](/help/forms/save-core-component-based-form-as-draft.md) consente agli utenti di completare i moduli in più sessioni.

**Forms HTML5**
Esegui il rendering dei moduli basati su XFA come [moduli HTML5](/help/forms/introductionhtml5.md) per dispositivi mobili e browser legacy. HTML5 Forms offre un’esperienza mobile nativa senza plug-in, mantenendo al contempo la logica del modulo e la convalida dai modelli XDP originali.

**Comunicazioni interattive**
Creare comunicazioni incentrate sui documenti, ad esempio rendiconti, fatture e avvisi, utilizzando un editor visivo. [Le comunicazioni interattive](/help/forms/interactive-communication/create-interactive-communication.md) combinano il contenuto statico con i dati dinamici per generare comunicazioni personalizzate tra i canali di stampa e digitali.

### Governare: revisione e conformità {#govern}

Stabilire processi di supervisione e approvazione per garantire che i moduli soddisfino gli standard organizzativi e i requisiti normativi.

**Approvazioni basate su flusso di lavoro**
Instradare le progettazioni dei moduli tramite processi di revisione in più fasi con assegnazioni basate su ruoli. Le parti interessate possono [rivedere](/help/forms/create-reviews-forms.md), [commentare](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) e approvare i moduli prima della pubblicazione, mantenendo il controllo di qualità e la supervisione della conformità tramite [flussi di lavoro AEM](/help/forms/aem-forms-workflow.md).

**Gestione versioni**
Monitora le versioni dei moduli e gestisci gli audit trail per garantire la conformità alle normative. Il controllo delle versioni [integrato](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) consente di ripristinare le modifiche, confrontare le iterazioni e gestire i record cronologici per i controlli di conformità.

**Controllo degli accessi e autorizzazioni**
Definisci le autorizzazioni granulari per la creazione, la modifica e la pubblicazione di moduli. [L&#39;accesso basato sul ruolo](/help/forms/forms-groups-privileges-tasks.md) garantisce che solo gli utenti autorizzati possano modificare i moduli, mantenendo al contempo la separazione dei compiti per i processi aziendali sensibili.

### Pubblicazione: distribuzione multicanale {#publish}

Distribuisci i moduli su più canali e punti di contatto per raggiungere gli utenti ovunque si trovino.

**Pubblicazione Omnichannel**
Pubblica moduli in [AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md), pagine Web autonome, applicazioni mobili o [incorporati in sistemi di terze parti](/help/forms/embed-adaptive-form-core-components-external-web-page.md). La pubblicazione da una singola origine garantisce la coerenza adattandosi al contempo ai diversi requisiti del canale.

**Localizzazione e Personalization**
Distribuisci moduli in più lingue utilizzando [flussi di lavoro di traduzione di AEM](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md), con supporto per [lingue da sinistra a destra e da destra a sinistra](/help/forms/right-left-languages.md). Integra con Adobe Target per personalizzare le esperienze dei moduli in base a segmenti di utenti, comportamenti o dati contestuali.

**Ottimizzazione delle prestazioni**
Sfrutta Edge Delivery Services per un caricamento delle forme estremamente rapido e prestazioni SEO ottimali. Le reti per la distribuzione dei contenuti garantiscono l&#39;accessibilità globale con una latenza minima.

**Portale Forms**
Creare archivi di moduli centralizzati in cui gli utenti possono individuare, accedere e gestire i moduli. [Forms Portal](/help/forms/configure-forms-portal.md) fornisce funzionalità di ricerca, categorizzazione dei moduli, gestione delle bozze e monitoraggio dell&#39;invio in un&#39;interfaccia unificata per migliorare l&#39;esperienza utente.

### Acquisizione: esperienza utente e raccolta dati {#capture}

Ottimizza l’esperienza di compilazione dei moduli per massimizzare i tassi di completamento e la qualità dei dati.

**Progettazione reattiva**
Forms si adatta automaticamente a diverse dimensioni di schermo e metodi di input. I controlli ottimizzati per il tocco, la navigazione da tastiera e la compatibilità con gli assistenti vocali garantiscono l&#39;[accessibilità](/help/forms/creating-accessible-adaptive-forms.md) per tutti i tipi di utenti.

**Firme digitali**
Integra [Adobe Sign](/help/forms/working-with-adobe-sign.md) per le firme elettroniche legalmente vincolanti nell&#39;esperienza del modulo. Gli utenti possono firmare i documenti senza uscire dal modulo, semplificando i processi di approvazione e riducendo l’abbandono.

**Invia azioni**
Configura [azioni di invio](/help/forms/configure-submit-actions-core-components.md) per definire cosa accade quando gli utenti completano e inviano i moduli. Inoltra i dati a e-mail, database, flussi di lavoro o sistemi esterni, fornendo al contempo feedback e conferma immediati agli utenti.

### Processo: gestione e instradamento invio {#process}

Gestisce l’invio dei moduli con solide funzionalità di elaborazione, convalida e indirizzamento.

**Convalida ed elaborazione dati**
Garantire l&#39;integrità dei dati tramite regole di convalida lato server e di elaborazione automatizzata. Trasforma, convalida e instrada i dati inviati durante la generazione di ricevute, conferme o materiali di follow-up per gli utenti.

**API di comunicazione**
Genera, modifica e proteggi documenti a livello di programmazione tramite [API RESTful](/help/forms/aem-forms-cloud-service-communications-introduction.md). Creazione di PDF, formati pronti per la stampa, assemblaggio di documenti, applicazione di firme digitali ed elaborazione di [operazioni batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) di volumi elevati per flussi di lavoro di documenti su scala aziendale.

**Documento record**
Genera automaticamente record PDF di invii di moduli per conformità e conferma da parte dell&#39;utente. [Il documento record](/help/forms/generate-document-of-record-core-components.md) crea versioni formattate e stampabili dei moduli completati con i dati inviati, fornendo documentazione ufficiale per le transazioni e i requisiti normativi.

**Orchestrazione flusso di lavoro**
Attiva processi aziendali complessi basati sull&#39;invio di moduli. Instradare i dati attraverso le catene di approvazione, assegnare attività a utenti specifici e automatizzare le operazioni di routine mantenendo gli audit trail.

**Gestione e ripristino errori**
I meccanismi di esecuzione dei nuovi tentativi incorporati e l’elaborazione dei fallback assicurano che non vadano persi invii. La registrazione completa consente di risolvere i problemi e di mantenere gli accordi sui livelli di servizio.

### Integrare: connettività back-end {#integrate}

Collegare i moduli ai sistemi aziendali e alle origini dati esistenti per un flusso di informazioni senza soluzione di continuità.

**Connettori predefiniti**
Integrazione nativa con [Salesforce](/help/forms/configure-salesforce.md), [Microsoft Dynamics](/help/forms/configure-msdynamics.md), [SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md) e soluzioni Adobe Experience Cloud. I connettori predefiniti riducono i tempi di sviluppo e garantiscono al tempo stesso una sincronizzazione affidabile dei dati.

**Integrazione API RESTful**
Connettersi a qualsiasi servizio accessibile tramite API RESTful tramite [azioni di invio](/help/forms/configure-submit-action-restpoint.md) o [integrazione dati](/help/forms/data-integration.md). Il modello di dati modulo astrae la complessità dell’integrazione, fornendo un’interfaccia coerente indipendentemente dall’architettura di sistema sottostante.

**Scambio di dati in tempo reale**
Consente il flusso bidirezionale dei dati tra moduli e sistemi aziendali. Precompila i moduli dai record esistenti, esegui la convalida rispetto ai dati live e aggiorna più sistemi simultaneamente all&#39;invio tramite l&#39;[integrazione completa dei dati](/help/forms/data-integration.md).

### Track: Analytics e monitoraggio delle prestazioni {#track}

Comprendere le prestazioni dei moduli e il comportamento degli utenti attraverso analisi e monitoraggio completi.

**Analisi modulo**
Tieni traccia dei tassi di completamento, dei pattern di abbandono e delle interazioni a livello di campo tramite [integrazione Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md). Identifica i punti di attrito, misura i funnel di conversione e comprendi il comportamento degli utenti in diversi segmenti.

**Monitoraggio delle prestazioni**
Monitora i tempi di caricamento dei moduli, i tassi di successo dell’invio e le prestazioni del sistema. Le dashboard in tempo reale forniscono informazioni approfondite sullo stato tecnico e sulle metriche di esperienza utente.

**Business Intelligence**
Genera report sull&#39;utilizzo delle maschere, sui volumi di invio e sull&#39;efficienza dei processi. Analytics informa la pianificazione della capacità, l’ottimizzazione dell’esperienza utente e i miglioramenti dei processi aziendali.

**Rapporti sulle transazioni**
Monitora l&#39;utilizzo delle API, i volumi di generazione dei documenti e [le transazioni fatturabili](/help/forms/transaction-reports-billable-apis.md) nella distribuzione AEM Forms. Monitorare i modelli di consumo, ottimizzare l&#39;allocazione delle risorse e garantire la conformità con i requisiti di licenza basati sull&#39;utilizzo.

### Archiviazione: gestione dei documenti e conformità {#archive}

Archiviare e gestire in modo sicuro gli invii di moduli e i documenti generati per la conservazione a lungo termine e la conformità.

**Archiviazione documenti**
Archivia i documenti generati e gli invii di moduli nel sistema Digital Asset Management di AEM o integra con archivi di documenti esterni come [SharePoint](/help/forms/configure-submit-action-sharepoint.md), [OneDrive](/help/forms/configure-submit-action-onedrive.md) o [Archiviazione BLOB di Azure](/help/forms/configure-submit-action-azure-blob-storage.md).

**Conformità e conservazione**
Implementazione di regole di conservazione dei dati conformi ai requisiti normativi, inclusi GDPR, CCPA e HIPAA. [I processi di archiviazione automatizzati](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) garantiscono la conservazione dei documenti per i periodi richiesti e la loro eliminazione sicura quando necessario.

**Sicurezza e controllo degli accessi**
Applicare la crittografia, le firme digitali e i [controlli di accesso basati sui ruoli](/help/forms/forms-groups-privileges-tasks.md) ai documenti archiviati. AuditTrail traccia dell’accesso ai documenti e delle modifiche per la generazione di rapporti di conformità e la supervisione della sicurezza.

### Migliorare: ottimizzazione e miglioramento {#improve}

Ottimizza continuamente le prestazioni dei moduli e l’esperienza utente attraverso insights e test basati sui dati.

**Integrazione test A/B**
Utilizza Adobe Target per testare diversi layout di moduli, disposizioni dei campi e flussi di utenti. L’analisi statistica aiuta a identificare gli approcci più efficaci per diversi segmenti di utenti e casi d’uso.

**Ottimizzazione guidata da Analytics**
Analizza i dati sul comportamento degli utenti per identificare le opportunità di miglioramento. [Visualizza e comprendi i rapporti di analisi](/help/forms/view-understand-aem-forms-analytics-reports.md) per la mappatura del calore, l&#39;analisi dell&#39;interazione dei campi e il riconoscimento del pattern di abbandono per informare i miglioramenti della progettazione iterativa.

**Miglioramento iterativo**
Implementa processi di miglioramento continuo basati sul feedback degli utenti, sulle metriche delle prestazioni e sui requisiti aziendali. [Le funzionalità di controllo della versione](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) e rollback consentono la sperimentazione sicura e l&#39;iterazione rapida.

## Guida introduttiva {#getting-started}

L&#39;approccio adottato dipende dalle esigenze immediate e dagli obiettivi a lungo termine.

### Guida introduttiva: Simple Forms {#quick-start}

Scegli l’approccio di authoring preferito in base al background tecnico e ai requisiti di prestazioni:

**Generazione modulo visivo:**

1. **[Creare moduli adattivi con i Componenti core](/help/forms/creating-adaptive-form-core-components.md)** per moduli moderni e reattivi
2. **[Configurare le azioni di invio](/help/forms/configure-submit-actions-core-components.md)** per gestire i dati del modulo
3. **[Incorpora moduli in AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)** o condividi tramite collegamenti diretti

**Authoring basato su documenti:**

1. **[Crea moduli con Excel](/help/edge/docs/forms/create-forms.md)** con Edge Delivery Services per moduli ad alte prestazioni
2. **[Pubblica su Edge Delivery](/help/edge/docs/forms/publish-forms.md)** per velocità di caricamento e SEO ottimali

**Supporto moduli legacy:**

- **[HTML5 Forms](/help/forms/introductionhtml5.md)** per il rendering di moduli XFA ottimizzati per dispositivi mobili

### Implementazione avanzata: processi aziendali {#advanced-implementation}

Per requisiti complessi che coinvolgono più sistemi, generazione di documenti e flussi di lavoro di approvazione:

**Integrazione dei dati e flussi di lavoro:**

1. **[Configura modelli dati modulo](/help/forms/create-form-data-models.md)** per connettere i sistemi back-end
2. **[Progetta i processi del flusso di lavoro](/help/forms/aem-forms-workflow.md)** per l&#39;approvazione e il routing
3. **[Configura analisi](/help/forms/integrate-aem-forms-with-adobe-analytics.md)** per misurare le prestazioni

**Servizi documentali e comunicazioni:**

1. **[Implementazione delle API di comunicazione](/help/forms/aem-forms-cloud-service-communications-introduction.md)** per la generazione automatica dei documenti
2. **[Crea comunicazioni interattive](/help/forms/interactive-communication/create-interactive-communication.md)** per istruzioni e avvisi personalizzati
3. **[Configura Forms Portal](/help/forms/configure-forms-portal.md)** per la gestione centralizzata dei moduli

### Distribuzione aziendale: scalabilità e governance {#enterprise-deployment}

Per implementazioni a livello di organizzazione che richiedono governance, conformità e monitoraggio:

**Architettura e governance:**

1. **[Esaminare i modelli dell&#39;architettura](/help/forms/aem-forms-cloud-service-architecture.md)** per la distribuzione scalabile
2. **[Configurare la gestione degli utenti](/help/forms/forms-groups-privileges-tasks.md)** e i controlli di accesso
3. **[Imposta flussi di lavoro di sviluppo](/help/forms/setup-local-development-environment.md)** per la collaborazione in team

**Migrazione e monitoraggio:**

1. **[Pianificare le strategie di migrazione](/help/forms/migrate-to-forms-as-a-cloud-service.md)** dai sistemi esistenti
2. **[Implementa monitoraggio delle transazioni](/help/forms/transaction-reports-billable-apis.md)** per il monitoraggio dell&#39;utilizzo e la conformità

<details>
<summary><strong>❓ domande frequenti</strong></summary>

**Che cos&#39;è un generatore di moduli?**
Un generatore di moduli è uno strumento che consente di creare moduli digitali senza codificarli. È possibile progettare moduli utilizzando interfacce di trascinamento della selezione, aggiungere campi come caselle di testo e menu a discesa e pubblicarli online per raccogliere dati dagli utenti.

**Come si crea un modulo online?**
Con AEM Forms, puoi creare moduli adattivi utilizzando i Componenti core tramite un editor drag-and-drop visivo, moduli ad alte prestazioni con Edge Delivery Services o utilizzare Componenti di base per flussi di lavoro consolidati. Per iniziare, seleziona un modello, aggiungi i campi del modulo, configura le connessioni dati e pubblica su più canali.

**Cosa rende un buon modulo online?**
I moduli online sono efficienti e reattivi da dispositivi mobili, vengono caricati rapidamente, dispongono di etichette chiare, utilizzano l’ordinamento dei campi logici, includono la convalida per evitare errori e forniscono agli utenti un feedback immediato all’invio.

**È possibile integrare i moduli con altri sistemi aziendali?**
Sì, i moderni generatori di moduli offrono ampie funzionalità di integrazione. Puoi collegare i moduli a sistemi di gestione delle relazioni con i clienti, piattaforme di e-mail marketing, database, archiviazione cloud e strumenti di automazione dei flussi di lavoro per semplificare i processi aziendali.

**I moduli online sono protetti?**
I creatori di moduli professionali includono funzioni di sicurezza di livello enterprise come la crittografia dei dati, la trasmissione sicura dei dati, i controlli di accesso e la conformità con normative come GDPR, HIPAA e CCPA per proteggere le informazioni sensibili.

**Come si aggiungono firme elettroniche ai moduli?**
Le firme digitali possono essere integrate direttamente nei moduli utilizzando Adobe Sign o altri provider di firma elettronica. Questo consente agli utenti di firmare i documenti all’interno dell’esperienza del modulo, eliminando la necessità di flussi di lavoro di firma separati e riducendo l’abbandono dei moduli.

**I moduli possono generare automaticamente documenti PDF?**
Sì, le piattaforme di moduli moderni possono generare automaticamente ricevute PDF, conferme o documenti di record al momento dell’invio dei moduli. Ciò è essenziale per la conformità, la conservazione dei documenti e la conferma immediata agli utenti.

**Come si tiene traccia delle prestazioni dei moduli e dell&#39;analisi?**
Le analisi dei moduli consentono di comprendere i tassi di completamento, i pattern di abbandono e il comportamento degli utenti. L’integrazione con piattaforme di analisi come Adobe Analytics fornisce informazioni su quali campi causano attrito e su come ottimizzare i tassi di conversione.

**Che cos&#39;è l&#39;automazione del flusso di lavoro del modulo?**
L’automazione del flusso di lavoro dei moduli indirizza gli invii attraverso i processi di approvazione, assegna attività ai membri del gruppo e attiva azioni in altri sistemi aziendali. In questo modo viene eliminata l&#39;elaborazione manuale e viene garantita la gestione coerente dei dati dei moduli.

**Come è possibile rendere i moduli accessibili agli utenti disabili?**
[I moduli accessibili](/help/forms/creating-accessible-adaptive-forms.md) includono l&#39;etichettatura corretta, la navigazione da tastiera, la compatibilità con gli assistenti vocali e la conformità alle linee guida WCAG. In questo modo tutti gli utenti possono completare i moduli indipendentemente dalle loro capacità o tecnologie per l’accessibilità.

**Quanto costano i generatori di moduli?**
Il prezzo di AEM Forms as a Cloud Service dipende dai requisiti specifici, dal volume di utilizzo e dalle esigenze delle funzioni. Per informazioni dettagliate sui prezzi e per discutere di una soluzione personalizzata per la tua organizzazione, contatta il reparto vendite di Adobe o il tuo rappresentante Adobe.

</details>

## Passaggi successivi {#next-steps}

Scopri le funzionalità che corrispondono alle tue priorità attuali:

- **[Crea il tuo primo modulo](/help/forms/creating-adaptive-form-core-components.md)** per sperimentare l&#39;ambiente di authoring
- **[Esaminare le opzioni dell&#39;architettura](/help/forms/aem-forms-cloud-service-architecture.md)** per la pianificazione della distribuzione
- **[Configura l&#39;ambiente di sviluppo](/help/forms/setup-local-development-environment.md)** per la collaborazione in team
- **[Esplora le opzioni di integrazione](/help/forms/data-integration.md)** per la connessione dei sistemi esistenti

Per una guida completa all’implementazione, considera Adobe Professional Services per accelerare l’implementazione e garantire best practice fin dall’inizio.
