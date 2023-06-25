---
title: Memorizzazione in cache e prestazioni
description: Scopri le diverse configurazioni disponibili per abilitare GraphQL e il caching dei contenuti per ottimizzare le prestazioni dell’implementazione di e-commerce.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: afbcd1e50a12a9b0642c586d7d81bb90ea91a58d
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 44%

---

# Memorizzazione in cache e prestazioni {#caching}

## Memorizzazione in cache di risposta di componenti e GraphQL {#graphql}

I componenti core CIF di AEM dispongono già del supporto integrato necessario per memorizzare nella cache le risposte GraphQL per i singoli componenti. Questa funzione può essere utilizzata per ridurre notevolmente il numero di chiamate back-end di GraphQL. È possibile ottenere una memorizzazione efficace nella cache, in particolare per query ripetute come il recupero della struttura delle categorie per un componente di navigazione o il recupero di tutti i valori aggregati/facet disponibili visualizzati sulle pagine di ricerca di prodotto e categoria.

Per i componenti core CIF di AEM, la memorizzazione in cache è configurata in base al componente, quindi è possibile controllare se (e per quanto tempo) le richieste e le risposte GraphQL vengono memorizzate nella cache per ciascun componente. È inoltre possibile definire il comportamento di caching per i servizi OSGi utilizzando il client GraphQL.

### Configurazione {#configuration}

Una volta configurata per un determinato componente, la cache inizia a memorizzare le query e le risposte GraphQL in base a quanto definito da ciascuna voce per la configurazione della cache. La dimensione della cache e la durata della memorizzazione nella cache di ciascuna voce vengono definite in base al progetto, a seconda, ad esempio, dei seguenti elementi:

* Frequenza con cui i dati del catalogo possono cambiare.
* Quanto è importante che un componente visualizzi sempre i dati più recenti e così via.

Non è prevista alcuna invalidazione della cache, quindi occorre prestare attenzione quando si impostano le durate della cache.

Quando si configura la memorizzazione in cache per i componenti, il nome della cache deve corrispondere al nome dei componenti **proxy** definiti nel progetto.

Prima che il client invii una richiesta GraphQL, verifica se **esatto** la stessa richiesta GraphQL è già stata memorizzata nella cache ed è possibile che restituisca la risposta nella cache. Per trovare una corrispondenza, devi trovare la richiesta GraphQL _deve_ corrisponde esattamente. Ossia query, nome dell’operazione (se presente), variabili (se presenti) _deve_ essere tutti uguali alla richiesta memorizzata nella cache. E, tutte le intestazioni HTTP personalizzate che potrebbero essere impostate _deve_ anche essere lo stesso. Ad esempio, Adobe Commerce `Store` intestazione _deve_ corrisponde a.

### Esempi {#examples}

L’Adobe consiglia di configurare il caching per il servizio di ricerca che recupera tutti i valori aggregati/facet disponibili visualizzati nelle pagine di ricerca e categoria del prodotto. Questi valori in genere cambiano solo quando un nuovo attributo viene aggiunto ai prodotti, ad esempio. Pertanto, la durata di questa voce della cache può essere &quot;lunga&quot; se il set di attributi di prodotto non cambia spesso. Anche se questa voce è specifica per il progetto, Adobe consiglia valori di alcuni minuti nelle fasi di sviluppo del progetto e di alcune ore nei sistemi di produzione stabili.

Questa impostazione è in genere configurata con la seguente voce della cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Un altro scenario esemplificativo in cui si consiglia l’utilizzo della funzione di caching GraphQl è il componente di navigazione. Il motivo è che invia la stessa query GraphQL su tutte le pagine. In questo caso, la voce cache viene generalmente impostata su:

```
venia/components/structure/navigation:true:10:600
```

Considerando che il [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) viene utilizzato. Si noti l’uso del nome proxy del componente `venia/components/structure/navigation` e **non** del nome del componente di navigazione CIF (`core/cif/components/structure/navigation/v1/navigation`).

La memorizzazione nella cache per altri componenti deve essere definita in base al progetto, in genere in coordinamento con la memorizzazione nella cache configurata a livello di Dispatcher. Non è prevista l’invalidazione attiva di queste cache, pertanto la durata di memorizzazione nella cache deve essere impostata con attenzione. Non esiste un valore universale che vada bene per tutti i possibili progetti e casi di utilizzo. Occorre definire una strategia di caching a livello di progetto che corrisponda meglio ai requisiti del progetto.

## Memorizzazione in cache di Dispatcher {#dispatcher}

La memorizzazione nella cache di pagine o frammenti AEM in [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) è una best practice per qualsiasi progetto AEM. In genere, si basa su tecniche di invalidazione che garantiscono che qualsiasi contenuto modificato in AEM venga aggiornato correttamente in Dispatcher. Questa funzione è fondamentale per la strategia di caching del Dispatcher AEM.

Oltre al contenuto CIF puro gestito dall’AEM, una pagina può in genere visualizzare dati di e-commerce recuperati dinamicamente da Adobe Commerce tramite GraphQL. Anche se la struttura di pagina stessa potrebbe non cambiare mai, il contenuto dell’e-commerce potrebbe cambiare. Ad esempio, se i dati di prodotto, come nome e prezzo, cambiano in Adobe Commerce.

Per garantire che le pagine CIF siano memorizzate nella cache per un periodo di tempo limitato in AEM Dispatcher, l’Adobe consiglia di utilizzare [Annullamento della validità della cache in base al tempo](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) (nota come memorizzazione in cache basata su TTL) quando si memorizzano nella cache le pagine CIF in AEM Dispatcher. Questa funzione può essere configurata in AEM utilizzando il pacchetto [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) aggiuntivo.

Con il caching basato su TTL, uno sviluppatore definisce in genere una o più durate di memorizzazione nella cache per le pagine AEM selezionate. Questa durata garantisce che le pagine CIF vengano memorizzate nella cache solo nel Dispatcher AEM fino alla durata configurata e che il contenuto venga aggiornato di frequente.

>[!NOTE]
>
>Anche se i dati lato server possono essere memorizzati nella cache da Dispatcher AEM, alcuni componenti CIF come `product`, `productlist`, e `searchresults` i componenti in genere recuperano sempre i prezzi dei prodotti in una richiesta browser lato client quando la pagina viene caricata. In questo modo, al caricamento della pagina verranno sempre recuperati i contenuti dinamici fondamentali.

## Risorse aggiuntive {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Configurazione della cache per GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it)
