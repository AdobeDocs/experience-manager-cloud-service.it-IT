---
title: Rimozione dell'indice generico lucene
description: Rimozione dell'indice generico lucene
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Rimozione dell&#39;indice generico lucene

L&#39;Adobe intende rimuovere l&#39;indice generico lucene (`/oak:index/lucene-*`) da Adobe Experience Manager as a Cloud Service. Questo indice è stato dichiarato obsoleto a partire dal AEM 6.5. In questa documentazione viene descritto l&#39;impatto di questa decisione, insieme a descrizioni dettagliate su come esaminare se un&#39;istanza AEM è interessata. Infine, contiene modi per modificare le query in modo che funzionino senza che questo indice sia presente.

## Sfondo

In AEM, query &#39;fulltext&#39; come quelle che utilizzano le seguenti funzioni:

* `jcr:contains()` in JCR XPATH
* `CONTAINS` in JCR-SQL2

Tali query non possono restituire risultati senza utilizzare un indice. A differenza di una query contenente solo restrizioni di percorso o proprietà, una query contenente una restrizione di testo completo per la quale non è possibile trovare alcun indice (e quindi viene eseguito un attraversamento) restituirà sempre 0 risultati.

Indice &quot;generico lucene&quot; (`/oak:index/lucene-*`) è esistito a partire da AEM 6.0 / Oak 1.0 per fornire una ricerca full-text nella maggior parte della gerarchia del repository (alcuni percorsi, come `/jcr:system` e `/var` sono sempre stati esclusi da questo) tuttavia questo indice è stato in gran parte sostituito da indici su tipi di nodo più specifici (per esempio `damAssetLucene-*` per il tipo di nodo &#39;dam:Asset&#39;) che supporta sia ricerche full-text che proprietà.

Nella AEM 6.5 l&#39;indice &quot;generico lucene&quot; è stato contrassegnato come obsoleto (indicato che sarebbe stato rimosso nelle versioni future), e da allora, quando l&#39;indice è stato utilizzato, è stato registrato un avviso:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

Nelle versioni recenti AEM, l&#39;indice generico lucene è stato utilizzato per supportare un numero molto ridotto di funzioni. Questi vengono rielaborati per utilizzare altri indici o modificati in altro modo per rimuovere la dipendenza da questo indice.
Ad esempio, le query di &#39;ricerca di riferimento&#39;, del modulo mostrato di seguito, ora devono utilizzare l&#39;indice in &#39;/oak:index/pathreference&#39; (che indicizza solo i valori delle proprietà String che corrispondono a un&#39;espressione regolare che cerca i percorsi JCR). 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Per supportare volumi di dati dei clienti più grandi, Adobe non creerà più l&#39;indice &quot;lucene generico&quot; su nuovi ambienti as a Cloud Service AEM e, di conseguenza, inizierà a rimuovere l&#39;indice dai repository esistenti. Abbiamo già modificato i costi dell&#39;indice (tramite le proprietà &#39;costPerEntry&#39; e &#39;costPerExecution&#39;) per garantire che altri indici (come `/oak:index/pathreference`) sono utilizzate in preferenza per `/oak:index/lucene-*` laddove possibile. 

Le applicazioni cliente che utilizzano query che dipendono ancora da questo indice devono essere aggiornate immediatamente per sfruttare altri indici esistenti (che possono essere personalizzati se necessario) o nuovi indici personalizzati devono essere aggiunti all&#39;applicazione cliente. Per istruzioni complete sulla gestione degli indici in AEM as a Cloud Service, consulta [documentazione sull&#39;indicizzazione](/help/operations/indexing.md).

## Come dire se la tua applicazione dipende dall&#39;indice &#39;generico lucene&#39;?

L&#39;indice &#39;generico lucene&#39; è attualmente utilizzato come &#39;fallback&#39; se nessun altro indice fulltext può soddisfare una query. Quando si utilizza questo indice obsoleto, un messaggio come questo verrà registrato a livello WARN:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

In alcune circostanze Oak potrebbe tentare di utilizzare un altro indice fulltext (come `/oak:index/pathreference`) per supportare la query full-text, ma se la stringa di query non corrisponde all’espressione regolare nella definizione dell’indice, verrà registrato un messaggio a livello WARN e la query probabilmente non restituirà risultati.

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Una volta rimosso l&#39;indice lucene generico, un messaggio come mostrato di seguito verrà registrato a livello WARN se una query di testo completo non è in grado di individuare alcuna definizione di indice adatta:

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

Se qualcuno di questi è registrato, potrebbe essere necessario rielaborare la query per utilizzare un indice fulltext diverso o fornire un nuovo indice per supportare la query. Di seguito sono riportati i dettagli sui tipi di dipendenze che potresti vedere e su come risolverle.

## Dipendenze potenziali dall&#39;indice &quot;generico lucene&quot;

### Pubblicazione

#### Query di applicazione personalizzate

L&#39;origine più comune di query che utilizzano l&#39;indice lucene generico su Publish saranno le query di applicazione personalizzate.

Nei casi più semplici, queste potrebbero essere query prive di nodetype specificato (che implicano &#39;nt:base&#39;) o nt:base specificato esplicitamente, ad esempio:

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

Azione richiesta : Queste query possono essere modificate per utilizzare un tipo di nodo appropriato - ad esempio, per restituire i risultati che corrispondono alle pagine (o uno qualsiasi degli &quot;aggregati&quot; sotto il nodo cq:Page), la query potrebbe diventare:

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

In altri casi, una query può specificare un tipo di nodo ma contiene una restrizione di tipo fulltext che non può essere gestita da un altro indice di tipo fulltext, ad esempio:

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

In questo caso la query ha il tipo di nodo &#39;dam:Asset&#39;, ma contiene una restrizione full-text sul relativo `jcr:content/metadata/@cq:tags` proprietà.

Questa proprietà non è contrassegnata come &#39;analizzata&#39; nell&#39;indice damAssetLucene (l&#39;indice fulltext più comunemente utilizzato per le query contro il nodetype &#39;dam:Asset&#39;), pertanto questo indice non può essere utilizzato per questa query.

Di conseguenza, la query rientra nell’indice &quot;generico fulltext&quot; in cui tutte le proprietà incluse sono contrassegnate come analizzate dalla corrispondenza con il carattere jolly in `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

Azione cliente richiesta : marcatura `jcr:content/metadata/@cq:tags` la proprietà &#39;analizzata&#39; in una versione personalizzata dell&#39;indice damAssetLucene comporterà la gestione di questa query da parte di questo indice e non verrà registrato alcun WARN.

### Autore 

Oltre alle query nei servlet dell&#39;applicazione del cliente, nei componenti OSGI e negli script di rendering possono essere utilizzati diversi utilizzi specifici dell&#39;autore dell&#39;indice lucene generico. 

#### Ricerca di riferimento

Storicamente l’indice lucene generico è stato utilizzato per supportare la ricerca di riferimento (ricerca di contenuti che contiene riferimenti a un altro percorso di contenuto). Tali query avrebbero già dovuto essere spostate per utilizzare il nuovo indice &#39;/oak:index/pathreference&#39;.
Azione cliente richiesta : non è richiesta alcuna azione del cliente.


#### Ricerca nel selettore dei percorsi

AEM include un componente di dialogo personalizzato (tipo di risorsa Sling &quot;granite/ui/components/coral/foundation/form/pathfield&quot;) che fornisce un browser (selettore) per selezionare un altro percorso AEM.  Il selettore di percorsi predefinito (utilizzato quando nessuna proprietà personalizzata &#39;pickerSrc&#39; definita nella struttura del contenuto) esegue il rendering di una barra di ricerca nella finestra di dialogo a comparsa.
I tipi di nodo rispetto ai quali eseguire la ricerca possono essere specificati utilizzando la proprietà &#39;nodeTypes&#39;.

Al momento, se non è presente alcuna proprietà &#39;nodeTypes&#39;, la query di ricerca sottostante utilizzerà il tipo di nodo &#39;nt:base&#39; e quindi è probabile che utilizzi l&#39;indice &#39;generico lucene&#39; (in genere registra i messaggi WARN mostrati di seguito).

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Prima della rimozione di &quot;lucene generico&quot;, il componente del campo percorso verrà aggiornato in modo che la casella di ricerca sia nascosta per i componenti che utilizzano il selettore predefinito, che non forniscono una proprietà &#39;nodeTypes&#39;.

| Selezione campi percorso con ricerca | Selettore di campi percorso senza ricerca |
|---|---|
| ![Selezione campi percorso con ricerca](assets/index-pathfield-picker-with-search.png) | ![Selettore di campi percorso senza ricerca](assets/index-pathfield-picker-without-search.png) |


Azione cliente richiesta : Se non è richiesta alcuna ricerca, non è necessaria alcuna azione da parte del cliente.

Se il cliente desidera mantenere la funzionalità di ricerca nel selettore percorsi, è necessario fornire una proprietà &#39;nodeTypes&#39; elencando i tipi di nodo su cui desidera eseguire la query. Questi possono essere specificati come elenco di tipi di nodi separati da virgola in una proprietà String.


>[!NOTE]
>L’Editor modello frammento di contenuto utilizza campi di percorso specializzati con Sling Resource Type &quot;dam/cfm/models/editor/components/contentreference&quot;.
> * Attualmente queste eseguono query senza tipi di nodo specificati - con conseguente registrazione di un WARN a causa dell&#39;utilizzo dell&#39;indice lucene generico.
> * Le istanze di questi componenti verranno presto automaticamente impostate sui tipi di nodo &#39;cq:Page&#39; e &#39;dam:Asset&#39; senza ulteriori azioni da parte del cliente.
> * È possibile aggiungere la proprietà &#39;nodeTypes&#39; per ignorare questi tipi di nodo predefiniti. 





## Timeline per rimuovere &#39;generico lucene&#39;

L&#39;Adobe adotterà un approccio in due fasi alla rimozione dell&#39;indice generico lucene.

**Fase 1** (inizio previsto: 31 gennaio 2022): Non creare più &#39;/oak:index/lucene-*&#39; nei nuovi ambienti as a Cloud Service AEM.

**Fase 2** (inizio previsto: 31 marzo 2022) : Rimuovi l&#39;indice &#39;/oak:index/lucene-*&#39; dai nuovi ambienti as a Cloud Service AEM.

L&#39;Adobe controllerà i messaggi di log sopra indicati e cercherà di contattare i clienti che rimangono dipendenti dall&#39;indice lucene generico.

Come mitigazione a breve termine, se necessario, l&#39;Adobe aggiungerà definizioni di indice personalizzate direttamente ai sistemi dei clienti per evitare problemi funzionali o di prestazioni dovuti alla rimozione dell&#39;indice &quot;lucene generico&quot;.

In questi casi, al cliente verrà fornita la definizione di indice aggiornata e consigliato di includerlo nelle versioni future della sua applicazione tramite Cloud Manager.
