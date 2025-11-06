---
title: Come strutturare i vari elementi - La tua app e il tuo contenuto in AEM headless
description: In questa parte del Percorso per sviluppatori AEM Headless, scoprirai come realizzare il tuo progetto AEM utilizzando i frammenti di contenuto, le chiamate GraphQL, le chiamate REST API e la tua applicazione, e prepararlo per la pubblicazione.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 100%

---

# Come strutturare i vari elementi - La tua app e il tuo contenuto in AEM headless {#put-it-all-together}

In questa parte del [Percorso per sviluppatori AEM headless](overview.md), scoprirai come utilizzare lo strumento di sviluppo AEM e l’SDK Headless per realizzare l’applicazione.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come aggiornare i contenuti tramite le API di AEM Assets](update-your-content.md) hai imparato ad aggiornare il contenuto headless esistente in AEM tramite API e ora dovresti:

* Comprendere l’API HTTP di AEM Assets.

## Obiettivo {#objective}

Questo articolo ha lo scopo di aiutarti a capire come strutturare la tua applicazione AEM headless:

* Scoprire l’SDK di AEM Headless e gli strumenti di sviluppo necessari
* Impostare un runtime di sviluppo locale per simulare il contenuto prima della pubblicazione
* Comprendere le nozioni di base di AEM sulla replica dei contenuti

## L’SDK di AEM {#the-aem-sdk}

L’SDK di AEM viene utilizzato per generare e distribuire il codice personalizzato. È lo strumento principale per sviluppare e testare un’applicazione headless prima di pubblicarla. Contiene i seguenti artefatti:

* Il file jar Quickstart: un file jar eseguibile che può essere utilizzato per impostare sia un’istanza di authoring che di pubblicazione
* Strumenti di Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX®
* Jar API Java™ - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per lo sviluppo rispetto ad AEM
* Jar Javadoc: i javadoc per il jar API Java™

## L’SDK di AEM Headless {#the-aem-headless-sdk}

Diverso dall’SDK di AEM, l’**SDK headless** di AEM è un set di librerie che possono essere utilizzate dai client per interagire in modo rapido e semplice con le API di AEM headless tramite HTTP.

Per ulteriori informazioni, consulta [SDK headless per AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=it).

## Strumenti di sviluppo aggiuntivi {#additional-development-tools}

Oltre all’SDK di AEM, sono necessari strumenti aggiuntivi per lo sviluppo e il test locale del codice e del contenuto:

* Java™
* Git
* Apache Maven
* La libreria Node.js
* L’IDE che preferisci

Poiché AEM è un’applicazione Java™, è necessario installare Java™ e l’SDK Java™ per supportare lo sviluppo di AEM as a Cloud Service.

Git è ciò che utilizzerai per gestire il controllo del codice sorgente e per tenere traccia delle modifiche a Cloud Manager e, quindi, distribuirle su un’istanza di produzione.

AEM utilizza Apache Maven per creare progetti generati dall’archetipo del progetto Maven di AEM. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente di esecuzione di codice JavaScript utilizzato per lavorare con le risorse front-end di un `ui.frontend` sottoprogetto di un progetto AEM. Node.js è distribuito con npm, il gestore di pacchetti Node.js utilizzato per gestire le dipendenze JavaScript.

## Panoramica dei componenti di un sistema AEM {#components-of-an-aem-system-at-a-glance}

Ora, osserviamo le parti costitutive di un ambiente AEM.

Un ambiente AEM completo è costituito da authoring, pubblicazione e Dispatcher. Questi stessi componenti sono resi disponibili nel runtime di sviluppo locale per facilitare l’anteprima del codice e del contenuto prima di pubblicarlo.

* Il **servizio di authoring** è il luogo in cui gli utenti interni creano, gestiscono e visualizzano in anteprima i contenuti.

* Il **servizio di pubblicazione** è considerato l’ambiente “live” ed è normalmente ciò con cui gli utenti finali interagiscono. I contenuti vengono modificati e approvati nel servizio di authoring e quindi distribuiti al servizio di pubblicazione. Il modello di implementazione più comune per le applicazioni headless AEM consiste nella connessione della versione di produzione dell’applicazione a un servizio di pubblicazione AEM.

* **Il Dispatcher** è un server web statico potenziato con il modulo Dispatcher di AEM. Memorizza nella cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti di codice o contenuto acquisiti dall’applicazione headless, devi distribuire gli aggiornamenti al runtime AEM locale, che include le istanze locali dei servizi di authoring e pubblicazione AEM.

Assicurati di prendere nota delle distinzioni tra ogni componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più. Ad esempio, prova gli aggiornamenti del contenuto sull’authoring o testa il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un Dispatcher e un server http Apache saranno sempre posti davanti a un’istanza di pubblicazione AEM. Fornisce servizi di caching e sicurezza per il sistema AEM, pertanto è fondamentale testare il codice e gli aggiornamenti di contenuto anche in Dispatcher.

## Anteprima del codice e del contenuto localmente con l’ambiente di sviluppo locale {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Per preparare il progetto headless di AEM per il lancio, è necessario assicurarsi che tutte le sue parti costitutive funzionino bene.

Per farlo, devi mettere tutto insieme: codice, contenuto e configurazione e testarlo in un ambiente di sviluppo locale per renderlo disponibile dal vivo.

L’ambiente di sviluppo locale si articola in tre aree principali:

1. Progetto AEM: questo progetto contiene tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori di AEM lavoreranno
1. Local AEM Runtime: versioni locali dei servizi di authoring e pubblicazione AEM utilizzati per distribuire il codice dal progetto AEM
1. Esecuzione del Dispatcher locale: una versione locale del server Web Apache httpd che include il modulo Dispatcher

Una volta configurato l’ambiente di sviluppo locale, puoi simulare la gestione dei contenuti nell’app React distribuendo localmente un server nodo statico.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## Passaggio successivo {#whats-next}

Ora che hai completato questa parte del percorso per sviluppatori headless di AEM, dovresti:

* Avere familiarità con gli strumenti di sviluppo di AEM
* Comprendere il flusso di lavoro di sviluppo locale

Continua il tuo percorso headless di AEM passando alla prossima revisione del documento [Come andare in diretta con la tua applicazione headless](/help/journey-headless/developer/go-live.md) dove si trasmette il tuo progetto headless di AEM in diretta!

## Risorse aggiuntive {#additional-resources}

* [L’SDK AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configurare un ambiente di sviluppo di AEM locale](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=it)
* [SDK headless di AEM per browser lato client (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [SDK headless di AEM per lato server/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [SDK headless di AEM per Java™](https://github.com/adobe/aem-headless-client-java)
* [Introduzione ad AEM come CMS headless](/help/headless/introduction.md)
* [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
