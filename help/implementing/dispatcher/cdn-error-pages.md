---
title: Configurazione delle pagine di errore CDN
description: Scopri come ignorare la pagina di errore predefinita ospitando file statici nell’archiviazione self-hosted, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a essi in un file di configurazione distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
source-git-commit: 11036c3e95f0444fc5d865232a7dccab5b7f26ae
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# Configurazione delle pagine di errore CDN {#cdn-error-pages}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, invia un messaggio e-mail a `aemcs-cdn-config-adopter@adobe.com` e descrivi il tuo caso d’uso.

Nel caso improbabile che il [CDN gestito da Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) non può raggiungere l’origine dell’AEM, per impostazione predefinita la rete CDN fornisce una pagina di errore generica e senza brand che indica che il server non può essere raggiunto. È possibile ignorare la pagina di errore predefinita ospitando file statici nell’archiviazione self-hosted, ad esempio Amazon S3 o Azure Blob Storage, e facendo riferimento a essi in un file di configurazione distribuito utilizzando [Pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Configurazione {#setup}

Prima di poter sovrascrivere la pagina di errore predefinita, è necessario effettuare le seguenti operazioni:

* Innanzitutto, crea questa cartella e struttura di file nella cartella di livello principale del progetto Git:

```
config/
     cdn.yaml
```

* In secondo luogo, `cdn.yaml` il file di configurazione deve contenere i metadati e i riferimenti alla pagina di errore, come descritto di seguito.

### Configurazione {#configuration}

La pagina di errore viene implementata come applicazione a pagina singola (SPA) e fa riferimento a una serie di proprietà, come illustrato nell’esempio seguente.  I file statici a cui fanno riferimento gli URL devono essere ospitati da te su un servizio accessibile a Internet come Amazon S3 o Azure Blob Storage.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
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
