---
title: Riferimenti sviluppatore per [!DNL Assets]
description: Le API di [!DNL Assets] e il contenuto di riferimento per sviluppatori consentono di gestire le risorse, inclusi file binari, metadati, rappresentazioni, commenti e così via [!DNL Content Fragments].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# [!DNL Assets] API e materiale di riferimento per sviluppatori {#assets-cloud-service-apis}

L&#39;articolo contiene materiale di riferimento e risorse per gli sviluppatori di [!DNL Assets] come Cloud Service. Include un nuovo metodo di caricamento, riferimenti API e informazioni sul supporto fornito nei flussi di lavoro di post-elaborazione.

## Caricamento risorsa {#asset-upload-technical}

[!DNL Experience Manager] come Cloud Service fornisce un nuovo metodo per caricare le risorse nell’archivio. Gli utenti possono caricare direttamente le risorse nell’archiviazione cloud utilizzando l’API HTTP. I passaggi per caricare un file binario sono:

1. [Invia una richiesta](#initiate-upload)HTTP. Consente di informare [!DNL Experience Manage]o distribuire l’intento di caricare un nuovo file binario.
1. [POST il contenuto del file binario](#upload-binary) a uno o più URI forniti dalla richiesta di avvio.
1. [Inviate una richiesta](#complete-upload) HTTP per informare il server che il contenuto del file binario è stato caricato correttamente.

![Panoramica del protocollo di caricamento binario diretto](assets/add-assets-technical.png)

Questo approccio fornisce una gestione scalabile e più efficace dei caricamenti delle risorse. Le differenze rispetto al punto [!DNL Experience Manager] 6.5 sono:

* I file binari non passano attraverso [!DNL Experience Manager], il che ora consiste semplicemente nel coordinare il processo di caricamento con l&#39;archiviazione cloud binaria configurata per la distribuzione.
* L&#39;archiviazione cloud binario funziona con una rete CDN (Content Delivery Network) o Edge. Una rete CDN seleziona un endpoint di caricamento più vicino a un client. Quando i dati si spostano a una distanza più breve da un endpoint vicino, le prestazioni di caricamento e l&#39;esperienza dell&#39;utente migliorano, soprattutto per i team distribuiti geograficamente.

>[!NOTE]
>
>Consultate il codice client per implementare questo approccio nella libreria [open-source](https://github.com/adobe/aem-upload)aem-upload.

### Avvia caricamento {#initiate-upload}

Inviate una richiesta di POST HTTP alla cartella desiderata. Le risorse vengono create o aggiornate in questa cartella. Includete il selettore `.initiateUpload.json` per indicare che la richiesta deve avviare il caricamento di un file binario. Ad esempio, il percorso della cartella in cui deve essere creata la risorsa è `/assets/folder`. La richiesta POST è `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Il tipo di contenuto del corpo della richiesta deve essere costituito dai dati del `application/x-www-form-urlencoded` modulo, contenente i campi seguenti:

* `(string) fileName`: Obbligatorio. Nome della risorsa così come viene visualizzata [!DNL Experience Manager].
* `(number) fileSize`: Obbligatorio. La dimensione del file, in byte, della risorsa da caricare.

Per avviare il caricamento di più file binari è possibile utilizzare una singola richiesta, purché ciascun file binario contenga i campi richiesti. In caso di esito positivo, la richiesta risponde con un codice di `201` stato e un corpo contenente dati JSON nel seguente formato:

```json
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

* `completeURI` (stringa): Chiama questo URI al termine del caricamento del binario. L’URI può essere assoluto o relativo e i client devono essere in grado di gestire entrambi. Questo significa che il valore può essere `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Vedere caricamento [](#complete-upload)completo.
* `folderPath` (stringa): Percorso completo della cartella in cui viene caricato il binario.
* `(files)` (array): Un elenco di elementi la cui lunghezza e ordine corrispondono alla lunghezza e all&#39;ordine dell&#39;elenco delle informazioni binarie fornite nella richiesta di avvio.
* `fileName` (stringa): Il nome del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `mimeType` (stringa): Il tipo mime del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `uploadToken` (stringa): Token di caricamento per il binario corrispondente. Questo valore deve essere incluso nella richiesta completa.
* `uploadURIs` (array): Un elenco di stringhe i cui valori sono URI completi in cui caricare il contenuto del binario (consultate [Carica binario](#upload-binary)).
* `minPartSize` (numero): Lunghezza minima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se è presente più di un URI.
* `maxPartSize` (numero): Lunghezza massima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se è presente più di un URI.

### Carica binario {#upload-binary}

L’output di avvio del caricamento include uno o più valori URI di caricamento. Se viene fornito più di un URI, il client divide il binario in parti ed effettua la richiesta POST di ciascuna parte in ciascun URI, in ordine. Utilizzate tutti gli URI. Assicurarsi che le dimensioni di ciascuna parte siano comprese tra le dimensioni minime e massime specificate nella risposta di avvio. I nodi Edge CDN consentono di accelerare il caricamento dei file binari richiesto.

Un potenziale metodo a tal fine consiste nel calcolare la dimensione della parte in base al numero di URI di caricamento forniti dall&#39;API. Ad esempio, si supponga che la dimensione totale del binario sia 20.000 byte e che il numero di URI di caricamento sia 2. Effettuate quindi le seguenti operazioni:

* Calcola la dimensione della parte dividendo la dimensione totale per il numero di URI: 20.000 / 2 = 10.000.
* Intervallo di byte POST 0-9,999 del binario al primo URI nell&#39;elenco degli URI di caricamento.
* Intervallo di byte POST 10.000 - 19.999 del binario al secondo URI nell’elenco degli URI di caricamento.

Se il caricamento ha esito positivo, il server risponde a ogni richiesta con un codice di `201` stato.

### Caricamento completo {#complete-upload}

Dopo aver caricato tutte le parti di un file binario, inviate una richiesta di POST HTTP all’URI completo fornito dai dati di avvio. Il tipo di contenuto del corpo della richiesta deve essere costituito dai dati del `application/x-www-form-urlencoded` modulo, contenente i campi seguenti.

| espandibili | Tipo | Obbligatorio o no | Descrizione |
|---|---|---|---|
| `fileName` | Stringa | Obbligatorio | Nome della risorsa, come fornito dai dati di iniziazione. |
| `mimeType` | Stringa | Obbligatorio | Il tipo di contenuto HTTP del binario, come fornito dai dati di avvio. |
| `uploadToken` | Stringa | Obbligatorio | Token di caricamento per il binario, come fornito dai dati di avvio. |
| `createVersion` | Booleano | Facoltativo | Se esiste `True` e una risorsa con il nome specificato, [!DNL Experience Manager] crea una nuova versione della risorsa. |
| `versionLabel` | Stringa | Facoltativo | Se viene creata una nuova versione, l’etichetta associata alla nuova versione di una risorsa. |
| `versionComment` | Stringa | Facoltativo | Se viene creata una nuova versione, i commenti associati alla versione. |
| `replace` | Booleano | Facoltativo | Se esiste `True` e una risorsa con il nome specificato, [!DNL Experience Manager] la risorsa viene eliminata e quindi ricreata. |

>!![NOTE]
Se la risorsa esiste e non `createVersion` viene specificata né `replace` specificata, [!DNL Experience Manager] aggiorna la versione corrente della risorsa con il nuovo binario.

Come il processo di avvio, i dati completi della richiesta possono contenere informazioni per più file.

Il processo di caricamento di un file binario non viene eseguito finché non viene richiamato l’URL completo per il file. Una risorsa viene elaborata al termine del processo di caricamento. L&#39;elaborazione non viene avviata anche se il file binario della risorsa viene caricato completamente ma il processo di caricamento non viene completato.

In caso di esito positivo, il server risponde con un codice di `200` stato.

### Libreria di caricamento open-source {#open-source-upload-library}

Per ulteriori informazioni sugli algoritmi di caricamento o per creare script e strumenti di caricamento personalizzati,  Adobe fornisce librerie e strumenti open source:

* [Libreria](https://github.com/adobe/aem-upload)di caricamento aem open-source.
* [Comando](https://github.com/adobe/aio-cli-plugin-aem)open-source

### API di caricamento risorse obsolete {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Il nuovo metodo di caricamento è supportato solo [!DNL Adobe Experience Manager] come Cloud Service. Le API di [!DNL Adobe Experience Manager] 6.5 sono obsolete. I metodi relativi al caricamento o all&#39;aggiornamento di risorse o rappresentazioni (qualsiasi caricamento binario) sono obsoleti nelle seguenti API:

* [API HTTP Risorse Experience Manager](mac-api-assets.md)
* `AssetManager` API Java, come `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Libreria](https://github.com/adobe/aem-upload)di caricamento aem open-source.
* [Comando](https://github.com/adobe/aio-cli-plugin-aem)open-source


## Flussi di lavoro di elaborazione e post-elaborazione delle risorse {#post-processing-workflows}

In [!DNL Experience Manager]questo caso, l’elaborazione delle risorse si basa sulla configurazione **[!UICONTROL Profili]** di elaborazione che utilizza i microservizi [delle](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)risorse. L&#39;elaborazione non richiede estensioni per sviluppatori.

Per la configurazione del flusso di lavoro di post-elaborazione, utilizzate i flussi di lavoro standard con estensioni con passaggi personalizzati.

## Supporto dei passaggi del flusso di lavoro nel flusso di lavoro di post-elaborazione {#post-processing-workflows-steps}

I clienti che eseguono l’aggiornamento da versioni precedenti di [!DNL Experience Manager] possono utilizzare i microservizi delle risorse per elaborare le risorse. I microservizi delle risorse nativi nel cloud sono molto più semplici da configurare e utilizzare. Alcuni passaggi del flusso di lavoro utilizzati nel flusso di lavoro [!UICONTROL DAM Update Asset] nella versione precedente non sono supportati.

[!DNL Experience Manager] come Cloud Service supportano i seguenti passaggi del flusso di lavoro:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

I seguenti modelli di flusso di lavoro tecnico vengono sostituiti da asset microservices o il supporto non è disponibile:

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

>[!MORELIKETHIS]
* [Experience Cloud  come SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)Cloud Service.

