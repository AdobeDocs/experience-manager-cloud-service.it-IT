---
title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un'API Java&trade; e un'API REST.
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---

# API Query Builder {#query-builder-api}

Query Builder offre un modo semplice per eseguire query sull’archivio dei contenuti di AEM. La funzionalità è esposta tramite un’API Java™ e un’API REST. Questo documento descrive queste API.

Il generatore di query lato server ([`QueryBuilder`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegui una query XPath, facoltativamente filtra il set di risultati ed estrae i facet, se necessario.

La descrizione della query è semplicemente un set di predicati ([`Predicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html)). Gli esempi includono un predicato full-text, che corrisponde alla funzione `jcr:contains()` in XPath.

Per ogni tipo di predicato, esiste un componente valutatore ([`PredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) che sa come gestire il predicato specifico per XPath, il filtro e l&#39;estrazione facet. È facile creare valutatori personalizzati, che sono collegati tramite il runtime del componente OSGi.

L’API REST consente di accedere alle stesse funzioni tramite HTTP con risposte inviate in JSON.

>[!NOTE]
>
>L’API QueryBuilder viene creata utilizzando l’API JCR. Puoi anche eseguire query sul JCR di AEM utilizzando l’API JCR all’interno di un bundle OSGi. Per informazioni, vedere [Query dei dati Adobe Experience Manager tramite l&#39;API JCR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/query-builder/querybuilder-api.html?lang=it).

## Sessione Gem {#gem-session}

[AEM Gems](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=it) è una serie di approfondimenti tecnici su Adobe Experience Manager forniti da esperti Adobe.

Puoi [rivedere la sessione dedicata al generatore di query](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-search-forms-using-querybuilder.html?lang=it) per una panoramica e l&#39;utilizzo dello strumento.

## Query di esempio {#sample-queries}

Questi esempi sono forniti nella notazione di stile delle proprietà Java™. Per utilizzarli con l&#39;API Java™, utilizzare un Java™ `HashMap` come nell&#39;esempio di API seguente.

Per il servlet JSON `QueryBuilder`, ogni esempio include un collegamento di esempio a un&#39;installazione di AEM (nel percorso predefinito, `http://<host>:<port>`). Accedi all’istanza di AEM prima di utilizzare questi collegamenti.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet JSON del generatore di query visualizza un massimo di dieci hit.
>
>L’aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>`p.limit=-1`

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, puoi usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query **restituisce dieci risultati** (o, per essere precisi, un massimo di dieci), ma ti informa del **numero di hit:** disponibile:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) **restituisce tutti i risultati** (potrebbe essere un numero elevato a seconda dell&#39;istanza):

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilizzo di p.guessTotal per restituire i risultati {#using-p-guesstotal-to-return-the-results}

Lo scopo del parametro `p.guessTotal` è restituire il numero appropriato di risultati che possono essere visualizzati combinando i valori minimi validi `p.offset` e `p.limit`. L&#39;utilizzo di questo parametro offre il vantaggio di migliorare le prestazioni con set di risultati di grandi dimensioni. Questo parametro evita inoltre di calcolare il totale completo (ad esempio, chiamando `result.getSize()`) e di leggere l&#39;intero set di risultati, ottimizzato fino al motore e all&#39;indice di Oak. Questo processo può rappresentare una differenza significativa quando si ottengono centinaia di migliaia di risultati, sia in termini di tempo di esecuzione che di utilizzo della memoria.

Lo svantaggio del parametro è che gli utenti non vedono il totale esatto. È tuttavia possibile impostare un numero minimo come `p.guessTotal=1000` in modo che venga sempre letto fino a 1000. In questo modo, si ottengono totali esatti per set di risultati più piccoli, ma se è di più, è possibile mostrare solo &quot;e altro&quot;.

Aggiungi `p.guessTotal=true` alla query per vedere come funziona:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

La query restituisce il valore predefinito `p.limit` di `10` risultati con un offset `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Puoi anche utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizzare la stessa query di cui sopra, ma modificare il valore di `p.guessTotal` in `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Restituisce un numero con lo stesso limite predefinito di 10 risultati con un offset pari a 0, ma visualizza solo un massimo di 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione della paginazione {#implementing-pagination}

Per impostazione predefinita, Query Builder fornisce anche il numero di hit. A seconda della dimensione del risultato, questo numero potrebbe richiedere molto tempo, poiché per determinare il conteggio accurato è necessario verificare ogni risultato per il controllo degli accessi. La maggior parte del totale viene utilizzata per implementare la paginazione per l’interfaccia utente dell’utente finale. Poiché la determinazione del conteggio esatto può essere lenta, si consiglia di utilizzare la funzione guessTotal per implementare l’impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottieni e visualizza il conteggio accurato del numero di hit totali ([SearchResult.getTotalMatches()](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) o totali nella risposta `querybuilder.json`) minori o uguali a 100;
* Impostare `guessTotal` su 100 per chiamare il Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`, `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati come parte della prima pagina e fornire l’impaginazione per le tre pagine successive. È inoltre possibile utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 risultati trovati&quot;**.
   * `total=100`, `more=true` - Indica che il numero totale di hit è maggiore di 100 e il conteggio esatto non è noto. L’interfaccia utente può visualizzare fino a dieci pagine come parte della prima pagina e fornire l’impaginazione per le dieci pagine successive. È inoltre possibile utilizzare questa funzionalità per visualizzare un testo come **&quot;sono stati trovati più di 100 risultati&quot;**. Quando l&#39;utente passa alle pagine successive, le chiamate effettuate al Generatore di query aumentano il limite di `guessTotal` e anche dei parametri `offset` e `limit`.

Inoltre, utilizza `guessTotal` nei casi in cui l&#39;interfaccia utente deve utilizzare lo scorrimento infinito per evitare che il Generatore di query determini il conteggio esatto degli hit.

### Trova i file jar e ordinali, a partire dal più recente {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Trova tutte le pagine e ordina per ultima modifica {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Trova tutte le pagine e ordina per ultima modifica, decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Ricerca full-text, ordinata per punteggio {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Cerca le pagine con un determinato tag {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Utilizza il predicato `tagid` come nell&#39;esempio se conosci l&#39;ID tag esplicito.

Utilizza il predicato `tag` per il percorso del titolo del tag (senza spazi).

Nell&#39;esempio precedente, poiché si stanno cercando pagine (`cq:Page` nodi), utilizzare il percorso relativo di tale nodo per il predicato `tagid.property`, ovvero `jcr:content/cq:tags`. Per impostazione predefinita, `tagid.property` è `cq:tags`.

### Ricerca di più percorsi (utilizzando i gruppi) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Questa query utilizza un *gruppo* (denominato `group`), che agisce per delimitare le sottoespressioni all&#39;interno di una query, proprio come fanno le parentesi nelle notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

All&#39;interno del gruppo nell&#39;esempio, il predicato `path` viene utilizzato più volte. Per differenziare e ordinare le due istanze del predicato (per alcuni predicati è richiesto l&#39;ordinamento), è necessario anteporre ai predicati il prefisso `N_`, dove `N` è l&#39;indice dell&#39;ordinamento. Nell&#39;esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

`p` in `p.or` è un delimitatore speciale che indica che il seguente (in questo caso un `or`) è un *parametro* del gruppo, anziché un subpredicato del gruppo, ad esempio `1_path`.

Se non viene fornito alcun `p.or`, tutti i predicati vengono AND insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per predicati diversi.

### Cerca proprietà {#search-for-properties}

Qui si stanno cercando tutte le pagine di un dato modello, utilizzando la proprietà `cq:template`:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Lo svantaggio è che vengono restituiti i nodi `jcr:content` delle pagine, non le pagine stesse. Per risolvere questo problema, è possibile eseguire una ricerca per percorso relativo:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Cerca più proprietà {#search-for-multiple-properties}

Quando utilizzi più volte il predicato proprietà, devi aggiungere nuovamente i prefissi numerici:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Ricerca di più valori di proprietà {#search-for-multiple-property-values}

Per evitare gruppi di grandi dimensioni quando si desidera cercare più valori di una proprietà (`"A" or "B" or "C"`), è possibile fornire più valori al predicato `property`:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

Per le proprietà con più valori, è inoltre possibile richiedere che più valori corrispondano (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Ottimizzazione di ciò che viene restituito {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON QueryBuilder restituisce un insieme predefinito di proprietà per ogni nodo del risultato della ricerca (ad esempio, percorso, nome e titolo). Per ottenere il controllo sulle proprietà restituite, effettuare una delle seguenti operazioni:

Specifica

```xml
p.hits=full
```

In questo caso, tutte le proprietà sono incluse per ciascun nodo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Utilizzare

```xml
p.hits=selective
```

E specifica le proprietà che desideri inserire

```xml
p.properties
```

Separato da uno spazio:

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

È inoltre possibile includere nodi figlio nella risposta di Query Builder. Specifica

```xml
p.nodedepth=n
```

Dove `n` è il numero di livelli che si desidera vengano restituiti dalla query. Per restituire un nodo figlio, è necessario specificarlo con il selettore delle proprietà

```xml
p.hits=full
```

Esempio:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## Altri predicati {#morepredicates}

Per ulteriori predicati, vedere la [pagina di riferimento del predicato di Query Builder](query-builder-predicates.md).

Puoi anche controllare [Javadoc per le `PredicateEvaluator` classi](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Il codice Javadoc per queste classi contiene l’elenco delle proprietà che puoi utilizzare.

Il prefisso del nome della classe (ad esempio, `similar` in [`SimilarityPredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è la *proprietà entità* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in minuscolo).

Per tali proprietà di entità, è possibile ridurre la query e utilizzare `similar=/content/en` invece della variante completa `similar.similar=/content/en`. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

## Esempio di utilizzo API di Query Builder {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

La stessa query viene eseguita su HTTP utilizzando il servlet Query Builder (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento delle query {#storing-and-loading-queries}

Le query possono essere archiviate nel repository in modo da poterle utilizzare in un secondo momento. `QueryBuilder` fornisce al metodo `storeQuery` la firma seguente:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza il metodo [`QueryBuilder#storeQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-), l&#39;elemento `Query` specificato viene archiviato nel repository come file o come proprietà in base al valore dell&#39;argomento `createFile`. Nell&#39;esempio seguente viene illustrato come salvare un `Query` nel percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Tutte le query archiviate in precedenza possono essere caricate dal repository utilizzando il metodo [`QueryBuilder#loadQuery`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` archiviato nel percorso `/mypath/getfiles` può essere caricato dal seguente snippet:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per eseguire il gioco e il debug delle query di Query Builder, puoi utilizzare la console del debugger di Query Builder all’indirizzo

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

In alternativa, il servlet JSON di Query Builder in

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` è solo un esempio.

### Consigli generali sul debug {#general-debugging-recommendations}

### Ottenere XPath spiegabile tramite la registrazione {#obtain-explain-able-xpath-via-logging}

Spiega **tutte** le query durante il ciclo di sviluppo rispetto al set di indici di destinazione.

1. Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile
   * Passa a `https://<host>:<port>/system/console/slinglog`. Crea un logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.
1. Dopo aver abilitato DEBUG per la classe precedente, nei registri viene visualizzato l&#39;XPath generato da Query Builder.
1. Copiare la query XPath dalla voce di registro per la query Query Builder associata, ad esempio:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Incollare la query XPath in Explain Query come XPath in modo da ottenere il piano di query.

### Ottenere XPath spiegabile tramite Query Builder Debugger {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilizza il debugger di AEM Query Builder per generare una query XPath spiegabile.

![Debugger di Query Builder](assets/query-builder-debugger.png)

1. Fornisci la query di Query Builder nel debugger di Query Builder
1. Eseguire la ricerca
1. Ottenere l&#39;XPath generato
1. Incollare la query XPath in Explain Query come XPath in modo da ottenere il piano di query

>[!NOTE]
>
>Le query non di Query Builder (XPath, JCR-SQL2) possono essere fornite direttamente in Explain Query.

## Eseguire il debug delle query con la registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nel documento [Registrazione](/help/implementing/developing/introduction/logging.md).

L&#39;output del log (livello INFO) dell&#39;implementazione del generatore di query durante l&#39;esecuzione della query descritta nella sezione precedente [Test e debug](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Se si dispone di una query che utilizza i valutatori dei predicati che filtrano o che utilizzano un ordine personalizzato tramite il comparatore, la query riporta quanto segue:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Collegamenti Javadoc {#javadoc-links}

| **Javadoc** | **Descrizione** |
|---|---|
| [com.day.cq.search](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | Generatore di query di base e API di query |
| [com.day.cq.search.result](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bucket](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Bucket (contenuti all’interno di facet) |
| [com.day.cq.search.eval](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | Valutatori predicato |
| [com.day.cq.search.facets.extractors](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori sfaccettatura (per valutatori) |
| [com.day.cq.search.writer](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | Hit writer risultati JSON per il servlet Query Builder (`/bin/querybuilder.json`) |
