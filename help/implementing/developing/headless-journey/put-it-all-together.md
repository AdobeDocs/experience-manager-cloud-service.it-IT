---
title: Come mettere tutto insieme - La tua app e il tuo contenuto in AEM headless
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come prendere il tuo progetto AEM compresi i frammenti di contenuto, le chiamate GraphQL, le chiamate API REST e l’applicazione e prepararlo per il loro lancio.
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Come mettere tutto insieme - La tua app e il tuo contenuto in AEM senza testa {#put-it-all-together}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) scopri come prendere il progetto AEM che include frammenti di contenuto, le chiamate GraphQL, le chiamate API REST e l’applicazione e come prepararlo per il lancio.

## La storia finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come aggiornare il contenuto tramite API AEM Assets](update-your-content.md) hai imparato ad aggiornare il contenuto esistente headless in AEM tramite API e ora devi:

* Comprendere l’API HTTP di AEM Assets.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il vostro progetto AEM headless per andare live.

## Obiettivo {#objective}

* Installa l&#39;SDK AEM per ottenere un runtime di sviluppo locale da utilizzare per testare il contenuto su
* Scopri gli strumenti di sviluppo necessari
* Verifica il codice e il contenuto localmente prima di iniziare a lavorare

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti di codice o contenuto che verranno acquisiti dall&#39;applicazione headless, devi distribuire gli aggiornamenti a un runtime AEM locale, che include le istanze locali dell&#39;istanza di authoring AEM e pubblicazione.

Assicurati di prendere nota delle distinzioni tra ciascun componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più - ad esempio, testare gli aggiornamenti di contenuto sull’autore o testare il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un dispatcher e un server http Apache si siederanno sempre davanti a un&#39;istanza di pubblicazione AEM. Forniscono servizi di memorizzazione in cache e sicurezza per il sistema AEM, quindi è fondamentale testare il codice e gli aggiornamenti di contenuto anche rispetto al dispatcher.

Una volta verificato che tutto sia stato testato e funzioni correttamente, puoi inviare gli aggiornamenti di codice a un archivio Git centralizzato in Cloud Manager.

Una volta caricati su Cloud Manager, gli aggiornamenti possono essere distribuiti su AEM come Cloud Service utilizzando la pipeline CI/CD di Cloud Manager.


## L&#39;SDK AEM {#the-aem-sdk}

L&#39;SDK AEM viene utilizzato per generare e distribuire il codice personalizzato. Contiene i seguenti artefatti:

* Il file jar di Quickstart - un file jar eseguibile che può essere utilizzato per impostare sia un autore che un&#39;istanza di pubblicazione
* Strumenti Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX
* Java API Jar - La dipendenza Java Jar/Maven che espone tutte le API Java consentite che possono essere utilizzate per sviluppare rispetto a AEM
* Javadoc jar - i javadocs per il jar delle API Java

## Configurazione ambiente di sviluppo locale {#local-development-environment}

Per preparare il progetto senza testa AEM per il lancio, è necessario assicurarsi che tutte le parti costitutive del progetto funzionino bene.

Per farlo, devi mettere tutto insieme - codice, contenuto e configurazione e testarlo in un ambiente di sviluppo locale per essere pronto al funzionamento.

L&#39;ambiente di sviluppo locale si articola in tre aree principali:

1. Progetto AEM: conterrà tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori AEM lavoreranno
1. Local AEM Runtime - versioni locali dei servizi di authoring e pubblicazione AEM che verranno utilizzati per distribuire il codice dal progetto AEM
1. Il Dispatcher Runtime locale - una versione locale del server Web Apache htttpd che include il modulo Dispatcher

## Strumenti di sviluppo {#development-tools}

Oltre all’SDK di AEM, avrai bisogno di strumenti aggiuntivi per lo sviluppo e il test locale del codice e del contenuto:

* Java
* Git
* Apache Maven
* La libreria Node.js
* L&#39;IDE che preferisci

Poiché AEM è un&#39;applicazione Java, devi installare Java e Java SDK per supportare lo sviluppo di AEM come Cloud Service.

Git è lo strumento che utilizzerai per gestire il controllo del codice sorgente e per archiviare le modifiche a Cloud Manager e quindi distribuirle in un’istanza di produzione.

AEM utilizza Apache Maven per creare progetti generati dall’archetipo AEM progetto Maven. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente di runtime JavaScript utilizzato per lavorare con le risorse front-end di un sottoprogetto ui.frontend di un progetto AEM. Node.js è distribuito con npm, è il gestore di pacchetti Node.js de facto, utilizzato per gestire le dipendenze JavaScript.

## Novità {#what-is-next}

Continua il tuo percorso AEM senza testa rivedendo il documento [Come andare in diretta con la tua applicazione senza testa](go-live.md) in cui prendi in diretta il tuo progetto senza testa AEM!

## Risorse aggiuntive {#additional-resources}

* [Configurazione ambiente di sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime) : scopri come installare gli strumenti necessari per iniziare a sviluppare per AEM
* [AEM come SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)  di Cloud Service: scopri in dettaglio l’SDK di AEM