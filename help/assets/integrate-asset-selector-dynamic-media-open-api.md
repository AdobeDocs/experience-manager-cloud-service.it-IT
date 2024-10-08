---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Integra il selettore delle risorse con varie applicazioni di Adobe, non di Adobe e di terze parti.
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 4%

---

# Integrazione per Dynamic Medie con funzionalità OpenAPI {#integrate-asset-selector-dynamic-media-open-apis}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Asset Selector consente di eseguire l’integrazione utilizzando diverse applicazioni di Adobe per consentire loro di lavorare insieme senza problemi.


## Prerequisiti {#prereqs-polaris}

Se integri Asset Selector con Dynamic Medie con le funzionalità OpenAPI, utilizza i seguenti prerequisiti:

* [Metodi di comunicazione](/help/assets/overview-asset-selector.md#prereqs)
* Per accedere a Dynamic Medie con funzionalità OpenAPI, è necessario disporre di licenze per:
   * Archivio Assets (ad esempio, Experience Manager Assets as a Cloud Service).
   * AEM-Dynamic Medie
* Solo [le risorse approvate](/help/assets/approve-assets.md) sono disponibili per l&#39;utilizzo per garantire la coerenza del brand.

## Integrazione per Dynamic Medie con funzionalità OpenAPI {#adobe-app-integration-polaris}

L’integrazione del selettore delle risorse con il processo OpenAPI di Dynamic Medie prevede diversi passaggi, tra cui la creazione di un URL Dynamic Media personalizzato o pronto per scegliere l’URL Dynamic Media, ecc.

### Integrare il Selettore risorse per Dynamic Media con funzionalità OpenAPI {#integrate-dynamic-media}

Le proprietà `rootPath` e `path` non devono far parte di Dynamic Medie con funzionalità OpenAPI. È invece possibile configurare la proprietà `aemTierType`. Di seguito è riportata la sintassi della configurazione:

```
aemTierType:[1: "delivery"]
```

Questa configurazione ti consente di visualizzare tutte le risorse approvate senza cartelle o come struttura semplice. Per ulteriori informazioni, passa alla proprietà `aemTierType` in [Proprietà selettore risorse](/help/assets/asset-selector-properties.md).


### Creare un URL di consegna dinamico da risorse approvate {#create-dynamic-media-url}

Una volta configurato il Selettore risorse, viene utilizzato uno schema di oggetti per creare un URL di consegna dinamico dalle risorse selezionate.
Ad esempio, uno schema di un oggetto da un array di oggetti che viene ricevuto al momento della selezione di una risorsa:

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

Tutte le risorse selezionate sono gestite dalla funzione `handleSelection` che agisce come oggetto JSON. Ad esempio, `JsonObj`. L’URL di consegna dinamico viene creato combinando i gestori seguenti:

| Oggetto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Directory principale API | `/adobe/dynamicmedia/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| formato | `.jpg` |

#### Specifiche API di consegna risorse approvate {#approved-assets-delivery-api-specification}

Formato URL:
`https://<delivery-api-host>/adobe/dynamicmedia/deliver/<asset-id>/<seo-name>.<format>?<image-modification-query-parameters>`

Dove:

* Host: `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La radice API è `"/adobe/dynamicmedia/deliver"`
* `<asset-id>` è l&#39;identificatore della risorsa
* `<seo-name>` è il nome di una risorsa
* `<format>` è il formato di output
* `<image modification query parameters>` come supporto dalla specifica API di consegna delle risorse approvate

#### API di consegna risorse approvate {#approved-assets-delivery-api}

L’URL di consegna dinamico ha la seguente sintassi:
`https://<delivery-api-host>/adobe/assets/deliver/<asset-id>/<seo-name>`, dove

* Host: `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La radice API per la consegna della rappresentazione originale è `"/adobe/assets/deliver"`
* `<asset-id>` è l&#39;identificatore della risorsa
* `<seo-name>` è il nome della risorsa che potrebbe avere o meno un&#39;estensione

### Pronto per scegliere l’URL di consegna dinamico {#ready-to-pick-dynamic-delivery-url}

Tutte le risorse selezionate sono gestite dalla funzione `handleSelection` che agisce come oggetto JSON. Ad esempio, `JsonObj`. L’URL di consegna dinamico viene creato combinando i gestori seguenti:

| Oggetto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Directory principale API | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

Di seguito sono riportati i due modi per attraversare l’oggetto JSON:

![URL di consegna dinamico](assets/dynamic-delivery-url.png)

* **Miniatura:** le miniature possono essere immagini e le risorse sono PDF, video, immagini e così via. Tuttavia, puoi utilizzare gli attributi di altezza e larghezza della miniatura di una risorsa come rappresentazione dinamica della consegna.
Per le risorse di tipo PDF è possibile utilizzare il seguente set di rappresentazioni:
Una volta selezionato un PDF nella barra laterale, il contesto di selezione offre le informazioni seguenti. Di seguito è riportato il modo per scorrere l’oggetto JSON:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  È possibile fare riferimento a `selection[0].....selection[4]` per l&#39;array del collegamento della rappresentazione dalla schermata precedente. Ad esempio, le proprietà chiave di una delle rappresentazioni delle miniature includono:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

Nella schermata precedente, se è necessario PDF, l’URL di consegna del rendering originale del PDF deve essere incorporato nell’esperienza di destinazione e non nella relativa miniatura. Ad esempio `https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf?accept-experimental=1`

* **Video:** Puoi utilizzare l&#39;URL del lettore video per le risorse dei tipi di video che utilizzano un iFrame incorporato. Nell’esperienza di destinazione puoi utilizzare le seguenti rappresentazioni di array:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

  È possibile fare riferimento a `selection[0].....selection[4]` per l&#39;array del collegamento della rappresentazione dalla schermata precedente. Ad esempio, le proprietà chiave di una delle rappresentazioni delle miniature includono:

  Lo snippet di codice nella schermata precedente è un esempio di risorsa video. Include l’array di collegamenti per le rappresentazioni. `selection[5]` nell&#39;estratto è l&#39;esempio della miniatura dell&#39;immagine che può essere utilizzata come segnaposto della miniatura video nell&#39;esperienza di destinazione. `selection[5]` nell&#39;array delle rappresentazioni è per il lettore video. Serve un HTML e può essere impostato come `src` dell&#39;iframe. Supporta lo streaming con bitrate adattivo, ovvero la distribuzione del video ottimizzata per il web.

  Nell&#39;esempio precedente, l&#39;URL del lettore video è `https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play?accept-experimental=1`

### Configurare filtri personalizzati {#configure-custom-filters-dynamic-media-open-api}

Il selettore risorse per Dynamic Medie con funzionalità OpenAPI consente di configurare proprietà personalizzate e i filtri basati su di esse. La proprietà `filterSchema` viene utilizzata per configurare tali proprietà. La personalizzazione può essere esposta come `metadata.<metadata bucket>.<property name>.` in base al quale è possibile configurare i filtri, dove

* `metadata` sono le informazioni di una risorsa
* `embedded` è il parametro statico utilizzato per la configurazione e
* `<propertyname>` è il nome del filtro che si sta configurando

Per la configurazione, le proprietà definite al livello `jcr:content/metadata/` sono esposte come `metadata.<metadata bucket>.<property name>.` per i filtri che si desidera configurare.

Ad esempio, in Asset Selector for Dynamic Medie con funzionalità OpenAPI, una proprietà su `asset jcr:content/metadata/client_name:market` viene convertita in `metadata.embedded.client_name:market` per la configurazione del filtro.

Per ottenere il nome, è necessario eseguire un’attività una tantum. Effettua una chiamata API di ricerca per la risorsa e ottieni il nome della proprietà (essenzialmente il bucket).

### Interfaccia utente di Asset Selector per Dynamic Medie con funzionalità OpenAPI {#interface-dynamic-media-open-api}

Dopo l’integrazione con il selettore delle risorse micro-front-end di Adobe, nell’archivio Experience Manager Assets puoi visualizzare solo la struttura delle risorse approvate.

![Dynamic Medie con funzionalità OpenAPI, interfaccia utente](assets/polaris-ui.png)

* **A**: [Nascondi/Mostra pannello](#hide-show-panel)
* **B**: [Assets](#repository)
* **C**: [Ordinamento](#sorting)
* **D**: [Filtri](#filters)
* **E**: [Barra di ricerca](#search-bar)
* **F**: [Ordinamento crescente o decrescente](#sorting)
* **G**: Annulla selezione
* **H**: selezionare una o più risorse

>[!MORELIKETHIS]
>
>* [Integrare Asset Selector con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà selettore risorse](/help/assets/asset-selector-properties.md)
>* [Personalizzazioni di Asset Selector](/help/assets/asset-selector-customization.md)
