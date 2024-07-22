---
title: API di consegna
description: Scopri come utilizzare le API di consegna.
role: User
source-git-commit: deae260ce34a0801ee534ddadfb14823ef461a87
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# API di consegna {#delivery-apis}

Tutte le [risorse approvate](approve-assets.md) disponibili nell&#39;archivio Experience Manager Assets possono essere [cercate](search-assets-api.md) e quindi consegnate alle applicazioni downstream integrate utilizzando un URL di consegna.

Eventuali modifiche apportate alle risorse approvate in DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, vengono automaticamente riportate negli URL di consegna. Con un valore TTL (Time-to-Live) breve di 10 minuti configurato per la distribuzione delle risorse tramite CDN, gli aggiornamenti diventano visibili in meno di 10 minuti su tutte le interfacce di authoring e pubblicazione.

L’immagine seguente illustra gli URL di consegna disponibili:

![API di consegna](assets/delivery-url.png)

La tabella seguente illustra l’utilizzo delle varie API di consegna disponibili:

| API di consegna | Descrizione |
|---|---|
| [Rappresentazione binaria ottimizzata per il web della risorsa nel formato di output richiesto](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | Restituisce la rappresentazione binaria ottimizzata per il web della risorsa nel formato di output richiesto in base all’ID risorsa inviato nella richiesta. Inoltre, puoi definire vari modificatori di immagini, ad esempio larghezza, altezza, rotazione, capovolgimento, qualità, ritaglio, formato e [ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md). Consulta [Dettagli API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) per i formati e i modificatori di immagini supportati.<br>L&#39;Adobe consiglia di utilizzare questa API per tutti i tipi di formato immagine. |
| [Rappresentazione binaria ottimizzata per il web della risorsa](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | L’API di convenienza che applica i valori predefiniti alla rappresentazione binaria ottimizzata per il web della risorsa restituita nella risposta. I valori predefiniti includono un formato standard JPEG/WEBP, qualità => 65 e larghezza => 1024. |
| [File binario caricato originale della risorsa](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | Restituisce i file binari caricati originariamente per la risorsa. L’Adobe consiglia di utilizzare questa API per i tipi di formato di documento e le immagini SVG. |
| [Rendering pregenerato della risorsa disponibile nell&#39;ambiente di authoring AEM Assets](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | Restituisce il bitstream del rendering della risorsa disponibile nell’ambiente di authoring AEM Assets in base all’ID risorsa e al nome del rendering inviati nella richiesta. |
| [Metadati risorsa](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | Restituisce le proprietà associate a una risorsa, ad esempio titolo, descrizione, CreateDate, ModifyDate e così via. |
| [Contenitore lettore per la risorsa video](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | Restituisce il contenitore del lettore per la risorsa video. Puoi incorporare il lettore in un elemento iframe HTML e riprodurre il video. |
| [Manifesti di riproduzione nel formato di output selezionato](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | Restituisce il file del manifesto di riproduzione per la risorsa video specificata nel formato di output selezionato. Per poter estrarre il file del manifesto di riproduzione e riprodurre il video, è necessario creare un lettore personalizzato in grado di eseguire lo streaming adattivo tramite i protocolli HLS o DASH. |

## Endpoint API di consegna {#delivery-apis-endpoint}

Gli endpoint API variano per ogni API di consegna. Ad esempio, l&#39;endpoint API per l&#39;API `Web-optimized binary representation of the asset in the requested output format` è:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

Il dominio di consegna è simile nella struttura al dominio dell’ambiente di authoring Experience Manager. L&#39;unica differenza consiste nella sostituzione del termine `author` con `delivery`.

`pXXXX` fa riferimento all&#39;ID del programma

`eYYYY` fa riferimento all&#39;ID ambiente

Per ulteriori informazioni, vedere [Dettagli API](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets).

## Metodo di richiesta API di consegna {#delivery-api-request-method}

GET

## Intestazione API di consegna {#deliver-assets-api-header}

Durante la definizione di un’intestazione nell’intestazione delle API di consegna, devi fornire i seguenti dettagli:

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

Per richiamare le API di consegna, è necessario un token IMS nei dettagli `Authorization` per inviare una risorsa con restrizioni. Il token IMS viene recuperato da un account tecnico. Consulta [Recuperare le credenziali di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) per creare un nuovo account tecnico. Consulta [Generazione del token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) per generare il token IMS e utilizzarlo in modo appropriato nell&#39;intestazione della richiesta API di consegna.


Per visualizzare esempi di richieste, campioni di risposta e codici di risposta, vedi [API di consegna](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).