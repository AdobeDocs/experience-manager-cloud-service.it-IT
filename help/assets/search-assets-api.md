---
title: Cerca API di Assets
description: Scopri come utilizzare l’API Search Assets.
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: 8b596c6e82d9beaeb922cc6635717f151bb390e7
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Cerca API di Assets {#search-assets-api}

Tutte le [risorse approvate](approve-assets.md) disponibili nell&#39;archivio delle risorse di Experience Manager possono essere cercate e quindi consegnate alle applicazioni a valle integrate utilizzando un URL di consegna.

La ricerca delle risorse approvate corrette dall’archivio di Experience Manager è il primo passo per consegnare le risorse utilizzando l’URL di consegna. La risposta alla richiesta di ricerca comprende un array di documenti JSON corrispondenti alle risorse che soddisfano i criteri di ricerca. Ogni documento JSON viene identificato utilizzando un campo `id`, utilizzato per comporre la richiesta di consegna della risorsa.

![Panoramica del protocollo di caricamento binario diretto](assets/search-assets-api-overview.png)

Puoi definire le proprietà all’interno della richiesta API Search Assets per abilitare le seguenti funzionalità:

* **Ricerca full-text**: utilizza la query `match` per definire il testo da cercare.  È inoltre possibile utilizzare gli operatori all&#39;interno della query `match` per filtrare i risultati.

* **Applica filtri**: utilizzare la query `term` per filtrare ulteriormente i risultati definendo un `key` e uno o più valori. `key` identifica il campo il cui valore deve corrispondere e `value` rappresenta l&#39;elemento su cui confrontare il valore. Analogamente, è possibile utilizzare la query `range` per definire un intervallo per un campo utilizzando le proprietà Greater-than (gt), Greater-than o equal-to (gte), Less-than (lt) e Less-than o equal-to (lte).

* **Ordina risultati**: utilizzare la proprietà `OrderBy` per ordinare i risultati di ricerca in base a uno o più campi. Puoi ordinare i risultati in ordine crescente o decrescente.

* **Paginazione**: utilizzare le proprietà `limit` e `cursor` per definire le proprietà di paginazione all&#39;interno di una richiesta API di ricerca. La proprietà `limit` definisce il numero massimo di elementi da recuperare in una risposta API. La proprietà `cursor` facilita il recupero del punto iniziale per il successivo set di risorse definito nella proprietà `limit`. Ad esempio, se definisci `50` come limite nella richiesta API, puoi utilizzare la proprietà `cursor` per avviare e recuperare i successivi 50 elementi utilizzando la richiesta API successiva.

## Endpoint API per la ricerca di risorse {#search-assets-api-endpoint}

L’endpoint in una richiesta API di Search assets deve essere nel seguente formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

Il dominio di consegna è simile nella struttura al dominio dell’ambiente di authoring Experience Manager. L&#39;unica differenza consiste nella sostituzione del termine `author` con `delivery`.

`pXXXX` fa riferimento all&#39;ID del programma

`eYYYY` fa riferimento all&#39;ID ambiente

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

Per richiamare l&#39;API di ricerca, è necessario un token IMS per definire nei dettagli `Authorization`. Il token IMS viene recuperato da un account tecnico. Consulta [Recuperare le credenziali di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=it#fetch-the-aem-as-a-cloud-service-credentials) per creare un nuovo account tecnico. Consulta [Generazione del token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=it#generating-the-access-token) per generare il token IMS e utilizzarlo in modo appropriato nell&#39;intestazione della richiesta API di Search Assets.

Per visualizzare esempi di richieste, campioni di risposta e codici di risposta, vedere [Cerca nell&#39;API Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/search).
