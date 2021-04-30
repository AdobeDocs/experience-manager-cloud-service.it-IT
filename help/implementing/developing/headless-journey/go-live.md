---
title: Come andare in diretta con la tua applicazione headless
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come distribuire in diretta un’applicazione headless prendendo il codice locale in Git e spostandolo in Cloud Manager Git per la pipeline CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '1039'
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

* Informazioni di base sulla replica dei contenuti AEM e sulla memorizzazione nella cache
* Configura gli strumenti necessari per simulare il funzionamento live dell&#39;applicazione headless
* Proteggere e ridimensionare l’applicazione prima di Launch
* Monitoraggio dei problemi di prestazioni e debug

## Nozioni di base sulla replica dei contenuti e sulla memorizzazione nella cache {#content-replication-and-caching}

Un ambiente AEM completo è costituito da Author, Publish e Dispatcher.

* **Il** servizio Author consente agli utenti interni di creare, gestire e visualizzare in anteprima i contenuti.

* **Il servizio Publish** è considerato l’ambiente &quot;Live&quot; ed è tipicamente quello con cui gli utenti finali interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio Author, vengono distribuiti al servizio Publish.

* **Il** Dispatcher è un server web statico integrato con il modulo dispatcher AEM. Memorizza in cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

Il modello di implementazione più comune con AEM applicazioni headless consiste nella connessione della versione di produzione dell’applicazione a un servizio AEM Publish.

## Requisiti e configurazione {#requirements-and-configuration}

1. Imposta un [Runtime locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#install-java) utilizzando [AEM come SDK di Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
2. Installa i [contenuti di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e gli endpoint GraphQL successivi
3. Distribuisci e configura un [server dei nodi statici](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/production-deployment.html?lang=en#static-server).

## Proteggi e ridimensiona l&#39;applicazione headless prima di Launch {#secure-and-scale-before-launch}

1. Configurare [Autenticazione basata su token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
2. Webhook protetti
3. Configurare la memorizzazione in cache e la scalabilità

## Distribuzione a produzione {#deploy-to-production}

Dopo aver testato localmente tutto il codice e il contenuto, ora puoi iniziare una distribuzione di produzione con AEM.

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

## Monitoraggio {#monitoring}

### Come controllare le prestazioni complessive {#check-overall-performance}

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

Per garantire il corretto funzionamento dell’applicazione prima dell’avvio, si consiglia di seguire questi passaggi come approccio generale al debug:

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

Continua il tuo percorso AEM headless rivedendo il documento [Post Launch](post-launch.md) dove imparerai a mantenere la tua esperienza headless.

## Risorse aggiuntive {#additional-resources}
