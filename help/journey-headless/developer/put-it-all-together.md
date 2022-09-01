---
title: Come mettere tutto insieme - La tua app e il tuo contenuto in AEM headless
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come prendere il tuo progetto AEM compresi i frammenti di contenuto, le chiamate GraphQL, le chiamate API REST e l’applicazione e prepararlo per il loro lancio.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 9%

---

# Come mettere tutto insieme - La tua app e il tuo contenuto in AEM headless {#put-it-all-together}

In questa parte del [AEM Percorso di sviluppatori headless](overview.md), scopri come utilizzare lo strumento di sviluppo AEM e l’SDK Headless per unire l’applicazione.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Come aggiornare i contenuti tramite le API di AEM Assets](update-your-content.md) hai imparato ad aggiornare il contenuto headless esistente in AEM tramite API e ora dovresti:

* Comprendere l’API HTTP di AEM Assets.

## Obiettivo {#objective}

Questo articolo ha lo scopo di aiutarti a capire come mettere insieme la tua AEM applicazione headless:

* Scopri l’SDK AEM Headless e gli strumenti di sviluppo necessari
* Impostazione di un runtime di sviluppo locale per simulare il contenuto prima di iniziare a vivere
* Nozioni di base sulla replica dei contenuti AEM

## L&#39;SDK AEM {#the-aem-sdk}

L&#39;SDK AEM viene utilizzato per generare e distribuire il codice personalizzato. È lo strumento principale di cui hai bisogno per sviluppare e testare la tua applicazione senza testa prima di andare in diretta. Contiene i seguenti artefatti:

* Il file jar di Quickstart - un file jar eseguibile che può essere utilizzato per impostare sia un autore che un&#39;istanza di pubblicazione
* Strumenti Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX®
* Jar API Java™ - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per sviluppare rispetto a AEM
* Javadoc jar - i javadocs per il jar API Java™

## L&#39;SDK AEM Headless {#the-aem-headless-sdk}

Diverso dall&#39;SDK AEM, il AEM **SDK headless** è un set di librerie che possono essere utilizzate dai client per interagire in modo rapido e semplice con AEM API headless tramite HTTP.

Per ulteriori informazioni sull’SDK senza titolo AEM, consulta la sezione [documentazione qui](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html).

## Strumenti di sviluppo aggiuntivi {#additional-development-tools}

Oltre all’SDK di AEM, sono necessari strumenti aggiuntivi per lo sviluppo e il test locale del codice e del contenuto:

* Java™
* Git
* Apache Maven
* La libreria Node.js
* L&#39;IDE che preferisci

Poiché AEM è un&#39;applicazione Java™, è necessario installare Java™ e l&#39;SDK Java™ per supportare lo sviluppo di AEM as a Cloud Service.

Git è ciò che utilizzi per gestire il controllo del codice sorgente e per archiviare le modifiche a Cloud Manager e quindi distribuirle in un’istanza di produzione.

AEM utilizza Apache Maven per generare progetti generati dall’archetipo del progetto Maven AEM. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente di runtime JavaScript utilizzato per lavorare con le risorse front-end di un progetto AEM `ui.frontend` sottoprogetto. Node.js è distribuito con npm, è di fatto Node.js Package Manager, utilizzato per gestire le dipendenze JavaScript.

## Panoramica dei componenti di un sistema AEM {#components-of-an-aem-system-at-a-glance}

Ora, osserviamo le parti costitutive di un ambiente AEM.

Un ambiente AEM completo è costituito da Author, Publish e Dispatcher. Questi stessi componenti sono resi disponibili nel runtime di sviluppo locale per facilitare l’anteprima del codice e del contenuto prima di iniziare a usare il programma.

* Il **servizio di authoring** è il luogo in cui gli utenti interni creano, gestiscono e visualizzano in anteprima i contenuti.

* Il **servizio di pubblicazione** è considerato l’ambiente “live” ed è normalmente ciò con cui gli utenti finali interagiscono. I contenuti vengono modificati e approvati nel servizio di authoring e quindi distribuiti al servizio di pubblicazione. Il modello di implementazione più comune per le applicazioni headless AEM consiste nella connessione della versione di produzione dell’applicazione a un servizio di pubblicazione AEM.

* **Dispatcher** è un server web statico integrato con il modulo Dispatcher AEM. Memorizza in cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti di codice o contenuto acquisiti dall&#39;applicazione headless, devi distribuire gli aggiornamenti al runtime AEM locale, che include le istanze locali dei servizi di authoring e pubblicazione AEM.

Assicurati di prendere nota delle distinzioni tra ogni componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più. Ad esempio, prova gli aggiornamenti del contenuto sull’autore o testa il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un’istanza di Dispatcher e un server http Apache si troveranno sempre davanti a un’istanza di pubblicazione AEM. Forniscono servizi di caching e sicurezza per il sistema AEM, pertanto è fondamentale testare il codice e gli aggiornamenti di contenuto anche in Dispatcher.

## Anteprima del codice e del contenuto localmente con l’ambiente di sviluppo locale {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Per preparare il progetto senza testa AEM per il lancio, è necessario assicurarsi che tutte le parti costitutive del progetto funzionino bene.

Per farlo, devi mettere tutto insieme: codice, contenuto e configurazione e testalo in un ambiente di sviluppo locale per renderlo disponibile dal vivo.

L&#39;ambiente di sviluppo locale si articola in tre aree principali:

1. Progetto AEM: questo progetto contiene tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori AEM lavoreranno
1. Local AEM Runtime - versioni locali dei servizi di authoring e pubblicazione AEM utilizzati per distribuire il codice dal progetto AEM
1. Il Dispatcher Runtime locale - una versione locale del server Web Apache htttpd che include il modulo Dispatcher

Una volta configurato l’ambiente di sviluppo locale, puoi simulare il servizio dei contenuti all’app React distribuendo localmente un server Node statico.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## Novità {#whats-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Verificare gli strumenti di sviluppo AEM
* Comprendere il flusso di lavoro di sviluppo locale

Continua il tuo percorso AEM senza testa passando alla prossima revisione del documento [Come andare in diretta con la tua applicazione headless](/help/journey-headless/developer/go-live.md) dove si prende il vostro progetto AEM Headless in diretta!

## Risorse aggiuntive {#additional-resources}

* [L’SDK AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configurare Un Ambiente AEM Locale](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=it)
* [SDK AEM Headless per browser lato client (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [AEM Headless SDK per server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [AEM Headless SDK per Java™](https://github.com/adobe/aem-headless-client-java)

