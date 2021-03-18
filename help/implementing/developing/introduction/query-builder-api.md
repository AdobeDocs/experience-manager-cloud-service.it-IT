---
title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un’API Java e un’API REST.
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# API Query Builder {#query-builder-api}

Query Builder offre un modo semplice per eseguire query sull’archivio dei contenuti di AEM. La funzionalità è esposta tramite un’API Java e un’API REST. Questo documento descrive queste API.

Il generatore di query lato server ([`QueryBuilder`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegue una query XPath, eventualmente filtra il set di risultati ed eventualmente estrae i facet.

La descrizione della query è semplicemente un set di predicati ([`Predicate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/Predicate.html)). Alcuni esempi includono un predicato full-text che corrisponde alla funzione `jcr:contains()` in XPath.

Per ogni tipo di predicato, esiste un componente valutatore ([`PredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) che sa come gestire quel predicato specifico per XPath, filtro ed estrazione del facet. È molto facile creare valutatori personalizzati, che sono collegati tramite il runtime del componente OSGi.

L’API REST consente di accedere esattamente alle stesse funzioni tramite HTTP e le risposte vengono inviate in JSON.

>[!NOTE]
>
>L’API QueryBuilder viene creata utilizzando l’API JCR. Puoi anche eseguire query sul JCR AEM utilizzando l&#39;API JCR da un bundle OSGi. Per informazioni, consulta [Query dei dati Adobe Experience Manager tramite l&#39;API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessione Gem {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis una serie di approfondimenti tecnici in Adobe Experience Manager forniti da esperti di Adobe.

Puoi [rivedere la sessione dedicata al generatore di query](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) per una panoramica e l&#39;utilizzo dello strumento.

## Query di esempio {#sample-queries}

Questi esempi sono forniti nella notazione dello stile delle proprietà Java. Per utilizzarli con l&#39;API Java, utilizza un Java `HashMap` come nell&#39;esempio API che segue.

Per il `QueryBuilder` Servlet JSON, ogni esempio include un collegamento di esempio a un’installazione AEM (nel percorso predefinito, `http://<host>:<port>`). Prima di utilizzare questi collegamenti, è necessario accedere all’istanza AEM.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet JSON del generatore di query visualizza un massimo di 10 hit.
>
>L’aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>`p.limit=-1`

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, potresti voler usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query **restituirà dieci risultati** (o per essere precisi un massimo di dieci), ma ti informa del **Numero di hit:** che sono effettivamente disponibili:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) restituirà tutti i risultati **(questo potrebbe essere un numero elevato a seconda dell&#39;istanza):**

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

Lo scopo del parametro `p.guessTotal` è quello di restituire il numero appropriato di risultati che possono essere mostrati combinando i valori minimi affidabili `p.offset` e `p.limit`. Il vantaggio di utilizzare questo parametro è il miglioramento delle prestazioni con grandi set di risultati. In questo modo si evita di calcolare l&#39;intero totale (ad esempio chiamando `result.getSize()`) e di leggere l&#39;intero set di risultati, ottimizzato fino al motore OAK e all&#39;indice. Questa può essere una differenza significativa quando ci sono centinaia di migliaia di risultati, sia in termini di tempo di esecuzione che di utilizzo della memoria.

Lo svantaggio del parametro è che gli utenti non vedono il totale esatto. Ma è possibile impostare un numero minimo come `p.guessTotal=1000` in modo che possa sempre leggere fino a 1000, in modo da ottenere i totali esatti per set di risultati più piccoli, ma se è più di questo, è solo possibile mostrare &quot;e più&quot;.

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

La query restituirà i risultati `p.limit` predefiniti di `10` con un offset `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

È inoltre possibile utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizza la stessa query di cui sopra, ma modifica il valore di `p.guessTotal` in `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Restituisce un numero con lo stesso limite predefinito di 10 risultati con un offset 0, ma visualizza solo un massimo di 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione impaginazione {#implementing-pagination}

Per impostazione predefinita, il Generatore di query fornisce anche il numero di hit. A seconda della dimensione del risultato, questo potrebbe richiedere molto tempo, in quanto la determinazione del conteggio accurato comporta il controllo di ogni risultato per il controllo degli accessi. Per lo più, il totale viene utilizzato per implementare l’impaginazione per l’interfaccia utente finale. Poiché la determinazione del conteggio esatto può essere lenta, si consiglia di utilizzare la funzione guessTotal per implementare l’impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottieni e visualizza il conteggio accurato del numero di hit totali ([SearchResult.getTotalMatches()](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) o totale nella risposta `querybuilder.json`) minori o uguali a 100;
* Imposta `guessTotal` su 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`,  `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati nella prima pagina e fornire l’impaginazione per le tre pagine successive. Puoi anche utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 results found&quot;**.
   * `total=100`,  `more=true` - Indica che il numero totale di hit è maggiore di 100 e che il conteggio esatto non è noto. L’interfaccia utente può visualizzare fino a dieci pagine come parte della prima pagina e fornire impaginazione per le dieci pagine successive. Puoi anche utilizzarlo per visualizzare un testo come **&quot;più di 100 risultati trovati&quot;**. Man mano che l’utente passa alle successive chiamate effettuate al Generatore di query, il limite di `guessTotal` e dei parametri `offset` e `limit` aumenta.

`guessTotal` Deve essere utilizzato anche nei casi in cui l’interfaccia utente deve utilizzare lo scorrimento infinito, per evitare che Query Builder determini l’esatto numero di hit.

### Trova i file jar e ordinali, il più recente {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Trova tutte le pagine e ordinale per ultima modifica {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Trova tutte le pagine e ordinale per ultima modifica, decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

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

### Cercare pagine con un determinato tag {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Utilizza il predicato `tagid` come nell&#39;esempio se conosci l&#39;ID tag esplicito.

Utilizza il predicato `tag` per il percorso del titolo del tag (senza spazi).

Poiché, nell’esempio precedente, stai cercando pagine (`cq:Page` nodi), devi utilizzare il percorso relativo da quel nodo per il predicato `tagid.property`, che è `jcr:content/cq:tags`. Per impostazione predefinita, il `tagid.property` è semplicemente `cq:tags`.

### Ricerca in più percorsi (utilizzando i gruppi) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Questa query utilizza un *gruppo* (denominato `group`) che agisce per delimitare le sottoespressioni all’interno di una query, come fanno le parentesi nelle notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

All’interno del gruppo nell’esempio, il predicato `path` viene utilizzato più volte. Per differenziare e ordinare le due istanze del predicato (l’ordinamento è necessario per alcuni predicati), è necessario impostare il prefisso dei predicati con `N_` dove `N` è l’indice di ordinamento. Nell’esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

Il `p` in `p.or` è un delimitatore speciale che indica che ciò che segue (in questo caso un `or`) è un *parametro* del gruppo, a differenza di un sottopredicato del gruppo, come `1_path`.

Se non viene fornito alcun `p.or`, tutti i predicati sono ANDed insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per predicati diversi.

### Cerca proprietà {#search-for-properties}

Qui stai cercando tutte le pagine di un dato modello, utilizzando la proprietà `cq:template` :

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Questo ha lo svantaggio che vengono restituiti i nodi `jcr:content` delle pagine, non le pagine stesse. Per risolvere questo problema, è possibile eseguire ricerche per percorso relativo:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Ricerca di più proprietà {#search-for-multiple-properties}

Quando si utilizza il predicato proprietà più volte, è necessario aggiungere di nuovo i prefissi numerici:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Ricerca di più valori di proprietà {#search-for-multiple-property-values}

Per evitare i grandi gruppi quando si desidera cercare più valori di una proprietà (`"A" or "B" or "C"`), è possibile fornire più valori al predicato `property`:

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

## Ottimizzazione dei risultati {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON di QueryBuilder restituisce un set predefinito di proprietà per ciascun nodo nel risultato della ricerca (ad esempio percorso, nome, titolo, ecc.). Per ottenere il controllo sulle proprietà restituite, è possibile effettuare una delle seguenti operazioni:

Specifica

```xml
p.hits=full
```

in tal caso tutte le proprietà verranno incluse per ogni nodo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Utilizzo

```xml
p.hits=selective
```

e specifica le proprietà che desideri inserire

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

Un’altra cosa che è possibile fare è includere nodi figlio nella risposta di Query Builder. Per eseguire questa operazione è necessario specificare

```xml
p.nodedepth=n
```

dove `n` è il numero di livelli che dovranno essere restituiti dalla query. Tieni presente che per restituire un nodo figlio, è necessario specificarlo dal selettore delle proprietà

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

Per ulteriori predicati, consulta la pagina [Riferimento predicato di Query Builder](query-builder-predicates.md).

È inoltre possibile controllare [Javadoc per le `PredicateEvaluator` classi](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc per queste classi contiene l&#39;elenco delle proprietà che è possibile utilizzare.

Il prefisso del nome della classe (ad esempio, `similar` in [`SimilarityPredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è la *proprietà principale* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in minuscolo).

Per tali proprietà principali, è possibile accorciare la query e utilizzare `similar=/content/en` invece della variante completa `similar.similar=/content/en`. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

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

La stessa query eseguita su HTTP utilizzando il servlet Query Builder (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento delle query {#storing-and-loading-queries}

Le query possono essere archiviate nell’archivio in modo da poterle utilizzare in un secondo momento. Il metodo `QueryBuilder` fornisce il metodo `storeQuery` con la seguente firma:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza il metodo [`QueryBuilder#storeQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-), il valore specificato `Query` viene memorizzato nell’archivio come file o come proprietà in base al valore dell’argomento `createFile`. L&#39;esempio seguente mostra come salvare un `Query` nel percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Qualsiasi query precedentemente archiviata può essere caricata dall&#39;archivio utilizzando il metodo [`QueryBuilder#loadQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` memorizzato nel percorso `/mypath/getfiles` può essere caricato dal seguente frammento:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per riprodurre e eseguire il debug delle query di Query Builder, puoi utilizzare la console di debug di Query Builder in

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

o in alternativa il servlet JSON di Query Builder all’indirizzo

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` è solo un esempio.

### Debug generale di Recommendations {#general-debugging-recommendations}

### Ottieni XPath spiegabile tramite Logging {#obtain-explain-able-xpath-via-logging}

Spiegare le query **all** durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

1. Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile
   * Accedi a `https://<host>:<port>/system/console/slinglog`. Crea un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.
1. Una volta abilitato DEBUG per la classe di cui sopra, i registri visualizzeranno l&#39;XPath generato da Query Builder.
1. Copia la query XPath dalla voce di registro per la query Query Builder associata, ad esempio:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Incolla la query XPath in Explain Query as XPath per ottenere il piano di query.

### Ottieni XPath spiegabile tramite il debugger di Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilizza il debugger di Query Builder AEM per generare una query XPath spiegabile.

![Debugger di Query Builder](assets/query-builder-debugger.png)

1. Fornire la query Query Builder nel debugger di Query Builder
1. Esegui la ricerca
1. Ottieni l&#39;XPath generato
1. Incolla la query XPath in Explain Query as XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non Query Builder (XPath, JCR-SQL2) possono essere fornite direttamente a Explain Query.

## Debug delle query con registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nel documento [Logging](/help/implementing/developing/introduction/logging.md).

L&#39;output di log (livello INFO) dell&#39;implementazione del generatore di query durante l&#39;esecuzione della query descritta nella sezione precedente [Test e debug:](#testing-and-debugging)

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

Se disponi di una query che utilizza valutatori predicati che filtrano o utilizzano un ordine personalizzato per comparatore, questa operazione verrà rilevata anche nella query:

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
| [com.day.cq.search](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/package-summary.html) | API Query Builder di base e query |
| [com.day.cq.search.result](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bukets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Punti (contenuti nei facet) |
| [com.day.cq.search.eval](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/package-summary.html) | Valutatori del predicato |
| [com.day.cq.search.facets.extractor](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori di sfaccettature (per valutatori) |
| [com.day.cq.search.writer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/writer/package-summary.html) | Scrittore di hit dei risultati JSON per il servlet di Query Builder (`/bin/querybuilder.json`) |
