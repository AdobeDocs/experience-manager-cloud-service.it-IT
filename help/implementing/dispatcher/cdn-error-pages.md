---
title: Configurazione delle pagine di errore CDN
description: Scopri come ignorare la pagina di errore predefinita ospitando file statici nell’archiviazione self-hosted, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a essi in un file di configurazione distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---


# Configurazione delle pagine di errore CDN {#cdn-error-pages}

Nel caso improbabile che la [rete CDN gestita dall&#39;Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) non raggiunga l&#39;origine dell&#39;AEM, per impostazione predefinita la rete CDN fornisce una pagina di errore generica senza marchio che indica che il server non può essere raggiunto. È possibile ignorare la pagina di errore predefinita ospitando i file statici nell&#39;archiviazione con hosting autonomo, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a tali file in un file di configurazione distribuito utilizzando la pipeline di configurazione [config di Cloud Manager.](/help/operations/config-pipeline.md#managing-in-cloud-manager)

## Configurazione {#setup}

Prima di poter sovrascrivere la pagina di errore predefinita, è necessario effettuare le seguenti operazioni:

1. Creare un file denominato `cdn.yaml` o simile, facendo riferimento alla sezione relativa alla sintassi riportata di seguito.

1. Posizionare il file in una cartella di primo livello denominata *config* o simile, come descritto nell&#39;articolo [config pipeline](/help/operations/config-pipeline.md#folder-structure).

1. Creare una pipeline di configurazione in Cloud Manager, come descritto nell&#39;articolo [config pipeline](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Distribuisci la configurazione.

### Sintassi {#syntax}

La pagina di errore viene implementata come applicazione a pagina singola (SPA) e fa riferimento a una serie di proprietà, come illustrato nell’esempio seguente.  I file statici a cui fanno riferimento gli URL devono essere ospitati da te su un servizio accessibile a Internet come Amazon S3 o Azure Blob Storage.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```
Per una descrizione delle proprietà al di sopra del nodo dati, consulta l&#39;articolo [config pipeline](/help/operations/config-pipeline.md#common-syntax). Il valore della proprietà kind deve essere *CDN* e la proprietà `version` deve essere impostata su *1*.


| Nome | Proprietà consentite | Significato |
|-----------|--------------------------|-------------|
| **spa** | titolo | Titolo della pagina di errore. |
|     | icoUrl | URL a un file di icona. |
|     | cssUrl | URL a un file CSS. |
|     | jsUrl | URL a un file JavaScript. |

### Esempio di HTML generato {#sample-generated-html}

Il codice HTML generato dalla rete CDN e distribuito al client, ad esempio un browser, assomiglierà (ma non sarà identico) al seguente snippet:

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### Test {#testing}

A scopo di test, chiama l’endpoint dedicato con il codice di errore supportato, ad esempio:

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

I codici supportati sono: 403, 404, 406, 500 e 503.

In questo modo, attivi direttamente il gestore degli errori della rete CDN per testare la risposta sintetica per un determinato codice di errore.
