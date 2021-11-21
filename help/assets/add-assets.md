---
title: Aggiungi le risorse digitali a [!DNL Adobe Experience Manager].
description: Aggiungi le risorse digitali a [!DNL Adobe Experience Manager] come [!DNL Cloud Service].
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: e7028272a32c2f53c3438cb918caaf04445442af
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 1%

---

# Aggiungi risorse digitali a [!DNL Adobe Experience Manager] come [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] accetta molti tipi di risorse digitali da molte sorgenti. Memorizza i binari e le rappresentazioni create, può eseguire l’elaborazione delle risorse utilizzando un’ampia gamma di flussi di lavoro e [!DNL Adobe Sensei] servizi, consente la distribuzione attraverso molti canali su più superfici.

[!DNL Adobe Experience Manager] arricchisce il contenuto binario dei file digitali caricati con metadati avanzati, tag avanzati, rappresentazioni e altri servizi di Digital Asset Management (DAM). È possibile caricare vari tipi di file, ad esempio immagini, documenti e file immagine non elaborati, dalla cartella locale o da un&#39;unità di rete a [!DNL Experience Manager Assets].

Oltre al caricamento del browser più comunemente utilizzato, altri metodi per aggiungere risorse al [!DNL Experience Manager] esiste un archivio, inclusi i client desktop, come Adobe Asset Link o [!DNL Experience Manager] script per app desktop, caricamento e acquisizione che i clienti creerebbero e integrazioni automatizzate di acquisizione aggiunte come [!DNL Experience Manager] estensioni.

Mentre puoi caricare e gestire qualsiasi file binario in [!DNL Experience Manager], i formati di file più comunemente utilizzati supportano servizi aggiuntivi, come l’estrazione dei metadati o la generazione di anteprime/rendering. Fai riferimento a [formati di file supportati](file-format-support.md) per i dettagli.

Puoi anche scegliere di eseguire un’ulteriore elaborazione sulle risorse caricate. È possibile configurare diversi profili di elaborazione delle risorse nella cartella in cui vengono caricate le risorse per aggiungere metadati, rappresentazioni o servizi di elaborazione delle immagini specifici. Vedi [elabora le risorse quando vengono caricate](#process-when-uploaded).

[!DNL Assets] fornisce i seguenti metodi di caricamento. L’Adobe consiglia di comprendere il caso d’uso e l’applicabilità di un’opzione di caricamento prima di utilizzarla.

| Metodo di caricamento | Quando utilizzare? | Persona principale |
|---------------------|----------------|-----------------|
| [Interfaccia utente della console Assets](#upload-assets) | Caricamento occasionale, facilità di pressione e trascinamento, caricamento del finder. Non utilizzare per caricare un numero elevato di risorse. | Tutti gli utenti |
| [Carica API](#upload-using-apis) | Per decisioni dinamiche durante il caricamento. | Developer (Sviluppatore) |
| App desktop [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Acquisizione di risorse a basso volume, ma non per la migrazione. | Amministratore, addetto al marketing |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Utile quando creativi e professionisti del marketing lavorano sulle risorse dall’interno del supportato [!DNL Creative Cloud] app desktop. | Creative, addetto al marketing |
| [Acquisizione in massa di risorse](#asset-bulk-ingestor) | Consigliato per migrazioni su larga scala e ingestioni di massa occasionali. Solo per i datastore supportati. | Amministratore, sviluppatore |

## Caricare le risorse {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Per caricare un file (o più file), puoi selezionarlo sul desktop e trascinarlo sull’interfaccia utente (browser web) nella cartella di destinazione. In alternativa, puoi avviare il caricamento da dall’interfaccia utente di .

1. In [!DNL Assets] nell’interfaccia utente, individua il percorso in cui desideri aggiungere risorse digitali.
1. Per caricare le risorse, effettua una delle seguenti operazioni:

   * Sulla barra degli strumenti, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL File]**. Se necessario, rinomina il file nella finestra di dialogo visualizzata.
   * In un browser che supporta HTML5, trascina le risorse direttamente sul [!DNL Assets] interfaccia utente. La finestra di dialogo per rinominare il file non viene visualizzata.

   ![crea_menu](assets/create_menu.png)

   Per selezionare più file, seleziona la `Ctrl` o `Command` e seleziona le risorse nella finestra di dialogo del selettore file. Quando utilizzi un iPad, puoi selezionare un solo file alla volta.

1. Per annullare un caricamento in corso, fai clic su chiudi (`X`) accanto alla barra di avanzamento. Quando si annulla l&#39;operazione di caricamento, [!DNL Assets] elimina la parte parzialmente caricata della risorsa.
Se annulli un&#39;operazione di caricamento prima del caricamento dei file, [!DNL Assets] interrompe il caricamento del file corrente e aggiorna il contenuto. Tuttavia, i file già caricati non vengono eliminati.

1. Finestra di dialogo di avanzamento del caricamento in [!DNL Assets] visualizza il numero di file caricati correttamente e i file che non sono stati caricati.
Inoltre, il [!DNL Assets] l’interfaccia utente visualizza la risorsa più recente caricata o la cartella creata per prima.

>[!NOTE]
>
>Per caricare gerarchie di cartelle nidificate, vedi [caricare in blocco le risorse](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Gestione dei caricamenti quando la risorsa esiste già {#handling-upload-existing-file}

Puoi caricare una risorsa con lo stesso percorso (nome e posizione identici) di una risorsa esistente. Tuttavia, viene visualizzata una finestra di dialogo di avviso con le seguenti opzioni:

* Sostituisci la risorsa esistente: Se sostituisci una risorsa esistente, i metadati della risorsa e le eventuali modifiche precedenti (ad esempio annotazioni, ritaglio e così via) apportate alla risorsa esistente vengono eliminati.
* Crea un&#39;altra versione: Nella directory archivio viene creata una nuova versione della risorsa esistente. È possibile visualizzare le due versioni nel [!UICONTROL Timeline] e, se necessario, può ripristinare la versione esistente precedente.
* Mantieni entrambi: Se scegli di mantenere entrambe le risorse, la nuova risorsa viene rinominata.

Per mantenere la risorsa duplicata in [!DNL Assets], fai clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, fai clic su **[!UICONTROL Elimina]**.

### Gestione dei nomi dei file e caratteri non consentiti {#filename-handling}

[!DNL Experience Manager Assets] tenta di impedire il caricamento di risorse con i caratteri non consentiti nei nomi dei file. Se tenti di caricare una risorsa con un nome file contenente un carattere non consentito o più, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento finché non rimuovi questi caratteri o li carichi con un nome consentito.

Per soddisfare convenzioni specifiche di denominazione dei file per la tua organizzazione, la [!UICONTROL Caricare risorse] La finestra di dialogo consente di specificare nomi lunghi per i file caricati. I seguenti caratteri (elenco separato da spazi) non sono supportati:

* caratteri non validi per il nome del file di risorse `* / : [ \\ ] | # % { } ? &`
* caratteri non validi per il nome della cartella risorse `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricamento in blocco delle risorse {#bulk-upload}

Il gestore di risorse in blocco può gestire in modo efficiente un numero molto elevato di risorse. Tuttavia, un’acquisizione su larga scala non è solo un’immagine di file ampia o una migrazione casuale. Affinché un’acquisizione su larga scala sia un progetto significativo per il tuo scopo aziendale ed efficiente, pianifica la migrazione e cura l’organizzazione delle risorse. Tutte le acquisizioni sono diverse, quindi invece di generalizzare, sono fattori nella composizione dell’archivio e nelle esigenze aziendali più articolate. Di seguito sono riportati alcuni suggerimenti generali per pianificare ed eseguire un’acquisizione in blocco:

* Cura risorse: Rimuovi le risorse non necessarie nel DAM. È consigliabile rimuovere le risorse inutilizzate, obsolete o duplicate. Questo consente di ridurre i dati trasferiti e le risorse acquisite, con conseguente maggiore velocità di assimilazione.
* Organizzare le risorse: È consigliabile organizzare il contenuto in un ordine logico, ad esempio per dimensione del file, formato del file, caso d’uso o priorità. In generale, i file complessi di grandi dimensioni richiedono una maggiore elaborazione. Puoi anche considerare l’acquisizione separata di file di grandi dimensioni utilizzando l’opzione di filtro delle dimensioni del file (descritta di seguito).
* Acquisizioni scaglioni: È consigliabile suddividere l’acquisizione in più progetti di inserimento in blocco. Questo ti consente di visualizzare il contenuto prima e di aggiornarlo come necessario. Ad esempio, puoi acquisire risorse ad alta intensità di elaborazione nelle ore non di picco o gradualmente in più blocchi. Tuttavia, puoi acquisire risorse più piccole e semplici che non richiedono molta elaborazione contemporaneamente.

Per caricare un numero maggiore di file, utilizza uno dei seguenti approcci. Inoltre, consulta la sezione [casi d’uso e metodi](#upload-methods-comparison)

* [API di caricamento risorse](developer-reference-material-apis.md#asset-upload): Utilizza uno script o uno strumento di caricamento personalizzato che sfrutta le API per aggiungere ulteriore gestione delle risorse (ad esempio, tradurre metadati o rinominare file), se necessario.
* [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Utile per i creativi professionisti e gli esperti di marketing che caricano le risorse dal loro file system locale. Utilizzalo per caricare le cartelle nidificate disponibili localmente.
* [Strumento per l’acquisizione in blocco](#asset-bulk-ingestor): Da utilizzare per l’acquisizione di grandi quantità di risorse occasionalmente o inizialmente durante la distribuzione [!DNL Experience Manager].

### Strumento per l’acquisizione collettiva delle risorse {#asset-bulk-ingestor}

Lo strumento viene fornito solo al gruppo di amministratori per utilizzare per l’acquisizione su larga scala di risorse dai datastore di Azure o S3. Guarda un video dettagliato sulla configurazione e l’acquisizione.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

Per configurare lo strumento, segui questi passaggi:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Importazione in blocco]**. Seleziona la **[!UICONTROL Crea]** opzione .

![Configurazione dell&#39;importatore di massa](assets/bulk-import-config.png)

1. On **[!UICONTROL configurazione di importazione in serie]** fornire i valori richiesti e quindi selezionare **[!UICONTROL Salva]**.

   * [!UICONTROL Titolo]: Titolo descrittivo.
   * [!UICONTROL Origine importazione]: Selezionare l&#39;origine dati applicabile.
   * [!UICONTROL Account di archiviazione di Azure]: Specifica il nome del [!DNL Azure] account di archiviazione.
   * [!UICONTROL Contenitore BLOB di Azure]: Fornisci [!DNL Azure] contenitore di archiviazione.
   * [!UICONTROL Chiave di accesso di Azure]: Fornisci la chiave di accesso a [!DNL Azure] conto.
   * [!UICONTROL Cartella di origine]: Questo filtro è in genere supportato dai provider di archiviazione cloud di Azure e AWS.
   * [!UICONTROL Filtra per dimensione minima]: Fornire la dimensione minima dei file delle risorse in MB.
   * [!UICONTROL Filtra per dimensione massima]: Fornire la dimensione massima dei file delle risorse in MB.
   * [!UICONTROL Escludi tipi di MIME]: Elenco di tipi MIME separati da virgole da escludere dall’acquisizione. Esempio, `image/jpeg, image/.*, video/mp4`. Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).
   * [!UICONTROL Includi tipi di mime]: Elenco di tipi MIME separati da virgole da includere nell’acquisizione. Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).
   * [!UICONTROL Modalità importazione]: Selezionare Ignora, Sostituisci o Crea versione. La modalità Salta è l’impostazione predefinita e in questa modalità l’utente che esegue l’acquisizione salta per importare una risorsa, se esiste già. Vedere il significato di [opzioni di sostituzione e creazione della versione](#handling-upload-existing-file).
   * [!UICONTROL Cartella di destinazione delle risorse]: Importa la cartella in DAM in cui devono essere importate le risorse. Esempio, `/content/dam/imported_assets`
   * [!UICONTROL File metadati]: Il file di metadati da importare, fornito in formato CSV. Fornisci questo file CSV nella posizione del BLOB di origine e fai riferimento al percorso nella configurazione dello strumento di inserimento in blocco.

1. Puoi eliminare, modificare, eseguire ed eseguire ulteriori operazioni con le configurazioni di acquisizione create. Quando selezioni una configurazione per l’acquisizione in serie, nella barra degli strumenti sono disponibili le seguenti opzioni:

   * [!UICONTROL Modifica]: Modifica la configurazione selezionata.
   * [!UICONTROL Elimina]: Elimina la configurazione selezionata.
   * [!UICONTROL Controlla]: Convalida la connessione al datastore.
   * [!UICONTROL Prova a secco]: Richiama un&#39;esecuzione di test dell&#39;acquisizione in massa.
   * [!UICONTROL Esegui]: Esegui la configurazione selezionata.
   * [!UICONTROL Interrompi]: Termina una configurazione attiva.
   * [!UICONTROL Pianificazione]: Impostare una pianificazione una tantum o ricorrente per l’acquisizione delle risorse.
   * [!UICONTROL Stato del processo]: Visualizza lo stato della configurazione quando viene utilizzata in un processo di importazione in corso o utilizzata per un processo completato.
   * [!UICONTROL Cronologia processi]: Istanze precedenti del processo.
   * [!UICONTROL Visualizzare le risorse]: Visualizza la cartella di destinazione se esiste.

   ![Opzioni della barra degli strumenti per le configurazioni di inserimento](assets/bulk-ingest-toolbar-options.png)

Per pianificare un’importazione in serie una tantum o ricorrente, effettua le seguenti operazioni:

1. Crea una configurazione di importazione in serie.
1. Seleziona la configurazione e seleziona **[!UICONTROL Pianificazione]** dalla barra degli strumenti.
1. Imposta un’acquisizione una tantum o pianifica una pianificazione oraria, giornaliera o settimanale. Fai clic su **[!UICONTROL Invia]**.

   ![Pianificare il processo di inserimento in blocco](assets/bulk-ingest-schedule1.png)

## Caricare risorse utilizzando client desktop {#upload-assets-desktop-clients}

Oltre all&#39;interfaccia utente del browser web, [!DNL Experience Manager] supporta altri client sul desktop. Forniscono anche un’esperienza di caricamento senza la necessità di andare al browser web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) consente l’accesso alle risorse da [!DNL Experience Manager] nelle applicazioni desktop Adobe Photoshop, Adobe Illustrator e Adobe InDesign. È possibile caricare il documento attualmente aperto in [!DNL Experience Manager] direttamente dall’interfaccia utente di Adobe Asset Link all’interno di queste applicazioni desktop.
* [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) semplifica l’utilizzo delle risorse sul desktop, indipendentemente dal tipo di file o dall’applicazione nativa che le gestisce. È particolarmente utile caricare file in gerarchie di cartelle nidificate dal file system locale, in quanto il caricamento del browser supporta solo il caricamento di elenchi di file flat.

## Elabora le risorse quando vengono caricate {#process-when-uploaded}

Per eseguire un’elaborazione aggiuntiva sulle risorse caricate, puoi applicare i profili di elaborazione sulle cartelle di caricamento. I profili sono disponibili nella **[!UICONTROL Proprietà]** pagina di una cartella [!DNL Assets]. Una risorsa digitale senza estensione o con estensione errata non viene elaborata come desiderato. Ad esempio, durante il caricamento di tali risorse, non si verifica nulla o un profilo di elaborazione errato può essere applicato alla risorsa. Gli utenti possono comunque memorizzare i file binari nel DAM.

![Proprietà di una cartella di risorse con opzioni per aggiungere un profilo di elaborazione](assets/assets-folder-properties.png)

Sono disponibili le seguenti schede:

* [Profili metadati](metadata-profiles.md) consente di applicare le proprietà metadati predefinite alle risorse caricate in quella cartella.
* [Profili di elaborazione](asset-microservices-configure-and-use.md) consente di generare più rendering di quanti siano possibili per impostazione predefinita.

Inoltre, se [!DNL Dynamic Media] è abilitata nella distribuzione, sono disponibili le seguenti schede:

* [[!DNL Dynamic Media] Profili immagine](dynamic-media/image-profiles.md) consente di applicare ritaglio specifico (**[!UICONTROL Ritaglio avanzato]** e ritaglio pixel) e la configurazione di nitidezza per le risorse caricate.
* [[!DNL Dynamic Media] Profili video](dynamic-media/video-profiles.md) consente di applicare profili di codifica video specifici (risoluzione, formato, parametri).

>[!NOTE]
>
>[!DNL Dynamic Media] le operazioni di ritaglio e altre operazioni sulle risorse non sono distruttive, ovvero le operazioni non modificano l’originale caricato. Fornisce invece parametri per ritagliare o trasformare le risorse durante la loro distribuzione.

Per le cartelle a cui è assegnato un profilo di elaborazione, il nome del profilo viene visualizzato sulla miniatura nella vista a schede. Nella vista a elenco, il nome del profilo viene visualizzato nella **[!UICONTROL Profilo di elaborazione]** colonna.

## Caricare o acquisire risorse tramite API {#upload-using-apis}

Dettagli tecnici delle API e del protocollo di caricamento, nonché collegamenti all’SDK open-source e ai client di esempio sono forniti in [caricamento risorsa](developer-reference-material-apis.md#asset-upload) sezione del riferimento per sviluppatori.

## Suggerimenti, best practice e limitazioni {#tips-limitations}

* Il caricamento binario diretto è un nuovo metodo per caricare le risorse. È supportato per impostazione predefinita dalle funzionalità del prodotto e dai client, come [!DNL Experience Manager] interfaccia utente, [!DNL Adobe Asset Link]e [!DNL Experience Manager] app desktop. Qualsiasi codice personalizzato personalizzato personalizzato o esteso dai team tecnici dei clienti deve utilizzare le nuove API e i nuovi protocolli di caricamento.

* Adobe consiglia di aggiungere non più di 1000 risorse in ogni cartella in [!DNL Experience Manager Assets]. Anche se è possibile aggiungere più risorse a una cartella, è possibile che si verifichino problemi di prestazioni, ad esempio una navigazione più lenta a tali cartelle.

* Quando selezioni **[!UICONTROL Sostituisci]** in [!UICONTROL Conflitto tra nomi] L’ID della risorsa viene rigenerato per la nuova risorsa. Questo ID è diverso dall’ID della risorsa precedente. Se [Informazioni sulle risorse](/help/assets/assets-insights.md) è abilitato per tenere traccia delle impression o dei clic con [!DNL Adobe Analytics], l’ID risorsa rigenerato invalida i dati acquisiti per la risorsa su [!DNL Analytics].

* Alcuni metodi di caricamento non impediscono il caricamento di risorse con [caratteri proibiti](#filename-handling) nei nomi dei file. I caratteri vengono sostituiti con `-` simbolo.

* Il caricamento delle risorse tramite il browser supporta solo elenchi di file semplici e non gerarchie di cartelle nidificate. Per caricare tutte le risorse all’interno di una cartella nidificata, considera l’utilizzo di [app desktop](#upload-assets-desktop-clients).

* Il metodo di importazione in blocco importa l’intera struttura di cartelle esistente sull’origine dati. Tuttavia, vengono create solo le cartelle non vuote in [!DNL Experience Manager].


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

>[!MORELIKETHIS]
>
>* App desktop [[!DNL Adobe Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Informazioni [!DNL Adobe Asset Link]](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentazione](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Riferimento tecnico per il caricamento delle risorse](developer-reference-material-apis.md#asset-upload)

