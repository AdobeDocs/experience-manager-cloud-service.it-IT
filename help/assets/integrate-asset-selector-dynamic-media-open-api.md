---
title: Integrare Asset Selector (Selettore risorse) con Dynamic Media open API
description: Integra il selettore delle risorse con varie applicazioni Adobe, non Adobe e di terze parti.
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: f171bbeaf01e2d9be3a8f3b5172919a5e8ca7d97
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 8%

---

# Integrazione per Dynamic Media con funzionalità OpenAPI {#integrate-asset-selector-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Asset Selector (Selettore risorse) consente di integrare utilizzando diverse applicazioni Adobe per consentire loro di lavorare insieme senza problemi.


## Prerequisiti {#prereqs-polaris}

Se integri Asset Selector con Dynamic Media con le funzionalità OpenAPI, utilizza i seguenti prerequisiti:

* [Metodi di comunicazione](/help/assets/overview-asset-selector.md#prereqs)
* Per accedere a Dynamic Media con funzionalità OpenAPI, è necessario disporre di licenze per:
   * Archivio Assets (ad esempio, Experience Manager Assets as a Cloud Service).
   * Dynamic Media di AEM.
* Solo [le risorse approvate](/help/assets/approve-assets.md) sono disponibili per l&#39;utilizzo per garantire la coerenza del brand.

## Integrazione per Dynamic Media con funzionalità OpenAPI {#adobe-app-integration-polaris}

L’integrazione di Asset Selector con il processo Dynamic Media OpenAPI prevede diversi passaggi, tra cui la creazione di un URL Dynamic Media personalizzato, la scelta dell’URL Dynamic Media e così via.

### Integrare il Selettore risorse per Dynamic Media con funzionalità OpenAPI {#integrate-dynamic-media}

Le proprietà `rootPath` e `path` non devono far parte di Dynamic Media con funzionalità OpenAPI. È invece possibile configurare la proprietà `aemTierType`. Di seguito è riportata la sintassi della configurazione:

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
| Directory principale API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| formato | `.jpg` |

#### Specifiche API di consegna risorse approvate {#approved-assets-delivery-api-specification}

Formato URL:
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

Dove:

* Host: `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La radice API è `"/adobe/assets"`
* `<asset-id>` è l&#39;identificatore della risorsa
* `as` è la parte costante della specifica API aperta che indica quale risorsa deve essere definita
* `<seo-name>` è il nome di una risorsa
* `<format>` è il formato di output
* `<image modification query parameters>` come supportato dalla specifica API di consegna delle risorse approvate

#### API di consegna rappresentazione originale delle risorse approvate {#approved-assets-delivery-api}

L’URL di consegna dinamico ha la seguente sintassi:
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`, dove

* Host: `https://delivery-pxxxxx-exxxxxx.adobe.com`
* La radice API per la consegna della rappresentazione originale è `"/adobe/assets"`
* `<asset-id>` è l&#39;identificatore della risorsa
* `/original/as` è la parte costante della specifica API aperta che indica quale rappresentazione originale deve essere definita
* `<seo-name>` è il nome della risorsa che potrebbe avere o meno un&#39;estensione

### Pronto per scegliere l’URL di consegna dinamico {#ready-to-pick-dynamic-delivery-url}

Tutte le risorse selezionate sono gestite dalla funzione `handleSelection` che agisce come oggetto JSON. Ad esempio, `JsonObj`. L’URL di consegna dinamico viene creato combinando i gestori seguenti:

| Oggetto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Directory principale API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

Di seguito sono riportati i due modi per attraversare l’oggetto JSON:

![URL di consegna dinamico](assets/dynamic-delivery-url.png)

* **Miniatura:** le miniature possono essere immagini e le risorse sono PDF, video, immagini e così via. Tuttavia, puoi utilizzare gli attributi di altezza e larghezza della miniatura di una risorsa come rappresentazione dinamica della consegna.
Per le risorse di tipo PDF può essere utilizzato il seguente set di rappresentazioni:
Una volta selezionato un PDF nella barra laterale, il contesto di selezione offre le informazioni seguenti. Di seguito è riportato il modo per scorrere l’oggetto JSON:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  È possibile fare riferimento a `selection[0].....selection[4]` per l&#39;array del collegamento della rappresentazione dalla schermata precedente. Ad esempio, le proprietà chiave di una delle rappresentazioni delle miniature includono:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

Nella schermata precedente, se è necessario PDF e non la sua miniatura, l’URL di consegna del rendering originale di PDF deve essere incorporato nell’esperienza di destinazione. Ad esempio `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **Video:** Puoi utilizzare l&#39;URL del lettore video per le risorse dei tipi di video che utilizzano un iFrame incorporato. Nell’esperienza di destinazione puoi utilizzare le seguenti rappresentazioni di array:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/DragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  È possibile fare riferimento a `selection[0].....selection[4]` per l&#39;array del collegamento della rappresentazione dalla schermata precedente. Ad esempio, le proprietà chiave di una delle rappresentazioni delle miniature includono:

  Lo snippet di codice nella schermata precedente è un esempio di risorsa video. Include l’array di collegamenti per le rappresentazioni. `selection[5]` nell&#39;estratto è l&#39;esempio della miniatura dell&#39;immagine che può essere utilizzata come segnaposto della miniatura video nell&#39;esperienza di destinazione. `selection[5]` nell&#39;array delle rappresentazioni è per il lettore video. Serve un HTML e può essere impostato come `src` dell&#39;iframe. Supporta lo streaming con bitrate adattivo, ovvero la distribuzione del video ottimizzata per il web.

  Nell&#39;esempio precedente, l&#39;URL del lettore video è `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

### Configurare filtri personalizzati {#configure-custom-filters-dynamic-media-open-api}

Il selettore risorse per Dynamic Media con funzionalità OpenAPI consente di configurare proprietà personalizzate e i filtri basati su di esse. La proprietà `filterSchema` viene utilizzata per configurare tali proprietà. La personalizzazione può essere esposta come `metadata.<metadata bucket>.<property name>.` in base al quale è possibile configurare i filtri, dove

* `metadata` sono le informazioni di una risorsa
* `embedded` è il parametro statico utilizzato per la configurazione e
* `<propertyname>` è il nome del filtro che si sta configurando

Per la configurazione, le proprietà definite al livello `jcr:content/metadata/` sono esposte come `metadata.<metadata bucket>.<property name>.` per i filtri che si desidera configurare.

Ad esempio, in Asset Selector for Dynamic Media con funzionalità OpenAPI, una proprietà su `asset jcr:content/metadata/client_name:market` viene convertita in `metadata.embedded.client_name:market` per la configurazione del filtro.

Per ottenere il nome, è necessario eseguire un’attività una tantum. Effettua una chiamata API di ricerca per la risorsa e ottieni il nome della proprietà (essenzialmente il bucket).

### Interfaccia utente di Asset Selector per Dynamic Media con funzionalità OpenAPI {#interface-dynamic-media-open-api}

Dopo l’integrazione con il selettore delle risorse micro-front-end di Adobe, nell’archivio delle risorse di Experience Manager puoi visualizzare solo la struttura delle risorse approvate.

![Interfaccia utente di Dynamic Media con funzionalità OpenAPI](assets/polaris-ui.png)

* **A**: Nascondi/Mostra pannello
* **B**: Assets
* **C**: ordinamento
* **D**: Filtri
* **E**: Barra di ricerca
* **F**: ordinamento crescente o decrescente
* **G**: Annulla selezione
* **H**: selezionare una o più risorse

>[!NOTE]
>
>Le cartelle sono supportate solo quando ci si connette all’archivio di authoring e non Dynamic Media con l’archivio OpenAPI.

>[!MORELIKETHIS]
>
>* [Integrare il Selettore risorse con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Personalizzazioni del Selettore risorse](/help/assets/asset-selector-customization.md)
