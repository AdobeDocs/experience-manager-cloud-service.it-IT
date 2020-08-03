---
title: Cache e prestazioni
description: Cache e prestazioni
translation-type: tm+mt
source-git-commit: 2997a28e79b51e88ececbd46c81dbc6a6c443e68
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# Cache e prestazioni {#caching}

## Memorizzazione nella cache delle risposte di Component e GraphQL {#graphql}

I componenti core CIF AEM hanno già un supporto integrato per memorizzare nella cache le risposte GraphQL per i singoli componenti. Questa funzione può essere utilizzata per ridurre il numero di chiamate back-end GraphQL di un fattore di grandi dimensioni. È possibile ottenere una memorizzazione efficace nella cache, in particolare per query ripetute come il recupero della struttura delle categorie per un componente di navigazione o il recupero di tutti i valori aggregati/facet disponibili visualizzati sulle pagine di ricerca e categoria del prodotto.

Per i componenti AEM CIF di base, il caching è configurato su base di componente, quindi è possibile controllare se (e per quanto tempo) le richieste/risposte GraphQL vengono memorizzate nella cache per ciascun componente. È inoltre possibile definire il comportamento di caching per i servizi OSGi utilizzando il client GraphQL.

### Configurazione

Una volta configurato per un determinato componente, la cache inizia a memorizzare le query GraphQL e le risposte come definite da ciascuna voce di configurazione della cache. Le dimensioni della cache e la durata della memorizzazione nella cache di ciascuna voce devono essere definite in base al progetto, a seconda, ad esempio, della frequenza con cui i dati del catalogo possono cambiare, di quanto sia importante che un componente visualizzi sempre i dati più recenti, ecc. Notate che non esiste alcuna invalidazione della cache, quindi prestate attenzione quando impostate le durate della cache.

Quando si configura il caching per i componenti, il nome della cache deve essere il nome dei componenti **proxy** definiti nel progetto.

Prima che il client invii una richiesta GraphQL, verificherà se la **** stessa richiesta GraphQL è già stata memorizzata nella cache e potrebbe restituire la risposta nella cache. Per trovare una corrispondenza, la richiesta GraphQL DEVE corrispondere esattamente, ovvero la query, il nome dell&#39;operazione (se presente), le variabili (se presenti) DEVONO essere tutte uguali alla richiesta memorizzata nella cache, e anche tutte le intestazioni HTTP personalizzate che potrebbero essere impostate DEVONO essere uguali. Ad esempio, l&#39;intestazione dell&#39;Magento `Store` DEVE corrispondere.

### Esempi

È consigliabile configurare alcuni caching per il servizio di ricerca che raccoglie tutti i valori aggregati/facet disponibili visualizzati nelle pagine di ricerca e categoria del prodotto. Questi valori generalmente cambiano solo quando un nuovo attributo viene ad esempio aggiunto ai prodotti, pertanto la durata di questa voce della cache può essere &quot;grande&quot; se il set di attributi di prodotto non cambia spesso. Anche se si tratta di un progetto specifico, consigliamo valori di alcuni minuti nelle fasi di sviluppo del progetto e di alcune ore su sistemi di produzione stabili.

Questa configurazione è in genere configurata con la seguente voce della cache:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Un altro scenario di esempio in cui si consiglia di utilizzare la funzione di caching GraphQl è il componente di navigazione perché invia la stessa query GraphQL su tutte le pagine. In questo caso, la voce della cache viene generalmente impostata su:

```
venia/components/structure/navigation:true:10:600
```

quando si prende in considerazione il negozio [](https://github.com/adobe/aem-cif-guides-venia) Venia Reference. Osservate l’uso del nome proxy del componente `venia/components/structure/navigation`e **non** del nome del componente di navigazione CIF (`core/cif/components/structure/navigation/v1/navigation`).

La memorizzazione nella cache per altri componenti deve essere definita a livello di progetto, in genere in coordinamento con la memorizzazione nella cache configurata a livello di Dispatcher. Tenere presente che non esiste alcuna invalidazione attiva di queste cache, pertanto la durata della memorizzazione nella cache deve essere impostata con attenzione. Non esiste un valore &quot;una dimensione adatta a tutti&quot; che corrisponda a tutti i possibili progetti e casi di utilizzo. Accertatevi di definire una strategia di caching a livello di progetto che corrisponda meglio ai requisiti del progetto.

## Memorizzazione nella cache di Dispatcher {#dispatcher}

La memorizzazione nella cache di pagine AEM o frammenti nell&#39;Dispatcher [](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html) AEM è una procedura consigliata per qualsiasi progetto AEM. Solitamente, si basa su tecniche di annullamento della validità che garantiscono che qualsiasi contenuto modificato in AEM venga aggiornato correttamente nell’Dispatcher. Si tratta di una funzione fondamentale della strategia di caching Dispatcher AEM.

Oltre al contenuto AEM gestito puro CIF, una pagina può in genere visualizzare i dati di e-commerce recuperati dinamicamente dall&#39;Magento tramite GraphQL. Anche se la struttura di pagina stessa potrebbe non cambiare mai, il contenuto del commercio potrebbe cambiare, ad esempio, se alcuni dati di prodotto (nome, prezzo, ecc.) cambiano nel Magento.

Per garantire che le pagine CIF possano essere memorizzate nella cache per un periodo di tempo limitato nel dispatcher AEM, si consiglia quindi di utilizzare l&#39;annullamento della validità [della cache](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) basata su tempo (altrimenti nota come cache TTL) durante il caching delle pagine CIF nell&#39;Dispatcher AEM. Questa funzione può essere configurata in AEM utilizzando il pacchetto [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) aggiuntivo.

Con il caching basato su TTL, uno sviluppatore definisce in genere una o più durate di memorizzazione nella cache per le pagine AEM selezionate. In questo modo le pagine CIF vengono memorizzate nella cache solo nel dispatcher AEM fino alla durata configurata e il contenuto viene aggiornato di frequente.

>[!NOTE]
>
>Anche se i dati lato server possono essere memorizzati nella cache dal dispatcher AEM, alcuni componenti CIF come `product`, `productlist`e `searchresults` componenti in genere recuperano sempre i prezzi dei prodotti in una richiesta browser lato client quando la pagina viene caricata. In questo modo, al caricamento della pagina viene sempre recuperato il contenuto dinamico fondamentale.

## Risorse aggiuntive

- [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione cache GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html)