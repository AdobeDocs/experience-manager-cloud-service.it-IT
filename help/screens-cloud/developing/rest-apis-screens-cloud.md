---
title: API REST
description: Screens as a Cloud Service fornisce una semplice API RESTful che segue le specifiche di Siren. Segui questa pagina per scoprire come navigare nella struttura del contenuto e inviare comandi ai dispositivi nell’ambiente.
exl-id: 2c52583f-0dd9-4fa3-880b-7671442989ae
feature: Developing Screens
role: Admin, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---

# API REST {#rest-apis}

AEM Screens fornisce una semplice API RESTful che segue la specifica [Siren](https://github.com/kevinswiber/siren). Consente di navigare nella struttura del contenuto e inviare comandi ai dispositivi nell’ambiente.

L&#39;API è accessibile da [*http://localhost:4502/api/screens.json*](http://localhost:4502/api/screens.json).

## Navigazione nella struttura del contenuto {#navigating-content-structure}

Il JSON restituito dalle chiamate API elenca le entità correlate alla risorsa corrente. Dopo il collegamento autonomo elencato, ciascuna di queste entità è nuovamente accessibile come risorsa REST.

Ad esempio, per accedere ai display nella nostra posizione di ammiraglia demo, puoi chiamare:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

Oppure utilizzando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

Il risultato sarà simile al seguente:

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

Per accedere alla visualizzazione a schermo singolo, è possibile chiamare:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## Esecuzione di azioni sulla risorsa {#executing-actions-on-the-resource}

Il JSON restituito dalle chiamate API può contenere un elenco di azioni disponibili nella risorsa.

La visualizzazione, ad esempio, elenca un&#39;azione *broadcast-command* che consente di inviare un comando a tutti i dispositivi assegnati alla visualizzazione.

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

Oppure utilizzando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***Risultato:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "title": "",
      "name": "broadcast-command",
      "method": "POST",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "fields": [
        {
          "name": ":operation",
          "value": "broadcast-command",
          "type": "hidden"
        },
        {
          "name": "msg",
          "type": "text"
        }
      ]
    }
  ]
}
```

Per attivare questa azione si richiama:

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&msg=reboot
```

Oppure utilizzando curl:

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&msg=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```
