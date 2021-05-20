---
title: Guida introduttiva AEM Headless come Cloud Service
description: In questa parte del Percorso di sviluppo headless AEM, scopri AEM prerequisiti headless.
source-git-commit: 8e96827f9353d6ffdf1e01645f2bc8bdaac2610f
workflow-type: tm+mt
source-wordcount: '3059'
ht-degree: 0%

---

# Guida introduttiva a AEM headless come Cloud Service {#getting-started}

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) scopri cosa è necessario per avviare il tuo progetto con AEM Headless.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Scopri lo sviluppo headless di CMS](learn-about.md) hai appreso la teoria di base su cosa è un CMS headless e dovresti ora:

* Comprendere i concetti e la terminologia di base per la distribuzione di contenuti headless
* Capire perché e quando è richiesto un headless
* Conoscere ad alto livello come vengono utilizzati i concetti senza testa e come si relazionano

Questo articolo si basa su questi elementi fondamentali per comprendere come utilizzare AEM per implementare una soluzione headless.

## Obiettivo {#objective}

Questo documento ti aiuta a capire AEM Headless nel contesto del tuo progetto. Dopo la lettura è necessario:

* Comprendere le nozioni di base AEM funzioni headless.
* Conoscere i prerequisiti per l&#39;utilizzo di AEM funzionalità headless.
* Presta attenzione AEM livelli di integrazione headless.
* Puoi definire il tuo progetto in termini di ambito.

## Nozioni di base AEM {#aem-basics}

Prima di poter definire il progetto headless all’interno di AEM, è importante comprendere alcuni concetti AEM di base.

### Istanza autore {#author}

Nella sua semplicità, AEM consiste di un&#39;istanza di authoring e di un&#39;istanza di [pubblicazione](#publish) che lavorano insieme per creare, gestire e pubblicare i contenuti.

Il contenuto inizia nell’istanza di authoring. In questa sezione gli autori dei contenuti creano i propri contenuti. L’ambiente di authoring offre agli autori diversi strumenti per creare, organizzare e riutilizzare i contenuti.

### Pubblica istanza {#publish}

Una volta creato il contenuto nell’istanza di authoring, deve essere pubblicato per essere disponibile ad altri servizi da utilizzare. Un’istanza di pubblicazione contiene tutti i contenuti pubblicati.

### Replica {#replication}

La replica è l’atto di trasferire il contenuto dall’istanza di authoring all’istanza di pubblicazione. Questa operazione viene eseguita automaticamente da AEM quando un autore o un altro utente con i diritti appropriati pubblica il contenuto.

### Riepilogo AEM di base {#aem-basics-summary}

Al livello più semplice, la creazione di esperienze digitali in AEM richiede i seguenti passaggi:

1. Gli autori dei contenuti creeranno i contenuti headless nell’istanza di authoring.
1. Quando il contenuto è pronto, viene replicato nell’istanza di pubblicazione.
1. Puoi quindi chiamare le API per recuperare questo contenuto.

AEM Headless sfrutta questa base tecnica offrendo potenti strumenti per gestire contenuti headless [descritti nella sezione successiva.](#aem-headless-basics)

## Nozioni di base AEM senza testa {#aem-headless-basics}

Le funzionalità headless di AEM si basano su alcune funzioni chiave. Queste saranno spiegate in dettaglio nelle successive parti del percorso. Ora è importante solo conoscere le basi di ciò che fanno e di ciò che vengono chiamati.

### Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto che verranno creati e gestiti in AEM. Servono come una sorta di impalcatura per i vostri contenuti. Quando scegli di creare un contenuto, gli autori selezionano i modelli di frammento di contenuto da te definiti, che li guida nella creazione di contenuti.

### Frammenti di contenuto {#content-fragments}

I frammenti di contenuto consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina. Consentono di preparare i contenuti pronti per l’uso in più posizioni e su più canali.

I frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

### API GraphQL e REST {#apis}

Per modificare il contenuto senza problemi, AEM offre due solide API.

* L’API GraphQL consente di creare richieste di accesso e distribuzione di frammenti di contenuto.
* L’API REST di Assets consente di creare e modificare frammenti di contenuto (e altre risorse).

Scoprirai queste API e come utilizzarle in una parte successiva del percorso AEM headless. Oppure consulta la sezione [risorse aggiuntive](#additional-resources) per ulteriore documentazione.

## Livelli di integrazione headless {#integration-levels}

AEM supporta sia i modelli full headless che quelli tradizionali full stack o headful di un CMS. Tuttavia AEM offre non solo queste due opzioni esclusive, ma anche la possibilità di supportare modelli ibridi che combinano i vantaggi di entrambi, offrendo una flessibilità unica per il vostro progetto headless.

Al fine di garantire la comprensione dei concetti headless, questo Percorso AEM Headless Developer si concentra sul modello headless puro per consentirti di iniziare a lavorare il prima possibile senza codifica in AEM.

Tuttavia, è necessario essere consapevoli delle possibilità ibride aggiuntive aperte a voi una volta compreso AEM caratteristiche headless. Qui di seguito riportiamo questi casi per la vostra consapevolezza. Al termine del percorso, riceverai informazioni più dettagliate su questi concetti nel caso in cui sia necessaria una tale flessibilità per il tuo progetto.

### Esiste già un consumo esterno di contenuti headless, ad esempio una singola applicazione pagina (SPA). {#already-have-a-spa}

Supponiamo che i requisiti di base per la distribuzione dei contenuti da AEM a un servizio esterno esistente siano minimi.

#### Livello 1: Integrazione dei frammenti di contenuto - Modello tradizionale senza testa {#level-1}

Questo livello di integrazione è il modello headless tradizionale e consente agli autori di contenuti di creare contenuti in AEM e distribuirli senza problemi a qualsiasi numero di servizi esterni tramite GraphQL o di modificarli da servizi esterni tramite l’API Assets. Non è richiesta alcuna codifica in AEM.

In questo modello, AEM viene utilizzato solo per creare e distribuire il contenuto tramite l’uso di frammenti di contenuto AEM. Il rendering e l’interazione con il contenuto vengono delegati all’applicazione esterna che consuma, spesso un’applicazione a pagina singola (SPA).

#### Livello 2: Incorpora il SPA in AEM - Modello ibrido {#level-2}

Questo livello di integrazione si basa sul primo livello, ma consente anche di incorporare in AEM l’applicazione esterna (SPA) in modo che gli autori dei contenuti possano visualizzare il contenuto nel contesto dell’applicazione esterna in AEM. L&#39;applicazione può anche supportare la modifica limitata dell&#39;applicazione esterna in AEM.

Questo livello offre il vantaggio di consentire agli autori di contenuti di creare in modo flessibile i contenuti in AEM in modo headful, con i contenuti contestuali presentati con un SPA esterno incorporato, e allo stesso tempo consegnarli senza problemi.

#### Livello 3: Incorpora e abilita completamente SPA in AEM - Modello ibrido {#level-3}

Questo livello di integrazione si basa sul secondo livello, consentendo la modifica della maggior parte dei contenuti del SPA esterno in AEM.

### Non disponi ancora di un consumer esterno per il contenuto headless, ad esempio un&#39;applicazione a pagina singola (SPA). {#do-not-have-a-spa}

Se l’obiettivo è quello di creare un nuovo SPA che consuma senza problemi contenuti da AEM, puoi utilizzare funzioni quali Frammenti di contenuto per gestire i contenuti headless e creare un SPA con AEM framework dell’editor SPA.

Utilizzando l’editor di SPA, il SPA non solo consuma contenuti da AEM, ma è anche completamente modificabile all’interno di AEM dagli autori di contenuti, offrendoti la flessibilità della distribuzione headless e della modifica contestuale in AEM.

## Requisiti e prerequisiti {#requirements-prerequisites}

Ci sono diversi requisiti prima di iniziare il progetto di AEM headless.

### Conoscenza {#knowledge}

* GraphQL
* Creare esperienze di sviluppo SPA con i framework React o Angular
* AEM di base per la creazione di frammenti di contenuto e l’utilizzo dell’editor

### Strumenti {#tools}

* Accesso alla sandbox per i test di distribuzione del progetto
* Istanza di sviluppo locale per la modellazione e il test dei dati
* SPA esterna esistente o altro consumatore del contenuto AEM headless

## Definizione del progetto {#defining-your-project}

Per ogni progetto di successo è importante definire chiaramente non solo i requisiti del progetto, ma anche i ruoli e le responsabilità.

### Ambito {#scope}

E&#39; molto importante avere un ambito di applicazione ben definito per il progetto. Ambito informa i criteri di accettazione e consente di stabilire una definizione di fatto.

La prima domanda che dovete farvi è &quot;Cosa sto cercando di ottenere con AEM Headless?&quot; In generale, la risposta dovrebbe essere che in futuro disponi o disporrai di un’applicazione di esperienza che hai creato con i tuoi strumenti di sviluppo non in combinazione con AEM. Questa applicazione di esperienza potrebbe essere un’app mobile, un sito web o qualsiasi altra applicazione per l’esperienza con i clienti finali. L’obiettivo per utilizzare AEM Headless è quello di alimentare l’applicazione di esperienza con contenuti creati, memorizzati e gestiti in AEM con API all’avanguardia che richiamerebbero AEM Headless per recuperare contenuti o persino contenuti CRUD completamente direttamente dall’applicazione di esperienza. Se questo non è quello che si desidera fare, probabilmente si desidera [tornare alla documentazione AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) e trovare la sezione che meglio si adatta a ciò che si desidera eseguire.

### Ruoli e responsabilità {#roles-responsibilities}

I ruoli di ogni singolo progetto variano, ma quelli importanti da considerare nel contenuto di AEM sviluppo headless sono:

* [Administrator](#administrator)
* [Autore del contenuto](#content-author)
* [Modellatore di contenuti](#content-modeler)
* [Developer (Sviluppatore)](#developer)

#### Amministratore {#administrator}

L&#39;amministratore è responsabile della configurazione e della configurazione di base del sistema. Ad esempio, l’amministratore configurerà la tua organizzazione all’interno del sistema di gestione utenti di Adobe, denominato Identity Management System (IMS). L’amministratore sarà il primo utente dell’organizzazione a ricevere un invito e-mail da Adobe dopo che l’organizzazione è stata creata per Adobe in IMS. L’amministratore potrà accedere a IMS e aggiungere utenti di altri utenti.

Una volta configurati dall’amministratore, gli utenti avranno le autorizzazioni per accedere a tutte le risorse di AEM per svolgere il loro lavoro come collaboratori per la distribuzione dell’applicazione di esperienza utilizzando AEM Headless.

L’amministratore deve essere l’utente che imposta AEM e prepara l’ambiente di runtime per consentire agli [autori di contenuti](#content-author) di creare e aggiornare contenuti e agli [sviluppatori](#developer) di utilizzare API che recuperano o modificano contenuti per le applicazioni di esperienza.

#### Autore del contenuto {#content-author}

Gli autori dei contenuti creano e gestiscono i contenuti consegnati senza problemi da AEM. Gli autori di contenuti utilizzano funzioni AEM quali Frammenti di contenuto e la console Risorse per gestirne i contenuti.

Gli autori dei contenuti devono tenere presenti le seguenti best practice.

#### Piano per la localizzazione {#localization}

Piano di traduzione e localizzazione all&#39;inizio del progetto. Considera &quot;Internationalization Project Manager&quot; come un utente distinto la cui responsabilità è quella di definire quali contenuti devono essere tradotti e cosa no, e quali contenuti tradotti possono essere modificati dai produttori di contenuti regionali o locali.

Crea un piano per la localizzazione dei contenuti necessaria.

* Hai solo bisogno di lingue diverse o anche lingue diverse da adottare per le specifiche regionali?
* È necessario che contenuti rich media come immagini o video siano diversi per diverse impostazioni internazionali?

Fai clic sul flusso di lavoro di aggiornamento del contenuto . Qual è il processo di approvazione che il sistema deve supportare? È possibile utilizzare AEM flussi di lavoro per automatizzare questo processo?

Tieni presente che la tua [gerarchia di contenuti](#content-hierarchy) può essere sfruttata per semplificare la localizzazione.

Consulta la sezione [risorse aggiuntive](#additional-resources) per la documentazione aggiuntiva sui flussi di lavoro AEM e gli strumenti di localizzazione.

##### Sfruttare la gerarchia dei contenuti {#content-hierarchy}

La gerarchia delle cartelle può risolvere due problemi principali relativi alla gestione dei contenuti:

* [Localizzazione](#localization) : AEM gestisce la localizzazione dei contenuti mantenendo copie dei contenuti in cartelle specifiche per le impostazioni internazionali.
* Organizzazione : le cartelle vengono utilizzate per definire una gerarchia di contenuti necessaria per supportare le esigenze di localizzazione e per gestire in modo logico i frammenti di contenuto.

AEM consente una struttura dei contenuti molto flessibile e una gerarchia può essere arbitrariamente grande. Tuttavia è importante tenere presente che eventuali modifiche nella struttura delle cartelle possono avere conseguenze indesiderate per le query esistenti che [si basano sul percorso del contenuto.](#developer) Pertanto, una gerarchia ben definita, chiaramente definita in anticipo, può essere estremamente utile per gli autori dei contenuti.

Le cartelle possono anche essere limitate per consentire solo alcuni tipi di contenuto (in base a Modelli per frammenti di contenuto). In genere si consiglia di specificare sempre in modo esplicito quali modelli sono consentiti per tutte le cartelle nella gerarchia. Specifica del contenuto consentito per una determinata cartella:

* Impedisce agli autori di contenuti di creare contenuti che non appartengono alla cartella.
* Ottimizza il processo di creazione dei contenuti filtrando i tipi di contenuto consentiti nella cartella durante la creazione per mostrare solo i tipi di contenuto validi.

La creazione di una struttura di contenuto appropriata rende più facile coordinare l’authoring di contenuti headless tra i diversi canali al fine di ottimizzare il riutilizzo dei contenuti. L&#39;utilizzo dei contenuti su più canali migliorerà notevolmente l&#39;efficienza della produzione dei contenuti e la gestione dei cambiamenti.

##### Stabilire buone convenzioni di denominazione {#naming-conventions}

I nomi dei frammenti di contenuto devono essere descrittivi per gli autori dei contenuti. AEM gestisce in modo trasparente l’escape e/o il troncamento dei nomi utilizzati a livello di archivio. Pertanto, i nomi logici forniti dagli autori dei contenuti devono essere sempre leggibili e rappresentare i contenuti.

* Nome non valido: `cta_btn_1`
* Nome: `Call To Action Button`

Consulta la sezione [risorse aggiuntive](#additional-resources) per la documentazione aggiuntiva sulle convenzioni di denominazione AEM pagina.

##### Non estendere la nidificazione dei contenuti {#content-nesting}

[I ](#content-fragments) frammenti di contenuto vengono utilizzati in AEM per creare contenuti headless. AEM supporta fino a dieci livelli di nidificazione dei contenuti per i frammenti di contenuto. Tuttavia, è importante tenere presente che AEM dovrà risolvere in modo iterativo ogni riferimento definito nel frammento di contenuto padre, quindi verificare se ci sono riferimenti figlio in tutti gli elementi di pari livello. Queste operazioni possono aumentare rapidamente e diventare un problema di prestazioni.

Come regola generale, i riferimenti ai frammenti di contenuto non devono essere nidificati oltre i cinque livelli.

#### Modellatore di contenuti {#content-modeler}

I modellatori di contenuti analizzano i requisiti dei dati che devono essere consegnati senza problemi e definiscono la struttura di tali dati. Queste strutture sono denominate [Modelli di frammento di contenuto](#content-fragment-models) in AEM. I modelli per frammenti di contenuto vengono utilizzati come base per i frammenti di contenuto creati dagli autori dei contenuti.

Un approccio utile quando si definiscono modelli di frammenti di contenuto, consiste nel creare modelli da associare ai componenti UX delle applicazioni che utilizzeranno il contenuto.

Poiché gli autori dei contenuti interagiscono continuamente con i modelli durante la creazione di nuovi contenuti, l’allineamento dei modelli all’UX li aiuta a visualizzare l’esperienza digitale risultante. Facendo un ulteriore passo avanti, puoi assegnare icone ai Modelli di frammento di contenuto che rappresentano l’elemento UX in modo che gli autori possano selezionare in modo intuitivo il modello corretto in base ai suggerimenti visivi.

#### Developer (Sviluppatore) {#developer}

Gli sviluppatori sono responsabili di unire i contenuti creati senza problemi AEM al consumatore di tali contenuti, che spesso possono essere un’applicazione a pagina singola (SPA), un’app web progressiva (PWA), un negozio di web o un altro servizio esterno a AEM.

GraphQL funge da &quot;colla&quot; tra AEM e consumatori di contenuti headless. GraphQL è la lingua che richiede AEM per il contenuto necessario.

Gli sviluppatori devono tenere presenti alcuni consigli di base durante la pianificazione delle query:

* Le query non devono basarsi su un percorso fisso (`ByPath`) per recuperare i frammenti di contenuto.
   * [Gli autori dei contenuti dispongono di un controllo completo sulla ](#content-hierarchy) gerarchia dei frammenti di contenuto e possono apportare modifiche tali da interrompere tale query.
   * Le query devono invece optare per i riferimenti al modello di frammento di contenuto con parametri di query dinamici per filtrare i risultati e generare il payload desiderato.
* Per ottenere le migliori prestazioni delle query, utilizza sempre query persistenti in AEM. Questi sono trattati più avanti nel percorso.
* GraphQL è progettato per essere dichiarativo seguendo il motto &quot;Chiedi esattamente ciò di cui hai bisogno, e ottieni esattamente quello.&quot; Ciò significa che durante la creazione di query GraphQL, evita sempre query di tipo `select *` che è possibile creare in un database relazionale.

Per una [tipica implementazione headless utilizzando AEM,](#level-1) lo sviluppatore non richiede alcuna conoscenza della codifica del AEM.

### Requisiti di prestazioni {#performance-requirements}

Affinché un progetto abbia successo, le prestazioni devono essere considerate prima di creare qualsiasi contenuto.

Devi comprendere le aspettative degli utenti/visitatori e progettarle. Impostare gli obiettivi del livello di servizio (SLOs) e misurarli per capire se si soddisfano le aspettative degli utenti.

#### Pattern di traffico {#traffic-patterns}

Per capire il traffico e i modelli di traffico inizia raccogliendo ciò che si sa dal passato e poi proiettare verso la crescita prevista nei prossimi anni. Alcune delle variabili più importanti da considerare:

* Quante chiamate API si aspettano all’ora/giorno/mese ed è possibile ottenere picchi e stagionalità?
* Quanti autori di contenuti diversi esistono?
* Quanti autori di contenuti prevedete di lavorare contemporaneamente?
* Qual è la frequenza degli aggiornamenti dei contenuti?
* Quanti modelli di contenuto sono necessari?
* Quante istanze di modelli saranno necessarie?

#### Aggiorna frequenza {#update-frequency}

Spesso diverse sezioni di esperienze hanno diverse frequenze di aggiornamenti dei contenuti. È importante per poter perfezionare le configurazioni di CDN e cache. Questo è importante anche per i [Modelli di contenuto](#content-modeler) in quanto progettano modelli per rappresentare il tuo contenuto. Considera:

* Alcuni tipi di contenuto devono scadere dopo un determinato periodo di tempo?
* Esistono elementi specifici dell’utente e quindi non possono essere memorizzati nella cache?

## Novità {#what-is-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Comprendere le nozioni di base AEM funzioni headless.
* Conoscere i prerequisiti per l&#39;utilizzo di AEM funzionalità headless.
* Presta attenzione AEM livelli di integrazione headless.
* Puoi definire il tuo progetto in termini di ambito.

Continua il tuo percorso AEM headless rivedendo il documento [Path to Your First Experience Using AEM Headless](path-to-first-experience.md) dove imparerai come impostare gli strumenti necessari e come iniziare a pensare alla modellazione dei dati in AEM.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di sviluppo headless esaminando il documento [Percorso della prima esperienza con AEM headless,](path-to-first-experience.md), di seguito sono riportate alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino nel percorso headless.

* [Introduzione all’architettura di Adobe Experience Manager as a Cloud Service](/help/core-concepts/architecture.md)  - Comprendere AEM come struttura di un Cloud Service
* [AEM Tutorials headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) : utilizza questi tutorial pratici per scoprire come utilizzare le varie opzioni per la distribuzione di contenuti agli endpoint headless con AEM e scegliere ciò che è più adatto alle tue esigenze.
* [Gestione dei contenuti headless tramite API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) : segui questo corso per una panoramica dell’API GraphQL implementata in AEM. È necessaria l’autenticazione tramite AdobeID.
* [AEM guide WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  - Questo progetto GitHub include applicazioni di esempio che evidenziano AEM API GraphQL.
* [Concetti di authoring](/help/sites-cloud/authoring/getting-started/concepts.md)  - Documentazione tecnica per l’ambiente di authoring di AEM, con dettagli sulla configurazione di authoring-pubblicazione
* [Pubblicazione delle pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  - Documentazione tecnica per la pubblicazione dei contenuti su AEM
* [Convenzioni di denominazione](/help/implementing/developing/introduction/naming-conventions.md)  - Documentazione tecnica sulle restrizioni di denominazione delle pagine in AEM
* [Multi Site Manager e Traduzione](/help/sites-cloud/administering/msm-and-translation.md)  - Documentazione tecnica su AEM potenti funzioni di traduzione
* [Flussi di lavoro AEM](/help/sites-cloud/authoring/workflows/overview.md)  - Documentazione tecnica su come automatizzare i flussi di lavoro in AEM
* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) : documentazione tecnica per i frammenti di contenuto.
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)  - Documentazione tecnica per i modelli per frammenti di contenuto.
* [Documentazione tecnica](https://graphql.org)  GraphQL - Definizione GraphQL (collegamento esterno)
* [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) : documentazione tecnica che spiega come creare richieste di accesso e distribuzione di frammenti di contenuto
* [API REST di Assets](/help/assets/content-fragments/assets-api-content-fragments.md) : documentazione tecnica che spiega come creare e modificare frammenti di contenuto (e altre risorse)
* [Query persistenti](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching)  - Documentazione tecnica sulle query persistenti in AEM
* [Cuffia e senza testa in AEM](/help/implementing/developing/headful-headless.md)  - Una discussione completa dei livelli di integrazione headless disponibili in AEM
