---
title: Configurazioni del Dispatcher in Screens come Cloud Service
description: Questa pagina descrive come un Cloud Service le configurazioni del Dispatcher in Screens.
source-git-commit: b00856e1be8842c4e9fa6ed4ada9129926c73ef5
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Configurazioni del Dispatcher in Screens come Cloud Service{#dispatcher-configurations-screens-cloud}

Questa sezione descrive le configurazioni del dispatcher per Screens come Cloud Service.

## Configurazioni del Dispatcher per Screens come implementazione di Cloud Service {#deployment}

Consenti i seguenti filtri e regole di cache nei dispatcher per le istanze di pubblicazione in Screens come Cloud Service.

### Filtri {#filters}

## Filtri AEM Screens

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

## Regole di cache {#cache-rules}

* Aggiungi `/statfileslevel "10"` alla sezione `/cache` in `publish_farm.any`/.

   >[!NOTE]
   >Questo supporta il caching fino a 10 livelli dal docroot della cache e invalida quando il contenuto viene pubblicato anziché invalidare tutto. Puoi modificare questo livello in base alla profondità della struttura del contenuto.

* Aggiungi quanto segue alla sezione `/invalidate` in `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Aggiungi le seguenti regole alla sezione `/rules` in `/cache` in publish_farm.any o in un file incluso in `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
            }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
