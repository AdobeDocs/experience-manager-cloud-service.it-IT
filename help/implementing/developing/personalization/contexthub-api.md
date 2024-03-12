---
title: Riferimento API JavaScript di ContextHub
description: L’API JavaScript ContextHub è disponibile per gli script quando il componente ContextHub è stato aggiunto alla pagina
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '4602'
ht-degree: 2%

---

# Riferimento API JavaScript di ContextHub {#contexthub-javascript-api-reference}

L’API JavaScript di ContextHub è disponibile per gli script quando [Il componente ContextHub è stato aggiunto alla pagina](adding-contexthub.md).

## Costanti ContextHub {#contexthub-constants}

Valori costanti definiti dall’API JavaScript ContextHub.

### Costanti evento {#event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per gli store ContextHub. Vedi anche [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Costante | Descrizione | Valore |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Spazio dei nomi dell’evento ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica che tutti gli archivi richiesti sono registrati, inizializzati e pronti per essere utilizzati | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica che non tutti gli archivi sono stati inizializzati entro un determinato timeout | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Generato quando un negozio è registrato | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica che i negozi sono pronti per funzionare. Viene attivato immediatamente dopo la registrazione, ad eccezione degli archivi JSONP in cui viene attivato al recupero dei dati. | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Generato quando un archivio aggiorna la sua persistenza | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nome contenitore persistenza | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Memorizza il nome della chiave di persistenza specifica in cui viene memorizzato il risultato JSON non elaborato | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Memorizza timestamp specifico che indica quando i dati JSON sono stati recuperati | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Memorizza l’URL specifico del servizio JSON utilizzato durante l’ultima chiamata | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica se l’interfaccia utente di ContextHub è espansa | `/_/container-expanded` |

### Costanti evento interfaccia utente {#ui-event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per l’interfaccia utente di ContextHub.

| **Costante** | **Descrizione** | **Valore** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Generato quando una modalità è registrata | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Generato quando una modalità viene annullata | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Generato quando un renderer modalità è registrato | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Generato quando un renderer modalità viene annullato | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Generato quando viene aggiunta una nuova modalità | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Generato quando una modalità viene rimossa | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Generato quando una modalità è selezionata dall&#39;utente | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Generato quando viene registrato un nuovo modulo | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Generato quando un modulo non è registrato | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Generato quando un modulo di rendering è registrato | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Generato quando un modulo di rendering viene annullato | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Generato quando viene aggiunto un nuovo modulo | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Generato quando un modulo viene rimosso | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Generato quando il contenitore dell’interfaccia utente viene aggiunto alla pagina | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Generato quando viene aperta l’interfaccia utente di ContextHub | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Generato quando l’interfaccia utente di ContextHub è compressa | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Generato quando una proprietà viene modificata | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Generato ogni volta che viene eseguito il rendering dell’interfaccia utente di ContextHub (ad esempio, dopo una modifica della proprietà) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Generato quando il contenitore dell’interfaccia utente viene inizializzato | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica la modalità interfaccia utente attiva | `/_/active-ui-mode` |

## Riferimento API JavaScript di ContextHub {#contexthub-javascript-api-reference-2}

L&#39;oggetto ContextHub consente di accedere a tutti gli archivi.

### Funzioni (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Restituisce tutti gli archivi ContextHub registrati.

Questa funzione non ha parametri.

##### Restituisce {#returns-}

Oggetto che contiene tutti gli archivi ContextHub. Ogni archivio è un oggetto che utilizza lo stesso nome dell&#39;archivio.

##### Esempio {#example-}

L’esempio seguente recupera tutti gli archivi e quindi l’archivio di geolocalizzazione:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera un archivio come oggetto JavaScript.

##### Parametri {#parameters-}

* **`name`:** Il nome con cui è stato registrato l’archivio.

##### Restituisce {#returns-getstore-name}

Oggetto che rappresenta l’archivio.

##### Esempio {#example-getstore-name}

L’esempio seguente recupera l’archivio di geolocalizzazione:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Rappresenta un segmento ContextHub. Utilizza il `ContextHub.SegmentEngine.SegmentManager` per ottenere i segmenti.

### Funzioni (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Restituisce il nome del segmento come valore String.

#### getPath() {#getpath}

Restituisce il percorso dell’archivio della definizione del segmento come valore String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornisce accesso ai segmenti ContextHub.

### Funzioni (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Restituisce i segmenti risolti nel contesto corrente. Questa funzione non ha parametri.

##### Restituisce {#returns-getresolvedsegments}

Un array di `ContextHub.SegmentEngine.Segment` oggetti.

## ContextHub.Store.Core {#contexthub-store-core}

La classe base per gli archivi ContextHub.

### Proprietà (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) oggetto. Utilizzare questo oggetto per le funzioni di associazione per memorizzare gli eventi. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

#### nome {#name}

Nome dell’archivio.

#### persistenza {#persistence}

A `ContextHub.Utils.Persistence` oggetto. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

### Funzioni (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Unisce un oggetto dati o un array con i dati dell’archivio. Ogni coppia chiave/valore nell&#39;oggetto o nell&#39;array viene aggiunta all&#39;archivio tramite `setItem` funzione ):

* **Oggetto:** Le chiavi sono i nomi delle proprietà.
* **Array:** Le chiavi sono gli indici di array.

I valori possono essere oggetti.

##### Parametri {#parameters-addallitems}

* **`tree`:** (Oggetto o array) I dati da aggiungere all&#39;archivio.
* **`options`:** (Oggetto) Oggetto facoltativo di opzioni passato alla funzione setItem. Per informazioni, vedere `options` parametro di [`setItem(key,value,options)`](#setitem-key-value-options).

##### Restituisce {#returns-addallitems}

A `boolean` valore:

* Un valore di `true` indica che l’oggetto dati è stato archiviato.
* Un valore di `false` indica che l&#39;archivio dati è invariato.

#### addReference(key, otherKey) {#addreference-key-anotherkey}

Crea un riferimento da una chiave a un&#39;altra chiave. Una chiave non può fare riferimento a se stessa.

##### Parametri {#parameters-addreference}

* **`key`:** Chiave a cui si fa riferimento `anotherKey`.

* **`anotherkey`:** Chiave a cui fa riferimento `key`.

##### Restituisce {#returns-addreference}

A `boolean` valore:

* Un valore di `true` indica che il riferimento è stato aggiunto.
* Un valore di `false` indica che non è stato aggiunto alcun riferimento.

#### announcementReadiness() {#announcereadiness}

Attiva il `ready` per questo archivio. Questa funzione non ha parametri e non restituisce alcun valore.

#### clean() {#clean}

Rimuove tutti i dati dall&#39;archivio. La funzione non ha parametri e nessun valore restituito.

#### getItem(key) {#getitem-key}

Restituisce il valore associato a una chiave.

##### Parametri {#parameters-getitem}

* **`key`:** (Stringa) Chiave per la quale restituire il valore.

##### Restituisce {#returns-getitem}

Oggetto che rappresenta il valore della chiave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera le chiavi dall’archivio. Facoltativamente, puoi recuperare le chiavi utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-getkeys}

* **`includeInternals`:** Un valore di `true` include nei risultati le chiavi utilizzate internamente. Questi tasti iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Restituisce {#returns-getkeys}

Matrice di nomi chiave ( `string` valori).

#### getReferences() {#getreferences}

Recupera i riferimenti dall’archivio.

##### Restituisce {#returns-getreferences}

Matrice che utilizza le chiavi di riferimento come indici per le chiavi di riferimento:

* Le chiavi di riferimento corrispondono a `key` parametro di `addReference` funzione.
* Le chiavi di riferimento corrispondono alle `anotherKey` parametro di `addReference` funzione.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera la struttura dati dall&#39;archivio. Facoltativamente, puoi includere le coppie chiave/valore utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-gettree}

* `includeInternals:` Un valore di `true` include nei risultati le coppie chiave/valore utilizzate internamente. Le chiavi di questi dati iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Restituisce {#returns-gettree}

Oggetto che rappresenta la struttura dati. Le chiavi sono i nomi delle proprietà dell&#39;oggetto.

#### init(name, config) {#init-name-config}

Inizializza l’archivio.

* Imposta i dati dell&#39;archivio su un oggetto vuoto.
* Imposta i riferimenti dell&#39;archivio su un oggetto vuoto.
* Il `eventChannel` è `data:<name>`, dove `<name>` è il nome dell’archivio.
* Il `storeDataKey` è `/store/<name>`, dove `<name>` è il nome dell’archivio.

##### Parametri {#parameters-init}

* **`name`:** Nome dell’archivio.
* **`config`:** Oggetto contenente le proprietà di configurazione:
   * `eventDeferring`: il valore predefinito è 32.
   * `eventing`: Il [ContextHub.Utils.Eventing](#contexthub-utils-eventing) oggetto per questo archivio. Il valore predefinito è `ContextHub.eventing` L’oggetto utilizza.
   * `persistence`: Il `ContextHub.Utils.Persistence` oggetto per questo archivio. Il valore predefinito è `ContextHub.persistence` oggetto.

#### isEventingPaused() {#iseventingpaused}

Determina se l&#39;evento viene sospeso per questo archivio.

##### Restituisce {#returns-iseventingpaused}

Un valore booleano:

* `true`: l’evento viene sospeso in modo che non venga attivato alcun evento per questo archivio.
* `false`: l’evento non viene sospeso in modo che gli eventi vengano attivati per questo archivio.

#### pauseEventing() {#pauseeventing}

Sospende l&#39;evento per l&#39;archivio in modo che non venga attivato alcun evento. Questa funzione non richiede parametri e non restituisce alcun valore.

#### removeItem(key, options) {#removeitem-key-options}

Rimuove una coppia chiave/valore dall&#39;archivio.

Quando un tasto viene rimosso, la funzione attiva il `data` evento. I dati dell’evento includono il nome dell’archivio, il nome della chiave rimossa, il valore rimosso, il nuovo valore per la chiave (null) e il tipo di azione &quot;remove&quot;.

Facoltativamente, puoi impedire l&#39;attivazione di `data` evento.

##### Parametri {#parameters-removeitem}

* **`key`:** (Stringa) Nome della chiave da rimuovere.
* **`options`:** (Oggetto) Oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * silenzioso: un valore di `true` impedisce l&#39;attivazione della `data` evento. Il valore predefinito è `false`.

##### Restituisce {#returns-removeitem}

A `boolean` valore:

* Un valore di `true` indica che la coppia chiave/valore è stata rimossa.
* Un valore di `false` indica che l&#39;archivio dati è invariato perché la chiave non è stata trovata nell&#39;archivio.

#### removeReference(key) {#removereference-key}

Rimuove un riferimento dall&#39;archivio.

##### Parametri {#parameters-removereference}

* **`key`:** Riferimento chiave da rimuovere. Questo parametro corrisponde al `key` parametro di `addReference` funzione.

##### Restituisce {#returns-removereference}

A `boolean` valore:

* Un valore di `true` indica che il riferimento è stato rimosso.
* Un valore di `false` indica che la chiave non era valida e che l’archivio non è stato modificato.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Reimposta i valori iniziali dei dati persistenti dell&#39;archivio. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo archivio durante la reimpostazione dello stesso. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nel `initialValues` proprietà dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset}

* **`keepRemainingData`**: (booleano) un valore true determina la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera una chiave di riferimento. Facoltativamente, puoi specificare il numero di iterazioni da utilizzare per risolvere la corrispondenza migliore.

##### Parametri {#parameters-resolvereference}

* **`key`:** (Stringa) Chiave per la quale risolvere il riferimento. Questo `key` il parametro corrisponde al `key` parametro di `addReference` funzione.
* **`retry`:** (Numero) Il numero di iterazioni da utilizzare.

##### Restituisce {#returns-resolvereference}

A `string` valore che rappresenta la chiave di riferimento. Se non viene risolto alcun riferimento, il valore di `key` viene restituito il parametro.

#### resumeEventing() {#resumeeventing}

Riprende gli eventi per questo archivio in modo che vengano attivati gli eventi. Questa funzione non definisce alcun parametro e non restituisce alcun valore.

#### setItem(key, value, options) {#setitem-key-value-options}

Aggiunge una coppia chiave/valore all&#39;archivio.

Attiva il `data` solo se il valore della chiave è diverso dal valore attualmente memorizzato per la chiave. Facoltativamente, puoi impedire l&#39;attivazione di `data` evento.

I dati dell’evento includono il nome dell’archivio, la chiave, il valore precedente, il nuovo valore e il tipo di azione `set`.

##### Parametri {#parameters-setitem}

* **`key`:** (Stringa) Nome della chiave.
* **`options`:** (Oggetto) Oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * `silent`: valore di `true` impedisce l&#39;attivazione della `data` evento. Il valore predefinito è `false`.
* **`value`:** (Oggetto) Valore da associare alla chiave.

##### Restituisce {#returns-setitem}

A `boolean` valore:

* Un valore di `true` indica che l’oggetto dati è stato archiviato.
* Un valore di `false` indica che l&#39;archivio dati è invariato.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Archivio che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno o, facoltativamente, da un servizio che restituisce dati JSON. Specifica i dettagli del servizio utilizzando [`init`](#init-name-config) quando si crea un&#39;istanza di questa classe.

L’archivio utilizza la persistenza in memoria (variabile JavaScript). I dati del Negozio sono disponibili solo per la durata della pagina.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](#contexthub-store-core) ed eredita le funzioni di tale classe.

### Funzioni (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura i dettagli per la connessione al servizio JSONP utilizzato da questo oggetto. Puoi aggiornare o sostituire la configurazione esistente. La funzione non restituisce alcun valore.

##### Parametri {#parameters-configureservice}

* **`serviceConfig`:** Oggetto contenente le seguenti proprietà:
   * `host`: (Stringa) nome o indirizzo IP del server.
   * `jsonp`: (booleano) il valore true indica che il servizio è un servizio JSONP; in caso contrario, false indica che si tratta di un servizio JSONP. Se è true, il callback {callback: &quot;ContextHub.Callbacks.*Object.name*} viene aggiunto all&#39;oggetto service.params.
   * `params`: (Oggetto) parametri URL rappresentati come proprietà dell’oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
   * `path`: (Stringa) percorso del servizio.
   * `port`: (Numero) il numero di porta del servizio.
   * `secure`: (stringa o booleano) determina il protocollo da utilizzare per l’URL del servizio:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **sostituisci:** (Booleano). Un valore di `true` fa sì che la configurazione del servizio esistente venga sostituita dalle proprietà di `serviceConfig`. Un valore di `false` determina l&#39;unione delle proprietà di configurazione del servizio esistenti con le proprietà di `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Restituisce la risposta non elaborata memorizzata nella cache dall&#39;ultima chiamata al servizio JSONP. La funzione non richiede parametri.

##### Restituisce {#returns-getrawresponse}

Oggetto che rappresenta la risposta raw.

#### getServiceDetails() {#getservicedetails}

Recupera l&#39;oggetto servizio per l&#39;oggetto ContextHub.Store.JSONPStore. L&#39;oggetto servizio contiene le informazioni necessarie per creare l&#39;URL del servizio.

##### Restituisce {#returns-getservicedetails}

Oggetto con le seguenti proprietà:

* **`host`:** (Stringa) Nome o indirizzo IP del server.
* **`jsonp`:** (Booleano) Il valore true indica che il servizio è un servizio JSONP, in caso contrario false. Se è true, il callback {callback: &quot;ContextHub.Callbacks.*Object.name*} viene aggiunto all&#39;oggetto service.params.
* **`params`:** (Oggetto) Parametri URL rappresentati come proprietà oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
* **`path`:** (Stringa) Percorso del servizio.
* **`port`:** (Numero) Il numero di porta del servizio.
* **`secure`:** (Stringa o booleano) Determina il protocollo da utilizzare per l&#39;URL del servizio:
   * `auto`: //
   * `true`: https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera l’URL del servizio JSONP.

##### Parametri {#parameters-getserviceurl}

* **`resolve`:** (Booleano) Determina se includere i parametri risolti nell’URL. Un valore di `true` risolve i parametri e `false` non lo fa.

##### Restituisce {#returns-getserviceurl}

A `string` valore che rappresenta l’URL del servizio.

#### init(name, config) {#init-name-config-1}

inizializza `ContextHub.Store.JSONPStore` oggetto.

##### Parametri {#parameters-init-1}

* **`name`:** (Stringa) Nome dell’archivio.
* **`config`:** (Oggetto) Oggetto contenente la proprietà service. L&#39;oggetto JSONPStore utilizza le proprietà `service` oggetto per creare l&#39;URL del servizio JSONP:
   * `eventDeferring`: 32.
   * `eventing`: oggetto ContextHub.Utils.Eventing per questo archivio. Il valore predefinito è `ContextHub.eventing` oggetto.
   * `persistence`: oggetto ContextHub.Utils.Persistence per questo archivio. Per impostazione predefinita, viene utilizzata la persistenza della memoria (oggetto JavaScript).
   * `service`: (oggetto)
      * `host`: (Stringa) nome o indirizzo IP del server.
      * `jsonp`: (booleano) il valore true indica che il servizio è un servizio JSONP; in caso contrario, false indica che si tratta di un servizio JSONP. Se è true, la proprietà `{callback: "ContextHub.Callbacks.*Object.name*}`l&#39;oggetto viene aggiunto a `service.params`.
      * `params`: (Oggetto) parametri URL rappresentati come proprietà dell’oggetto. I nomi e i valori dei parametri sono rispettivamente i nomi e i valori delle proprietà dell&#39;oggetto.
      * `path`: (Stringa) percorso del servizio.
      * `port`: (Numero) il numero di porta del servizio.
      * `secure`: (stringa o booleano) determina il protocollo da utilizzare per l’URL del servizio:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Numero) il tempo di attesa della risposta del servizio JSONP prima del timeout, in millisecondi.
         * `ttl`: tempo minimo in millisecondi che trascorre tra le chiamate al servizio JSONP. (consultare la [queryService](#queryservice-reload) funzione ).

#### queryService(reload) {#queryservice-reload}

Interroga il servizio JSONP remoto e memorizza nella cache la risposta. Se il tempo trascorso dalla precedente chiamata a questa funzione è inferiore al valore di `config.service.ttl`, il servizio non viene chiamato e la risposta nella cache non viene modificata. Facoltativamente, puoi forzare la chiamata del servizio. Il `config.service.ttl`viene impostata quando si chiama [init](#init-name-config) per inizializzare l&#39;archivio.

Attiva l&#39;evento ready al termine della query. Se l&#39;URL del servizio JSONP non è impostato, la funzione non esegue alcuna operazione.

##### Parametri {#parameters-queryservice}

* **`reload`:** (Booleano) Il valore true rimuove la risposta dalla cache e forza la chiamata al servizio JSONP.

#### ripristina {#reset}

Reimposta i valori iniziali dei dati persistenti dell&#39;archivio, quindi chiama il servizio JSONP. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo archivio mentre i valori iniziali vengono reimpostati. Questa funzione non restituisce alcun valore.

I valori iniziali vengono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Un valore true determina la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveParameter(f) {#resolveparameter-f}

Risolve il parametro specificato.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` si estende [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) quindi eredita tutte le funzioni di quella classe. Tuttavia, i dati recuperati dal servizio JSONP vengono mantenuti in base alla configurazione della persistenza di ContextHub. (vedere [Modalità di persistenza:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` si estende [ContextHub.Store.Core](#contexthub-store-core) quindi eredita tutte le funzioni di quella classe. I dati in questo archivio vengono salvati in modo permanente in base alla configurazione della persistenza di ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` si estende [ContextHub.Store.Core](#contexthub-store-core) quindi eredita tutte le funzioni di quella classe. I dati in questo archivio vengono salvati in modo permanente utilizzando la persistenza in memoria (oggetto JavaScript).

## ContextHub.UI {#contexthub-ui}

Gestisce i moduli UI e i renderer dei moduli UI.

### Funzioni (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un modulo di rendering dell’interfaccia utente con ContextHub. Dopo la registrazione, il renderer può essere utilizzato per [creare moduli UI](configuring-contexthub.md#adding-a-ui-module). Utilizza questa funzione quando sei [estensione `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) per creare un modulo di rendering dell&#39;interfaccia utente personalizzato.

##### Parametri {#parameters-registerrenderer}

* **`moduleType`:** (Stringa) Identificatore del modulo di rendering dell’interfaccia utente. Se un renderer è già registrato utilizzando il valore specificato, la registrazione del renderer esistente viene annullata prima della registrazione del renderer.
* **`renderer`:** (Stringa) Nome della classe che esegue il rendering del modulo dell’interfaccia utente.
* **`dontRender`:** (Booleano) Imposta su `true` per impedire che venga eseguito il rendering dell’interfaccia utente di ContextHub dopo la registrazione del renderer. Il valore predefinito è `false`.

##### Esempio {#example-registerrenderer}

Nell&#39;esempio seguente viene registrato un renderer come `contexthub.browserinfo` tipo di modulo.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Classe di utilità per l&#39;interazione con i cookie.

### Funzioni (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se esiste un cookie.

##### Parametri {#parameters-exists}

* **`key`:** A `String` che contiene la chiave del cookie per il quale stai eseguendo il test.

##### Restituisce {#returns-exists}

A `boolean` il valore true indica che il cookie esiste.

##### Esempio {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Restituisce tutti i cookie con chiavi che corrispondono a un filtro.

##### Parametri {#parameters-getallitems}

* **`filter`:** (Facoltativo) Criteri per la corrispondenza delle chiavi dei cookie. Per restituire tutti i cookie, non specificare alcun valore. Sono supportati i seguenti tipi:
   * Stringa: la stringa viene confrontata con la chiave del cookie.
   * Array: ogni elemento nell’array è un filtro.
   * Un oggetto RegExp: la funzione di test dell’oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Una funzione: funzione che verifica una chiave cookie per rilevare una corrispondenza. La funzione deve accettare la chiave del cookie come parametro e restituire true se il test conferma una corrispondenza.

##### Restituisce {#returns-getallitems}

Oggetto dei cookie. Le proprietà dell’oggetto sono chiavi di cookie e i valori chiave sono valori di cookie.

##### Esempio {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Restituisce un valore di cookie.

##### Parametri {#parameters-getitem-1}

* **`key`:** Chiave del cookie di cui desideri il valore.

##### Restituisce {#returns-getitem-1}

Il valore del cookie, oppure `null` se non è stato trovato alcun cookie per la chiave.

##### Esempio {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Restituisce una matrice delle chiavi dei cookie esistenti che corrispondono a un filtro.

##### Parametri {#parameters-getkeys-1}

* **`filter`:** Criteri per la corrispondenza delle chiavi dei cookie. Sono supportati i seguenti tipi:
   * Stringa: la stringa viene confrontata con la chiave del cookie.
   * Array: ogni elemento nell’array è un filtro.
   * Un oggetto RegExp: la funzione di test dell’oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Una funzione: funzione che verifica una chiave cookie per rilevare una corrispondenza. La funzione deve accettare la chiave del cookie come parametro e restituire `true` se il test conferma una corrispondenza.

##### Restituisce {#returns-getkeys-1}

Matrice di stringhe in cui ogni stringa è la chiave di un cookie che corrisponde al filtro.

##### Esempio {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Rimuovi un cookie. Per rimuovere il cookie, il valore viene impostato su una stringa vuota e la data di scadenza viene impostata sul giorno precedente alla data corrente.

##### Parametri {#parameters-removeitem-1}

* **`key`:** A `String` valore che rappresenta la chiave del cookie da rimuovere.
* **`options`:** Oggetto contenente i valori delle proprietà per la configurazione degli attributi dei cookie. Consulta la [`setItem`](#setitem-key-value-options) per informazioni. Il `expires` non ha alcun effetto.

##### Restituisce {#returns-removeitem-1}

Questa funzione non restituisce un valore.

##### Esempio {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea un cookie della chiave e del valore specificati e aggiunge il cookie al documento corrente. Facoltativamente, puoi specificare le opzioni che configurano gli attributi del cookie.

##### Parametri {#parameters-setitem-1}

* **`key`:** Stringa che contiene la chiave del cookie.
* **`value`:** Stringa che contiene il valore del cookie.
* **`options`:** (Facoltativo) Oggetto contenente una delle seguenti proprietà che configurano gli attributi del cookie:
   * `expires`: A `date` o `number` valore che specifica quando scade il cookie. Un valore di data specifica l&#39;ora assoluta di scadenza. Un numero (in giorni) imposta l&#39;ora di scadenza sull&#39;ora corrente più il numero. Il valore predefinito è `undefined`.
   * `secure`: A `boolean` valore che specifica `Secure` attributo del cookie. Il valore predefinito è `false`.
   * `path`: A `String` valore da utilizzare come `Path` attributo del cookie. Il valore predefinito è `undefined`.

##### Restituisce {#returns-setitem-1}

Cookie con il valore impostato.

##### Esempio {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filtro, opzioni) {#vanish-filter-options}

Rimuove tutti i cookie che corrispondono a un determinato filtro. I cookie vengono confrontati utilizzando `getKeys` e rimossi utilizzando `removeItem` funzione.

##### Parametri {#parameters-vanish}

* **`filter`:** Il `filter` argomento da utilizzare nella chiamata al [`getKeys`](#getkeys-filter) funzione.
* **`options`:** Il `options` argomento da utilizzare nella chiamata al [`removeItem`](#removeitem-key-options) funzione.

##### Restituisce {#returns-vanish}

Questa funzione non restituisce un valore.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Consente di associare e annullare l’associazione di funzioni agli eventi store ContextHub. Accesso `ContextHub.Utils.Eventing` oggetti per un archivio utilizzando [evento](#eventing) dell&#39;archivio.

### Funzioni (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Scollega una funzione da un evento.

##### Parametri {#parameters-off}

* **`name`:** Il [nome dell’evento](#contexthub-utils-eventing) per cui si sta annullando l’associazione della funzione.
* **`selector`:** Selettore che identifica l&#39;associazione. (consultare la `selector` parametro per [`on`](#on-name-handler-selector-triggerforpastevents) e [`once`](#once-name-handler-selector-triggerforpastevents) funzioni ).

##### Restituisce {#returns-off}

Questa funzione non restituisce alcun valore.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Associazione una funzione a un evento. La funzione viene chiamata ogni volta che si verifica l’evento. Facoltativamente, la funzione può essere chiamata per eventi che si sono verificati in passato, prima che l’associazione venga stabilita.

##### Parametri {#parameters-on}

* **`name`:** (Stringa) Il [nome dell’evento](#contexthub-utils-eventing) a cui si sta associando la funzione.
* **`handler`:** (Funzione) Funzione da associare all’evento.
* **`selector`:** (Stringa) Identificatore univoco del binding. È necessario il selettore per identificare l&#39;associazione se si desidera utilizzare `off` per rimuovere l&#39;associazione.
* **`triggerForPastEvents`:** (Booleano) Indica se il gestore deve essere eseguito per eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Restituisce {#returns-on}

Quando `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l’evento si è verificato in passato:

* `true`: l’evento si è verificato in passato e il gestore viene chiamato.
* `false`: l’evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

##### Esempio {#example-on}

L’esempio seguente associa una funzione all’evento dati dell’archivio di geolocalizzazione. La funzione compila un elemento sulla pagina con il valore per l’elemento di dati di latitudine dall’archivio.

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

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Associazione una funzione a un evento. La funzione viene chiamata una sola volta, per la prima occorrenza dell’evento. Facoltativamente, la funzione può essere chiamata per l’evento che si è verificato in passato, prima che l’associazione venga stabilita.

##### Parametri {#parameters-once}

* **`name`:** (Stringa) Il [nome dell’evento](#contexthub-utils-eventing) a cui si sta associando la funzione.
* **`handler`:** (Funzione) Funzione da associare all’evento.
* **`selector`:** (Stringa) Identificatore univoco del binding. È necessario il selettore per identificare l&#39;associazione se si desidera utilizzare `off` per rimuovere l&#39;associazione.
* **`triggerForPastEvents`:** (Booleano) Indica se il gestore deve essere eseguito per eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Restituisce {#returns-once}

Quando `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l’evento si è verificato in passato:

* `true`: l’evento si è verificato in passato e il gestore viene chiamato.
* `false`: l’evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Classe di utilità che consente a un oggetto di ereditare le proprietà e i metodi di un altro oggetto.

### Funzioni (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Fa sì che un oggetto erediti le proprietà e i metodi di un altro oggetto.

##### Parametri {#parameters-inherit}

* **`child`:** (Oggetto) L’oggetto che eredita.
* **`parent`:** (Oggetto) Oggetto che definisce le proprietà e i metodi ereditati.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornisce funzioni per serializzare gli oggetti in formato JSON e deserializzare le stringhe JSON negli oggetti.

### Funzioni (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analizza un valore stringa come JSON e lo converte in un oggetto JavaScript.

##### Parametri {#parameters-parse}

* **`data`:** Valore stringa in formato JSON.

##### Restituisce {#returns-parse}

Oggetto JavaScript.

##### Esempio {#example-parse}

Il codice:

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

Restituisce il seguente oggetto:

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringivy(data) {#stringify-data}

Serializza i valori e gli oggetti JavaScript in valori stringa in formato JSON.

##### Parametri {#parameters-stringify}

* **`data`:** Valore o oggetto da serializzare. Questa funzione supporta valori booleani, di matrice, numerici, stringa e di data.

##### Restituisce {#returns-stringify}

Valore stringa serializzato. Quando `data` è una R `egExp` questa funzione restituisce un oggetto vuoto. Quando `data` è una funzione, restituisce `undefined`.

##### Esempio {#example-stringify}

Il seguente codice:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Restituisce:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Questa classe facilita la manipolazione degli oggetti dati che devono essere memorizzati o che vengono recuperati dagli archivi ContextHub.

### Funzioni (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia di un oggetto dati e vi aggiunge la struttura dati da un secondo oggetto. La funzione restituisce la copia e non modifica nessuno degli oggetti originali. Quando gli alberi dati dei due oggetti contengono chiavi identiche, il valore del secondo oggetto sovrascrive il valore del primo oggetto.

##### Parametri {#parameters-addallitems-1}

* **`tree`:** Oggetto copiato.
* **`secondTree`:** Oggetto che viene unito alla copia del `tree` oggetto.

##### Restituisce {#returns-addallitems-1}

Oggetto contenente i dati uniti.

#### cleanup() {#cleanup}

Crea una copia di un oggetto, trova e rimuove elementi nella struttura dati che non contengono valori, valori Null o valori non definiti e restituisce la copia.

##### Parametri {#parameters-cleanup}

* **`tree`:** Oggetto da pulire.

##### Restituisce {#returns-cleanup}

Copia dell&#39;albero pulita.

#### getItem() {#getitem}

Recupera il valore da un oggetto per la chiave.

##### Parametri {#parameters-getitem-2}

* **`tree`:** L’oggetto dati.
* **`key`:** Chiave del valore che si desidera recuperare.

##### Restituisce {#returns-getitem-2}

Valore corrispondente alla chiave. Quando la chiave ha chiavi secondarie, questa funzione restituisce un oggetto complesso. Quando il tipo di valore per la chiave è `undefined`, `null` viene restituito.

##### Esempio {#example-getitem-2}

Considera il seguente oggetto JavaScript:

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

Il codice di esempio seguente restituisce il valore `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

Il codice di esempio seguente recupera il valore di una chiave con chiavi secondarie:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La funzione restituisce il seguente oggetto:

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

Recupera tutte le chiavi dalla struttura dati di un oggetto. Facoltativamente, puoi recuperare solo le chiavi degli elementi secondari di una chiave specifica. Facoltativamente, puoi anche specificare l’ordinamento delle chiavi recuperate.

##### Parametri {#parameters-getkeys-2}

* **`tree`:** Oggetto da cui recuperare le chiavi della struttura dati.
* **`parent`:** (Facoltativo) Chiave di un elemento nella struttura dati per il quale si desidera recuperare le chiavi degli elementi figlio.
* **`order`:** (Facoltativo) Funzione che determina l&#39;ordinamento delle chiavi restituite. (vedere [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) su Mozilla Developer Network.)

##### Restituisce {#returns-getkeys-2}

Matrice di chiavi.

##### Esempio {#example-getkeys-2}

Considera il seguente oggetto:

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

Il `ContextHub.Utils.JSON.tree.getKeys(myObject);` script restituisce il seguente array:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia di un determinato oggetto, rimuove il ramo specificato dalla struttura dati e restituisce la copia modificata.

##### Parametri {#parameters-removeitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** Chiave da rimuovere.

##### Restituisce {#returns-removeitem-2}

Copia dell&#39;oggetto dati originale con la chiave rimossa.

##### Esempio {#example-removeitem-2}

Considera il seguente oggetto:

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

Lo script di esempio seguente rimuove il ramo /one/two/three/four dalla struttura dati:

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La funzione restituisce il seguente oggetto:

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Sanitizza i valori stringa per renderli utilizzabili come chiavi. Per bonificare una stringa, questa funzione esegue le azioni seguenti:

* Riduce più barre consecutive in avanti a una singola barra.
* Rimuove lo spazio vuoto dall&#39;inizio e dalla fine della stringa.
* Divide il risultato in una matrice di stringhe delimitate da barre.

Utilizza l’array risultante per creare una chiave utilizzabile.

##### Parametri {#parameters-sanitizekey}

* **`key`:** Il `string` per bonificare.

##### Restituisce {#returns-sanitizekey}

Un array di `string` valori in cui ogni stringa è la porzione della `key` che era delimitata da barre. rappresenta la chiave bonificata. Se la lunghezza dell’array bonificato è zero, questa funzione restituisce `null`.

##### Esempio {#example-sanitizekey}

Il codice seguente bonifica una stringa per produrre l’array `["this", "is", "a", "path"]`, quindi genera la chiave `"/this/is/a/path"` dall’array:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Aggiunge una coppia chiave/valore alla struttura dati di una copia di un oggetto. Per informazioni sulle strutture dati, vedi [Persistenza.](contexthub.md#persistence)

##### Parametri {#parameters-setitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** Chiave da associare al valore che si sta aggiungendo. La chiave è il percorso dell&#39;elemento nella struttura dati. Questa funzione chiama `ContextHub.Utils.JSON.tree.sanitize` per bonificare la chiave prima di aggiungerla.
* **`value`:** Valore da aggiungere alla struttura dati.

##### Restituisce {#returns-setitem-2}

Una copia della `tree` oggetto che include `key`/ `value` coppia.

##### Esempio {#example-setitem-2}

Considera il seguente codice JavaScript:

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

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Consente di registrare i candidati per lo store e di ottenere i candidati per lo store registrati.

### Funzioni (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Restituisce i tipi di punto vendita registrati come candidati. Recupera i candidati registrati di un tipo di archivio specifico o di tutti i tipi di archivio.

##### Parametri {#parameters-getregisteredcandidates}

* **`storeType`:** (Stringa) Nome del tipo di archivio. Consulta la `storeType` parametro di [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione.

##### Restituisce {#returns-getregisteredcandidates}

Oggetto di tipo store. Le proprietà dell&#39;oggetto sono i nomi dei tipi di archivio e i valori delle proprietà sono una matrice dei candidati di archivio registrati.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Restituisce un tipo di archivio dai candidati registrati. Se sono registrati più tipi di archivio con lo stesso nome, la funzione restituisce il tipo di archivio con la priorità più elevata.

##### Parametri {#parameters-getstorefromcandidates}

* `storeType`: (Stringa) nome del candidato dell’archivio. Consulta la `storeType` parametro di [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) funzione.

##### Restituisce {#returns-getstorefromcandidates}

Oggetto che rappresenta il candidato dell&#39;archivio registrato. Se il tipo di archivio richiesto non è registrato, viene generato un errore.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Restituisce i nomi dei tipi di punto vendita registrati come candidati. Questa funzione non richiede parametri.

##### Restituisce {#returns-getsupportedstoretypes}

Matrice di valori stringa, in cui ogni stringa è lo storetype con cui è stato registrato il candidato dell&#39;archivio. Consulta la `storeType` parametro di [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione.

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra un oggetto store come candidato all&#39;archivio utilizzando un nome e una priorità.

La priorità è un numero che indica l&#39;importanza degli archivi con lo stesso nome. Quando un candidato per lo store viene registrato con lo stesso nome di un candidato per lo store già registrato, viene utilizzato il candidato con la priorità più elevata. Quando si registra un candidato per un punto vendita, l&#39;archivio viene registrato solo se la priorità è superiore a quella dei candidati per lo stesso punto vendita registrati con lo stesso nome.

##### Parametri {#parameters-registerstorecandidate}

* **`store`:** (Oggetto) Oggetto store da registrare come candidato per lo store.
* **`storeType`:** (Stringa) Il nome del candidato dell’archivio. Questo valore è necessario quando si crea un’istanza del candidato per lo store.
* **`priority`:** (Numero) La priorità del candidato del punto vendita.
* **`applies`:** (Funzione) La funzione da richiamare che valuta l’applicabilità dell’archivio nell’ambiente corrente. La funzione deve restituire `true` se il deposito è idoneo, e `false` altrimenti. Il valore predefinito è una funzione che restituisce true: `function() {return true;}`

##### Esempio {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
