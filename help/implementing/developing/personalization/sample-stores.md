---
title: Candidati per l'archivio ContextHub di esempio
description: ContextHub offre diversi store candidati di esempio che potete utilizzare nelle vostre soluzioni
translation-type: tm+mt
source-git-commit: c3f69e4b03819fea9a1842a87cad38bd1e485d83
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Candidati per l&#39;archivio ContextHub di esempio {#sample-contexthub-store-candidates}

ContextHub offre diversi esempi di candidati store che potete utilizzare nelle soluzioni. Per ciascun campione vengono fornite le seguenti informazioni:

* Dove trovare il codice sorgente per aprirlo a scopo di apprendimento.
* Come configurare gli store creati dai candidati allo store.
* Struttura dei dati dello store in modo da potervi accedere.

>[!WARNING]
>
>I candidati allo store di esempio vengono forniti come configurazioni di riferimento per facilitare la creazione di una propria configurazione dedicata per il progetto e pertanto non devono essere utilizzati direttamente.

## aem.segmentation Sample Store Candidate {#aem-segmentation-sample-store-candidate}

Memorizzazione per segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager.

### Posizione origine {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementazione di base {#base-implementation-segmentation}

Il candidato per l&#39;archivio di segmentazione aem.segmentation si estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-segmentation}

Quando create uno `aem.segmentation` store, non è necessario fornire una configurazione dettagliata. La configurazione predefinita specifica la posizione delle definizioni del segmento ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Esempio di candidatura per store {#contexthub-geolocation-sample-store-candidate}

Il candidato all&#39; `contexthub.geolocation` archivio di esempio utilizza Google Maps per ottenere e archiviare informazioni sulla posizione del client.

### Posizione origine {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementazione di base {#base-implementation-geolocation}

Il `contexthub.geolocation` candidato del negozio si estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-geolocation}

La configurazione predefinita specifica informazioni sul servizio Google e sulle coordinate di latitudine e longitudine iniziali.

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
>Una politica di sicurezza introdotta in Chrome 50.x richiede che tutte le chiamate relative alla geolocalizzazione siano effettuate su una connessione protetta. Pertanto, AEM forza l&#39;utilizzo https per le chiamate API di geolocalizzazione se AEM è in esecuzione anche su https. In caso contrario, http viene utilizzato per rispettare i criteri della stessa origine.
>
>Consultate [questo post](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) di Google blog per ulteriori dettagli sulla modifica in Chrome.

## contexthub.surferinfo Esempio di candidato per store {#contexthub-surferinfo-sample-store-candidate}

Memorizza informazioni sull&#39;ambiente client corrente, ad esempio il dispositivo, la finestra, il browser, la data e l&#39;ora.

### Posizione origine {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementazione di base {#base-implementation-surferinfo}

Il `contexthub.surferinfo` candidato del negozio si estende [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-surferinfo}

La configurazione predefinita viene ereditata da `ContextHub.Store.PersistedStore`.

### Elementi dati {#data-items-surferinfo}

I negozi che utilizzano il candidato all&#39;archiviazione dispongono di una struttura dati simile al seguente esempio:

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

## granite.emulators Esempio di candidatura per store {#granite-emulators-sample-store-candidate}

Il candidato all&#39; `granite.emulators` archivio di esempio memorizza le informazioni sui dispositivi client.

### Posizione origine {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementazione di base {#base-implementation-emulators}

Il `granite.emulators` candidato del negozio si estende [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-emulators}

La configurazione predefinita include un array denominato `defaultEmulators` che contiene informazioni sui diversi dispositivi. Quando create uno store, fornite profili dispositivo diversi nella proprietà Configurazione dettagli come necessario, utilizzando il formato illustrato nell&#39;esempio seguente:

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

Memorizza le informazioni sull&#39;utente corrente.

### Posizione origine {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementazione di base {#base-implementation-profile}

Il `granite.profile` candidato del negozio si estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-profile}

Viene utilizzata la seguente configurazione predefinita. Non modificare questa configurazione.

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

I negozi che utilizzano il candidato all&#39;archiviazione dispongono di una struttura dati simile al seguente esempio:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
