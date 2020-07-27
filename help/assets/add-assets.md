---
title: Aggiungi le tue risorse digitali a [!DNL Adobe Experience Manager].
description: Aggiungi le tue risorse digitali [!DNL Adobe Experience Manager] a un Cloud Service.
translation-type: tm+mt
source-git-commit: 9c5dd93be316417014fc665cc813a0d83c3fac6f
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# Aggiungere risorse digitali al Adobe Experience Manager  {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] arricchisce il contenuto binario dei file digitali caricati con metadati avanzati, smart tag, rappresentazioni e altri servizi di gestione delle risorse digitali (DAM). Potete caricare vari tipi di file, ad esempio immagini, documenti e file immagine non elaborati, dalla cartella locale o da un’unità di rete a [!DNL Experience Manager Assets].

Sono disponibili diversi metodi di caricamento. Oltre al caricamento del browser più comunemente utilizzato, esistono altri metodi per aggiungere risorse all&#39;archivio Experience Manager , inclusi client desktop, come Adobe Asset Link o  app desktop Experience Manager, script di caricamento e caricamento che i clienti potrebbero creare e integrazioni di assimilazione automatizzate aggiunte  estensioni Experience Manager.

Qui ci concentreremo sui metodi di caricamento per gli utenti finali e forniremo collegamenti agli articoli che descrivono gli aspetti tecnici del caricamento e dell’assimilazione delle risorse tramite  API e SDK Experience Manager.

Sebbene sia possibile caricare e gestire qualsiasi file binario in  Experience Manager, i formati file più comunemente utilizzati supportano servizi aggiuntivi, come l&#39;estrazione di metadati o la generazione di anteprime/rappresentazioni. Per informazioni dettagliate, fare riferimento ai formati [di file](file-format-support.md) supportati.

Potete anche scegliere di effettuare un’ulteriore elaborazione sulle risorse caricate. Potete configurare diversi profili di elaborazione delle risorse nella cartella in cui vengono caricate le risorse per aggiungere metadati, rappresentazioni o servizi di elaborazione delle immagini specifici. Per ulteriori informazioni, consulta [Ulteriore elaborazione](#additional-processing) .

>[!NOTE]
>
> Experience Manager come Cloud Service sfrutta un nuovo metodo di caricamento delle risorse: caricamento binario diretto. È supportato per impostazione predefinita dalle funzionalità e dai client di prodotto preconfigurati, come &#39;interfaccia utente Experience Manager, Adobe Asset Link,  app desktop Experience Manager, e quindi trasparenti per gli utenti finali.
>
>Il codice di caricamento personalizzato o esteso dai team tecnici dei clienti deve usare le nuove API e i nuovi protocolli di caricamento.

## Upload assets {#upload-assets}

Per caricare uno o più file, potete selezionarli sul desktop e trascinarli sull’interfaccia utente (browser Web) nella cartella di destinazione. In alternativa, potete avviare il caricamento dall’interfaccia utente.

1. Nell’interfaccia [!DNL Assets] utente, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare le risorse, effettuate una delle seguenti operazioni:

   * Sulla barra degli strumenti, toccate l&#39;icona **[!UICONTROL Crea]** . Quindi, dal menu, toccate **[!UICONTROL File]**. Se necessario, potete rinominare il file nella finestra di dialogo visualizzata.
   * In un browser che supporta HTML5, trascinate le risorse direttamente sull’interfaccia [!DNL Assets] utente. La finestra di dialogo per rinominare il file non viene visualizzata.

   ![create_menu](assets/create_menu.png)

   Per selezionare più file, premete il tasto Ctrl o Comando e selezionate le risorse nella finestra di dialogo del selettore file. Quando usate un iPad, potete selezionare un solo file alla volta.

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

1. Per annullare un caricamento in corso, fate clic su Chiudi (`X`) accanto alla barra di avanzamento. Quando annullate l’operazione di caricamento, [!DNL Assets] elimina la parte parzialmente caricata della risorsa.

   Se annullate l’operazione di caricamento prima del caricamento dei file, [!DNL Assets] interrompe il caricamento del file corrente e aggiorna il contenuto. Tuttavia, i file già caricati non vengono eliminati.


<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->


1. Nella finestra di dialogo di avanzamento del caricamento [!DNL Assets] viene visualizzato il numero di file caricati correttamente e i file che non sono stati caricati correttamente.

Inoltre, l’interfaccia utente di Risorse mostra la risorsa più recente caricata o la cartella creata per la prima volta.

>[!NOTE]
>
>Per caricare gerarchie di cartelle nidificate in AEM, consultate Caricare [in massa le risorse](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Gestione dei caricamenti quando la risorsa esiste già {#handling-upload-existing-file}

Se caricate una risorsa con lo stesso nome di una già disponibile nel percorso in cui state caricando la risorsa, viene visualizzata una finestra di dialogo di avviso.

Potete scegliere di sostituire una risorsa esistente, crearne un’altra o tenerle entrambe rinominando la nuova risorsa caricata. Se sostituite una risorsa esistente, i metadati della risorsa e le eventuali modifiche precedenti (ad esempio annotazioni, ritaglio e così via) apportate alla risorsa esistente vengono eliminati. Se scegliete di mantenere entrambe le risorse, la nuova risorsa viene rinominata con il numero `1` aggiunto al nome.

>[!NOTE]
>
>Quando selezionate **[!UICONTROL Sostituisci]** nella finestra di dialogo Conflitto  nome, l’ID risorsa viene rigenerato per la nuova risorsa. Questo ID è diverso dall’ID della risorsa precedente.
>
>Se Asset Insights è abilitato per tenere traccia di impression/clic con Adobe  Analytics, l’ID risorsa rigenerata invalida i dati acquisiti per la risorsa su  Analytics.

Per mantenere la risorsa duplicata in [!DNL Assets], fate clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, toccate o fate clic su **[!UICONTROL Elimina]**.

### Gestione dei nomi dei file e caratteri non consentiti {#filename-handling}

[!DNL Experience Manager Assets] impedisce il caricamento di risorse con i caratteri proibiti nel nome del file. Se provate a caricare una risorsa con un nome file contenente un carattere non consentito o più, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento fino a quando non rimuovete questi caratteri o lo caricate con un nome consentito.

Per soddisfare convenzioni di denominazione dei file specifiche per la vostra organizzazione, la finestra di dialogo [!UICONTROL Carica risorse] consente di specificare nomi lunghi per i file caricati.

Tuttavia, i seguenti caratteri (elenco separato da spazi) non sono supportati:

* il nome del file di risorse non deve contenere `* / : [ \\ ] | # % { } ? &`
* il nome della cartella di risorse non deve contenere `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricare in blocco le risorse {#bulk-upload}

Per caricare un numero maggiore di file, in particolare se esistono in una gerarchia di cartelle nidificata su disco, è possibile utilizzare i seguenti approcci:

* Utilizzate uno script o uno strumento di caricamento personalizzato che sfrutta le API [di caricamento delle](developer-reference-material-apis.md#asset-upload-technical)risorse. Questo strumento personalizzato può aggiungere ulteriore gestione delle risorse (ad esempio, tradurre i metadati o rinominare i file), se necessario.
* Utilizzate [app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) desktop Experience Manager per caricare gerarchie di cartelle nidificate.

>[!NOTE]
>
>Il caricamento in blocco come parte della migrazione dei contenuti da altri sistemi quando la configurazione e la distribuzione  Experience Manager richiedono un’attenta pianificazione, considerazione e scelta degli strumenti. Consultate la guida [alla](/help/implementing/deploying/overview.md) distribuzione per informazioni sugli approcci per la migrazione dei contenuti.

## Caricare le risorse mediante client desktop {#upload-assets-desktop-clients}

Oltre all&#39;interfaccia utente del browser Web,  Experience Manager supporta altri client sul desktop. Offrono inoltre un’esperienza di caricamento senza dover passare al browser Web.

* [Collegamento](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) risorse Adobe consente di accedere alle risorse dalle applicazioni desktop Adobe Photoshop, Adobe Illustrator e Adobe InDesign [!DNL Experience Manager] . Potete caricare il documento attualmente aperto [!DNL Experience Manager] direttamente dall’interfaccia utente di Adobe Asset Link dall’interno di queste applicazioni desktop.
* [&#39;app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) desktop Experience Manager semplifica l&#39;utilizzo delle risorse sul desktop, indipendentemente dal tipo di file o dall&#39;applicazione nativa che le gestisce. È particolarmente utile caricare i file in gerarchie di cartelle nidificate dal file system locale, in quanto il caricamento del browser supporta solo il caricamento di elenchi di file semplici.

## Elaborazione aggiuntiva {#additional-processing}

Per un’ulteriore elaborazione delle risorse caricate, potete usare i profili di elaborazione delle risorse presenti nella cartella in cui vengono caricate. Sono disponibili nella finestra di dialogo **[!UICONTROL Proprietà]** della cartella.

![assets-folder-properties](assets/assets-folder-properties.png)

Sono disponibili i seguenti profili:

* [I profili](metadata-profiles.md) di metadati consentono di applicare proprietà di metadati predefinite alle risorse caricate in tale cartella
* [I profili](asset-microservices-configure-and-use.md#processing-profiles) di elaborazione consentono di applicare l&#39;elaborazione delle rappresentazioni e di generare rappresentazioni oltre a quelle predefinite

Inoltre, se Dynamic Media è abilitato nell’ambiente in uso:

* [I profili](dynamic-media/image-profiles.md) immagine di Dynamic Media consentono di applicare alle risorse caricate specifiche configurazioni di ritaglio (ritaglio **** avanzato e ritaglio pixel) e nitidezza.
* [I profili](dynamic-media/video-profiles.md) video Dynamic Media consentono di applicare specifici profili di codifica video (risoluzione, formato, parametri).

>[!NOTE]
>
>Il ritaglio Dynamic Media e altre operazioni sulle risorse non sono distruttive, ovvero non modificano l’originale caricato, ma forniscono parametri per il ritaglio o la trasformazione del supporto da eseguire durante la distribuzione delle risorse

Per le cartelle a cui è assegnato un profilo di elaborazione, il nome del profilo viene visualizzato sulla miniatura nella vista a schede. Nella vista a elenco, il nome del profilo viene visualizzato nella colonna Profilo **[!UICONTROL di]** elaborazione.

## Caricare o assimilare le risorse mediante le API {#upload-using-apis}

I dettagli tecnici delle API e del protocollo di caricamento e i collegamenti all’SDK open-source e ai client di esempio sono forniti nella sezione di caricamento [delle](developer-reference-material-apis.md#asset-upload-technical) risorse del riferimento per sviluppatori.

>[!MORELIKETHIS]
>
>* [App desktop Adobe Experience Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-desktop-app/using/introduction.html)
>* [Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Documentazione di Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Riferimento tecnico per il caricamento delle risorse](developer-reference-material-apis.md#asset-upload-technical)

