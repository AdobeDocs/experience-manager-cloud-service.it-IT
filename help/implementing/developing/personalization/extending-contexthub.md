---
title: Estensione di ContextHub
description: Definire nuovi tipi di archivi e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Estensione di ContextHub {#extending-contexthub}

Definisci nuovi tipi di archivi e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione.

## Creazione di candidati store personalizzati {#creating-custom-store-candidates}

Gli archivi ContextHub vengono creati dai candidati store registrati. Per creare uno store personalizzato, è necessario creare e registrare un candidato allo store.

Il file javascript che include il codice che crea e registra il candidato store deve essere incluso in un [cartella libreria client](/help/implementing/developing/introduction/clientlibs.md). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.store.[storeType]
```

La `storeType` parte della categoria è `storeType` con cui è registrato il candidato del negozio. (Vedi [Registrazione di un candidato all’archivio ContextHub](#registering-a-contexthub-store-candidate)). Ad esempio, per storeType di `contexthub.mystore`, la categoria della cartella della libreria client deve essere `contexthub.store.contexthub.mystore`.

### Creazione di un candidato all’archivio ContextHub {#creating-a-contexthub-store-candidate}

Per creare un candidato allo store, utilizza la [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) funzione per estendere uno degli archivi di base:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Tieni presente che ogni archivio di base estende [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) archiviare.

Nell&#39;esempio seguente viene creata l&#39;estensione più semplice di `ContextHub.Store.PersistedStore` candidato al negozio:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

In modo realistico, i candidati all&#39;archivio personalizzati definiranno funzioni aggiuntive o ignoreranno la configurazione iniziale dell&#39;archivio. Diversi [candidati allo store di esempio](sample-stores.md) sono installati nell&#39;archivio sottostante `/libs/granite/contexthub/components/stores`.

### Registrazione di un candidato all’archivio ContextHub {#registering-a-contexthub-store-candidate}

Registra un candidato store per integrarlo con il framework ContextHub e abilita la creazione di archivi da esso. Per registrare un candidato di un negozio, utilizza la [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) funzione `ContextHub.Utils.storeCandidates` classe.

Quando si registra un candidato allo store, specificare un nome per il tipo di store. Quando si crea un negozio dal candidato, si utilizza il tipo di negozio per identificare il candidato su cui si basa.

Quando si registra un candidato al negozio, viene indicata la sua priorità. Quando un candidato viene registrato utilizzando lo stesso tipo di negozio di un candidato già registrato, viene utilizzato il candidato con la priorità più alta. Pertanto, puoi sostituire i candidati esistenti allo store con nuove implementazioni.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Nella maggior parte dei casi è necessario un solo candidato e la priorità può essere impostata su `0`, ma se siete interessati potete saperne di più [registrazioni più avanzate,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) che consente di scegliere una delle poche implementazioni store in base alla condizione javascript (`applies`) e priorità del candidato.

## Creazione di tipi di moduli di interfaccia utente ContextHub {#creating-contexthub-ui-module-types}

Crea tipi di moduli di interfaccia utente personalizzati quando quelli che sono [installato con ContextHub](sample-modules.md) non soddisfa le tue esigenze. Per creare un tipo di modulo dell’interfaccia utente, crea un nuovo modulo di rendering dell’interfaccia utente estendendo `ContextHub.UI.BaseModuleRenderer` e quindi registrarla con `ContextHub.UI`.

Per creare un modulo di rendering dell’interfaccia utente, crea un `Class` oggetto contenente la logica che esegue il rendering del modulo dell’interfaccia utente. Come minimo, la classe deve eseguire le azioni seguenti:

* Estendi la `ContextHub.UI.BaseModuleRenderer` classe. Questa classe è l’implementazione di base per tutti i moduli di rendering dell’interfaccia utente. La `Class` l&#39;oggetto definisce una proprietà denominata `extend` che si utilizza per denominare questa classe come quella in corso di estensione.
* Fornisci una configurazione predefinita. Crea un `defaultConfig` proprietà. Questa proprietà è un oggetto che include le proprietà definite per [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) Modulo dell’interfaccia utente e tutte le altre proprietà richieste.

L&#39;origine per `ContextHub.UI.BaseModuleRenderer` si trova in `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Per registrare il modulo di rendering, utilizza la [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) metodo `ContextHub.UI` classe. È necessario specificare un nome per il tipo di modulo. Quando gli amministratori creano un modulo di interfaccia utente basato su questo modulo di rendering, specificano questo nome.

Crea e registra la classe renderer in una funzione anonima con esecuzione automatica. L&#39;esempio seguente è basato sul codice sorgente per `contexthub.browserinfo` Modulo interfaccia utente . Questo modulo di interfaccia utente è una semplice estensione del `ContextHub.UI.BaseModuleRenderer` classe.

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

Il file javascript che include il codice che crea e registra il renderer deve essere incluso in un [cartella libreria client](/help/implementing/developing/introduction/clientlibs.md). La categoria della cartella deve corrispondere al seguente pattern:

```javascript
contexthub.module.[moduleType]
```

La `[moduleType]` parte della categoria è `moduleType` con cui viene registrato il modulo di rendering. Ad esempio, per `moduleType` di `contexthub.browserinfo`, la categoria della cartella della libreria client deve essere `contexthub.module.contexthub.browserinfo`.
