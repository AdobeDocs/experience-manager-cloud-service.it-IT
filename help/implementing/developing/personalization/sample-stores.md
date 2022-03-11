---
title: Candidati allo store ContextHub di esempio
description: ContextHub fornisce diversi esempi di candidati all'archivio che puoi utilizzare nelle soluzioni
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Candidati allo store ContextHub di esempio {#sample-contexthub-store-candidates}

ContextHub fornisce diversi esempi di candidati all&#39;archivio che puoi utilizzare nelle tue soluzioni. Per ciascun campione sono fornite le seguenti informazioni:

* Dove trovare il codice sorgente in modo da poterlo aprire a scopo di apprendimento.
* Come configurare gli archivi creati dai candidati allo store.
* Struttura dei dati dell’archivio in modo da potervi accedere.

>[!WARNING]
>
>I candidati all’archivio di esempio vengono forniti come configurazioni di riferimento per facilitare la creazione di una configurazione dedicata per il progetto e non devono quindi essere utilizzati direttamente.

## aem.segmentation Sample Store Candidato {#aem-segmentation-sample-store-candidate}

Memorizzazione di segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager.

### Posizione origine {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementazione di base {#base-implementation-segmentation}

Il candidato all&#39;archivio aem.segmentation si estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-segmentation}

Quando crei un `aem.segmentation` non è necessario fornire una configurazione dettagliata. La configurazione predefinita specifica la posizione delle definizioni dei segmenti ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Candidato all&#39;archivio di esempio {#contexthub-geolocation-sample-store-candidate}

La `contexthub.geolocation` sample store candidate utilizza Google Maps per ottenere e memorizzare informazioni sulla posizione del client.

### Posizione origine {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementazione di base {#base-implementation-geolocation}

La `contexthub.geolocation` estensione del candidato al negozio [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-geolocation}

La configurazione predefinita specifica le informazioni sul servizio Google e le coordinate di latitudine e longitudine iniziali.

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Elementi dati {#data-items-geolocation}

L&#39;archivio utilizza una struttura dati simile all&#39;esempio seguente:

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Una policy di sicurezza introdotta in Chrome 50.x richiede che tutte le chiamate relative alla geolocalizzazione siano effettuate su una connessione protetta. Pertanto, AEM forza l’utilizzo https per le chiamate API di geolocalizzazione se anche AEM è in esecuzione su https. In caso contrario, http viene utilizzato per rispettare i criteri della stessa origine.
>
>Vedi [questo post del blog Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) per ulteriori dettagli sulla modifica in Chrome.

## contexthub.surferinfo Candidato all&#39;archivio di esempio {#contexthub-surferinfo-sample-store-candidate}

Memorizza informazioni sull&#39;ambiente client corrente, ad esempio il dispositivo, la finestra, il browser, la data e l&#39;ora.

### Posizione origine {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementazione di base {#base-implementation-surferinfo}

La `contexthub.surferinfo` estensione del candidato al negozio [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-surferinfo}

La configurazione predefinita viene ereditata da `ContextHub.Store.PersistedStore`.

### Elementi dati {#data-items-surferinfo}

I negozi che utilizzano questo candidato all&#39;archivio hanno una struttura dati simile all&#39;esempio seguente:

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators Candidato all&#39;archivio di esempio {#granite-emulators-sample-store-candidate}

La `granite.emulators` sample store candidate memorizza informazioni sui dispositivi client.

### Posizione origine {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementazione di base {#base-implementation-emulators}

La `granite.emulators` estensione del candidato al negozio [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-emulators}

La configurazione predefinita include un array denominato `defaultEmulators` che contiene informazioni su dispositivi diversi. Quando crei un archivio, fornisci profili dispositivo diversi nella proprietà Configurazione dettagli come necessario, utilizzando il formato illustrato nell&#39;esempio seguente:

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Elementi dati {#data-items-emulators}

La struttura ad albero dei dati dell&#39;archivio è simile all&#39;esempio seguente:

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Sample Store Candidate {#granite-profile-sample-store-candidate}

Memorizza informazioni sull&#39;utente corrente.

### Posizione origine {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementazione di base {#base-implementation-profile}

La `granite.profile` estensione del candidato al negozio [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-profile}

Viene utilizzata la seguente configurazione predefinita. Non devi modificare questa configurazione.

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Elementi dati {#data-items-profile}

I negozi che utilizzano questo candidato all&#39;archivio hanno una struttura dati simile all&#39;esempio seguente:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
