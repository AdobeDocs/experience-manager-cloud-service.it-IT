---
title: Best practice per query e indicizzazione
description: Scopri come ottimizzare indici e query in base alle linee guida sulle best practice di Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 95%

---

# Best practice per query e indicizzazione {#query-and-indexing-best-practices}

In AEM as a Cloud Service, tutti gli aspetti operativi relativi all’indicizzazione sono automatizzati. Questo consente agli sviluppatori di concentrarsi sulla creazione di query efficienti e sulle relative definizioni di indice.

## Quando utilizzare le query {#when-to-use-queries}

Le query sono un modo per accedere ai contenuti, ma non sono l’unica possibilità. In molte situazioni, si può accedere ai contenuti dell’archivio in modo più efficace con altri mezzi. Dovresti verificare se le query sono il modo migliore e più efficiente per accedere al contenuto nel caso d’uso.

### Struttura dell’archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, occorre tenere conto di diversi fattori, tra cui: controlli di accesso, localizzazione, ereditarietà di componenti e proprietà di pagina e altro ancora.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la “fruibilità” del design di indicizzazione. In questo contesto, la fruibilità è la capacità di una tassonomia di consentire l’accesso prevedibile ai contenuti in base al relativo percorso. Questo garantisce un sistema più efficiente e più semplice da gestire rispetto a uno che richiede l’esecuzione di più query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l’importanza dell’ordinamento. Nei casi in cui non è richiesto un ordinamento esplicito e si prevede un numero elevato di nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesto l’ordinamento, `nt:unstructured` e `sling:OrderedFolder` potrebbero essere più adatti.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni più gravose su un sistema AEM, è consigliabile evitarle nei componenti. Spesso, l’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l’esecuzione di query durante il rendering dei componenti: **[navigazione dei nodi](#traversing-nodes)** e **[preacquisizione dei risultati.](#prefetching-results)**

### Navigazione dei nodi {#traversing-nodes}

Se l’archivio è progettato in modo da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera tali dati dai percorsi necessari può essere distribuito senza dover eseguire query per trovarli.

Un esempio potrebbe essere il rendering di contenuti che rientrano a una determinata categoria. Un approccio consiste nell’organizzare i contenuti con una proprietà di categoria su cui è possibile eseguire una query per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nello strutturare i contenuti in una tassonomia per categoria, in modo da poterli recuperare manualmente.

Ad esempio, se il contenuto viene memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

il `/content/myUnstructuredContent/parentCategory/childCategory` nodo può essere semplicemente recuperato, i relativi nodi secondari possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, navigare l’archivio e raccogliere i nodi richiesti può essere una soluzione più veloce rispetto alla creazione di una query per restituire lo stesso set di risultati. In generale, occorre evitare le query laddove possibile.

### Preacquisizione dei risultati {#prefetching-results}

A volte il contenuto o i requisiti relativi al componente non consentono l’uso della navigazione dei nodi come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query obbligatorie prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto cambi, la query può essere eseguita dopo aver apportato una modifica.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita secondo una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Dopodiché, i risultati possono essere scritti in una posizione condivisa nell’archivio. Tutti i componenti che necessitano di questi dati possono quindi richiamare i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

Una strategia simile può essere utilizzata per mantenere il risultato in una cache in memoria, che viene popolata all’avvio e aggiornata ogni volta che vengono apportate modifiche (utilizzando `ObservationListener` JCR o `ResourceChangeListener` Sling).

## Ottimizzazione delle query {#optimizing-queries}

La documentazione Oak fornisce una [panoramica di alto livello sulle modalità di esecuzione delle query.](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) Questo costituisce la base di tutte le attività di ottimizzazione descritte nel presente documento.

AEM as a Cloud Service fornisce lo strumento Prestazioni query, progettato per supportare l’implementazione di query efficienti.

* Vengono visualizzate le query già eseguite con le relative caratteristiche di prestazione e la pianificazione delle query.
* Consente l’esecuzione di query ad-hoc a vari livelli, a partire dalla semplice visualizzazione della pianificazione delle query, fino all’esecuzione della query completa.

Lo strumento Prestazioni query è raggiungibile tramite la [Console per sviluppatori in Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it#queries) Lo strumento Prestazioni query di AEM as a Cloud Service fornisce ulteriori informazioni sui dettagli dell’esecuzione della query sulla versione 6.x di AEM.

Questo grafico illustra il flusso generale da utilizzare per ottimizzare le query con lo strumento Prestazioni query.

![Flusso di ottimizzazione query](assets/query-optimization-flow.png)

### Utilizzare un indice {#use-an-index}

Per fornire prestazioni ottimali, ogni query deve utilizzare un indice. Nella maggior parte dei casi, gli indici predefiniti esistenti dovrebbero essere sufficienti per gestire le query.

A volte è necessario aggiungere proprietà personalizzate a un indice esistente, in modo che sia possibile eseguire query sui vincoli aggiuntivi utilizzando l’indice. Per ulteriori dettagli, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#changing-an-index). Il [Scheda di riferimento rapido per le query JCR](#jcr-query-cheatsheet) sezione di questo documento descrive come deve essere visualizzata una definizione di proprietà in un indice per supportare un tipo di query specifico.

### Utilizzare i criteri giusti {#use-the-right-criteria}

Il vincolo principale su qualsiasi query deve essere una corrispondenza di proprietà, in quanto questo è il tipo più efficiente. L’aggiunta di più vincoli di proprietà limita ulteriormente il risultato.

Il motore di query considera solo un singolo indice. Ciò significa che un indice esistente può e deve essere personalizzato aggiungendovi proprietà di indice più personalizzate.

Nella sezione [Scheda di riferimento rapido per le query JCR](#jcr-query-cheatsheet) di questo documento sono elencati i vincoli disponibili e inoltre viene illustrato come la definizione di un indice deve essere visualizzata per essere selezionata. Utilizza lo [Strumento Prestazioni query](#query-performance-tool) per verificare la query e assicurarti che sia utilizzato l’indice corretto e che il motore di query non debba valutare i vincoli al di fuori dell’indice.

### Ordinamento {#ordering}

Se viene richiesto un ordinamento specifico del risultato, esistono due opzioni per ottenerlo da parte del motore di query:

1. L’indice può fornire il risultato completo e nell’ordine giusto.
   * Questa opzione funziona se le proprietà utilizzate per l’ordinamento vengono annotate con `ordered=true` nella definizione dell’indice.
1. Il motore di query esegue il processo di ordinamento.
   * Ciò può verificarsi quando il motore di query esegue il filtro all’esterno dell’indice oppure la proprietà di ordinamento non viene annotata con la proprietà `ordered=true`.
   * Questa opzione richiede che il set di risultati completo venga letto in memoria per l’ordinamento che è un processo molto più lento rispetto alla prima opzione.

### Limitare le dimensioni dei risultati {#restrict-result-size}

La dimensione recuperata del risultato della query è un fattore importante nelle prestazioni della query. Poiché il risultato viene recuperato in modo più lento, esiste una differenza nel recupero dei primi 20 risultati rispetto al recupero di 10.000 risultati, sia nella fase di esecuzione che nell’utilizzo della memoria.

Ciò significa anche che le dimensioni del set di risultati possono essere determinate correttamente solo se tutti i risultati vengono recuperati. Per questo motivo, il set di risultati recuperato deve sempre essere limitato, sia incrementando la query (per i dettagli, consulta la sezione [Scheda di riferimento rapido per le query JCR](#jcr-query-cheatsheet) del presente documento) o limitando la lettura dei risultati.

Tale limite impedisce inoltre al motore di query di raggiungere il **limite trasversale** di 100.000 nodi, che comporta un arresto forzato della query.

Se deve essere elaborato completamente un set di risultati potenzialmente di grandi dimensioni, consulta la sezione [Query con risultati di grandi dimensioni](#queries-with-large-result-sets) di questo documento.

## Scheda di riferimento rapido per le query JCR {#jcr-query-cheatsheet}

Per supportare la creazione di query JCR e le definizioni degli indici efficienti, la [Scheda di riferimento rapido per le query JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=it#jcrquerycheatsheet) è disponibile per il download e l’utilizzo come riferimento durante lo sviluppo.

Contiene query di esempio per QueryBuilder, XPath e SQL-2 comprendendo scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre consigli su come creare o personalizzare gli indici Oak. Il contenuto di questa Scheda di riferimento rapido si applica a AEM as a Cloud Service e a AEM 6.5.

## Query con set di risultati di grandi dimensioni {#queries-with-large-result-sets}

Anche se si consiglia di evitare le query con set di risultati di grandi dimensioni, ci sono casi validi in cui è necessario elaborarli. Spesso le dimensioni del risultato non possono essere note subito, quindi si devono prendere alcune precauzioni per rendere affidabile l’elaborazione.

* La query non deve essere eseguita all’interno di una richiesta. La query deve invece essere eseguita come parte di un processo Sling oppure di un flusso di lavoro AEM. Essi non hanno limitazioni nella fase di esecuzione totale e vengono riavviati nel caso in cui l’istanza si abbassi durante l’elaborazione della query e dei relativi risultati.
* Per superare il limite di query di 100.000 nodi, è consigliabile utilizzare [Paginazione keyset](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) e suddividere la query in più sottoquery.

## Archivio trasversale {#repository-traversal}

Le query che attraversano l’archivio non utilizzano un indice e si registrano con un messaggio simile al seguente.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Con questo frammento di log puoi determinare:

* La query stessa: `//*`
* Il codice Java che ha eseguito questa query: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` per aiutare a identificare l’autore della query.

Con queste informazioni, è possibile ottimizzare questa query utilizzando i metodi descritti nella sezione [Ottimizzazione delle query](#optimizing-queries) di questo documento.
