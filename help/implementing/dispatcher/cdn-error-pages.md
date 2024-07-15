---
title: Configurazione delle pagine di errore CDN
description: Scopri come ignorare la pagina di errore predefinita ospitando file statici nell’archiviazione self-hosted, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a essi in un file di configurazione distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 5%

---

# Configurazione delle pagine di errore CDN {#cdn-error-pages}

Nel caso improbabile che la [rete CDN gestita dall&#39;Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) non raggiunga l&#39;origine dell&#39;AEM, per impostazione predefinita la rete CDN fornisce una pagina di errore generica senza marchio che indica che il server non può essere raggiunto. È possibile ignorare la pagina di errore predefinita ospitando file statici nell&#39;archiviazione self-hosted, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a tali file in un file di configurazione distribuito utilizzando la [pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Configurazione {#setup}

Prima di poter sovrascrivere la pagina di errore predefinita, è necessario effettuare le seguenti operazioni:

* Crea questa cartella e struttura di file nella cartella di livello principale del progetto Git:

```
config/
     cdn.yaml
```

* Il file di configurazione `cdn.yaml` deve contenere sia i metadati che le regole descritte negli esempi seguenti. Il parametro `kind` deve essere impostato su `CDN` e la versione deve essere impostata sulla versione dello schema, attualmente `1`.

* Crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager. Consulta [configurazione delle pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configurazione delle pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

**Note**

* Al momento gli RDE non supportano la pipeline di configurazione.
* Puoi utilizzare `yq` per convalidare localmente la formattazione YAML del file di configurazione (ad es. `yq cdn.yaml`).

### Configurazione {#configuration}

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
