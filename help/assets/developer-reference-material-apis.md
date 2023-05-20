---
title: Riferimenti per sviluppatori per [!DNL Assets]
description: "[!DNL Assets] API e contenuti di riferimento per sviluppatori consentono di gestire le risorse, tra cui file binari, metadati, rappresentazioni, commenti e [!DNL Content Fragments]."
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] casi d’uso per sviluppatori, API e materiale di riferimento {#assets-cloud-service-apis}

L’articolo contiene consigli, materiali di riferimento e risorse per gli sviluppatori di [!DNL Assets] as a [!DNL Cloud Service]. Include un nuovo modulo di caricamento delle risorse, un riferimento API e informazioni sul supporto fornito nei flussi di lavoro di post-elaborazione.

## [!DNL Experience Manager Assets] API e operazioni {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] fornisce diverse API per interagire in modo programmatico con le risorse digitali. Ogni API supporta casi d’uso specifici, come indicato nella tabella seguente. Il [!DNL Assets] interfaccia utente, [!DNL Experience Manager] app desktop e [!DNL Adobe Asset Link] supporta tutte o alcune delle operazioni.

>[!CAUTION]
>
>Alcune API continuano a esistere ma non sono supportate attivamente (indicate con un ×). Per quanto possibile, non utilizzare queste API.

| Livello di supporto | Descrizione |
| ------------- | --------------------------- |
| ✓ | Funzione supportata |
| × | Non supportato. Non utilizzare. |
| - | Non disponibile |

| Caso d’uso | [aem-caricamento](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) API Java | [servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlet | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binario originale** |  |  |  |  |  |  |
| Crea originale | ✓ | × | - | × | × | - |
| Leggi originale | - | × | ✓ | ✓ | ✓ | - |
| Aggiorna originale | ✓ | × | ✓ | × | × | - |
| Elimina originale | - | ✓ | - | ✓ | ✓ | - |
| Copia originale | - | ✓ | - | ✓ | ✓ | - |
| Sposta originale | - | ✓ | - | ✓ | ✓ | - |
| **Metadati** |  |  |  |  |  |  |
| Creare i metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Leggi metadati | - | ✓ | - | ✓ | ✓ | - |
| Aggiornare i metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Elimina metadati | - | ✓ | ✓ | ✓ | ✓ | - |
| Copia metadati | - | ✓ | - | ✓ | ✓ | - |
| Sposta metadati | - | ✓ | - | ✓ | ✓ | - |
| **Frammenti di contenuto (CF)** |  |  |  |  |  |  |
| Crea CF | - | ✓ | - | ✓ | - | - |
| Lettura CF | - | ✓ | - | ✓ | - | ✓ |
| Aggiorna CF | - | ✓ | - | ✓ | - | - |
| Elimina CF | - | ✓ | - | ✓ | - | - |
| Copia CF | - | ✓ | - | ✓ | - | - |
| Sposta CF | - | ✓ | - | ✓ | - | - |
| **Versioni** |  |  |  |  |  |  |
| Crea versione | ✓ | ✓ | - | - | - | - |
| Versione di lettura | - | ✓ | - | - | - | - |
| Elimina versione | - | ✓ | - | - | - | - |
| **Cartelle** |  |  |  |  |  |  |
| Crea cartella | ✓ | ✓ | - | ✓ | - | - |
| Leggi cartella | - | ✓ | - | ✓ | - | - |
| Elimina cartella | ✓ | ✓ | - | ✓ | - | - |
| Copia cartella | ✓ | ✓ | - | ✓ | - | - |
| Sposta cartella | ✓ | ✓ | - | ✓ | - | - |

## Caricamento risorse {#asset-upload}

In entrata [!DNL Experience Manager] as a [!DNL Cloud Service], puoi caricare direttamente le risorse nell’archiviazione cloud utilizzando l’API HTTP. Di seguito sono riportati i passaggi per caricare un file binario. Esegui questi passaggi in un’applicazione esterna e non all’interno del [!DNL Experience Manager] JVM

1. [Inviare una richiesta HTTP](#initiate-upload). Informa [!DNL Experience Manage]o la distribuzione dell’intento di caricare un nuovo binario.
1. [PUT il contenuto del file binario](#upload-binary) a uno o più URI forniti dalla richiesta di avvio.
1. [Inviare una richiesta HTTP](#complete-upload) per informare il server che il contenuto del binario è stato caricato correttamente.

![Panoramica del protocollo di caricamento binario diretto](assets/add-assets-technical.png)

>[!IMPORTANT]
Eseguire i passaggi precedenti in un&#39;applicazione esterna e non all&#39;interno del [!DNL Experience Manager] JVM

L’approccio offre una gestione scalabile e più performante dei caricamenti di risorse. Le differenze rispetto a [!DNL Experience Manager] 6.5 sono:

* I file binari non vengono attraversati [!DNL Experience Manager], che ora coordina semplicemente il processo di caricamento con l’archiviazione cloud binaria configurata per la distribuzione.
* L’archiviazione cloud binaria funziona con una rete CDN (Content Delivery Network) o Edge. Una rete CDN seleziona un endpoint di caricamento più vicino a un client. Quando i dati vengono trasferiti a una distanza inferiore da un endpoint vicino, le prestazioni di caricamento e l’esperienza utente migliorano, in particolare per i team distribuiti geograficamente.

>[!NOTE]
Consulta il codice client per implementare questo approccio in open-source. [libreria di caricamento aem](https://github.com/adobe/aem-upload).
[!IMPORTANT]
In alcune circostanze, le modifiche potrebbero non propagarsi completamente tra le richieste di Experience Manager a causa della natura infine coerente dello storage nel Cloud Service. Questo porta a 404 risposte per avviare o completare chiamate di caricamento a causa della mancata propagazione delle creazioni della cartella richieste. I clienti devono aspettarsi risposte 404 e gestirle implementando un nuovo tentativo con una strategia di back-off.

### Avvia caricamento {#initiate-upload}

Invia una richiesta HTTP POST alla cartella desiderata. Le risorse vengono create o aggiornate in questa cartella. Includi il selettore `.initiateUpload.json` per indicare che la richiesta deve avviare il caricamento di un file binario. Ad esempio, il percorso della cartella in cui deve essere creata la risorsa è `/assets/folder`. La richiesta POST è `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Il tipo di contenuto del corpo della richiesta deve essere `application/x-www-form-urlencoded` dati del modulo, contenenti i seguenti campi:

* `(string) fileName`: Obbligatorio. Nome della risorsa così come appare in [!DNL Experience Manager].
* `(number) fileSize`: Obbligatorio. Dimensione file, in byte, della risorsa caricata.

È possibile utilizzare una singola richiesta per avviare caricamenti per più file binari, purché ogni file binario contenga i campi obbligatori. In caso di esito positivo, la richiesta risponde con un `201` il codice di stato e un corpo contenente i dati JSON nel formato seguente:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (stringa): chiama questo URI al termine del caricamento del binario. L’URI può essere assoluto o relativo e i client devono essere in grado di gestirlo. Il valore può essere `"https://[aem_server]:[port]/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"` Consulta [caricamento completo](#complete-upload).
* `folderPath` (stringa): percorso completo della cartella in cui viene caricato il file binario.
* `(files)` (matrice): Elenco di elementi la cui lunghezza e ordine corrispondono alla lunghezza e all&#39;ordine dell&#39;elenco di informazioni binarie fornite nella richiesta di avvio.
* `fileName` (stringa): nome del file binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `mimeType` (stringa): tipo mime del file binario corrispondente, come specificato nella richiesta di avvio. Questo valore deve essere incluso nella richiesta completa.
* `uploadToken` (stringa): token di caricamento per il file binario corrispondente. Questo valore deve essere incluso nella richiesta completa.
* `uploadURIs` (matrice): elenco di stringhe i cui valori sono URI completi in cui caricare il contenuto del binario (vedere [Carica binario](#upload-binary)).
* `minPartSize` (numero): Lunghezza minima, in byte, dei dati che possono essere forniti a uno qualsiasi dei `uploadURIs`, se è presente più di un URI.
* `maxPartSize` (numero): La lunghezza massima, in byte, dei dati che possono essere forniti a uno qualsiasi dei `uploadURIs`, se è presente più di un URI.

### Carica binario {#upload-binary}

L’output dell’avvio di un caricamento include uno o più valori URI di caricamento. Se viene fornito più di un URI, il client può suddividere il binario in parti ed effettuare richieste PUT di ciascuna parte agli URI di caricamento forniti, nell&#39;ordine. Se scegli di dividere il binario in parti, attieniti alle seguenti linee guida:

* Ciascuna parte, ad eccezione dell&#39;ultima, deve essere di dimensioni pari o superiori a `minPartSize`.
* Ogni parte deve avere una dimensione minore o uguale a `maxPartSize`.
* Se le dimensioni del file binario superano `maxPartSize`, dividi il binario in parti per caricarlo.
* Non è necessario utilizzare tutti gli URI.

Se la dimensione del file binario è minore o uguale a `maxPartSize`, è invece possibile caricare l’intero binario in un singolo URI di caricamento. Se viene fornito più di un URI di caricamento, utilizza il primo e ignora il resto. Non è necessario utilizzare tutti gli URI.

I nodi edge CDN consentono di accelerare il caricamento richiesto di dati binari.

Il modo più semplice per farlo è utilizzare il valore di `maxPartSize` come dimensione della parte. Il contratto API garantisce che siano presenti URI di caricamento sufficienti per caricare il file binario se utilizzi questo valore come dimensione della parte. Per eseguire questa operazione, dividere il binario in parti di dimensione `maxPartSize`, utilizzando un URI per ogni parte, nell&#39;ordine. La parte finale può essere di qualsiasi dimensione minore o uguale a `maxPartSize`. Si supponga, ad esempio, che la dimensione totale del file binario sia 20.000 byte, `minPartSize` è di 5.000 byte, `maxPartSize` è di 8.000 byte e il numero di URI di caricamento è 5. Esegui i seguenti passaggi:

* Carica i primi 8.000 byte del file binario utilizzando l’URI del primo caricamento.
* Carica i secondi 8.000 byte del file binario utilizzando il secondo URI di caricamento.
* Carica gli ultimi 4.000 byte del file binario utilizzando il terzo URI di caricamento. Poiché questa è la parte finale, non è necessario che sia maggiore di `minPartSize`.
* Non è necessario utilizzare gli ultimi due URI di caricamento. Puoi ignorarli.

Un errore comune consiste nel calcolare la dimensione della parte in base al numero di URI di caricamento forniti dall’API. Il contratto API non garantisce che questo approccio funzioni e può effettivamente causare dimensioni delle parti che non rientrano nell’intervallo tra `minPartSize` e `maxPartSize`. Questo può causare errori di caricamento binario.

Anche in questo caso, il modo più semplice e sicuro è quello di utilizzare semplicemente parti di dimensione uguale a `maxPartSize`.

Se il caricamento ha esito positivo, il server risponde a ogni richiesta con un `201` codice di stato.

>[!NOTE]
Per ulteriori informazioni sull&#39;algoritmo di caricamento, vedere [documentazione ufficiale delle funzioni](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) e [Documentazione API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) nel progetto Apache Jackrabbit Oak.

### Caricamento completo {#complete-upload}

Dopo aver caricato tutte le parti di un file binario, invia una richiesta HTTP POST all’URI completo fornito dai dati di avvio. Il tipo di contenuto del corpo della richiesta deve essere `application/x-www-form-urlencoded` dati del modulo, contenenti i seguenti campi.

| Campi | Tipo | Obbligatorio o no | Descrizione |
|---|---|---|---|
| `fileName` | Stringa | Obbligatorio | Nome della risorsa, fornito dai dati di avvio. |
| `mimeType` | Stringa | Obbligatorio | Il tipo di contenuto HTTP del binario, fornito dai dati di avvio. |
| `uploadToken` | Stringa | Obbligatorio | Carica il token per il file binario, fornito dai dati di avvio. |
| `createVersion` | Booleano | Facoltativo | Se `True` ed esiste già una risorsa con il nome specificato, quindi [!DNL Experience Manager] crea una nuova versione della risorsa. |
| `versionLabel` | Stringa | Facoltativo | Se viene creata una nuova versione, l’etichetta associata alla nuova versione di una risorsa. |
| `versionComment` | Stringa | Facoltativo | Se viene creata una nuova versione, i commenti associati alla versione. |
| `replace` | Booleano | Facoltativo | Se `True` ed esiste già una risorsa con il nome specificato, [!DNL Experience Manager] elimina la risorsa e la ricrea. |
| `uploadDuration` | Numero | Facoltativo | Tempo totale, in millisecondi, per il caricamento dell&#39;intero file. Se specificato, la durata del caricamento viene inclusa nei file di registro del sistema per l&#39;analisi della velocità di trasferimento. |
| `fileSize` | Numero | Facoltativo | Dimensione in byte del file. Se specificato, la dimensione del file viene inclusa nei file di registro del sistema per l&#39;analisi della velocità di trasferimento. |

>[!NOTE]
Se la risorsa esiste e nessuno dei due `createVersion` né `replace` è specificato, quindi [!DNL Experience Manager] aggiorna la versione corrente della risorsa con il nuovo binario.

Analogamente al processo di avvio, i dati completi della richiesta possono contenere informazioni relative a più file.

Il processo di caricamento di un file binario non viene eseguito finché non viene richiamato l’URL completo del file. Una risorsa viene elaborata al termine del processo di caricamento. L’elaborazione non viene avviata anche se il file binario della risorsa è stato caricato completamente, ma il processo di caricamento non è stato completato. Se il caricamento ha esito positivo, il server risponde con un `200` codice di stato.

### Libreria di caricamento open-source {#open-source-upload-library}

Per ulteriori informazioni sugli algoritmi di caricamento o per creare script e strumenti di caricamento, Adobe fornisce librerie e strumenti open-source:

* [Libreria aem-upload open-source](https://github.com/adobe/aem-upload).
* [Strumento a riga di comando open source](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
La libreria di caricamento AEM e lo strumento della riga di comando utilizzano entrambi [libreria node-httptransfer](https://github.com/adobe/node-httptransfer/)

### API di caricamento risorse obsolete {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Il nuovo metodo di caricamento è supportato solo per [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. Le API di [!DNL Adobe Experience Manager] 6.5 sono obsolete. I metodi relativi al caricamento o all’aggiornamento delle risorse o delle rappresentazioni (qualsiasi caricamento binario) sono obsoleti nelle seguenti API:

* [API HTTP EXPERIENCE MANAGER ASSETS](mac-api-assets.md)
* `AssetManager` API Java, like `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Libreria aem-upload open-source](https://github.com/adobe/aem-upload).
* [Strumento a riga di comando open source](https://github.com/adobe/aio-cli-plugin-aem).
* [Documentazione di Apache Jackrabbit Oak per il caricamento diretto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## Flussi di lavoro di elaborazione e post-elaborazione delle risorse {#post-processing-workflows}

In entrata [!DNL Experience Manager], l’elaborazione delle risorse si basa su **[!UICONTROL Profili elaborazione]** configurazione che utilizza [microservizi per risorse](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). L’elaborazione non richiede estensioni per sviluppatori.

Per la configurazione del flusso di lavoro di post-elaborazione, utilizza i flussi di lavoro standard con estensioni e passaggi personalizzati.

## Supporto dei passaggi del flusso di lavoro nella post-elaborazione del flusso di lavoro {#post-processing-workflows-steps}

Se esegui l’aggiornamento da una versione precedente di [!DNL Experience Manager], puoi utilizzare i microservizi per le risorse per elaborarle. I microservizi per le risorse native per il cloud sono più semplici da configurare e utilizzare. Alcuni passaggi del flusso di lavoro utilizzati in [!UICONTROL Aggiorna risorsa DAM] nella versione precedente non sono supportati. Per ulteriori informazioni sulle classi supportate, vedere [Riferimento API Java o JavaScript](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

I seguenti modelli di flusso di lavoro tecnico sono sostituiti dai microservizi per le risorse oppure il supporto non è disponibile:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati da Assets](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

