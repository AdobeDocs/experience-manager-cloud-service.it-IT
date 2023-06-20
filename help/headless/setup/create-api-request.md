---
title: Creare una richiesta API - Configurazione headless
description: Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e API REST di Assets di AEM per gestire i frammenti di contenuto.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 98%

---

# Creare una richiesta API - Configurazione headless {#accessing-delivering-content-fragments}

Scopri come utilizzare l’API GraphQL per la distribuzione headless di contenuti con frammenti di contenuto e API REST di Assets di AEM per gestire i frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto,](create-content-fragment.md) puoi utilizzare le API AEM per distribuirle senza problemi.

* [API GraphQL](/help/headless/graphql-api/content-fragments.md) consente di creare richieste per accedere e distribuire frammenti di contenuto. Questa API offre la serie più solida di funzionalità per eseguire query e utilizzare contenuti di frammenti di contenuto.
   * Per utilizzare questo [gli endpoint devono essere definiti e abilitati in AEM](/help/headless/graphql-api/graphql-endpoint.md) e, se necessario, l’[Interfaccia GraphiQL deve essere installata](/help/headless/graphql-api/graphiql-ide.md).
* [API REST di Assets](/help/assets/content-fragments/assets-api-content-fragments.md) consente di creare e modificare frammenti di contenuto (e altre risorse).

Il resto di questa guida sarà incentrato sull’accesso a GraphQL e la distribuzione di frammenti di contenuto.

## Abilitare endpoint GraphQL {#enable-graphql-endpoint}

Prima di poter utilizzare le API GraphQL, è necessario creare un endpoint GraphQL.

1. Passa a **Strumenti**, **Generale**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Si aprirà la finestra di dialogo **Crea nuovo endpoint GraphQL**. Qui potrai definire:
   * **Nome**: nome dell’endpoint; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza il menu a discesa per selezionare la configurazione richiesta.
1. Conferma con **Crea**.
1. Nella console verrà ora visualizzato un **Percorso** in base alla configurazione creata in precedenza. Questo è il percorso utilizzato per eseguire le query GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Ulteriori dettagli sull’abilitazione degli [endpoint GraphQL si trovano qui](/help/headless/graphql-api/graphql-endpoint.md).

## Query del contenuto tramite GraphQL con GraphiQL

Gli architetti dell’informazione devono progettare query per gli endpoint di canale per distribuire i contenuti. In genere queste query devono essere considerate solo una volta per endpoint per modello. Ai fini di questa guida introduttiva, è sufficiente crearne una.

GraphiQL è un IDE, incluso nel tuo ambiente AEM e accessibile/visibile dopo aver [configurato gli endpoint](#enable-graphql-endpoint).

1. Accedi AEM as a Cloud Service e accedi all’interfaccia GraphiQL:

   Puoi accedere all’editor delle query da:

   * **Strumenti** -> **Generale** -> **Editor query GraphQL**
   * direttamente; ad esempio, `http://localhost:4502/aem/graphiql.html`

1. L’IDE GraphiQL è un editor di query interno al browser per GraphQL. Puoi utilizzarlo per creare query per recuperare frammenti di contenuto da distribuire in modalità headless come JSON.
   * L’elenco a discesa in alto a destra consente di selezionare l’endpoint.
   * L’ultimo pannello a sinistra elenca le query persistenti (se disponibili)
   * Il pannello nella parte centrale sinistra ti consente di creare la query.
   * Nel pannello centrale di destra vengono visualizzati i risultati.
   * L’editor delle query dispone del completamento del codice e dei tasti di scelta rapida per eseguire facilmente la query.

   ![Editor GraphiQL](../assets/graphiql.png)

1. Supponendo che il modello che abbiamo creato si chiama `person` con campi `firstName`, `lastName` e `position`, possiamo creare una semplice query per recuperare il contenuto del frammento di contenuto.

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

1. Fai clic sul pulsante **Esegui query** o utilizza il tasto di scelta rapida `Ctrl-Enter` e i risultati vengono visualizzati come JSON nel pannello di destra.
   ![Risultati GraphiQL](../assets/graphiql-results.png)

1. Fai clic sul collegamento **Documenti** in alto a destra della pagina per visualizzare la documentazione contestuale per aiutarti a creare le query che si adattano ai tuoi modelli.
   ![Documentazione di GraphiQL](../assets/graphiql-documentation.png)

GraphQL consente query strutturate in grado di eseguire il targeting non solo di set di dati specifici o di singoli oggetti di dati, ma anche di fornire elementi specifici degli oggetti, risultati nidificati, offerte di supporto per variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegna in eccesso, e consente invece la distribuzione in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

Tutto qui. Ora hai una conoscenza di base della gestione dei contenuti headless in AEM. Naturalmente, sono disponibili molte altre risorse da approfondire per una comprensione completa delle funzioni disponibili.

* **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md)**: per informazioni dettagliate sulla creazione e la gestione dei frammenti di contenuto
* **[Supporto per frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**: per informazioni dettagliate sull’accesso diretto ai contenuti AEM tramite l’API HTTP, mediante operazioni CRUD (Crea, Leggi, Aggiorna, Elimina)
* **[API di GraphQL](/help/headless/graphql-api/content-fragments.md)**: per informazioni dettagliate su come distribuire i frammenti di contenuto in modo corretto
