---
title: Gestione di archivi di contenuti di grandi dimensioni
description: Questa sezione descrive la gestione di archivi di contenuti di grandi dimensioni
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
feature: Migration
role: Admin
source-git-commit: b729c07c78519cd9b6536a0dd142aa8ed01d2a22
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 7%

---

# Gestione di archivi di contenuti di grandi dimensioni {#handling-large-content-repositories}

## Panoramica {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestione di archivi di contenuti di grandi dimensioni"
>abstract="Per velocizzare in modo significativo le fasi di estrazione ed acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service, lo Strumento di trasferimento dei contenuti (CTT) può utilizzare AzCopy come fase di pre-copia opzionale. Una volta configurato questo passaggio preliminare, nella fase di estrazione AzCopy copia i BLOB da Amazon S3 o dall’archiviazione BLOB di Azure nell’archivio BLOB del set di migrazione. Nella fase di acquisizione AzCopy copia i BLOB dall’archivio BLOB del set di migrazione all’archivio BLOB di AEM as a Cloud Service di destinazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=it#setting-up-pre-copy-step" text="Guida introduttiva ad AzCopy come passaggio di pre-copia"

La copia di molti BLOB con lo strumento Content Transfer (CTT) può richiedere diversi giorni.
Per accelerare le fasi di estrazione e acquisizione dell&#39;attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service, CTT può utilizzare [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) come passaggio facoltativo di pre-copia. Questo passaggio di pre-copia può essere utilizzato quando l’istanza AEM di origine è configurata per utilizzare un archivio dati di Amazon S3, Azure Blob Storage o File Data Store. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione complete. Tuttavia, l’utilizzo della pre-copia per i successivi integratori non è consigliato (se la dimensione dell’integratore è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB dall’archivio dati di Amazon S3, Azure Blob Storage o File nell’archivio BLOB del set di migrazione. Nella fase di acquisizione AzCopy copia i BLOB dall’archivio BLOB del set di migrazione all’archivio BLOB di AEM as a Cloud Service di destinazione.

## Considerazioni importanti prima di iniziare {#important-considerations}

Prima di iniziare, segui la sezione seguente per comprendere le considerazioni importanti:

* A partire dalla versione 2.0.16 di CTT, la precopia viene impostata automaticamente quando il bundle viene installato. Inoltre, se la dimensione del set di migrazione è maggiore di 200 GB, il processo di estrazione utilizza automaticamente la funzione di precopia. Il file azcopy.config viene creato nella directory crx-quickstart/cloud-migration/. Non è necessario eseguire manualmente la precopia se si utilizza CTT versione 2.0.16 o successiva.

* La versione di Source AEM deve essere 6.3 - 6.5.

* L’archivio dati di Source AEM è configurato per l’utilizzo dell’archiviazione BLOB di Amazon S3 o Azure. Per ulteriori dettagli, vedere [Configurazione degli archivi nodi e dei dati in AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=it).

* Ogni set di migrazione copia l’intero archivio dati, pertanto è necessario utilizzare un solo set di migrazione.

* È necessario accedere per installare [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) nell&#39;istanza (o macchina virtuale) che esegue l&#39;istanza AEM di origine.

* La raccolta oggetti inattivi dell’archivio dati è stata eseguita nei sette giorni precedenti sull’origine. Per ulteriori dettagli, vedere [Raccolta di oggetti inattivi dell&#39;archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=it#data-store-garbage-collection).

### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare un archivio dati di archiviazione BLOB di Amazon S3 o Azure {#additional-considerations-amazons3-azure}

* Il trasferimento dei dati da Amazon S3 e dall’archiviazione BLOB di Azure comporta un costo. Il costo del trasferimento è relativo alla quantità totale di dati nel contenitore di archiviazione esistente (a prescindere dal fatto che si faccia riferimento o meno in AEM). Per ulteriori dettagli, vedi [Archiviazione BLOB di Azure](https://aws.amazon.com/s3/pricing/) e [Amazon S3](https://azure.microsoft.com/en-us/pricing/details/bandwidth/).

* È necessaria una coppia chiave di accesso e chiave segreta per il bucket Amazon S3 di origine esistente oppure un URI SAS per il contenitore Archiviazione BLOB di Azure di origine esistente (l’accesso in sola lettura va bene).

### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare l’archivio dati dei file {#additional-considerations-aem-instance-filedatastore}

* Il sistema locale deve disporre di uno spazio libero notevolmente maggiore di 1/256 delle dimensioni dell’archivio dati di origine. Ad esempio, se la dimensione dell&#39;archivio dati è di 3 terabyte, è necessario che nella cartella `crx-quickstart/cloud-migration` dell&#39;origine esista uno spazio libero maggiore di 11,72 GB affinché AzCopy funzioni. Il sistema di origine deve disporre almeno di 1 GB di spazio libero. È possibile ottenere spazio libero utilizzando il comando `df -h` sulle istanze Linux® e il comando dir nelle istanze Windows.

* Ogni volta che l’estrazione viene eseguita con AzCopy abilitato, l’intero archivio dati del file viene appiattito e copiato nel contenitore di migrazione cloud. Se il set di migrazione è più piccolo delle dimensioni dell’archivio dati, l’estrazione AzCopy non è l’approccio ottimale.

* Una volta che AzCopy è stato utilizzato per copiare sull’archivio dati esistente, disattivarlo per le estrazioni delta o integrative.

## Impostazione dell’utilizzo di AzCopy come passaggio di pre-copia {#setting-up-pre-copy-step}

>[!NOTE]
>A partire dalla versione 2.0.16 di CTT, la precopia viene impostata automaticamente quando il bundle viene installato. Inoltre, se la dimensione del set di migrazione è maggiore di 200 GB, il processo di estrazione utilizza automaticamente la funzione di precopia. Il file azcopy.config viene creato nella directory crx-quickstart/cloud-migration/. Se desideri aggiornare manualmente la configurazione del file, consulta le sezioni seguenti.

Segui questa sezione per scoprire come impostare l’utilizzo di AzCopy come passaggio pre-copia con lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM as a Cloud Service:

### &#x200B;0. Determinare la dimensione totale di tutto il contenuto nell’archivio dati {#determine-total-size}

È importante determinare la dimensione totale dell’archivio dati per due motivi:

* Se l&#39;AEM di origine è configurato per l&#39;utilizzo dell&#39;archivio dati File, lo spazio disponibile nel sistema locale deve essere notevolmente superiore a 1/256.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage}

Dalla pagina delle proprietà del contenitore esistente nel portale di Azure, utilizzare il pulsante **Calcola dimensione** per determinare le dimensioni di tutto il contenuto nel contenitore. Ad esempio:

![immagine](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Archivio dati Amazon S3 {#amazon-data}

Puoi utilizzare la scheda Metriche del contenitore per determinare le dimensioni di tutto il contenuto al suo interno. Ad esempio:


![immagine](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Archivio file di dati {#file-data-store-determine-size}

* Per i sistemi Mac e UNIX®, eseguire il comando du nella directory del datastore per ottenere le dimensioni:
  `du -sh [path to datastore on the instance]`. Ad esempio, se l&#39;archivio dati si trova in `/mnt/author/crx-quickstart/repository/datastore`, le dimensioni del comando seguente verranno recuperate: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Per Windows, utilizza il comando dir nella directory dell’archivio dati per ottenerne le dimensioni:
  `dir /a/s [location of datastore]`.

### &#x200B;1. Installare AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è uno strumento della riga di comando fornito da Microsoft® che deve essere disponibile nell&#39;istanza di origine per abilitare questa funzionalità.

In breve, si desidera scaricare il binario Linux® x86-64 dalla [pagina dei documenti AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e raddrizzarlo in una posizione come /usr/bin.

>[!IMPORTANT]
>Prendere nota della posizione in cui è stato posizionato il binario, in quanto in un passaggio successivo è necessario specificare il percorso completo.

### &#x200B;2. Installare la versione dello strumento Content Transfer (CTT) con supporto AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Deve essere utilizzata la versione di CTT rilasciata più di recente.

Il supporto di AzCopy per Amazon S3, Azure Blob Storage e File Data Store è incluso nell’ultima versione CTT.
Puoi scaricare l&#39;ultima versione di CTT dal portale [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).
È opportuno notare che sono supportate solo le versioni 2.0.0 e successive ed è consigliabile utilizzare la versione più recente.

### &#x200B;3. Configurare un file azcopy.config {#configure-azcopy-config-file}

Nell&#39;istanza AEM di origine in `crx-quickstart/cloud-migration` creare un file denominato `azcopy.config`.

>[!NOTE]
>Il contenuto di questo file di configurazione varia a seconda che l’istanza AEM di origine utilizzi un archivio dati di Azure o Amazon S3 o un archivio dati di file.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage-data}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare i valori azCopyPath e azureSas corretti per la tua istanza).

>[!NOTE]
>
> Se non si desidera concedere l&#39;accesso in scrittura al contenitore di archiviazione BLOB esistente, è possibile generare un nuovo URI SAS che dispone solo delle autorizzazioni di lettura ed elenco.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Archivio dati Amazon S3 {#amazon-sdata-store}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare i valori corretti per l’istanza).

>[!NOTE]
>
> Se l’istanza utilizza i ruoli IAM per consentire ad AEM di accedere a S3, devi creare un criterio e un utente con le azioni ListBucket e GetObject abilitate per il bucket S3. Una volta effettuata la configurazione, utilizza la chiave di accesso e la chiave segreta di questo utente.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Archivio file di dati {#file-data-store-azcopy-config}

Il file `azcopy.config` deve contenere la proprietà azCopyPath e una proprietà repository.home facoltativa che punta alla posizione dell&#39;archivio dati del file. Utilizza i valori corretti per l’istanza.
Archivio file di dati

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La proprietà azCopyPath deve contenere il percorso completo del percorso in cui è installato lo strumento da riga di comando azCopy nell’istanza AEM di origine. Se manca la proprietà azCopyPath, il passaggio di precopia BLOB non viene eseguito.

Se la proprietà `repository.home` non è presente in azcopy.config, per eseguire la precopia viene utilizzato il percorso predefinito dell&#39;archivio dati `/mnt/crx/author/crx-quickstart/repository/datastore`.

### &#x200B;4. Estrazione con AzCopy {#extracting-azcopy}

Con il file di configurazione di cui sopra attivo, la fase di pre-copia di AzCopy viene eseguita come parte di ogni estrazione successiva. Per evitare che venga eseguito, è possibile rinominare il file o rimuoverlo.

>[!NOTE]
>Se AzCopy non è configurato correttamente, nei registri viene visualizzato il seguente messaggio:
>&#x200B;>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inizia un’estrazione dall’interfaccia utente CTT. Per ulteriori dettagli, vedere [Guida introduttiva allo strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) e [Processo di estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md).

1. Conferma che nel registro di estrazione sia stampata la seguente riga:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Congratulazioni Questa voce di registro indica che la configurazione è stata considerata valida e che AzCopy sta copiando tutti i BLOB dal contenitore di origine al contenitore di migrazione.

Le voci di registro da AzCopy vengono visualizzate nel registro di estrazione con il prefisso c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Precopia AzCopy]

>[!CAUTION]
>
> Per i primi minuti di un’estrazione, controlla attentamente i registri di estrazione per individuare eventuali segni di un problema. Ad esempio, di seguito è riportato ciò che verrebbe registrato se non fosse possibile trovare il contenitore Azure di origine:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason > github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Se si verifica un problema con AzCopy, l’estrazione non riesce immediatamente e i registri di estrazione contengono i dettagli dell’errore.

Eventuali BLOB copiati prima dell’errore vengono ignorati automaticamente da AzCopy nelle esecuzioni successive e non è necessario copiarli nuovamente.

>[!TIP]
>Ora è possibile pianificare l’avvio automatico di un’acquisizione subito dopo la riuscita di un’estrazione. Per ulteriori informazioni, vedere [Inserimento di contenuto in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

>[!TIP]
>Se il trasferimento BLOB con AzCopy è andato avanti per un po’ ma poi non è riuscito per alcuni BLOB, eseguire nuovamente l’estrazione deselezionando le opzioni PreCopy e Overwrite Staging Container. In questo modo verranno migrati solo i BLOB rimanenti che non sono stati trasferiti in precedenza.

#### Per archivio dati file {#file-data-store-extract}

Quando AzCopy è in esecuzione per il file di origine dataStore, nei registri dovresti visualizzare messaggi come questi che indicano che le cartelle vengono elaborate:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### &#x200B;5. Acquisizione con AzCopy {#ingesting-azcopy}

Per informazioni generali sull&#39;acquisizione di contenuti in Target da Cloud Acceleration Manager (CAM), incluse le istruzioni sull&#39;utilizzo di AzCopy (pre-copia) o meno, nella finestra di dialogo &quot;Nuova acquisizione&quot;, vedere [Acquisizione di contenuti in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

Per sfruttare AzCopy durante l’acquisizione, Adobe richiede di utilizzare una versione di AEM as a Cloud Service che sia almeno la versione 2021.6.5561.

Consulta l’elenco &quot;Processi di acquisizione&quot; in Cloud Acceleration Manager e i registri di acquisizione per visualizzare l’avanzamento. Le voci di registro relative al
le attività AzCopy riuscite vengono visualizzate come segue (tenendo conto di alcune differenze). Controllare occasionalmente i registri potrebbe segnalare eventuali problemi
e aiutarti a trovare una soluzione rapida a qualsiasi problema.

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination does not have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## Passaggio successivo {#whats-next}

Ora hai imparato a gestire archivi di contenuti di grandi dimensioni per velocizzare le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service. Ora puoi imparare il processo di estrazione utilizzando lo strumento Content Transfer (Trasferimento contenuti). Consulta [Estrazione del contenuto da Source nello strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per scoprire come estrarre il set di migrazione dallo strumento Content Transfer.
