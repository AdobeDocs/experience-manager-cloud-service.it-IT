---
title: Accesso e distribuzione di frammenti di contenuto Guida di avvio rapido senza titolo
description: L’API REST di Assets consente di gestire i frammenti di contenuto e l’API GraphQL consente una distribuzione semplice e senza precedenti del contenuto dei frammenti di contenuto.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Accesso e distribuzione di frammenti di contenuto Guida di avvio rapido senza titolo {#accessing-delivering-content-fragments}

L’API REST di Assets consente di gestire i frammenti di contenuto e l’API GraphQL consente una distribuzione semplice e senza precedenti del contenuto dei frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto, ](create-content-fragment.md) potete utilizzare AEM API per distribuirli senza problemi.

* [L&#39;](/help/assets/content-fragments/graphql-api-content-fragments.md) API GraphQL consente di creare richieste per l&#39;accesso e la distribuzione di frammenti di contenuto.
* [L’](/help/assets/content-fragments/assets-api-content-fragments.md) API REST di Risorse consente di creare e modificare frammenti di contenuto (e altre risorse).

Il resto di questa guida sarà incentrato sull&#39;accesso GraphQL e sulla distribuzione di frammenti di contenuto.

## Come distribuire un frammento di contenuto utilizzando GraphQL {#how-to-deliver-a-content-fragment}

Gli architetti delle informazioni dovranno progettare query per i loro endpoint di canale per distribuire i contenuti. Queste query in genere devono essere considerate solo una volta per endpoint per modello. Ai fini di questa guida introduttiva, sarà necessario crearne solo una.

1. Accedi al AEM come Cloud Service e dal menu principale seleziona **Strumenti -> Risorse -> GraphQL**
   * In alternativa, aprite la pagina direttamente in `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL è un editor di query interno al browser per GraphQL. Potete utilizzarlo per creare query per recuperare i frammenti di contenuto e distribuirli direttamente come JSON.
   * Il pannello a sinistra consente di creare la query.
   * Nel pannello a destra vengono visualizzati i risultati.
   * L&#39;editor di query dispone di completamento del codice e tasti di scelta rapida per eseguire facilmente la query.
      ![Editor GraphiQL](../assets/graphiql.png)

1. Supponendo che il modello creato sia stato denominato `person` con i campi `firstName`, `lastName` e `position`, è possibile creare una semplice query per recuperare il contenuto del frammento di contenuto.

   ```
   query {
     persons {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Immettete la query nel pannello a sinistra.
   ![Query GraphiQL](../assets/graphiql-query.png)

1. Fare clic sul pulsante **Esegui query** o utilizzare il tasto di scelta rapida `Ctrl-Enter` e i risultati vengono visualizzati come JSON nel pannello a destra.
   ![Risultati GraphiQL](../assets/graphiql-results.png)

1. Fare clic sul collegamento **Docs** in alto a destra della pagina per visualizzare la documentazione contestuale per facilitare la creazione di query che si adattano ai propri modelli.
   ![Documentazione GraphiQL](../assets/graphiql-documentation.png)

GraphQL consente query strutturate in grado di eseguire il targeting non solo di set di dati specifici o di singoli oggetti dati, ma anche di fornire elementi specifici degli oggetti, risultati nidificati, offre supporto per le variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegna in eccesso, e consente invece la consegna in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

È tutto! È ora possibile avere una conoscenza di base della gestione dei contenuti headless in AEM. Naturalmente, ci sono molte altre risorse in cui è possibile approfondire la conoscenza delle funzioni disponibili.

* **Browser**  di configurazione - Per informazioni dettagliate sul browser di configurazione AEM
* **[Frammenti](/help/assets/content-fragments/content-fragments.md)**  di contenuto - Per informazioni dettagliate sulla creazione e la gestione di frammenti di contenuto
* **[Supporto per i frammenti di contenuto  API](/help/assets/content-fragments/assets-api-content-fragments.md)**  AEM Assets HTTP - Per informazioni dettagliate sull&#39;accesso AEM contenuto direttamente tramite l&#39;API HTTP, tramite operazioni CRUD (Creazione, lettura, aggiornamento, eliminazione)
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  - Per informazioni dettagliate su come distribuire senza problemi i frammenti di contenuto
