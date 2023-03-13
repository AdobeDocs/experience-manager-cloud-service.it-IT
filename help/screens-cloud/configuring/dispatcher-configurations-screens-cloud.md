---
title: Configurazioni del Dispatcher in Screens as a Cloud Service
description: Questa pagina descrive le configurazioni del Dispatcher in Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configurazioni del Dispatcher in Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

Questa sezione descrive le configurazioni del dispatcher per Screens as a Cloud Service.

## Aggiunta di filtri e regole di cache in Dispatcher per la distribuzione as a Cloud Service di Screens {#deployment}

Consenti i seguenti filtri e regole di cache nei dispatcher per le istanze Publish in Screens as a Cloud Service.

### Filtri AEM Screens {#filters}

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

### Regole cache {#cache-rules}

* Aggiungi `/statfileslevel "10"` a `/cache` sezione in `publish_farm.any`/.

   >[!NOTE]
   >Questa regola di cache supporta il caching fino a 10 livelli dalla directory principale dei documenti della cache e invalida quando il contenuto viene pubblicato, anziché invalidare tutto. Puoi modificare questo livello in base alla profondità con cui è impostata la struttura del contenuto.

* Aggiungi quanto segue a `/invalidate` sezione in `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Aggiungi le seguenti regole a `/rules` sezione in `/cache` in publish_farm.any o in un file incluso da `publish_farm.any`.

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
