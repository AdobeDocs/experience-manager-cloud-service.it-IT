---
title: Ottimizzazione delle query GraphQL
description: Scopri come ottimizzare le query GraphQL durante l’applicazione di filtri, paging e ordinamento di frammenti di contenuto in Adobe Experience Manager as a Cloud Service per la distribuzione headless di contenuti.
source-git-commit: e156ed7348815e02c942cb8feace70c675956752
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# Ottimizzazione delle query GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Prima di applicare queste raccomandazioni di ottimizzazione, considera [Aggiornamento dei frammenti di contenuto per la gestione delle pagine e l’ordinamento in GraphQL Filtering](/help/headless/graphql-api/graphql-paging-sorting-content-update.md) per prestazioni migliori.

In un’istanza AEM con un numero elevato di frammenti di contenuto che condividono lo stesso modello, le query di elenco GraphQL possono diventare costose (in termini di risorse).

Questo perché *tutto* i frammenti che condividono un modello utilizzato nella query GraphQL devono essere caricati in memoria. Questo consuma sia tempo che memoria. Il filtro, che può ridurre il numero di elementi nel set di risultati (finale), può essere applicato solo **dopo** caricamento dell&#39;intero set di risultati in memoria.

Questo può dare l’impressione che anche piccoli set di risultati (possono) portino a prestazioni sbagliate. Tuttavia, in realtà la lentezza è causata dalla dimensione del set di risultati iniziali, in quanto deve essere gestito internamente prima di poter applicare il filtro.

Per ridurre i problemi di prestazioni e memoria, questo set di risultati iniziale deve essere mantenuto il più piccolo possibile.

AEM fornisce due approcci per l’ottimizzazione delle query GraphQL:

* [Filtro ibrido](#hybrid-filtering)
* [Paging](#paging) (o impaginazione)

   * [Ordinamento](#sorting) non è direttamente correlato all’ottimizzazione, ma è correlato al paging

Ogni approccio ha i propri casi d’uso e limitazioni. Questo documento fornisce informazioni su Filtro ibrido e Paging, con alcune [best practice](#best-practices) per ottimizzare le query GraphQL.

## Filtro ibrido {#hybrid-filtering}

Il filtro ibrido combina il filtro JCR con il filtro AEM.

Applica un filtro JCR (sotto forma di un vincolo di query) prima di caricare il set di risultati in memoria per AEM filtro. Questo per ridurre il set di risultati caricato in memoria, in quanto il filtro JCR rimuove i risultati superflui prima di questo.

>[!NOTE]
>
>Per motivi tecnici (ad esempio flessibilità, nidificazione dei frammenti), AEM non può delegare l’intero filtro a JCR.

Questa tecnica mantiene la flessibilità fornita dai filtri GraphQL, delegando al contempo il maggior numero possibile di filtri a JCR.

## Paging {#paging}

GraphQL in AEM supporta due tipi di impaginazione:

* [impaginazione basata su limiti/offset](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Viene utilizzato per le query di elenco; queste finiscono con 
`List`; ad esempio, `articleList`.
Per utilizzarlo, è necessario specificare la posizione del primo elemento da restituire (il `offset`) e il numero di elementi da restituire (il `limit`, o dimensioni della pagina).

* [impaginazione basata su cursore](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (rappresentanti: `first`e `after`) Fornisce un ID univoco per ogni elemento; anche noto come cursore.
Nella query, specificare il cursore dell’ultimo elemento della pagina precedente, oltre alla dimensione della pagina (il numero massimo di elementi da restituire).

   Poiché l’impaginazione basata su cursore non si adatta alle strutture di dati delle query basate su elenchi, AEM introdotto `Paginated` tipo di query; ad esempio, `articlePaginated`. Le strutture di dati e i parametri utilizzati seguono la [Specifiche di connessione del cursore GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM supporta attualmente il paging in avanti (utilizzando `after`/`first` ).
   >
   >Pagamento precedente (utilizzando `before`/`last` ) non è supportato.

## Ordinamento {#sorting}

L’ordinamento può essere efficiente solo se tutti i criteri di ordinamento sono correlati ai frammenti di livello principale.

Se l’ordinamento include uno o più campi situati in un frammento nidificato, tutti i frammenti che condividono il modello di livello superiore devono essere caricati in memoria. Questo causa un impatto negativo sulle prestazioni.

>[!NOTE]
>
>Anche l’ordinamento su campi di primo livello ha un impatto (anche se ridotto) sulle prestazioni.

## Best practice   {#best-practices}

L&#39;obiettivo principale di tutte le ottimizzazioni è quello di ridurre il set di risultati iniziale. Le best practice qui elencate forniscono i modi per farlo. Possono (e devono) essere combinati.

### Filtrare solo sulle proprietà di primo livello {#filter-top-level-properties-only}

Attualmente, il filtro a livello JCR funziona solo per i frammenti di livello superiore.

Se un filtro riguarda i campi di un frammento nidificato, AEM deve tornare al caricamento (nella memoria) di tutti i frammenti che condividono il modello sottostante.

È comunque possibile ottimizzare tali query GraphQL combinando le espressioni filtro nei campi dei frammenti di livello principale e in quelli nei campi dei frammenti nidificati con [Operatore AND](#logical-operations-in-filter-expressions).

### Utilizzare la struttura del contenuto {#use-content-structure}

In AEM, è generalmente considerata buona prassi utilizzare la struttura dell’archivio per limitare l’ambito del contenuto da elaborare.

Questo approccio dovrebbe essere applicato anche alle query GraphQL.

A tale scopo, puoi applicare un filtro al `_path` campo del frammento di livello principale:

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
>Il trailing `/` su `value` è necessario per ottenere le migliori prestazioni.

### Usa paging {#use-paging}

È inoltre possibile utilizzare il paging per ridurre il set di risultati iniziale; specialmente se le richieste non utilizzano filtri e ordinamento.

Se si filtra o si esegue l’ordinamento sui frammenti nidificati, le query impaginate possono essere ancora lente, in quanto potrebbe AEM comunque necessario caricare in memoria grandi quantità di frammenti. Pertanto, se combini filtro e paging, considera le regole per il filtro (come indicato sopra).

Per il paging, l&#39;ordinamento è ugualmente importante, in quanto i risultati impaginati vengono sempre ordinati in modo esplicito o implicito.

Se sei principalmente interessato a recuperare solo le prime pagine, non c&#39;è differenza significativa tra l&#39;utilizzo del `...List` o `...Paginated` query. Tuttavia, se l&#39;applicazione è interessata a leggere più di una o due pagine, è necessario considerare la `...Paginated` , in quanto offre prestazioni notevolmente migliori con le pagine successive.

### Operazioni logiche nelle espressioni filtro {#logical-operations-in-filter-expressions}

Se filtri su frammenti nidificati, puoi comunque sfruttare il filtro JCR fornendo un filtro di accompagnamento su un campo di primo livello combinato utilizzando `AND` operatore.

Un caso d’uso tipico consiste nel limitare l’ambito della query utilizzando un filtro nella `_path` del frammento principale, quindi filtrare campi aggiuntivi che potrebbero trovarsi al livello principale o in un frammento nidificato.

In questo caso, le diverse espressioni del filtro vengono combinate con `AND`. Pertanto, il filtro `_path` può limitare efficacemente il set di risultati iniziale. Tutti gli altri filtri nei campi di primo livello possono essere utili anche per ridurre il set di risultati iniziale, purché siano combinati con `AND`.

Espressioni filtro combinate con `OR` non può essere ottimizzata se sono coinvolti frammenti nidificati. `OR` le espressioni possono essere ottimizzate solo se *no* sono coinvolti frammenti nidificati.

### Evitare di filtrare su più righe campi di testo {#avoid-filtering-multiline-textfields}

I campi di un campo di testo su più righe (html, markdown, plaintext, json) non possono essere filtrati tramite una query JCR, in quanto il contenuto di questi campi deve essere calcolato immediatamente.

Se è ancora necessario filtrare un campo di testo a più righe, è consigliabile limitare la dimensione del set di risultati iniziale aggiungendo ulteriori espressioni di filtro e combinarle con `AND`. Limitazione dell’ambito filtrando l’elemento `_path` anche il settore è un buon approccio.

### Evitare di filtrare i campi virtuali {#avoid-filtering-virtual-fields}

Campi virtuali (la maggior parte dei campi inizia con `_`) viene calcolata durante l’esecuzione di una query GraphQL e pertanto non rientra nell’ambito del filtro basato su JCR.

Un&#39;eccezione importante è la `_path` , che può essere utilizzato in modo efficace per ridurre le dimensioni del set di risultati iniziale, se il contenuto è strutturato di conseguenza (vedi [Utilizzare la struttura del contenuto](#use-content-structure)).

### Filtro: Esclusioni {#filtering-exclusions}

Ci sono diverse altre situazioni in cui un&#39;espressione di filtro non può essere valutata a livello JCR (e quindi dovrebbe essere evitata per ottenere le migliori prestazioni):

* Filtrare le espressioni in un `Float` che utilizzano `_sensitiveness` opzione filtro, e dove `_sensitiveness` è impostato su un valore diverso da `0.0` .

* Filtrare le espressioni in un `String` utilizzando `_ignoreCase` opzione filtro.

* Filtro su `null` valori.

* Filtri per gli array con `_apply: ALL_OR_EMPTY`.

* Filtri per gli array con `_apply: INSTANCES`, `_instances: 0`.

* Filtra le espressioni utilizzando `CONTAINS_NOT` operatore.

* Filtrare le espressioni in un `Calendar`, `Date` o `Time` che utilizzano `NOT_AT` operatore.
