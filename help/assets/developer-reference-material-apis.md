---
title: Riferimenti per sviluppatori per [!DNL Assets]
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments].'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 77b4d9f07626419ddab3a7363b06c382447ec982
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] API e materiale di riferimento per sviluppatori  {#assets-cloud-service-apis}

L’articolo contiene raccomandazioni, materiali di riferimento e risorse per gli sviluppatori di [!DNL Assets] come [!DNL Cloud Service]. Include un nuovo modulo di caricamento delle risorse, riferimenti API e informazioni sul supporto fornito nei flussi di lavoro di post-elaborazione.

## [!DNL Experience Manager Assets] API e operazioni  {#use-cases-and-apis}

[!DNL Assets] as a  [!DNL Cloud Service] fornisce diverse API per interagire in modo programmatico con le risorse digitali. Ciascuna API supporta casi d’uso specifici, come indicato nella tabella seguente. L’ [!DNL Assets] interfaccia utente, l’ [!DNL Experience Manager] app desktop e [!DNL Adobe Asset Link] supportano tutte o parte delle operazioni.

>[!CAUTION]
>
>Alcune API continuano a esistere ma non sono supportate attivamente (contrassegnate con un ×) e non devono essere utilizzate.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| . | Supportata |
| × | Non supportato. Non usare. |
| - | Non disponibile |

| Caso d’uso | [aem-upload](https://github.com/adobe/aem-upload) | [API AEM / Sling / ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava | [Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Servlet Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _(anteprima)_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **binario originale** |  |  |  |  |  |  |
| Crea originale | . | × | - | × | × | - |
| Leggi originale | - | × | . | . | . | - |
| Aggiorna originale | . | × | . | × | × | - |
| Elimina originale | - | . | - | . | . | - |
| Copia originale | - | . | - | . | . | - |
| Sposta originale | - | . | - | . | . | - |
| **Metadati** |  |  |  |  |  |  |
| Creare metadati | - | . | . | . | . | - |
| Leggi metadati | - | . | - | . | . | - |
| Aggiornare i metadati | - | . | . | . | . | - |
| Eliminare i metadati | - | . | . | . | . | - |
| Copia metadati | - | . | - | . | . | - |
| Spostare i metadati | - | . | - | . | . | - |
| **Frammenti di contenuto (CF)** |  |  |  |  |  |  |
| Crea CF | - | . | - | . | - | - |
| Leggi CF | - | . | - | . | - | . |
| Aggiorna CF | - | . | - | . | - | - |
| Elimina CF | - | . | - | . | - | - |
| Copia CF | - | . | - | . | - | - |
| Sposta CF | - | . | - | . | - | - |
| **Versioni** |  |  |  |  |  |  |
| Crea versione | . | . | - | - | - | - |
| Versione lettura | - | . | - | - | - | - |
| Elimina versione | - | . | - | - | - | - |
| **Cartelle** |  |  |  |  |  |  |
| Crea cartella | . | . | - | . | - | - |
| Leggi cartella | - | . | - | . | - | - |
| Elimina cartella | . | . | - | . | - | - |
| Copia cartella | . | . | - | . | - | - |
| Sposta cartella | . | . | - | . | - | - |

## Caricamento risorsa {#asset-upload-technical}

[!DNL Experience Manager] as a  [!DNL Cloud Service] fornisce un nuovo metodo per caricare le risorse nell’archivio. Gli utenti possono caricare direttamente le risorse nell’archiviazione cloud utilizzando l’API HTTP. I passaggi per caricare un file binario sono i seguenti:

1. [Invia una richiesta](#initiate-upload) HTTP. Indica a [!DNL Experience Manage]r la distribuzione dell&#39;intento di caricare un nuovo binario.
1. [POST il contenuto del ](#upload-binary) binario a uno o più URI forniti dalla richiesta di avvio.
1. [Invia una ](#complete-upload) richiesta HTTP per informare il server che il contenuto del binario è stato caricato correttamente.

![Panoramica del protocollo di caricamento binario diretto](assets/add-assets-technical.png)

L’approccio fornisce una gestione scalabile e più performante del caricamento delle risorse. Le differenze rispetto a [!DNL Experience Manager] 6.5 sono le seguenti:

* I binari non passano attraverso [!DNL Experience Manager], che ora sta semplicemente coordinando il processo di caricamento con l&#39;archiviazione cloud binaria configurata per la distribuzione.
* L’archiviazione cloud binaria funziona con una rete CDN (Content Delivery Network) o Edge. Una rete CDN seleziona un endpoint di caricamento più vicino per un client. Quando i dati si spostano a una distanza più breve da un endpoint vicino, le prestazioni di caricamento e l’esperienza utente migliorano, soprattutto per i team distribuiti geograficamente.

>[!NOTE]
Vedi il codice client per implementare questo approccio nella libreria open-source [aem-upload](https://github.com/adobe/aem-upload).

### Avviare il caricamento {#initiate-upload}

Invia una richiesta HTTP POST alla cartella desiderata. Le risorse vengono create o aggiornate in questa cartella. Includi il selettore `.initiateUpload.json` per indicare che la richiesta è quella di avviare il caricamento di un file binario. Ad esempio, il percorso della cartella in cui deve essere creata la risorsa è `/assets/folder`. La richiesta POST è `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Il tipo di contenuto del corpo della richiesta deve essere costituito da dati del modulo `application/x-www-form-urlencoded` contenenti i campi seguenti:

* `(string) fileName`: Obbligatorio. Il nome della risorsa così come viene visualizzato in [!DNL Experience Manager].
* `(number) fileSize`: Obbligatorio. La dimensione del file, in byte, della risorsa da caricare.

È possibile utilizzare una singola richiesta per avviare i caricamenti per più binari, purché ogni binario contenga i campi richiesti. In caso di esito positivo, la richiesta risponde con un codice di stato `201` e un corpo contenente dati JSON nel seguente formato:

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

* `completeURI` (stringa): Chiama questo URI al termine del caricamento del binario. L’URI può essere un URI assoluto o relativo e i client devono essere in grado di gestirlo. In altre parole, il valore può essere `"https://author.acme.com/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Consulta [upload completo](#complete-upload).
* `folderPath` (stringa): Percorso completo della cartella in cui viene caricato il binario.
* `(files)` (matrice): Elenco di elementi la cui lunghezza e ordine corrispondono alla lunghezza e all’ordine dell’elenco delle informazioni binarie fornite nella richiesta di avvio.
* `fileName` (stringa): Il nome del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `mimeType` (stringa): Il tipo mime del binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `uploadToken` (stringa): Un token di caricamento per il binario corrispondente. Questo valore deve essere incluso nella richiesta completa.
* `uploadURIs` (matrice): Elenco di stringhe i cui valori sono URI completi a cui deve essere caricato il contenuto del binario (consulta  [Carica binario](#upload-binary)).
* `minPartSize` (numero): Lunghezza minima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se sono presenti più URI.
* `maxPartSize` (numero): La lunghezza massima, in byte, dei dati che possono essere forniti a uno qualsiasi degli URI di caricamento, se sono presenti più URI.

### Carica binario {#upload-binary}

L&#39;output di avvio di un caricamento include uno o più valori URI di caricamento. Se viene fornito più di un URI, il client divide il binario in parti ed effettua la richiesta POST di ciascuna parte in ogni URI, in ordine. Usa tutti gli URI. Assicurati che le dimensioni di ogni parte siano entro le dimensioni minime e massime specificate nella risposta di avvio. I nodi edge CDN consentono di accelerare il caricamento richiesto dei binari.

Un metodo potenziale per farlo è calcolare la dimensione della parte in base al numero di URI di caricamento forniti dall’API. Ad esempio, si supponga che la dimensione totale del binario sia di 20.000 byte e che il numero di URI di caricamento sia di 2. Quindi segui questi passaggi:

* Calcola la dimensione della parte dividendo la dimensione totale per il numero di URI: 20.000 / 2 = 10.000.
* Intervallo di byte di POST 0-9.999 del binario al primo URI nell’elenco degli URI di caricamento.
* Intervallo di byte di POST 10.000 - 19.999 del binario al secondo URI nell’elenco degli URI di caricamento.

Se il caricamento ha esito positivo, il server risponde a ogni richiesta con un codice di stato `201`.

### Caricamento completo {#complete-upload}

Dopo aver caricato tutte le parti di un file binario, invia una richiesta HTTP POST all’URI completo fornito dai dati di avvio. Il tipo di contenuto del corpo della richiesta deve essere `application/x-www-form-urlencoded` dati del modulo, contenente i campi seguenti.

| espandibili | Tipo | Obbligatorio o no | Descrizione |
|---|---|---|---|
| `fileName` | Stringa | Obbligatorio | Nome dell’attività, come indicato dai dati di apertura. |
| `mimeType` | Stringa | Obbligatorio | Il tipo di contenuto HTTP del binario, come fornito dai dati di avvio. |
| `uploadToken` | Stringa | Obbligatorio | Carica il token per il binario, come fornito dai dati di avvio. |
| `createVersion` | Booleano | Facoltativo | Se esiste `True` e una risorsa con il nome specificato, [!DNL Experience Manager] crea una nuova versione della risorsa. |
| `versionLabel` | Stringa | Facoltativo | Se viene creata una nuova versione, l’etichetta associata alla nuova versione di una risorsa . |
| `versionComment` | Stringa | Facoltativo | Se viene creata una nuova versione, i commenti associati alla versione. |
| `replace` | Booleano | Facoltativo | Se esiste `True` e una risorsa con il nome specificato, [!DNL Experience Manager] elimina la risorsa, quindi la ricrea. |

>[!NOTE]
Se la risorsa esiste e non è specificato né `createVersion` né `replace`, [!DNL Experience Manager] aggiorna la versione corrente della risorsa con il nuovo binario.

Come il processo di avvio, i dati completi della richiesta possono contenere informazioni per più di un file.

Il processo di caricamento di un binario non viene eseguito finché non viene richiamato l’URL completo per il file. Una risorsa viene elaborata al termine del processo di caricamento. L’elaborazione non si avvia anche se il file binario della risorsa viene caricato completamente ma il processo di caricamento non è completato.

In caso di esito positivo, il server risponde con un codice di stato `200`.

### Libreria di caricamento open source {#open-source-upload-library}

Per ulteriori informazioni sugli algoritmi di caricamento o per creare script e strumenti di caricamento personalizzati, Adobe fornisce librerie e strumenti open source:

* [Libreria](https://github.com/adobe/aem-upload) open-source aem-upload.
* [Strumento](https://github.com/adobe/aio-cli-plugin-aem) a riga di comando open source

### API di caricamento risorse obsolete {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Il nuovo metodo di caricamento è supportato solo per [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Le API di [!DNL Adobe Experience Manager] 6.5 sono obsolete. I metodi relativi al caricamento o all’aggiornamento di risorse o rappresentazioni (qualsiasi caricamento binario) sono obsoleti nelle seguenti API:

* [API HTTP di Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API Java, come  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Libreria](https://github.com/adobe/aem-upload) open-source aem-upload.
* [Strumento](https://github.com/adobe/aio-cli-plugin-aem) a riga di comando open source


## Flussi di lavoro di elaborazione e post-elaborazione delle risorse {#post-processing-workflows}

In [!DNL Experience Manager], l’elaborazione delle risorse si basa sulla configurazione **[!UICONTROL Profili di elaborazione]** che utilizza i [microservizi per le risorse](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). L’elaborazione non richiede estensioni per sviluppatori.

Per la configurazione del flusso di lavoro di post-elaborazione, utilizza i flussi di lavoro standard con estensioni con passaggi personalizzati.

## Supporto dei passaggi del flusso di lavoro nel flusso di lavoro di post-elaborazione {#post-processing-workflows-steps}

I clienti che eseguono l’aggiornamento dalle versioni precedenti di [!DNL Experience Manager] possono utilizzare i microservizi per le risorse per elaborare le risorse. I microservizi per le risorse native per il cloud sono molto più semplici da configurare e utilizzare. Alcuni passaggi del flusso di lavoro utilizzati nel flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] nella versione precedente non sono supportati.

[!DNL Experience Manager] come  [!DNL Cloud Service] supporto dei seguenti passaggi del flusso di lavoro:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

I seguenti modelli di flusso di lavoro tecnici vengono sostituiti dai microservizi per le risorse o il supporto non è disponibile:

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
* [Experience Cloud come  [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

