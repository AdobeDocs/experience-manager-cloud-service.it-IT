---
title: AEM GraphQL API per l'utilizzo con frammenti di contenuto
description: Scoprite come utilizzare i frammenti di contenuto in Adobe Experience Manager (AEM) come Cloud Service con l'API AEM GraphQL per la distribuzione senza titolo dei contenuti.
translation-type: tm+mt
source-git-commit: 36e0fd66c9119571cde5c8791862abed8b552d5a
workflow-type: tm+mt
source-wordcount: '3220'
ht-degree: 1%

---


# AEM GraphQL API per l&#39;utilizzo con frammenti di contenuto {#graphql-api-for-use-with-content-fragments}

L&#39;API Adobe Experience Manager come Cloud Service (AEM) GraphQL utilizzata con i frammenti di contenuto è fortemente basata sull&#39;API GraphQL standard open source.

L&#39;utilizzo dell&#39;API GraphQL in AEM consente la distribuzione efficiente di frammenti di contenuto ai client JavaScript nelle implementazioni CMS headless:

* Evitare richieste API iterative come con REST,
* garantire che la consegna sia limitata ai requisiti specifici,
* Consentire la consegna in massa di esattamente ciò che è necessario per il rendering come risposta a una singola query API.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) come Cloud Service:
>
>* [AEM Commerce consuma i dati provenienti da una piattaforma di eCommerce tramite GraphQL](/help/commerce-cloud/architecture/magento.md).
>* AEM Frammenti di contenuto collaborano con l&#39;API AEM GraphQL (un&#39;implementazione personalizzata, basata su GraphQL standard) per fornire contenuto strutturato da utilizzare nelle applicazioni.


## API GraphQL {#graphql-api}

GraphQL è:

* &quot;*...un linguaggio di query per le API e un runtime per l&#39;esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell&#39;API, dà ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, rende più semplice l&#39;evoluzione delle API nel tempo e abilita potenti strumenti di sviluppo.*&quot;.

   Vedere [GraphQL.org](https://graphql.org)

* &quot;*...una specifica aperta per un livello API flessibile. Inserisci GraphQL sui tuoi backend esistenti per creare prodotti più rapidamente che mai....*&quot;.

   Vedere [Esplora GraphQL](https://www.graphql.com).

* *&quot;...una lingua e una specifica per le query di dati sviluppata internamente da Facebook nel 2012 prima di essere pubblicamente aperta dal 2015. Offre un&#39;alternativa alle architetture basate su REST allo scopo di aumentare la produttività degli sviluppatori e ridurre al minimo le quantità di dati trasferiti. GraphQL è utilizzato nella produzione da centinaia di organizzazioni di tutte le dimensioni...&quot;*

   Vedere [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Per ulteriori informazioni sull&#39;API GraphQL, consultate le seguenti sezioni (tra cui molte altre risorse):

* A [graphql.org](https://graphql.org):

   * [Introduzione a GraphQL](https://graphql.org/learn)

   * [Specifica GraphQL](http://spec.graphql.org/)

* A [graphql.com](https://graphql.com):

   * [Guide](https://www.graphql.com/guides/)

   * [Esercitazioni](https://www.graphql.com/tutorials/)

   * [Case study](https://www.graphql.com/case-studies/)

GraphQL per AEM implementazione si basa sulla libreria Java GraphQL standard. Consulta:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java a GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL utilizza quanto segue:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemi e tipi](https://graphql.org/learn/schema/)**:

   * Gli schemi sono generati da AEM basati sui modelli di frammenti di contenuto.
   * Utilizzando gli schemi, GraphQL presenta i tipi e le operazioni consentiti per GraphQL per AEM implementazione.

* **[Campi](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * Percorso in AEM che risponde alle query GraphQL e fornisce l&#39;accesso agli schemi GraphQL.

   * Per ulteriori informazioni, vedere [Abilitazione dell&#39;endpoint GraphQL](#enabling-graphql-endpoint).

Per informazioni dettagliate, comprese le [Best Practices](https://graphql.org/learn/best-practices/), consultate [(GraphQL.org) Introduction to GraphQL](https://graphql.org/learn/) (Introduzione a GraphQL.org).

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per restituire:

* A **voce singola**

* Un **[elenco di voci](https://graphql.org/learn/schema/#lists-and-non-null)**

Potete inoltre eseguire le seguenti operazioni:

* [Query persistenti memorizzate nella cache](#persisted-queries-caching)

## GraphQL per AEM endpoint {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la vostra app) potete:

* accedere allo schema GraphQL,
* invia le tue query GraphQL,
* ricevere le risposte (alle query GraphQL).

Il percorso del repository di GraphQL per AEM endpoint è:

`/content/cq:graphql/global/endpoint`

Nell’URL della richiesta l’app può usare il seguente percorso:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare l&#39;endpoint per GraphQL per AEM è necessario:

>[!CAUTION]
>
>Questi passi possono cambiare nel prossimo futuro.

* [Abilita l&#39;endpoint GraphQL](#enabling-graphql-endpoint)
* [Eseguire configurazioni aggiuntive](#additional-configurations-graphql-endpoint)

### Abilitazione dell&#39;endpoint GraphQL {#enabling-graphql-endpoint}

>[!NOTE]
>
>Per informazioni dettagliate sui pacchetti forniti  Adobe per semplificare i passaggi descritti, vedere [Pacchetti di supporto](#supporting-packages).

Per abilitare le query GraphQL in AEM, create un endpoint in `/content/cq:graphql/global/endpoint`:

* I nodi `cq:graphql` e `global` devono essere di tipo `sling:Folder`.
* Il nodo `endpoint` deve essere di tipo `nt:unstructured` e contenere `sling:resourceType` di `graphql/sites/components/endpoint`.

>[!CAUTION]
>
>Si è verificato un problema noto con l&#39;endpoint:
>
>* La voce `cq:graphql` è visibile nella console **Siti**; al livello superiore.
   >  Questo non deve essere utilizzato.


>[!CAUTION]
>
>L&#39;endpoint è accessibile a tutti. Ciò può causare problemi di sicurezza, soprattutto nelle istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>È possibile impostare gli ACL, in base al caso di utilizzo, sull&#39;endpoint.

>[!NOTE]
>
>L&#39;endpoint non funzionerà. È necessario fornire [configurazioni aggiuntive per GraphQL Endpoint](#additional-configurations-graphql-endpoint) separatamente.

>[!NOTE]
>È inoltre possibile testare ed eseguire il debug delle query GraphQL utilizzando l&#39; [GraphiQL IDE](#graphiql-interface).

### Configurazioni aggiuntive per Endpoint GraphQL {#additional-configurations-graphql-endpoint}

>[!NOTE]
>
>Per informazioni dettagliate sui pacchetti forniti  Adobe per semplificare i passaggi descritti, vedere [Pacchetti di supporto](#supporting-packages).

Sono necessarie configurazioni aggiuntive:

* Dispatcher:
   * Per consentire gli URL richiesti
   * Obbligatorio
* URL personalizzato:
   * Per allocare un URL semplificato per l&#39;endpoint
   * Facoltativo
* Configurazione OSGi:
   * Configurazione servlet GraphQL:
      * Gestisce le richieste all&#39;endpoint
      * Il nome della configurazione è `org.apache.sling.graphql.core.GraphQLServlet`. Deve essere fornito come configurazione di fabbrica OSGi
      * `sling.servlet.extensions` deve essere impostato su  `[json]`
      * `sling.servlet.methods` deve essere impostato su  `[GET,POST]`
      * `sling.servlet.resourceTypes` deve essere impostato su  `[graphql/sites/components/endpoint]`
      * Obbligatorio
   * Configurazione servlet schema:
      * Crea lo schema GraphQL
      * Il nome della configurazione è `com.adobe.aem.graphql.sites.adapters.SlingSchemaServlet`. Deve essere fornito come configurazione di fabbrica OSGi
      * `sling.servlet.extensions` deve essere impostato su  `[GQLschema]`
      * `sling.servlet.methods` deve essere impostato su  `[GET]`
      * `sling.servlet.resourceTypes` deve essere impostato su  `[graphql/sites/components/endpoint]`
      * Obbligatorio
   * Configurazione CSRF:
      * Protezione dell&#39;endpoint
      * Il nome della configurazione è `com.adobe.granite.csrf.impl.CSRFFilter`
      * Aggiungi `/content/cq:graphql/global/endpoint` all&#39;elenco esistente di percorsi esclusi (`filter.excluded.paths`)
      * Obbligatorio

### Pacchetti di supporto {#supporting-packages}

Per semplificare la configurazione di un endpoint GraphQL,  Adobe fornisce il pacchetto [GraphQL Sample Project](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-sample.zip).

Questo archivio contiene sia [la configurazione aggiuntiva ](#additional-configurations-graphql-endpoint) che [l&#39;endpoint GraphQL](#enabling-graphql-endpoint). Se installato in un&#39;istanza AEM normale, verrà esposto un endpoint GraphQL completamente funzionante in `/content/cq:graphql/global/endpoint`.

Questo pacchetto è inteso come un progetto per i vostri progetti GraphQL. Per informazioni sull&#39;utilizzo del pacchetto, vedere il pacchetto **README**.

Se preferite creare manualmente la configurazione richiesta,  Adobe fornisce anche un [GraphQL Endpoint Content Package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip) dedicato. Questo pacchetto di contenuto contiene solo l&#39;endpoint GraphQL, senza alcuna configurazione.

## Interfaccia GraphiQL {#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

È disponibile per l&#39;uso con AEM GraphQL un&#39;implementazione dell&#39;interfaccia standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql). Questo può essere installato [con AEM](#installing-graphiql-interface).

Questa interfaccia consente di inserire e testare direttamente le query.

Esempio:

* `http://localhost:4502/content/graphiql.html`

Questo fornisce funzioni come evidenziazione della sintassi, completamento automatico, suggerimento automatico, insieme a una cronologia e alla documentazione online:

![Interfaccia ](assets/cfm-graphiql-interface.png "GraphiQLGraphiQL")

### Installazione dell&#39;interfaccia AEM GraphiQL {#installing-graphiql-interface}

L&#39;interfaccia utente GraphiQL può essere installata su AEM con un pacchetto dedicato: il pacchetto [GraphiQL Content Package v0.0.4](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphiql-0.0.4.zip).

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## Casi di utilizzo per ambienti di creazione e pubblicazione {#use-cases-author-publish-environments}

I casi di utilizzo possono dipendere dal tipo di AEM come ambiente di Cloud Service:

* Ambiente di pubblicazione; utilizzato per:
   * Dati query per l&#39;applicazione JS (caso d&#39;uso standard)

* Ambiente di authoring; utilizzato per:
   * Dati query per &quot;scopi di gestione del contenuto&quot;:
      * GraphQL in AEM come Cloud Service è attualmente un&#39;API di sola lettura.
      * L&#39;API REST può essere utilizzata per le operazioni CR(u)D.

## Autorizzazioni  {#permission}

Le autorizzazioni sono quelle necessarie per accedere alle risorse.

## Generazione schema {#schema-generation}

GraphQL è un&#39;API fortemente tipizzata, il che significa che i dati devono essere chiaramente strutturati e organizzati per tipo.

La specifica GraphQL fornisce una serie di linee guida su come creare un&#39;API affidabile per l&#39;interrogazione dei dati su una determinata istanza. A tal fine, un client deve recuperare il [Schema](#schema-generation), che contiene tutti i tipi necessari per una query.

Per i frammenti di contenuto, gli schemi GraphQL (struttura e tipi) si basano su **Enabled** [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati da modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l&#39;endpoint GraphQL.
>
>Ciò significa che è necessario assicurarsi che non siano disponibili dati sensibili, in quanto potrebbero essere divulgati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello di frammento di contenuto denominato `Article`, AEM genera l&#39;oggetto `article` di tipo `ArticleModel`. I campi all&#39;interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Un Modello Di Frammento Di Contenuto:

   ![Modello di frammento di contenuto da utilizzare con ](assets/cfm-graphqlapi-01.png "GraphQLComponente modello di frammento di contenuto per l&#39;utilizzo con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su ](assets/cfm-graphqlapi-02.png "modello di frammento di contenutoSchemaQL basato su modello di frammento di contenuto")

   Questo indica che il tipo generato `ArticleModel` contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall&#39;utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano utili metodi per fornire informazioni su un determinato frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Questi [campi helper](#helper-fields) sono contrassegnati con un `_` precedente per distinguere tra ciò che è stato definito dall&#39;utente e ciò che è stato generato automaticamente.

1. Dopo che un utente crea un frammento di contenuto basato sul modello Articolo, può essere interrogato tramite GraphQL. Ad esempio, vedere [Query di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (basate su una struttura di frammenti di contenuto di esempio da utilizzare con GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).[

In GraphQL per AEM, lo schema è flessibile. Questo significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si aggiorna un modello di frammento di contenuto.

Il servizio Sites GraphQL ascolta (in background) le modifiche apportate a un modello di frammento di contenuto. Quando vengono rilevati aggiornamenti, solo la parte dello schema viene rigenerata. Questa ottimizzazione consente di risparmiare tempo e stabilità.

Ad esempio, se:

1. Installare un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Verranno generati i tipi GraphQL per `Model-1` e `Model-2`.

1. Quindi modificare `Content-Fragment-Model-2`:

   1. Viene aggiornato solo il tipo `Model-2` GraphQL.

   1. Mentre `Model-1` rimarrà uguale.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui si desidera eseguire aggiornamenti in blocco sui modelli di frammenti di contenuto tramite l&#39;API REST, o in altro modo.

Lo schema viene distribuito attraverso lo stesso endpoint delle query GraphQL, con il client che gestisce il fatto che lo schema viene chiamato con l&#39;estensione `GQLschema`. Ad esempio, eseguendo una semplice richiesta `GET` su `/content/cq:graphql/global/endpoint.GQLschema` si ottiene l&#39;output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

## espandibili {#fields}

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati.

   Una selezione di [Tipi di campo](#field-types) viene utilizzata per creare campi in base alla modalità di configurazione del modello di frammento di contenuto. I nomi dei campi sono ricavati dal campo **Nome proprietà** del **Tipo di dati**.

   * È inoltre disponibile la proprietà **Rendering come**, in quanto gli utenti possono configurare alcuni tipi di dati; ad esempio, come testo a riga singola o multicampo.

* GraphQL per AEM genera anche un numero di [campi helper](#helper-fields).

   Questi vengono utilizzati per identificare un frammento di contenuto o per ottenere ulteriori informazioni su un frammento di contenuto.

### Tipi di campi {#field-types}

GraphQL per AEM supporta un elenco di tipi. Sono rappresentati tutti i tipi di dati supportati per i modelli di frammento di contenuto e i tipi di GraphQL corrispondenti:

| Modello frammento di contenuto - Tipo di dati | GraphQL Type | Descrizione |
|--- |--- |--- |
| Testo su riga singola | String, [String] |  Utilizzata per stringhe semplici come nomi di autore, nomi di posizione ecc. |
| Testo su più righe | Stringa |  Utilizzato per l&#39;output di testo, ad esempio il corpo di un articolo |
| Numero |  Mobile, [Mobile] | Utilizzato per visualizzare il numero a virgola mobile e i numeri regolari |
| Booleano |  Booleano |  Utilizzato per visualizzare le caselle di controllo → semplici istruzioni true/false |
| Data e ora | Calendario |  Utilizzato per visualizzare data e ora in formato ISO 8086 |
| Enumerazione |  Stringa |  Utilizzato per visualizzare un&#39;opzione da un elenco di opzioni definite durante la creazione del modello |
|  Tag |  [Stringa] |  Utilizzato per visualizzare un elenco di stringhe che rappresentano i tag utilizzati in AEM |
| Riferimento contenuto |  Stringa |  Utilizzato per visualizzare il percorso verso un&#39;altra risorsa in AEM |
| Riferimento frammento |  *Tipo di modello* |  Utilizzato per fare riferimento a un altro frammento di contenuto di un certo tipo di modello, definito al momento della creazione del modello |

### Campi helper {#helper-fields}

Oltre ai tipi di dati per i campi generati dall&#39;utente, GraphQL per AEM genera anche un numero di campi *helper* per facilitare l&#39;identificazione di un frammento di contenuto o per fornire ulteriori informazioni su un frammento di contenuto.

#### Percorso {#path}

Il campo percorso viene utilizzato come identificatore in GraphQL. Rappresenta il percorso della risorsa Frammento di contenuto all&#39;interno dell&#39;archivio AEM. È stato scelto come identificatore di un frammento di contenuto, in quanto:

* è univoco all&#39;interno di AEM,
* può essere facilmente recuperato.

Nel codice seguente vengono visualizzati i percorsi di tutti i frammenti di contenuto creati in base al modello di frammento di contenuto `Person`.

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

Vedere [Esempio di query - Un singolo frammento di città specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadati {#metadata}

Tramite GraphQL, AEM anche esporre i metadati di un frammento di contenuto. Per metadati si intendono le informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso delle miniature, la descrizione di un frammento di contenuto, la data di creazione, tra l’altro.

Poiché i metadati vengono generati tramite l&#39;Editor schema e in quanto tali non dispongono di una struttura specifica, il tipo `TypedMetaData` GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate dai seguenti tipi di scala:

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

Ogni tipo di scala rappresenta una coppia nome-valore singola o un array di coppie nome-valore, dove il valore di quella coppia è del tipo in cui è stata raggruppata.

Ad esempio, se desiderate recuperare il titolo di un frammento di contenuto, sappiamo che questa proprietà è una proprietà String, quindi eseguiamo una query per tutti i metadati stringa:

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

È possibile visualizzare tutti i tipi di metadati GraphQL se si visualizza lo schema Generated GraphQL. Tutti i tipi di modello hanno lo stesso `TypedMetaData`.

>[!NOTE]
>
>**Differenza tra metadati normali e metadati array**
>Tenere presente che `StringMetadata` e `StringArrayMetadata` si riferiscono entrambi a ciò che è memorizzato nella directory archivio, non a come viene recuperato.
>
>Ad esempio, chiamando il campo `stringMetadata` si riceverà un array di tutti i metadati memorizzati nell&#39;archivio come `String`, e se si chiama `stringArrayMetadata` si riceverà un array di tutti i metadati memorizzati nell&#39;archivio come `String[]`.

Consultate [Esempio di query per metadati - Elenco dei metadati per i premi denominati GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

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

Vedere [Esempio di query - Tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variabili GraphQL {#graphql-variables}

GraphQL consente di inserire le variabili nella query. Per ulteriori informazioni, consulta la documentazione di [GraphQL per GraphiQL](https://graphql.org/learn/queries/#variables).

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Article` con una specifica variante, è possibile specificare la variabile `variation` in GraphiQL.

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "VariablesGraphQL")

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

Ad esempio, è possibile includere il campo `adventurePrice` in una query per tutti i `AdventureModels`, in base a una variabile `includePrice`.

![GraphQL ](assets/cfm-graphqlapi-04.png "DirectivesGraphDirettive QL")

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

Potete inoltre utilizzare il filtro nelle query GraphQL per restituire dati specifici.

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

Per ulteriori esempi, vedete:

* dettagli di [GraphQL per AEM estensioni](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-extensions)

* [Query di esempio con questo contenuto e struttura di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E [Contenuto e struttura del campione](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparati per l&#39;uso nelle query di esempio

* [Query di esempio basate sul progetto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## Query persistenti (memorizzazione nella cache) {#persisted-queries-caching}

Dopo aver preparato una query con una richiesta di POST, può essere eseguita con una richiesta di GET che può essere memorizzata nella cache dalle cache HTTP o da una CDN.

Questo è richiesto perché le query POST in genere non sono memorizzate nella cache e se si utilizza GET con la query come parametro, esiste un rischio significativo che il parametro diventi troppo grande per i servizi HTTP e gli intermediari.

Di seguito sono riportati i passaggi necessari per mantenere una determinata query:

>[!NOTE]
>Prima di questo, è necessario abilitare le **Query di persistenza GraphQL** per la configurazione appropriata. Per ulteriori informazioni, vedere [Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).

1. Preparate la query inserendola nel nuovo URL dell&#39;endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Ad esempio, create una query persistente:

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

1. A questo punto, controllate la risposta.

   Ad esempio, verificate che l&#39;esito sia positivo:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Potete quindi riprodurre nuovamente la query persistente utilizzando GETing l&#39;URL `/graphql/execute.json/<shortPath>`.

   Ad esempio, utilizzate la query persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Aggiornare una query persistente tramite POSTing a un percorso di query già esistente.

   Ad esempio, utilizzate la query persistente:

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

1. Create una query normale con wrapping.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Create una query normale con wrapping con il controllo della cache.

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

   * Utilizzo di un pacchetto:
      1. Create una nuova definizione di pacchetto.
      1. Includete la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Create il pacchetto.
      1. Replicate il pacchetto.
   * Utilizzo dello strumento di replica/distribuzione.
      1. Passate allo strumento di distribuzione.
      1. Selezionate l&#39;attivazione della struttura per la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
   * Utilizzo di un flusso di lavoro (tramite la configurazione di avvio del flusso di lavoro):
      1. Definite una regola di avvio del flusso di lavoro per eseguire un modello di workflow che replichi la configurazione su eventi diversi (ad esempio, create, modificate, tra gli altri).



1. Una volta che la configurazione della query è stata pubblicata, si applicano gli stessi principi, utilizzando solo l&#39;endpoint di pubblicazione.

   >[!NOTE]
   >
   >Per l&#39;accesso anonimo, il sistema presuppone che l&#39;ACL consenta a &quot;tutti&quot; di accedere alla configurazione della query.
   >
   >In caso contrario, non potrà essere eseguito.

   >[!NOTE]
   >
   >Eventuali punti e virgola (&quot;;&quot;) negli URL devono essere codificati.
   >
   >Ad esempio, come nella richiesta per eseguire una query persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Query dell&#39;endpoint GraphQL da un sito Web esterno {#query-graphql-endpoint-from-external-website}

>[!NOTE]
>
>Per una panoramica dettagliata del criterio di condivisione delle risorse CORS, vedere [Comprendere la condivisione delle risorse tra le origini (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors)).

Per consentire a un sito Web di terze parti di utilizzare l&#39;output JSON, è necessario configurare un criterio CORS nell&#39;archivio Git del cliente. A questo scopo, aggiungete un file di configurazione OSGi CORS appropriato per l’endpoint desiderato. Questa configurazione deve specificare un nome di sito Web attendibile (regex) per il quale concedere l&#39;accesso.

* Accesso all’endpoint GraphQL:

   * alloworigin: [il vostro dominio] o alloworiginregexp: [il dominio regex]
   * metodi supportati: [POST]
   * Percorsi consentiti: [&quot;/content/graphql/global/endpoint.json&quot;]

* Accesso all&#39;endpoint di query persistenti GraphQL:

   * alloworigin: [il vostro dominio] o alloworiginregexp: [il dominio regex]
   * metodi supportati: [GET]
   * Percorsi consentiti: [&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>Resta responsabilità del cliente:
>
>* concedere solo l&#39;accesso ai domini trusted
>* assicurarsi che non siano esposte informazioni riservate
>* non utilizzare la sintassi con carattere jolly [*]; ciò disattiverà sia l&#39;accesso autenticato all&#39;endpoint GraphQL sia l&#39;esposizione al mondo intero.


>[!CAUTION]
>
>Tutti gli schemi GraphQL [](#schema-generation) (derivati da modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l&#39;endpoint GraphQL.
>
>Ciò significa che è necessario assicurarsi che non siano disponibili dati sensibili, in quanto potrebbero essere divulgati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

## Autenticazione {#authentication}

Vedere [Autenticazione per query AEM GraphQL remote su frammenti di contenuto](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Domande frequenti {#faqs}

Domande sorte:

1. **D**: &quot;*In che modo l&#39;API GraphQL per AEM è diversa dall&#39;API di Query Builder?*&quot;

   * **A**: &quot;*L&#39;API AEM GraphQL offre il controllo totale sull&#39;output JSON ed è uno standard di settore per l&#39;esecuzione di query sui contenuti.
In futuro, AEM intende investire nell&#39;API AEM GraphQL.*&quot;

## Esercitazione - Guida introduttiva a AEM headless e GraphQL {#tutorial}

Stai cercando un&#39;esercitazione pratica? Scoprite la [Guida introduttiva AEM headless e l&#39;esercitazione end-to-end di GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) che illustra come creare ed esporre contenuti utilizzando le API GraphQL di AEM e utilizzati da un&#39;app esterna, in uno scenario CMS headless.
