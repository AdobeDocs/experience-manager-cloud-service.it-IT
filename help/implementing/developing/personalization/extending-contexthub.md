---
title: Estensione di ContextHub
description: Definire nuovi tipi di store e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# Estensione di ContextHub {#extending-contexthub}

Definite nuovi tipi di store e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione.

## Creazione di candidati store personalizzati {#creating-custom-store-candidates}

Gli store ContextHub vengono creati dai candidati store registrati. Per creare uno store personalizzato, dovete creare e registrare un candidato per lo store.

Il file javascript che include il codice che crea e registra il candidato store deve essere incluso in una [cartella libreria client](/help/implementing/developing/introduction/clientlibs.md). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.store.[storeType]
```

La parte `storeType` della categoria è la `storeType` con cui è registrato il candidato all&#39;acquisto. (Vedere [Registrazione di un candidato per lo store ContextHub](#registering-a-contexthub-store-candidate)). Ad esempio, per storeType di `contexthub.mystore`, la categoria della cartella della libreria client deve essere `contexthub.store.contexthub.mystore`.

### Creazione di un candidato per lo store ContextHub {#creating-a-contexthub-store-candidate}

Per creare un candidato all&#39;acquisto, utilizzate la funzione [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) per estendere uno dei punti vendita di base:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Tenere presente che ogni archivio di base estende lo store [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core).

Nell&#39;esempio seguente viene creata l&#39;estensione più semplice del candidato `ContextHub.Store.PersistedStore` allo store:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Realisticamente, i candidati all&#39;acquisto personalizzati definiranno funzioni aggiuntive o ignoreranno la configurazione iniziale dello store. Diversi candidati [store di esempio](sample-stores.md) sono installati nella directory archivio sotto `/libs/granite/contexthub/components/stores`.

### Registrazione di un candidato per lo store ContextHub {#registering-a-contexthub-store-candidate}

Registrate un candidato per lo store per integrarlo con il framework ContextHub e consentire la creazione di store da esso. Per registrare un candidato per uno store, utilizzare la funzione [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) della classe `ContextHub.Utils.storeCandidates`.

Quando registrate un candidato per uno store, fornite un nome per il tipo di store. Quando create uno store dal candidato, utilizzate il tipo di store per identificare il candidato su cui si basa.

Quando registrate un candidato per un negozio, ne indicate la priorità. Quando un candidato del negozio viene registrato con lo stesso tipo di negozio di un candidato già registrato, viene utilizzato il candidato con la priorità più alta. Pertanto, potete escludere i candidati esistenti per lo store con nuove implementazioni.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Nella maggior parte dei casi è necessario un solo candidato e la priorità può essere impostata su `0`, ma se siete interessati è possibile conoscere [registrazioni più avanzate,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) che consente di scegliere una delle poche implementazioni dello store in base alla condizione javascript (`applies`) e alla priorità del candidato.

## Creazione di tipi di moduli interfaccia utente ContextHub {#creating-contexthub-ui-module-types}

Crea tipi di moduli di interfaccia utente personalizzati quando quelli installati con ContextHub[ non soddisfano i requisiti dell&#39;utente. ](sample-modules.md) Per creare un tipo di modulo dell&#39;interfaccia utente, create un nuovo renderer di moduli dell&#39;interfaccia utente estendendo la classe `ContextHub.UI.BaseModuleRenderer` e quindi registrandola con `ContextHub.UI`.

Per creare un renderer di moduli dell&#39;interfaccia utente, create un oggetto `Class` contenente la logica che esegue il rendering del modulo dell&#39;interfaccia utente. Come minimo, la classe deve eseguire le azioni seguenti:

* Estende la classe `ContextHub.UI.BaseModuleRenderer`. Questa classe è l&#39;implementazione di base per tutti i renderer di moduli dell&#39;interfaccia utente. L&#39;oggetto `Class` definisce una proprietà denominata `extend` che viene utilizzata per denominare questa classe come quella che viene estesa.
* Fornire una configurazione predefinita. Creare una proprietà `defaultConfig`. Questa proprietà è un oggetto che include le proprietà definite per il modulo [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) dell&#39;interfaccia utente e tutte le altre proprietà richieste.

L&#39;origine per `ContextHub.UI.BaseModuleRenderer` si trova in `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Per registrare il renderer, utilizzate il metodo [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) della classe `ContextHub.UI`. È necessario specificare un nome per il tipo di modulo. Quando gli amministratori creano un modulo dell&#39;interfaccia utente basato su questo renderer, specificano questo nome.

Creare e registrare la classe del renderer in una funzione anonima che esegue automaticamente. L&#39;esempio seguente è basato sul codice sorgente per il modulo `contexthub.browserinfo` dell&#39;interfaccia utente. Questo modulo dell&#39;interfaccia utente è una semplice estensione della classe `ContextHub.UI.BaseModuleRenderer`.

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

Il file javascript che include il codice che crea e registra il renderer deve essere incluso in una [cartella libreria client](/help/implementing/developing/introduction/clientlibs.md). La categoria della cartella deve corrispondere al seguente pattern:

```javascript
contexthub.module.[moduleType]
```

La parte `[moduleType]` della categoria è la `moduleType` con cui è registrato il renderer del modulo. Ad esempio, per `moduleType` di `contexthub.browserinfo`, la categoria della cartella della libreria client deve essere `contexthub.module.contexthub.browserinfo`.
