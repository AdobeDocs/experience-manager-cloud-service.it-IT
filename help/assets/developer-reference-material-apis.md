---
title: 'API Assets per la gestione delle risorse digitali in Adobe Experience Manager come servizio Cloud '
description: Le API Assets consentono operazioni di base di creazione-lettura-aggiornamento-eliminazione (CRUD) per gestire le risorse, inclusi file binari, metadati, rappresentazioni, commenti e frammenti di contenuto.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## Caricamento risorsa {#asset-upload-technical}

Experience Manager come servizio cloud offre un nuovo metodo di caricamento delle risorse nell’archivio: caricamento binario diretto nell’archivio cloud binario. Questa sezione fornisce una panoramica tecnica.

### Panoramica del caricamento binario diretto {#overview-binary-upload}

L&#39;algoritmo di alto livello per caricare un binario è:

1. Inviate una richiesta HTTP per informare AEM dell’intenzione di caricare un nuovo file binario.
1. POST il contenuto del binario a uno o più URI forniti dalla richiesta di avvio.
1. Inviate una richiesta HTTP per informare il server che il contenuto del file binario è stato caricato correttamente.

![Panoramica del protocollo di caricamento binario diretto](assets/add-assets-technical.png)

Le differenze importanti rispetto alle versioni precedenti di AEM includono:

* I file binari non passano attraverso AEM, che ora sta semplicemente coordinando il processo di caricamento con lo storage cloud binario configurato per la distribuzione
* Lo storage cloud binario è caratterizzato da una rete di distribuzione dei contenuti (CDN, Edge Network), che avvicina l’endpoint di caricamento al client, migliorando le prestazioni di caricamento e l’esperienza dell’utente, in particolare per i team distribuiti che caricano le risorse

Questo approccio dovrebbe fornire una gestione più scalabile e performante dei caricamenti delle risorse.

> !![NOTE]
Per controllare il codice client che implementa questo approccio, fate riferimento alla libreria di caricamento [aem open-source](https://github.com/adobe/aem-upload)

### Avvia caricamento {#initiate-upload}

Il primo passaggio consiste nell’inviare una richiesta HTTP POST alla cartella in cui deve essere creata o aggiornata la risorsa; includete il selettore `.initiateUpload.json` per indicare che la richiesta deve iniziare un caricamento binario. Ad esempio, il percorso della cartella in cui deve essere creata la risorsa è `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

Il tipo di contenuto del corpo della richiesta deve essere costituito dai dati del `application/x-www-form-urlencoded` modulo, contenente i campi seguenti:

* `(string) fileName`: Obbligatorio. Nome della risorsa così come apparirà nell’istanza.
* `(number) fileSize`: Obbligatorio. Lunghezza totale, in byte, del binario da caricare.

Per avviare il caricamento di più file binari è possibile utilizzare una singola richiesta, purché ciascun file binario contenga i campi richiesti. In caso di esito positivo, la richiesta risponde con un codice di `201` stato e un corpo contenente dati JSON nel seguente formato:

```
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI` (stringa): Richiamate questo URI al termine del caricamento del binario. L’URI può essere assoluto o relativo e i client devono essere in grado di gestire entrambi. Questo significa che il valore può essere `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Vedere caricamento [](#complete-upload)completo.
* `folderPath` (stringa): Percorso completo della cartella in cui viene caricato il binario.
* `(files)` (array): Un elenco di elementi la cui lunghezza e ordine corrisponderanno alla lunghezza e all&#39;ordine dell&#39;elenco delle informazioni binarie fornite nella richiesta di avvio.
* `fileName` (stringa): Il nome del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `mimeType` (stringa): Il tipo mime del binario corrispondente, come specificato nella richiesta di avvio in. Questo valore deve essere incluso nella richiesta completa.
* `uploadToken` (stringa): Token di caricamento per il binario corrispondente. Questo valore deve essere incluso nella richiesta completa.
* `uploadURIs` (array): Un elenco di stringhe i cui valori sono URI completi in cui caricare il contenuto del binario (consultate [Carica binario](#upload-binary)).
* `minPartSize` (numero): Lunghezza minima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se è presente più di un URI.
* `maxPartSize` (numero): Lunghezza massima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se è presente più di un URI.

### Carica binario {#upload-binary}

L’output di avvio di un caricamento includerà uno o più valori URI di caricamento. Se viene fornito più di un URI, è responsabilità del client &quot;dividere&quot; il binario in parti e POST ciascuna parte, in ordine, a ciascun URI, in ordine. Tutti gli URI devono essere utilizzati e ogni parte deve essere maggiore della dimensione minima e inferiore alla dimensione massima specificata nella risposta di avvio. Tali richieste saranno affrontate da nodi edge CDN per accelerare il caricamento dei file binari.

Un modo potenziale per ottenere questo risultato è calcolare la dimensione della parte in base al numero di URI di caricamento forniti dall&#39;API. Ad esempio, se la dimensione totale del binario è 20.000 byte e il numero di URI di caricamento è 2:

* Calcola la dimensione della parte dividendo la dimensione totale per il numero di URI: 20.000 / 2 = 10.000
* Intervallo di byte POST 0-9,999 del binario al primo URI nell&#39;elenco degli URI di caricamento
* Intervallo di byte POST 10.000 - 19.999 del binario al secondo URI nell&#39;elenco degli URI di caricamento

In caso di esito positivo, il server risponde a ogni richiesta con un codice di `201` stato.

### Caricamento completo {#complete-upload}

Dopo aver caricato tutte le parti di un file binario, inviate una richiesta POST HTTP all’URI completo fornito dai dati di avvio. Il tipo di contenuto del corpo della richiesta deve essere costituito dai dati del `application/x-www-form-urlencoded` modulo, contenente i campi seguenti.

| espandibili | Tipo | Obbligatorio o no | Descrizione |
|---|---|---|---|
| `fileName` | Stringa | Obbligatorio | Nome della risorsa, come fornito dai dati di iniziazione. |
| `mimeType` | Stringa | Obbligatorio | Il tipo di contenuto HTTP del binario, come fornito dai dati di avvio. |
| `uploadToken` | Stringa | Obbligatorio | Token di caricamento per il binario, come fornito dai dati di avvio. |
| `createVersion` | Booleano | Facoltativo | Se `True` e una risorsa con il nome specificato esiste già, Experience Manager crea una nuova versione della risorsa. |
| `versionLabel` | Stringa | Facoltativo | Se viene creata una nuova versione, l’etichetta associata alla nuova versione di una risorsa. |
| `versionComment` | Stringa | Facoltativo | Se viene creata una nuova versione, i commenti associati alla versione. |
| `replace` | Booleano | Facoltativo | Se `True` e una risorsa con il nome specificato esiste già, Experience Manager elimina la risorsa e quindi la ricrea. |

>!![NOTE]
>
> Se la risorsa esiste già e non `createVersion` viene specificata né `replace` specificata, Experience Manager aggiorna la versione corrente della risorsa con il nuovo binario.

Come il processo di avvio, i dati completi della richiesta possono contenere informazioni per più file.

Il processo di caricamento di un file binario non viene eseguito finché non viene richiamato l’URL completo per il file. Anche se il binario di un file viene caricato interamente, la risorsa non verrà elaborata dall’istanza fino al completamento del processo di caricamento.

In caso di esito positivo, il server risponde con un codice di `200` stato.

### Libreria di caricamento open-source {#open-source-upload-library}

Per ulteriori informazioni sugli algoritmi di caricamento o per creare script e strumenti di caricamento personalizzati, Adobe fornisce librerie e strumenti open source come punti di partenza:

* [Libreria di caricamento aem open-source](https://github.com/adobe/aem-upload)
* [Open-source, strumento da riga di comando](https://github.com/adobe/aio-cli-plugin-aem)

### API di caricamento risorse obsolete {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Per Adobe Experience Manager come servizio Cloud sono supportate solo le nuove API di caricamento. Le API di Adobe Experience Manager 6.5 sono obsolete. I metodi relativi al caricamento o all&#39;aggiornamento di risorse o rappresentazioni (qualsiasi caricamento binario) sono obsoleti nelle seguenti API:

* [API HTTP AEM Assets](mac-api-assets.md)
* `AssetManager` API Java, come `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Libreria](https://github.com/adobe/aem-upload)di caricamento aem open-source.
* [Comando](https://github.com/adobe/aio-cli-plugin-aem)open-source


## Flussi di lavoro di elaborazione e post-elaborazione delle risorse {#post-processing-workflows}

In Experience Manager, l&#39;elaborazione delle risorse è basata sulla configurazione **[!UICONTROL Profili]** elaborazione che utilizza i microservizi [delle](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)risorse. L&#39;elaborazione non richiede estensioni per sviluppatori.

Per la configurazione del flusso di lavoro di post-elaborazione, utilizzate i flussi di lavoro standard con estensioni con passaggi personalizzati.

## Supporto dei passaggi del flusso di lavoro nel flusso di lavoro di post-elaborazione {#post-processing-workflows-steps}

I clienti che eseguono l’aggiornamento a Experience Manager come servizio Cloud dalle versioni precedenti di Experience Manager possono utilizzare i microservizi delle risorse per l’elaborazione delle risorse. I microservizi delle risorse nativi nel cloud sono molto più semplici da configurare e utilizzare. Alcuni passaggi del flusso di lavoro utilizzati nel flusso di lavoro [!UICONTROL DAM Update Asset] nella versione precedente non sono supportati.

I seguenti passaggi del flusso di lavoro sono supportati in Experience Manager come servizio Cloud.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

I seguenti modelli di flusso di lavoro tecnico vengono sostituiti da risorse microservizi o il supporto non è disponibile.

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->
