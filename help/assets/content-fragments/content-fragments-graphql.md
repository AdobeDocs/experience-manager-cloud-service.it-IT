---
title: Distribuzione di contenuti headless con frammenti di contenuto con GraphQL
description: Scoprite come utilizzare i frammenti di contenuto in Adobe Experience Manager (AEM) come Cloud Service con GraphQL per la distribuzione di contenuti headless.
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Distribuzione di contenuti headless con frammenti di contenuto con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

>[!CAUTION]
>
>L&#39;API AEM GraphQL, per la distribuzione dei frammenti di contenuto, verrà rilasciata all&#39;inizio del 2021.
>
>La documentazione correlata è già disponibile a scopo di anteprima.

Con Adobe Experience Manager (AEM) come Cloud Service, potete utilizzare i frammenti di contenuto, insieme all&#39;API AEM GraphQL (un&#39;implementazione personalizzata, basata su GraphQL standard), per distribuire contenuti strutturati da utilizzare nelle applicazioni.

## CMS senza testa {#headless-cms}

Un sistema CMS (headless Content Management System) è:

* &quot;*Un sistema di gestione dei contenuti headless, o CMS headless, è un sistema di gestione dei contenuti (CMS) di tipo back-end basato su un archivio di contenuti che rende accessibile il contenuto tramite un&#39;API per la visualizzazione su qualsiasi dispositivo.*

   *Il termine &quot;senza testa&quot; deriva dal concetto di tagliare la &quot;testa&quot; (il front-end, cioè il sito web) del &quot;corpo&quot; (il back-end, cioè il repository dei contenuti).*&quot;

   Vedere [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

In termini di creazione di frammenti di contenuto in AEM ciò significa che:

* È possibile utilizzare i frammenti di contenuto per creare contenuto che non deve essere pubblicato direttamente (1:1) nelle pagine formattate.

* Il contenuto dei frammenti di contenuto sarà strutturato in modo predeterminato, in base ai modelli di frammenti di contenuto. Questo semplifica l&#39;accesso alle applicazioni e consente di elaborare ulteriormente i contenuti.

>[!NOTE]
>
>Per un&#39;introduzione a Headless Development per  AEM Sites come Cloud Service, vedere [Headless and AEM](/help/implementing/developing/headless/introduction.md).

## GraphQL - Panoramica {#graphql-overview}

GraphQL è:

* &quot;*...un linguaggio di query per le API e un runtime per l&#39;esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell&#39;API, dà ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, rende più semplice l&#39;evoluzione delle API nel tempo e abilita potenti strumenti di sviluppo.*&quot;.

   Vedere [GraphQL.org](https://graphql.org)

* &quot;*...una specifica aperta per un livello API flessibile. Inserisci GraphQL sui tuoi backend esistenti per creare prodotti più rapidamente che mai....*&quot;.

   Vedere [Esplora GraphQL](https://www.graphql.com). &quot;*Esplora GraphQL è gestito dal team Apollo. Il nostro obiettivo è quello di fornire agli sviluppatori e ai leader tecnici di tutto il mondo tutti gli strumenti necessari per comprendere e adottare GraphQL.*&quot;.

L&#39; [AEM GraphQL API](#aem-graphql-api) consente di eseguire query (complesse) sui [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md); con ogni query in base a un tipo di modello specifico. Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

### Terminologia GraphQL {#graphql-terminology}

GraphQL utilizza quanto segue:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemi e tipi](https://graphql.org/learn/schema/)** : utilizzando questi, GraphQL presenta i tipi e le operazioni consentiti per GraphQL per AEM implementazione.

* **[Campi](https://graphql.org/learn/queries/#fields)**

* **Endpoint**  GraphQL - il percorso in AEM che risponde alle query GraphQL e fornisce l&#39;accesso agli schemi GraphQL.

Per informazioni dettagliate, comprese le [Best Practices](https://graphql.org/learn/best-practices/), consultate [(GraphQL.org) Introduction to GraphQL](https://graphql.org/learn/) (Introduzione a GraphQL.org).

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per:

* **Voce singola**

* **[Elenco delle voci](https://graphql.org/learn/schema/#lists-and-non-null)**

## AEM GraphQL API {#aem-graphql-api}

Per [Adobe Experience as a Cloud Experience, è stata implementata un&#39;implementazione personalizzata dell&#39;API GraphQL standard](/help/assets/content-fragments/graphql-api-content-fragments.md).

L&#39;implementazione dell&#39;API AEM GraphQL si basa sulle [librerie Java GraphQL](https://graphql.org/code/#java).

## Frammenti di contenuto da utilizzare con l&#39;API AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

[I ](#content-fragments) frammenti di contenuto possono essere utilizzati come base per GraphQL per AEM query come:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* I [modelli di frammento di contenuto](#content-fragments-models) forniscono la struttura richiesta tramite tipi di dati definiti.
* Per definire livelli aggiuntivi di struttura è possibile utilizzare la [Riferimento frammento](#fragment-references), disponibile per la definizione di un modello.

![Frammenti di contenuto da utilizzare con ](assets/cfm-nested-01.png "GraphQLCombramenti di contenuto per l&#39;utilizzo con GraphQL")

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contengono contenuto strutturato.

* Si basano su un [modello di frammento di contenuto](#content-fragments-models) che preimposta la struttura per il frammento risultante.

### Modelli per frammenti di contenuto {#content-fragments-models}

Questi [Modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md):

* Specifica i tipi di dati e i campi richiesti per GraphQL. Garantiscono che l&#39;applicazione richieda solo quanto è possibile e riceva ciò che è previsto.

* Il tipo di dati **[Riferimenti frammento](#fragment-references)** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre livelli aggiuntivi di struttura.

### Riferimenti frammento {#fragment-references}

Il **[riferimento al frammento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato per definire un modello di frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di uno specifico modello di frammento di contenuto.

* Consente di recuperare dati strutturati.

   * Se definito come **multifeed**, è possibile fare riferimento a più sottoframmenti (recuperati) dal frammento principale.

### Anteprima JSON {#json-preview}

Per facilitare la progettazione e lo sviluppo dei modelli di frammento di contenuto, potete visualizzare in anteprima l&#39;output [JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Per un&#39;introduzione all&#39;utilizzo dell&#39;API AEM GraphQL, vedere [Learning to use GraphQL with AEM - Sample Content and Queries](/help/assets/content-fragments/content-fragments-graphql-samples.md).

## Esercitazione - Guida introduttiva a AEM headless e GraphQL

Stai cercando un&#39;esercitazione pratica? Scoprite la [Guida introduttiva AEM headless e l&#39;esercitazione end-to-end di GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) che illustra come creare ed esporre contenuti utilizzando le API GraphQL di AEM e utilizzati da un&#39;app esterna, in uno scenario CMS headless.