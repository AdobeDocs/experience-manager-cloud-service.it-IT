---
title: Come accedere al contenuto tramite API di consegna di AEM
description: In questa parte del Percorso per sviluppatori di AEM headless, scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.
exl-id: 1adecc69-5f92-4007-8a2a-65bf1e960645
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 100%

---

# Come accedere al contenuto tramite API di consegna di AEM {#access-your-content}

In questa parte del [Percorso per sviluppatori AEM headless](overview.md), puoi scoprire come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto e inviarlo all’app (consegna headless).

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come modellare il contenuto](model-your-content.md) hai appreso le nozioni di base sulla modellazione dei contenuti in AEM, quindi ora hai appreso come modellare la struttura dei contenuti, e realizzare tale struttura utilizzando i modelli per frammenti di contenuto e i frammenti di contenuto di AEM. Inoltre hai acquisito quanto segue:

* I concetti e la terminologia relativi alla modellazione dei contenuti.
* Perché è necessaria la modellazione dei contenuti per la distribuzione di contenuti headless.
* Come realizzare questa struttura utilizzando i Modelli per frammenti di contenuto di AEM (e creare contenuti con frammenti di contenuto).
* Come modellare i contenuti e ne conosci i principi con esempi di base.

Sulla base di questi elementi fondamentali, questo articolo parte spiega come accedere al contenuto headless esistente in AEM utilizzando l’API GraphQL di AEM.

* **Pubblico**: principiante
* **Obiettivo**: scopri come accedere al contenuto dei frammenti di contenuto utilizzando query GraphQL di AEM:
   * Introduzione a GraphQL e all’API GraphQL di AEM.
   * Approfondisci i dettagli dell’API GraphQL di AEM.
   * Osserva alcune query di esempio per vedere come funzionano in pratica.

## Desideri accedere ai tuoi contenuti? {#so-youd-like-to-access-your-content}

Allora... disponi di tutto questo contenuto, ben strutturato (in Frammenti di contenuto) e in attesa di alimentare la tua nuova app. La domanda è: come arrivarci?

Ciò di cui hai bisogno è un modo per eseguire il targeting di contenuti specifici, selezionare ciò che ti serve e restituirlo all’app per un’ulteriore elaborazione.

Con Adobe Experience Manager (AEM) as a Cloud Service, puoi accedere in modo selettivo ai frammenti di contenuto, utilizzando l’API GraphQL di AEM, per restituire solo il contenuto necessario. Ciò significa che è possibile realizzare una distribuzione headless di contenuti strutturati da utilizzare nelle applicazioni.

>[!NOTE]
>
>API GraphQL di AEM è un’implementazione personalizzata, basata sulle specifiche API GraphQL standard.

## GraphQL - Introduzione {#graphql-introduction}

GraphQL è una specifica open-source che fornisce:

* un linguaggio di query che consente di selezionare contenuto specifico da oggetti strutturati.
* un runtime per eseguire queste query con i contenuti strutturati.

GraphQL è un’API fortemente tipizzata. Ciò significa che *tutti* i contenuti devono essere chiaramente strutturati e organizzati per tipo, in modo che GraphQL *comprenda* accesso e modalità dello stesso. I campi dati sono definiti all’interno degli schemi GraphQL che definiscono la struttura degli oggetti contenuto.

Gli endpoint GraphQL forniscono quindi i percorsi che rispondono alle query GraphQL.

Ciò significa che l’app può selezionare in modo preciso, affidabile ed efficiente il contenuto necessario, esattamente ciò di cui hai bisogno quando viene utilizzata con AEM.

>[!NOTE]
>
>Vedi *GraphQL*.org e *GraphQL*.com.

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## API GraphQL di AEM {#aem-graphql-api}

L’API GraphQL di AEM è una versione personalizzata basata sulle specifiche API standard di GraphQL, appositamente configurata per consentire l’esecuzione di query (complesse) sui frammenti di contenuto.

I frammenti di contenuto vengono utilizzati, in quanto il contenuto è strutturato in base ai modelli di frammenti di contenuto. Questo soddisfa i requisiti fondamentali di GraphQL.

* Un modello di frammento di contenuto è costituito da uno o più campi.
   * Ogni campo è definito in base a un tipo di dati.
* I modelli per frammenti di contenuto vengono utilizzati per generare gli schemi GraphQL di AEM corrispondenti.

Per accedere effettivamente a GraphQL per AEM (e il contenuto) viene utilizzato un endpoint per fornire il percorso di accesso.

Il contenuto restituito, tramite l’API GraphQL di AEM, può quindi essere utilizzato dalle tue applicazioni.

Per facilitare l’input diretto e il test delle query, è disponibile anche un’implementazione dell’interfaccia standard GraphiQL da usare con GraphQL di AEM (installabile con AEM). Offre funzioni quali evidenziazione della sintassi, completamento automatico, suggerimenti automatici, nonché una cronologia e una documentazione online.

>[!NOTE]
>
>L’implementazione dell’API GraphQL per AEM si basa sulle librerie Java GraphQL.

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## Frammenti di contenuto da utilizzare con l’API GraphQL di AEM {#content-fragments-use-with-aem-graphql-api}

I frammenti di contenuto possono essere utilizzati come base per GraphQL per schemi e query AEM dato che:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina che possono essere distribuiti in modo headless.
* Si basano su un modello per frammenti di contenuto, che predefinisce la struttura del frammento risultante utilizzando una selezione di tipi di dati.
* È possibile ottenere livelli aggiuntivi di struttura con il tipo di dati Riferimento frammento, disponibile quando si definisce un modello.

### Modelli per frammenti di contenuto {#content-fragments-models}

Questi Modelli per frammenti di contenuto:

* Sono utilizzati per generare gli Schemi, una volta **Abilitati**.
* Forniscono i tipi di dati e i campi richiesti per GraphQL. Assicurano che l’applicazione trasmetta solo richieste ammesse e riceva solo i contenuti previsti.
* Il tipo di dati **Riferimenti frammento** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre ulteriori livelli di struttura.

### Riferimenti frammento {#fragment-references}

**Riferimento frammento** e **Riferimento frammento UUID**:

* Sono tipi di dati specifici disponibili quando si definisce un modello per frammenti di contenuto.
* Fa riferimento a un altro frammento, a seconda di un modello per frammenti di contenuto specifici.
* Consente di creare e quindi recuperare dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a (recuperare) più frammenti secondari dal frammento principale.

## Accessibili tramite l’API GraphQL di AEM {#actually-using-aem-graphiql}

### Configurazione iniziale {#initial-setup}

Prima di iniziare con le query sul contenuto è necessario:

* Abilitare l’endpoint 
   * Usa Strumenti -> Generale -> GraphQL
   * [Abilitazione dell’endpoint GraphQL](/help/headless/graphql-api/graphql-endpoint.md)
      * In questo modo sarà possibile abilitare anche IDE GraphiQL.

### Struttura di esempio {#sample-structure}

Per utilizzare effettivamente l’API GraphQL di AEM in una query, possiamo utilizzare le due strutture modello di frammento di contenuto molto semplici:

* Azienda
   * Nome - Testo
   * Amministratore delegato (Persona) - Riferimento al frammento
   * Dipendenti (Persone) - Riferimento/i al frammento
* Persona
   * Nome - Testo
   * Nome - Testo

Come puoi vedere, i campi Amministratore delegato e Dipendenti fanno riferimento ai frammenti persona.

I modelli di frammento vengono utilizzati:

* durante la creazione del contenuto nell’Editor frammento di contenuto
* per generare gli schemi GraphQL da interrogare

### Dove testare le query {#where-to-test-your-queries}

Le query possono essere immesse nell&#39;interfaccia GraphiQL. Puoi accedere all’editor di query da:

* **Strumenti** -> **Generale** -> **Editor di query GraphQL**
* direttamente; ad esempio `http://localhost:4502/aem/graphiql.html`

![Interfaccia di GraphiQL](assets/graphiql-interface.png "Interfaccia di GraphiQL")

### Guida introduttiva alle query {#getting-Started-with-queries}

Una query semplice consiste nel restituire il nome di tutte le voci nello schema Azienda. Qui si richiede un elenco di tutti i nomi aziendali:

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

Una query leggermente più complessa consiste nel selezionare tutte le persone che non hanno un nome di “Jobs”. In questo modo verranno filtrate tutte le persone per quelle che non hanno il nome Jobs. Questo si ottiene con l&#39;operatore EQUALS_NOT (ce ne sono molti altri):

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

È inoltre possibile creare query più complesse. Ad esempio, eseguire una query per tutte le aziende che hanno almeno un dipendente con il nome di “Smith”. Questa query illustra il filtro per qualsiasi persona di nome “Smith” e restituisce informazioni da frammenti nidificati:

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

Per informazioni dettagliate sull’utilizzo dell’API GraphQL di AEM e sulla configurazione degli elementi necessari, puoi fare riferimento a:

* Imparare a utilizzare GraphQL con AEM
* La struttura del frammento di contenuto di esempio
* Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query

## Passaggio successivo {#whats-next}

Ora che hai imparato ad accedere ai contenuti headless e ad eseguire query tramite l’API GraphQL di AEM puoi [imparare ad utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto](update-your-content.md).

## Risorse aggiuntive {#additional-resources}

* [API di Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [GraphQL.org](https://graphql.org)
   * [Schemi](https://graphql.org/learn/schema/)
   * [Variabili](https://graphql.org/learn/queries/#variables)
   * [Librerie Java GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Imparare a utilizzare GraphQL con AEM](/help/headless/graphql-api/content-fragments.md)
   * [Abilitazione dell’endpoint GraphQL](/help/headless/graphql-api/graphql-endpoint.md)
   * [Installazione dell’interfaccia di GraphiQL per AEM](/help/headless/graphql-api/graphiql-ide.md)
* [La struttura del frammento di contenuto di esempio](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query](/help/headless/graphql-api/sample-queries.md)
   * [Query di esempio: un singolo frammento di città specifico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
   * [Esempio di query per metadati: elenco dei metadati per i riconoscimenti denominati GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
   * [Query di esempio: tutte le città con una variante denominata](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)
* [Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)
* [Utilizzo di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md)
   * [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
   * [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprendere la condivisione CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=it#understand-cross-origin-resource-sharing-(cors))
* [Query persistenti GraphQL: abilitazione della memorizzazione in cache in Dispatcher](/help/headless/deployment/dispatcher-caching.md)
* [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Guida introduttiva ad AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) - Una breve serie di video tutorial che offre una panoramica dell’utilizzo di funzioni headless di AEM, tra cui modellazione dei contenuti e GraphQL.
