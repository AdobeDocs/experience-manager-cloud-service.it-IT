---
title: Tecniche consigliate per query e indicizzazione
seo-title: Best Practices for Queries and Indexing
description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
topic-tags: best-practices
source-git-commit: 85cbdaa6e6d01856005cb47f289d391fb44bd65e
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Tecniche consigliate per query e indicizzazione{#best-practices-for-queries-and-indexing}

A differenza delle versioni precedenti in AEM, tutti gli aspetti operativi relativi all&#39;indicizzazione sono automatizzati. Questo consente agli sviluppatori di concentrarsi sulla creazione di query efficienti e sulle relative definizioni di indice.

## Quando utilizzare le query {#when-to-use-queries}

Le query sono un modo per accedere ai contenuti, ma non l’unico. Per questo motivo è necessario valutare se le query sono il modo migliore e più performante per accedere al contenuto. In molte situazioni, l’accesso al contenuto nell’archivio è più performante con altri metodi.

### Struttura dell&#39;archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, è necessario tenere conto di diversi fattori. tra cui controlli di accesso, localizzazione, ereditarietà di componenti e proprietà di pagina.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la &quot;traversabilità&quot; del design di indicizzazione. In questo contesto, l’attraversabilità è la capacità di una tassonomia che consente un accesso prevedibile ai contenuti in base al relativo percorso. Questo renderà più performante un sistema più semplice da mantenere rispetto a uno che richiederà l&#39;esecuzione di molte query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l&#39;importanza dell&#39;ordine. Nei casi in cui non è richiesto un ordine esplicito e si prevede un numero elevato di nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesta l&#39;ordinazione, `nt:unstructured` e `sling:OrderedFolder` sarebbe più appropriato.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni di imposizione più eseguite su un sistema AEM, è consigliabile evitarle nei componenti. L’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può spesso compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l’esecuzione di query durante il rendering dei componenti: **attraversamento dei nodi** e **risultati di preacquisizione**.

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

A volte il contenuto o i requisiti intorno al componente non consentono l’uso di node traversal come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query necessarie prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto cambi, la query può essere eseguita dopo aver apportato una modifica.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita su una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Quindi, i risultati possono essere scritti in una posizione condivisa nell&#39;archivio. Tutti i componenti che necessitano di questi dati possono quindi estrarre i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.
Una strategia simile può essere utilizzata per mantenere il risultato in una cache in memoria, che viene popolata all&#39;avvio e aggiornata ogni volta che vengono apportate modifiche (utilizzando un JCR ObservationListener o un Sling ResourceChangeListener).

## Ottimizzazione delle query {#optimizing-queries}

La documentazione Oak fornisce un [panoramica di alto livello sulle modalità di esecuzione delle query](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing). Questo costituisce la base di tutte le attività di ottimizzazione descritte nel presente documento.

AEM as a Cloud Service fornisce Query Performance Tool, progettato per supportare l’implementazione di query efficienti.
* Vengono visualizzate le query già eseguite con le relative caratteristiche di prestazioni e il piano di query.
* Consente di eseguire query adhoc a vari livelli, partendo dalla semplice visualizzazione del piano di query fino all’esecuzione della query completa.

Lo strumento Prestazioni query è raggiungibile tramite la [Console per sviluppatori in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it#queries). A differenza dello strumento di prestazioni Query delle versioni precedenti di AEM 6.x, lo strumento di query delle prestazioni fornito per AEM as a Cloud Service fornisce ulteriori informazioni sui dettagli dell’esecuzione della query, utili per migliorare una query.


L’approccio generale su come utilizzare lo strumento Prestazioni query per ottimizzare le query è descritto in questo grafico.
![Flusso di ottimizzazione query](assets/query-optimization-flow.png)



### Utilizzare un indice {#use-an-index}

Ogni query deve utilizzare un indice per fornire prestazioni ottimali. Nella maggior parte dei casi, gli indici preconfigurati esistenti dovrebbero essere sufficienti per gestire le query.
A volte è necessario aggiungere proprietà personalizzate a un indice esistente, in modo che sia possibile eseguire query sui vincoli aggiuntivi utilizzando questo indice. Vedi [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#changing-an-index) per ulteriori dettagli. La [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) descrive l&#39;aspetto di una definizione di proprietà su un indice per supportare un tipo di query specifico.



### Utilizzare i criteri giusti

Il vincolo principale su qualsiasi query deve essere una corrispondenza di proprietà, in quanto questo è il tipo più efficiente. L’aggiunta di ulteriori vincoli di proprietà limita ulteriormente il risultato.
Il motore di query considera un solo indice; ciò significa che un indice esistente può e deve essere personalizzato aggiungendo ad esso proprietà di indice più personalizzate.

La [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) elenca i vincoli disponibili e illustra anche come deve essere simile a una definizione di indice in modo che venga ripresa. Utilizza la [Strumento Prestazioni query](#query-performance-tool) per verificare la query e assicurarsi che venga utilizzato l&#39;indice corretto e che il motore di query non debba valutare i vincoli al di fuori dell&#39;indice.


### Ordinazione

Se viene richiesto un ordine specifico del risultato, sono disponibili 2 modi per ottenere questo risultato:

1. l&#39;indice può fornire il risultato completamente e nell&#39;ordine giusto; questo funziona se le proprietà utilizzate per l&#39;ordinamento vengono annotate con ```ordered=true``` nella definizione dell&#39;indice.
2. Se il motore di query deve eseguire un filtraggio al di fuori dell’indice o se la proprietà di ordinamento non viene annotata con il ```ordered=true``` , il motore di query esegue anche il processo di ordinamento. Questo caso richiede che il set di risultati completo sia letto in memoria per l’ordinamento, il che è molto più lento della prima opzione.





### Limitare la dimensione del risultato

La dimensione recuperata del risultato della query è un fattore importante nelle prestazioni della query. Poiché il risultato viene recuperato in modo pigro, c&#39;è una differenza nel recupero dei primi 20 risultati rispetto al recupero di 10.000 risultati, sia in runtime che in uso di memoria.

Ciò significa anche che le dimensioni del set di risultati possono essere determinate correttamente solo se vengono recuperati tutti i risultati. Per questo motivo il set di risultati recuperato deve sempre essere limitato, sia mediante l’aumento della query (consulta la sezione [Foglio di riferimento per le query JCR](#jcr-query-cheatsheet) per dettagli) o limitando la lettura dei risultati.
Tale limite impedisce inoltre al motore di query di raggiungere il **limite di traversata** di 100.000 nodi, che porta a un arresto forzato della query.

Vedi la sezione [Query con risultati di grandi dimensioni](#queries-with-large-result-sets) di seguito se un set di risultati potenzialmente grande deve essere elaborato completamente.


## Foglio di riferimento per le query JCR

Per supportare la creazione di query JCR efficienti e le definizioni degli indici, la [Foglio di calcolo della query JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) è disponibile per il download e l’utilizzo come riferimento durante lo sviluppo. Contiene query di esempio per QueryBuilder, XPath e SQL-2, che coprono scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre raccomandazioni su come creare o personalizzare gli indici Oak. Il contenuto di questo Cheat Sheet si applica a AEM 6.5 e AEM as a Cloud Service.


## Query con set di risultati di grandi dimensioni

Sebbene sia consigliabile evitare le query con un set di risultati di grandi dimensioni, ci sono casi validi in cui è necessario elaborare risultati di grandi dimensioni. Spesso la dimensione del risultato non è nota in anticipo, quindi si dovrebbero prendere alcune precauzioni per rendere affidabile il trattamento.

* la query non deve essere eseguita all’interno di una richiesta; la query deve invece essere eseguita come parte di un processo Sling o di un flusso di lavoro AEM. Queste non presentano limitazioni nel runtime totale e vengono riavviate nel caso in cui l’istanza venga disattivata durante l’elaborazione della query e dei relativi risultati.
* Per superare il limite di query di 100.000 nodi letti è consigliabile utilizzare [Paginazione dei keyset](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) e suddivide la query in più sottoquery.



## Query che attraversa il repository

Le query che attraversano il repository non utilizzano un indice e registrano messaggi come questo:

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Questo frammento di log contiene informazioni rilevanti:

* la query stessa: ```//* ```
* il codice java che ha eseguito questa query: ```com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics```; questo aiuta a identificare il creatore della query.

Con queste informazioni è possibile ottimizzare questa query utilizzando i metodi descritti in [Ottimizzazione delle query](#optimizing-queries).