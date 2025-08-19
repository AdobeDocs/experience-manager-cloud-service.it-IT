---
title: Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL (Assets - Frammenti di contenuto)
description: Scopri i concetti di base per la realizzazione di un CMS headless AEM utilizzando frammenti di contenuto con GraphQL per la distribuzione di contenuti headless.
feature: Content Fragments
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
role: User
solution: Experience Manager Sites
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 83%

---

# Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con i frammenti di contenuto e l’API GraphQL puoi utilizzare Adobe Experience Manager (AEM) as a Cloud Service come sistema CMS per la gestione dei contenuti headless.

Vengono utilizzati Frammenti di contenuto AEM insieme all’API GraphQL di AEM (un’implementazione personalizzata, basata sul linguaggio GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni. La possibilità di personalizzare una singola query API consente di recuperare e fornire il contenuto specifico che desideri riprodurre (come risposta alla singola query API).

>[!NOTE]
>
>Consulta anche:
>
>* [Cosa si intende con Headless?](/help/headless/what-is-headless.md) per un’introduzione ai concetti e alla terminologia headless.
>
>* [Headless e AEM](/help/headless/introduction.md) per un’introduzione allo sviluppo headless per AEM Sites as a Cloud Service.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce sfrutta i dati da una piattaforma commerce tramite GraphQL.](/help/commerce-cloud/cif-storefront/integrating/magento.md)
>* [I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/headless/graphql-api/content-fragments.md).

## CMS headless {#headless-cms}

“Un sistema per la gestione dei contenuti headless è un sistema di gestione dei contenuti (CMS) solo back-end progettato e creato esplicitamente come archivio di contenuti che li rende accessibili tramite un’API per la visualizzazione su qualsiasi dispositivo“.

In termini di authoring di frammenti di contenuto in AEM, questo significa che:

* È possibile utilizzare i frammenti di contenuto per creare contenuti che non sono destinati principalmente alla pubblicazione diretta (1:1) su pagine formattate.

* Il contenuto dei frammenti di contenuto è strutturato in modo predeterminato, in base ai modelli per frammenti di contenuto. Questo ne semplifica l’accesso da parte delle applicazioni che poi elaboreranno ulteriormente i contenuti.

## GraphQL: panoramica {#graphql-overview}

GraphQL è:

* “*...un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti.*”

  Vedi [GraphQL.org](https://graphql.org)

L&#39;[API GraphQL di AEM](#aem-graphql-api) consente di eseguire query (complesse) sui [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md); ogni query è basata su un tipo di modello specifico. Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

## API GraphQL di AEM {#aem-graphql-api}

Per Adobe Experience as a Cloud Experience è stata sviluppata un’implementazione personalizzata dell’API GraphQL standard. Per informazioni, consulta [API GraphQL AEM per l’utilizzo con Frammenti di contenuto](/help/headless/graphql-api/content-fragments.md).

L’implementazione dell’API GraphQL per AEM si basa sulle [librerie Java GraphQL](https://graphql.org/code/#java).

## Frammenti di contenuto da utilizzare con l’API GraphQL di AEM {#content-fragments-use-with-aem-graphql-api}

I [frammenti di contenuto](#content-fragments) possono essere utilizzati come base per GraphQL per query AEM per i seguenti motivi:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* I [Modelli per frammenti di contenuto](#content-fragments-models) forniscono la struttura richiesta per mezzo di tipi di dati definiti.
* Il [Riferimento frammento](#fragment-references), disponibile quando si definisce un modello, può essere utilizzato per definire livelli di struttura aggiuntivi.

![Frammenti di contenuto da utilizzare con GraphQL](assets/cfm-nested-01.png "Frammenti di contenuto da utilizzare con GraphQL")

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contengono contenuti strutturati.

* Sono basati su un [Modello per frammenti di contenuto](#content-fragments-models) che predefinisce la struttura del frammento risultante.

### Modelli per frammenti di contenuto {#content-fragments-models}

I [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md):

* Sono utilizzati per generare gli [Schemi](https://graphql.org/learn/schema/), una volta **Abilitati**.

* Forniscono i tipi di dati e i campi richiesti per GraphQL. Assicurano che l’applicazione trasmetta solo richieste ammesse e riceva solo i contenuti previsti.

* Il tipo di dati **[Riferimenti frammento](#fragment-references)** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre ulteriori livelli di struttura.

### Riferimenti frammento {#fragment-references}

Il **[Riferimento frammento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato durante la definizione di un modello per frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di un modello per frammento di contenuto specifico.

* Consente di recuperare i dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a (recuperare) più frammenti secondari dal frammento principale.

### Anteprima JSON {#json-preview}

Per semplificare la progettazione e lo sviluppo dei modelli per frammenti di contenuto, puoi visualizzare in anteprima l’[output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Per un’introduzione all’utilizzo dell’API GraphQL di AEM, consulta [Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query](/help/headless/graphql-api/sample-queries.md).

## Tutorial: guida introduttiva ad AEM headless e GraphQL

Cerchi un pratico tutorial? Dai un’occhiata al tutorial [Guida introduttiva di AEM headless e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it), che illustra come creare ed esporre contenuti, utilizzati da un’app esterna, mediante le API GraphQL di AEM in uno scenario CMS headless.
