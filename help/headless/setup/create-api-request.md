---
title: Creare una richiesta API - Configurazione headless
description: Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e API REST di Assets di AEM per gestire i frammenti di contenuto.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 88%

---

# Creare una richiesta API - Configurazione headless {#accessing-delivering-content-fragments}

Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e API REST di Assets di AEM per gestire i frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto](create-content-fragment.md), puoi utilizzare le API di AEM per distribuirle senza problemi.

* L’[API GraphQL](/help/headless/graphql-api/content-fragments.md) consente di creare richieste per accedere e distribuire frammenti di contenuto. Questa API offre la serie più solida di funzionalità per eseguire query e utilizzare contenuti di frammenti di contenuto.
   * Per utilizzare l’API, [definisci e abilita gli endpoint in AEM](/help/headless/graphql-api/graphql-endpoint.md) e, se necessario, [installa l’Interfaccia GraphiQL](/help/headless/graphql-api/graphiql-ide.md).
* È disponibile una selezione di [API AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) da utilizzare con i frammenti di contenuto.

Il resto di questa guida è incentrato sull’accesso a GraphQL e sulla distribuzione di frammenti di contenuto.

## Abilitare endpoint GraphQL {#enable-graphql-endpoint}

Prima di poter utilizzare le API GraphQL, è necessario creare un endpoint GraphQL.

Per informazioni dettagliate, consulta [Gestire gli endpoint di GraphQL in AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Query del contenuto tramite GraphQL con GraphiQL

Gli architetti di informazioni progettano query per i loro endpoint di canale per distribuire contenuti. Prendi in considerazioni queste query una sola volta per endpoint, per modello. Ai fini di questa guida introduttiva, è sufficiente crearne una.

GraphiQL è un IDE, incluso nel tuo ambiente AEM e accessibile/visibile dopo aver [configurato gli endpoint](#enable-graphql-endpoint).

Per informazioni dettagliate, vedere [Utilizzo dell&#39;IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

GraphQL consente query strutturate in grado di eseguire il targeting non solo di set di dati specifici o di singoli oggetti di dati, ma anche di fornire elementi specifici degli oggetti, risultati nidificati, offerte di supporto per variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegne in eccesso, e consente invece la distribuzione in massa esattamente di ciò che è necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

Tutto qui. Ora hai una conoscenza di base della gestione dei contenuti headless in AEM. Sono disponibili molte altre risorse da approfondire per una comprensione completa delle funzioni disponibili.

* **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md)**: per informazioni dettagliate sulla creazione e la gestione dei frammenti di contenuto
* **[Supporto per frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**: per informazioni dettagliate sull’accesso diretto ai contenuti AEM tramite l’API HTTP, mediante operazioni CRUD (Crea, Leggi, Aggiorna, Elimina)
* **[API di GraphQL](/help/headless/graphql-api/content-fragments.md)**: per informazioni dettagliate su come distribuire i frammenti di contenuto in modo corretto

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).
