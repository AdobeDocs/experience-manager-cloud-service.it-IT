---
title: Sviluppo headless per AEM Sites as a Cloud Service
description: Scopri come AEM potenti funzionalità headless del Cloud Service come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---


# Sviluppo headless per AEM Sites as a Cloud Service {#headless-development}

Scopri come AEM potenti funzionalità headless del Cloud Service come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.

## Panoramica {#overview}

L’implementazione headless sta diventando sempre più importante per la distribuzione di esperienze al pubblico, ovunque si trovi e indipendentemente dal canale utilizzato.

L’implementazione headless dimentica la gestione di pagine e componenti come avviene nelle soluzioni complete stack e ibride e si concentra sulla creazione di frammenti di contenuto riutilizzabili e neutri per i canali e sulla loro distribuzione cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l’implementazione di esperienze web.

![Modelli di implementazione AEM](assets/aem-implementation-models.png)

## Confronto tra headful e headless {#headful-headless}

Questo documento si concentra sul modello di implementazione senza testa di AEM completo. Tuttavia headful contro headless non deve essere una scelta binaria in AEM. Le funzioni headless consentono di gestire e distribuire i contenuti a diversi endpoint, consentendo agli autori di contenuti di modificare applicazioni a pagina singola. Tutto in AEM.

>[!TIP]
>
>Per ulteriori informazioni, consulta il documento [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) .

## AEM come Cloud Service e headless {#aem-headless}

AEM come Cloud Service è uno strumento flessibile per il modello di implementazione headless offrendo tre potenti servizi:

1. Modelli di contenuto
   * I modelli di contenuto sono una rappresentazione strutturata del contenuto.
   * Questi sono definiti dagli architetti delle informazioni nell’editor AEM modello di frammento di contenuto .
   * I modelli di contenuto fungono da base per i frammenti di contenuto.
1. Frammenti di contenuto
   * I frammenti di contenuto sono istanze di modelli di contenuto.
   * Vengono create dagli autori di contenuti tramite l’editor Frammento di contenuto AEM.
   * Vengono memorizzati in AEM Assets e gestiti nell’interfaccia utente di amministrazione delle risorse.
1. API di contenuto per la consegna
   * L’API GraphQL di AEM supporta la distribuzione di frammenti di contenuto.
   * L’API REST di AEM Assets supporta le operazioni CRUD relative ai frammenti di contenuto.
   * La consegna diretta del contenuto è possibile anche con l&#39;esportazione JSON del componente core [Frammento di contenuto .](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## Guide introduttive headless {#getting-started}

Le guide introduttive headless forniscono un percorso semplice per creare, gestire e distribuire esperienze utilizzando AEM come Cloud Service in cinque passaggi. Ogni guida si basa sul precedente, quindi si consiglia di esplorarle in modo approfondito e in ordine.

1. [Creazione di una configurazione](getting-started/create-configuration.md)
1. [Creazione di un modello di frammento di contenuto](getting-started/create-content-model.md)
1. [Creazione di una cartella di risorse](getting-started/create-assets-folder.md)
1. [Creazione di un frammento di contenuto](getting-started/create-content-fragment.md)
1. [Accesso e distribuzione di frammenti di contenuto](getting-started/create-api-request.md)

## Pubblico {#audience}

Le attività descritte in [Guide introduttive headless](#getting-started) sono necessarie per una dimostrazione completa e di base delle funzionalità headless AEM. Chiunque abbia accesso come amministratore a un’istanza di test AEM può seguire queste guide per comprendere la consegna headless in AEM, anche se qualcuno con esperienza di sviluppo è ideale.

Tuttavia, in una situazione di produzione, le attività saranno eseguite da diversi utenti tipo in un numero variabile di volte. Esempio:

* **** Gli amministratori dovranno impostare la configurazione iniziale e la struttura delle cartelle per il contenuto normalmente una sola volta o sporadicamente.
* **Gli** architetti di informazioni in genere aggiungeranno nuovi modelli man mano che le esigenze dell&#39;organizzazione evolvono.
* **Gli autori dei contenuti** creeranno continuamente nuovi contenuti come Frammenti di contenuto in base ai modelli definiti dagli architetti.

Le Guide introduttive headless indicano chi eseguirebbe in genere le attività descritte e con quale frequenza.

## Passaggio successivo {#next-step}

Pronti per saperne di più? Per iniziare, leggi la prima parte della Guida introduttiva a Headless: [Creazione di una configurazione.](getting-started/create-configuration.md)
