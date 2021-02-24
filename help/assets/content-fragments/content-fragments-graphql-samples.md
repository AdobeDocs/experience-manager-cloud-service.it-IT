---
title: Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query
description: Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query.
translation-type: tm+mt
source-git-commit: 6a60238b13d66ea2705063670295a62e3cbf6255
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 5%

---


# Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

>[!NOTE]
>
>Questa pagina deve essere letta insieme a:
>
>* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
>* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM GraphQL API per l&#39;utilizzo con frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)


Per iniziare a utilizzare le query GraphQL e come funzionano con AEM frammenti di contenuto, è possibile vedere alcuni esempi pratici.

Per assistenza, consulta:

* A [struttura frammento di contenuto di esempio](#content-fragment-structure-graphql)

* Alcune query [GraphQL di esempio](#graphql-sample-queries) basate sulla struttura del frammento di contenuto di esempio (Modelli di frammenti di contenuto e frammenti di contenuto correlati).

## GraphQL per AEM - Riepilogo delle estensioni {#graphql-extensions}

Il funzionamento di base delle query con GraphQL per AEM aderire alla specifica GraphQL standard. Per le query GraphQL con AEM esistono alcune estensioni:

* Se si richiede un singolo risultato:
   * utilizzare il nome del modello; città esempio

* Se si prevede un elenco di risultati:
   * aggiungere `List` al nome del modello; ad esempio, `cityList`
   * Vedere [Esempio di query - Tutte le informazioni su tutte le città](#sample-all-information-all-cities)

* Se si desidera utilizzare un OR logico:
   * use ` _logOp: OR`
   * Vedere [Esempio di query - Tutte le persone con un nome &quot;Job&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Esiste anche un AND logico, ma è (spesso) implicito

* È possibile eseguire query sui nomi dei campi corrispondenti ai campi all&#39;interno del modello di frammento di contenuto
   * Vedere [Esempio di query - Dettagli completi sull&#39;amministratore delegato e sui dipendenti di una società](#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono disponibili alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale` : rivelare la lingua; basato su Language Manager
         * Vedere [Query di esempio per più frammenti di contenuto di una determinata lingua](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : visualizzazione dei metadati per il frammento
         * Consultate [Esempio di query per metadati - Elenco dei metadati per i premi denominati GB](#sample-metadata-awards-gb)
      * `_model` : consenti query per un modello di frammento di contenuto (percorso e titolo)
         * Vedere [Query di esempio per un modello di frammento di contenuto da un modello](#sample-wknd-content-fragment-model-from-model)
      * `_path` : percorso del frammento di contenuto all&#39;interno dell&#39;archivio
         * Vedere [Esempio di query - Un singolo frammento città specifico](#sample-single-specific-city-fragment)
      * `_reference` : rivelare i riferimenti; inclusione di riferimenti in linea nell’Editor di testo RTF
         * Vedere [Query di esempio per più frammenti di contenuto con riferimenti preimpostati](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : per visualizzare specifiche varianti all’interno del frammento di contenuto
         * Vedere [Esempio di query - Tutte le città con una variante denominata](#sample-cities-named-variation)
   * E operazioni:

      * `_operator` : applicare operatori specifici;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`
         * Vedere [Esempio di query - Tutte le persone che non hanno un nome di &quot;Processi&quot;](#sample-all-persons-not-jobs)
      * `_apply` : applicare condizioni specifiche; ad esempio,   `AT_LEAST_ONCE`
         * Vedere [Query di esempio - Filtro su un array con un elemento che deve verificarsi almeno una volta](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : per ignorare il caso durante la query
         * Vedere [Esempio di query - Tutte le città con SAN nel nome, indipendentemente da case](#sample-all-cities-san-ignore-case)









* I tipi di unione GraphQL sono supportati:

   * utilizza `... on`
      * Vedere [Query di esempio per un frammento di contenuto di un modello specifico con riferimento a contenuto](#sample-wknd-fragment-specific-model-content-reference)

## GraphQL - Query di esempio con struttura frammento di contenuto di esempio {#graphql-sample-queries-sample-content-fragment-structure}

Per informazioni su come creare query e per ottenere risultati di esempio, consultate queste query di esempio.

>[!NOTE]
>
>A seconda dell&#39;istanza in uso è possibile accedere direttamente all&#39;interfaccia [Graph *i* QL inclusa con AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) per l&#39;invio e il test delle query.
>
>Esempio: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>Le query di esempio si basano sulla [struttura del frammento di contenuto di esempio da utilizzare con GraphQL](#content-fragment-structure-graphql)

### Query di esempio - Tutti gli schemi e i tipi di dati disponibili {#sample-all-schemes-datatypes}

Verrà restituito tutto `types` per tutti gli schemi disponibili.

**Query di esempio**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Risultato campione**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le informazioni su tutte le città {#sample-all-information-all-cities}

Per recuperare tutte le informazioni su tutte le città, è possibile utilizzare la query di base:
**Query di esempio**

```xml
{
  cityList {
    items
  }
}
```

Una volta eseguita, il sistema espanderà automaticamente la query per includere tutti i campi:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Query di esempio - Nomi di tutte le città {#sample-names-all-cities}

Si tratta di una semplice query per restituire la `name`di tutte le voci nello schema `city`schema.

**Query di esempio**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Query di esempio - Un singolo frammento di città specifico {#sample-single-specific-city-fragment}

Si tratta di una query per restituire i dettagli di una singola voce di frammento in una posizione specifica nell&#39;archivio.

**Query di esempio**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Query di esempio - Tutte le città con una variante denominata {#sample-cities-named-variation}

Se si crea una nuova variante, denominata &quot;Berlin Center&quot; (`berlin_centre`), per `city` Berlino, è possibile utilizzare una query per restituire i dettagli della variante.

**Query di esempio**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Dettagli completi sull&#39;amministratore delegato e sui dipendenti di una società {#sample-full-details-company-ceos-employees}

Utilizzando la struttura dei frammenti nidificati, questa query restituisce i dettagli completi dell&#39;amministratore delegato di una società e di tutti i relativi dipendenti.

**Query di esempio**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le persone con un nome &quot;Processi&quot; o &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Questo filtrerà tutti i `persons` per tutti quelli che hanno il nome `Jobs`o `Smith`.

**Query di esempio**

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

**Risultati di esempio**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le persone che non hanno un nome &quot;Processi&quot; {#sample-all-persons-not-jobs}

Questo filtrerà tutti i `persons` per tutti quelli che hanno il nome `Jobs`o `Smith`.

**Query di esempio**

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

**Risultati di esempio**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le città situate in Germania o Svizzera con una popolazione compresa tra 400000 e 999999 {#sample-all-cities-d-ch-population}

Qui viene filtrata una combinazione di campi. Per selezionare l&#39;intervallo `AND` (implicito) viene utilizzato un `population`, mentre viene utilizzato un `OR` (esplicito) per selezionare le città richieste.

**Query di esempio**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le città con SAN nel nome, indipendentemente dal caso {#sample-all-cities-san-ignore-case}

Questa query interroga tutte le città che hanno `SAN` nel nome, indipendentemente dal caso.

**Query di esempio**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Query di esempio - Filtro su una matrice con un elemento che deve verificarsi almeno una volta {#sample-array-item-occur-at-least-once}

Questa query filtra su una matrice con un elemento (`city:na`) che deve verificarsi almeno una volta.

**Query di esempio**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Filtro su un valore di matrice esatto {#sample-array-exact-value}

Questa query filtra un valore di matrice esatto.

**Query di esempio**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio per i frammenti di contenuto nidificato - Tutte le società con almeno un dipendente con il nome &quot;Smith&quot; {#sample-companies-employee-smith}

Questa query illustra il filtraggio per qualsiasi `person` di `name` &quot;Smith&quot;, restituendo informazioni da due frammenti nidificati: `company` e `employee`.

**Query di esempio**

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

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Query di esempio per i frammenti di contenuto nidificato - Tutte le società in cui tutti i dipendenti hanno vinto il premio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Questa query illustra il filtraggio tra tre frammenti nidificati: `company`, `employee` e `award`.

**Query di esempio**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
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
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Query di esempio per metadati - Elenca i metadati per i premi denominati GB {#sample-metadata-awards-gb}

Questa query illustra il filtraggio tra tre frammenti nidificati: `company`, `employee` e `award`.

**Query di esempio**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Query di esempio con il progetto WKND {#sample-queries-using-wknd-project}

Queste query di esempio si basano sul progetto WKND. Sono disponibili:

* Modelli di frammenti di contenuto disponibili in:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Frammenti di contenuto (e altro contenuto) disponibili in:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Poiché i risultati possono essere estesi, non sono riportati qui.

### Query di esempio per tutti i frammenti di contenuto di un determinato modello con le proprietà specificate {#sample-wknd-all-model-properties}

Questa query di esempio interroga:

* per tutti i frammenti di contenuto di tipo `article`
* con le proprietà `path`e `author`.

**Query di esempio**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Query di esempio per metadati {#sample-wknd-metadata}

Questa query interroga:

* per tutti i frammenti di contenuto di tipo `adventure`
* Metadati

**Query di esempio**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Query di esempio per un singolo frammento di contenuto di un dato modello {#sample-wknd-single-content-fragment-of-given-model}

Questa query di esempio interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno di tali formati, tutti i formati di contenuto:
      * HTML
      * Markdown
      * Testo normale
      * JSON

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Query di esempio per un modello di frammento di contenuto da un modello {#sample-wknd-content-fragment-model-from-model}

Questa query di esempio interroga:

* per un singolo frammento di contenuto
   * dettagli del modello di frammento di contenuto sottostante

**Query di esempio**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Query di esempio per un frammento di contenuto nidificato - Tipo di modello singolo{#sample-wknd-nested-fragment-single-model}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno di esso, il percorso e l&#39;autore del frammento a cui viene fatto riferimento (nidificato)

>[!NOTE]
>
>Il campo `referencearticle` ha il tipo di dati `fragment-reference`.

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Query di esempio per un frammento di contenuto nidificato - Tipo di modello multiplo{#sample-wknd-nested-fragment-multiple-model}

Questa query interroga:

* per più frammenti di contenuto di tipo `bookmark`
   * con i riferimenti ai frammenti ad altri frammenti dei tipi di modelli specifici `article` e `adventure`

>[!NOTE]
>
>Il campo `fragments` ha il tipo di dati `fragment-reference`, con i modelli `Article`, `Adventure` selezionati.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Query di esempio per un frammento di contenuto di un modello specifico con riferimenti di contenuto{#sample-wknd-fragment-specific-model-content-reference}

Questa query offre due aspetti:

1. Per restituire tutti i riferimenti di contenuto.
1. Per restituire i riferimenti di contenuto specifici di tipo `attachments`.

Queste domande interrogano:

* per più frammenti di contenuto di tipo `bookmark`
   * con riferimenti di contenuto ad altri frammenti

#### Query di esempio per più frammenti di contenuto con riferimenti preacquisiti {#sample-wknd-multiple-fragments-prefetched-references}

La seguente query restituisce tutti i riferimenti di contenuto utilizzando `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Query di esempio per più frammenti di contenuto con allegati {#sample-wknd-multiple-fragments-attachments}

La seguente query restituisce tutti i campi `attachments` - uno specifico campo (sottogruppo) di tipo `content-reference`:

>[!NOTE]
>
>Il campo `attachments` ha il tipo di dati `content-reference`, con diversi moduli selezionati.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Query di esempio per un singolo frammento di contenuto con riferimento in linea RTE {#sample-wknd-single-fragment-rte-inline-reference}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `bookmark` in un percorso specifico
   * all&#39;interno di tali riferimenti, RTE in linea

>[!NOTE]
>
>I riferimenti in linea dell&#39;editor Rich Text sono idratati in `_references`.

**Query di esempio**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Query di esempio per una singola variante di frammento di contenuto di un dato modello {#sample-wknd-single-fragment-given-model}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno di tale, i dati relativi alla variazione: `variation1`

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query di esempio per una variante denominata di più frammenti di contenuto di un dato modello {#sample-wknd-variation-multiple-fragment-given-model}

Questa query interroga:

* per i frammenti di contenuto di tipo `article` con una variazione specifica: `variation1`

**Query di esempio**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query di esempio per più frammenti di contenuto di una determinata lingua {#sample-wknd-multiple-fragments-given-locale}

Questa query interroga:

* per i frammenti di contenuto di tipo `article` nelle `fr` impostazioni internazionali

**Query di esempio**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## Struttura del frammento di contenuto di esempio (utilizzata con GraphQL) {#content-fragment-structure-graphql}

Le query di esempio si basano sulla struttura seguente, che utilizza:

* Uno o più [modelli di frammenti di contenuto di esempio](#sample-content-fragment-models-schemas) - costituiscono la base per gli schemi GraphQL

* [Esempio di ](#sample-content-fragments) frammenti di contenuto basati sui modelli precedenti

### Modelli di frammenti di contenuto di esempio (schemi) {#sample-content-fragment-models-schemas}

Per le query di esempio, verranno utilizzati i seguenti modelli di contenuto e le relative interrelazioni (riferimenti ->):

* [Company](#model-company)
->  [Person](#model-person)
    ->  [Award](#model-award)

* [Città](#model-city)

#### Azienda {#model-company}

I campi di base che definiscono la società sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome società | Testo su riga singola |  |
| Direttore Generale | Riferimento frammento (singolo) | [Person](#model-person) |
| Dipendenti | Riferimento frammento (campo multiplo) | [Person](#model-person) |

#### Person {#model-person}

Campi che definiscono una persona, che può anche essere un dipendente:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome | Testo su riga singola |  |
| Nome | Testo su riga singola |  |
| Awards | Riferimento frammento (campo multiplo) | [Award](#model-award) |

#### Premio {#model-award}

I campi che definiscono un premio sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Collegamento/ID | Testo su riga singola |  |
| Titolo | Testo su riga singola |  |

#### Città {#model-city}

I campi per la definizione di una città sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome | Testo su riga singola |  |
| Paese | Testo su riga singola |  |
| Popolazione | Numero |  |
| Categorie | Tag |  |

### Frammenti di contenuto di esempio {#sample-content-fragments}

Per il modello appropriato vengono utilizzati i seguenti frammenti.

#### Azienda {#fragment-company}

| Nome società | Direttore Generale | Dipendenti |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Sfera di taglio |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nome | Nome | Awards |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Slade |  Cutter |  Gameblitz<br>Gamestar |
| Palude |  Duke |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Processi |  Steve |   |

#### Premio {#fragment-award}

| Collegamento/ID | Titolo |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Città {#fragment-city}

| Nome | Paese | Popolazione | Categorie |
|--- |--- |--- |--- |
| Basilea | Svizzera | 172258 | città:emea |
| Berlino | Germania | 3669491 | città:capitale<br>città:emea |
| Bucarest | Romania | 1821000 |  città:capitale<br>città:emea |
| San Francisco |  USA |  883306 |  città:spiaggia<br>città:na |
| San Jose |  USA |  102635 |  città:na |
| Stoccarda |  Germania |  634830 |  città:emea |
|  Zurigo |  Svizzera |  415367 |  città:capitale<br>città:emea |
