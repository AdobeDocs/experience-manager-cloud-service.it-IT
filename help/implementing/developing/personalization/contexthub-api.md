---
title: Riferimento API ContextHub Javascript
description: L'API ContextHub Javascript è disponibile per gli script quando il componente ContextHub è stato aggiunto alla pagina
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 3%

---


# Riferimento API ContextHub Javascript {#contexthub-javascript-api-reference}

L&#39;API ContextHub Javascript è disponibile per gli script quando il componente [ContextHub è stato aggiunto alla pagina](adding-contexthub.md).

## Costanti ContextHub {#contexthub-constants}

Valori costanti definiti dall&#39;API ContextHub Javascript.

### Costanti evento {#event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per gli store ContextHub. Vedere anche [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Costante | Descrizione | Valore |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Spazio dei nomi evento di ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica che tutti gli store richiesti sono registrati, inizializzati e pronti per essere consumati | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica che non tutti gli store sono stati inizializzati entro un determinato timeout | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Generato quando un negozio è registrato | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica che i negozi sono pronti per funzionare. Viene attivato immediatamente dopo la registrazione, ad eccezione degli store JSONP, dove viene attivato quando vengono estratti i dati. | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Generato quando uno store aggiorna la sua persistenza | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nome contenitore persistenza | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Memorizza il nome della chiave di persistenza specifica in cui è memorizzato il risultato JSON non elaborato | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Memorizza la marca temporale specifica che indica quando sono stati estratti i dati JSON | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Memorizza l’URL specifico del servizio JSON utilizzato durante l’ultima chiamata | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica se l&#39;interfaccia utente di ContextHub è espansa | `/_/container-expanded` |

### Costanti evento interfaccia utente {#ui-event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per l’interfaccia utente ContextHub.

| **Costante** | **Descrizione** | **Valore** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Generato quando una modalità viene registrata | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Generato quando una modalità non è registrata | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Generato quando viene registrato un renderer di modalità | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Generato quando un renderer di modalità non è registrato | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Generato quando viene aggiunta una nuova modalità | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Generato quando una modalità viene rimossa | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Generato quando l’utente seleziona una modalità | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Generato quando viene registrato un nuovo modulo | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Generato quando un modulo non è registrato | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Generato quando viene registrato un renderer di moduli | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Generato quando un renderer di modulo non è registrato | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Generato quando viene aggiunto un nuovo modulo | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Generato quando un modulo viene rimosso | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Generato quando il contenitore dell’interfaccia utente viene aggiunto alla pagina | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Generato all’apertura dell’interfaccia utente ContextHub | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Generato quando l’interfaccia utente ContextHub viene compressa | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Generato quando una proprietà viene modificata | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Generato ogni volta che viene eseguito il rendering dell’interfaccia utente ContextHub (ad esempio dopo una modifica di proprietà) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Generato quando il contenitore dell&#39;interfaccia utente viene inizializzato | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica la modalità interfaccia attiva | `/_/active-ui-mode` |

## Riferimento API ContextHub Javascript {#contexthub-javascript-api-reference-2}

L&#39;oggetto ContextHub consente l&#39;accesso a tutti gli store.

### Funzioni (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Restituisce tutti gli store ContextHub registrati.

Questa funzione non ha parametri.

##### Valore restituito {#returns-}

Un oggetto che contiene tutti gli store ContextHub. Ogni store è un oggetto che utilizza lo stesso nome dello store.

##### Esempio {#example-}

L&#39;esempio seguente recupera tutti gli store e recupera lo store di geolocalizzazione:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera uno store come oggetto Javascript.

##### Parametri {#parameters-}

* **`name`:** Nome con cui è stato registrato lo store.

##### Valore restituito {#returns-getstore-name}

Un oggetto che rappresenta lo store.

##### Esempio {#example-getstore-name}

L&#39;esempio seguente recupera l&#39;archivio di geolocalizzazione:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Rappresenta un segmento ContextHub. Utilizzate l&#39;icona `ContextHub.SegmentEngine.SegmentManager` per ottenere i segmenti.

### Funzioni (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Restituisce il nome del segmento come valore String.

#### getPath() {#getpath}

Restituisce il percorso dell&#39;archivio della definizione del segmento come valore String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornisce l&#39;accesso ai segmenti ContextHub.

### Funzioni (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Restituisce i segmenti risolti nel contesto corrente. Questa funzione non ha parametri.

##### Valore restituito {#returns-getresolvedsegments}

Un array di `ContextHub.SegmentEngine.Segment` oggetti.

## ContextHub.Store.Core {#contexthub-store-core}

La classe base per gli store ContextHub.

### Proprietà (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) oggetto. Utilizzare questo oggetto per eseguire il binding delle funzioni per memorizzare gli eventi. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

#### name {#name}

Il nome dello store.

#### persistenza {#persistence}

Un `ContextHub.Utils.Persistence` oggetto. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

### Funzioni (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(struttura ad albero, opzioni) {#addallitems-tree-options}

Unisce un oggetto dati o una matrice ai dati dello store. Ogni coppia chiave/valore nell&#39;oggetto o nella matrice viene aggiunta allo store (tramite la `setItem` funzione):

* **Oggetto:** Le chiavi sono i nomi delle proprietà.
* **Array:** I tasti sono gli indici della matrice.

I valori possono essere oggetti.

##### Parametri {#parameters-addallitems}

* **`tree`:** (Oggetto o array) I dati da aggiungere allo store.
* **`options`:** (Oggetto) Un oggetto facoltativo di opzioni passato alla funzione setItem. Per informazioni, vedete il `options` parametro di [`setItem(key,value,options)`](#setitem-key-value-options).

##### Valore restituito {#returns-addallitems}

Un `boolean` valore:

* Il valore di `true` indica che l&#39;oggetto dati è stato memorizzato.
* Il valore di `false` indica che l&#39;archivio dati è invariato.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Crea un riferimento da una chiave a un&#39;altra chiave. Una chiave non può fare riferimento a se stessa.

##### Parametri {#parameters-addreference}

* **`key`:** La chiave a cui fa riferimento `anotherKey`.

* **`anotherkey`:** Chiave a cui fa riferimento `key`.

##### Valore restituito {#returns-addreference}

Un `boolean` valore:

* Un valore di `true` indica che il riferimento è stato aggiunto.
* Un valore di `false` indica che non è stato aggiunto alcun riferimento.

#### announceReadiness() {#announcereadiness}

Attiva l’ `ready` evento per lo store. Questa funzione non ha parametri e non restituisce alcun valore.

#### clean() {#clean}

Rimuove tutti i dati dallo store. La funzione non ha parametri e non restituisce valori.

#### getItem(key) {#getitem-key}

Restituisce il valore associato a una chiave.

##### Parametri {#parameters-getitem}

* **`key`:** (String) La chiave per la quale restituire il valore.

##### Valore restituito {#returns-getitem}

Un oggetto che rappresenta il valore della chiave.

#### getKeys(includeInternali) {#getkeys-includeinternals}

Recupera le chiavi dallo store. Facoltativamente potete recuperare le chiavi utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-getkeys}

* **`includeInternals`:** Un valore di `true` include le chiavi utilizzate internamente nei risultati. Queste chiavi iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Valore restituito {#returns-getkeys}

Un array di nomi chiave ( `string` valori).

#### getReferences() {#getreferences}

Recupera i riferimenti dallo store.

##### Valore restituito {#returns-getreferences}

Un array che utilizza le chiavi di riferimento come indici per le chiavi di riferimento:

* Le chiavi di riferimento corrispondono al `key` parametro della `addReference` funzione.
* Le chiavi di riferimento corrispondono al `anotherKey` parametro della `addReference` funzione.

#### getTree(includeInterni) {#gettree-includeinternals}

Recupera la struttura dati dallo store. Facoltativamente potete includere le coppie chiave/valore utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-gettree}

* `includeInternals:` Un valore di `true` include nei risultati coppie chiave/valore utilizzate internamente. Le chiavi di questi dati iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Valore restituito {#returns-gettree}

Un oggetto che rappresenta la struttura dei dati. Le chiavi sono i nomi delle proprietà dell&#39;oggetto.

#### init(name, config) {#init-name-config}

Inizializza lo store.

* Imposta i dati dello store su un oggetto vuoto.
* Imposta i riferimenti dell&#39;archivio su un oggetto vuoto.
* Il nome `eventChannel` è `data:<name>`, dove `<name>` è il nome del negozio.
* Il nome `storeDataKey` è `/store/<name>`, dove `<name>` è il nome del negozio.

##### Parametri {#parameters-init}

* **`name`:** Il nome dello store.
* **`config`:** Un oggetto che contiene le proprietà di configurazione:
   * `eventDeferring`: Il valore predefinito è 32.
   * `eventing`: L&#39;oggetto [ContextHub.Utils.Eventing](#contexthub-utils-eventing) per questo store. Il valore predefinito è l&#39; `ContextHub.eventing` oggetto utilizzato.
   * `persistence`: L&#39; `ContextHub.Utils.Persistence` oggetto per lo store. Il valore predefinito è l&#39; `ContextHub.persistence` oggetto.

#### isEventingPaused() {#iseventingpaused}

Determina se l&#39;evento viene messo in pausa per lo store.

##### Valore restituito {#returns-iseventingpaused}

Un valore booleano:

* `true`: Eventing viene messo in pausa in modo che non venga attivato alcun evento per lo store.
* `false`: Eventing non viene messo in pausa in modo che gli eventi vengano attivati per lo store.

#### pauseEventing() {#pauseeventing}

Sospende l&#39;evento per lo store in modo da non attivare eventi. Questa funzione non richiede parametri e non restituisce alcun valore.

#### removeItem(key, options) {#removeitem-key-options}

Rimuove una coppia chiave/valore dallo store.

Quando una chiave viene rimossa, la funzione attiva l&#39; `data` evento. I dati dell&#39;evento includono il nome dell&#39;archivio, il nome della chiave che è stata rimossa, il valore rimosso, il nuovo valore per la chiave (null) e il tipo di azione &quot;remove&quot;.

Facoltativamente, potete impedire l&#39;attivazione dell&#39; `data` evento.

##### Parametri {#parameters-removeitem}

* **`key`:** (Stringa) Il nome della chiave da rimuovere.
* **`options`:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * silenzioso: Un valore di `true` impedisce l&#39;attivazione dell&#39; `data` evento. Il valore predefinito è `false`.

##### Valore restituito {#returns-removeitem}

Un `boolean` valore:

* Un valore di `true` indica che la coppia chiave/valore è stata rimossa.
* Il valore di `false` indica che l&#39;archivio dati è invariato perché la chiave non è stata trovata nello store.

#### removeReference(key) {#removereference-key}

Rimuove un riferimento dallo store.

##### Parametri {#parameters-removereference}

* **`key`:** Il riferimento chiave da rimuovere. Questo parametro corrisponde al `key` parametro della `addReference` funzione.

##### Valore restituito {#returns-removereference}

Un `boolean` valore:

* Un valore di `true` indica che il riferimento è stato rimosso.
* Il valore di `false` indica che la chiave non era valida e che lo store non è cambiato.

#### reset(keepRemainData) {#reset-keepremainingdata}

Ripristina i valori iniziali dei dati persistenti dello store. Facoltativamente, puoi rimuovere tutti gli altri dati dallo store. L&#39;evento viene messo in pausa per lo store mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella `initialValues` proprietà dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset}

* **`keepRemainingData`**: (Booleano) Un valore true causa la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveReference(key, try) {#resolvereference-key-retry}

Recupera una chiave di riferimento. Facoltativamente, è possibile specificare il numero di iterazioni da utilizzare per risolvere la corrispondenza migliore.

##### Parametri {#parameters-resolvereference}

* **`key`:** (String) La chiave per la quale risolvere il riferimento. Questo `key` parametro corrisponde al `key` parametro della `addReference` funzione.
* **`retry`:** (Numero) Il numero di iterazioni da utilizzare.

##### Valore restituito {#returns-resolvereference}

Un `string` valore che rappresenta la chiave di riferimento. Se non viene risolto alcun riferimento, viene restituito il valore del `key` parametro.

#### curriculumEventing() {#resumeeventing}

Riprende l&#39;evento per lo store in modo da attivare gli eventi. Questa funzione non definisce alcun parametro e non restituisce alcun valore.

#### setItem(key, value, options) {#setitem-key-value-options}

Aggiunge una coppia chiave/valore allo store.

Attiva l&#39; `data` evento solo se il valore della chiave è diverso dal valore attualmente memorizzato per la chiave. Facoltativamente, potete impedire l&#39;attivazione dell&#39; `data` evento.

I dati dell&#39;evento includono il nome dello store, la chiave, il valore precedente, il nuovo valore e il tipo di azione di `set`.

##### Parametri {#parameters-setitem}

* **`key`:** (String) Il nome della chiave.
* **`options`:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * `silent`: Un valore di `true` impedisce l&#39;attivazione dell&#39; `data` evento. Il valore predefinito è `false`.
* **`value`:** (Oggetto) Il valore da associare alla chiave.

##### Valore restituito {#returns-setitem}

Un `boolean` valore:

* Il valore di `true` indica che l&#39;oggetto dati è stato memorizzato.
* Il valore di `false` indica che l&#39;archivio dati è invariato.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Uno store che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno o, facoltativamente, da un servizio che restituisce dati JSON. Specificate i dettagli del servizio utilizzando la [`init`](#init-name-config) funzione quando create un&#39;istanza di questa classe.

Lo store utilizza la persistenza in memoria (variabile Javascript). I dati dello store sono disponibili solo per tutta la durata della pagina.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](#contexthub-store-core) ed eredita le funzioni di tale classe.

### Funzioni (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura i dettagli per la connessione al servizio JSONP utilizzato da questo oggetto. Potete aggiornare o sostituire la configurazione esistente. La funzione non restituisce alcun valore.

##### Parametri {#parameters-configureservice}

* **`serviceConfig`:** Un oggetto che contiene le proprietà seguenti:
   * `host`: (String) Il nome del server o l&#39;indirizzo IP.
   * `jsonp`: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {callback: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.
   * `params`: (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
   * `path`: (String) Il percorso del servizio.
   * `port`: (Numero) Il numero di porta del servizio.
   * `secure`: (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:
      * `auto`: //
      * `true`: https://
      * `false`: Http://
* **override:** (Boolean). Un valore di `true` determina la sostituzione della configurazione del servizio esistente con le proprietà di `serviceConfig`. Un valore di `false` determina l&#39;unione delle proprietà di configurazione del servizio esistenti con quelle di `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Restituisce la risposta non elaborata memorizzata nella cache dall&#39;ultima chiamata al servizio JSONP. La funzione non richiede parametri.

##### Valore restituito {#returns-getrawresponse}

Un oggetto che rappresenta la risposta non elaborata.

#### getServiceDetails() {#getservicedetails}

Recupera l&#39;oggetto del servizio per questo oggetto ContextHub.Store.JSONPStore. L&#39;oggetto service contiene tutte le informazioni necessarie per creare l&#39;URL del servizio.

##### Valore restituito {#returns-getservicedetails}

Un oggetto con le seguenti proprietà:

* **`host`:** (String) Il nome del server o l&#39;indirizzo IP.
* **`jsonp`:** (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {callback: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.
* **`params`:** (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
* **`path`:** (String) Il percorso del servizio.
* **`port`:** (Numero) Il numero di porta del servizio.
* **`secure`:** (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:
   * `auto`: //
   * `true`: https://
   * `false`: Http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera l&#39;URL del servizio JSONP.

##### Parametri {#parameters-getserviceurl}

* **`resolve`:** (Booleano) Determina se includere nell&#39;URL i parametri risolti. Un valore di `true` risolve i parametri e `false` non lo è.

##### Valore restituito {#returns-getserviceurl}

Un `string` valore che rappresenta l&#39;URL del servizio.

#### init(name, config) {#init-name-config-1}

inizializza l&#39; `ContextHub.Store.JSONPStore` oggetto.

##### Parametri {#parameters-init-1}

* **`name`:** (String) Il nome dello store.
* **`config`:** (Oggetto) Un oggetto che contiene la proprietà service. L&#39;oggetto JSONPStore utilizza le proprietà dell&#39; `service` oggetto per creare l&#39;URL del servizio JSONP:
   * `eventDeferring`: 32.
   * `eventing`: L&#39;oggetto ContextHub.Utils.Eventing per lo store. Il valore predefinito è l&#39; `ContextHub.eventing` oggetto.
   * `persistence`: L&#39;oggetto ContextHub.Utils.Persistenza per lo store. Per impostazione predefinita, viene utilizzata la persistenza della memoria (oggetto Javascript).
   * `service`: (Oggetto)
      * `host`: (String) Il nome del server o l&#39;indirizzo IP.
      * `jsonp`: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Quando è true, l&#39; `{callback: "ContextHub.Callbacks.*Object.name*}`oggetto viene aggiunto a `service.params`.
      * `params`: (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi e i valori dei parametri sono rispettivamente i nomi e i valori delle proprietà dell&#39;oggetto.
      * `path`: (String) Il percorso del servizio.
      * `port`: (Numero) Il numero di porta del servizio.
      * `secure`: (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:
         * `auto`: //
         * `true`: https://
         * `false`: Http://
      * `timeout`: (Numero) Il tempo di attesa che il servizio JSONP risponda prima del timeout, in millisecondi.
         * `ttl`: Il tempo minimo in millisecondi che trascorre tra le chiamate al servizio JSONP. (Vedere la funzione [queryService](#queryservice-reload) ).

#### queryService(reload) {#queryservice-reload}

Interrompe il servizio JSONP remoto e memorizza nella cache la risposta. Se il tempo trascorso dalla precedente chiamata a questa funzione è inferiore al valore di `config.service.ttl`, il servizio non viene chiamato e la risposta nella cache non viene modificata. Facoltativamente, puoi forzare la chiamata al servizio. La `config.service.ttl`proprietà viene impostata quando si chiama la funzione [init](#init-name-config) per inizializzare lo store.

Attiva l’evento ready al termine della query. Se l&#39;URL del servizio JSONP non è impostato, la funzione non esegue alcuna operazione.

##### Parametri {#parameters-queryservice}

* **`reload`:** (Booleano) Il valore true rimuove la risposta memorizzata nella cache e forza la chiamata al servizio JSONP.

#### reset {#reset}

Ripristina i valori iniziali dei dati persistenti dello store e chiama il servizio JSONP. Facoltativamente, puoi rimuovere tutti gli altri dati dallo store. L&#39;evento viene messo in pausa per lo store mentre i valori iniziali vengono reimpostati. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare l&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Un valore true causa la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveParameter(f) {#resolveparameter-f}

Risolve il parametro specificato.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` estende [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) in modo da ereditare tutte le funzioni di tale classe. Tuttavia, i dati recuperati dal servizio JSONP vengono memorizzati in base alla configurazione della persistenza ContextHub. (Vedere Modalità [di persistenza:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` estende [ContextHub.Store.Core](#contexthub-store-core) in modo da ereditare tutte le funzioni di tale classe. I dati in questo archivio sono persistenti in base alla configurazione della persistenza ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` estende [ContextHub.Store.Core](#contexthub-store-core) in modo da ereditare tutte le funzioni di tale classe. I dati in questo archivio sono persistenti utilizzando la persistenza in memoria (oggetto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestisce i moduli dell’interfaccia utente e i renderer dei moduli dell’interfaccia utente.

### Funzioni (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, DontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un renderer di moduli dell&#39;interfaccia utente con ContextHub. Dopo la registrazione del renderer, può essere utilizzato per [creare moduli](configuring-contexthub.md#adding-a-ui-module)di interfaccia utente. Utilizzate questa funzione quando vi [estendete `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) per creare un renderer di moduli interfaccia utente personalizzato.

##### Parametri {#parameters-registerrenderer}

* **`moduleType`:** (String) Identificatore per il renderer del modulo dell&#39;interfaccia utente. Se un renderer è già registrato utilizzando il valore specificato, il renderer esistente non viene registrato prima della registrazione del renderer.
* **`renderer`:** (String) Il nome della classe che esegue il rendering del modulo dell&#39;interfaccia utente.
* **`dontRender`:** (Booleano) Impostato `true` per impedire il rendering dell&#39;interfaccia utente ContextHub dopo la registrazione del renderer. Il valore predefinito è `false`.

##### Esempio {#example-registerrenderer}

L&#39;esempio seguente registra un renderer come tipo di `contexthub.browserinfo` modulo.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Una classe di utilità per l&#39;interazione con i cookie.

### Funzioni (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se esiste un cookie.

##### Parametri {#parameters-exists}

* **`key`:** Un elemento `String` che contiene la chiave del cookie per il quale si sta eseguendo il test.

##### Valore restituito {#returns-exists}

Il `boolean` valore true indica che il cookie esiste.

##### Esempio {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Restituisce tutti i cookie con chiavi che corrispondono a un filtro.

##### Parametri {#parameters-getallitems}

* **`filter`:** (Facoltativo) Criteri per la corrispondenza delle chiavi dei cookie. Per restituire tutti i cookie, non specificate alcun valore. Sono supportati i tipi seguenti:
   * Stringa: La stringa viene confrontata con il cookie key.
   * Array: Ogni elemento dell&#39;array è un filtro.
   * Un oggetto RegExp: La funzione test dell&#39;oggetto viene utilizzata per far corrispondere i tasti cookie.
   * Una funzione: Una funzione che verifica la presenza di un cookie key per una corrispondenza. La funzione deve accettare il cookie key come parametro e restituire true se il test conferma una corrispondenza.

##### Valore restituito {#returns-getallitems}

Un oggetto di cookie. Le proprietà dell&#39;oggetto sono cookie key e i valori chiave sono cookie values.

##### Esempio {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Restituisce un valore di cookie.

##### Parametri {#parameters-getitem-1}

* **`key`:** Chiave del cookie per il quale si desidera ottenere il valore.

##### Valore restituito {#returns-getitem-1}

Il valore del cookie, o `null` se non è stato trovato alcun cookie per la chiave.

##### Esempio {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Restituisce un array delle chiavi dei cookie esistenti che corrispondono a un filtro.

##### Parametri {#parameters-getkeys-1}

* **`filter`:** Criteri per la corrispondenza delle chiavi dei cookie. Sono supportati i tipi seguenti:
   * Stringa: La stringa viene confrontata con il cookie key.
   * Array: Ogni elemento dell&#39;array è un filtro.
   * Un oggetto RegExp: La funzione test dell&#39;oggetto viene utilizzata per far corrispondere i tasti cookie.
   * Una funzione: Una funzione che verifica la presenza di un cookie key per una corrispondenza. La funzione deve prendere il cookie key come parametro e restituire `true` se il test conferma una corrispondenza.

##### Valore restituito {#returns-getkeys-1}

Un array di stringhe in cui ogni stringa è la chiave di un cookie che corrisponde al filtro.

##### Esempio {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Rimuove un cookie. Per rimuovere il cookie, il valore è impostato su una stringa vuota e la data di scadenza è impostata sul giorno prima della data corrente.

##### Parametri {#parameters-removeitem-1}

* **`key`:** Un `String` valore che rappresenta la chiave del cookie da rimuovere.
* **`options`:** Un oggetto che contiene i valori delle proprietà per la configurazione degli attributi del cookie. Vedere la [`setItem`](#setitem-key-value-options) funzione per ulteriori informazioni. La `expires` proprietà non ha effetto.

##### Valore restituito {#returns-removeitem-1}

Questa funzione non restituisce un valore.

##### Esempio {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea un cookie della chiave e del valore specificati e aggiunge il cookie al documento corrente. Facoltativamente, potete specificare opzioni che configurano gli attributi del cookie.

##### Parametri {#parameters-setitem-1}

* **`key`:** Una stringa che contiene la chiave del cookie.
* **`value`:** Una stringa che contiene il valore del cookie.
* **`options`:** (Facoltativo) Un oggetto che contiene una delle seguenti proprietà che configurano gli attributi del cookie:
   * `expires`: Un valore `date` o `number` che specifica quando scade il cookie. Un valore data specifica l&#39;ora assoluta di scadenza. Un numero (in giorni) imposta l&#39;ora di scadenza sull&#39;ora corrente più il numero. Il valore predefinito è `undefined`.
   * `secure`: Un `boolean` valore che specifica l&#39; `Secure` attributo del cookie. Il valore predefinito è `false`.
   * `path`: Un `String` valore da utilizzare come `Path` attributo del cookie. Il valore predefinito è `undefined`.

##### Valore restituito {#returns-setitem-1}

Il cookie con il valore impostato.

##### Esempio {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Rimuove tutti i cookie che corrispondono a un determinato filtro. I cookie vengono associati utilizzando la `getKeys` funzione e rimossi utilizzando la `removeItem` funzione.

##### Parametri {#parameters-vanish}

* **`filter`:** L&#39; `filter` argomento da utilizzare nella chiamata alla [`getKeys`](#getkeys-filter) funzione.
* **`options`:** L&#39; `options` argomento da utilizzare nella chiamata alla [`removeItem`](#removeitem-key-options) funzione.

##### Valore restituito {#returns-vanish}

Questa funzione non restituisce un valore.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Consente di eseguire il binding e la disassociazione delle funzioni agli eventi dell&#39;archivio ContextHub. Accedere `ContextHub.Utils.Eventing` agli oggetti per uno store utilizzando la proprietà [eventing](#eventing) dello store.

### Funzioni (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Separa una funzione da un evento.

##### Parametri {#parameters-off}

* **`name`:** Il [nome dell&#39;evento](#contexthub-utils-eventing) per il quale si desidera annullare il binding della funzione.
* **`selector`:** Selettore che identifica il binding. (Vedere il `selector` parametro per le funzioni [`on`](#on-name-handler-selector-triggerforpastevents) e [`once`](#once-name-handler-selector-triggerforpastevents) ).

##### Valore restituito {#returns-off}

Questa funzione non restituisce alcun valore.

#### on(nome, gestore, selettore, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Collega una funzione a un evento. La funzione viene chiamata ogni volta che si verifica l&#39;evento. Facoltativamente, è possibile chiamare la funzione per gli eventi che si sono verificati in passato, prima che venga stabilito il binding.

##### Parametri {#parameters-on}

* **`name`:** (Stringa) Il [nome dell&#39;evento](#contexthub-utils-eventing) a cui si sta effettuando il binding della funzione.
* **`handler`:** (Funzione) La funzione da associare all&#39;evento.
* **`selector`:** (String) Un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la `off` funzione per rimuovere il binding.
* **`triggerForPastEvents`:** (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Valore restituito {#returns-on}

Quando l&#39; `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e il gestore verrà chiamato.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

##### Esempio {#example-on}

Nell&#39;esempio seguente viene associata una funzione all&#39;evento data dell&#39;archivio di geolocalizzazione. La funzione compila un elemento sulla pagina con il valore per l&#39;elemento di dati di latitudine dallo store.

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(nome, gestore, selettore, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Collega una funzione a un evento. La funzione viene chiamata una sola volta, per la prima occorrenza dell&#39;evento. Facoltativamente, è possibile chiamare la funzione per l&#39;evento che si è verificato in passato, prima che venga stabilito il binding.

##### Parametri {#parameters-once}

* **`name`:** (Stringa) Il [nome dell&#39;evento](#contexthub-utils-eventing) a cui si sta effettuando il binding della funzione.
* **`handler`:** (Funzione) La funzione da associare all&#39;evento.
* **`selector`:** (String) Un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la `off` funzione per rimuovere il binding.
* **`triggerForPastEvents`:** (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Valore restituito {#returns-once}

Quando l&#39; `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e il gestore verrà chiamato.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Una classe di utilità che consente a un oggetto di ereditare le proprietà e i metodi di un altro oggetto.

### Funzioni (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Fa sì che un oggetto erediti le proprietà e i metodi di un altro oggetto.

##### Parametri {#parameters-inherit}

* **`child`:** (Oggetto) L&#39;oggetto che eredita.
* **`parent`:** (Oggetto) L&#39;oggetto che definisce le proprietà e i metodi ereditati.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornisce funzioni per la serializzazione di oggetti in formato JSON e la deserializzazione di stringhe JSON in oggetti.

### Funzioni (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analizza un valore di stringa come JSON e lo converte in un oggetto javascript.

##### Parametri {#parameters-parse}

* **`data`:** Un valore stringa in formato JSON.

##### Valore restituito {#returns-parse}

Un oggetto Javascript.

##### Esempio {#example-parse}

Codice:

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

Restituisce l&#39;oggetto seguente:

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializza i valori e gli oggetti JavaScript in valori stringa del formato JSON.

##### Parametri {#parameters-stringify}

* **`data`:** Il valore o l&#39;oggetto da serializzare. Questa funzione supporta valori booleani, array, numero, stringa e data.

##### Valore restituito {#returns-stringify}

Il valore di stringa serializzato. Quando `data` `egExp` è un valore R, questa funzione restituisce un oggetto vuoto. Quando `data` è una funzione, restituisce `undefined`.

##### Esempio {#example-stringify}

Il codice seguente:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Valore restituito:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Questa classe semplifica la manipolazione degli oggetti dati da memorizzare o da recuperare dagli store ContextHub.

### Funzioni (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia di un oggetto dati e vi aggiunge la struttura dati da un secondo oggetto. La funzione restituisce la copia e non modifica nessuno degli oggetti originali. Quando le strutture ad albero dati dei due oggetti contengono chiavi identiche, il valore del secondo oggetto sovrascrive il valore del primo oggetto.

##### Parametri {#parameters-addallitems-1}

* **`tree`:** L&#39;oggetto copiato.
* **`secondTree`:** L&#39;oggetto unito alla copia dell&#39; `tree` oggetto.

##### Valore restituito {#returns-addallitems-1}

Un oggetto che contiene i dati uniti.

#### cleanup() {#cleanup}

Crea una copia di un oggetto, trova e rimuove elementi nella struttura dati che non contengono valori, valori null o valori non definiti e restituisce la copia.

##### Parametri {#parameters-cleanup}

* **`tree`:** L&#39;oggetto da pulire.

##### Valore restituito {#returns-cleanup}

Una copia della struttura ad albero che viene pulita.

#### getItem() {#getitem}

Recupera il valore da un oggetto per la chiave.

##### Parametri {#parameters-getitem-2}

* **`tree`:** L&#39;oggetto data.
* **`key`:** Chiave per il valore da recuperare.

##### Valore restituito {#returns-getitem-2}

Il valore che corrisponde alla chiave. Quando la chiave dispone di chiavi figlio, questa funzione restituisce un oggetto complesso. Quando il tipo del valore della chiave è `undefined`, `null` viene restituito.

##### Esempio {#example-getitem-2}

Considerare il seguente oggetto Javascript:

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

Il seguente codice di esempio restituisce il valore `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

Il codice di esempio seguente recupera il valore per una chiave con chiavi figlio:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La funzione restituisce l&#39;oggetto seguente:

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera tutte le chiavi dalla struttura dati di un oggetto. Facoltativamente, è possibile recuperare solo le chiavi degli elementi secondari di una chiave specifica. Facoltativamente, potete anche specificare un ordinamento delle chiavi recuperate.

##### Parametri {#parameters-getkeys-2}

* **`tree`:** L&#39;oggetto da cui recuperare le chiavi della struttura dati.
* **`parent`:** (Facoltativo) Chiave di un elemento nella struttura dei dati per la quale si desidera recuperare le chiavi degli elementi secondari.
* **`order`:** (Facoltativo) Funzione che determina l&#39;ordine delle chiavi restituite. (Vedere [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) in Mozilla Developer Network.)

##### Valore restituito {#returns-getkeys-2}

Un array di chiavi.

##### Esempio {#example-getkeys-2}

Considerare il seguente oggetto:

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

Lo `ContextHub.Utils.JSON.tree.getKeys(myObject);` script restituisce la seguente matrice:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia di un dato oggetto, rimuove il ramo specificato dalla struttura dei dati e restituisce la copia modificata.

##### Parametri {#parameters-removeitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** La chiave da rimuovere.

##### Valore restituito {#returns-removeitem-2}

Una copia dell&#39;oggetto dati originale con la chiave rimossa.

##### Esempio {#example-removeitem-2}

Considerare il seguente oggetto:

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

Lo script di esempio seguente rimuove il ramo /uno/due/tre/quattro dalla struttura dei dati:

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La funzione restituisce l&#39;oggetto seguente:

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanizeKey(key) {#sanitizekey-key}

Rimuove i valori stringa per renderli utilizzabili come chiavi. Per eliminare una stringa, questa funzione esegue le azioni seguenti:

* Riduce più barre consecutive a una singola barra.
* Rimuove gli spazi bianchi dall&#39;inizio e dalla fine della stringa.
* Divide il risultato in un array di stringhe delimitate da barre.

Utilizzare l&#39;array risultante per creare una chiave utilizzabile.

##### Parametri {#parameters-sanitizekey}

* **`key`:** La `string` pulizia.

##### Valore restituito {#returns-sanitizekey}

Un array di `string` valori in cui ogni stringa è la porzione di `key` cui sono state delimitate le barre. rappresenta la chiave sanizzata. Se la matrice sanizzata ha una lunghezza pari a zero, questa funzione restituisce `null`.

##### Esempio {#example-sanitizekey}

Il codice seguente rimuove una stringa per generare l&#39;array `["this", "is", "a", "path"]`e genera quindi la chiave `"/this/is/a/path"` dall&#39;array:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Aggiunge una coppia chiave/valore alla struttura dati di una copia di un oggetto. Per informazioni sulle strutture ad albero dei dati, vedere [Persistenza.](contexthub.md#persistence)

##### Parametri {#parameters-setitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** Chiave da associare al valore che si sta aggiungendo. La chiave è il percorso dell&#39;elemento nella struttura dei dati. Questa funzione richiede `ContextHub.Utils.JSON.tree.sanitize` di rimuovere completamente la chiave prima di aggiungerla.
* **`value`:** Valore da aggiungere alla struttura dati.

##### Valore restituito {#returns-setitem-2}

Una copia dell&#39; `tree` oggetto che include la coppia `key`/ `value` .

##### Esempio {#example-setitem-2}

Considerate il seguente codice JavaScript:

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandidate {#contexthub-utils-storecandidates}

Consente di registrare i candidati allo store e di ottenere i candidati allo store registrati.

### Funzioni (ContextHub.Utils.storeCandidate) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandiates(storeType) {#getregisteredcandidates-storetype}

Restituisce i tipi di store registrati come candidati store. Recuperare i candidati registrati di un tipo di store specifico o di tutti i tipi di store.

##### Parametri {#parameters-getregisteredcandidates}

* **`storeType`:** (String) Il nome del tipo di store. Vedere il `storeType` parametro della [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione.

##### Valore restituito {#returns-getregisteredcandidates}

Un oggetto di tipi di store. Le proprietà dell&#39;oggetto sono i nomi dei tipi di archivio e i valori delle proprietà sono un array di candidati store registrati.

#### getStoreFromCandidate(storeType) {#getstorefromcandidates-storetype}

Restituisce un tipo di archivio dai candidati registrati. Se sono registrati più tipi di store con lo stesso nome, la funzione restituisce il tipo di store con la priorità più alta.

##### Parametri {#parameters-getstorefromcandidates}

* `storeType`: (String) Il nome del candidato dello store. Vedere il `storeType` parametro della [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) funzione.

##### Valore restituito {#returns-getstorefromcandidates}

Un oggetto che rappresenta il candidato dello store registrato. Se il tipo di archivio richiesto non è registrato, viene generato un errore.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Restituisce i nomi dei tipi di store registrati come candidati store. Questa funzione non richiede parametri.

##### Valore restituito {#returns-getsupportedstoretypes}

Un array di valori stringa, in cui ogni stringa è il tipo di storetype con cui è stato registrato un candidato all&#39;archiviazione. Vedere il `storeType` parametro della [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione.

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra un oggetto store come candidato allo store utilizzando un nome e una priorità.

La priorità è un numero che indica l&#39;importanza degli store con lo stesso nome. Quando un candidato del negozio viene registrato con lo stesso nome di un candidato del negozio già registrato, viene utilizzato il candidato con la priorità più alta. Quando si registra un candidato per un negozio, lo store viene registrato solo se la priorità è superiore ai candidati dello store registrato dello stesso nome.

##### Parametri {#parameters-registerstorecandidate}

* **`store`:** (Oggetto) L&#39;oggetto store da registrare come candidato store.
* **`storeType`:** (String) Il nome del candidato dello store. Questo valore è richiesto quando si crea un&#39;istanza del candidato store.
* **`priority`:** (Numero) La priorità del candidato del negozio.
* **`applies`:** (Funzione) La funzione da richiamare che valuta l&#39;applicabilità dello store nell&#39;ambiente corrente. La funzione deve restituire `true` se lo store è applicabile e `false` in caso contrario. Il valore predefinito è una funzione che restituisce true: `function() {return true;}`

##### Esempio {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
