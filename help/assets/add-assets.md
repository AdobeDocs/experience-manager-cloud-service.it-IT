---
title: Aggiungi le risorse digitali a [!DNL Adobe Experience Manager].
description: Aggiungi le risorse digitali a  [!DNL Adobe Experience Manager] come a [!DNL Cloud Service].
translation-type: tm+mt
source-git-commit: 7e8c794752073da0b4815c97dc53282989cd3fb5
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 1%

---


# Aggiungere risorse digitali ad Adobe Experience Manager {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] arricchisce il contenuto binario dei file digitali caricati con metadati avanzati, smart tag, rappresentazioni e altri servizi di gestione delle risorse digitali (DAM). Potete caricare vari tipi di file, ad esempio immagini, documenti e file immagine non elaborati, dalla cartella locale o da un&#39;unità di rete a [!DNL Experience Manager Assets].

Sono disponibili diversi metodi di caricamento. Oltre al caricamento del browser più comunemente utilizzato, esistono altri metodi per aggiungere risorse all&#39;archivio [!DNL Experience Manager], inclusi client desktop, come  collegamento risorsa Adobe o [!DNL Experience Manager] app desktop, script di caricamento e caricamento che i clienti potrebbero creare e integrazioni di assimilazione automatizzate aggiunte come estensioni [!DNL Experience Manager].

Qui ci concentreremo sui metodi di caricamento per gli utenti finali e forniremo collegamenti agli articoli che descrivono gli aspetti tecnici del caricamento e dell&#39;assimilazione delle risorse tramite [!DNL Experience Manager] API e SDK.

Anche se potete caricare e gestire qualsiasi file binario in [!DNL Experience Manager], i formati file più comunemente utilizzati supportano servizi aggiuntivi, come l&#39;estrazione di metadati o la generazione di anteprime/rappresentazioni. Per ulteriori informazioni, fare riferimento a [formati di file supportati](file-format-support.md).

Potete anche scegliere di effettuare un’ulteriore elaborazione sulle risorse caricate. Potete configurare diversi profili di elaborazione delle risorse nella cartella in cui vengono caricate le risorse per aggiungere metadati, rappresentazioni o servizi di elaborazione delle immagini specifici. Consultate [elaborare le risorse durante il caricamento](#process-when-uploaded).

>[!NOTE]
>
>[!DNL Experience Manager] come strumento  [!DNL Cloud Service] che sfrutta un nuovo metodo di caricamento delle risorse: caricamento binario diretto. È supportato per impostazione predefinita dalle funzionalità e dai client dei prodotti forniti, come l&#39;interfaccia utente [!DNL Experience Manager], l&#39;app [!DNL Adobe Asset Link], [!DNL Experience Manager] desktop, e quindi trasparente per gli utenti finali.
>
>Il codice di caricamento personalizzato o esteso dai team tecnici dei clienti deve usare le nuove API e i nuovi protocolli di caricamento.

Le risorse come [!DNL Cloud Service] forniscono i seguenti metodi di caricamento.  Adobe consiglia di comprendere il caso d’uso e l’applicabilità di un’opzione di caricamento prima di utilizzarla.

| Metodo Carica | Quando utilizzare? | Persona principale |
|---------------------|----------------|-----------------|
| [Interfaccia utente della console Risorse](#upload-assets) | Caricamento occasionale, facilità di pressione e trascinamento, caricamento del mirino. Non usate per caricare un gran numero di risorse. | Tutti gli utenti |
| [API di caricamento](#upload-using-apis) | Per decisioni dinamiche durante il caricamento. | Developer (Sviluppatore) |
| [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Caricamento di risorse a basso volume, ma per la migrazione. | Amministratore, Marketer |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Utile quando creativi e professionisti del marketing lavorano sulle risorse dalle app desktop [!DNL Creative Cloud] supportate. | Creative, Marketer |
| [Caricamento massa risorsa](#asset-bulk-ingestor) | Consigliato per migrazioni su larga scala e ingestioni di massa occasionali. Solo per gli archivi dati supportati. | Amministratore, sviluppatore |

## Caricare le risorse {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Per caricare uno o più file, potete selezionarli sul desktop e trascinarli sull’interfaccia utente (browser Web) nella cartella di destinazione. In alternativa, potete avviare il caricamento dall’interfaccia utente.

1. Nell&#39;interfaccia utente [!DNL Assets], andate alla posizione in cui desiderate aggiungere le risorse digitali.
1. Per caricare le risorse, effettuate una delle seguenti operazioni:

   * Sulla barra degli strumenti, fare clic su **[!UICONTROL Crea]** > **[!UICONTROL File]**. Se necessario, potete rinominare il file nella finestra di dialogo visualizzata.
   * In un browser che supporta HTML5, trascinate le risorse direttamente sull&#39;interfaccia utente [!DNL Assets]. La finestra di dialogo per rinominare il file non viene visualizzata.

   ![create_menu](assets/create_menu.png)

   Per selezionare più file, selezionate il tasto `Ctrl` o `Command` e selezionate le risorse nella finestra di dialogo del selettore file. Quando usate un iPad, potete selezionare un solo file alla volta.

1. Per annullare un caricamento in corso, fate clic su Chiudi (`X`) accanto alla barra di avanzamento. Quando annullate l’operazione di caricamento, [!DNL Assets] elimina la parte parzialmente caricata della risorsa.
Se annullate un&#39;operazione di caricamento prima del caricamento dei file, [!DNL Assets] interrompe il caricamento del file corrente e aggiorna il contenuto. Tuttavia, i file già caricati non vengono eliminati.

1. La finestra di dialogo di avanzamento del caricamento in [!DNL Assets] mostra il numero di file caricati correttamente e i file che non sono stati caricati correttamente.
Inoltre, l&#39;interfaccia utente [!DNL Assets] mostra la risorsa più recente caricata o la cartella creata per prima.

>[!NOTE]
>
>Per caricare gerarchie di cartelle nidificate, consultate [caricare in massa risorse](#bulk-upload).

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

Potete caricare una risorsa con lo stesso percorso (lo stesso nome e la stessa posizione) di una risorsa esistente. Tuttavia, viene visualizzata una finestra di dialogo di avviso con le seguenti opzioni:

* Sostituisci risorsa esistente: Se sostituite una risorsa esistente, i metadati della risorsa e le eventuali modifiche precedenti (ad esempio annotazioni, ritaglio e così via) apportate alla risorsa esistente vengono eliminati.
* Create un&#39;altra versione: Nella directory archivio viene creata una nuova versione della risorsa esistente. È possibile visualizzare le due versioni nella [!UICONTROL Timeline] e, se necessario, ripristinare la versione esistente precedente.
* Mantieni entrambi: Se scegliete di mantenere entrambe le risorse, la nuova risorsa viene rinominata con il numero `1` aggiunto al nome.

>[!NOTE]
>
>Quando si seleziona **[!UICONTROL Replace]** nella finestra di dialogo [!UICONTROL Name Conflict], l&#39;ID risorsa viene rigenerato per la nuova risorsa. Questo ID è diverso dall’ID della risorsa precedente.
>
>Se Asset Insights è abilitato per tenere traccia delle impression o dei clic con [!DNL Adobe Analytics], l’ID risorsa rigenerata invalida i dati acquisiti per la risorsa su [!DNL Analytics].

Per mantenere la risorsa duplicata in [!DNL Assets], fate clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, toccate o fate clic su **[!UICONTROL Elimina]**.

### Gestione dei nomi dei file e caratteri non consentiti {#filename-handling}

[!DNL Experience Manager Assets] tenta di impedire il caricamento di risorse con i caratteri proibiti nel nome del file. Se provate a caricare una risorsa con un nome file contenente un carattere non consentito o più, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento fino a quando non rimuovete questi caratteri o lo caricate con un nome consentito. Alcuni metodi di caricamento non impediscono il caricamento di risorse con caratteri proibiti nei nomi dei file, ma sostituiscono i caratteri con `-`.

Per rispettare convenzioni di denominazione dei file specifiche per la vostra organizzazione, la finestra di dialogo [!UICONTROL Carica risorse] consente di specificare nomi lunghi per i file caricati. I seguenti caratteri (elenco separato da spazi) non sono supportati:

* caratteri non validi per il nome del file di risorse `* / : [ \\ ] | # % { } ? &`
* caratteri non validi per il nome della cartella di risorse `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricamento in blocco delle risorse {#bulk-upload}

L’assimilazione di massa delle risorse può gestire migliaia di risorse in modo efficiente. Tuttavia, un&#39;assimilazione su larga scala non è solo un dump di file ampio e grande o una migrazione cieca. Affinché sia un progetto significativo che possa essere utile al tuo scopo aziendale, la pianificazione e la cura delle risorse portano a un&#39;assimilazione molto più efficiente. Tutte le operazioni di assimilazione non sono le stesse e non è possibile generalizzare senza tenere conto della composizione e delle esigenze aziendali dei repository. Di seguito sono riportati alcuni suggerimenti generali per pianificare ed eseguire un&#39;assimilazione in blocco:

* Cura risorse: Rimuovere risorse non necessarie nel DAM. Prendete in considerazione la rimozione di risorse inutilizzate, obsolete o duplicate. Questo riduce i dati trasferiti e le risorse assimilate, consentendo un&#39;assimilazione più rapida.
* Organizzare le risorse: È consigliabile organizzare il contenuto in un ordine logico, ad esempio per dimensione file, formato file, caso di utilizzo o priorità. In generale, i file complessi di grandi dimensioni richiedono maggiore elaborazione. Potete anche considerare l’assimilazione separata dei file di grandi dimensioni utilizzando l’opzione di filtro delle dimensioni dei file (descritta di seguito).
* Assunzioni scaglioni: Considerate la possibilità di suddividere l’assimilazione in più progetti di assimilazione di massa. Questo consente di visualizzare il contenuto prima e di aggiornarlo secondo necessità. Ad esempio, potete assimilare risorse che richiedono molta elaborazione nelle ore non di picco o gradualmente in più blocchi. Tuttavia, potete assimilare risorse più piccole e semplici che non richiedono molta elaborazione contemporaneamente.

Per caricare un numero maggiore di file, utilizzate uno dei seguenti approcci. Vedere anche i [casi di utilizzo e metodi](#upload-methods-comparison)

* [API](developer-reference-material-apis.md#asset-upload-technical) di caricamento risorse: Usate uno script o uno strumento di caricamento personalizzato che sfrutta le API per aggiungere ulteriore gestione delle risorse (ad esempio, tradurre i metadati o rinominare i file), se necessario.
* [[!DNL Experience Manager] app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) desktop: Utile per i creativi professionisti del marketing che caricano le risorse dal file system locale. Utilizzatelo per caricare localmente le cartelle nidificate disponibili.
* [Strumento](#asset-bulk-ingestor) di assimilazione di massa: Utilizzate per l&#39;assimilazione di grandi quantità di risorse occasionalmente o inizialmente durante la distribuzione  [!DNL Experience Manager].

### Strumento di inserimento di massa risorse {#asset-bulk-ingestor}

Lo strumento viene fornito solo al gruppo di amministratori per l&#39;assimilazione su larga scala delle risorse da archivi dati di Azure o S3.

Per configurare lo strumento, effettuare le seguenti operazioni:

1. Passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Importazione in blocco]**. Selezionare l&#39;opzione **[!UICONTROL Crea]**.

![Configurazione dell&#39;importatore di massa](assets/bulk-import-config.png)

1. Nella [!UICONTROL configurazione di importazione in blocco], fornire i valori richiesti.

   * [!UICONTROL Titolo]: Titolo descrittivo.
   * [!UICONTROL Importa origine]: Selezionare l&#39;origine dati applicabile.
   * [!UICONTROL Filtra per dimensione] min.: Specificate la dimensione minima dei file delle risorse in MB.
   * [!UICONTROL Filtra per dimensione] massima: Specificate la dimensione massima dei file delle risorse in MB.
   * [!UICONTROL Escludi tipi] di mime: Elenco separato da virgole di tipi MIME da escludere dall’assimilazione. Esempio, `image/jpeg, image/.*, video/mp4`.
   * [!UICONTROL Includi tipi] mime: Elenco di tipi MIME separati da virgole da includere nell&#39;assimilazione. Vedere [tutti i formati di file supportati](/help/assets/file-format-support.md).
   * [!UICONTROL Modalità] di importazione: Selezionate Ignora, Sostituisci o Crea versione. La modalità Ignora è l’impostazione predefinita e in questa modalità l’assimilatore salta per importare una risorsa, se esiste già. Vedere il significato di [sostituire e creare le opzioni di versione](#handling-upload-existing-file).
   * [!UICONTROL Cartella] di destinazione risorse: Importare una cartella in DAM in cui importare le risorse. Esempio, `/content/dam/imported_assets`

1. Puoi eliminare, modificare, eseguire e fare di più con le configurazioni di assimilazione create. Quando selezionate una configurazione per l’inserimento di massa, nella barra degli strumenti sono disponibili le seguenti opzioni.

   * [!UICONTROL Modifica]: Modifica la configurazione selezionata.
   * [!UICONTROL Elimina]: Elimina la configurazione selezionata.
   * [!UICONTROL Controlla]: Convalida della connessione all&#39;archivio dati.
   * [!UICONTROL Prova]: Richiama un&#39;esecuzione di test dell&#39;assimilazione in blocco.
   * [!UICONTROL Esegui]: Esegui la configurazione selezionata.
   * [!UICONTROL Interrompi]: Terminare una configurazione attiva.
   * [!UICONTROL Stato] processo: Visualizzare lo stato della configurazione quando viene utilizzata in un processo di importazione in corso o utilizzata per un processo completato.
   * [!UICONTROL Visualizza risorse]: Visualizzate la cartella di destinazione, se esiste.

>[!NOTE]
>
>Il caricamento in blocco come parte della migrazione dei contenuti da altri sistemi durante la configurazione e la distribuzione in [!DNL Experience Manager] richiede un&#39;attenta pianificazione, considerazione e scelta degli strumenti. Per informazioni sugli approcci per la migrazione dei contenuti, consultate la [guida alla distribuzione](/help/implementing/deploying/overview.md).

## Caricare le risorse mediante client desktop {#upload-assets-desktop-clients}

Oltre all&#39;interfaccia utente del browser Web, [!DNL Experience Manager] supporta altri client sul desktop. Offrono inoltre un’esperienza di caricamento senza dover passare al browser Web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) consente di accedere alle risorse  [!DNL Experience Manager] nelle  applicazioni desktop Adobe Photoshop,  Adobe Illustrator e  Adobe InDesign. È possibile caricare il documento aperto in [!DNL Experience Manager] direttamente dall&#39;interfaccia utente di Collegamento risorse di  Adobe direttamente da queste applicazioni desktop.
* [[!DNL Experience Manager] le ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) applicazioni desktop semplificano l’utilizzo delle risorse sul desktop, indipendentemente dal tipo di file o dall’applicazione nativa che le gestisce. È particolarmente utile caricare i file in gerarchie di cartelle nidificate dal file system locale, in quanto il caricamento del browser supporta solo il caricamento di elenchi di file semplici.

## Elabora risorse durante il caricamento di {#process-when-uploaded}

Per eseguire un’ulteriore elaborazione sulle risorse caricate, potete applicare i profili di elaborazione alle cartelle di caricamento. I profili sono disponibili nella pagina **[!UICONTROL Proprietà]** di una cartella in [!DNL Assets].

![assets-folder-properties](assets/assets-folder-properties.png)

Sono disponibili le seguenti schede:

* [I ](metadata-profiles.md) profili di metadati consentono di applicare proprietà di metadati predefinite alle risorse caricate in tale cartella
* [I ](asset-microservices-configure-and-use.md) profili di elaborazione consentono di generare più rappresentazioni di quante siano possibili per impostazione predefinita.

Inoltre, se [!DNL Dynamic Media] è abilitato nella distribuzione, sono disponibili le seguenti schede:

* [I ](dynamic-media/image-profiles.md) profili Immagine elemento multimediale dinamico consentono di applicare alle risorse caricate specifiche impostazioni di ritaglio (**** Ritaglio avanzato e ritaglio pixel) e nitidezza.
* [I ](dynamic-media/video-profiles.md) profili video per contenuti multimediali dinamici consentono di applicare specifici profili di codifica video (risoluzione, formato, parametri).

>[!NOTE]
>
>Il ritaglio di elementi multimediali dinamici e altre operazioni sulle risorse non sono distruttive, ovvero non modificano l’originale caricato, ma forniscono parametri per il ritaglio o la trasformazione di elementi multimediali da eseguire durante la distribuzione delle risorse

Per le cartelle a cui è assegnato un profilo di elaborazione, il nome del profilo viene visualizzato sulla miniatura nella vista a schede. Nella vista a elenco, il nome del profilo viene visualizzato nella colonna **[!UICONTROL Profilo di elaborazione]**.

## Caricare o assimilare le risorse mediante le API {#upload-using-apis}

I dettagli tecnici delle API e del protocollo di caricamento e i collegamenti all’SDK open-source e ai client di esempio sono forniti nella sezione [caricamento delle risorse](developer-reference-material-apis.md#asset-upload-technical) del riferimento per gli sviluppatori.

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Informazioni [!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentazione](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Riferimento tecnico per il caricamento delle risorse](developer-reference-material-apis.md#asset-upload-technical)

