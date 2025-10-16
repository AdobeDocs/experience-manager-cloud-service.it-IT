---
title: Come pubblicare con la tua applicazione headless
description: In questa parte del Percorso per sviluppatori AEM Headless, scopri come distribuire un’applicazione headless in tempo reale prendendo il codice locale nel Git e spostandolo nel Git di Cloud Manager per la pipeline CI/CD.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 100%

---

# Come pubblicare con la tua applicazione headless {#go-live}

In questa parte del [Percorso per sviluppatori AEM headless](overview.md), scopri come distribuire in tempo reale un’applicazione headless prendendo il codice locale nel Git e spostandolo nel Git di Cloud Manager per la pipeline CI/CD.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso headless AEM, [Come strutturare i vari elementi - La tua app e il tuo contenuto in AEM headless](put-it-all-together.md), hai imparato a utilizzare gli strumenti di sviluppo AEM per strutturare tutti i facet del tuo progetto.

Questo articolo si basa sulle nozioni di base che ti faranno capire come preparare il progetto AEM headless da pubblicare.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la pipeline di pubblicazione headless AEM e le considerazioni sulle prestazioni di cui devi tener conto prima di pubblicare l’applicazione.

* Proteggi e ridimensiona l’applicazione prima del lancio
* Monitoraggio dei problemi di prestazioni e debug

Per preparare l’applicazione AEM headless per il lancio, segui le best practice descritte di seguito.

## Proteggi e ridimensiona l’applicazione headless prima del lancio {#secure-and-scale-before-launch}

1. Configura [Autenticazione basata su token](/help/headless/security/authentication.md) con le tue richieste GraphQL
1. Configura [Memorizzazione in cache](/help/implementing/dispatcher/caching.md).

## Struttura del modello e output GraphQL {#structure-vs-output}

* Evita di creare query con output superiore a 15 kb di JSON (gzip compresso). I file JSON lunghi richiedono un uso intensivo delle risorse per l’analisi da parte dell’applicazione client.
* Evita più di cinque livelli nidificati di gerarchie di frammenti. Livelli aggiuntivi rendono difficile per gli autori dei contenuti valutare l’impatto delle loro modifiche.
* Utilizza query con più oggetti invece di modellare query con gerarchie di dipendenza all’interno dei modelli. Ciò consente una maggiore flessibilità a lungo termine per ristrutturare l’output JSON senza dover apportare molte modifiche al contenuto.

## Massimizza il rapporto Hit-cache CDN {#maximize-cdn}

* Non utilizzare query GraphQL dirette, a meno che stia richiedendo contenuto in tempo reale dalla superficie.
   * Utilizza le query persistenti quando possibile.
   * Fornisci a CDN un TTL di oltre 600 secondi per consentire alla CDN di memorizzarli nella cache.
   * AEM può calcolare l’impatto di una modifica del modello sulle query esistenti.
* Dividi i file JSON/le query GraphQL tra la frequenza di variazione del contenuto bassa e alta in modo da ridurre il traffico client verso CDN e assegnare un TTL più alto. Questo riduce al minimo la riconvalida da parte della CDN di JSON con il server di origine.
* Per invalidare attivamente il contenuto dalla rete CDN, utilizza la rimozione temporanea. Questo consente alla rete CDN di scaricare nuovamente il contenuto senza causare una perdita della cache.

## Migliora il tempo di download dei contenuti headless {#improve-download-time}

* Assicurati che i client HTTP utilizzino HTTP/2.
* Assicurati che i client HTTP accettino la richiesta di intestazioni per gzip.
* Riduci al minimo il numero di domini utilizzati per ospitare JSON e gli artefatti di riferimento.
* Sfrutta `Last-modified-since` per aggiornare le risorse.
* Utilizza l’output `_reference` nel file JSON per iniziare a scaricare risorse senza dover analizzare file JSON completi.

## Distribuzione alla produzione {#deploy-to-production}

Una volta verificato che tutto sia stato testato e funzioni correttamente, puoi inviare gli aggiornamenti di codice a un [archivio Git centralizzato di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=it).

Dopo il caricamento su Cloud Manager, gli aggiornamenti possono essere distribuiti su AEM as a Cloud Service utilizzando la [pipeline CI/CD di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it).

Puoi iniziare a implementare il codice utilizzando la pipeline CI/CD di Cloud Manager, ampiamente trattata in [Implementazione di pacchetti di contenuti tramite Cloud Manager e il gestore di pacchetti](/help/implementing/deploying/overview.md).

## Monitoraggio delle prestazioni {#performance-monitoring}

Per garantire agli utenti la migliore esperienza possibile quando utilizzano l’applicazione AEM headless, è importante monitorare le metriche delle prestazioni chiave, come illustrato di seguito:

* Convalida delle versioni di anteprima e di produzione dell’app
* Verifica delle pagine di stato di AEM per lo stato di disponibilità del servizio corrente
* Accesso ai rapporti sulle prestazioni
   * Prestazioni della distribuzione
      * Prestazioni CDN (Fastly): verificare il numero di chiamate, la velocità della cache, i tassi di errore e il traffico del payload
      * Server di origine - numero di chiamate, tassi di errore, carichi della CPU, traffico del payload
   * Prestazioni dell’authoring
      * Verifica del numero di utenti, di richieste e caricamento
* Accesso ai rapporti specifici sulle prestazioni di app e spazio
   * Una volta che il server è attivo, controllare se le metriche generali sono verde/arancione/rosso, quindi identificare problemi specifici dell’app
   * Aprire i rapporti di cui sopra, filtrati per app o spazio (ad esempio Photoshop per desktop, paywall)
   * Utilizzare le API del registro Splunk per accedere alle prestazioni del servizio e dell’applicazione
   * Contattare l’Assistenza clienti in caso di altri problemi.

## Risoluzione dei problemi {#troubleshooting}

### Debugging {#debugging}

Segui queste best practice come approccio generale al debug:

* Convalida funzionalità e prestazioni con la versione di anteprima dell’applicazione
* Convalida funzionalità e prestazioni con la versione di produzione dell’applicazione
* Convalida con JSON l’anteprima dell’Editor di frammento di contenuto
* Controlla JSON nell’applicazione client per verificare la presenza di problemi nell’applicazione client o nella distribuzione
* Controlla l’uso da parte di JSON di GraphQL per verificare la presenza di problemi relativi al contenuto della cache o ad AEM

### Registrazione di un bug con Support {#logging-a-bug-with-support}

Per registrare in modo efficiente un bug con il supporto nel caso sia necessaria ulteriore assistenza, effettua le seguenti operazioni:

* Se necessario, acquisisci le schermate del problema
* Documenta un modo per riprodurre il problema
* Documenta il contenuto con cui il problema si ripresenta
* Segnala un problema tramite il portale di supporto AEM con la priorità appropriata

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il Percorso per sviluppatori AEM headless! Ora dovresti aver appreso quanto segue:

* La differenza tra distribuzione headless e headful dei contenuti.
* Le funzionalità headless di AEM.
* Come organizzare un progetto AEM headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come pubblicare con un progetto AEM headless.
* Cosa fare dopo la pubblicazione.

Hai già lanciato il tuo primo progetto AEM Headless oppure possiedi ormai tutte le conoscenze necessarie per farlo. Ottimo lavoro!

### Esplora le applicazioni a pagina singola {#explore-spa}

Il potenziale headless in AEM non si ferma qui. Nella [Guida introduttiva al percorso](getting-started.md#integration-levels) abbiamo accennato a come AEM supporta non solo la distribuzione headless e i modelli tradizionali full-stack, ma anche i modelli ibridi che combinano i vantaggi di entrambi.

Se questo tipo di flessibilità è un elemento necessario per il tuo progetto, continua con l’ulteriore parte opzionale del percorso, [Come creare applicazioni a pagina singola (SPA) con AEM](create-spa.md).

## Risorse aggiuntive {#additional-resources}

* [Introduzione ad AEM come CMS headless](/help/headless/introduction.md)
* [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
* [Panoramica della distribuzione in AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Utilizzare Cloud Manager per distribuire il codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it)
* [Integra l’archivio Git di Cloud Manager con un archivio Git esterno e distribuisci un progetto in AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=it)
