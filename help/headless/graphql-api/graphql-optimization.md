---
title: Ottimizzazione delle query GraphQL
description: Scopri come ottimizzare le query GraphQL per filtrare, impaginare e ordinare i frammenti di contenuto in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
source-git-commit: cda6d7e382b090fd726b27e565da08c8b1c80008
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# Ottimizzazione delle query GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Prima di applicare queste raccomandazioni di ottimizzazione, considera [Aggiornamento dei frammenti di contenuto per il paging e l’ordinamento nel filtro GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) per prestazioni ottimali.

In un’istanza AEM con un numero elevato di frammenti di contenuto che condividono lo stesso modello, le query di elenco GraphQL possono diventare costose (in termini di risorse).

Questo perché *tutto* i frammenti che condividono un modello utilizzato all’interno della query GraphQL devono essere caricati in memoria. Ciò richiede tempo e memoria. Il filtro, che può ridurre il numero di elementi nel set di risultati (finale), può essere applicato solo **dopo** caricamento dell&#39;intero set di risultati in memoria.

Questo può portare all’impressione che anche piccoli set di risultati (possono) portino a cattive prestazioni. Tuttavia, in realtà la lentezza è causata dalle dimensioni del set di risultati iniziale, in quanto deve essere gestito internamente prima di poter applicare il filtro.

Per ridurre i problemi di prestazioni e memoria, questo set di risultati iniziale deve essere ridotto il più possibile.

L’AEM fornisce due approcci per ottimizzare le query GraphQL:

* [Filtro ibrido](#hybrid-filtering)
* [Paging](#paging) (o impaginazione)

   * [Ordinamento](#sorting) non è direttamente correlato all’ottimizzazione, ma è correlato al paging

Ogni approccio ha i propri casi d’uso e limitazioni. Questo documento fornisce informazioni su Filtro e paging ibridi, con alcuni [best practice](#best-practices) per ottimizzare le query GraphQL.

## Filtro ibrido {#hybrid-filtering}

Il filtro ibrido combina il filtro JCR con il filtro AEM.

Applica un filtro JCR (sotto forma di vincolo di query) prima di caricare il set di risultati in memoria per il filtro AEM. In questo modo si riduce il set di risultati caricato in memoria, in quanto il filtro JCR rimuove i risultati superflui precedenti.

>[!NOTE]
>
>Per motivi tecnici (ad esempio flessibilità, nidificazione di frammenti), l’AEM non può delegare l’intero filtro al JCR.

Questa tecnica mantiene la flessibilità fornita dai filtri GraphQL, delegando la maggior parte del filtro possibile a JCR.

## Paging {#paging}

GraphQL nell’AEM supporta due tipi di impaginazione:

* [paginazione basata su limite/scostamento](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Viene utilizzato per le query elenco; queste terminano con 
`List`ad esempio, `articleList`.
Per utilizzarlo, devi fornire la posizione del primo elemento da restituire (il `offset`) e il numero di elementi da restituire (il `limit`, o dimensioni della pagina).

* [paginazione basata su cursore](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (rappresentante: `first`e `after`) Fornisce un ID univoco per ciascun elemento, noto anche come cursore.
Nella query, si specifica il cursore dell&#39;ultimo elemento della pagina precedente, più le dimensioni della pagina (il numero massimo di elementi da restituire).

   Poiché l’impaginazione basata su cursore non si adatta alle strutture di dati delle query basate su elenco, l’AEM ha introdotto `Paginated` tipo di query; ad esempio, `articlePaginated`. Le strutture di dati e i parametri utilizzati seguono i [Specifica connessione cursore GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM attualmente supporta il paging in avanti (utilizzando `after`/`first` parametri).
   >
   >Paging all&#39;indietro (utilizzando `before`/`last` ) non è supportato.

## Ordinamento {#sorting}

L’ordinamento può essere efficiente solo se tutti i criteri di ordinamento sono correlati ai frammenti di primo livello.

Se l’ordinamento include uno o più campi che si trovano su un frammento nidificato, tutti i frammenti che condividono il modello di livello principale devono essere caricati in memoria. Questo causa un impatto negativo sulle prestazioni.

>[!NOTE]
>
>L’ordinamento sui campi di livello superiore ha anche un impatto sulle prestazioni, anche se ridotto.

## Best practice   {#best-practices}

L’obiettivo principale di tutte le ottimizzazioni è ridurre il set di risultati iniziale. Le best practice elencate di seguito forniscono i modi per farlo. Possono (e devono) essere combinate.

### Filtra solo sulle proprietà di livello superiore {#filter-top-level-properties-only}

Attualmente, il filtro a livello JCR funziona solo per i frammenti di livello superiore.

Se un filtro si rivolge ai campi di un frammento nidificato, l’AEM deve ricorrere al caricamento (nella memoria) di tutti i frammenti che condividono il modello sottostante.

Puoi comunque ottimizzare tali query GraphQL combinando espressioni filtro su campi di frammenti di primo livello e su campi di frammenti nidificati con [Operatore AND](#logical-operations-in-filter-expressions).

### Utilizzare la struttura del contenuto {#use-content-structure}

Nell&#39;AEM, si ritiene generalmente buona prassi utilizzare la struttura dell&#39;archivio per restringere l&#39;ambito dei contenuti da elaborare.

Questo approccio deve essere applicato anche alle query GraphQL.

A questo scopo, puoi applicare un filtro sulla `_path` campo del frammento di livello principale:

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
>Il finale `/` il `value` per ottenere le migliori prestazioni.

### Usa paging {#use-paging}

È inoltre possibile utilizzare la paginazione per ridurre il set di risultati iniziale, in particolare se le richieste non utilizzano alcun filtro e ordinamento.

Se si filtra o si ordina in base a frammenti nidificati, le query impaginate possono risultare ancora lente, in quanto l’AEM potrebbe dover ancora caricare in memoria grandi quantità di frammenti. Pertanto, se combini filtraggio e paging, considera le regole per il filtraggio (come indicato sopra).

Per il paging, l’ordinamento è ugualmente importante, in quanto i risultati impaginati vengono sempre ordinati in modo esplicito o implicito.

Se sei principalmente interessato a recuperare solo le prime pagine, non vi è alcuna differenza significativa tra l’utilizzo di `...List` o `...Paginated` query. Tuttavia, se l’applicazione è interessata a leggere più di una o due pagine, è necessario considerare `...Paginated` , poiché offre prestazioni notevolmente migliori con le pagine successive.

### Operazioni logiche nelle espressioni filtro {#logical-operations-in-filter-expressions}

Se esegui il filtro su frammenti nidificati, puoi comunque sfruttare il filtro JCR fornendo un filtro correlato su un campo di livello principale combinato utilizzando `AND` operatore.

Un caso d’uso tipico è quello di limitare l’ambito della query utilizzando un filtro su `_path` del frammento di livello principale, quindi applica un filtro ai campi aggiuntivi che potrebbero trovarsi nel livello principale o in un frammento nidificato.

In questo caso, le diverse espressioni di filtro vengono combinate con `AND`. Pertanto, il filtro su `_path` può limitare efficacemente il set di risultati iniziale. Tutti gli altri filtri sui campi di livello superiore possono aiutare a ridurre il set di risultati iniziale, purché siano combinati con `AND`.

Filtrare le espressioni combinate con `OR` non può essere ottimizzato se sono interessati frammenti nidificati. `OR` le espressioni possono essere ottimizzate solo se *no* sono coinvolti frammenti nidificati.

### Evita di filtrare i campi di testo su più righe {#avoid-filtering-multiline-textfields}

I campi di un campo di testo multiriga (html, markdown, testo normale, json) non possono essere filtrati tramite una query JCR, in quanto il contenuto di tali campi deve essere calcolato al volo.

Se devi ancora filtrare in base a un campo di testo multiriga, prova a limitare la dimensione del set di risultati iniziale aggiungendo ulteriori espressioni di filtro e combinale con `AND`. Limitazione dell’ambito tramite filtraggio sul `_path` è un buon approccio.

### Evita di filtrare i campi virtuali {#avoid-filtering-virtual-fields}

Campi virtuali (la maggior parte dei campi inizia con `_`) vengono calcolati durante l’esecuzione di una query GraphQL e non rientrano pertanto nell’ambito del filtro basato su JCR.

Un&#39;eccezione importante è `_path` , che può essere utilizzato in modo efficace per ridurre le dimensioni del set di risultati iniziale, se il contenuto è strutturato di conseguenza (vedi [Utilizzare la struttura del contenuto](#use-content-structure)).

### Filtro: Esclusioni {#filtering-exclusions}

Ci sono diverse altre situazioni in cui un’espressione di filtro non può essere valutata a livello JCR (e quindi deve essere evitata per ottenere le migliori prestazioni):

* Filtrare le espressioni su una `Float` valore che utilizza il `_sensitiveness` opzione filtro e dove `_sensitiveness` è impostato su un valore diverso da `0.0` .

* Filtrare le espressioni su una `String` valore utilizzando `_ignoreCase` opzione filtro.

* Filtro attivato `null` valori.

* Filtri su array con `_apply: ALL_OR_EMPTY`.

* Filtri su array con `_apply: INSTANCES`, `_instances: 0`.

* Filtrare le espressioni utilizzando `CONTAINS_NOT` operatore.

* Filtrare le espressioni su una `Calendar`, `Date` o `Time` valore che utilizza il `NOT_AT` operatore.
