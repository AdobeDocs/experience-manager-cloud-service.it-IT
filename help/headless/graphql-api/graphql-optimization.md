---
title: Ottimizzazione delle query GraphQL
description: Scopri come ottimizzare le query GraphQL per il filtro, il paging e l’ordinamento dei frammenti di contenuto in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
exl-id: 67aec373-4e1c-4afb-9c3f-a70e463118de
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 100%

---

# Ottimizzazione delle query GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Prima di applicare questi consigli di ottimizzazione, prova l’[Aggiornamento dei frammenti di contenuto per il paging e l’ordinamento nel filtro GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) per prestazioni ottimali.

In un’istanza AEM con un numero elevato di frammenti di contenuto che condividono lo stesso modello, le query di elenco GraphQL possono diventare costose (in termini di risorse).

Questo perché devono essere caricati in memoria *tutti* i frammenti che condividono un modello utilizzato all’interno della query GraphQL. Ciò richiede tempo e memoria. Il filtro, che può ridurre il numero di elementi nel set di risultati (finale), può essere applicato solo **dopo** il caricamento dell’intero set di risultati in memoria.

Questo può dare l’impressione che anche piccoli set di risultati portino a cattive prestazioni. Tuttavia, in realtà la lentezza è causata dalle dimensioni del set di risultati iniziale, in quanto deve essere gestito internamente prima di poter applicare il filtro.

Per ridurre i problemi di prestazioni e memoria, il set di risultati iniziale deve essere ridotto il più possibile.

AEM consente due approcci per ottimizzare le query GraphQL:

* [Filtro ibrido](#hybrid-filtering)
* [Paging](#paging) (o impaginazione)

   * [Ordinamento](#sorting) non è direttamente correlato all’ottimizzazione, ma è correlato al paging

Ogni approccio ha i propri casi d’uso e limitazioni. Questo documento fornisce informazioni su Filtro ibrido e Paging, con alcune [best practice](#best-practices) per ottimizzare le query GraphQL.

## Filtro ibrido {#hybrid-filtering}

Il filtro ibrido combina il filtro JCR con il filtro AEM.

Un filtro JCR viene applicato (sotto forma di vincolo di query) prima di caricare il set di risultati in memoria per il filtro AEM. In questo modo si riduce il set di risultati caricato in memoria, dato che il filtro JCR rimuove i risultati superflui precedenti.

>[!NOTE]
>
>Per motivi tecnici (ad esempio flessibilità, nidificazione di frammenti), AEM non può delegare l’intera operazione di filtro a JCR.

Questa tecnica mantiene la flessibilità fornita dai filtri GraphQL, delegando la maggior parte del filtro possibile a JCR.

## Paging {#paging}

GraphQL in AEM supporta due tipi di impaginazione:

* [paginazione basata su limite/offset](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Viene utilizzata per le query elenco; queste terminano con 
`List`; per esempio, `articleList`.
Per utilizzarlo, devi fornire la posizione del primo elemento da restituire (il `offset`) e il numero di elementi da restituire (il `limit`, o dimensioni della pagina).

* [paginazione basata su cursore](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (rappresentato da `first` e `after`)
Fornisce un ID univoco per ciascun elemento, noto anche come cursore.
Nella query, si specifica il cursore dell’ultimo elemento della pagina precedente, più le dimensioni della pagina (il numero massimo di elementi da restituire).

   Poiché l’impaginazione basata su cursore non si adatta alle strutture di dati delle query basate su elenco, AEM ha introdotto il tipo di query `Paginated`; ad esempio, `articlePaginated`. Le strutture di dati e i parametri utilizzati seguono i [Specifica di connessione cursore GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM attualmente supporta il paging in avanti (utilizzando i parametri `after`/`first`).
   >
   >Il paging all’indietro (utilizzando `before`/`last`) non è supportato.

## Ordinamento {#sorting}

L’ordinamento può essere efficiente solo se tutti i criteri di ordinamento sono correlati ai frammenti di primo livello.

Se l’ordinamento include uno o più campi che si trovano su un frammento nidificato, tutti i frammenti che condividono il modello di livello principale devono essere caricati in memoria. Questo causa un impatto negativo sulle prestazioni.

>[!NOTE]
>
>L’ordinamento sui campi di livello superiore ha anche un impatto sulle prestazioni, seppure ridotto.

## Best practice {#best-practices}

L’obiettivo principale di tutte le ottimizzazioni è ridurre il set di risultati iniziale. Le best practice elencate di seguito indicano come farlo. Possono (e devono) essere combinate.

### Filtrare solo le proprietà di livello superiore {#filter-top-level-properties-only}

Attualmente, il filtro a livello JCR funziona solo per i frammenti di livello superiore.

Se un filtro comprende i campi di un frammento nidificato, AEM deve ricorrere al caricamento (nella memoria) di tutti i frammenti che condividono il modello sottostante.

Puoi comunque ottimizzare tali query GraphQL combinando espressioni filtro su campi di frammenti di primo livello e su campi di frammenti nidificati con l’[operatore AND](#logical-operations-in-filter-expressions).

### Utilizzare la struttura del contenuto {#use-content-structure}

In AEM, si ritiene generalmente buona prassi utilizzare la struttura dell’archivio per restringere l’ambito dei contenuti da elaborare.

Questo approccio deve essere applicato anche alle query GraphQL.

A questo scopo, puoi applicare un filtro sul campo `_path` del frammento di livello principale:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>Il finale `/` su `value` è necessario per ottenere le migliori prestazioni.

### Usare il paging {#use-paging}

È inoltre possibile utilizzare il paging per ridurre il set di risultati iniziale, in particolare se le richieste non utilizzano alcun filtro e ordinamento.

Se si filtra o si ordina in base a frammenti nidificati, le query impaginate possono ancora risultare lente, in quanto l’AEM potrebbe dover ancora caricare in memoria grandi quantità di frammenti. Pertanto, se combini filtri e paging, tieni in considerazione le regole per il filtraggio (come indicato sopra).

Per il paging, l’ordinamento è ugualmente importante, in quanto i risultati impaginati vengono sempre ordinati in modo esplicito o implicito.

Se sei principalmente interessato a recuperare solo le prime pagine, non vi è alcuna differenza significativa tra l’utilizzo le query `...List` o `...Paginated`. Tuttavia, se l’applicazione è interessata a leggere più di una o due pagine, è necessario considerare la query `...Paginated` , poiché offre prestazioni notevolmente migliori con le pagine successive.

### Operazioni logiche nelle espressioni di filtro {#logical-operations-in-filter-expressions}

Se esegui il filtro su frammenti nidificati, puoi comunque sfruttare il filtro JCR fornendone uno correlato su un campo di livello principale combinato utilizzando l’operatore `AND`.

Un caso d’uso tipico è quello di limitare l’ambito della query utilizzando un filtro sul campo `_path` del frammento di livello principale, per poi applicare un filtro ai campi aggiuntivi che potrebbero trovarsi nel livello principale o in un frammento nidificato.

In questo caso, le diverse espressioni di filtro vengono combinate con `AND`. Pertanto, il filtro su `_path` può limitare efficacemente il set di risultati iniziale. Tutti gli altri filtri sui campi di livello superiore possono aiutare a ridurre il set di risultati iniziale, purché siano combinati con `AND`.

Le espressioni di filtro combinate con `OR` non possono essere ottimizzate se sono interessati dei frammenti nidificati. Le espressioni `OR` possono essere ottimizzate solo se *nessun* frammento nidificato è coinvolto.

### Evitare di filtrare i campi di testo su più righe {#avoid-filtering-multiline-textfields}

I campi di un campo di testo multiriga (html, markdown, testo semplice, JSON) non possono essere filtrati tramite una query JCR, in quanto il contenuto di tali campi deve essere calcolato al volo.

Se devi ancora filtrare un campo di testo multiriga, prova a limitare la dimensione del set di risultati iniziale aggiungendo ulteriori espressioni di filtro e combinale con `AND`. Limitare l’ambito filtrando sul campo `_path` è un altro buon approccio.

### Evitare di filtrare i campi virtuali {#avoid-filtering-virtual-fields}

I campi virtuali (la maggior parte dei campi inizia con `_`) vengono calcolati durante l’esecuzione di una query GraphQL e non rientrano pertanto nell’ambito del filtro basato su JCR.

Un’eccezione importante è il campo `_path`, che può essere utilizzato in modo efficace per ridurre le dimensioni del set di risultati iniziale, se il contenuto è strutturato di conseguenza (vedi [Utilizzare la struttura del contenuto](#use-content-structure)).

### Filtro: esclusioni {#filtering-exclusions}

Ci sono molte altre situazioni in cui un’espressione di filtro non può essere valutata a livello JCR (e quindi deve essere evitata per ottenere le migliori prestazioni):

* Espressioni di filtro su un valore `Float` che utilizzano l’opzione filtro `_sensitiveness` e dove `_sensitiveness` è impostato su un valore diverso da `0.0`.

* Espressioni di filtro sul valore `String` che utilizzano l’opzione filtro `_ignoreCase`.

* Filtro sui valori `null`.

* Filtri su array con `_apply: ALL_OR_EMPTY`.

* Filtri su array con `_apply: INSTANCES`, `_instances: 0`.

* Espressioni di filtro che utilizzano l’operatore `CONTAINS_NOT`.

* Espressioni di filtro su un valore `Calendar`, `Date` o `Time` che utilizza l’operatore `NOT_AT`.
