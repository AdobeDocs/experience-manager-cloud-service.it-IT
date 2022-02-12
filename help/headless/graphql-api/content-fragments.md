---
title: AEM API GraphQL per l’utilizzo con frammenti di contenuto
description: Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service con l’API GraphQL AEM per la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---


# AEM API GraphQL per l’utilizzo con frammenti di contenuto {#graphql-api-for-use-with-content-fragments}

Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service con l’API GraphQL AEM per la distribuzione di contenuti headless.

AEM’API GraphQL as a Cloud Service utilizzata con i frammenti di contenuto è fortemente basata sull’API GraphQL standard open source.

L’utilizzo dell’API GraphQL in AEM consente la distribuzione efficiente di frammenti di contenuto ai client JavaScript in implementazioni CMS headless:

* Evitare richieste API iterative come con REST,
* garantire che la consegna sia limitata ai requisiti specifici,
* Consentire la distribuzione in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce consuma dati da una piattaforma Commerce tramite GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Frammenti di contenuto collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni.


## API GraphQL {#graphql-api}

GraphQL è:

* &quot;*...un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell’API, offre ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, semplifica l’evoluzione delle API nel tempo e consente potenti strumenti per gli sviluppatori.*&quot;.

   Vedi [GraphQL.org](https://graphql.org)

* &quot;*...una specifica aperta per un livello API flessibile. Posiziona GraphQL sui backend esistenti per creare prodotti più rapidamente che mai....*&quot;.

   Vedi [Esplorare GraphQL](https://www.graphql.com).

* *&quot;..un linguaggio e una specifica di query di dati sviluppati internamente da Facebook nel 2012 prima di essere pubblicamente aperti dal 2015. Offre un’alternativa alle architetture basate su REST allo scopo di aumentare la produttività degli sviluppatori e ridurre al minimo le quantità di dati trasferiti. GraphQL viene utilizzato nella produzione da centinaia di organizzazioni di tutte le dimensioni...&quot;*

   Vedi [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Per ulteriori informazioni sull’API GraphQL, consulta le sezioni seguenti (tra cui molte altre risorse):

* A [graphql.org](https://graphql.org):

   * [Introduzione a GraphQL](https://graphql.org/learn)

   * [Specifica GraphQL](https://spec.graphql.org/)

* A [graphql.com](https://graphql.com):

   * [Guide](https://www.graphql.com/guides/)

   * [Esercitazioni](https://www.graphql.com/tutorials/)

   * [Case study](https://www.graphql.com/case-studies/)

GraphQL per AEM implementazione si basa sulla libreria Java GraphQL standard. Consulta:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [Java GraphQL su GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL utilizza quanto segue:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemi e tipi](https://graphql.org/learn/schema/)**:

   * Gli schemi vengono generati da AEM in base ai modelli di frammenti di contenuto.
   * Utilizzando i tuoi schemi, GraphQL presenta i tipi e le operazioni consentiti per l’implementazione AEM GraphQL.

* **[Campi](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](graphql-endpoint.md)**
   * Il percorso in AEM che risponde alle query GraphQL e fornisce accesso agli schemi GraphQL.

   * Vedi [Abilitazione dell’endpoint GraphQL](graphql-endpoint.md) per ulteriori dettagli.

Consulta la sezione [(GraphQL.org) Introduzione a GraphQL](https://graphql.org/learn/) per informazioni complete, tra cui [Best practice](https://graphql.org/learn/best-practices/).

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per restituire:

* A **ingresso singolo**

* A **[elenco delle voci](https://graphql.org/learn/schema/#lists-and-non-null)**

Puoi anche eseguire le seguenti operazioni:

* [Query persistenti memorizzate nella cache](/help/headless/graphql-api/persisted-queries.md)

### IDE GraphiQL {#graphiql-ide}

Puoi testare ed eseguire il debug delle query GraphQL utilizzando [IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

## Casi d’uso per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi di utilizzo possono dipendere dal tipo di ambiente as a Cloud Service AEM:

* ambiente di pubblicazione; utilizzato per:
   * Dati query per l’applicazione JS (caso d’uso standard)

* Ambiente di authoring; utilizzato per:
   * Dati query per &quot;scopo di gestione del contenuto&quot;:
      * GraphQL in AEM as a Cloud Service è attualmente un&#39;API di sola lettura.
      * L’API REST può essere utilizzata per le operazioni CR(u)D.

## Autorizzazioni {#permission}

Le autorizzazioni sono quelle necessarie per accedere ad Assets.

## Generazione schema {#schema-generation}

GraphQL è un’API fortemente tipizzata, il che significa che i dati devono essere chiaramente strutturati e organizzati per tipo.

La specifica GraphQL fornisce una serie di linee guida su come creare una solida API per l&#39;interrogazione dei dati su una determinata istanza. A questo scopo, un client deve recuperare il [Schema](#schema-generation), che contiene tutti i tipi necessari per una query.

Per i frammenti di contenuto, gli schemi GraphQL (struttura e tipi) sono basati su **Abilitato** [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di frammenti di contenuto che sono stati **Abilitato**) sono leggibili attraverso l’endpoint GraphQL .
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello di frammento di contenuto denominato `Article`, quindi AEM genera l’oggetto `article` di un tipo `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Un Modello Di Frammento Di Contenuto:

   ![Modello per frammenti di contenuto da utilizzare con GraphQL](assets/cfm-graphqlapi-01.png "Modello per frammenti di contenuto da utilizzare con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su modello di frammento di contenuto](assets/cfm-graphqlapi-02.png "Schema GraphQL basato su modello di frammento di contenuto")

   Mostra il tipo generato `ArticleModel` contiene diversi [field](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Tali [campi di supporto](#helper-fields) sono contrassegnate con un `_` per distinguere tra ciò che è stato definito dall’utente e ciò che è stato generato automaticamente.

1. Dopo che un utente crea un frammento di contenuto basato sul modello di articolo, può essere interrogato tramite GraphQL. Per esempi, consulta la sezione [Query di esempio](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (basato su un [struttura dei frammenti di contenuto di esempio da utilizzare con GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si aggiorna un modello di frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e di garantire stabilità.

Ad esempio, se:

1. Installa un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Tipi GraphQL per `Model-1` e `Model-2` verrà generato.

1. Quindi modificare `Content-Fragment-Model-2`:

   1. Solo il `Model-2` Il tipo GraphQL verrà aggiornato.

   1. considerando che `Model-1` rimarrà lo stesso.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di frammenti di contenuto tramite l’api REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, con il client che gestisce il fatto che lo schema viene chiamato con l&#39;estensione `GQLschema`. Ad esempio, l’esecuzione di un `GET` richiesta di `/content/cq:graphql/global/endpoint.GQLschema` si tradurrà nell&#39;output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

### Generazione schema - Modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che un modello di frammento di contenuto principale venga pubblicato, ma non lo è un modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera un *incompleto* Schema per il modello di frammento di contenuto principale. Ciò significa che il Riferimento frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## espandibili {#fields}

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati.

   Selezione di [Tipi di campi](#field-types) vengono utilizzati per creare campi in base alla modalità di configurazione del modello di frammento di contenuto. I nomi dei campi vengono ricavati dal **Nome proprietà** campo **Tipo di dati**.

   * C&#39;è anche la **Rendering come** proprietà da prendere in considerazione, in quanto gli utenti possono configurare determinati tipi di dati; ad esempio, come testo a riga singola o come campo multiplo.

* GraphQL per AEM genera anche una serie di [campi di supporto](#helper-fields).

   Vengono utilizzati per identificare un frammento di contenuto o per ottenere ulteriori informazioni su un frammento di contenuto.

### Tipi di campi {#field-types}

GraphQL per AEM supporta un elenco di tipi. Sono rappresentati tutti i tipi di dati dei modelli di frammento di contenuto supportati e i corrispondenti tipi GraphQL:

| Modello per frammento di contenuto - Tipo di dati | Tipo GraphQL | Descrizione |
|--- |--- |--- |
| Testo a riga singola | Stringa, [Stringa] |  Utilizzato per stringhe semplici come nomi di autore, nomi di posizione, ecc. |
| Testo a più righe | Stringa |  Utilizzato per l’output di testo, ad esempio il corpo di un articolo |
| Numero |  Mobile, [Mobile] | Utilizzato per visualizzare il numero a virgola mobile e i numeri regolari |
| Booleano |  Booleano |  Utilizzato per visualizzare le caselle di controllo → semplici istruzioni true/false |
| Data E Ora | Calendario |  Utilizzato per visualizzare data e ora in formato ISO 8086. A seconda del tipo selezionato, sono disponibili tre aromi da utilizzare in AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumerazione |  Stringa |  Utilizzato per visualizzare un&#39;opzione da un elenco di opzioni definite durante la creazione del modello |
|  Tag |  [Stringa] |  Utilizzato per visualizzare un elenco di stringhe che rappresentano tag utilizzati in AEM |
| Riferimento contenuto |  Stringa |  Utilizzato per visualizzare il percorso verso un’altra risorsa in AEM |
| Riferimento frammento |  *Un tipo di modello* |  Utilizzato per fare riferimento a un altro frammento di contenuto di un determinato tipo di modello, definito al momento della creazione del modello |

### Campi helper {#helper-fields}

Oltre ai tipi di dati per i campi generati dall’utente, GraphQL per AEM genera anche una serie di *aiutante* per facilitare l’identificazione di un frammento di contenuto o per fornire informazioni aggiuntive su un frammento di contenuto.

#### Percorso {#path}

Il campo percorso viene utilizzato come identificatore in GraphQL. Rappresenta il percorso della risorsa Frammento di contenuto all’interno dell’archivio AEM. Questo è l’identificatore di un frammento di contenuto, in quanto:

* è univoco all&#39;interno di AEM,
* può essere facilmente recuperato.

Il codice seguente visualizza i percorsi di tutti i frammenti di contenuto creati in base al modello di frammento di contenuto `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Per recuperare un singolo frammento di contenuto di un tipo specifico, è necessario anche determinarne prima il percorso. ad esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Vedi [Query Di Esempio - Un Singolo Frammento Di Città Specifico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadati {#metadata}

Tramite GraphQL, AEM espone anche i metadati di un frammento di contenuto. I metadati sono informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso delle miniature, la descrizione di un frammento di contenuto, la data di creazione, tra gli altri.

Poiché i metadati vengono generati tramite l’Editor di schema e in quanto tali non dispongono di una struttura specifica, il `TypedMetaData` Il tipo GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate per i seguenti tipi scalari:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Ogni tipo scalare rappresenta una coppia nome-valore singola o una matrice di coppie nome-valore, in cui il valore di tale coppia è del tipo in cui è stato raggruppato.

Ad esempio, se desideri recuperare il titolo di un frammento di contenuto, questa proprietà è una proprietà String , quindi eseguiamo una query per tutti i metadati stringa:

Per eseguire una query per i metadati:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Puoi visualizzare tutti i tipi di metadati GraphQL se visualizzi lo schema GraphQL generato. Tutti i tipi di modello hanno lo stesso `TypedMetaData`.

>[!NOTE]
>
>**Differenza tra i metadati normali e quelli dell&#39;array**
>Nota bene `StringMetadata` e `StringArrayMetadata` entrambi si riferiscono a ciò che è memorizzato nell’archivio, non a come lo si recupera.
>
>Ad esempio, chiamando il `stringMetadata` riceveresti un array di tutti i metadati memorizzati nel repository come `String` e se si chiama `stringArrayMetadata` riceveresti un array di tutti i metadati memorizzati nel repository come `String[]`.

Vedi [Esempio di query per metadati - Elenco dei metadati per i riconoscimenti denominati GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Varianti {#variations}

La `_variations` è stato implementato per semplificare la query delle varianti di un frammento di contenuto. Esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Vedi [Query di esempio - Tutte le città con una variante denominata](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variabili GraphQL {#graphql-variables}

GraphQL consente di inserire le variabili nella query. Per ulteriori informazioni, consulta la sezione [Documentazione GraphQL per le variabili](https://graphql.org/learn/queries/#variables).

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Article` che hanno una variante specifica, puoi specificare la variabile `variation` in GraphiQL.

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Direttive GraphQL {#graphql-directives}

In GraphQL è possibile modificare la query in base alle variabili, denominate Direttive GraphQL.

Ad esempio, in questo caso puoi includere il `adventurePrice` in una query per tutti gli `AdventureModels`, basato su una variabile `includePrice`.

![Direttive GraphQL](assets/cfm-graphqlapi-04.png "Direttive GraphQL")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtro {#filtering}

È inoltre possibile utilizzare il filtro nelle query GraphQL per restituire dati specifici.

Il filtro utilizza una sintassi basata su operatori logici ed espressioni.

Ad esempio, la seguente query (di base) filtra tutte le persone con un nome di `Jobs` o `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

Per ulteriori esempi, consulta:

* informazioni dettagliate [GraphQL per estensioni AEM](#graphql-extensions)

* [Query di esempio con contenuto e struttura di esempio](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * e [Contenuto e struttura di esempio](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) preparato per l’utilizzo in query di esempio

* [Query di esempio basate sul progetto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## GraphQL per AEM - Riepilogo delle estensioni {#graphql-extensions}

Il funzionamento di base delle query con GraphQL per AEM rispettare la specifica GraphQL standard. Per le query GraphQL con AEM sono disponibili alcune estensioni:

* Se hai bisogno di un singolo risultato:
   * utilizzare il nome del modello; città

* Se si prevede un elenco di risultati:
   * add `List` al nome del modello; ad esempio,  `cityList`
   * Vedi [Query di esempio - Tutte le informazioni su tutte le città](#sample-all-information-all-cities)

* Se desideri utilizzare un operatore OR logico:
   * use ` _logOp: OR`
   * Vedi [Query di esempio - Tutte le persone con un nome &quot;Jobs&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Esiste anche l&#39;AND logico, ma è (spesso) implicito

* È possibile eseguire query sui nomi di campo corrispondenti ai campi all’interno del modello di frammento di contenuto
   * Vedi [Query di esempio - Dettagli completi dell&#39;amministratore delegato e dei dipendenti di un&#39;azienda](#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono presenti alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale` : rivelare la lingua; basato su Language Manager
         * Vedi [Query di esempio per più frammenti di contenuto di una determinata impostazione internazionale](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : per visualizzare i metadati del frammento
         * Vedi [Esempio di query per metadati - Elenco dei metadati per i riconoscimenti denominati GB](#sample-metadata-awards-gb)
      * `_model` : consentire la query per un modello di frammento di contenuto (percorso e titolo)
         * Vedi [Query di esempio per un modello di frammento di contenuto da un modello](#sample-wknd-content-fragment-model-from-model)
      * `_path` : percorso del frammento di contenuto all’interno dell’archivio
         * Vedi [Query Di Esempio - Un Singolo Frammento Di Città Specifico](#sample-single-specific-city-fragment)
      * `_reference` : rivelare riferimenti; inclusione di riferimenti in linea nell’Editor Rich Text
         * Vedi [Query di esempio per più frammenti di contenuto con riferimenti prerecuperati](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : per visualizzare varianti specifiche all’interno del frammento di contenuto
         * Vedi [Query di esempio - Tutte le città con una variante denominata](#sample-cities-named-variation)
   * e operazioni:

      * `_operator` : applicare operatori specifici; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Vedi [Query di esempio - Tutte le persone che non hanno un nome &quot;Jobs&quot;](#sample-all-persons-not-jobs)
         * Vedi [Query di esempio - Tutte le avventure in cui `_path` inizia con un prefisso specifico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : applicare condizioni specifiche; ad esempio,  `AT_LEAST_ONCE`
         * Vedi [Query di esempio - Filtro su una matrice con un elemento che deve verificarsi almeno una volta](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : per ignorare il caso durante la query
         * Vedi [Query di esempio - Tutte le città con SAN nel nome, indipendentemente dal caso](#sample-all-cities-san-ignore-case)









* I tipi di unione GraphQL sono supportati:

   * use `... on`
      * Vedi [Query di esempio per un frammento di contenuto di un modello specifico con un riferimento al contenuto](#sample-wknd-fragment-specific-model-content-reference)

* Abbandono durante la query dei frammenti nidificati:

   * Se una determinata variante non esiste in un frammento nidificato, la variabile **Master** viene restituita una variante.

## Query dell’endpoint GraphQL da un sito Web esterno {#query-graphql-endpoint-from-external-website}

Per accedere all’endpoint GraphQL da un sito web esterno è necessario configurare i seguenti elementi:

* [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Filtro di riferimento](/help/headless/deployment/referrer-filter.md)

## Autenticazione {#authentication}

Vedi [Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/headless/security/authentication.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Domande frequenti {#faqs}

Domande sollevate:

1. **Q**: &quot;*In che modo l’API GraphQL per AEM è diversa dall’API di Query Builder?*&quot;

   * **A**: &quot;*L’API GraphQL di AEM offre il controllo totale sull’output JSON ed è uno standard di settore per l’esecuzione di query sui contenuti.
In futuro, AEM prevede di investire nell’API GraphQL AEM.*&quot;

## Tutorial: guida introduttiva a AEM Headless e GraphQL {#tutorial}

Stai cercando un tutorial pratico? Consulta [Guida introduttiva a AEM Headless e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) esercitazione end-to-end che illustra come creare ed esporre contenuti utilizzando le API GraphQL di AEM e utilizzati da un’app esterna, in uno scenario CMS headless.
