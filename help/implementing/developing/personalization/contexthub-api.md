---
title: Riferimento API di ContextHub Javascript
description: L’API Javascript di ContextHub è disponibile per i tuoi script quando il componente ContextHub è stato aggiunto alla pagina
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 3%

---

# Riferimento API di ContextHub Javascript {#contexthub-javascript-api-reference}

L’API JavaScript di ContextHub è disponibile per gli script quando [Il componente ContextHub è stato aggiunto alla pagina](adding-contexthub.md).

## Costanti ContextHub {#contexthub-constants}

Valori costanti definiti dall’API Javascript di ContextHub.

### Costanti evento {#event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per gli archivi ContextHub. Vedi anche [ContextHub.Utils.Event](#contexthub-utils-eventing).

| Costante | Descrizione | Valore |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Spazio dei nomi evento di ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica che tutti gli archivi richiesti sono registrati, inizializzati e pronti per essere consumati | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica che non tutti gli archivi sono stati inizializzati entro un determinato timeout | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Generato quando un negozio è registrato | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica che gli archivi sono pronti per funzionare. Viene attivato immediatamente dopo la registrazione, ad eccezione degli archivi JSONP, dove viene attivato quando i dati vengono recuperati). | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Generato quando un archivio aggiorna la sua persistenza | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nome del contenitore di persistenza | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Memorizza il nome della chiave di persistenza specifica in cui è memorizzato il risultato JSON non elaborato | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Memorizza una marca temporale specifica che indica quando sono stati recuperati i dati JSON | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Memorizza l’url specifico del servizio JSON utilizzato durante l’ultima chiamata | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica se l’interfaccia utente di ContextHub è espansa | `/_/container-expanded` |

### Costanti evento dell’interfaccia utente {#ui-event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per l’interfaccia utente di ContextHub.

| **Costante** | **Descrizione** | **Valore** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Attivazione quando viene registrata una modalità | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Attivato quando una modalità non è registrata | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Generato quando viene registrato un renderer di modalità | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Generato quando un renderer di modalità non è registrato | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Attivazione quando viene aggiunta una nuova modalità | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Attivato quando viene rimossa una modalità | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Attivazione quando l’utente seleziona una modalità | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Generato quando viene registrato un nuovo modulo | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Generato quando un modulo non viene registrato | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Generato quando un modulo di rendering è registrato | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Generato quando un modulo di rendering non viene registrato | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Generato quando viene aggiunto un nuovo modulo | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Generato quando un modulo viene rimosso | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Generato quando il contenitore dell’interfaccia utente viene aggiunto alla pagina | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Attivazione all’apertura dell’interfaccia utente di ContextHub | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Attivazione quando l’interfaccia utente di ContextHub viene compressa | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Generato quando una proprietà viene modificata | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Viene attivata ogni volta che viene eseguito il rendering dell’interfaccia utente di ContextHub (ad esempio dopo una modifica della proprietà) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Generato quando il contenitore dell’interfaccia utente viene inizializzato | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica la modalità di interfaccia attiva | `/_/active-ui-mode` |

## Riferimento API di ContextHub Javascript {#contexthub-javascript-api-reference-2}

L&#39;oggetto ContextHub fornisce l&#39;accesso a tutti gli archivi.

### Funzioni (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Restituisce tutti gli archivi ContextHub registrati.

Questa funzione non dispone di parametri.

##### Valore restituito {#returns-}

Un oggetto che contiene tutti gli archivi ContextHub. Ogni archivio è un oggetto che utilizza lo stesso nome dell&#39;archivio.

##### Esempio {#example-}

L&#39;esempio seguente recupera tutti gli archivi e quindi recupera l&#39;archivio di geolocalizzazione:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera un archivio come oggetto Javascript.

##### Parametri {#parameters-}

* **`name`:** Nome con cui è stato registrato il negozio.

##### Valore restituito {#returns-getstore-name}

Oggetto che rappresenta l&#39;archivio.

##### Esempio {#example-getstore-name}

L&#39;esempio seguente recupera l&#39;archivio di geolocalizzazione:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Rappresenta un segmento ContextHub. Utilizza la `ContextHub.SegmentEngine.SegmentManager` per ottenere segmenti.

### Funzioni (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Restituisce il nome del segmento come valore String.

#### getPath() {#getpath}

Restituisce il percorso del repository della definizione del segmento come valore String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Consente l’accesso ai segmenti ContextHub.

### Funzioni (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Restituisce i segmenti risolti nel contesto corrente. Questa funzione non dispone di parametri.

##### Valore restituito {#returns-getresolvedsegments}

Matrice di `ContextHub.SegmentEngine.Segment` oggetti.

## ContextHub.Store.Core {#contexthub-store-core}

La classe di base per gli archivi ContextHub.

### Proprietà (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

A [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) oggetto. Utilizzare questo oggetto per eseguire il binding delle funzioni per memorizzare gli eventi. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

#### name {#name}

Nome del negozio.

#### persistenza {#persistence}

A `ContextHub.Utils.Persistence` oggetto. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [`init(name,config)`](#init-name-config).

### Funzioni (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Unisce un oggetto dati o una matrice ai dati archiviati. Ogni coppia chiave/valore nell&#39;oggetto o nella matrice viene aggiunta all&#39;archivio (tramite `setItem` funzione):

* **Oggetto:** Le chiavi sono i nomi delle proprietà.
* **Matrice:** Le chiavi sono gli indici della matrice.

I valori possono essere oggetti.

##### Parametri {#parameters-addallitems}

* **`tree`:** (Oggetto o matrice) I dati da aggiungere all&#39;archivio.
* **`options`:** (Oggetto) Un oggetto facoltativo di opzioni passato alla funzione setItem. Per informazioni, consulta la sezione `options` parametro di [`setItem(key,value,options)`](#setitem-key-value-options).

##### Valore restituito {#returns-addallitems}

A `boolean` valore:

* Un valore di `true` indica che l’oggetto dati è stato memorizzato.
* Un valore di `false` indica che l&#39;archivio dati è invariato.

#### addReference(key, otherKey) {#addreference-key-anotherkey}

Crea un riferimento da una chiave a un&#39;altra chiave. Una chiave non può fare riferimento a se stessa.

##### Parametri {#parameters-addreference}

* **`key`:** Chiave a cui fa riferimento `anotherKey`.

* **`anotherkey`:** Chiave a cui fa riferimento `key`.

##### Valore restituito {#returns-addreference}

A `boolean` valore:

* Un valore di `true` indica che il riferimento è stato aggiunto.
* Un valore di `false` indica che non è stato aggiunto alcun riferimento.

#### annuncioReadiness() {#announcereadiness}

Attiva la `ready` evento per questo archivio. Questa funzione non ha parametri e non restituisce alcun valore.

#### clean() {#clean}

Rimuove tutti i dati dall’archivio. La funzione non dispone di parametri e di valori restituiti.

#### getItem(key) {#getitem-key}

Restituisce il valore associato a una chiave.

##### Parametri {#parameters-getitem}

* **`key`:** (Stringa) La chiave per la quale restituire il valore.

##### Valore restituito {#returns-getitem}

Oggetto che rappresenta il valore della chiave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera le chiavi dall&#39;archivio. Facoltativamente, puoi recuperare le chiavi utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-getkeys}

* **`includeInternals`:** Un valore di `true` include nei risultati le chiavi utilizzate internamente. Queste chiavi iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Valore restituito {#returns-getkeys}

Matrice di nomi chiave ( `string` ).

#### getReferences() {#getreferences}

Recupera i riferimenti dall&#39;archivio.

##### Valore restituito {#returns-getreferences}

Matrice che utilizza le chiavi di riferimento come indici per le chiavi di riferimento:

* Le chiavi di riferimento corrispondono alle `key` del `addReference` funzione .
* Le chiavi di riferimento corrispondono alle `anotherKey` del `addReference` funzione .

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera la struttura dati dall&#39;archivio. Facoltativamente, puoi includere le coppie chiave/valore utilizzate internamente dal framework ContextHub.

##### Parametri {#parameters-gettree}

* `includeInternals:` Un valore di `true` include nei risultati coppie chiave/valore utilizzate internamente. Le chiavi di questi dati iniziano con il carattere di sottolineatura (`_`). Il valore predefinito è `false`.

##### Valore restituito {#returns-gettree}

Oggetto che rappresenta la struttura dati. Le chiavi sono i nomi delle proprietà dell&#39;oggetto.

#### init(name, config) {#init-name-config}

Inizializza l&#39;archivio.

* Imposta i dati dell&#39;archivio su un oggetto vuoto.
* Imposta i riferimenti dell&#39;archivio su un oggetto vuoto.
* La `eventChannel` è `data:<name>`, dove `<name>` è il nome del negozio.
* La `storeDataKey` è `/store/<name>`, dove `<name>` è il nome del negozio.

##### Parametri {#parameters-init}

* **`name`:** Nome del negozio.
* **`config`:** Un oggetto che contiene le proprietà di configurazione:
   * `eventDeferring`: Il valore predefinito è 32.
   * `eventing`: La [ContextHub.Utils.Event](#contexthub-utils-eventing) oggetto per questo archivio. Il valore predefinito è il `ContextHub.eventing` viene utilizzato dall&#39;oggetto .
   * `persistence`: La `ContextHub.Utils.Persistence` oggetto per questo archivio. Il valore predefinito è il `ContextHub.persistence` oggetto.

#### isEventingPaused() {#iseventingpaused}

Determina se l&#39;evento viene messo in pausa per questo archivio.

##### Valore restituito {#returns-iseventingpaused}

Un valore booleano:

* `true`: L&#39;evento viene messo in pausa in modo che non vengano attivati eventi per questo archivio.
* `false`: L&#39;evento non viene messo in pausa in modo che gli eventi vengano attivati per questo archivio.

#### pauseEvent() {#pauseeventing}

Sospende l&#39;evento per l&#39;archivio in modo che non vengano attivati eventi. Questa funzione non richiede parametri e non restituisce alcun valore.

#### removeItem(key, options) {#removeitem-key-options}

Rimuove una coppia chiave/valore dall’archivio.

Quando una chiave viene rimossa, la funzione attiva la funzione `data` evento. I dati dell&#39;evento includono il nome dell&#39;archivio, il nome della chiave rimossa, il valore rimosso, il nuovo valore per la chiave (null) e il tipo di azione &quot;remove&quot;.

Facoltativamente, puoi impedire l’attivazione del `data` evento.

##### Parametri {#parameters-removeitem}

* **`key`:** (Stringa) Il nome della chiave da rimuovere.
* **`options`:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * silenzioso: Un valore di `true` impedisce l&#39;attivazione del `data` evento. Il valore predefinito è `false`.

##### Valore restituito {#returns-removeitem}

A `boolean` valore:

* Un valore di `true` indica che la coppia chiave/valore è stata rimossa.
* Un valore di `false` indica che l&#39;archivio dati è invariato perché la chiave non è stata trovata nell&#39;archivio.

#### removeReference(key) {#removereference-key}

Rimuove un riferimento dall&#39;archivio.

##### Parametri {#parameters-removereference}

* **`key`:** Riferimento chiave da rimuovere. Questo parametro corrisponde alla variabile `key` del `addReference` funzione .

##### Valore restituito {#returns-removereference}

A `boolean` valore:

* Un valore di `true` indica che il riferimento è stato rimosso.
* Un valore di `false` indica che la chiave non era valida e che l&#39;archivio è invariato.

#### reset(keepRemainData) {#reset-keepremainingdata}

Ripristina i valori iniziali dei dati persistenti dell&#39;archivio. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo negozio mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella variabile `initialValues` proprietà dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset}

* **`keepRemainingData`**: (Booleano) Un valore true causa la persistenza dei dati non iniziali. Il valore false causa la rimozione di tutti i dati, ad eccezione dei valori iniziali.

#### resolveReference(key, try) {#resolvereference-key-retry}

Recupera una chiave di riferimento. Facoltativamente, puoi specificare il numero di iterazioni da utilizzare per risolvere la corrispondenza migliore.

##### Parametri {#parameters-resolvereference}

* **`key`:** (Stringa) La chiave per la quale risolvere il riferimento. Questo `key` corrisponde a `key` del `addReference` funzione .
* **`retry`:** (Numero) Il numero di iterazioni da utilizzare.

##### Valore restituito {#returns-resolvereference}

A `string` che rappresenta la chiave di riferimento. Se non viene risolto alcun riferimento, il valore del `key` viene restituito il parametro .

#### curriculumEventing() {#resumeeventing}

Riprende gli eventi per questo archivio in modo che gli eventi vengano attivati. Questa funzione non definisce alcun parametro e non restituisce alcun valore.

#### setItem(key, value, options) {#setitem-key-value-options}

Aggiunge una coppia chiave/valore all’archivio.

Attiva la `data` solo se il valore della chiave è diverso dal valore attualmente memorizzato per la chiave. Facoltativamente, puoi impedire l’attivazione del `data` evento.

I dati dell’evento includono il nome dell’archivio, la chiave, il valore precedente, il nuovo valore e il tipo di azione di `set`.

##### Parametri {#parameters-setitem}

* **`key`:** (Stringa) Il nome della chiave.
* **`options`:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:
   * `silent`: Un valore di `true` impedisce l&#39;attivazione del `data` evento. Il valore predefinito è `false`.
* **`value`:** (Oggetto) Il valore da associare alla chiave.

##### Valore restituito {#returns-setitem}

A `boolean` valore:

* Un valore di `true` indica che l’oggetto dati è stato memorizzato.
* Un valore di `false` indica che l&#39;archivio dati è invariato.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Un archivio che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno o facoltativamente da un servizio che restituisce dati JSON. Specifica i dettagli del servizio utilizzando [`init`](#init-name-config) quando si crea un&#39;istanza di questa classe.

L&#39;archivio utilizza la persistenza in memoria (variabile Javascript). I dati dell’archivio sono disponibili solo per tutta la durata della pagina.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](#contexthub-store-core) e eredita le funzioni di tale classe.

### Funzioni (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura i dettagli della connessione al servizio JSONP utilizzato da questo oggetto. È possibile aggiornare o sostituire la configurazione esistente. La funzione non restituisce alcun valore.

##### Parametri {#parameters-configureservice}

* **`serviceConfig`:** Un oggetto che contiene le seguenti proprietà:
   * `host`: (Stringa) Il nome del server o l&#39;indirizzo IP.
   * `jsonp`: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {è: &quot;ContextHub.Callback.*Object.name*} viene aggiunto all&#39;oggetto service.params.
   * `params`: (Oggetto) Parametri URL rappresentati come proprietà dell’oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
   * `path`: (Stringa) Il percorso del servizio.
   * `port`: (Numero) Il numero di porta del servizio.
   * `secure`: (Stringa o booleana) Determina il protocollo da utilizzare per l&#39;URL del servizio:
      * `auto`: //
      * `true`: https://
      * `false`: Http://
* **override:** (Booleano). Un valore di `true` fa sì che la configurazione del servizio esistente venga sostituita dalle proprietà di `serviceConfig`. Un valore di `false` fa sì che le proprietà di configurazione del servizio esistenti vengano unite alle proprietà di `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Restituisce la risposta non elaborata memorizzata nella cache dall&#39;ultima chiamata al servizio JSONP. La funzione non richiede parametri.

##### Valore restituito {#returns-getrawresponse}

Oggetto che rappresenta la risposta non elaborata.

#### getServiceDetails() {#getservicedetails}

Recupera l&#39;oggetto del servizio per questo oggetto ContextHub.Store.JSONPStore. L&#39;oggetto service contiene tutte le informazioni necessarie per creare l&#39;URL del servizio.

##### Valore restituito {#returns-getservicedetails}

Un oggetto con le seguenti proprietà:

* **`host`:** (Stringa) Il nome del server o l&#39;indirizzo IP.
* **`jsonp`:** (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {è: &quot;ContextHub.Callback.*Object.name*} viene aggiunto all&#39;oggetto service.params.
* **`params`:** (Oggetto) Parametri URL rappresentati come proprietà dell’oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
* **`path`:** (Stringa) Il percorso del servizio.
* **`port`:** (Numero) Il numero di porta del servizio.
* **`secure`:** (Stringa o booleana) Determina il protocollo da utilizzare per l&#39;URL del servizio:
   * `auto`: //
   * `true`: https://
   * `false`: Http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera l&#39;URL del servizio JSONP.

##### Parametri {#parameters-getserviceurl}

* **`resolve`:** (Booleano) Determina se includere nell&#39;URL i parametri risolti. Un valore di `true` risolve i parametri e `false` No.

##### Valore restituito {#returns-getserviceurl}

A `string` che rappresenta l&#39;URL del servizio.

#### init(name, config) {#init-name-config-1}

inizializza il `ContextHub.Store.JSONPStore` oggetto.

##### Parametri {#parameters-init-1}

* **`name`:** (Stringa) Il nome dell&#39;archivio.
* **`config`:** (Oggetto) Un oggetto contenente la proprietà del servizio. L&#39;oggetto JSONPStore utilizza le proprietà `service` oggetto per creare l&#39;URL del servizio JSONP:
   * `eventDeferring`: 32.
   * `eventing`: L&#39;oggetto ContextHub.Utils.Eventing per questo archivio. Il valore predefinito è il `ContextHub.eventing` oggetto.
   * `persistence`: L&#39;oggetto ContextHub.Utils.Persistence per questo archivio. Per impostazione predefinita, viene utilizzata la persistenza della memoria (oggetto Javascript).
   * `service`: (Oggetto)
      * `host`: (Stringa) Il nome del server o l&#39;indirizzo IP.
      * `jsonp`: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Quando è true, il `{callback: "ContextHub.Callbacks.*Object.name*}`viene aggiunto a `service.params`.
      * `params`: (Oggetto) Parametri URL rappresentati come proprietà dell’oggetto. I nomi e i valori dei parametri sono rispettivamente i nomi e i valori delle proprietà dell&#39;oggetto.
      * `path`: (Stringa) Il percorso del servizio.
      * `port`: (Numero) Il numero di porta del servizio.
      * `secure`: (Stringa o booleana) Determina il protocollo da utilizzare per l&#39;URL del servizio:
         * `auto`: //
         * `true`: https://
         * `false`: Http://
      * `timeout`: (Numero) Il tempo di attesa della risposta del servizio JSONP prima del timeout, in millisecondi.
         * `ttl`: La quantità minima di tempo in millisecondi che trascorre tra le chiamate al servizio JSONP. (Vedi [queryService](#queryservice-reload) (funzione).

#### queryService(reload) {#queryservice-reload}

Esegue una query sul servizio JSONP remoto e memorizza nella cache la risposta. Se il tempo trascorso dalla chiamata precedente a questa funzione è inferiore al valore di `config.service.ttl`, il servizio non viene chiamato e la risposta nella cache non viene modificata. Facoltativamente, puoi forzare la chiamata del servizio. La `config.service.ttl`viene impostata quando si chiama il [init](#init-name-config) per inizializzare l&#39;archivio.

Attiva l&#39;evento ready al termine della query. Se l’URL del servizio JSONP non è impostato, la funzione non esegue alcuna operazione.

##### Parametri {#parameters-queryservice}

* **`reload`:** (Booleano) Il valore true rimuove la risposta nella cache e forza la chiamata al servizio JSONP.

#### reset {#reset}

Reimposta i valori iniziali dei dati persistenti dell&#39;archivio e quindi chiama il servizio JSONP. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo archivio mentre i valori iniziali vengono reimpostati. Questa funzione non restituisce alcun valore.

I valori iniziali vengono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

##### Parametri {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Un valore true causa la persistenza dei dati non iniziali. Il valore false causa la rimozione di tutti i dati, ad eccezione dei valori iniziali.

#### resolveParameter(f) {#resolveparameter-f}

Risolve il parametro specificato.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` Estensioni [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) quindi eredita tutte le funzioni di quella classe. Tuttavia, i dati recuperati dal servizio JSONP vengono mantenuti in base alla configurazione della persistenza ContextHub. (Vedi [Modalità di persistenza:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` Estensioni [ContextHub.Store.Core](#contexthub-store-core) quindi eredita tutte le funzioni di quella classe. I dati in questo archivio vengono mantenuti in base alla configurazione della persistenza ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` Estensioni [ContextHub.Store.Core](#contexthub-store-core) quindi eredita tutte le funzioni di quella classe. I dati in questo archivio vengono mantenuti utilizzando la persistenza in memoria (oggetto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestisce i moduli di interfaccia utente e i moduli di rendering dell’interfaccia utente.

### Funzioni (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un modulo di rendering dell&#39;interfaccia utente con ContextHub. Una volta registrato, il renderer può essere utilizzato per [creare moduli di interfaccia](configuring-contexthub.md#adding-a-ui-module). Utilizza questa funzione quando [estensione `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) per creare un modulo di rendering dell’interfaccia utente personalizzato.

##### Parametri {#parameters-registerrenderer}

* **`moduleType`:** (Stringa) L’identificatore del modulo di rendering dell’interfaccia utente. Se un renderer è già registrato utilizzando il valore specificato, il renderer esistente viene annullato prima della registrazione del renderer.
* **`renderer`:** (Stringa) Il nome della classe che esegue il rendering del modulo dell&#39;interfaccia utente.
* **`dontRender`:** (Booleano) Imposta su `true` per impedire il rendering dell’interfaccia utente ContextHub dopo la registrazione del renderer. Il valore predefinito è `false`.

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

* **`key`:** A `String` che contiene la chiave del cookie di cui stai eseguendo il test.

##### Valore restituito {#returns-exists}

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
   * Stringa: La stringa viene confrontata con la chiave cookie.
   * Matrice: Ogni elemento della matrice è un filtro.
   * Un oggetto RegExp: La funzione di test dell&#39;oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Funzione: Funzione che verifica una chiave cookie per una corrispondenza. La funzione deve prendere la chiave del cookie come parametro e restituire true se il test conferma una corrispondenza.

##### Valore restituito {#returns-getallitems}

Un oggetto di cookie. Le proprietà dell’oggetto sono chiavi cookie e i valori chiave sono valori cookie.

##### Esempio {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Restituisce un valore cookie.

##### Parametri {#parameters-getitem-1}

* **`key`:** Chiave del cookie di cui desideri il valore.

##### Valore restituito {#returns-getitem-1}

Il valore del cookie, oppure `null` se non è stato trovato alcun cookie per la chiave.

##### Esempio {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Restituisce una matrice delle chiavi dei cookie esistenti che corrispondono a un filtro.

##### Parametri {#parameters-getkeys-1}

* **`filter`:** Criteri per la corrispondenza delle chiavi dei cookie. Sono supportati i seguenti tipi:
   * Stringa: La stringa viene confrontata con la chiave cookie.
   * Matrice: Ogni elemento della matrice è un filtro.
   * Un oggetto RegExp: La funzione di test dell&#39;oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Funzione: Funzione che verifica una chiave cookie per una corrispondenza. La funzione deve prendere la chiave cookie come parametro e restituire `true` se il test conferma una corrispondenza.

##### Valore restituito {#returns-getkeys-1}

Array di stringhe in cui ogni stringa è la chiave di un cookie che corrisponde al filtro.

##### Esempio {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Rimuove un cookie. Per rimuovere il cookie, il valore è impostato su una stringa vuota e la data di scadenza è impostata sul giorno precedente la data corrente.

##### Parametri {#parameters-removeitem-1}

* **`key`:** A `String` che rappresenta la chiave del cookie da rimuovere.
* **`options`:** Oggetto che contiene i valori delle proprietà per la configurazione degli attributi cookie. Consulta la sezione [`setItem`](#setitem-key-value-options) funzione per informazioni. La `expires` non ha alcun effetto.

##### Valore restituito {#returns-removeitem-1}

Questa funzione non restituisce un valore.

##### Esempio {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea un cookie della chiave e del valore specificati e aggiunge il cookie al documento corrente. Facoltativamente, puoi specificare le opzioni che configurano gli attributi del cookie.

##### Parametri {#parameters-setitem-1}

* **`key`:** Una stringa che contiene la chiave del cookie.
* **`value`:** Una stringa che contiene il valore del cookie.
* **`options`:** (Facoltativo) Un oggetto che contiene una delle seguenti proprietà che configurano gli attributi del cookie:
   * `expires`: A `date` o `number` che specifica quando scade il cookie. Un valore di data specifica l&#39;ora assoluta di scadenza. Un numero (in giorni) imposta l&#39;ora di scadenza all&#39;ora corrente più il numero. Il valore predefinito è `undefined`.
   * `secure`: A `boolean` che specifica il valore `Secure` attributo del cookie. Il valore predefinito è `false`.
   * `path`: A `String` valore da utilizzare come `Path` attributo del cookie. Il valore predefinito è `undefined`.

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

#### vanish(filtro, opzioni) {#vanish-filter-options}

Rimuove tutti i cookie che corrispondono a un determinato filtro. I cookie vengono associati utilizzando `getKeys` e rimossi utilizzando `removeItem` funzione .

##### Parametri {#parameters-vanish}

* **`filter`:** La `filter` argomento da utilizzare nella chiamata al [`getKeys`](#getkeys-filter) funzione .
* **`options`:** La `options` argomento da utilizzare nella chiamata al [`removeItem`](#removeitem-key-options) funzione .

##### Valore restituito {#returns-vanish}

Questa funzione non restituisce un valore.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Consente di eseguire il binding e il binding delle funzioni agli eventi dell’archivio ContextHub. Accesso `ContextHub.Utils.Eventing` oggetti per un archivio che utilizza [evento](#eventing) proprietà dello store.

### Funzioni (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Separa una funzione da un evento.

##### Parametri {#parameters-off}

* **`name`:** La [nome dell’evento](#contexthub-utils-eventing) per cui si sta scollegando la funzione.
* **`selector`:** Il selettore che identifica il binding. (Vedi `selector` per [`on`](#on-name-handler-selector-triggerforpastevents) e [`once`](#once-name-handler-selector-triggerforpastevents) funzioni).

##### Valore restituito {#returns-off}

Questa funzione non restituisce alcun valore.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Associa una funzione a un evento. La funzione viene chiamata ogni volta che si verifica l&#39;evento. Facoltativamente, è possibile chiamare la funzione per gli eventi che si sono verificati in passato, prima che venga stabilito il binding.

##### Parametri {#parameters-on}

* **`name`:** (Stringa) [nome dell’evento](#contexthub-utils-eventing) a cui si sta eseguendo il binding della funzione.
* **`handler`:** (Funzione) La funzione da associare all&#39;evento.
* **`selector`:** (Stringa) Un identificatore univoco per il binding. Per utilizzare il binding, è necessario che il selettore identifichi il binding `off` per rimuovere il binding.
* **`triggerForPastEvents`:** (Booleano) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Valore restituito {#returns-on}

Quando il `triggerForPastEvents` argomento `true`, questa funzione restituisce un `boolean` che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e verrà chiamato il gestore.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

##### Esempio {#example-on}

Nell&#39;esempio seguente viene associata una funzione all&#39;evento dati dell&#39;archivio di geolocalizzazione. La funzione popola un elemento della pagina con il valore dell&#39;elemento dati di latitudine dall&#39;archivio.

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

Associa una funzione a un evento. La funzione viene chiamata una sola volta, per la prima occorrenza dell&#39;evento. Facoltativamente, è possibile chiamare la funzione per l&#39;evento che si è verificato in passato, prima che il binding sia stabilito.

##### Parametri {#parameters-once}

* **`name`:** (Stringa) [nome dell’evento](#contexthub-utils-eventing) a cui si sta eseguendo il binding della funzione.
* **`handler`:** (Funzione) La funzione da associare all&#39;evento.
* **`selector`:** (Stringa) Un identificatore univoco per il binding. Per utilizzare il binding, è necessario che il selettore identifichi il binding `off` per rimuovere il binding.
* **`triggerForPastEvents`:** (Booleano) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

##### Valore restituito {#returns-once}

Quando il `triggerForPastEvents` argomento `true`, questa funzione restituisce un `boolean` che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e verrà chiamato il gestore.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Classe di utilità che consente a un oggetto di ereditare le proprietà e i metodi di un altro oggetto.

### Funzioni (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Fa sì che un oggetto erediti le proprietà e i metodi di un altro oggetto.

##### Parametri {#parameters-inherit}

* **`child`:** (Oggetto) L&#39;oggetto che eredita.
* **`parent`:** (Oggetto) L&#39;oggetto che definisce le proprietà e i metodi ereditati.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornisce funzioni per serializzare gli oggetti in formato JSON e deserializzare le stringhe JSON negli oggetti.

### Funzioni (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analizza un valore stringa come JSON e lo converte in un oggetto javascript.

##### Parametri {#parameters-parse}

* **`data`:** Un valore stringa in formato JSON.

##### Valore restituito {#returns-parse}

Un oggetto Javascript.

##### Esempio {#example-parse}

Il codice:

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

Serializza i valori e gli oggetti Javascript in valori stringa in formato JSON.

##### Parametri {#parameters-stringify}

* **`data`:** Il valore o l&#39;oggetto da serializzare. Questa funzione supporta valori booleani, array, numero, stringa e data.

##### Valore restituito {#returns-stringify}

Il valore della stringa serializzata. Quando `data` è una R `egExp` questa funzione restituisce un oggetto vuoto. Quando `data` è una funzione, restituisce `undefined`.

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

Questa classe facilita la manipolazione degli oggetti dati da memorizzare o recuperare dagli archivi ContextHub.

### Funzioni (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia di un oggetto dati e gli aggiunge la struttura dati da un secondo oggetto. La funzione restituisce la copia e non modifica nessuno degli oggetti originali. Quando le strutture ad albero dati dei due oggetti contengono chiavi identiche, il valore del secondo oggetto sovrascrive il valore del primo oggetto.

##### Parametri {#parameters-addallitems-1}

* **`tree`:** L&#39;oggetto copiato.
* **`secondTree`:** L&#39;oggetto unito alla copia del `tree` oggetto.

##### Valore restituito {#returns-addallitems-1}

Oggetto contenente i dati uniti.

#### cleanup() {#cleanup}

Crea una copia di un oggetto, trova e rimuove gli elementi nella struttura dati che non contengono valori, valori nulli o valori non definiti e restituisce la copia.

##### Parametri {#parameters-cleanup}

* **`tree`:** L&#39;oggetto da pulire.

##### Valore restituito {#returns-cleanup}

Una copia dell&#39;albero che viene pulita.

#### getItem() {#getitem}

Recupera il valore da un oggetto per la chiave a.

##### Parametri {#parameters-getitem-2}

* **`tree`:** L&#39;oggetto dati.
* **`key`:** Chiave del valore da recuperare.

##### Valore restituito {#returns-getitem-2}

Il valore che corrisponde alla chiave. Quando la chiave dispone di chiavi secondarie, questa funzione restituisce un oggetto complesso. Quando il tipo del valore per la chiave è `undefined`, `null` viene restituito .

##### Esempio {#example-getitem-2}

Considera il seguente oggetto Javascript:

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

Il codice di esempio seguente recupera il valore di una chiave con chiavi figlio:

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

Recupera tutte le chiavi dalla struttura dati di un oggetto. Facoltativamente, puoi recuperare solo le chiavi degli elementi secondari di una chiave specifica. Facoltativamente, puoi anche specificare un ordinamento delle chiavi recuperate.

##### Parametri {#parameters-getkeys-2}

* **`tree`:** L&#39;oggetto da cui recuperare le chiavi della struttura dati.
* **`parent`:** (Facoltativo) Chiave di un elemento nella struttura dati per la quale si desidera recuperare le chiavi degli elementi secondari.
* **`order`:** (Facoltativo) Funzione che determina l&#39;ordinamento delle chiavi restituite. (Vedi [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) su Mozilla Developer Network.)

##### Valore restituito {#returns-getkeys-2}

Un array di chiavi.

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

La `ContextHub.Utils.JSON.tree.getKeys(myObject);` lo script restituisce la seguente matrice:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia di un oggetto specificato, rimuove il ramo specificato dalla struttura dati e restituisce la copia modificata.

##### Parametri {#parameters-removeitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** Chiave da rimuovere.

##### Valore restituito {#returns-removeitem-2}

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

Lo script di esempio seguente rimuove il ramo /uno/due/tre/quattro dalla struttura dati:

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

#### cleanizeKey(key) {#sanitizekey-key}

Rimuove i valori stringa per renderli utilizzabili come chiavi. Per bonificare una stringa, questa funzione esegue le azioni seguenti:

* Riduce più barre consecutive a una singola barra.
* Rimuove gli spazi bianchi dall’inizio e dalla fine della stringa.
* Divide il risultato in una matrice di stringhe delimitate da barre.

Utilizzare la matrice risultante per creare una chiave utilizzabile.

##### Parametri {#parameters-sanitizekey}

* **`key`:** La `string` di bonificare.

##### Valore restituito {#returns-sanitizekey}

Matrice di `string` valori in cui ogni stringa è la parte del `key` che è stato delimitato da slash. rappresenta la chiave sanizzata. Se la matrice bonificata ha una lunghezza pari a zero, questa funzione restituisce `null`.

##### Esempio {#example-sanitizekey}

Il codice seguente bonifica una stringa per produrre l&#39;array `["this", "is", "a", "path"]`, quindi genera la chiave `"/this/is/a/path"` dalla matrice:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Aggiunge una coppia chiave/valore alla struttura dati di una copia di un oggetto. Per informazioni sulle strutture ad albero dei dati, vedi [Persistenza.](contexthub.md#persistence)

##### Parametri {#parameters-setitem-2}

* **`tree`:** Un oggetto dati.
* **`key`:** Chiave da associare al valore aggiunto. La chiave è il percorso dell’elemento nella struttura dati. Questa funzione chiama `ContextHub.Utils.JSON.tree.sanitize` per igienizzare la chiave prima di aggiungerla.
* **`value`:** Valore da aggiungere alla struttura dati.

##### Valore restituito {#returns-setitem-2}

Una copia del `tree` che include `key`/ `value` coppia.

##### Esempio {#example-setitem-2}

Prendi in considerazione il seguente codice JavaScript:

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

Consente di registrare i candidati allo store e ottenere i candidati allo store registrati.

### Funzioni (ContextHub.Utils.storeCandidate) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidate(storeType) {#getregisteredcandidates-storetype}

Restituisce i tipi di archivio registrati come candidati allo store. Recuperare i candidati registrati di un tipo di negozio specifico o di tutti i tipi di negozio.

##### Parametri {#parameters-getregisteredcandidates}

* **`storeType`:** (Stringa) Il nome del tipo di archivio. Consulta la sezione `storeType` del [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione .

##### Valore restituito {#returns-getregisteredcandidates}

Un oggetto di tipi di archivio. Le proprietà dell&#39;oggetto sono i nomi dei tipi di archivio e i valori delle proprietà sono una matrice di candidati store registrati.

#### getStoreFromCandidate(storeType) {#getstorefromcandidates-storetype}

Restituisce un tipo di archivio dai candidati registrati. Se sono registrati più di un tipo di archivio con lo stesso nome, la funzione restituisce il tipo di archivio con la priorità più elevata.

##### Parametri {#parameters-getstorefromcandidates}

* `storeType`: (Stringa) Il nome del candidato dello store. Consulta la sezione `storeType` del [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) funzione .

##### Valore restituito {#returns-getstorefromcandidates}

Oggetto che rappresenta il candidato all&#39;archiviazione registrato. Se il tipo di archivio richiesto non è registrato, viene generato un errore.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Restituisce i nomi dei tipi di archivio registrati come candidati allo store. Questa funzione non richiede parametri.

##### Valore restituito {#returns-getsupportedstoretypes}

Matrice di valori stringa, in cui ogni stringa è il tipo di archivio con cui è stato registrato un candidato all&#39;archiviazione. Consulta la sezione `storeType` del [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) funzione .

#### registerStoreCandidate(store, storeType, priority, applica) {#registerstorecandidate-store-storetype-priority-applies}

Registra un oggetto store come candidato all&#39;archiviazione utilizzando un nome e una priorità.

La priorità è un numero che indica l’importanza degli archivi con lo stesso nome. Quando un candidato del negozio viene registrato con lo stesso nome di un candidato del negozio già registrato, viene utilizzato il candidato con la priorità più alta. Quando si registra un candidato al negozio, il negozio viene registrato solo se la priorità è superiore ai candidati registrati dello stesso nome.

##### Parametri {#parameters-registerstorecandidate}

* **`store`:** (Oggetto) L&#39;oggetto store da registrare come candidato store.
* **`storeType`:** (Stringa) Il nome del candidato dello store. Questo valore è necessario quando si crea un&#39;istanza del candidato store.
* **`priority`:** (Numero) La priorità del candidato del negozio.
* **`applies`:** (Funzione) La funzione da richiamare che valuta l&#39;applicabilità dell&#39;archivio nell&#39;ambiente corrente. La funzione deve restituire `true` se il deposito è applicabile, e `false` altrimenti. Il valore predefinito è una funzione che restituisce true: `function() {return true;}`

##### Esempio {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
