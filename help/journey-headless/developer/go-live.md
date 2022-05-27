---
title: Come andare in diretta con la tua applicazione headless
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come distribuire in diretta un’applicazione headless prendendo il codice locale in Git e spostandolo in Cloud Manager Git per la pipeline CI/CD.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Come andare in diretta con la tua applicazione headless {#go-live}

In questa parte del [AEM Percorso di sviluppatori headless](overview.md), scopri come distribuire in tempo reale un’applicazione headless prendendo il codice locale in Git e spostandolo in Cloud Manager Git per la pipeline CI/CD.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Come mettere tutto insieme - La tua app e il tuo contenuto in AEM headless](put-it-all-together.md) hai imparato a utilizzare gli strumenti di sviluppo AEM per mettere insieme tutti i facet del tuo progetto.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il vostro progetto AEM headless per andare live.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la pipeline di pubblicazione headless AEM e le considerazioni sulle prestazioni di cui devi tener conto prima di iniziare a utilizzare l’applicazione.

* Proteggere e ridimensionare l’applicazione prima di Launch
* Monitoraggio dei problemi di prestazioni e debug

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
Per preparare l&#39;applicazione senza testa AEM per il lancio, segui le best practice descritte di seguito.

## Proteggere e ridimensionare l&#39;applicazione headless prima di Launch {#secure-and-scale-before-launch}

1. Configura [Autenticazione basata su token](/help/headless/security/authentication.md) con le richieste GraphQL
1. Configura [Memorizzazione in cache](/help/implementing/dispatcher/caching.md).

## Struttura del modello e uscita GraphQL {#structure-vs-output}

* Evita di creare query con output superiore a 15 kb di JSON (gzip compresso). I file JSON lunghi richiedono un uso intensivo delle risorse per l’analisi da parte dell’applicazione client.
* Evitare più di cinque livelli nidificati di gerarchie di frammenti. Livelli aggiuntivi rendono difficile per gli autori dei contenuti considerare l’impatto delle loro modifiche.
* Utilizzare query con più oggetti invece di modellare query con gerarchie di dipendenza all’interno dei modelli. Ciò consente una maggiore flessibilità a lungo termine per ristrutturare l’output JSON senza dover apportare molte modifiche al contenuto.

## Massimizza il rapporto Hit cache CDN {#maximize-cdn}

* Non utilizzare query GraphQL dirette, a meno che tu non richieda contenuto live dalla superficie.
   * Utilizza le query persistenti quando possibile.
   * Fornisci TTL CDN oltre 600 secondi per consentire alla CDN di memorizzarle nella cache.
   * AEM calcolare l&#39;impatto di una modifica del modello sulle query esistenti.
* Dividi i file JSON/le query GraphQL tra una variazione del tasso di contenuto bassa e alta al fine di ridurre il traffico client a CDN e assegnare un valore TTL più alto. Questo riduce al minimo la validità della rete CDN con il server di origine.
* Per annullare attivamente la validità del contenuto dalla rete CDN, utilizza la funzione di rimozione Soft. Questo consente alla rete CDN di scaricare nuovamente il contenuto senza causare una perdita di cache.

## Migliorare il tempo di download dei contenuti headless {#improve-download-time}

* Assicurati che i client HTTP utilizzino HTTP/2.
* Assicurati che i client HTTP accetti la richiesta di intestazioni per gzip.
* Riduci al minimo il numero di domini utilizzati per ospitare JSON e gli artefatti di riferimento.
* Sfruttamento `Last-modified-since` per aggiornare le risorse.
* Utilizzo `_reference` output in file JSON per iniziare a scaricare risorse senza dover analizzare file JSON completi.

## Distribuzione in produzione {#deploy-to-production}

Una volta verificato che tutto sia stato testato e funzioni correttamente, puoi inviare gli aggiornamenti di codice a un [archivio Git centralizzato in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

Dopo il caricamento su Cloud Manager, gli aggiornamenti possono essere distribuiti su AEM as a Cloud Service utilizzando [pipeline CI/CD di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Puoi iniziare a distribuire il codice sfruttando la pipeline CI/CD di Cloud Manager, ampiamente illustrata [qui](/help/implementing/deploying/overview.md).

## Monitoraggio delle prestazioni {#performance-monitoring}

Per garantire agli utenti la migliore esperienza possibile quando si utilizza l&#39;applicazione senza testa di AEM, è importante monitorare le metriche delle prestazioni chiave, come illustrato di seguito:

* Convalida delle versioni di anteprima e produzione dell’app
* Verificare le pagine di stato AEM per lo stato di disponibilità del servizio corrente
* Accedere ai rapporti sulle prestazioni
   * Prestazioni
      * Prestazioni CDN (finale): verifica il numero di chiamate, la velocità della cache, i tassi di errore e il traffico del payload
      * Server di origine - numero di chiamate, tassi di errore, carichi della CPU, traffico del payload
   * Prestazioni dell’autore
      * Verifica il numero di utenti, richieste e caricamento
* Accedere ai rapporti sulle prestazioni specifici per app e spazio
   * Una volta che il server è attivo, controlla se le metriche generali sono verde/arancione/rosso, quindi identifica problemi specifici dell&#39;app
   * Apri gli stessi rapporti sopra filtrati nell’app o nello spazio (ad esempio desktop Photoshop, paywall)
   * Utilizza le API del registro Splunk per accedere alle prestazioni del servizio e dell&#39;applicazione
   * Contatta l’Assistenza clienti in caso di altri problemi.

## Risoluzione dei problemi {#troubleshooting}

### Debugging {#debugging}

Segui queste best practice come approccio generale al debug:

* Convalida funzionalità e prestazioni con la versione di anteprima dell&#39;applicazione
* Convalidare funzionalità e prestazioni con la versione di produzione dell&#39;applicazione
* Convalida con l’anteprima JSON dell’Editor frammento di contenuto
* Inspect JSON nell’applicazione client per verificare la presenza di applicazioni client o problemi di consegna
* Inspect utilizza JSON utilizzando GraphQL per verificare la presenza di problemi relativi al contenuto o AEM memorizzati nella cache

### Registrazione di un bug con il supporto {#logging-a-bug-with-support}

Per registrare in modo efficiente un bug con il supporto nel caso in cui ti occorra ulteriore assistenza, segui i passaggi seguenti:

* Se necessario, scegli le schermate del problema
* Documentare un modo per riprodurre il problema
* Documentare il contenuto riprodotto dal problema con
* Segnala un problema tramite il portale di supporto AEM con la priorità appropriata

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

### Esplora applicazioni a pagina singola {#explore-spa}

I negozi senza testa in AEM non devono fermarsi qui, però. Si potrebbe ricordare nel [Introduzione al percorso](getting-started.md#integration-levels) abbiamo discusso brevemente come AEM supporta non solo la consegna headless e i modelli tradizionali full-stack, ma anche i modelli ibridi che combinano i vantaggi di entrambi.

Se questo tipo di flessibilità è un elemento necessario per il progetto, continuate con l&#39;ulteriore parte opzionale del percorso, [Come creare applicazioni a pagina singola (SPA) con AEM.](create-spa.md)

## Risorse aggiuntive {#additional-resources}

* [Panoramica della distribuzione in AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Utilizzare Cloud Manager per distribuire il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integra l’archivio Git di Cloud Manager con un archivio Git esterno e distribuisci un progetto per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
