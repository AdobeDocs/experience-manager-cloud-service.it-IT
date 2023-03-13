---
title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un’API Java e un’API REST.
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---

# API Query Builder {#query-builder-api}

Query Builder offre un modo semplice per eseguire query sull’archivio dei contenuti dell’AEM. La funzionalità è esposta tramite un’API Java e un’API REST. Questo documento descrive queste API.

Generatore di query lato server ([`QueryBuilder`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html)) accetterà una descrizione della query, creerà ed eseguirà una query XPath, facoltativamente filtrerà il set di risultati e, se necessario, estrarrà i facet.

La descrizione della query è semplicemente un set di predicati ([`Predicate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html)). Gli esempi includono un predicato full-text, che corrisponde al `jcr:contains()` funzione in XPath.

Per ogni tipo di predicato, è disponibile un componente valutatore ([`PredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) che sa come gestire il predicato specifico per XPath, il filtro e l&#39;estrazione facet. È molto semplice creare valutatori personalizzati, collegati tramite il runtime del componente OSGi.

L’API REST consente di accedere esattamente alle stesse funzioni tramite HTTP, con risposte inviate in JSON.

>[!NOTE]
>
>L’API QueryBuilder viene creata utilizzando l’API JCR. Puoi anche eseguire query sul JCR dell’AEM utilizzando l’API JCR all’interno di un bundle OSGi. Per informazioni, consulta [Query dei dati di Adobe Experience Manager tramite l’API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessione Gem {#gem-session}

[AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) è una serie di approfondimenti tecnici su Adobe Experience Manager forniti da esperti Adobi.

È possibile [rivedi la sessione dedicata al generatore di query](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) per una panoramica e l’utilizzo dello strumento.

## Query di esempio {#sample-queries}

Questi esempi sono forniti nella notazione di stile delle proprietà Java. Per utilizzarli con l’API Java, utilizza un’interfaccia Java `HashMap` come nell’esempio di API che segue.

Per `QueryBuilder` Servlet JSON, ogni esempio include un collegamento di esempio a un’installazione AEM (nella posizione predefinita, `http://<host>:<port>`). Tieni presente che devi accedere all’istanza AEM prima di utilizzare questi collegamenti.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet JSON del generatore di query visualizza un massimo di 10 hit.
>
>L’aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>`p.limit=-1`

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, è possibile utilizzare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query **restituisce dieci risultati** (o per essere precisi un massimo di dieci), ma informarti del **Numero di hit:** effettivamente disponibili:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) si **restituisce tutti i risultati** (numero elevato a seconda dell’istanza):

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

Scopo della `p.guessTotal` parametro è quello di restituire il numero appropriato di risultati che possono essere mostrati combinando la soglia minima `p.offset` e `p.limit` valori. L&#39;utilizzo di questo parametro offre il vantaggio di migliorare le prestazioni con set di risultati di grandi dimensioni. In questo modo si evita di calcolare il totale completo (ad es. chiamando `result.getSize()`) e la lettura dell&#39;intero set di risultati, ottimizzati fino al motore e all&#39;indice OAK. Questa può essere una differenza significativa quando ci sono centinaia di migliaia di risultati, sia nel tempo di esecuzione che nell&#39;utilizzo della memoria.

Lo svantaggio del parametro è che gli utenti non vedono il totale esatto. Ma puoi impostare un numero minimo come `p.guessTotal=1000` quindi può sempre leggere fino a 1000, in modo da ottenere totali esatti per set di risultati più piccoli, ma se è più di questo, puoi mostrare solo &quot;e altro&quot;.

Aggiungi `p.guessTotal=true` alla query seguente per vedere come funziona:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

La query restituirà il `p.limit` valore predefinito di `10` risultati con un `0` offset:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Puoi anche utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizza la stessa query di cui sopra, ma modifica il valore di `p.guessTotal` a `50`:

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

Per impostazione predefinita, Query Builder fornisce anche il numero di hit. A seconda della dimensione del risultato, l’operazione potrebbe richiedere molto tempo, poiché per determinare il conteggio accurato è necessario verificare ogni risultato per il controllo degli accessi. La maggior parte del totale viene utilizzata per implementare la paginazione per l’interfaccia utente dell’utente finale. Poiché la determinazione del conteggio esatto può essere lenta, si consiglia di utilizzare la funzione guessTotal per implementare l’impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottieni e visualizza il conteggio accurato del numero di hit totali ([SearchResult.getTotalMatches()](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) o totale nel `querybuilder.json` risposta) sono inferiori o pari a 100;
* Imposta `guessTotal` a 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`, `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati come parte della prima pagina e fornire l’impaginazione per le tre pagine successive. Puoi inoltre utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 risultati trovati&quot;**.
   * `total=100`, `more=true` - Indica che il numero totale di hit è maggiore di 100 e il conteggio esatto non è noto. L’interfaccia utente può visualizzare fino a dieci pagine come parte della prima pagina e fornire l’impaginazione per le dieci pagine successive. Puoi anche utilizzarlo per visualizzare un testo come **&quot;trovati più di 100 risultati&quot;**. Quando l’utente passa alle pagine successive, le chiamate effettuate al Query Builder aumentano il limite di `guessTotal` e anche del `offset` e `limit` parametri.

`guessTotal` deve essere utilizzato anche nei casi in cui l’interfaccia utente deve utilizzare uno scorrimento infinito, al fine di evitare che Query Builder determini il conteggio esatto degli hit.

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

Utilizza il `tagid` predicato come nell’esempio, se conosci l’ID tag esplicito.

Utilizza il `tag` predicato per il percorso del titolo del tag (senza spazi).

Perché nell&#39;esempio precedente si stanno cercando le pagine (`cq:Page` ), è necessario utilizzare il percorso relativo di tale nodo per `tagid.property` predicato, che è `jcr:content/cq:tags`. Per impostazione predefinita, il `tagid.property` sarebbe semplicemente `cq:tags`.

### Ricerca di più percorsi (utilizzando i gruppi) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Questa query utilizza un *gruppo* (denominato `group`), che agisce per delimitare le sottoespressioni all’interno di una query, proprio come fanno le parentesi nelle notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

All&#39;interno del gruppo nell&#39;esempio, il `path` Il predicato viene utilizzato più volte. Per differenziare e ordinare le due istanze del predicato (per alcuni predicati è necessario ordinare), è necessario anteporre ai predicati il prefisso `N_` dove `N` è l’indice di ordinamento. Nell’esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

Il `p` in `p.or` è un delimitatore speciale che indica che quanto segue (in questo caso un `or`) è un *parametro* del gruppo, anziché un subpredicato del gruppo, ad esempio `1_path`.

In caso negativo `p.or` è dato allora tutti i predicati sono AND insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per predicati diversi.

### Cerca proprietà {#search-for-properties}

Qui si stanno cercando tutte le pagine di un dato modello, utilizzando `cq:template` proprietà:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Questo ha lo svantaggio che il `jcr:content` vengono restituiti i nodi delle pagine, non le pagine stesse. Per risolvere questo problema, puoi eseguire ricerche per percorso relativo:

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

Per evitare gruppi numerosi quando si desidera cercare più valori di una proprietà (`"A" or "B" or "C"`), è possibile fornire più valori al `property` predicato:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

Per le proprietà con più valori, puoi anche richiedere che più valori corrispondano (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Ottimizzazione di ciò che viene restituito {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON QueryBuilder restituisce un set predefinito di proprietà per ciascun nodo del risultato della ricerca (ad esempio, percorso, nome, titolo e così via). Per controllare quali proprietà vengono restituite, è possibile effettuare una delle seguenti operazioni:

Specifica

```xml
p.hits=full
```

in questo caso, tutte le proprietà verranno incluse per ciascun nodo:

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

e specificare le proprietà che si desidera ottenere

```xml
p.properties
```

separati da uno spazio:

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

È inoltre possibile includere nodi figlio nella risposta di Query Builder. A questo scopo è necessario specificare

```xml
p.nodedepth=n
```

dove `n` è il numero di livelli che la query deve restituire. Per restituire un nodo figlio, è necessario specificarlo con il selettore delle proprietà

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

Per ulteriori predicati, vedere [Pagina Riferimento predicato di Query Builder](query-builder-predicates.md).

È inoltre possibile controllare [JavaScript per `PredicateEvaluator` classi](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Il codice Javadoc per queste classi contiene l’elenco delle proprietà che puoi utilizzare.

Il prefisso del nome della classe (ad esempio, `similar` in [`SimilarityPredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è il *proprietà principale* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in minuscolo).

Per tali proprietà principali, puoi abbreviare la query e utilizzare `similar=/content/en` invece della variante completamente qualificata `similar.similar=/content/en`. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

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

Le query possono essere archiviate nel repository in modo da poterle utilizzare in un secondo momento. Il `QueryBuilder` fornisce `storeQuery` metodo con la firma seguente:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza [`QueryBuilder#storeQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) metodo, il valore specificato `Query` viene memorizzato nel repository come file o come proprietà in base al `createFile` valore argomento. L’esempio seguente mostra come salvare un `Query` al percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Tutte le query memorizzate in precedenza possono essere caricate dall’archivio utilizzando [`QueryBuilder#loadQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) metodo:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` memorizzato nel percorso `/mypath/getfiles` può essere caricato dal seguente snippet:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per eseguire il gioco e il debug delle query di Query Builder, puoi utilizzare la console del debugger di Query Builder all’indirizzo

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

o in alternativa il servlet JSON di Query Builder in

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` è solo un esempio.

### Debug generale di Recommendations {#general-debugging-recommendations}

### Ottenere XPath spiegabile tramite la registrazione {#obtain-explain-able-xpath-via-logging}

Spiega **tutto** query durante il ciclo di sviluppo rispetto al set di indici di destinazione.

1. Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile
   * Accedi a `https://<host>:<port>/system/console/slinglog`. Crea un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` a **DEBUG**.
1. Una volta abilitato DEBUG per la classe precedente, nei registri verrà visualizzato l&#39;XPath generato da Query Builder.
1. Copiare la query XPath dalla voce di registro per la query Query Builder associata, ad esempio:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Incollare la query XPath in Explain Query come XPath per ottenere il piano di query.

### Ottenere XPath spiegabile tramite Query Builder Debugger {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilizza il debugger di AEM Query Builder per generare una query XPath spiegabile.

![Debugger di Query Builder](assets/query-builder-debugger.png)

1. Fornisci la query di Query Builder nel debugger di Query Builder
1. Eseguire la ricerca
1. Ottenere l&#39;XPath generato
1. Incollare la query XPath in Explain Query come XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non Query Builder (XPath, JCR-SQL2) possono essere fornite direttamente in Explain Query.

## Eseguire il debug delle query con la registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nel documento [Registrazione](/help/implementing/developing/introduction/logging.md).

L’output del registro (livello INFO) dell’implementazione del generatore di query durante l’esecuzione della query descritta nella sezione precedente [Test e debug:](#testing-and-debugging)

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

Se una query utilizza valutatori di predicati che filtrano o che utilizzano un ordine personalizzato per comparatore, nella query verrà annotato anche quanto segue:

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
| [com.day.cq.search](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | Generatore di query di base e API di query |
| [com.day.cq.search.result](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bucket](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Bucket (contenuti all’interno di facet) |
| [com.day.cq.search.eval](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | Valutatori predicato |
| [com.day.cq.search.facets.extractors](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori sfaccettatura (per valutatori) |
| [com.day.cq.search.writer](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | Hit writer di risultati JSON per il servlet Query Builder (`/bin/querybuilder.json`) |
