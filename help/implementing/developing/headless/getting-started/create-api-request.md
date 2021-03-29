---
title: Guida rapida all’accesso e alla distribuzione di frammenti di contenuto senza intestazione
description: Scopri come utilizzare AEM API REST di Assets per gestire i frammenti di contenuto e l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Guida rapida all’accesso e alla distribuzione di frammenti di contenuto senza intestazione {#accessing-delivering-content-fragments}

Scopri come utilizzare AEM API REST di Assets per gestire i frammenti di contenuto e l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto, ](create-content-fragment.md) puoi utilizzare le API AEM per distribuirli senza problemi.

* [L’](/help/assets/content-fragments/graphql-api-content-fragments.md) API GraphQL consente di creare richieste di accesso e distribuzione di frammenti di contenuto.
* [L’](/help/assets/content-fragments/assets-api-content-fragments.md) API REST di Assets consente di creare e modificare frammenti di contenuto (e altre risorse).

Il resto di questa guida sarà incentrato sull’accesso GraphQL e la distribuzione di frammenti di contenuto.

## Come consegnare un frammento di contenuto utilizzando GraphQL {#how-to-deliver-a-content-fragment}

Gli architetti di informazioni dovranno progettare query per i loro endpoint di canale per distribuire contenuti. In genere queste query devono essere considerate solo una volta per endpoint per modello. Ai fini di questa guida introduttiva, è sufficiente crearne una.

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. Accedi a AEM come Cloud Service e accedi all&#39;interfaccia GraphiQL:
   * Esempio: `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL è un editor di query interno al browser per GraphQL. Puoi utilizzarlo per creare query per recuperare frammenti di contenuto e distribuirli direttamente come JSON.
   * Il pannello a sinistra ti consente di creare la query.
   * Nel pannello a destra vengono visualizzati i risultati.
   * L’editor delle query dispone del completamento del codice e dei tasti di scelta rapida per eseguire facilmente la query.
      ![Editor GraphiQL](../assets/graphiql.png)

1. Presupponendo che il modello creato sia stato denominato `person` con campi `firstName`, `lastName` e `position`, possiamo creare una semplice query per recuperare il contenuto del frammento di contenuto.

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

1. Fai clic sul pulsante **Esegui query** o utilizza la chiave di scelta rapida `Ctrl-Enter` e i risultati vengono visualizzati come JSON nel pannello di destra.
   ![Risultati GraphiQL](../assets/graphiql-results.png)

1. Fai clic sul collegamento **Documenti** in alto a destra della pagina per visualizzare la documentazione contestuale per aiutarti a creare le query che si adattano ai tuoi modelli.
   ![Documentazione di GraphiQL](../assets/graphiql-documentation.png)

GraphQL consente query strutturate in grado di eseguire il targeting non solo di set di dati specifici o di singoli oggetti di dati, ma anche di fornire elementi specifici degli oggetti, risultati nidificati, offerte di supporto per variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegna in eccesso, e consente invece la distribuzione in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

Tutto qui! Ora hai una conoscenza di base della gestione dei contenuti headless in AEM. Naturalmente, ci sono molte altre risorse in cui puoi immergerti per una comprensione completa delle funzioni disponibili.

* **Browser di configurazione** : per informazioni dettagliate sul browser di configurazione AEM
* **[Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)** : per informazioni dettagliate sulla creazione e la gestione dei frammenti di contenuto
* **[Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**  - Per informazioni dettagliate sull’accesso AEM contenuto direttamente tramite l’API HTTP tramite operazioni CRUD (creazione, lettura, aggiornamento, eliminazione)
* **[API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)** : per informazioni dettagliate su come distribuire frammenti di contenuto senza problemi
