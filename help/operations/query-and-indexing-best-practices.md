---
title: Tecniche consigliate per query e indicizzazione
description: Scopri come ottimizzare indici e query in base alle linee guida sulle best practice di Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: afeff7cfb8606eb58126a4ca62ce9e6e58c44215
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# Tecniche consigliate per query e indicizzazione {#query-and-indexing-best-practices}

In AEM as a Cloud Service, tutti gli aspetti operativi relativi all&#39;indicizzazione sono automatizzati. Questo consente agli sviluppatori di concentrarsi sulla creazione di query efficienti e sulle relative definizioni di indice.

## Quando utilizzare le query {#when-to-use-queries}

Le query sono un modo per accedere ai contenuti, ma non sono l’unica possibilità. In molte situazioni, l’accesso ai contenuti dell’archivio è più efficace con altri mezzi. È consigliabile considerare se le query sono il modo migliore e più efficiente per accedere al contenuto del caso d’uso.

### Struttura dell&#39;archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, è necessario tenere conto di diversi fattori. tra cui controlli di accesso, localizzazione, ereditarietà di componenti e proprietà di pagina e altro ancora.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la &quot;traversabilità&quot; del design di indicizzazione. In questo contesto, l’attraversabilità è la capacità di una tassonomia di consentire l’accesso prevedibile ai contenuti in base al relativo percorso. Ciò rende un sistema più efficiente, più semplice da gestire rispetto a uno che richiede l’esecuzione di più query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l&#39;importanza dell&#39;ordine. Nei casi in cui non è richiesto un ordine esplicito e si prevede un numero elevato di nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesta l&#39;ordinazione, `nt:unstructured` e `sling:OrderedFolder` sarebbe più appropriato.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni di imposizione più eseguite su un sistema AEM, è consigliabile evitarle nei componenti. L’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può spesso compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l’esecuzione di query durante il rendering dei componenti: **[attraversamento dei nodi](#traversing-nodes)** e **[preacquisizione dei risultati.](#prefetching-results)**

### Navigazione nei nodi {#traversing-nodes}

Se l&#39;archivio è progettato in modo tale da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera questi dati dai percorsi necessari può essere distribuito senza dover eseguire query per trovarli.

Un esempio potrebbe essere il rendering di contenuti che si adattano a una determinata categoria. Un approccio consiste nell’organizzare il contenuto con una proprietà di categoria su cui è possibile eseguire una query per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nel strutturare il contenuto in una tassonomia per categoria in modo che possa essere recuperato manualmente.

Ad esempio, se il contenuto viene memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

la `/content/myUnstructuredContent/parentCategory/childCategory` il nodo può essere semplicemente recuperato, i relativi figli possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, può essere più veloce attraversare l’archivio e raccogliere i nodi richiesti, anziché creare una query per restituire lo stesso set di risultati. In generale, occorre evitare le interrogazioni laddove possibile.

### Recupero preventivo dei risultati {#prefetching-results}

A volte il contenuto o i requisiti intorno al componente non consentono l’uso di nodi traversal come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query necessarie prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto cambi, la query può essere eseguita dopo aver apportato una modifica.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita su una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Quindi, i risultati possono essere scritti in una posizione condivisa nell&#39;archivio. Tutti i componenti che necessitano di questi dati possono quindi estrarre i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

Una strategia simile può essere utilizzata per mantenere il risultato in una cache in memoria, che viene popolata all&#39;avvio e aggiornata ogni volta che vengono apportate modifiche (utilizzando un JCR `ObservationListener` o Sling `ResourceChangeListener`).

## Ottimizzazione delle query {#optimizing-queries}

La documentazione Oak fornisce un [panoramica di alto livello sulle modalità di esecuzione delle query.](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) Questo costituisce la base di tutte le attività di ottimizzazione descritte nel presente documento.

AEM as a Cloud Service fornisce lo strumento Prestazioni query, progettato per supportare l’implementazione di query efficienti.

* Vengono visualizzate le query già eseguite con le relative caratteristiche di prestazioni e il piano di query.
* Consente l’esecuzione di query ad-hoc a vari livelli, a partire dalla semplice visualizzazione del piano di query fino all’esecuzione della query completa.

Lo strumento Prestazioni query è raggiungibile tramite la [Console per sviluppatori in Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it#queries) AEM Query Performance Tool di as a Cloud Service fornisce ulteriori informazioni sui dettagli dell’esecuzione della query sulla versione 6.x di AEM.

Questo grafico illustra il flusso generale da utilizzare per ottimizzare le query con lo strumento Prestazioni query.

![Flusso di ottimizzazione query](assets/query-optimization-flow.png)

### Utilizzare un indice {#use-an-index}

Ogni query deve utilizzare un indice per fornire prestazioni ottimali. Nella maggior parte dei casi, gli indici preconfigurati esistenti dovrebbero essere sufficienti per gestire le query.

A volte è necessario aggiungere proprietà personalizzate a un indice esistente, in modo che sia possibile eseguire query sui vincoli aggiuntivi utilizzando l&#39;indice. Vedere il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#changing-an-index) per ulteriori dettagli. La [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) in questa sezione viene descritto come cercare una definizione di proprietà in un indice per supportare un tipo di query specifico.

### Utilizzare i criteri giusti {#use-the-right-criteria}

Il vincolo principale su qualsiasi query deve essere una corrispondenza di proprietà, in quanto questo è il tipo più efficiente. L’aggiunta di più vincoli di proprietà limita ulteriormente il risultato.

Il motore di query considera un solo indice. Ciò significa che un indice esistente può e deve essere personalizzato aggiungendo ad esso proprietà di indice più personalizzate.

La [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) in questa sezione sono elencati i vincoli disponibili e viene inoltre illustrato come la definizione di un indice deve essere visualizzata in modo da essere selezionata. Utilizza la [Strumento Prestazioni query](#query-performance-tool) per verificare la query e assicurarsi che venga utilizzato l&#39;indice corretto e che il motore di query non debba valutare i vincoli al di fuori dell&#39;indice.

### Ordinazione {#ordering}

Se viene richiesto un ordine specifico del risultato, esistono due modi per ottenere questo risultato da parte del motore di query:

1. L&#39;indice può fornire il risultato completamente e nell&#39;ordine giusto.
   * Questo funziona se le proprietà utilizzate per l&#39;ordinamento vengono annotate con `ordered=true` nella definizione dell&#39;indice.
1. Il motore di query esegue il processo di ordinamento.
   * Ciò può verificarsi quando il motore di query esegue il filtraggio all’esterno dell’indice o la proprietà di ordinamento non viene annotata con `ordered=true` proprietà.
   * Questo richiede che il set di risultati completo venga letto in memoria per l’ordinamento, il che è molto più lento della prima opzione.

### Limitare le dimensioni dei risultati {#restrict-result-size}

La dimensione recuperata del risultato della query è un fattore importante nelle prestazioni della query. Poiché il risultato viene recuperato in modo pigro, c&#39;è una differenza nel recupero dei primi 20 risultati rispetto al recupero di 10.000 risultati, sia in runtime che nell&#39;utilizzo della memoria.

Ciò significa anche che le dimensioni del set di risultati possono essere determinate correttamente solo se tutti i risultati vengono recuperati. Per questo motivo, il set di risultati recuperato deve sempre essere limitato, sia incrementando la query (vedi la [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) sezione del presente documento per dettagli) o limitando la lettura dei risultati.

Tale limite impedisce inoltre al motore di query di raggiungere il **limite di traversata** di 100.000 nodi, che porta a un arresto forzato della query.

Vedi la sezione [Query con risultati di grandi dimensioni](#queries-with-large-result-sets) di questo documento se un set di risultati potenzialmente grande deve essere elaborato completamente.

## Foglio di riferimento per le query JCR {#jcr-query-cheatsheet}

Per supportare la creazione di query JCR efficienti e le definizioni degli indici, la [Foglio di calcolo della query JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) è disponibile per il download e l’utilizzo come riferimento durante lo sviluppo.

Contiene query di esempio per QueryBuilder, XPath e SQL-2, che coprono scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre raccomandazioni su come creare o personalizzare gli indici Oak. Il contenuto di questo Cheat Sheet si applica a AEM as a Cloud Service e a AEM 6.5.

## Query con set di risultati di grandi dimensioni {#queries-with-large-result-sets}

Anche se si consiglia di evitare le query con set di risultati di grandi dimensioni, ci sono casi validi in cui è necessario elaborare set di risultati di grandi dimensioni. Spesso le dimensioni del risultato non sono note in anticipo, quindi si dovrebbero prendere alcune precauzioni per rendere affidabile il trattamento.

* La query non deve essere eseguita all’interno di una richiesta. La query deve invece essere eseguita come parte di un processo Sling o di un flusso di lavoro AEM. Questi non hanno limitazioni nel runtime totale e vengono riavviati nel caso in cui l’istanza si abbassi durante l’elaborazione della query e dei relativi risultati.
* Per superare il limite di query di 100.000 nodi, è consigliabile utilizzare [Paginazione dei keyset](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) e suddivide la query in più sottoquery.

## Archivio Traversal {#repository-traversal}

Le query che attraversano l&#39;archivio non utilizzano un indice e registrano con un messaggio simile al seguente.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Con questo frammento di log puoi determinare:

* La query stessa: `//*`
* Il codice Java che ha eseguito questa query: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` per identificare l’autore della query.

Con queste informazioni, è possibile ottimizzare questa query utilizzando i metodi descritti in [Ottimizzazione delle query](#optimizing-queries) sezione di questo documento.
