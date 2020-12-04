---
title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un'API Java e un'API REST.
translation-type: tm+mt
source-git-commit: cfd54f0cd84cef72b6f2fad1a85132c312a19348
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# API Query Builder {#query-builder-api}

Query Builder offre un modo semplice per interrogare l&#39;archivio dei contenuti di AEM. La funzionalità è esposta tramite un&#39;API Java e un&#39;API REST. Questo documento descrive queste API.

Il generatore di query lato server ([`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegue una query XPath, eventualmente applica un filtro al set di risultati e, se necessario, estrae anche i facet.

La descrizione della query è semplicemente un insieme di predicati ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Alcuni esempi includono un predicato full-text, che corrisponde alla funzione `jcr:contains()` in XPath.

Per ciascun tipo di predicato, è presente un componente valutatore ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) in grado di gestire tale predicato specifico per XPath, filtraggio ed estrazione dei facet. È molto facile creare valutatori personalizzati, che vengono collegati tramite il runtime dei componenti OSGi.

L&#39;API REST fornisce l&#39;accesso esattamente alle stesse funzionalità tramite HTTP, con le risposte inviate in JSON.

>[!NOTE]
>
>L&#39;API QueryBuilder viene creata utilizzando l&#39;API JCR. Potete anche eseguire una query sul JCR AEM utilizzando l&#39;API JCR da un bundle OSGi. Per informazioni, vedere [Query dei dati Adobe Experience Manager tramite l&#39;API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessione Gem {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis una serie di approfondimenti tecnici in Adobe Experience Manager forniti da  esperti Adobe.

È possibile [rivedere la sessione dedicata al generatore di query](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) per una panoramica e l&#39;utilizzo dello strumento.

## Query di esempio {#sample-queries}

Questi esempi sono riportati nella notazione dello stile delle proprietà Java. Per utilizzarli con l&#39;API Java, utilizzate Java `HashMap` come nell&#39;esempio di API che segue.

Per il Servlet `QueryBuilder` JSON, ogni esempio include un collegamento di esempio a un&#39;installazione AEM (nel percorso predefinito, `http://<host>:<port>`). Prima di usare questi collegamenti è necessario accedere all&#39;istanza AEM.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet JSON del generatore di query visualizza un massimo di 10 hit.
>
>L&#39;aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>`p.limit=-1`

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, potresti voler usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query restituisce **dieci risultati** (o per essere precisi, un massimo di dieci), ma vi informa del **Numero di hit:** effettivamente disponibili:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) restituirà tutti i risultati **(a seconda dell&#39;istanza potrebbe essere un numero elevato):**

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilizzo di p.impressionTotal per restituire i risultati {#using-p-guesstotal-to-return-the-results}

Lo scopo del parametro `p.guessTotal` è quello di restituire il numero appropriato di risultati che possono essere mostrati combinando i valori minimi vitali `p.offset` e `p.limit`. Il vantaggio di utilizzare questo parametro è rappresentato da prestazioni migliori con set di risultati di grandi dimensioni. In questo modo si evita di calcolare il totale totale (ad es. `result.getSize()`) e di leggere l&#39;intero set di risultati, ottimizzato fino al motore OAK e all&#39;indice. Questa differenza può essere significativa in presenza di centinaia di migliaia di risultati, sia in termini di tempo di esecuzione che di utilizzo della memoria.

Lo svantaggio per il parametro è che gli utenti non vedono il totale esatto. È tuttavia possibile impostare un numero minimo come `p.guessTotal=1000` in modo che possa sempre leggere fino a 1000, quindi si ottengono i totali esatti per i set di risultati più piccoli, ma se è più di questo, è possibile solo mostrare &quot;e più&quot;.

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

La query restituirà il valore predefinito `p.limit` di `10` risultati con un offset `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

È inoltre possibile utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizzate la stessa query di cui sopra, ma modificate il valore di `p.guessTotal` in `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Verrà restituito un numero con lo stesso limite predefinito di 10 risultati con un offset pari a 0, ma verranno visualizzati solo 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione impaginazione {#implementing-pagination}

Per impostazione predefinita, Query Builder fornisce anche il numero di hit. A seconda della dimensione del risultato, questo potrebbe richiedere molto tempo, poiché per determinare il conteggio accurato è necessario controllare ogni risultato per il controllo dell&#39;accesso. La maggior parte del totale viene utilizzata per implementare l&#39;impaginazione per l&#39;interfaccia utente finale. Poiché determinare il conteggio esatto può essere lento, si consiglia di utilizzare la funzione approssimativaTotale per implementare l&#39;impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottenere e visualizzare il conteggio accurato del numero totale di hit ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) o totale nella `querybuilder.json` risposta) è minore o uguale a 100;
* Impostate `guessTotal` su 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`,  `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati nella prima pagina e fornire impaginazione per le tre pagine successive. Potete inoltre utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 Results found&quot;**.
   * `total=100`,  `more=true` - Indica che il numero totale di hit è maggiore di 100 e che il conteggio esatto non è noto. L’interfaccia utente può essere visualizzata fino a dieci nella prima pagina e fornire impaginazione per le dieci pagine successive. È inoltre possibile utilizzare questa opzione per visualizzare un testo come **&quot;oltre 100 risultati trovati&quot;**. Man mano che l&#39;utente passa alle pagine successive, le chiamate effettuate al Generatore di query aumentano il limite di `guessTotal` e anche dei parametri `offset` e `limit`.

`guessTotal` dovrebbe essere utilizzato anche nei casi in cui l&#39;interfaccia utente deve utilizzare lo scorrimento infinito, per evitare che il Generatore di query determini l&#39;esatto numero di hit.

### Trova file Jar e ordinali, il più recente {#find-jar-files-and-order-them-newest-first}

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

### Cerca pagine con un determinato tag {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Utilizzate il predicato `tagid` come nell&#39;esempio, se conoscete l&#39;ID di tag esplicito.

Utilizzate il predicato `tag` per il percorso del titolo del tag (senza spazi).

Poiché, nell&#39;esempio precedente, si stanno cercando pagine (`cq:Page` nodi), è necessario utilizzare il percorso relativo da tale nodo per il predicato `tagid.property`, che è `jcr:content/cq:tags`. Per impostazione predefinita, il `tagid.property` è semplicemente `cq:tags`.

### Cerca più percorsi (tramite gruppi) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Questa query utilizza un *gruppo* (denominato `group`) che agisce per delimitare le sottoespressioni all&#39;interno di una query, come accade per le parentesi in notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

All&#39;interno del gruppo nell&#39;esempio, il predicato `path` viene utilizzato più volte. Per distinguere e ordinare le due istanze del predicato (l&#39;ordine è richiesto per alcuni predicati), è necessario preimpostare i predicati con `N_` dove `N` è l&#39;indice di ordinamento. Nell&#39;esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

`p` in `p.or` è un delimitatore speciale che indica che ciò che segue (in questo caso un `or`) è un *parametro* del gruppo, a differenza di un subpredicato del gruppo, come `1_path`.

Se non viene fornito alcun valore `p.or`, tutti i predicati vengono inseriti insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per diversi predicati.

### Cerca proprietà {#search-for-properties}

Qui state cercando tutte le pagine di un dato modello, utilizzando la proprietà `cq:template`:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Questo ha lo svantaggio di restituire i nodi `jcr:content` delle pagine, non le pagine stesse. Per risolvere questo problema, potete eseguire una ricerca in base al percorso relativo:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Ricerca di più proprietà {#search-for-multiple-properties}

Quando si utilizza più volte il predicato delle proprietà, è necessario aggiungere di nuovo i prefissi numerici:

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

Per le proprietà multivalore, potete anche richiedere che più valori corrispondano (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Ottimizzazione dei valori restituiti {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON QueryBuilder restituirà un set predefinito di proprietà per ciascun nodo nel risultato della ricerca (ad esempio percorso, nome, titolo, ecc.). Per controllare quali proprietà vengono restituite, è possibile effettuare una delle seguenti operazioni:

Specifica

```xml
p.hits=full
```

in tal caso tutte le proprietà saranno incluse per ciascun nodo:

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

e specificare le proprietà in cui si desidera accedere

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

È inoltre possibile includere nodi secondari nella risposta di Query Builder. A tal fine è necessario specificare

```xml
p.nodedepth=n
```

dove `n` è il numero di livelli che si desidera che venga restituito dalla query. Per restituire un nodo figlio, è necessario specificarlo dal selettore delle proprietà

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

Per ulteriori predicati, consultate la pagina [Riferimento predicato Generatore di query](query-builder-predicates.md).

È inoltre possibile controllare il codice [Javadoc per le classi `PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc per queste classi contiene l&#39;elenco delle proprietà utilizzabili.

Il prefisso del nome della classe (ad esempio, `similar` in [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è la proprietà *principal* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in lettere minuscole).

Per tali proprietà principali, è possibile ridurre la query e utilizzare `similar=/content/en` invece della variante completa `similar.similar=/content/en`. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

## Esempio di utilizzo dell&#39;API Query Builder {#example-query-builder-api-usage}

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

La stessa query eseguita su HTTP tramite il servlet Query Builder (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento di query {#storing-and-loading-queries}

Le query possono essere memorizzate nella directory archivio in modo da poterle utilizzare in un secondo momento. `QueryBuilder` fornisce il metodo `storeQuery` con la seguente firma:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza il metodo [`QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession), l&#39;elemento `Query` specificato viene memorizzato nell&#39;archivio come file o come proprietà in base al valore dell&#39;argomento `createFile`. L&#39;esempio seguente mostra come salvare un `Query` nel percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Eventuali query precedentemente archiviate possono essere caricate dall&#39;archivio utilizzando il metodo [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` memorizzato nel percorso `/mypath/getfiles` può essere caricato dal frammento seguente:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per la riproduzione e il debug delle query di Query Builder, potete utilizzare la console di debug di Query Builder in

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

oppure, in alternativa, il servlet JSON di Query Builder all&#39;indirizzo

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` è solo un esempio.

### Debug generale Recommendations {#general-debugging-recommendations}

### Ottenere XPath spiegabile tramite la registrazione {#obtain-explain-able-xpath-via-logging}

Spiegare le query **all** durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

1. Abilitare i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante spiegabile
   * Accedi a `https://<host>:<port>/system/console/slinglog`. Create un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.
1. Una volta attivato DEBUG per la classe sopra riportata, i registri visualizzeranno l&#39;XPath generato da Query Builder.
1. Copiate la query XPath dalla voce di registro per la query di Query Builder associata, ad esempio:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Incollate la query XPath in Spiega query come XPath per ottenere il piano di query.

### Ottenete XPath spiegabile tramite Query Builder Debugger {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilizzate AEM Query Builder Debugger per generare una query XPath esplorabile.

![Debugger Query Builder](assets/query-builder-debugger.png)

1. Fornisce la query Query Builder nel debugger di Query Builder
1. Eseguire la ricerca
1. Ottenete l&#39;XPath generato
1. Incollare la query XPath in Explain Query come XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non Query Builder (XPath, JCR-SQL2) possono essere fornite direttamente a Explain Query.

## Debug di query con registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nel documento [Logging](/help/implementing/developing/introduction/logging.md).

L&#39;output di registro (livello INFO) dell&#39;implementazione del generatore di query durante l&#39;esecuzione della query descritta nella sezione precedente [Test and Debugging:](#testing-and-debugging)

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

Se si dispone di una query utilizzando i valutatori predicati che filtrano o utilizzano un ordine personalizzato per confronto, anche questo verrà notato nella query:

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
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | Query Builder di base e API Query |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bukets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Punti (contenuti nei facet) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Predicate Valutatori |
| [com.day.cq.search.facets.extrattori](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori di sfaccettature (per valutatori) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Scrittore di risultati JSON per il servlet Query Builder (`/bin/querybuilder.json`) |
