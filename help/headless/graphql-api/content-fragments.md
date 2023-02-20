---
title: API GraphQL AEM per l’utilizzo con Frammenti di contenuto
description: Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service con l’API GraphQL AEM per la consegna di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: e156ed7348815e02c942cb8feace70c675956752
workflow-type: tm+mt
source-wordcount: '4203'
ht-degree: 58%

---


# API GraphQL AEM per l’utilizzo con Frammenti di contenuto {#graphql-api-for-use-with-content-fragments}

Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service con l’API GraphQL AEM per la consegna di contenuti headless.

L’API GraphQL AEM as a Cloud Service utilizzata con i Frammenti di contenuto è pesantemente basata sull’API GraphQL standard open source.

L’utilizzo dell’API GraphQL in AEM consente la consegna efficiente di Frammenti di contenuto ai client JavaScript in implementazioni CMS headless:

* evita richieste API iterative come con REST,
* garantisce che la consegna sia limitata ai requisiti specifici,
* consente la consegna in massa di ciò che è esattamente necessario per il rendering come risposta a una singola query API.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce sfrutta i dati da una piattaforma Commerce tramite GraphQL](/help/commerce-cloud/integrating/magento.md).
>* I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni.


## API GraphQL {#graphql-api}

GraphQL è:

* “*...un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell’API, offre ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, semplifica l’evoluzione delle API nel tempo e abilita potenti strumenti per gli sviluppatori.*”.

   Vedi [GraphQL.org](https://graphql.org)

* “*...una specifica aperta per un livello API flessibile. Posiziona GraphQL sui backend esistenti per costruire prodotti più rapidamente che mai....*”.

   Vedi [Esplorare GraphQL](https://www.graphql.com).

* *“..un linguaggio e una specifica di query di dati sviluppati internamente da Facebook nel 2012 prima di essere resi open source nel 2015. Offre un’alternativa alle architetture basate su REST allo scopo di aumentare la produttività degli sviluppatori e ridurre al minimo le quantità di dati trasferiti. GraphQL viene utilizzato in produzione da centinaia di organizzazioni di tutte le dimensioni...”*

   Vedi [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Per ulteriori informazioni sull’API GraphQL, consulta le sezioni seguenti (tra molte altre risorse):

* In [graphql.org](https://graphql.org):

   * [Introduzione a GraphQL](https://graphql.org/learn)

   * [Specifiche GraphQL](https://spec.graphql.org/)

* In [graphql.com](https://graphql.com):

   * [Guide](https://www.graphql.com/guides/)

   * [Esercitazioni](https://www.graphql.com/tutorials/)

   * [Casi di studio](https://www.graphql.com/case-studies/)

L’implementazione di GraphQL per AEM si basa sulla libreria Java GraphQL standard. Consulta:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [Java GraphQL su GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL utilizza quanto segue:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemi e tipi](https://graphql.org/learn/schema/)**:

   * Gli schemi vengono generati da AEM in base ai modelli di Frammenti di contenuto.
   * Utilizzando i tuoi schemi, GraphQL presenta i tipi e le operazioni consentiti per l’implementazione GraphQL per AEM.

* **[Campi](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](graphql-endpoint.md)**
   * Il percorso in AEM che risponde alle query GraphQL e fornisce accesso agli schemi GraphQL.

   * Consulta [Abilitazione dell’endpoint GraphQL](graphql-endpoint.md) per ulteriori dettagli.

Consulta[(GraphQL.org) Introduzione a GraphQL](https://graphql.org/learn/) per informazioni complete, che comprendono le [Best practice](https://graphql.org/learn/best-practices/).

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per ottenere:

* Un **ingresso singolo**

* Un **[elenco delle voci](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM fornisce funzionalità per convertire le query (entrambi i tipi) in [Query persistenti, che possono essere memorizzate nella cache](/help/headless/graphql-api/persisted-queries.md) da Dispatcher e dalla rete CDN.

### Tecniche consigliate per le query GraphQL (Dispatcher e CDN) {#graphql-query-best-practices}

La [Query persistenti](/help/headless/graphql-api/persisted-queries.md) sono il metodo consigliato da utilizzare nelle istanze di pubblicazione come:

* vengono memorizzate nella cache;
* sono gestite centralmente da AEM as a Cloud Service.

>[!NOTE]
>
>Di solito non esiste un dispatcher/CDN sull’autore, quindi non c’è alcun guadagno nell’utilizzo di query persistenti lì; oltre a testarli.

Le query GraphQL che utilizzano richieste POST non sono consigliate in quanto non sono memorizzate nella cache, pertanto in un’istanza predefinita Dispatcher è configurato per bloccare tali query.

Anche se GraphQL supporta anche le richieste GET, possono raggiungere i limiti (ad esempio la lunghezza dell’URL) che possono essere evitati utilizzando le query persistenti.

>[!NOTE]
>
>Per consentire query dirette e/o POST in Dispatcher, puoi chiedere all’amministratore di sistema di:
>
>* Crea un [Variabile di ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) chiamato `ENABLE_GRAPHQL_ENDPOINT`
>* con il valore `true`


>[!NOTE]
>
>In futuro, la capacità di eseguire query dirette potrebbe diventare obsoleta.

### IDE GraphiQL {#graphiql-ide}

Puoi testare ed eseguire il debug delle query GraphQL utilizzando [IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

## Casi di utilizzo per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi di utilizzo possono dipendere dal tipo di ambiente AEM as a Cloud Service:

* ambiente di pubblicazione; utilizzato per:
   * effettuare query sui dati per l’applicazione JS (caso di utilizzo standard)

* ambiente di authoring; utilizzato per:
   * effettuare query sui dati a “scopo di gestione dei contenuti”:
      * GraphQL in AEM as a Cloud Service è attualmente un’API di sola lettura.
      * L’API REST può essere utilizzata per le operazioni CR(u)D.

## Autorizzazioni {#permission}

Le autorizzazioni sono quelle necessarie per accedere ad Assets.

Le query GraphQL vengono eseguite con l&#39;autorizzazione dell&#39;utente AEM della richiesta sottostante. Se l’utente non dispone dell’accesso in lettura ad alcuni frammenti (memorizzati come risorse), non farà parte del set di risultati.

Inoltre, l’utente deve avere accesso a un endpoint GraphQL per poter eseguire query GraphQL.

## Generazione schema {#schema-generation}

GraphQL è un’API fortemente tipizzata, il che significa che i dati devono essere chiaramente strutturati e organizzati per tipo.

La specifica GraphQL fornisce una serie di linee guida su come creare una solida API per l’interrogazione dei dati su una determinata istanza. A questo scopo, un client deve recuperare lo [Schema](#schema-generation), che contiene tutti i tipi necessari per una query.

Per quanto riguarda i Frammenti di contenuto, gli schemi GraphQL (struttura e tipi) sono basati su [modelli di Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) **abilitati** e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di Frammenti di contenuto che sono stati **abilitati**) sono leggibili attraverso l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, che in questo modo potrebbero trapelare; ad esempio, informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello di frammento di contenuto denominato `Article`, quindi AEM genera un tipo GraphQL `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello. Inoltre, crea alcuni punti di ingresso per le query che operano su questo tipo, come `articleByPath` o `articleList`.

1. Modello di Frammento di contenuto:

   ![Modello di Frammento di contenuto da utilizzare con GraphQL](assets/cfm-graphqlapi-01.png "Modello di Frammento di contenuto da utilizzare con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su modello di Frammento di contenuto](assets/cfm-graphqlapi-02.png "Schema GraphQL basato su modello di Frammento di contenuto")

   Questo mostra che il tipo `ArticleModel` generato contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato frammento di contenuto; in questo esempio, [campi di supporto](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. Un Frammento di contenuto basato sul modello di articolo creato da un utente può essere interrogato tramite GraphQL. Per esempi, consulta la sezione [Query di esempio](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (basata su una [struttura di Frammento di contenuto di esempio da utilizzare con GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di Frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si rivede un modello di Frammento di contenuto.

<!-- move the following to a separate "in depth" page -->

Le cache dello schema dati vengono aggiornate anche quando si rivede un modello di Frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di Frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e garantisce stabilità.

Ad esempio, se:

1. installi un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. vengono generati dei tipi GraphQL per `Model-1` e `Model-2`.

1. Poi modifica `Content-Fragment-Model-2`:

   1. verrà aggiornato solo il tipo GraphQL `Model-2`.

   1. Mentre `Model-1` rimarrà lo stesso.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di Frammento di contenuto tramite l’API REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, dove il client gestisce il fatto che lo schema viene chiamato con l’estensione `GQLschema`. Ad esempio, l’esecuzione di una semplice richiesta `GET` di `/content/cq:graphql/global/endpoint.GQLschema` si tradurrà nell’output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

<!-- move through to here to a separate "in depth" page -->

### Generazione schema: modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che venga pubblicato un modello di Frammento di contenuto principale, ma non il modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera uno schema *incompleto* per il modello di Frammento di contenuto principale. Ciò significa che il Riferimento al frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## Campi {#fields}

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati dall’utente.

   Selezione di [Tipi di dati](#Data-types) vengono utilizzati per creare campi in base alla modalità di configurazione del modello di frammento di contenuto. I nomi dei campi vengono ricavati dal **Nome proprietà** campo **Tipo di dati** scheda .

   * C&#39;è anche la **Rendering come** , in quanto gli utenti possono configurare determinati tipi di dati. Ad esempio, un campo di testo a riga singola può essere configurato in modo da contenere più testi a riga singola scegliendo `multifield` dal menu a discesa .

* GraphQL per AEM genera anche una serie di [campi di supporto](#helper-fields).

### Tipi di dati {#data-types}

GraphQL per AEM supporta un elenco di tipi. Vengono rappresentati tutti i tipi di dati dei modelli di Frammento di contenuto supportati e i corrispondenti tipi GraphQL:

| Modello di Frammento di contenuto: tipo di dati | Tipo GraphQL | Descrizione |
|--- |--- |--- |
| Testo su riga singola | Stringa, [Stringa] | Utilizzato per stringhe semplici come nomi di autore, nomi di posizione, ecc. |
| Testo su più righe | Stringa, [Stringa] | Utilizzato per l’output di testo, ad esempio il corpo di un articolo |
| Numero | Mobile, [Mobile] | Utilizzato per visualizzare il numero a virgola mobile e i numeri regolari |
| Booleano | Booleano | Utilizzato per visualizzare le caselle di controllo → semplici istruzioni true/false |
| Data e ora | Calendario | Utilizzato per visualizzare la data e l’ora in formato ISO 8601. A seconda del tipo selezionato, sono disponibili tre versioni da utilizzare in AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumerazione | Stringa | Utilizzato per visualizzare un’opzione da un elenco di opzioni definito durante la creazione del modello |
| Tag | [Stringa] | Utilizzato per visualizzare un elenco di stringhe che rappresentano tag utilizzati in AEM |
| Riferimento contenuto | Stringa, [Stringa] | Utilizzato per visualizzare il percorso per un’altra risorsa in AEM |
| Riferimento frammento | *Un tipo di modello* | Utilizzato per fare riferimento ad altri frammenti di contenuto di un determinato tipo di modello, definito al momento della creazione del modello |

### Campi di supporto {#helper-fields}

Oltre ai tipi di dati per i campi generati dall’utente, GraphQL for AEM genera anche una serie di campi *di supporto* per consentire l’identificazione di un frammento di contenuto o per fornire informazioni aggiuntive su un frammento di contenuto.

Tali [campi di supporto](#helper-fields) sono contrassegnati con un `_` per distinguere tra ciò che è stato definito dall’utente e ciò che è stato generato automaticamente.

#### Percorso  {#path}

Il campo percorso viene utilizzato come identificatore in AEM GraphQL. Rappresenta il percorso della risorsa Frammenti di contenuto all’interno dell’archivio AEM. Questo è l’identificatore di un frammento di contenuto, in quanto:

* è univoco all’interno di AEM,
* può essere facilmente recuperato.

Il codice seguente visualizza i percorsi di tutti i frammenti di contenuto creati in base al modello di frammento di contenuto `Author`, come fornito dall’esercitazione WKND .

```graphql
{
  authorList {
    items {
      _path
    }
  }
}
```

Inoltre, per recuperare un singolo frammento di contenuto di un tipo specifico, è necessario determinarne prima il percorso. Esempio:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _path
      firstName
      lastName
    }
  }
}
```

Vedi [Query di esempio: un singolo frammento di città specifico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadati {#metadata}

Tramite GraphQL, AEM espone inoltre i metadati di un frammento di contenuto. I metadati sono informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso delle miniature, la descrizione di un frammento di contenuto, la data di creazione, tra gli altri.

Poiché i metadati vengono generati tramite l’Editor schemi e, pertanto, non dispongono di una struttura specifica, il tipo di `TypedMetaData` GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate per i seguenti tipi scalari:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Ogni tipo scalare rappresenta una coppia nome-valore singola o un array di coppie nome-valore, in cui il valore di tale coppia è del tipo all&#39;interno del quale è stato raggruppato.

Ad esempio, se vuoi recuperare il titolo di un frammento di contenuto, si tratta di una proprietà stringa, pertanto è necessario eseguire una query per tutti i metadati stringa:

Per eseguire una query per i metadati:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
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
>**Differenza tra metadati normali e quelli di array**
>Nota: `StringMetadata` e `StringArrayMetadata` si riferiscono a ciò che è memorizzato nell’archivio, non alla modalità di recupero.
>
>Ad esempio, effettuando una chiamata del campo `stringMetadata`, può essere restituito un array di tutti i metadati memorizzati nell’archivio come una `String`; se si effettua una chiamata dell’`stringArrayMetadata` può essere restituito un array di tutti i metadati memorizzati nell’archivio come `String[]`.

Vedi [Query di esempio per metadati: elenca i metadati per riconoscimenti con titolo GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Varianti {#variations}

Il campo `_variations` è stato implementato per semplificare l’esecuzione delle query sulle varianti di un frammento di contenuto. Esempio:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>Tieni presente che `_variations` il campo non contiene un `master` variazione, tecnicamente, dei dati originali (a cui si fa riferimento come *Master* nell’interfaccia utente) non è considerata una variante esplicita.

Vedi [Query di esempio: tutte le città con una variante denominata](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>Se la variante specificata non esiste per un frammento di contenuto, i dati originali (noti anche come variante principale) verranno restituiti come impostazione predefinita (fallback).

<!--
## Security Considerations {#security-considerations}
-->

## Variabili GraphQL {#graphql-variables}

GraphQL consente di inserire variabili nella query. Per ulteriori informazioni, consulta la [documentazione di GraphQL per variabili](https://graphql.org/learn/queries/#variables).

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Author` in una specifica variante (se disponibile), puoi specificare l’argomento `variation` in GraphiQL.

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

**Query**:

```graphql
query($variation: String!) {
  authorList(variation: $variation) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

**Variabili di query**:

```json
{
  "variation": "another"
}
```

Questa query restituirà l’elenco completo degli autori. Autori senza `another` la variazione torna ai dati originali (`_variation` riferirà `master` in questo caso).

Se desideri limitare l’elenco agli autori che forniscono la variante specificata (e saltare gli autori che ritornano ai dati originali), devi applicare un [filter](#filtering):

```graphql
query($variation: String!) {
  authorList(variation: $variation, filter: {
    _variation: {
      _expressions: {
        value: $variation
      }
    }
  }) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

## Direttive GraphQL {#graphql-directives}

In GraphQL è possibile modificare le query basate su variabili, denominate Direttive GraphQL.

Ad esempio, puoi includere il campo `adventurePrice` in una query per tutti i `AdventureModels` basati su una variabile `includePrice`.

![Direttive GraphQL](assets/cfm-graphqlapi-04.png "Direttive GraphQL")

**Query**:

```graphql
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      title
      price @include(if: $includePrice)
    }
  }
}
```

**Variabili di query**:

```json
{
    "includePrice": true
}
```

## Filtro {#filtering}

Puoi inoltre utilizzare il filtro nelle query GraphQL per restituire dati specifici.

Il filtro utilizza una sintassi basata su operatori ed espressioni di tipo logico.

La parte più atomica è una singola espressione che può essere applicata al contenuto di un determinato campo. Confronta il contenuto del campo con un valore costante specificato.

Ad esempio, l&#39;espressione

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

confronta il contenuto del campo con il valore `some text` ed ha successo se il contenuto è uguale al valore . In caso contrario, l’espressione avrà esito negativo.

Per confrontare i campi con un determinato valore è possibile utilizzare i seguenti operatori:

| Operatore | Tipo/i | L’espressione ha esito positivo se ... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... il valore è esattamente lo stesso del contenuto del campo |
| `EQUALS_NOT` | `String`, `ID` | ... il valore è *not* come il contenuto del campo |
| `CONTAINS` | `String` | ... il contenuto del campo contiene il valore (`{ value: "mas", _op: CONTAINS }` corrisponderà `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ... il contenuto del campo *not* contiene il valore |
| `STARTS_WITH` | `ID` | ... l&#39;ID inizia con un certo valore (`{ value: "/content/dam/", _op: STARTS_WITH` corrisponderà `/content/dam/path/to/fragment`, ma non `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ... il valore è esattamente lo stesso del contenuto del campo |
| `UNEQUAL` | `Int`, `Float` | ... il valore è *not* come il contenuto del campo |
| `GREATER` | `Int`, `Float` | ... il contenuto del campo è maggiore del valore |
| `GREATER_EQUAL` | `Int`, `Float` | ... il contenuto del campo è maggiore o uguale al valore |
| `LOWER` | `Int`, `Float` | ... il contenuto del campo è inferiore al valore |
| `LOWER_EQUAL` | `Int`, `Float` | ... il contenuto del campo è inferiore o uguale al valore |
| `AT` | `Calendar`, `Date`, `Time` | ... il contenuto del campo è esattamente lo stesso del valore (inclusa l’impostazione del fuso orario) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ... il contenuto del campo è *not* uguale al valore |
| `BEFORE` | `Calendar`, `Date`, `Time` | ... il punto nel tempo indicato dal valore è prima del punto nel tempo indicato dal contenuto del campo |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... il momento indicato dal valore è precedente o nello stesso momento indicato dal contenuto del campo |
| `AFTER` | `Calendar`, `Date`, `Time` | ... il punto nel tempo indicato dal valore è successivo al punto nel tempo indicato dal contenuto del campo |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... il momento indicato dal valore è successivo o nello stesso momento indicato dal contenuto del campo |

Alcuni tipi consentono inoltre di specificare opzioni aggiuntive che modificano la modalità di valutazione di un’espressione:

| Opzione | Tipo/i | Descrizione |
|--- |--- |--- |
| `_ignoreCase` | `String` | Ignora il caso di una stringa, ad esempio un valore di `time` corrisponderà `TIME`, `time`, `tImE`... |
| `_sensitiveness` | `Float` | Consente un certo margine per `float` valori da considerare uguali (per aggirare i limiti tecnici dovuti alla rappresentazione interna di `float` valori; dovrebbe essere evitata, in quanto questa opzione potrebbe avere un impatto negativo sulle prestazioni |

Le espressioni possono essere combinate con un set tramite un operatore logico (`_logOp`):

* `OR` - il set di espressioni avrà esito positivo se almeno un’espressione avrà esito positivo
* `AND` - il set di espressioni avrà successo se tutte le espressioni avranno esito positivo (impostazione predefinita)

Ogni campo può essere filtrato in base al proprio set di espressioni. I set di espressioni di tutti i campi menzionati nell’argomento del filtro verranno infine combinati dal proprio operatore logico.

Una definizione di filtro (passata come `filter` argomento a una query) contiene:

* Una sottodefinizione per ciascun campo (a cui è possibile accedere tramite il suo nome, ad esempio, è disponibile una `lastName` nel filtro per `lastName` nel campo Tipo di dati (campo)
* Ogni sottodefinizione contiene la variabile `_expressions` array, fornendo il set di espressioni e `_logOp` campo che definisce l’operatore logico con cui combinare le espressioni
* Ciascuna espressione è definita dal valore (`value` e l&#39;operatore (`_operator` campo) il contenuto di un campo deve essere confrontato con

È possibile omettere `_logOp` per combinare gli elementi con `AND` e `_operator` se desideri verificare l’uguaglianza, in quanto questi sono i valori predefiniti.

L&#39;esempio seguente illustra una query completa che filtra tutte le persone con una `lastName` di `Provo` o contenenti `sjö`, indipendentemente dal caso:

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

È anche possibile filtrare i campi nidificati, ma non è consigliabile, in quanto potrebbe causare problemi di prestazioni.

Per altri esempi, consulta:

* informazioni dettagliate di [GraphQL per estensioni AEM](#graphql-extensions)

* [Query di esempio che utilizzano il contenuto e la struttura di esempio](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * e il [contenuto e la struttura di esempio](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) predisposta per l’utilizzo in query di esempio

* [Query di esempio basate sul progetto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## Ordinamento {#sorting}

>[!NOTE]
>
>Considera le migliori prestazioni [Aggiornamento dei frammenti di contenuto per la gestione delle pagine e l’ordinamento in GraphQL Filtering](/help/headless/graphql-api/graphql-paging-sorting-content-update.md).

Questa funzione ti consente di ordinare i risultati della query in base a un campo specificato.

I criteri di ordinamento:

* è un elenco di valori separati da virgola che rappresenta il percorso del campo
   * il primo campo dell’elenco definisce l’ordinamento primario, il secondo campo viene utilizzato se due valori del criterio di ordinamento principale sono uguali, il terzo se i primi due criteri sono uguali, ecc.
   * notazione tratteggiata, ad esempio field1.subfield.subfield, ecc.
* con una direzione d&#39;ordine opzionale
   * ASC (crescente) o DESC (decrescente); come ASC predefinito viene applicato
   * la direzione può essere specificata per campo; ciò significa che è possibile ordinare un campo in ordine crescente, un altro in ordine decrescente (nome, nome DESC)

Esempio:

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

Inoltre:

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

È inoltre possibile ordinare in base a un campo all’interno di un frammento nidificato utilizzando il formato `nestedFragmentname.fieldname`.

>[!NOTE]
>
>Questo potrebbe avere un impatto negativo sulle prestazioni.

Esempio:

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## Paging {#paging}

>[!NOTE]
>
>Considera le migliori prestazioni [Aggiornamento dei frammenti di contenuto per la gestione delle pagine e l’ordinamento in GraphQL Filtering](/help/headless/graphql-api/graphql-paging-sorting-content-update.md).

Questa funzione consente di eseguire il paging sui tipi di query che restituiscono un elenco. Vengono forniti due metodi:

* `offset` e `limit` in `List` query
* `first` e `after` in `Paginated` query

### Query elenco - offset e limite {#list-offset-limit}

In una `...List`query utilizzabile `offset` e `limit` per restituire un sottoinsieme specifico di risultati:

* `offset`: Specifica il primo set di dati da restituire
* `limit`: Specifica il numero massimo di set di dati da restituire

Ad esempio, per trasmettere la pagina dei risultati contenenti fino a cinque articoli, a partire dal quinto articolo dal *completato* elenco dei risultati:

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* Il paging richiede un ordinamento stabile per funzionare correttamente in più query che richiedono pagine diverse dello stesso set di risultati. Per impostazione predefinita, utilizza il percorso del repository di ogni elemento del set di risultati per assicurarsi che l&#39;ordine sia sempre lo stesso. Se viene utilizzato un ordinamento diverso e se tale ordinamento non può essere eseguito a livello di query JCR, le prestazioni risulteranno negative, poiché l’intero set di risultati deve essere caricato in memoria prima di determinare le pagine.
>
>* Maggiore è l&#39;offset, più tempo sarà necessario per saltare gli elementi dal set di risultati completo della query JCR. Una soluzione alternativa per i set di risultati di grandi dimensioni è quella di utilizzare la query impaginata con `first` e `after` metodo .


### Query impaginata - prima e dopo {#paginated-first-after}

La `...Paginated` il tipo di query riutilizza la maggior parte dei `...List` funzionalità del tipo di query (filtro, ordinamento), ma non utilizzare `offset`/`limit` utilizza `first`/`after` argomenti definiti [Specifica delle connessioni del cursore GraphQL](https://relay.dev/graphql/connections.htm). È possibile trovare un’introduzione meno formale nella [Introduzione a GraphQL](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: La `n` primi elementi da restituire.
Il valore predefinito è `50`.
Il massimo è `100`.
* `after`: Il cursore che determina l’inizio della pagina richiesta; notare che la voce rappresentata dal cursore non è inclusa nel set di risultati; il cursore di un elemento è determinato dalla `cursor` campo `edges` struttura.

Ad esempio, restituisce la pagina dei risultati contenenti fino a cinque avventure, a partire dalla voce del cursore specificata nel *completato* elenco dei risultati:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* Per impostazione predefinita, il paging utilizza l’UUID del nodo dell’archivio che rappresenta il frammento per ordinare in modo che l’ordine dei risultati sia sempre lo stesso. Quando `sort` viene utilizzato, l’UUID viene utilizzato implicitamente per garantire un ordinamento univoco; anche per due elementi con chiavi di ordinamento identiche.
>
>* A causa di vincoli tecnici interni, le prestazioni peggioreranno se l’ordinamento e il filtro vengono applicati ai campi nidificati. Si consiglia pertanto di utilizzare i campi di filtro/ordinamento memorizzati a livello di radice. Questo è anche il modo consigliato per eseguire query su set di risultati impaginati di grandi dimensioni.


## GraphQL per AEM: riepilogo delle estensioni {#graphql-extensions}

Le operazioni di base delle query con GraphQL per AEM sono conformi alle specifiche standard di GraphQL. Per le query GraphQL con AEM sono disponibili alcune estensioni:

* Se prevedi un elenco di risultati:
   * aggiungi `List` al nome del modello; ad esempio, `cityList`
   * Vedi [Query di esempio: informazioni su tutte le città](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

   Potete effettuare le seguenti operazioni:

   * [Ordinare i risultati](#sorting)

      * `ASC` : crescente
      * `DESC` : decrescente
   * Restituisce una pagina di risultati utilizzando:

      * [Query elenco con offset e limite](#list-offset-limit)
      * [Query impaginata con prima e dopo](#paginated-first-after)
   * Vedi [Query di esempio: informazioni su tutte le città](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)



* Se necessiti di un singolo risultato:
   * utilizza il nome del modello; ad es. città

* Se prevedi un elenco di risultati:
   * aggiungi `List` al nome del modello; ad esempio, `cityList`
   * Vedi [Query di esempio: informazioni su tutte le città](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* Se vuoi utilizzare un operatore OR logico:
   * utilizza ` _logOp: OR`
   * Vedi [Query di esempio: tutti gli utenti denominati “Jobs” o “Smith”](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* Esiste anche l’operatore AND logico, ma è (spesso) implicito

* Puoi eseguire query sui nomi dei campi corrispondenti ai campi all’interno del modello per frammenti di contenuto
   * Vedi [Query di esempio: informazioni complete sull’amministratore delegato e sui dipendenti di un’azienda](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono disponibili alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale`: per visualizzare la lingua; basato su Language Manager
         * Vedi [Query di esempio per più frammenti di contenuto di una specifica impostazione locale](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata`: per visualizzare i metadati del frammento
         * Vedi [Query di esempio per metadati: elenca i metadati per riconoscimenti con titolo GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
      * `_model`: consente di eseguire query per un modello per frammenti di contenuto (percorso e titolo)
         * Vedi [Query di esempio per un modello per frammenti di contenuto da un modello](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)
      * `_path`: il percorso del frammento di contenuto all’interno dell’archivio
         * Vedi [Query di esempio: un singolo frammento di città specifico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
      * `_reference`: per visualizzare riferimenti; inclusi riferimenti in linea nell’Editor testo RTF
         * Vedi [Query di esempio per più frammenti di contenuto con riferimenti di prelettura](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation`: per visualizzare varianti specifiche all’interno del frammento di contenuto

         >[!NOTE]
         >
         >Se per un frammento di contenuto non esiste la variante determinata, la variante principale verrà restituita come impostazione predefinita (fallback).

         * Vedi [Query di esempio: tutte le città con una variante denominata](#sample-cities-named-variation)
   * E operazioni:

      * `_operator`: applica operatori specifici; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Vedi [Query di esempio: tutti gli utenti non denominati “Jobs”](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * Vedi [Query di esempio: tutte le avventure in cui `_path` inizia con un prefisso specifico](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`: applica condizioni specifiche; ad esempio, `AT_LEAST_ONCE`
         * Vedi [Query di esempio: applica filtro su un array con un elemento che deve verificarsi almeno una volta](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase`: per ignorare il caso durante la query
         * Vedi [Query di esempio: tutte le città che contengono SAN nel nome, indipendentemente da maiuscole/minuscole](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)









* I tipi di unione GraphQL sono supportati:

   * utilizza `... on`
      * Vedi [Query di esempio per un frammento di contenuto di un modello specifico con un riferimento ai contenuti](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* Fallback durante la query dei frammenti nidificati:

   * Se una determinata variante non esiste in un frammento nidificato, viene restituita la variabile **principale**.

## Query dell’endpoint di GraphQL da un sito Web esterno {#query-graphql-endpoint-from-external-website}

Per accedere all’endpoint di GraphQL da un sito web esterno è necessario configurare i seguenti elementi:

* [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Filtro referrer](/help/headless/deployment/referrer-filter.md)

## Autenticazione {#authentication}

Vedi [Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/headless/security/authentication.md).

## Domande frequenti {#faqs}

Domande poste:

1. **D**: “*quali sono le differenze tra l’API di GraphQL per AEM e l’API di Query Builder?*”

   * **R**: 
“*l’API di GraphQL per AEM offre il controllo totale dell’output JSON ed è uno standard di settore per l’esecuzione di query sui contenuti.
In futuro, AEM prevede di investire nell’API di GraphQL per AEM.*”

## Tutorial: guida introduttiva ad AEM headless e GraphQL {#tutorial}

Cerchi un pratico tutorial? Dai un&#39;occhiata al tutorial [Guida introduttiva di headless AEM e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) che illustra come creare ed esporre contenuti, utilizzati da un’app esterna, mediante le API GraphQL di AEM in uno scenario CMS headless.
