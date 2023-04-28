---
title: Aggiungi le risorse digitali a [!DNL Adobe Experience Manager].
description: Aggiungi le risorse digitali a [!DNL Adobe Experience Manager] come [!DNL Cloud Service].
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '3094'
ht-degree: 1%

---

# Aggiungi risorse digitali a [!DNL Adobe Experience Manager] come [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] accetta molti tipi di risorse digitali da molte sorgenti. Memorizza i binari e le rappresentazioni create, può eseguire l’elaborazione delle risorse utilizzando un’ampia gamma di flussi di lavoro e [!DNL Adobe Sensei] servizi, consente la distribuzione attraverso molti canali su più superfici.

[!DNL Adobe Experience Manager] arricchisce il contenuto binario dei file digitali caricati con metadati avanzati, tag avanzati, rappresentazioni e altri servizi di Digital Asset Management (DAM). È possibile caricare vari tipi di file, ad esempio immagini, documenti e file immagine non elaborati, dalla cartella locale o da un&#39;unità di rete a [!DNL Experience Manager Assets].

Oltre al caricamento del browser più comunemente utilizzato, altri metodi per aggiungere risorse al [!DNL Experience Manager] esiste un archivio, inclusi i client desktop, come Adobe Asset Link o [!DNL Experience Manager] script per app desktop, caricamento e acquisizione che i clienti creerebbero e integrazioni automatizzate di acquisizione aggiunte come [!DNL Experience Manager] estensioni.

Mentre puoi caricare e gestire qualsiasi file binario in [!DNL Experience Manager], i formati di file più comunemente utilizzati supportano servizi aggiuntivi, come l’estrazione dei metadati o la generazione di anteprime/rendering. Fai riferimento a [formati di file supportati](file-format-support.md) per i dettagli.

Puoi anche scegliere di eseguire un’ulteriore elaborazione sulle risorse caricate. È possibile configurare diversi profili di elaborazione delle risorse nella cartella in cui vengono caricate le risorse per aggiungere metadati, rappresentazioni o servizi di elaborazione delle immagini specifici. Vedi [elabora le risorse quando vengono caricate](#process-when-uploaded).

[!DNL Assets] fornisci i seguenti metodi di caricamento. L’Adobe consiglia di comprendere il caso d’uso e l’applicabilità di un’opzione di caricamento prima di utilizzarla.

| Metodo di caricamento | Quando utilizzare? | Persona principale |
|---------------------|----------------|-----------------|
| [Interfaccia utente della console Assets](#upload-assets) | Caricamento occasionale, facilità di pressione e trascinamento, caricamento del finder. Non utilizzare per caricare un numero elevato di risorse. | Tutti gli utenti |
| [Carica API](#upload-using-apis) | Per decisioni dinamiche durante il caricamento. | Sviluppatore |
| [[!DNL Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Acquisizione di risorse a basso volume, ma non per la migrazione. | Amministratore, addetto al marketing |
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

Per caricare un file (o più file), puoi selezionarlo sul desktop e trascinarlo sull’interfaccia utente (browser web) nella cartella di destinazione. In alternativa, puoi avviare il caricamento dall’interfaccia utente di .

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

   >[!NOTE]
   >
   >L’opzione per sostituire le risorse non è disponibile se la risorsa è bloccata o estratta.

* Crea un&#39;altra versione: Nella directory archivio viene creata una nuova versione della risorsa esistente. È possibile visualizzare le due versioni nel [!UICONTROL Timeline] e può, se necessario, ripristinare la versione esistente precedente.
* Mantieni entrambi: Se scegli di mantenere entrambe le risorse, la nuova risorsa viene rinominata.

Per mantenere la risorsa duplicata in [!DNL Assets], fai clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, fai clic su **[!UICONTROL Elimina]**.

### Gestione dei nomi dei file e caratteri non consentiti {#filename-handling}

[!DNL Experience Manager Assets] impedisce il caricamento di risorse con i caratteri non consentiti nei nomi dei file. Se tenti di caricare una risorsa con nomi di file contenenti un carattere non consentito o più, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento finché non rimuovi questi caratteri o li carichi con un nome consentito.

Per soddisfare convenzioni di denominazione dei file specifiche per la tua organizzazione, la [!UICONTROL Caricare risorse] La finestra di dialogo consente di specificare nomi lunghi per i file caricati. I seguenti caratteri (elenco separato da spazi) non sono supportati:

* Caratteri non validi per il nome della risorsa: `* / : [ \\ ] | # % { } ? &`
* Caratteri non validi per il nome della cartella di risorse: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Caricamento in blocco delle risorse {#bulk-upload}

Il gestore di risorse in blocco può gestire in modo efficiente un numero molto elevato di risorse. Tuttavia, un’acquisizione su larga scala non è solo un’immagine di file ampia o una migrazione casuale. Affinché un’acquisizione su larga scala sia un progetto significativo per il tuo scopo aziendale ed efficiente, pianifica la migrazione e cura l’organizzazione delle risorse. Tutte le acquisizioni sono diverse, quindi invece di generalizzare, sono fattori nella composizione dell’archivio e nelle esigenze aziendali più articolate. Di seguito sono riportati alcuni suggerimenti generali per pianificare ed eseguire un’acquisizione in blocco:

* Cura risorse: Rimuovi le risorse non necessarie nel DAM. È consigliabile rimuovere le risorse inutilizzate, obsolete o duplicate. Questo consente di ridurre i dati trasferiti e le risorse acquisite, con conseguente maggiore velocità di assimilazione.
* Organizzare le risorse: È consigliabile organizzare il contenuto in un ordine logico, ad esempio per dimensione del file, formato del file, caso d’uso o priorità. In generale, i file complessi di grandi dimensioni richiedono una maggiore elaborazione. Puoi anche considerare l’acquisizione separata di file di grandi dimensioni utilizzando l’opzione di filtro delle dimensioni del file (descritta di seguito).
* Acquisizioni scaglioni: È consigliabile suddividere l’acquisizione in più progetti di inserimento in blocco. Questo ti consente di visualizzare il contenuto prima e di aggiornarlo come necessario. Ad esempio, puoi acquisire risorse ad alta intensità di elaborazione nelle ore non di picco o gradualmente in più blocchi. Tuttavia, puoi acquisire risorse più piccole e semplici che non richiedono molta elaborazione contemporaneamente.

Per caricare un numero maggiore di file, utilizza uno dei seguenti approcci. Inoltre, consulta la sezione [casi d’uso e metodi](#upload-methods-comparison)

* [API di caricamento risorse](developer-reference-material-apis.md#asset-upload): Utilizza uno script o uno strumento di caricamento personalizzato che sfrutta le API per aggiungere ulteriore gestione delle risorse (ad esempio, tradurre metadati o rinominare file), se necessario.
* [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Utile per i creativi professionisti e gli esperti di marketing che caricano le risorse dal loro file system locale. Utilizzalo per caricare le cartelle nidificate disponibili localmente.
* [Strumento per l’acquisizione in blocco](#asset-bulk-ingestor): Da utilizzare per l’acquisizione di grandi quantità di risorse occasionalmente o inizialmente durante la distribuzione [!DNL Experience Manager].

### Strumento di importazione in blocco risorsa {#asset-bulk-ingestor}

Lo strumento viene fornito solo al gruppo di amministratori per utilizzare per l’inserimento su larga scala di risorse dai datastore di Azure o S3. Guarda un video dettagliato sulla configurazione e l’acquisizione.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

L’immagine seguente illustra le varie fasi durante il caricamento delle risorse in Experience Manager da un archivio dati:

![Strumento di inserimento in blocco](assets/bulk-ingestion.png)

**Prerequisiti**

Per utilizzare questa funzione è necessario un account di archiviazione esterno o un bucket da Azure o AWS.

>[!NOTE]
>
>Crea il contenitore o il bucket dell’account di archiviazione come privato e accetta connessioni solo da richieste autorizzate. Tuttavia, non sono supportate ulteriori restrizioni sulle connessioni di rete in ingresso.

>[!NOTE]
>
>Gli account di archiviazione esterni possono avere regole di nome file/cartella diverse da quelle dello strumento di importazione in blocco. Vedi [Gestione dei nomi dei file durante l’importazione in serie](#filename-handling-bulkimport) per ulteriori dettagli sui nomi non consentiti/escape.


### Configura lo strumento di importazione in blocco {#configure-bulk-ingestor-tool}

Per configurare lo strumento di importazione in blocco, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Importazione in blocco]**. Seleziona la **[!UICONTROL Crea]** opzione .

1. Specifica un titolo per la configurazione di importazione in serie nella **[!UICONTROL Titolo]** campo .

1. Seleziona il tipo di origine dati dal **[!UICONTROL Origine importazione]** elenco a discesa.

1. Immetti i valori per creare una connessione con l’origine dati. Ad esempio, se selezioni **Archiviazione BLOB di Azure** come origine dati, specifica i valori per l’account di archiviazione Azure, il contenitore BLOB di Azure e la chiave di accesso di Azure.

1. Seleziona la modalità di autenticazione desiderata dall’elenco a discesa. **Chiave di accesso di Azure** fornisce accesso completo all’account di archiviazione di Azure, mentre **Token SAS di Azure** consente all’amministratore di limitare le funzionalità del token utilizzando le autorizzazioni e i criteri di scadenza.

1. Fornisci il nome della cartella principale che contiene le risorse nell’origine dati in **[!UICONTROL Cartella di origine]** campo .

1. (Facoltativo) Immetti la dimensione minima dei file in MB per includerli nel processo di acquisizione nel **[!UICONTROL Filtra per dimensione minima]** campo .

1. (Facoltativo) Immetti la dimensione massima dei file in MB per includerli nel processo di acquisizione nel **[!UICONTROL Filtra per dimensione massima]** campo .

1. (Facoltativo) Specifica un elenco separato da virgole di tipi MIME da escludere dall’acquisizione nel **[!UICONTROL Escludere i tipi MIME]** campo . Ad esempio, `image/jpeg, image/.*, video/mp4`. Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).

1. Specifica l’elenco di tipi MIME separati da virgola da includere dall’acquisizione in **[!UICONTROL Includi tipi MIME]** campo . Vedi [tutti i formati di file supportati](/help/assets/file-format-support.md).

1. Seleziona la **[!UICONTROL Elimina il file sorgente dopo l’importazione]** opzione per eliminare i file originali dall&#39;archivio dati di origine dopo l&#39;importazione in [!DNL Experience Manager].

1. Seleziona la **[!UICONTROL Modalità importazione]**. Seleziona **Salta**, **Sostituisci** oppure **Crea versione**. La modalità Salta è l’impostazione predefinita e in questa modalità l’utente che esegue l’acquisizione salta per importare una risorsa, se esiste già. Vedere il significato di [opzioni di sostituzione e creazione della versione](#handling-upload-existing-file).

1. Specifica un percorso per definire una posizione in DAM in cui le risorse devono essere importate tramite **[!UICONTROL Cartella di destinazione delle risorse]** campo . Esempio: `/content/dam/imported_assets`.

1. (Facoltativo) Specifica il file di metadati da importare, fornito in formato CSV, nel **[!UICONTROL File metadati]** campo . Specifica il file CSV nella posizione del BLOB di origine e fai riferimento al percorso durante la configurazione dello strumento di importazione in blocco. Il formato di file CSV a cui si fa riferimento in questo campo è lo stesso del formato di file CSV quando [Importare ed esportare in blocco i metadati delle risorse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/metadata-import-export.html). Se selezioni la **Elimina il file sorgente dopo l’importazione** , filtra i file CSV utilizzando **Escludi** o **Includi tipo MIME** o **Filtra per percorso/file** campi. Puoi usare un’espressione regolare per filtrare i file CSV in questi campi.

1. Fai clic su **[!UICONTROL Salva]** per salvare la configurazione.

### Gestire la configurazione dello strumento di importazione in blocco {#manage-bulk-import-configuration}

Dopo aver creato la configurazione dello strumento di importazione in blocco, puoi eseguire attività per valutare la configurazione prima di acquisire in massa le risorse nell’istanza di Experience Manager. Seleziona la configurazione disponibile in **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Importazione in blocco]** per visualizzare le opzioni disponibili per gestire la configurazione dello strumento di importazione in serie.

### Modificare la configurazione {#edit-configuration}

Seleziona la configurazione e fai clic su **[!UICONTROL Modifica]** per modificare i dettagli di configurazione. Non è possibile modificare il titolo della configurazione e l’origine dati di importazione durante l’operazione di modifica.

### Elimina la configurazione {#delete-configuration}

Seleziona la configurazione e fai clic su **[!UICONTROL Elimina]** per eliminare la configurazione di importazione in blocco.

### Convalida della connessione all’origine dati {#validate-connection}

Seleziona la configurazione e fai clic su **[!UICONTROL check]** per convalidare la connessione all’origine dati. In caso di connessione riuscita, in Experience Manager viene visualizzato il seguente messaggio:

![Messaggio di successo Importazione in blocco](assets/bulk-import-success-message.png)

### Richiamare un&#39;esecuzione di test per il processo di importazione in serie {#invoke-test-run-bulk-import}

Seleziona la configurazione e fai clic su **[!UICONTROL Prova a secco]** per richiamare un&#39;esecuzione di test per il processo di importazione in serie. Nell&#39;Experience Manager vengono visualizzati i seguenti dettagli sul processo di importazione in blocco:

![Risultato esecuzione di prova](assets/dry-assets-result.png)

### Gestione dei nomi dei file durante l’importazione in serie {#filename-handling-bulkimport}

Quando si importano in massa risorse o cartelle, [!DNL Experience Manager Assets] importa l’intera struttura di ciò che esiste nella fonte di importazione. [!DNL Experience Manager] segue le regole integrate per i caratteri speciali nei nomi delle risorse e delle cartelle, pertanto questi nomi di file devono essere eliminati. Sia per il nome della cartella che per il nome della risorsa, il titolo definito dall’utente rimane invariato e viene memorizzato in `jcr:title`.

Durante l&#39;importazione alla rinfusa, [!DNL Experience Manager] cerca le cartelle esistenti per evitare di reimportare le risorse e le cartelle e verifica anche le regole di pulizia applicate nella cartella padre in cui avviene l’importazione. Se le regole di pulizia vengono applicate nella cartella padre, le stesse regole vengono applicate all&#39;origine di importazione. Per la nuova importazione, vengono applicate le seguenti regole di pulizia per gestire i nomi file delle risorse e delle cartelle.

**Nomi non consentiti nell&#39;importazione in blocco**

I seguenti caratteri non sono consentiti nei nomi di file e cartelle:

* Caratteri di controllo e uso privato (da 0x00 a 0x1F, \u0081, \uE000)
* Nomi di file o cartelle con punto (.)

I file o le cartelle con nomi corrispondenti a queste condizioni vengono ignorati durante il processo di importazione e contrassegnati come non riusciti.

**Gestione del nome della risorsa nell’importazione in blocco**

Per i nomi dei file delle risorse, il nome e il percorso JCR vengono bonificati utilizzando l’API: `JcrUtil.escapeIllegalJcrChars`.

* I caratteri Unicode non vengono modificati
* Sostituisci i caratteri speciali con il relativo codice di escape URL, ad esempio: `new%asset.png` è stato aggiornato a `new%25asset.png`:

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

**Gestione del nome della cartella nell’importazione in serie**

Per i nomi dei file delle cartelle, il nome e il percorso JCR vengono bonificati utilizzando l’API: `DamUtil.getSanitizedFolderName`.

* I caratteri maiuscoli vengono convertiti in lettere minuscole
* I caratteri Unicode non vengono modificati
* Sostituisci i caratteri speciali con il trattino (&#39;-&#39;), ad esempio: `new folder` è stato aggiornato a `new-folder`:

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

#### Pianificare un’importazione in serie una tantum o ricorrente {#schedule-bulk-import}

Per pianificare un’importazione in serie una tantum o ricorrente, effettua le seguenti operazioni:

1. Crea una configurazione di importazione in serie.
1. Seleziona la configurazione e seleziona **[!UICONTROL Pianificazione]** dalla barra degli strumenti.
1. Imposta un’acquisizione una tantum o pianifica una pianificazione oraria, giornaliera o settimanale. Fai clic su **[!UICONTROL Invia]**.

   ![Pianificare il processo di inserimento in blocco](assets/bulk-ingest-schedule1.png)


#### Visualizzare la cartella di destinazione delle risorse {#view-assets-target-folder}

Seleziona la configurazione e fai clic su **[!UICONTROL Visualizzare le risorse]** per visualizzare la posizione di destinazione delle risorse in cui vengono importate le risorse dopo l’esecuzione del processo di importazione in blocco.

#### Esegui lo strumento di importazione in blocco {#run-bulk-import-tool}

Dopo [configurazione dello strumento di importazione in blocco](#configure-bulk-ingestor-tool) e facoltativamente [gestione della configurazione dello strumento di importazione in blocco](#manage-bulk-import-configuration), puoi eseguire il processo di configurazione per avviare l’acquisizione in massa delle risorse.

Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Importazione in blocco]**, seleziona [Configurazione dell’importazione in blocco](#configure-bulk-ingestor-tool) e fai clic su **[!UICONTROL Esegui]** per avviare il processo di importazione in blocco. Fai clic su **[!UICONTROL Esegui]** di nuovo per confermare.

L&#39;Experience Manager aggiorna lo stato del processo a **Elaborazione** e **Completato** una volta completato con successo il lavoro. Fai clic su **Visualizzare le risorse** per visualizzare le risorse importate in Experience Manager.

Quando il processo è in corso, puoi anche selezionare la configurazione e fare clic su **Interrompi** per interrompere il processo di inserimento in blocco. Fai clic su **Esegui** per riprendere il processo. Puoi anche fare clic su **Prova a secco** per conoscere i dettagli delle risorse che sono ancora in attesa di importazione.

#### Gestisci processi dopo l&#39;esecuzione {#manage-jobs-after-execution}

L’Experience Manager ti consente di visualizzare la cronologia dei processi di importazione in blocco. La cronologia processo include lo stato del processo, il creatore del processo, i registri, insieme ad altri dettagli quali la data e l&#39;ora di inizio, la data e l&#39;ora di creazione e la data e l&#39;ora di fine.

Per accedere alla cronologia dei processi per una configurazione, seleziona la configurazione e fai clic su **[!UICONTROL Cronologia processi]**. Seleziona un processo e fai clic su **Apri**.

![Pianificare il processo di inserimento in blocco](assets/job-history-bulk-import.png)

Nell&#39;Experience Manager viene visualizzata la cronologia dei processi. Nella pagina della cronologia dei processi di importazione in blocco è inoltre possibile fare clic su **Elimina** per eliminare quel processo per la configurazione di importazione in blocco.


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

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
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
>
>* [[!DNL Adobe Experience Manager] App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it)
>* [Informazioni su [!DNL Adobe Asset Link]](https://www.adobe.com/it/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentazione](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [Riferimento tecnico per il caricamento delle risorse](developer-reference-material-apis.md#asset-upload)

