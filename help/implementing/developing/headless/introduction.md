---
title: Sviluppo senza testa per  AEM Sites come Cloud Service
description: L'utilizzo di potenti funzioni come Modelli di contenuto, Frammenti di contenuto e API GraphQL, AEM come Cloud Service, consente di gestire le esperienze centralmente e di distribuirle tra i canali.
translation-type: tm+mt
source-git-commit: 712a99095494ab333cf0ebb2ac9fffe3f5945f3b
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 3%

---


# Sviluppo senza testa per  AEM Sites come Cloud Service {#headless-development}

L&#39;utilizzo di potenti funzioni come Modelli di contenuto, Frammenti di contenuto e API GraphQL, AEM come Cloud Service, consente di gestire le esperienze centralmente e di distribuirle tra i canali.

## Panoramica {#overview}

L&#39;implementazione senza limiti di tempo sta diventando sempre più importante per la distribuzione di esperienze al pubblico, ovunque si trovi e indipendentemente dai canali.

L&#39;implementazione senza problemi dimentica la gestione delle pagine e dei componenti, come avviene nelle soluzioni complete per stack e ibridi, e si concentra sulla creazione di frammenti di contenuto versatili e versatili e sulla loro distribuzione multicanale. Si tratta di un modello di sviluppo moderno e dinamico per l&#39;implementazione di esperienze Web.

![Modelli di implementazione AEM](assets/aem-implementation-models.png)

## AEM come Cloud Service e senza testa {#aem-headless}

AEM come Cloud Service è uno strumento flessibile per il modello di implementazione senza testa, offrendo tre potenti servizi:

1. Modelli di contenuto
   * I modelli di contenuto sono una rappresentazione strutturata del contenuto.
   * Questi sono definiti dagli architetti delle informazioni nell&#39;editor AEM Content Fragment Model.
   * Modelli di contenuto fungono da base per i frammenti di contenuto.
1. Frammenti di contenuto
   * I frammenti di contenuto sono istanze di modelli di contenuto.
   * Questi vengono creati dagli autori di contenuti tramite l&#39;editor AEM frammenti di contenuto.
   * Vengono memorizzati in  AEM Assets e gestiti nell’interfaccia utente di amministrazione delle risorse.
1. Content API per la distribuzione
   * L&#39;API AEM GraphQL supporta la distribuzione di frammenti di contenuto.
   * L&#39;API REST di AEM Assets  supporta le operazioni CRUD dei frammenti di contenuto.
   * La distribuzione diretta del contenuto è possibile anche con l&#39;esportazione JSON del componente principale [frammento di contenuto.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## Guide introduttive senza testa {#getting-started}

Le Guide introduttive headless forniscono un percorso semplice per creare, gestire e distribuire esperienze utilizzando AEM come Cloud Service in cinque passaggi. Ogni guida si basa sul precedente, quindi si consiglia di esplorarle accuratamente e in ordine.

1. [Creazione di una configurazione](getting-started/create-configuration.md)
1. [Creazione di un modello di frammento di contenuto](getting-started/create-content-model.md)
1. [Creazione di una cartella di risorse](getting-started/create-assets-folder.md)
1. [Creazione di un frammento di contenuto](getting-started/create-content-fragment.md)
1. [Accesso e distribuzione di frammenti di contenuto](getting-started/create-api-request.md)

## Pubblico {#audience}

Le attività descritte in [Guide introduttive senza testa](#getting-started) sono necessarie per una dimostrazione completa e di base delle AEM funzionalità senza testa. Chiunque abbia accesso amministratore a un&#39;istanza di test AEM può seguire queste guide per comprendere la distribuzione senza problemi in AEM, anche se qualcuno con esperienza di sviluppatore è ideale.

Tuttavia, in una situazione di produzione, le attività saranno eseguite da persone diverse in un numero variabile di volte. Esempio:

* **Gli** amministratori dovranno impostare la configurazione iniziale e la struttura delle cartelle per il contenuto normalmente una sola volta o sporadicamente.
* **Gli** architetti delle informazioni in genere aggiungeranno nuovi modelli man mano che le esigenze dell&#39;organizzazione evolvono.
* **Gli** autori dei contenuti creeranno continuamente nuovi contenuti come frammenti di contenuto basati sui modelli definiti dagli architetti.

Le Guide introduttive senza titolo indicano chi esegue generalmente le attività descritte e con quale frequenza.

## Passaggio successivo {#next-step}

Pronti per saperne di più? Per iniziare, leggi la prima parte della Guida introduttiva per headless: [Creazione di una configurazione.](getting-started/create-configuration.md)
