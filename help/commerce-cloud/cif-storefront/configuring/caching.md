---
title: Memorizzazione in cache e prestazioni
description: Scopri le diverse configurazioni disponibili per abilitare GraphQL e il caching dei contenuti per ottimizzare le prestazioni dell’implementazione di e-commerce.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 39%

---


# Memorizzazione in cache e prestazioni {#caching}

## Memorizzazione in cache di risposta di componenti e GraphQL {#graphql}

I componenti core CIF di AEM dispongono già del supporto incorporato necessario per memorizzare nella cache le risposte GraphQL per i singoli componenti. Questa funzione può essere utilizzata per ridurre notevolmente il numero di chiamate back-end di GraphQL. È possibile ottenere una memorizzazione efficace nella cache, in particolare per query ripetute come il recupero della struttura delle categorie per un componente di navigazione o il recupero di tutti i valori aggregati/facet disponibili visualizzati sulle pagine di ricerca di prodotto e categoria.

Per i componenti core CIF di AEM, la memorizzazione in cache è configurata in base al componente, quindi è possibile controllare se (e per quanto tempo) le richieste e le risposte GraphQL vengono memorizzate nella cache per ciascun componente. È inoltre possibile definire il comportamento di caching per i servizi OSGi utilizzando il client GraphQL.

### Configurazione {#configuration}

Una volta configurata per un determinato componente, la cache inizia a memorizzare le query e le risposte GraphQL in base a quanto definito da ciascuna voce per la configurazione della cache. La dimensione della cache e la durata della memorizzazione nella cache di ciascuna voce vengono definite in base al progetto, a seconda, ad esempio, dei seguenti elementi:

* Frequenza con cui i dati del catalogo possono cambiare.
* Quanto è importante che un componente visualizzi sempre i dati più recenti e così via.

Non è prevista alcuna invalidazione della cache, quindi occorre prestare attenzione quando si impostano le durate della cache.

Quando si configura la memorizzazione in cache per i componenti, il nome della cache deve corrispondere al nome dei componenti **proxy** definiti nel progetto.

Prima che il client invii una richiesta GraphQL, controlla se quella **esatta** stessa richiesta GraphQL è già stata memorizzata nella cache e potrebbe restituire la risposta nella cache. Per trovare una corrispondenza, la richiesta di GraphQL _deve_ corrispondere esattamente. In altre parole, la query, il nome dell&#39;operazione (se presente), le variabili (se presenti) _devono_ essere tutte uguali alla richiesta memorizzata nella cache. Inoltre, anche tutte le intestazioni HTTP personalizzate che potrebbero essere impostate _devono_ essere uguali. Ad esempio, l&#39;intestazione `Store` di Adobe Commerce _deve_ corrispondere.

### Esempi {#examples}

Adobe consiglia di configurare il caching per il servizio di ricerca che recupera tutti i valori aggregati/facet disponibili visualizzati nelle pagine di ricerca e categoria del prodotto. Questi valori in genere cambiano solo quando un nuovo attributo viene aggiunto ai prodotti, ad esempio. Pertanto, la durata di questa voce della cache può essere &quot;lunga&quot; se il set di attributi di prodotto non cambia spesso. Sebbene questa voce sia specifica per il progetto, Adobe consiglia valori di alcuni minuti nelle fasi di sviluppo del progetto e di alcune ore nei sistemi di produzione stabili.

Questa impostazione è in genere configurata con la seguente voce della cache:

```text
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Un altro scenario esemplificativo in cui si consiglia l’utilizzo della funzione di caching GraphQl è il componente di navigazione. Il motivo è che invia la stessa query GraphQL su tutte le pagine. In questo caso, la voce cache viene generalmente impostata su:

```text
venia/components/structure/navigation:true:10:600
```

Considerando che è utilizzato l&#39;[archivio riferimenti Venia](https://github.com/adobe/aem-cif-guides-venia). Si noti l’uso del nome proxy del componente `venia/components/structure/navigation` e **non** del nome del componente di navigazione CIF (`core/cif/components/structure/navigation/v1/navigation`).

La memorizzazione nella cache per altri componenti deve essere definita in base al progetto, in genere in coordinamento con la memorizzazione nella cache configurata a livello di Dispatcher. Non è prevista l’invalidazione attiva di queste cache, pertanto la durata della memorizzazione nella cache deve essere impostata con attenzione. Non esiste un valore universale che corrisponda a tutti i possibili progetti e casi d’uso. Occorre definire una strategia di caching a livello di progetto che corrisponda meglio ai requisiti del progetto.

## Memorizzazione in cache di Dispatcher {#dispatcher}

La memorizzazione nella cache di pagine o frammenti AEM in [AEM Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher) è una best practice per qualsiasi progetto AEM. In genere, si basa su tecniche di invalidazione che garantiscono che qualsiasi contenuto modificato in AEM venga aggiornato correttamente in Dispatcher. Questa funzione è fondamentale per la strategia di caching di AEM Dispatcher.

Oltre al contenuto CIF puro gestito da AEM, in una pagina possono in genere essere visualizzati i dati di e-commerce recuperati dinamicamente da Adobe Commerce tramite GraphQL. Anche se la struttura di pagina stessa potrebbe non cambiare mai, il contenuto dell’e-commerce potrebbe cambiare. Ad esempio, se i dati di prodotto, come nome e prezzo, cambiano in Adobe Commerce.

Per garantire che le pagine CIF vengano memorizzate nella cache per un periodo di tempo limitato in AEM Dispatcher, Adobe consiglia di utilizzare [l&#39;invalidazione della cache basata sul tempo](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-time-based-cache-invalidation-enablettl) (nota come memorizzazione in cache basata su TTL) durante il caching delle pagine CIF in AEM Dispatcher. Questa funzione può essere configurata in AEM utilizzando il pacchetto [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) aggiuntivo.

Con il caching basato su TTL, uno sviluppatore definisce in genere una o più durate di memorizzazione nella cache per le pagine AEM selezionate. Questa durata garantisce che le pagine CIF vengano memorizzate nella cache solo in AEM Dispatcher fino alla durata configurata e che il contenuto venga aggiornato di frequente.

>[!NOTE]
>
>Anche se i dati lato server possono essere memorizzati nella cache da AEM Dispatcher, alcuni componenti di CIF come `product`, `productlist` e `searchresults` in genere recuperano sempre i prezzi dei prodotti in una richiesta browser lato client quando la pagina viene caricata. In questo modo, al caricamento della pagina verranno sempre recuperati i contenuti dinamici fondamentali.

## Risorse aggiuntive {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Configurazione della cache per GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)
