---
title: Aggiungi le risorse digitali a  [!DNL Adobe Experience Manager].
description: Aggiungi le tue risorse digitali a  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Ingestion, Asset Management, Asset Processing, Upload
role: User, Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '3177'
ht-degree: 10%

---

# Aggiungi risorse digitali a [!DNL Adobe Experience Manager] come [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] accetta molti tipi di risorse digitali da diverse origini. Memorizza i binari e le rappresentazioni create, può eseguire l&#39;elaborazione delle risorse utilizzando vari flussi di lavoro e servizi [!DNL Adobe AI], consente la distribuzione attraverso molti canali su molte superfici.

[!DNL Adobe Experience Manager] arricchisce il contenuto binario dei file digitali caricati con metadati avanzati, tag avanzati, rappresentazioni e altri servizi di gestione delle risorse digitali (DAM). È possibile caricare vari tipi di file, ad esempio immagini, documenti e file di immagini raw, dalla cartella locale o da un&#39;unità di rete in [!DNL Experience Manager Assets].

Oltre al caricamento del browser più comunemente utilizzato, esistono altri metodi per aggiungere risorse all&#39;archivio [!DNL Experience Manager]. Questi altri metodi includono client desktop, come Adobe Asset Link o l&#39;app desktop [!DNL Experience Manager], script di caricamento e acquisizione che verrebbero creati dai clienti e integrazioni di acquisizione automatizzate aggiunte come estensioni [!DNL Experience Manager].

Anche se è possibile caricare e gestire qualsiasi file binario in [!DNL Experience Manager], i formati di file più comunemente utilizzati supportano servizi aggiuntivi, come l&#39;estrazione di metadati o la generazione di anteprime/rappresentazioni. Per ulteriori informazioni, vedere [formati di file supportati](file-format-support.md).

Puoi anche scegliere di eseguire un’elaborazione aggiuntiva sulle risorse caricate. Sulla cartella è possibile configurare diversi profili di elaborazione delle risorse, in cui vengono caricate le risorse, per aggiungere metadati specifici, rappresentazioni o servizi di elaborazione delle immagini. Consulta [Elabora risorse al momento del caricamento](#process-when-uploaded).

[!DNL Assets] forniscono i seguenti metodi di caricamento. Adobe consiglia di comprendere il caso d’uso e l’applicabilità di un’opzione di caricamento prima di utilizzarla.

| Metodo di caricamento | Quando utilizzare? | Persona primaria |
|---------------------|----------------|-----------------|
| [Interfaccia utente della console Assets](#upload-assets) | Caricamento occasionale, facilità di pressione e trascinamento, caricamento del mirino. Non utilizzare per caricare più risorse. | Tutti gli utenti |
| [Carica API](#upload-using-apis) | Per decisioni dinamiche durante il caricamento. | Sviluppatore |
| [[!DNL Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it) | Acquisizione di risorse di volume ridotto, ma non per la migrazione. | Amministratore, addetto marketing |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) | Utile quando creativi e addetti al marketing lavorano su risorse dalle app desktop [!DNL Creative Cloud] supportate. | Creative, addetto marketing |
| [Acquisizione in blocco risorse](#asset-bulk-ingestor) | Consigliato per migrazioni su larga scala e acquisizioni in blocco occasionali. Solo per gli archivi dati supportati. | Amministratore, sviluppatore |

## Caricare le risorse {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Select the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

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

Per caricare uno o più file, selezionali sul desktop e trascinali sull&#39;interfaccia utente (browser Web) nella cartella di destinazione. In alternativa, puoi avviare il caricamento dall’interfaccia utente.

>[!IMPORTANT]
>
>Gli Assets caricati in Experience Manager con un nome file superiore a 100 caratteri hanno un nome abbreviato quando vengono utilizzati in Dynamic Media.
>
>I primi 100 caratteri nel nome del file vengono utilizzati così come sono; tutti i caratteri rimanenti vengono sostituiti da una stringa alfanumerica. Questo metodo di ridenominazione garantisce un nome univoco quando la risorsa viene utilizzata in Dynamic Media. Inoltre, deve contenere la lunghezza massima consentita per il nome del file di risorse in Dynamic Media.


1. Nell&#39;interfaccia utente di [!DNL Assets], passa alla posizione in cui desideri aggiungere risorse digitali.
1. Per caricare le risorse, effettua una delle seguenti operazioni:

   * Sulla barra degli strumenti fare clic su **[!UICONTROL Crea]** > **[!UICONTROL File]**. Se necessario, puoi rinominare il file nella finestra di dialogo visualizzata.
   * In un browser che supporta HTML5, trascina le risorse direttamente sull&#39;interfaccia utente [!DNL Assets]. La finestra di dialogo per rinominare il file non viene visualizzata.

   ![crea_menu](assets/create_menu.png)

   Per selezionare più file, seleziona la chiave `Ctrl` o `Command` e seleziona le risorse nella finestra di dialogo del selettore file. Quando si utilizza un iPad, è possibile selezionare un solo file alla volta.

1. Per annullare un caricamento in corso, fare clic su Chiudi (`X`) accanto alla barra di avanzamento. Quando si annulla l&#39;operazione di caricamento, [!DNL Assets] elimina la parte parzialmente caricata della risorsa.
Se si annulla un&#39;operazione di caricamento prima che i file vengano caricati, [!DNL Assets] interrompe il caricamento del file corrente e aggiorna il contenuto. Tuttavia, i file già caricati non vengono eliminati.

1. La finestra di dialogo di avanzamento del caricamento in [!DNL Assets] visualizza il numero di file caricati correttamente e i file che non è stato possibile caricare.
Inoltre, nell&#39;interfaccia utente di [!DNL Assets] viene visualizzata la risorsa più recente caricata o la cartella creata per prima.

>[!NOTE]
>
>Per caricare le gerarchie di cartelle nidificate, vedi [risorse per il caricamento in blocco](#bulk-upload).

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

### Gestione dei caricamenti per le risorse esistenti {#handling-upload-existing-file}

Puoi caricare una risorsa con lo stesso percorso (stesso nome e stessa posizione) di una risorsa esistente. Tuttavia, viene visualizzata una finestra di dialogo di avviso con le seguenti opzioni:

* Sostituisci cespite esistente: se sostituisci un cespite esistente, i metadati del cespite ed eventuali modifiche precedenti (ad esempio, annotazioni e ritagli) apportate al cespite esistente vengono eliminati.

  >[!NOTE]
  >
  >L&#39;opzione per la sostituzione delle risorse non è disponibile se la risorsa è bloccata o estratta.

* Crea un’altra versione: viene creata una nuova versione della risorsa esistente nell’archivio. È possibile visualizzare le due versioni nella [!UICONTROL Timeline] e, se necessario, ripristinare la versione esistente precedente.
* Mantieni entrambe: se scegli di mantenere entrambe le risorse, la nuova risorsa viene rinominata.

Per mantenere la risorsa duplicata in [!DNL Assets], fai clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, fai clic su **[!UICONTROL Elimina]**.

### Gestione del nome file e caratteri non consentiti {#filename-handling}

[!DNL Experience Manager Assets] impedisce di caricare risorse con i caratteri non consentiti nei nomi dei file. Se tenti di caricare una risorsa i cui nomi contengono uno o più caratteri non consentiti, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento finché non rimuovi questi caratteri o non carichi con un nome consentito.

Per adattarsi a specifiche convenzioni di denominazione dei file per l&#39;organizzazione, la finestra di dialogo [!UICONTROL Carica Assets] consente di specificare nomi lunghi per i file caricati. I seguenti caratteri (separati da spazi) non sono supportati:

* Caratteri non validi per il nome della risorsa: `* / : [ \\ ] | # % { } ? &`
* Caratteri non validi per il nome della cartella di risorse: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricare risorse in blocco {#bulk-upload}

L’inserimento in blocco delle risorse può gestire molte risorse in modo efficiente. Tuttavia, un’acquisizione su larga scala non è solo un’immagine di file ampia o una migrazione casuale. Affinché l’acquisizione su larga scala sia un progetto significativo, efficiente e rispondente alle esigenze del tuo business, pianifica la migrazione e cura l’organizzazione delle risorse. Tutte le acquisizioni sono diverse, quindi, invece di generalizzare, influiscono sulla composizione dell’archivio e sulle esigenze aziendali specifiche. Di seguito sono riportati alcuni suggerimenti generali per pianificare ed eseguire un’acquisizione in blocco:

* Cura risorse: rimuovi le risorse non necessarie in DAM. È consigliabile rimuovere le risorse non utilizzate, obsolete o duplicate. Tale gestione riduce i dati trasferiti e le risorse acquisite, consentendo acquisizioni più rapide.
* Organizzare le risorse: è consigliabile organizzare il contenuto in un ordine logico, ad esempio in base alla dimensione del file, al formato del file, al caso d’uso o alla priorità. In generale, i file complessi di grandi dimensioni richiedono una maggiore elaborazione. Puoi anche prendere in considerazione l’acquisizione separata di file di grandi dimensioni utilizzando l’opzione di filtro delle dimensioni del file (descritta di seguito).
* Acquisizioni scaglionate: prendi in considerazione di suddividere l’acquisizione in più progetti di acquisizione in blocco. q ti consente di visualizzare il contenuto prima e di aggiornare l’acquisizione in base alle esigenze. Ad esempio, è possibile acquisire le risorse con elaborazione intensiva nelle ore non di picco o gradualmente in più blocchi. Tuttavia, puoi acquisire risorse più piccole e semplici che non richiedono molta elaborazione in un’unica operazione.

Per caricare un numero maggiore di file, utilizza uno dei seguenti approcci. Vedi anche [casi d&#39;uso e metodi](#upload-methods-comparison)

* [API per il caricamento di risorse](developer-reference-material-apis.md#asset-upload): se necessario, usa uno script o uno strumento di caricamento personalizzato che utilizza le API per aggiungere ulteriore gestione delle risorse (ad esempio, tradurre i metadati o rinominare i file).
* [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it): utile per professionisti del settore creativo e addetti al marketing che caricano risorse dal file system locale. Utilizzala per caricare le cartelle nidificate disponibili localmente.
* [Strumento di acquisizione in blocco](#asset-bulk-ingestor): utilizza per l&#39;acquisizione di grandi quantità di risorse occasionalmente o inizialmente durante la distribuzione di [!DNL Experience Manager].

### Strumento Importazione in blocco risorse {#asset-bulk-ingestor}

Lo strumento viene fornito solo al gruppo di amministratori da utilizzare per l’acquisizione su larga scala delle risorse dai datastore di Azure o S3. Guarda un video con la procedura dettagliata sulla configurazione e l’acquisizione.

>[!VIDEO](https://video.tv.adobe.com/v/341387/?captions=ita&quality=12&learn=on)

L’immagine seguente illustra le varie fasi di acquisizione delle risorse in Experience Manager da un archivio dati:

![Strumento di acquisizione in blocco](assets/bulk-ingestion.png)

**Prerequisiti**

Per utilizzare questa funzione è necessario un account di archiviazione esterno o un bucket di Azure o AWS.

>[!NOTE]
>
>Crea il contenitore o il bucket dell’account di archiviazione come privato e accetta connessioni solo da richieste autorizzate. Tuttavia, non sono supportate ulteriori restrizioni sulle connessioni di rete in ingresso.

>[!NOTE]
>
>Gli account di archiviazione esterna possono avere regole di nome file/cartella diverse dallo strumento Importazione in blocco. Consulta [Gestione dei nomi di file durante l&#39;importazione in blocco](#filename-handling-bulkimport) per ulteriori dettagli sui nomi non consentiti/con escape.


### Configurare lo strumento Importazione in blocco {#configure-bulk-ingestor-tool}

Per configurare lo strumento Importazione in blocco, effettuare le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Importazione in blocco]**. Selezionare l&#39;opzione **[!UICONTROL Crea]**.

1. Specifica un titolo per la configurazione dell&#39;importazione in blocco nel campo **[!UICONTROL Titolo]**.

1. Selezionare il tipo di origine dati dall&#39;elenco a discesa **[!UICONTROL Importa Source]**.

1. Immetti i valori per creare una connessione con l’origine dati. Se ad esempio si seleziona **Archiviazione BLOB di Azure** come origine dati, specificare i valori per l&#39;account di archiviazione di Azure, il contenitore BLOB di Azure e la chiave di accesso di Azure.

1. Seleziona la modalità di autenticazione richiesta dall’elenco a discesa. **Chiave di accesso Azure** fornisce l&#39;accesso completo all&#39;account di archiviazione Azure, mentre **Token SAS di Azure** consente all&#39;amministratore di limitare le funzionalità del token utilizzando le autorizzazioni e i criteri di scadenza.

1. Immetti il nome della cartella principale che contiene le risorse nell’origine dati nel campo **[!UICONTROL Cartella di origine]**.

1. (Facoltativo) Specifica la dimensione minima del file delle risorse in MB da includere nel processo di acquisizione nel campo **[!UICONTROL Filtra per dimensione minima]**.

1. (Facoltativo) Specifica la dimensione massima in MB del file delle risorse da includere nel processo di acquisizione del campo **[!UICONTROL Filtra per dimensione max]**.

1. (Facoltativo) Specifica un elenco separato da virgole di tipi MIME da escludere dall&#39;acquisizione nel campo **[!UICONTROL Escludi tipi MIME]**. Ad esempio, `image/jpeg, image/.*, video/mp4`. Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).

1. Specifica un elenco separato da virgole di tipi MIME da includere dall&#39;acquisizione nel campo **[!UICONTROL Includi tipi MIME]**. Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).

1. Selezionare l&#39;opzione **[!UICONTROL Elimina file di origine dopo l&#39;importazione]** per eliminare i file originali dall&#39;archivio dati di origine dopo l&#39;importazione in [!DNL Experience Manager].

1. Seleziona la **[!UICONTROL Modalità di importazione]**. Seleziona **Ignora**, **Sostituisci** o **Crea versione**. La modalità Ignora è l’impostazione predefinita e, in questa modalità, l’importazione di una risorsa viene ignorata se esiste già. Vedi il significato di [sostituisci e crea opzioni di versione](#handling-upload-existing-file).

1. Per definire una posizione in DAM in cui importare le risorse utilizzando il campo **[!UICONTROL Cartella risorse di destinazione]**, specifica un percorso. Esempio: `/content/dam/imported_assets`.

1. (Facoltativo) Specifica il file di metadati da importare, fornito in formato CSV, nel campo **[!UICONTROL File di metadati]**. Specifica il file CSV nel percorso del BLOB di origine e fai riferimento al percorso durante la configurazione dello strumento Importazione in blocco. Il formato di file CSV a cui si fa riferimento in questo campo è lo stesso del formato di file CSV quando si [Importa ed esporta metadati di risorse in blocco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/metadata-import-export.html?lang=it). Se si seleziona l&#39;opzione **Elimina file di origine dopo l&#39;importazione**, filtrare i file CSV utilizzando i campi **Escludi** o **Includi tipo MIME** o **Filtra per percorso/file**. È possibile utilizzare un’espressione regolare per filtrare i file CSV in questi campi.

1. Fai clic su **[!UICONTROL Salva]** per salvare la configurazione.

### Gestire la configurazione dello strumento Importazione in blocco {#manage-bulk-import-configuration}

Dopo aver creato la configurazione dello strumento Importazione in blocco, puoi eseguire attività per valutarla prima di acquisire in blocco le risorse nell’istanza di Experience Manager. Per visualizzare le opzioni disponibili per gestire la configurazione dello strumento Importazione in blocco, seleziona la configurazione disponibile in **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Importazione in blocco]**.

### Modificare la configurazione {#edit-configuration}

Per modificare i dettagli della configurazione, selezionare la configurazione, quindi fare clic su **[!UICONTROL Modifica]**. Non è possibile modificare il titolo della configurazione e l&#39;origine dati di importazione durante l&#39;operazione di modifica.

### Elimina la configurazione {#delete-configuration}

Seleziona la configurazione e fai clic su **[!UICONTROL Elimina]** per eliminare la configurazione dell&#39;importazione in blocco.

### Convalidare la connessione all’origine dati {#validate-connection}

Per convalidare la connessione all&#39;origine dati, selezionare la configurazione e quindi fare clic su **[!UICONTROL check]**. Se la connessione ha esito positivo, Experience Manager visualizza il seguente messaggio:

![Messaggio di completamento importazione in blocco](assets/bulk-import-success-message.png)

### Richiama un’esecuzione dei test per il processo di importazione in blocco {#invoke-test-run-bulk-import}

Selezionare la configurazione e fare clic su **[!UICONTROL Esegui prova]** per richiamare un&#39;esecuzione dei test per il processo di importazione in blocco. Experience Manager mostra i seguenti dettagli sul processo di importazione in blocco:

![Risultato esecuzione di prova](assets/dry-assets-result.png)

### Gestione dei nomi dei file durante l’importazione in blocco {#filename-handling-bulkimport}

Quando importi risorse o cartelle in blocco, [!DNL Experience Manager Assets] importa l’intera struttura di ciò che esiste nell’origine di importazione. [!DNL Experience Manager] segue le regole predefinite per i caratteri speciali nei nomi delle risorse e delle cartelle; pertanto, questi nomi di file devono essere bonificati. Sia per il nome della cartella che per quello della risorsa, il titolo definito dall’utente rimane invariato e viene memorizzato in `jcr:title`.

Durante l’importazione in blocco, [!DNL Experience Manager] cerca le cartelle esistenti per evitare di reimportare le risorse e le cartelle e verifica inoltre le regole di bonifica applicate nella cartella principale in cui avviene l’importazione. Se le regole di bonifica vengono applicate nella cartella principale, le stesse regole vengono applicate all’origine di importazione. Per le nuove importazioni, per gestire i nomi file di risorse e cartelle vengono applicate le seguenti regole di bonifica.

**Nomi non consentiti nell&#39;importazione in blocco**

I seguenti caratteri non sono consentiti nei nomi di file e cartelle:

* Caratteri di controllo e uso privato (da 0x00 a 0x1F, \u0081, \uE000)
* Nomi di file o cartelle che terminano con un punto (.)

I file o le cartelle con nomi corrispondenti a queste condizioni vengono ignorati durante il processo di importazione e contrassegnati come non riusciti.

**Gestione del nome della risorsa nell&#39;importazione in blocco**

Per i nomi file delle risorse, il nome e il percorso JCR vengono bonificati utilizzando l&#39;API `JcrUtil.escapeIllegalJcrChars`.

* I caratteri Unicode non vengono modificati
* Sostituire i caratteri speciali con il relativo codice di escape URL. Ad esempio, `new%asset.png` è aggiornato a `new%25asset.png`:

  ```
                  URL escape code   
  
  "               %22
  %               %25
  '               %27
  *               %2A
  /               %2F
  :               %3A
  [               %5B
  \n              %0A
  \r              %0D
  \t              %09
  ]               %5D
  |               %7C
  ```

**Gestione del nome della cartella nell&#39;importazione in blocco**

Per i nomi di file della cartella, il nome e il percorso JCR sono bonificati utilizzando l&#39;API `DamUtil.getSanitizedFolderName`.

* I caratteri maiuscoli vengono convertiti in minuscoli
* I caratteri Unicode non vengono modificati
* Sostituire i caratteri speciali con un trattino (&#39;-&#39;). Ad esempio, `new folder` è aggiornato a `new-folder`:

  ```
  "                           
  #                         
  %                           
  &                          
  *                           
  +                          
  .                           
  :                           
  ;                          
  ?                          
  [                           
  ]                           
  ^                         
  {                         
  }                         
  |                           
  /         It is used for split folder in cloud storage and is pre-handled, no conversion here.
  \         Not allowed in Azure, allowed in AWS.
  \t
  space     It is the space character.
  ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### Pianificare un’importazione in blocco una tantum o ricorrente {#schedule-bulk-import}

Per pianificare un’importazione in blocco una tantum o ricorrente, effettua le seguenti operazioni:

1. Crea una configurazione di importazione in blocco.
1. Seleziona la configurazione e seleziona **[!UICONTROL Pianifica]** dalla barra degli strumenti.
1. Imposta un’acquisizione una tantum o una pianificazione oraria, giornaliera o settimanale. Fai clic su **[!UICONTROL Invia]**.

   ![Pianifica processo di acquisizione in blocco](assets/bulk-ingest-schedule1.png)


#### Visualizzare la cartella di destinazione di Assets {#view-assets-target-folder}

Per visualizzare il percorso di destinazione di Assets in cui vengono importate le risorse dopo l&#39;esecuzione del processo di importazione in blocco, selezionare la configurazione e quindi fare clic su **[!UICONTROL Visualizza Assets]**.

#### Eseguire lo strumento Importazione in blocco {#run-bulk-import-tool}

Dopo la [configurazione dello strumento Importazione in blocco](#configure-bulk-ingestor-tool) e, facoltativamente, la [gestione della configurazione dello strumento Importazione in blocco](#manage-bulk-import-configuration), è possibile eseguire il processo di configurazione per avviare l&#39;acquisizione in blocco delle risorse.

Per avviare il processo di importazione in blocco, passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Importazione in blocco]**, selezionare la [Configurazione importazione in blocco](#configure-bulk-ingestor-tool), quindi fare clic su **[!UICONTROL Esegui]**. Fai di nuovo clic su **[!UICONTROL Esegui]** per confermare.

Experience Manager aggiorna lo stato del processo a **Elaborazione** e a **Completata** al completamento del processo. Per visualizzare le risorse importate in Experience Manager, fai clic su **Visualizza Assets**.

Quando il processo è in corso, puoi anche selezionare la configurazione e fare clic su **Interrompi** per interrompere il processo di acquisizione in blocco. Fai di nuovo clic su **Esegui** per riprendere il processo. È inoltre possibile fare clic su **Dry Run** per conoscere i dettagli delle risorse ancora in attesa di importazione.

#### Gestisci processi dopo l&#39;esecuzione {#manage-jobs-after-execution}

Experience Manager consente di visualizzare la cronologia dei processi di importazione in blocco. La cronologia processo include lo stato del processo, l&#39;autore del processo, i registri e altri dettagli quali la data e l&#39;ora di inizio, la data e l&#39;ora di creazione e la data e l&#39;ora di fine.

Per accedere alla cronologia dei processi per una configurazione, selezionare la configurazione e fare clic su **[!UICONTROL Cronologia processi]**. Selezionare un processo e fare clic su **Apri**.

![Pianifica processo di acquisizione in blocco](assets/job-history-bulk-import.png)

In Experience Manager viene visualizzata la cronologia dei processi. Nella pagina della cronologia dei processi di importazione in blocco è inoltre possibile fare clic su **Elimina** per eliminare il processo per la configurazione dell&#39;importazione in blocco.


## Caricare risorse tramite client desktop {#upload-assets-desktop-clients}

Oltre all&#39;interfaccia utente del browser Web, [!DNL Experience Manager] supporta altri client sul desktop. Inoltre, forniscono un’esperienza di caricamento senza dover passare al browser web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) fornisce l&#39;accesso alle risorse da [!DNL Experience Manager] nelle applicazioni desktop Adobe Photoshop, Adobe Illustrator e Adobe InDesign. Puoi caricare il documento attualmente aperto in [!DNL Experience Manager] direttamente dall&#39;interfaccia utente di Adobe Asset Link, direttamente da queste applicazioni desktop.
* L&#39;[[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it) semplifica l&#39;utilizzo delle risorse sul desktop, indipendentemente dal tipo di file o dall&#39;applicazione nativa che le gestisce. È utile caricare i file nelle gerarchie di cartelle nidificate dal file system locale, in quanto il caricamento del browser supporta solo il caricamento di elenchi di file flat.

## Elabora risorse quando caricate {#process-when-uploaded}

Per eseguire ulteriori elaborazioni sulle risorse caricate, puoi applicare i profili di elaborazione alle cartelle di caricamento. I profili sono disponibili nella pagina **[!UICONTROL Proprietà]** di una cartella in [!DNL Assets]. Una risorsa digitale senza un’estensione o con un’estensione non corretta non viene elaborata come desiderato. Ad esempio, quando carichi tali risorse, potrebbe non accadere nulla oppure potrebbe essere applicato un profilo di elaborazione errato. Gli utenti possono comunque memorizzare i file binari in DAM.

![Proprietà di una cartella di risorse con opzioni per aggiungere un profilo di elaborazione](assets/assets-folder-properties.png)

Sono disponibili le seguenti schede:

* [I profili metadati](metadata-profiles.md) ti consentono di applicare proprietà metadati predefinite alle risorse caricate in tale cartella.
* [I profili di elaborazione](asset-microservices-configure-and-use.md) ti consentono di generare più rappresentazioni di quante siano possibili per impostazione predefinita.

Inoltre, se [!DNL Dynamic Media] è abilitato nella distribuzione, sono disponibili le seguenti schede:

* [[!DNL Dynamic Media] I profili immagine](dynamic-media/image-profiles.md) ti consentono di applicare alle risorse caricate specifiche configurazioni di nitidezza e ritaglio (**[!UICONTROL Ritaglio avanzato]** e ritaglio pixel).
* [[!DNL Dynamic Media] Profili video](dynamic-media/video-profiles.md) consente di applicare profili di codifica video specifici (risoluzione, formato, parametri).

>[!NOTE]
>
>Il ritaglio di [!DNL Dynamic Media] e altre operazioni sulle risorse non sono distruttive, ovvero le operazioni non modificano l&#39;originale caricato. Al contrario, fornisce parametri da ritagliare o trasformare durante la distribuzione delle risorse.

Per le cartelle a cui è assegnato un profilo di elaborazione, il nome del profilo viene visualizzato sulla miniatura nella vista a schede. Nella vista a elenco, il nome del profilo viene visualizzato nella colonna **[!UICONTROL Profilo di elaborazione]**.

## Caricare o acquisire risorse tramite API {#upload-using-apis}

I dettagli tecnici delle API di caricamento e del protocollo, nonché i collegamenti a client open-source SDK e di esempio sono forniti nella sezione [asset upload](developer-reference-material-apis.md#asset-upload) della documentazione per sviluppatori.

## Suggerimenti, best practice e limitazioni {#tips-limitations}

* Il caricamento binario diretto è un nuovo metodo per caricare le risorse. È supportato per impostazione predefinita dalle funzionalità del prodotto e dai client, come l&#39;interfaccia utente [!DNL Experience Manager], [!DNL Adobe Asset Link] e l&#39;app desktop [!DNL Experience Manager]. Qualsiasi codice personalizzato personalizzato o esteso dai team tecnici del cliente deve utilizzare le nuove API e i nuovi protocolli di caricamento.

* [!DNL Experience Manager Assets] ora supporta le cartelle contenenti un numero elevato di risorse secondarie. Quando una cartella contiene più di 1000 elementi secondari diretti (risorse o sottocartelle), l’interfaccia utente di amministrazione utilizza un indice aggiornato in modo asincrono per elencare il contenuto della cartella. Di conseguenza, potrebbe verificarsi un breve ritardo nella visibilità delle cartelle e delle risorse appena create (in genere solo di pochi secondi) e, quando si apre tale cartella nella visualizzazione Amministratore, viene mostrato un banner per informare gli utenti finali di questo comportamento, che indica quanto segue: &quot;Questa directory contiene 1000+ elementi. I caricamenti e le creazioni di nuove cartelle potrebbero subire ritardi.&quot;

* Quando selezioni **[!UICONTROL Sostituisci]** nella finestra di dialogo [!UICONTROL Conflitto nome], l&#39;ID della risorsa viene rigenerato per la nuova risorsa. Questo ID è diverso da quello della risorsa precedente. Se [Assets Insights](/help/assets/assets-insights.md) è abilitato per monitorare impression o clic con [!DNL Adobe Analytics], l&#39;ID risorsa rigenerato invalida i dati acquisiti per la risorsa in [!DNL Analytics].

* Alcuni metodi di caricamento non impediscono il caricamento di risorse con [caratteri non consentiti](#filename-handling) nei nomi dei file. I caratteri vengono sostituiti con il simbolo `-`.

* Il caricamento delle risorse tramite il browser supporta solo elenchi di file sequenziali e non gerarchie di cartelle nidificate. Per caricare tutte le risorse all&#39;interno della cartella nidificata, prova a utilizzare l&#39;[app desktop](#upload-assets-desktop-clients).

* Il metodo di importazione in blocco importa l&#39;intera struttura di cartelle così come esiste nell&#39;origine dati. Tuttavia, in [!DNL Experience Manager] vengono create solo le cartelle non vuote.


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it)
>* [Informazioni su [!DNL Adobe Asset Link]](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] - documentazione](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Riferimento tecnico per il caricamento delle risorse](developer-reference-material-apis.md#asset-upload)
