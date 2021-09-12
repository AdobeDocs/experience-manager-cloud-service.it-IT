---
title: AEM API GraphQL per l’utilizzo con frammenti di contenuto
description: Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) come Cloud Service con l’API GraphQL AEM per la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '3929'
ht-degree: 1%

---


# AEM API GraphQL per l’utilizzo con frammenti di contenuto {#graphql-api-for-use-with-content-fragments}

Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) come Cloud Service con l’API GraphQL AEM per la distribuzione di contenuti headless.

AEM come API GraphQL di Cloud Service utilizzata con i frammenti di contenuto si basa principalmente sull’API GraphQL standard open source.

L’utilizzo dell’API GraphQL in AEM consente la distribuzione efficiente di frammenti di contenuto ai client JavaScript in implementazioni CMS headless:

* Evitare richieste API iterative come con REST,
* garantire che la consegna sia limitata ai requisiti specifici,
* Consentire la distribuzione in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) come Cloud Service:
>
>* [AEM Commerce consuma dati da una piattaforma Commerce tramite GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Frammenti di contenuto collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni.


## API GraphQL {#graphql-api}

GraphQL è:

* &quot;*..un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell&#39;API, dà ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, rende più semplice evolvere le API nel tempo e consente potenti strumenti per sviluppatori.*&quot;.

   Consulta [GraphQL.org](https://graphql.org)

* &quot;*..una specifica aperta per un livello API flessibile. Posiziona GraphQL sui backend esistenti per creare prodotti più rapidamente che mai....*&quot;.

   Consulta [Esplorare GraphQL](https://www.graphql.com).

* *&quot;..un linguaggio e una specifica di query di dati sviluppati internamente da Facebook nel 2012 prima di essere pubblicamente aperti dal 2015. Offre un’alternativa alle architetture basate su REST allo scopo di aumentare la produttività degli sviluppatori e ridurre al minimo le quantità di dati trasferiti. GraphQL viene utilizzato in produzione da centinaia di organizzazioni di tutte le dimensioni...&quot;*

   Consulta [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Per ulteriori informazioni sull’API GraphQL, consulta le sezioni seguenti (tra cui molte altre risorse):

* In [graphql.org](https://graphql.org):

   * [Introduzione a GraphQL](https://graphql.org/learn)

   * [Specifica GraphQL](http://spec.graphql.org/)

* Su [graphql.com](https://graphql.com):

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

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * Il percorso in AEM che risponde alle query GraphQL e fornisce accesso agli schemi GraphQL.

   * Per ulteriori informazioni, consulta [Abilitazione dell&#39;endpoint GraphQL](#enabling-graphql-endpoint) .

Per informazioni dettagliate, incluse le [best practice](https://graphql.org/learn/best-practices/), consulta l’ [(GraphQL.org) Introduzione a GraphQL](https://graphql.org/learn/) .

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per restituire:

* A **singola voce**

* A **[elenco di voci](https://graphql.org/learn/schema/#lists-and-non-null)**

Puoi anche eseguire le seguenti operazioni:

* [Query persistenti memorizzate nella cache](#persisted-queries-caching)

>[!NOTE]
>Puoi testare ed eseguire il debug delle query GraphQL utilizzando l&#39; [IDE GraphiQL](#graphiql-interface).

## GraphQL per AEM endpoint {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere allo schema GraphQL,
* invia le query GraphQL,
* ricevere le risposte (alle query GraphQL).

Esistono due tipi di endpoint in AEM:

* Globale
   * Disponibile per tutti i siti.
   * Questo endpoint può utilizzare tutti i modelli di frammenti di contenuto da tutte le configurazioni di Sites (definite in [Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Se esistono modelli di frammento di contenuto che devono essere condivisi tra le configurazioni di Sites, questi devono essere creati nelle configurazioni di Sites globali.
* Configurazioni siti:
   * Corrisponde a una configurazione Sites, come definita nel [Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Specifico per un sito/progetto specifico.
   * Un endpoint specifico per la configurazione di Sites utilizzerà i modelli di frammento di contenuto di quella specifica configurazione di Sites insieme a quelli della configurazione di Sites globale.

>[!CAUTION]
>
>L’Editor frammento di contenuto può consentire a un frammento di contenuto di una configurazione Sites di fare riferimento a un frammento di contenuto di un’altra configurazione Sites (tramite criteri).
>
>In questo caso non tutti i contenuti saranno recuperabili utilizzando un endpoint specifico per la configurazione di Sites.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile considerare l’idea di inserire modelli di frammenti di contenuto condivisi nella configurazione Siti globali .

Il percorso dell&#39;archivio di GraphQL per AEM endpoint globale è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare un endpoint per GraphQL per AEM è necessario:

* [Abilita l&#39;endpoint GraphQL](#enabling-graphql-endpoint)
* [Pubblica l’endpoint GraphQL](#publishing-graphql-endpoint)

### Abilitazione dell’endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata. Consulta [Frammenti di contenuto - Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se l&#39;utilizzo dei modelli di frammento di contenuto [non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l&#39;opzione **Crea** non sarà disponibile.

Per abilitare l&#39;endpoint corrispondente:

1. Passa a **Strumenti**, **Risorse**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Viene aperta la finestra di dialogo **Crea nuovo endpoint GraphQL** . Qui puoi specificare:
   * **Nome**: nome del punto finale; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza il menu a discesa per selezionare il sito o il progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato il seguente avviso:
   >
   >* *Se non vengono gestiti correttamente, gli endpoint GraphQL possono introdurre problemi di prestazioni e sicurezza dei dati. Dopo aver creato un endpoint, assicurati di impostare le autorizzazioni appropriate.*


1. Conferma con **Crea**.
1. La finestra di dialogo **Passaggi successivi** fornirà un collegamento diretto alla console Sicurezza per garantire che l’endpoint appena creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare ACL, appropriati al tuo caso d&#39;uso, sull&#39;endpoint.

### Pubblicazione dell’endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Devi impostare ACL appropriati al tuo caso d&#39;uso sull&#39;endpoint.

## Interfaccia GraphiQL {#graphiql-interface}

È disponibile un’implementazione dell’interfaccia standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) da utilizzare con AEM GraphQL. Può essere installato [con AEM](#installing-graphiql-interface).

>[!NOTE]
>
>GraphiQL è associato all’endpoint globale (e non funziona con altri endpoint per configurazioni specifiche di Sites).

Questa interfaccia ti consente di inserire e testare direttamente le query.

Esempio:

* `http://localhost:4502/content/graphiql.html`

Questo fornisce funzioni quali evidenziazione della sintassi, completamento automatico, auto-suggerimento, insieme a una cronologia e a una documentazione online:

![Interfaccia ](assets/cfm-graphiql-interface.png "GraphiQL")

### Installazione dell&#39;interfaccia AEM GraphiQL {#installing-graphiql-interface}

L&#39;interfaccia utente GraphiQL può essere installata su AEM con un pacchetto dedicato: il pacchetto [GraphiQL Content Package v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

## Casi d’uso per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi di utilizzo possono dipendere dal tipo di AEM come ambiente di Cloud Service:

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

Per i frammenti di contenuto, gli schemi GraphQL (struttura e tipi) si basano su **Enabled** [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello per frammenti di contenuto denominato `Article`, AEM genera l’oggetto `article` di tipo `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Un Modello Di Frammento Di Contenuto:

   ![Modello per frammento di contenuto da utilizzare con ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model per l’utilizzo con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su schema ](assets/cfm-graphqlapi-02.png "ModelGraphQL per frammenti di contenuto basato su modello di frammento di contenuto")

   Questo indica che il tipo generato `ArticleModel` contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Questi [campi helper](#helper-fields) sono contrassegnati con un `_` precedente per distinguere tra ciò che è stato definito dall&#39;utente e ciò che è stato generato automaticamente.

1. Dopo che un utente crea un frammento di contenuto basato sul modello di articolo, può essere interrogato tramite GraphQL. Per esempi, consulta le [Query di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (basate su una [struttura di frammenti di contenuto di esempio da utilizzare con GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si aggiorna un modello di frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e di garantire stabilità.

Ad esempio, se:

1. Installa un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Verranno generati i tipi GraphQL per `Model-1` e `Model-2`.

1. Quindi modifica `Content-Fragment-Model-2`:

   1. Verrà aggiornato solo il tipo `Model-2` GraphQL.

   1. `Model-1` rimarrà invariato.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di frammenti di contenuto tramite l’api REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, con il client che gestisce il fatto che lo schema viene chiamato con l&#39;estensione `GQLschema`. Ad esempio, l’esecuzione di una semplice richiesta `GET` su `/content/cq:graphql/global/endpoint.GQLschema` darà luogo all’output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

### Generazione schema - Modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che un modello di frammento di contenuto principale venga pubblicato, ma non lo è un modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera uno schema *incompleto* per il modello di frammento di contenuto principale. Ciò significa che il Riferimento frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## espandibili {#fields}

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati.

   Una selezione di [Tipi di campo](#field-types) viene utilizzata per creare campi in base alla modalità di configurazione del modello di frammento di contenuto. I nomi dei campi sono ricavati dal campo **Nome proprietà** del **Tipo di dati**.

   * È inoltre disponibile la proprietà **Rendering come** da considerare, in quanto gli utenti possono configurare determinati tipi di dati; ad esempio, come testo a riga singola o come campo multiplo.

* GraphQL per AEM genera anche un numero di [campi helper](#helper-fields).

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
| Riferimento frammento |  *Tipo di modello* |  Utilizzato per fare riferimento a un altro frammento di contenuto di un determinato tipo di modello, definito al momento della creazione del modello |

### Campi helper {#helper-fields}

Oltre ai tipi di dati per i campi generati dall’utente, GraphQL per AEM genera anche una serie di campi *helper* per facilitare l’identificazione di un frammento di contenuto o per fornire informazioni aggiuntive su un frammento di contenuto.

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

Consulta [Query di esempio - Un singolo frammento di città specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadati {#metadata}

Tramite GraphQL, AEM espone anche i metadati di un frammento di contenuto. I metadati sono informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso delle miniature, la descrizione di un frammento di contenuto, la data di creazione, tra gli altri.

Poiché i metadati vengono generati tramite l’Editor di schema e in quanto tali non dispongono di una struttura specifica, il tipo `TypedMetaData` GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate per i seguenti tipi scalari:

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
>Tieni presente che `StringMetadata` e `StringArrayMetadata` si riferiscono entrambi a ciò che è memorizzato nell’archivio e non a come lo recuperi.
>
>Ad esempio, chiamando il campo `stringMetadata` riceverai un array di tutti i metadati memorizzati nell&#39;archivio come `String` , e se richiami `stringArrayMetadata` riceverai un array di tutti i metadati memorizzati nell&#39;archivio come `String[]`.

Consulta [Query di esempio per metadati - Elencare i metadati per i premi denominati GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Varianti {#variations}

Il campo `_variations` è stato implementato per semplificare la query delle varianti di un frammento di contenuto. Esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulta [Query di esempio - Tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variabili GraphQL {#graphql-variables}

GraphQL consente di inserire le variabili nella query. Per ulteriori informazioni, consulta la documentazione [GraphQL per le variabili](https://graphql.org/learn/queries/#variables).

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Article` con una variante specifica, puoi specificare la variabile `variation` in GraphiQL.

![Variabili GraphQL ](assets/cfm-graphqlapi-03.png "VariablesGraphQL")

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

Ad esempio, è possibile includere il campo `adventurePrice` in una query per tutti i valori `AdventureModels`, in base a una variabile `includePrice`.

![Direttive ](assets/cfm-graphqlapi-04.png "GraphQL")

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

Ad esempio, la seguente query (di base) filtra tutte le persone con un nome `Jobs` o `Smith`:

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

* dettagli di [GraphQL per le estensioni AEM](#graphql-extensions)

* [Query di esempio con contenuto e struttura di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E la [Struttura e contenuto di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparata per l&#39;uso nelle query di esempio

* [Query di esempio basate sul progetto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL per AEM - Riepilogo delle estensioni {#graphql-extensions}

Il funzionamento di base delle query con GraphQL per AEM rispettare la specifica GraphQL standard. Per le query GraphQL con AEM sono disponibili alcune estensioni:

* Se hai bisogno di un singolo risultato:
   * utilizzare il nome del modello; città

* Se si prevede un elenco di risultati:
   * aggiungere `List` al nome del modello; ad esempio, `cityList`
   * Consulta [Query di esempio - Tutte le informazioni su Tutte le città](#sample-all-information-all-cities)

* Se desideri utilizzare un operatore OR logico:
   * use ` _logOp: OR`
   * Vedere [Query di esempio - Tutte le persone con un nome &quot;Jobs&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Esiste anche l&#39;AND logico, ma è (spesso) implicito

* È possibile eseguire query sui nomi di campo corrispondenti ai campi all’interno del modello di frammento di contenuto
   * Consulta [Query di esempio - Dettagli completi sull&#39;amministratore delegato e sui dipendenti di un&#39;azienda](#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono presenti alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale` : rivelare la lingua; basato su Language Manager
         * Consulta [Query di esempio per più frammenti di contenuto di una determinata impostazione internazionale](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : per visualizzare i metadati del frammento
         * Consulta [Esempio di query per metadati - Elenco dei metadati per i premi denominati GB](#sample-metadata-awards-gb)
      * `_model` : consentire la query per un modello di frammento di contenuto (percorso e titolo)
         * Consulta [Query di esempio per un modello di frammento di contenuto da un modello](#sample-wknd-content-fragment-model-from-model)
      * `_path` : percorso del frammento di contenuto all’interno dell’archivio
         * Vedere [Query di esempio - Un singolo frammento di città specifico](#sample-single-specific-city-fragment)
      * `_reference` : rivelare riferimenti; inclusione di riferimenti in linea nell’Editor Rich Text
         * Consulta [Query di esempio per più frammenti di contenuto con riferimenti prerecuperati](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : per visualizzare varianti specifiche all’interno del frammento di contenuto
         * Consulta [Query di esempio - Tutte le città con una variante denominata](#sample-cities-named-variation)
   * e operazioni:

      * `_operator` : applicare operatori specifici;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Vedere [Query di esempio - Tutte le persone che non hanno un nome di &quot;Jobs&quot;](#sample-all-persons-not-jobs)
         * Consulta [Query di esempio - Tutte le avventure in cui il `_path` inizia con un prefisso specifico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : applicare condizioni specifiche; ad esempio,   `AT_LEAST_ONCE`
         * Vedere [Query di esempio - Filtro su una matrice con un elemento che deve verificarsi almeno una volta](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : per ignorare il caso durante la query
         * Vedere [Query di esempio - Tutte le città con SAN nel nome, indipendentemente dal caso](#sample-all-cities-san-ignore-case)









* I tipi di unione GraphQL sono supportati:

   * utilizza `... on`
      * Consulta [Query di esempio per un frammento di contenuto di un modello specifico con un riferimento di contenuto](#sample-wknd-fragment-specific-model-content-reference)

## Query persistenti (memorizzazione in cache) {#persisted-queries-caching}

Dopo aver preparato una query con una richiesta POST, può essere eseguita con una richiesta GET memorizzabile nella cache tramite cache HTTP o CDN.

Questo è necessario in quanto le query POST di solito non vengono memorizzate nella cache e se si utilizza GET con la query come parametro esiste un rischio significativo che il parametro diventi troppo grande per i servizi HTTP e gli intermediari.

Le query persistenti devono sempre utilizzare l&#39;endpoint correlato alla [configurazione Sites appropriata](#graphql-aem-endpoint); in modo che possano utilizzare una delle due opzioni, oppure entrambe:

* Configurazione globale ed endpoint
La query ha accesso a tutti i modelli di frammento di contenuto.
* Configurazione e endpoint di Sites specifici
La creazione di una query persistente per una configurazione specifica di Sites richiede un endpoint specifico per la configurazione di Sites corrispondente (per fornire accesso ai relativi modelli di frammenti di contenuto).
Ad esempio, per creare una query persistente specifica per la configurazione di WKND Sites, è necessario creare in anticipo una configurazione di Sites specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Abilita funzionalità frammento di contenuto nel browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) .
>
>È necessario abilitare le **query di persistenza GraphQL** per la configurazione Sites appropriata.

Ad esempio, se esiste una particolare query denominata `my-query` che utilizza un modello `my-model` dalla configurazione Sites `my-conf`:

* Puoi creare una query utilizzando l’endpoint specifico `my-conf`, quindi la query verrà salvata come segue:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puoi creare la stessa query utilizzando l’endpoint `global`, ma la query verrà salvata come segue:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Queste sono due query diverse - salvate in percorsi diversi.
>
>Usano lo stesso modello, ma attraverso endpoint diversi.


Di seguito sono riportati i passaggi necessari per mantenere una determinata query:

1. Prepara la query inserendola nel nuovo URL dell&#39;endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Ad esempio, crea una query persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. A questo punto, controlla la risposta.

   Ad esempio, controlla il successo:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. È quindi possibile riprodurre nuovamente la query persistente utilizzando GETing l&#39;URL `/graphql/execute.json/<shortPath>`.

   Ad esempio, utilizza la query persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Aggiornare una query persistente tramite POSTing a un percorso di query già esistente.

   Ad esempio, utilizza la query persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Crea una query normale con wrapping.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crea una query normale con wrapping con il controllo della cache.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crea una query persistente con parametri:

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Esecuzione di una query con parametri.

   Esempio:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Per eseguire la query al momento della pubblicazione, la struttura ad albero persistente correlata deve essere replicata

   * Utilizzo di un POST per la replica:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Utilizzando un pacchetto:
      1. Crea una nuova definizione di pacchetto.
      1. Includi la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Crea il pacchetto.
      1. Replicare il pacchetto.
   * Utilizzo dello strumento di replica/distribuzione.
      1. Passa allo strumento Distribuzione .
      1. Seleziona l’attivazione ad albero per la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
   * Utilizzo di un flusso di lavoro (tramite la configurazione del modulo di avvio del flusso di lavoro):
      1. Definisci una regola di avvio del flusso di lavoro per l’esecuzione di un modello di flusso di lavoro che replichi la configurazione su eventi diversi (ad esempio, crea, modifica, tra gli altri).



1. Quando la configurazione della query è attiva per la pubblicazione, si applicano gli stessi principi, utilizzando solo l’endpoint di pubblicazione.

   >[!NOTE]
   >
   >Per l&#39;accesso anonimo il sistema presuppone che l&#39;ACL consenta a &quot;tutti&quot; di avere accesso alla configurazione della query.
   >
   >In caso contrario, non potrà essere eseguito.

   >[!NOTE]
   >
   >Eventuali punti e virgola (&quot;;&quot;) negli URL devono essere codificati.
   >
   >Ad esempio, come nella richiesta di eseguire una query persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Query dell’endpoint GraphQL da un sito Web esterno {#query-graphql-endpoint-from-external-website}

Per accedere all’endpoint GraphQL da un sito Web esterno è necessario configurare i seguenti elementi:

* [Filtro CORS](#cors-filter)
* [Filtro di riferimento](#referrer-filter)

### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Per una panoramica dettagliata dei criteri di condivisione delle risorse CORS in AEM, consulta [Comprendere la condivisione delle risorse tra le origini (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS nell’archivio Git del cliente. Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati.

Questa configurazione deve specificare un&#39;origine del sito web attendibile `alloworigin` o `alloworiginregexp` per la quale è necessario concedere l&#39;accesso.

Ad esempio, per concedere l’accesso all’endpoint GraphQL e all’endpoint di query persistenti per `https://my.domain` puoi utilizzare:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se hai configurato un percorso personalizzato per l’endpoint, puoi utilizzarlo anche in `allowedpaths`.

### Filtro di riferimento {#referrer-filter}

Oltre alla configurazione CORS, è necessario configurare un filtro Referrer per consentire l’accesso da host di terze parti.

A questo scopo, aggiungi un file di configurazione OSGi Referrer Filter appropriato che:

* specifica un nome host del sito web fidato; `allow.hosts` o `allow.hosts.regexp`,
* concede l&#39;accesso per questo nome host.

Ad esempio, per concedere l’accesso alle richieste con il referente `my.domain` puoi:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Spetta al cliente:
>
>* concedere solo l&#39;accesso ai domini trusted
>* assicurati che non siano esposte informazioni sensibili
>* non utilizzare una sintassi jolly [*]; entrambi disattiveranno l’accesso autenticato all’endpoint GraphQL e lo esporranno a tutto il mondo.


>[!CAUTION]
>
>Tutti gli schemi GraphQL [](#schema-generation) (derivati dai modelli di frammenti di contenuto che sono stati **Abilitati**) sono leggibili tramite l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

## Autenticazione {#authentication}

Consulta [Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

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

1. **D**: &quot;*In che modo l’API GraphQL per AEM è diversa dall’API di Query Builder?*&quot;

   * **A**: &quot;*L’API GraphQL di AEM offre il controllo totale sull’output JSON ed è uno standard di settore per l’esecuzione di query sui contenuti.
In futuro, AEM sta pianificando di investire nell&#39;API GraphQL AEM.*&quot;

## Tutorial: guida introduttiva a AEM Headless e GraphQL {#tutorial}

Stai cercando un tutorial pratico? Consulta la [Guida introduttiva AEM Headless e l’esercitazione end-to-end GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) che illustra come creare ed esporre contenuti utilizzando le API GraphQL di AEM e utilizzati da un’app esterna, in uno scenario CMS headless.
