---
title: Cerca API di Assets
description: Scopri come utilizzare l’API Search Assets.
role: User
source-git-commit: 3e2fe458460fe8ec4c1dd12152c1134bfb9ca62b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Cerca API di Assets {#search-assets-api}

Tutti [risorse approvate](approve-assets.md) disponibili nell’archivio Experience Manager assets, possono essere cercati e quindi consegnati alle applicazioni a valle integrate utilizzando un URL di consegna.

La ricerca delle risorse approvate corrette dall’archivio Experience Manager è il primo passo per consegnare le risorse utilizzando l’URL di consegna. La risposta alla richiesta di ricerca comprende un array di documenti JSON corrispondenti alle risorse che soddisfano i criteri di ricerca. Ogni documento JSON viene identificato utilizzando un `id` , utilizzato per comporre la richiesta di consegna della risorsa.

![Panoramica del protocollo di caricamento binario diretto](assets/search-assets-api-overview.png)

Puoi definire le proprietà all’interno della richiesta API Search Assets per abilitare le seguenti funzionalità:

* **Ricerca full-text**: utilizza `match` per definire il testo da cercare.  È inoltre possibile utilizzare gli operatori all&#39;interno di `match` per filtrare i risultati.

* **Applicare i filtri**: utilizza `term` per filtrare ulteriormente i risultati definendo un `key` e uno o più valori. `key` identifica il campo il cui valore deve corrispondere e `value` rappresenta l’oggetto del confronto. Allo stesso modo, è possibile utilizzare `range` query per definire un intervallo per un campo utilizzando le proprietà Greater than (gt), Greater than o equal-to (gte), Less-than (lt) e Less-than o equal-to (lte).

* **Ordinare i risultati**: utilizza `OrderBy` per ordinare i risultati della ricerca in base a uno o più campi. Puoi ordinare i risultati in ordine crescente o decrescente.

* **Paginazione**: utilizza `limit` e `cursor` per definire le proprietà di impaginazione all’interno di una richiesta API di ricerca. `limit` definisce il numero massimo di elementi da recuperare in una risposta API. `cursor` facilita il recupero del punto di partenza per il successivo set di risorse definito nel `limit` proprietà. Ad esempio, se definisci `50` come limite nella richiesta API, puoi utilizzare il `cursor` per avviare e recuperare i successivi 50 elementi utilizzando la successiva richiesta API.

## Endpoint API per la ricerca di risorse {#search-assets-api-endpoint}

L’endpoint in una richiesta API di Search assets deve essere nel seguente formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

Il dominio di consegna è simile nella struttura al dominio dell’ambiente di authoring Experience Manager. L&#39;unica differenza consiste nel sostituire il termine `author` con `delivery`.

`pXXXX` fa riferimento all’ID del programma

`eYYYY` fa riferimento all’ID ambiente

## Metodo di richiesta API per la ricerca di risorse {#search-assets-api-request-method}

POST

## Cerca nell’intestazione API di Assets {#search-assets-api-header}

Durante la definizione di un’intestazione nell’API Search Assets devi fornire i seguenti dettagli:

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

Per richiamare l’API di ricerca, è necessario un token IMS per definire nella `Authorization` dettagli. Il token IMS viene recuperato da un account tecnico. Consulta [Recupera le credenziali di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) per creare un nuovo account tecnico. Consulta [Generazione del token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) per generare il token IMS e utilizzarlo in modo appropriato nell’intestazione della richiesta API Search Assets.

Per visualizzare campioni di richieste, campioni di risposta e codici di risposta, vedere [Cerca API di Assets](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).
