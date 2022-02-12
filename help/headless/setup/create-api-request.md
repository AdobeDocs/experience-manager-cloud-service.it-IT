---
title: Creare una richiesta API - Configurazione headless
description: Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e AEM API REST di Assets per gestire i frammenti di contenuto.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Creare una richiesta API - Configurazione headless {#accessing-delivering-content-fragments}

Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e AEM API REST di Assets per gestire i frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto,](create-content-fragment.md) puoi utilizzare le API AEM per distribuirle senza problemi.

* [API GraphQL](/help/headless/graphql-api/content-fragments.md) consente di creare richieste per accedere e distribuire frammenti di contenuto. Questa API offre la serie più solida di funzionalità per eseguire query e utilizzare contenuti di frammenti di contenuto.
   * Per utilizzare questo [gli endpoint devono essere definiti e abilitati in AEM](/help/headless/graphql-api/graphql-endpoint.md)e, se necessario, il [Interfaccia GraphiQL installata](/help/headless/graphql-api/graphiql-ide.md).
* [API REST di Assets](/help/assets/content-fragments/assets-api-content-fragments.md) consente di creare e modificare frammenti di contenuto (e altre risorse).

Il resto di questa guida sarà incentrato sull’accesso GraphQL e la distribuzione di frammenti di contenuto.

## Abilita endpoint GraphQL

Prima di poter utilizzare le API GraphQL, è necessario creare un endpoint GraphQL.

1. Passa a **Strumenti**, **Risorse**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. La **Crea nuovo endpoint GraphQL** si aprirà la finestra di dialogo . Qui puoi specificare:
   * **Nome**: nome del punto finale; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza il menu a discesa per selezionare la configurazione richiesta.
1. Conferma con **Crea**.
1. Nella console a **Percorso** verrà ora visualizzato in base alla configurazione creata in precedenza. Questo è il percorso utilizzato per eseguire le query GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Ulteriori dettagli sull&#39;abilitazione [Gli endpoint GraphQL si trovano qui](/help/headless/graphql-api/graphql-endpoint.md).

## Query del contenuto tramite GraphQL con GraphiQL

Gli architetti di informazioni dovranno progettare query per i loro endpoint di canale per distribuire contenuti. In genere queste query devono essere considerate solo una volta per endpoint per modello. Ai fini di questa guida introduttiva, è sufficiente crearne una.

GraphiQL è un IDE che può essere installato in un ambiente AEM. Segui i passaggi seguenti [Utilizzo dell&#39;IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md) per eseguire l’installazione nell’ambiente AEM.

1. Accedi AEM as a Cloud Service e accedi all&#39;interfaccia GraphiQL:
   * Esempio: `https://<host>:<port>/content/graphiql.html`.

1. L’IDE GraphiQL è un editor di query interno al browser per GraphQL. Puoi utilizzarlo per creare query per recuperare frammenti di contenuto e distribuirli direttamente come JSON.
   * Il pannello a sinistra ti consente di creare la query.
   * Nel pannello a destra vengono visualizzati i risultati.
   * L’editor delle query dispone del completamento del codice e dei tasti di scelta rapida per eseguire facilmente la query.
      ![Editor GraphiQL](../assets/graphiql.png)

1. Supponendo che il modello che abbiamo creato si chiama `person` con campi `firstName`, `lastName`e `position`, possiamo creare una semplice query per recuperare il contenuto del frammento di contenuto.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Inserisci la query nel pannello a sinistra.
   ![Query GraphiQL](../assets/graphiql-query.png)

1. Fai clic sul pulsante **Esegui query** o utilizzare `Ctrl-Enter` il tasto di scelta rapida e i risultati vengono visualizzati come JSON nel pannello di destra.
   ![Risultati GraphiQL](../assets/graphiql-results.png)

1. Fai clic sul pulsante **Documenti** link in alto a destra della pagina per visualizzare la documentazione contestuale per aiutarti a creare le query che si adattano ai tuoi modelli.
   ![Documentazione di GraphiQL](../assets/graphiql-documentation.png)

GraphQL consente query strutturate in grado di eseguire il targeting non solo di set di dati specifici o di singoli oggetti di dati, ma anche di fornire elementi specifici degli oggetti, risultati nidificati, offerte di supporto per variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegna in eccesso, e consente invece la distribuzione in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

Tutto qui! Ora hai una conoscenza di base della gestione dei contenuti headless in AEM. Naturalmente, ci sono molte altre risorse in cui puoi immergerti per una comprensione completa delle funzioni disponibili.

* **[Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)** - Per informazioni dettagliate sulla creazione e la gestione dei frammenti di contenuto
* **[Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)** - Per informazioni sull’accesso diretto AEM contenuto tramite l’API HTTP tramite operazioni CRUD (Crea, Leggi, Aggiorna, Elimina)
* **[API GraphQL](/help/headless/graphql-api/content-fragments.md)** - Per informazioni dettagliate su come distribuire i frammenti di contenuto senza problemi
