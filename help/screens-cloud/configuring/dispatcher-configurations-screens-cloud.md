---
title: Configurazioni Dispatcher in Screens as a Cloud Service
description: Questa pagina descrive le configurazioni di Dispatcher in Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configurazioni Dispatcher in Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

Questa sezione descrive le configurazioni del dispatcher per Screens as a Cloud Service.

## Aggiunta di filtri e regole di cache in Dispatcher per l’implementazione as a Cloud Service di Screens {#deployment}

Consenti i seguenti filtri e regole di cache nei dispatcher per le istanze Publish in Screens as a Cloud Service.

### Filtri AEM Screens {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Regole cache {#cache-rules}

* Aggiungi `/statfileslevel "10"` alla sezione `/cache` in `publish_farm.any`/.

  >[!NOTE]
  >Questa regola di cache supporta il caching fino a 10 livelli dalla directory principale dei documenti della cache e invalida quando il contenuto viene pubblicato, anziché invalidare tutto. Puoi modificare questo livello in base alla profondità con cui è impostata la struttura del contenuto.

* Aggiungere quanto segue alla sezione `/invalidate` in `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* Aggiungere le regole seguenti alla sezione `/rules` in `/cache` in publish_farm.any o in un file incluso in `publish_farm.any`.

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
