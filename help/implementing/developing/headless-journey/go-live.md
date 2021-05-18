---
title: Come andare in diretta con la tua applicazione headless
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come distribuire in diretta un’applicazione headless prendendo il codice locale in Git e spostandolo in Cloud Manager Git per la pipeline CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: a2588f420258522cc3a4b7b10f4ab52f2dd669d8
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---

# Come andare in diretta con la tua applicazione headless {#go-live}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) scopri come distribuire in tempo reale un’applicazione headless prendendo il codice locale in Git e spostandolo in Cloud Manager Git per la pipeline CI/CD.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Come mettere insieme tutto - La tua app e il tuo contenuto in AEM senza testa](put-it-all-together.md) hai imparato a preparare il tuo progetto senza testa AEM per andare in diretta e dovresti ora:

* Comprendi i requisiti per andare in diretta.

Questo articolo si basa su questi elementi fondamentali per capire come portare in diretta il tuo progetto headless AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la pipeline di pubblicazione headless AEM e le considerazioni sulle prestazioni di cui hai bisogno prima di iniziare a utilizzare l’applicazione.

* Scopri l’SDK per AEM e gli strumenti di sviluppo necessari
* Imposta un runtime di sviluppo locale per simulare il contenuto prima di iniziare a vivere
* Informazioni di base sulla replica dei contenuti AEM e sulla memorizzazione nella cache
* Proteggere e ridimensionare l’applicazione prima di Launch
* Monitoraggio dei problemi di prestazioni e debug

## L&#39;SDK AEM {#the-aem-sdk}

Contiene i seguenti artefatti:

* Il file jar di Quickstart - un file jar eseguibile che può essere utilizzato per impostare sia un autore che un&#39;istanza di pubblicazione
* Strumenti Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX
* Java API Jar - La dipendenza Java Jar/Maven che espone tutte le API Java consentite che possono essere utilizzate per sviluppare rispetto a AEM
* Javadoc jar - i javadocs per il jar delle API Java

## Strumenti di sviluppo {#development-tools}

Oltre all’SDK di AEM, avrai bisogno di strumenti aggiuntivi per lo sviluppo e il test locale del codice e del contenuto:

* Java
* L&#39;SDK AEM
* Git
* Apache Maven
* La libreria Node.js
* L&#39;IDE che preferisci

Poiché AEM è un&#39;applicazione Java, devi installare Java e Java SDK per supportare lo sviluppo di AEM come Cloud Service.

L&#39;SDK AEM viene utilizzato per generare e distribuire il codice personalizzato. È lo strumento principale di cui hai bisogno per testare la tua applicazione headless prima di andare in diretta.

Git è ciò che utilizzerai per gestire il controllo del codice sorgente e per archiviare le modifiche a Cloud Manager e quindi distribuirle in un’istanza di produzione.

AEM utilizza Apache Maven per creare progetti generati dall’archetipo AEM progetto Maven. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente di runtime JavaScript utilizzato per lavorare con le risorse front-end di un sottoprogetto ui.frontend di un progetto AEM. Node.js è distribuito con npm, è il gestore di pacchetti Node.js de facto, utilizzato per gestire le dipendenze JavaScript.

## Panoramica dei componenti di un sistema AEM {#components-of-an-aem-system-at-a-glance}

Un ambiente AEM completo è costituito da Author, Publish e Dispatcher. Questi stessi componenti saranno resi disponibili nel runtime di sviluppo locale per facilitare l’anteprima del codice e del contenuto prima di iniziare a usare il programma.

* **Il** servizio Author consente agli utenti interni di creare, gestire e visualizzare in anteprima i contenuti.

* **Il servizio Publish** è considerato l’ambiente &quot;Live&quot; ed è tipicamente quello con cui gli utenti finali interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio Author, vengono distribuiti al servizio Publish. Il modello di implementazione più comune con AEM applicazioni headless consiste nella connessione della versione di produzione dell’applicazione a un servizio AEM Publish.

* **Il** Dispatcher è un server web statico integrato con il modulo dispatcher AEM. Memorizza in cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti di codice o contenuto che verranno acquisiti dall&#39;applicazione headless, devi distribuire gli aggiornamenti al runtime AEM locale, che include le istanze locali dei servizi di authoring e pubblicazione AEM.

Assicurati di prendere nota delle distinzioni tra ogni componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più. Ad esempio, prova gli aggiornamenti del contenuto sull’autore o testa il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un dispatcher e un server http Apache si siederanno sempre davanti a un&#39;istanza di pubblicazione AEM. Forniscono servizi di memorizzazione in cache e sicurezza per il sistema AEM, quindi è fondamentale testare il codice e gli aggiornamenti di contenuto anche rispetto al dispatcher.

Una volta verificato che tutto sia stato testato e funzioni correttamente, puoi inviare gli aggiornamenti di codice a un archivio Git centralizzato in Cloud Manager.

Una volta caricati su Cloud Manager, gli aggiornamenti possono essere distribuiti su AEM come Cloud Service utilizzando la pipeline CI/CD di Cloud Manager.

## Anteprima del codice e del contenuto localmente con l’ ambiente di sviluppo locale {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Per preparare il progetto senza testa AEM per il lancio, è necessario assicurarsi che tutte le parti costitutive del progetto funzionino bene.

Per farlo, devi mettere tutto insieme: codice, contenuto e configurazione e testalo in un ambiente di sviluppo locale per renderlo disponibile dal vivo.

L&#39;ambiente di sviluppo locale si articola in tre aree principali:

1. Progetto AEM: conterrà tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori AEM lavoreranno
1. Local AEM Runtime - versioni locali dei servizi di authoring e pubblicazione AEM che verranno utilizzati per distribuire il codice dal progetto AEM
1. Il Dispatcher Runtime locale - una versione locale del server Web Apache htttpd che include il modulo Dispatcher

Una volta configurato l’ambiente di sviluppo locale, puoi simulare il servizio dei contenuti all’app React distribuendo localmente un server Node statico.

Per maggiori informazioni sulla configurazione di un ambiente di sviluppo locale e di tutte le dipendenze necessarie per l’anteprima dei contenuti, consulta [Distribuzione di produzione con un servizio di pubblicazione AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Distribuzione a produzione {#deploy-to-production}

Una volta testati localmente tutto il codice e il contenuto, puoi iniziare una distribuzione di produzione con AEM.

Puoi iniziare a distribuire il codice sfruttando la pipeline CI/CD di Cloud Manager, ampiamente trattata [qui](/help/implementing/deploying/overview.md).

## Prepara la tua applicazione AEM headless per GoLive {#prepare-your-aem-headless-application-for-golive}

Ora è il momento di preparare l&#39;applicazione AEM headless per il lancio, seguendo le best practice descritte di seguito.

### Proteggi e ridimensiona l&#39;applicazione headless prima di Launch {#secure-and-scale-before-launch}

1. Configurare [Autenticazione basata su token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
1. Webhook protetti
1. Configurare la memorizzazione in cache e la scalabilità

### Struttura del modello e uscita GraphQL {#structure-vs-output}

* Evita di creare query con output superiore a 15 kb di JSON (gzip compresso). I file JSON lunghi richiedono un uso intensivo delle risorse per l’analisi da parte dell’applicazione client.
* Evitare più di cinque livelli nidificati di gerarchie di frammenti. Livelli aggiuntivi rendono difficile per gli autori dei contenuti considerare l’impatto delle loro modifiche.
* Utilizzare query con più oggetti invece di modellare query con gerarchie di dipendenza all’interno dei modelli. Ciò consente una maggiore flessibilità a lungo termine per ristrutturare l’output JSON senza dover apportare molte modifiche al contenuto.

### Massimizza il rapporto Hit cache CDN {#maximize-cdn}

* Non utilizzare query GraphQL dirette, a meno che tu non richieda contenuto live dalla superficie.
   * Utilizza invece query persistenti.
   * Fornisci TTL CDN oltre 600 secondi in modo che la CDN possa memorizzarli nella cache.
   * AEM calcolare l&#39;impatto di una modifica del modello sulle query esistenti.
* Dividi i file JSON/le query GraphQL tra una variazione del tasso di contenuto bassa e alta al fine di ridurre il traffico client a CDN e assegnare un valore TTL più alto. Questo riduce al minimo la validità della rete CDN con il server di origine.
* Per annullare attivamente la validità del contenuto dalla rete CDN, utilizza la funzione di rimozione Soft. Questo consente alla rete CDN di scaricare nuovamente il contenuto senza causare una perdita di cache.

### Migliorare il tempo di download dei contenuti headless {#improve-download-time}

* Assicurati che i client HTTP utilizzino HTTP/2.
* Assicurati che i client HTTP accetti la richiesta di intestazioni per gzip.
* Riduci al minimo il numero di domini utilizzati per ospitare JSON e gli artefatti di riferimento.
* Utilizza `Last-modified-since` per aggiornare le risorse.
* Utilizza l’output `_reference` nel file JSON per iniziare a scaricare le risorse senza dover analizzare file JSON completi.

## Monitoraggio delle prestazioni {#performance-monitoring}

Per garantire agli utenti la migliore esperienza possibile quando si utilizza l’applicazione senza testa di AEM, è importante monitorare le metriche delle prestazioni chiave, come illustrato di seguito:

* Convalida delle versioni di anteprima e produzione dell’app
* Verificare le pagine di stato AEM per lo stato di disponibilità del servizio corrente
* Accedere ai rapporti sulle prestazioni
   * Prestazioni
      * Flast (CDN) - numero di chiamate, tasso di cache, tassi di errore, traffico payload
      * Server di origine - numero di chiamate, tassi di errore, carichi della CPU, traffico del payload
   * Prestazioni dell’autore
      * Verifica il numero di utenti, richieste e caricamento
* Accedere ai rapporti sulle prestazioni specifici per app e spazio
   * Una volta che il server è attivo, controlla se le metriche generali sono verde/arancione/rosso, quindi identifica problemi specifici dell&#39;app
   * Apri gli stessi rapporti sopra filtrati in app/spazio (ad esempio desktop Photoshop, paywall, ecc.)
   * Utilizza le API del registro Splunk per accedere alle prestazioni del servizio e dell&#39;applicazione
   * Contatta l’Assistenza clienti in caso di altri problemi.

## Risoluzione dei problemi {#troubleshooting}

### Debug {#debugging}

Segui queste best practice come approccio generale al debug:

* Convalida funzionalità e prestazioni con la versione di anteprima dell&#39;applicazione
* Convalidare funzionalità e prestazioni con la versione di produzione dell&#39;applicazione
* Convalida con l’anteprima JSON dell’Editor frammento di contenuto
* Inspect JSON nell’applicazione client per verificare la presenza di applicazioni client o problemi di consegna
* Inspect utilizza JSON utilizzando GraphQL per verificare la presenza di problemi relativi al contenuto o AEM memorizzati nella cache

### Registrazione di un bug con supporto {#logging-a-bug-with-support}

Per registrare in modo efficiente un bug con il supporto nel caso in cui ti occorra ulteriore assistenza, segui i passaggi seguenti:

* Se necessario, scegli le schermate del problema
* Documentare un modo per riprodurre il problema
* Documentare il contenuto riprodotto dal problema con
* Segnala un problema tramite il portale di supporto AEM con la priorità appropriata

## Novità {#what-is-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Scopri AEM Nozioni di base sulla replica dei contenuti e sulla memorizzazione nella cache.
* Scopri come configurare gli strumenti necessari per simulare il funzionamento live dell’applicazione headless.
* Scopri come proteggere e ridimensionare l’applicazione prima di Launch.
* Scopri come monitorare i problemi di prestazioni e debug.

## Il Percorso Termina - O Lo Fa? {#journey-ends}

Congratulazioni! Hai completato il Percorso di sviluppo headless AEM! Ora dovresti avere una comprensione di:

* Differenza tra distribuzione headless e headful dei contenuti.
* AEM senza testa.
* Come organizzare e AEM il progetto Headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come andare a vivere con un progetto senza testa AEM.
* Cosa fare dopo il go-live.

Hai già lanciato il tuo primo progetto AEM Headless o ora hai tutte le conoscenze necessarie per farlo. Ottimo lavoro!

I negozi senza testa in AEM non devono fermarsi qui, però. È possibile ricordare che nella [Guida introduttiva del percorso](getting-started.md#integration-levels) abbiamo discusso brevemente di come AEM non solo supporta la consegna headless e i modelli tradizionali full-stack, ma anche il supporto di modelli ibridi che combinano i vantaggi di entrambi.

Se questo tipo di flessibilità è necessario per il progetto, continua con la parte facoltativa e aggiuntiva del percorso [Come creare applicazioni a pagina singola (SPA) con AEM.](create-spa.md)

## Risorse aggiuntive {#additional-resources}

* [Configurare Un Ambiente AEM Locale](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [L’SDK AEM come Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Panoramica della distribuzione in AEM come Cloud Service](/help/implementing/deploying/overview.md)
* [Utilizzare Cloud Manager per distribuire il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integrare l’archivio Git di Cloud Manager con un archivio Git esterno e distribuire un progetto da AEM come Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/master/help/implementing/developing/headless-journey/access-your-content.md)