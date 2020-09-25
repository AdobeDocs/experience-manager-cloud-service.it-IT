---
title: Aggiunta di ContextHub alle pagine e accesso agli store
description: Aggiungere ContextHub alle pagine per abilitare le funzionalità ContextHub e per collegarsi alle librerie ContextHub Javascript
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# Aggiunta di ContextHub alle pagine e accesso agli store {#adding-contexthub-to-pages-and-accessing-stores}

Aggiungete ContextHub alle pagine per abilitare le funzionalità ContextHub e per collegarvi alle librerie ContextHub Javascript.

L&#39;API ContextHub Javascript fornisce l&#39;accesso ai dati contestuali gestiti da ContextHub. Questa pagina descrive brevemente le funzioni principali dell&#39;API per l&#39;accesso e la manipolazione dei dati contestuali. Seguite i collegamenti alla documentazione di riferimento API per visualizzare informazioni dettagliate ed esempi di codice.

## Aggiunta di ContextHub a un componente Pagina {#adding-contexthub-to-a-page-component}

Per abilitare le funzioni ContextHub e per collegarsi alle librerie ContextHub Javascript, includete il `contexthub` componente nella `head` sezione della pagina. Il codice HTL per il componente pagina deve essere simile al seguente esempio:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

È inoltre necessario configurare la visualizzazione della barra degli strumenti ContextHub in modalità Anteprima. Consultate [Mostrare e nascondere l’interfaccia utente](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui)ContextHub.

## Informazioni su ContextHub Store {#about-contexthub-stores}

Utilizzate gli store ContextHub per mantenere i dati contestuali. ContextHub fornisce i seguenti tipi di store che costituiscono la base di tutti i tipi di store:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tutti i tipi di store sono estensioni della [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe. Per informazioni sulla creazione di un nuovo tipo di store, consultate [Creazione di store](extending-contexthub.md#creating-custom-store-candidates)personalizzati. Per informazioni sui tipi di store di esempio, consultate [Esempio di candidati](sample-stores.md)per lo store ContextHub.

### Modalità di persistenza {#persistence-modes}

Gli store Context Hub utilizzano una delle seguenti modalità di persistenza:

* **Locale:** Utilizza HTML5 localStorage per mantenere i dati. L&#39;archiviazione locale viene mantenuta nel browser tra le sessioni.
* **Sessione:** Utilizza HTML5 sessionStorage per mantenere i dati. L&#39;archiviazione delle sessioni viene mantenuta per tutta la durata della sessione del browser ed è disponibile per tutte le finestre del browser.
* **Cookie:** Utilizza il supporto nativo dei cookie del browser per l&#39;archiviazione dei dati. I dati del cookie vengono inviati a e dal server in richieste HTTP.
* **Window.name:** Utilizza la proprietà window.name per mantenere i dati.
* **Memoria:** Utilizza un oggetto Javascript per mantenere i dati.

Per impostazione predefinita, Context Hub utilizza la modalità di persistenza locale. Se il browser non supporta o non consente HTML5 localStorage, viene utilizzata la persistenza della sessione. Se il browser non supporta o non consente HTML5 sessionStorage, viene utilizzata la persistenza Window.name.

### Dati store {#store-data}

All&#39;interno, memorizzare i dati in una struttura ad albero, consentendo l&#39;aggiunta di valori come tipi primari o oggetti complessi. Quando si aggiungono oggetti complessi agli store, le proprietà dell&#39;oggetto vengono suddivise in rami nella struttura dei dati. Ad esempio, il seguente oggetto complesso viene aggiunto a uno store vuoto denominato location:

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

La struttura ad albero dei dati dello store può essere concettualizzata come segue:

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

La struttura ad albero definisce gli elementi dati nell&#39;archivio come coppie chiave/valore. Nell&#39;esempio precedente, la chiave `/number` corrisponde al valore `321`, mentre la chiave `/data/country` corrisponde al valore `Switzerland`.

### Manipolazione di oggetti {#manipulating-objects}

ContextHub fornisce la [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) classe per la manipolazione degli oggetti Javascript. Utilizzare le funzioni di questa classe per manipolare gli oggetti Javascript prima di aggiungerli a uno store o dopo averli ottenuti da uno store.

Inoltre, la [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) classe fornisce funzioni per la serializzazione degli oggetti alle stringhe e la deserializzazione delle stringhe agli oggetti. Utilizzare questa classe per gestire i dati JSON per supportare i browser che non includono in modo nativo le funzioni `JSON.parse` e `JSON.stringify` .

## Interazione con gli store ContextHub {#interacting-with-contexthub-stores}

Utilizzare l&#39;oggetto [`ContextHub`](contexthub-api.md#ui-event-constants) Javascript per ottenere uno store come oggetto Javascript. Una volta ottenuto l&#39;oggetto store è possibile manipolare i dati in esso contenuti. Utilizzare la [`getAllStores`](contexthub-api.md#getallstores) funzione o la [`getStore`](contexthub-api.md#getstore-name) funzione per ottenere lo store.

### Accesso ai dati dell&#39;archivio {#accessing-store-data}

La classe [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript definisce diverse funzioni per l&#39;interazione con i dati dello store. Le seguenti funzioni memorizzano e recuperano più elementi di dati contenuti negli oggetti:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

I singoli elementi di dati sono memorizzati come un insieme di coppie chiave/valore. Per memorizzare e recuperare i valori si specifica la chiave corrispondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

I candidati all&#39;archivio personalizzati possono definire funzioni aggiuntive che forniscono l&#39;accesso ai dati dell&#39;archivio.

>[!NOTE]
>
>Per impostazione predefinita, ContextHub non è a conoscenza dell&#39;accesso attualmente utilizzato sui server di pubblicazione e tali utenti sono considerati da ContextHub come &quot;anonimi&quot;.
>
>Potete rendere ContextHub consapevole degli utenti connessi caricando l&#39;archivio profili. Fate riferimento al codice [di esempio su GitHub qui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### ContextHub Eventing {#contexthub-eventing}

ContextHub include un framework di eventi che consente di reagire automaticamente agli eventi di memorizzazione. Ciascun oggetto store contiene un [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) oggetto disponibile come [`eventing`](contexthub-api.md#eventing) proprietà dello store. Utilizzare la [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) funzione o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) per eseguire il binding di una funzione Javascript con un evento store.

## Utilizzo di Context Hub per manipolare i cookie {#using-context-hub-to-manipulate-cookies}

L&#39;API Context Hub Javascript fornisce il supporto cross-browser per la gestione dei cookie del browser. Lo [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) spazio dei nomi definisce diverse funzioni per la creazione, la manipolazione e l&#39;eliminazione dei cookie.

## Determinazione dei segmenti ContextHub risolti {#determining-resolved-contexthub-segments}

Il motore del segmento ContextHub consente di determinare quali segmenti registrati vengono risolti nel contesto corrente. Utilizzare la funzione getResolvedSegments della [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) classe per recuperare i segmenti risolti. Quindi, utilizzate la `getName` funzione o `getPath` della [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) classe per eseguire il test per un segmento.

### Segmenti ContextHub {#contexthub-segments}

I segmenti ContextHub sono installati sotto il `/conf/<site>/settings/wcm/segments` nodo.

I seguenti segmenti sono installati con il sito di esercitazione [WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* estate
* inverno

Le regole utilizzate per risolvere questi segmenti sono riepilogate come segue:

* Per determinare la latitudine dell&#39;utente viene utilizzato innanzitutto lo [store di geolocalizzazione](sample-stores.md#contexthub-geolocation-sample-store-candidate) .
* Quindi l&#39;elemento dei dati del mese dello store [](sample-stores.md#contexthub-surferinfo-sample-store-candidate) surferinfo determina la stagione in cui si trova in quella latitudine.

>[!WARNING]
>
>I segmenti installati sono forniti come configurazioni di riferimento per facilitare la creazione di una propria configurazione dedicata per il progetto e come tali non devono essere utilizzati direttamente.

## Debug di ContextHub {#debugging-contexthub}

Sono disponibili diverse opzioni per il debug di ContextHub, compresa la generazione dei registri. Per ulteriori informazioni, consulta [Configurazione di ContextHub.](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## Vedere una panoramica del framework ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fornisce una pagina [di](contexthub-diagnostics.md) diagnostica in cui potete vedere una panoramica del framework ContextHub.
