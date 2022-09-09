---
title: Rimozione dell'indice Lucene generico
description: Scopri la rimozione pianificata degli indici Lucene generici e le possibili conseguenze.
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# Rimozione dell&#39;indice Lucene generico {#generic-lucene-index-removal}

L&#39;Adobe intende rimuovere l&#39;indice &quot;generico Lucene&quot; (`/oak:index/lucene-*`) da Adobe Experience Manager as a Cloud Service. Questo indice è stato dichiarato obsoleto a partire dal AEM 6.5. In questo documento viene descritto l&#39;impatto di questa decisione, insieme a descrizioni dettagliate su come esaminare se un&#39;istanza AEM è interessata. Contiene anche modi per modificare le query in modo che continuino a funzionare senza l&#39;indice Lucene generico.

## Informazioni di base {#background}

In AEM, le query full text sono quelle che utilizzano le seguenti funzioni:

* `jcr:contains()` in JCR XPATH
* `CONTAINS` in JCR-SQL2

Tali query non possono restituire risultati senza utilizzare un indice. A differenza di una query contenente solo restrizioni di percorso o proprietà, una query contenente una restrizione di testo completa per la quale non è possibile trovare alcun indice (e quindi viene eseguito un attraversamento) restituirà sempre zero risultati.

Indice Lucene generico (`/oak:index/lucene-*`) esiste a partire da AEM 6.0 / Oak 1.0 per fornire una ricerca full-text nella maggior parte della gerarchia dell&#39;archivio, anche se alcuni percorsi, come `/jcr:system` e `/var` sono sempre stati esclusi da questo. Tuttavia, questo indice è stato in gran parte sostituito dagli indici su tipi di nodo più specifici (ad esempio `damAssetLucene-*` per `dam:Asset` tipo di nodo), che supporta sia le ricerche full text che di proprietà.

Nella AEM 6.5 l&#39;indice generico Lucene è stato contrassegnato come obsoleto, indicando che sarebbe stato rimosso nelle versioni future. Da allora, è stato registrato un WARN quando l&#39;indice è stato utilizzato come illustrato dal seguente frammento di log:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

Nelle versioni recenti AEM, l&#39;indice Lucene generico è stato utilizzato per supportare un numero molto ridotto di funzioni. Questi vengono rielaborati per utilizzare altri indici o modificati in altro modo per rimuovere la dipendenza da questo indice.

Ad esempio, le query di ricerca di riferimento, come nell’esempio seguente, ora devono utilizzare l’indice in `/oak:index/pathreference`, che indicizza solo `String` valori di proprietà che corrispondono a un&#39;espressione regolare che cerca i percorsi JCR.

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Per supportare volumi di dati dei clienti più grandi, Adobe non creerà più l’indice Lucene generico sui nuovi ambienti as a Cloud Service AEM. Inoltre, Adobe inizierà a rimuovere l&#39;indice dagli archivi esistenti. [Visualizzare la timeline](#timeline) alla fine del presente documento per ulteriori dettagli.

L&#39;Adobe ha già adeguato i costi dell&#39;indice tramite il `costPerEntry` e `costPerExecution` per garantire che altri indici, come `/oak:index/pathreference` sono utilizzati nella preferenza laddove possibile.

Le applicazioni cliente che utilizzano query che dipendono ancora da questo indice devono essere aggiornate immediatamente per sfruttare altri indici esistenti, personalizzabili se necessario. In alternativa, è possibile aggiungere nuovi indici personalizzati all’applicazione cliente. Le istruzioni complete per la gestione degli indici in AEM as a Cloud Service sono disponibili nella sezione [documentazione sull&#39;indicizzazione.](/help/operations/indexing.md)

## Sei Interessata? {#are-you-affected}

L&#39;indice Lucene generico è attualmente utilizzato come fallback se nessun altro indice full text può soddisfare una query. Quando si utilizza questo indice obsoleto, un messaggio come questo verrà registrato a livello WARN:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

In alcune circostanze, Oak potrebbe tentare di utilizzare un altro indice full text (come `/oak:index/pathreference`) per supportare la query full text, ma se la stringa di query non corrisponde all’espressione regolare nella definizione dell’indice, verrà registrato un messaggio a livello WARN e la query probabilmente non restituirà risultati.

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Una volta rimosso l&#39;indice Lucene generico, un messaggio come mostrato di seguito verrà registrato a livello WARN se una query full text non è in grado di individuare alcuna definizione di indice adatta:

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**Azione del cliente richiesta**
>
> Se viene registrato uno dei messaggi di avviso di cui sopra, potrebbe essere necessario rielaborare la query per utilizzare un indice di testo completo diverso o fornire un nuovo indice per supportare la query.
>
>I dettagli sui tipi di dipendenze che è possibile visualizzare e su come risolverle sono forniti nelle sezioni seguenti.

## Dipendenze potenziali dagli indici Lucene generici {#potential-dependencies}

Ci sono diverse aree in cui le applicazioni e le installazioni di AEM possono dipendere da indici Lucene generici sia sulle istanze di authoring che di pubblicazione.

### Pubblica istanza {#publish-instance}

#### Query di applicazione personalizzate {#custom-application-queries}

L&#39;origine più comune di query che utilizzano l&#39;indice Lucene generico su un&#39;istanza di pubblicazione saranno query di applicazione personalizzate.

Nei casi più semplici, queste potrebbero essere query prive di un tipo di nodo specificato, il che implica `nt:base` o `nt:base` specificato esplicitamente, ad esempio:

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**Azione del cliente richiesta**
>
>Le query di cui sopra devono essere modificate per utilizzare un tipo di nodo appropriato come descritto nella sezione seguente.

Ad esempio, le query possono essere modificate per restituire i risultati corrispondenti alle pagine o a uno qualsiasi degli aggregati sotto la `cq:Page node`. La query potrebbe quindi diventare:

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

In altri casi, una query può specificare un tipo di nodo ma contiene una restrizione full text che non può essere gestita da un altro indice full text, ad esempio:

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

In questo caso, la query ha la `dam:Asset` tipo di nodo, ma contiene una restrizione full text sul relativo `jcr:content/metadata/@cq:tags` proprietà.

Questa proprietà non è contrassegnata come analizzata nella `damAssetLucene` index, che è l&#39;indice full text più comunemente utilizzato per le query contro `dam:Asset` tipo di nodo. Pertanto questo indice non può essere utilizzato per questa query.

Di conseguenza, la query rientra nell’indice generico full text in cui tutte le proprietà incluse vengono contrassegnate come analizzate dalla corrispondenza con il carattere jolly in `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**Azione del cliente richiesta**
>
>Contrassegno del `jcr:content/metadata/@cq:tags` come analizzato in una versione personalizzata del `damAssetLucene` l&#39;indice farà sì che questa query venga gestita da questo indice e non verrà registrato alcun WARN.

### Istanza autore {#author-instance}

Oltre alle query nei servlet dell&#39;applicazione del cliente, nei componenti OSGi e negli script di rendering, possono esserci diversi utilizzi specifici dell&#39;autore dell&#39;indice Lucene generico.

#### Ricerca di riferimento {#reference-search}

Storicamente l’indice Lucene generico è stato utilizzato per supportare la ricerca di riferimenti o la ricerca di contenuti che contengono riferimenti a un altro percorso di contenuto. Tali query avrebbero già dovuto essere aggiornate per utilizzare il nuovo `/oak:index/pathreference` indice.

#### Ricerca selettore campi percorso {#picker-search}

AEM include un componente di dialogo personalizzato con il tipo di risorsa Sling `granite/ui/components/coral/foundation/form/pathfield`, che fornisce un browser/selettore per selezionare un altro percorso AEM. Selettore campo percorso predefinito, utilizzato quando non è personalizzato `pickerSrc` viene definita nella struttura del contenuto, esegue il rendering di una barra di ricerca nella finestra di dialogo a comparsa.

I tipi di nodo su cui eseguire la ricerca possono essere specificati utilizzando la variabile `nodeTypes` proprietà.

Attualmente, se no `nodeTypes` la proprietà è presente, la query di ricerca sottostante utilizzerà la proprietà `nt:base` tipo di nodo, e quindi è probabile che utilizzi l&#39;indice Lucene generico, in genere registrando messaggi WARN simili al seguente.

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Prima della rimozione dell&#39;indice generico Lucene, il `pathfield` il componente viene aggiornato in modo che la casella di ricerca sia nascosta per i componenti che utilizzano il selettore predefinito, che non fornisce un `nodeTypes` proprietà.

| Selettore campo percorso con ricerca | Selettore dei campi di percorso senza ricerca |
|---|---|
| ![Selettore campo percorso con ricerca](assets/index-pathfield-picker-with-search.png) | ![Selettore dei campi di percorso senza ricerca](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**Azione del cliente richiesta**
>
>Se il cliente desidera mantenere la funzionalità di ricerca nel selettore dei campi del percorso, un `nodeTypes` fornire la proprietà elencando i tipi di nodo su cui si desidera eseguire la query. Questi possono essere specificati come un elenco separato da virgole dei tipi di nodo in un `String` proprietà. Se non è richiesta alcuna ricerca, non è necessaria alcuna azione da parte del cliente.

>[!NOTE]
>
>L’Editor modello frammento di contenuto utilizza un percorso specializzato con il tipo di risorsa Sling `dam/cfm/models/editor/components/contentreference`.
> * Attualmente queste eseguono query senza tipi di nodo specificati, con conseguente registrazione di un WARN a causa dell&#39;utilizzo dell&#39;indice Lucene generico.
> * Le istanze di questi componenti verranno presto automaticamente impostate su `cq:Page` e `dam:Asset` tipi di nodo senza ulteriori azioni da parte del cliente.
> * La `nodeTypes` è possibile aggiungere la proprietà per ignorare questi tipi di nodo predefiniti.


## Timeline per rimozione Lucene generica {#timeline}

L&#39;Adobe adotterà un approccio in due fasi per rimuovere l&#39;indice Lucene generico.

* **Fase 1** (inizio previsto: 31 gennaio 2022): Non creare più `/oak:index/lucene-*` sui nuovi ambienti as a Cloud Service AEM.
* **Fase 2** (inizio previsto: 31 marzo 2022): Rimuovi `/oak:index/lucene-*` da ambienti as a Cloud Service AEM esistenti.

L&#39;Adobe controllerà i messaggi di log sopra indicati e cercherà di contattare i clienti che rimangono dipendenti dall&#39;indice Lucene generico.

Come mitigazione a breve termine, l&#39;Adobe aggiungerà definizioni di indice personalizzate direttamente ai sistemi dei clienti per evitare problemi funzionali o di prestazioni in seguito alla rimozione dell&#39;indice Lucene generico, se necessario.

In questi casi, al cliente verrà fornita la definizione di indice aggiornata e consigliato di includerlo nelle versioni future della sua applicazione tramite Cloud Manager.
