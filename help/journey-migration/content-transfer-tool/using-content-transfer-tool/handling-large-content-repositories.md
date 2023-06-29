---
title: Gestione di archivi di contenuti di grandi dimensioni
description: Questa sezione descrive la gestione di archivi di contenuti di grandi dimensioni
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 6%

---

# Gestione di archivi di contenuti di grandi dimensioni {#handling-large-content-repositories}

## Panoramica {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestione di archivi di contenuti di grandi dimensioni"
>abstract="Per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti e spostare i contenuti in AEM as a Cloud Service, lo strumento Content Transfer (CTT) può utilizzare AzCopy come fase di pre-copia opzionale. Una volta configurato questo passaggio preliminare, nella fase di estrazione AzCopy copia i BLOB da Amazon S3 o dall’archiviazione BLOB di Azure nell’archivio BLOB del set di migrazione. Nella fase di acquisizione AzCopy copia i BLOB dall’archivio BLOB del set di migrazione all’archivio BLOB di AEM as a Cloud Service di destinazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step" text="Guida introduttiva ad AzCopy come passaggio di pre-copia"

La copia di molti BLOB con lo strumento Content Transfer (CTT) può richiedere diversi giorni.
Per velocizzare le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti e spostare i contenuti in AEM as a Cloud Service, la CTT può utilizzare [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) come passaggio pre-copia facoltativo. Questo passaggio di pre-copia può essere utilizzato quando l’istanza AEM di origine è configurata per utilizzare un archivio dati di Amazon S3, Azure Blob Storage o File Data Store. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione complete. Tuttavia, l’utilizzo della pre-copia per i successivi integratori non è consigliato (se la dimensione dell’integratore è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB dall’archivio dati di Amazon S3, Azure Blob Storage o File nell’archivio BLOB del set di migrazione. Nella fase di acquisizione AzCopy copia i BLOB dall’archivio BLOB del set di migrazione all’archivio BLOB di AEM as a Cloud Service di destinazione.

## Considerazioni importanti prima di iniziare {#important-considerations}

Prima di iniziare, segui la sezione seguente per comprendere le considerazioni importanti:

* A partire dalla versione 2.0.16 di CTT, la precopia viene impostata automaticamente quando il bundle viene installato. Inoltre, se la dimensione del set di migrazione è maggiore di 200 GB, il processo di estrazione utilizza automaticamente la funzione di precopia. Il file azcopy.config viene creato nella directory crx-quickstart/cloud-migration/. Non è necessario eseguire manualmente la precopia se si utilizza CTT versione 2.0.16 o successiva.

* La versione dell’AEM di origine deve essere 6.3 - 6.5.

* L’archivio dati dell’AEM di origine è configurato per l’utilizzo dell’archiviazione BLOB di Amazon S3 o Azure. Per ulteriori dettagli, consulta [Configurazione degli archivi dei nodi e dei dati in AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* Ogni set di migrazione copia l’intero archivio dati, pertanto è necessario utilizzare un solo set di migrazione.

* Per installare è necessario disporre dell&#39;accesso [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) sull&#39;istanza (o VM) che esegue l&#39;istanza AEM di origine.

* La raccolta oggetti inattivi dell’archivio dati è stata eseguita nei sette giorni precedenti sull’origine. Per ulteriori dettagli, consulta [Raccolta oggetti inattivi dell’archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare un archivio dati di archiviazione Amazon S3 o Azure Blob {#additional-considerations-amazons3-azure}

* Il trasferimento dei dati da Amazon S3 e dall’archiviazione BLOB di Azure comporta un costo. Il costo del trasferimento è relativo alla quantità totale di dati nel contenitore di storage esistente (a prescindere dal fatto che vi si faccia riferimento o meno nell&#39;AEM). Consulta [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Archiviazione BLOB di Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) per ulteriori dettagli.

* È necessaria una coppia chiave di accesso e chiave segreta per il bucket Amazon S3 di origine esistente oppure un URI SAS per il contenitore Archiviazione BLOB di Azure di origine esistente (l’accesso in sola lettura va bene).

### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare l’archivio dati dei file {#additional-considerations-aem-instance-filedatastore}

* Il sistema locale deve disporre di uno spazio libero notevolmente maggiore di 1/256 delle dimensioni dell’archivio dati di origine. Ad esempio, se la dimensione del datastore è di 3 terabyte, lo spazio libero deve essere maggiore di 11,72 GB `crx-quickstart/cloud-migration` nella cartella di origine di AzCopy. Il sistema di origine deve disporre almeno di 1 GB di spazio libero. Lo spazio disponibile può essere ottenuto utilizzando `df -h` sulle istanze Linux® e dir nelle istanze Windows.

* Ogni volta che l’estrazione viene eseguita con AzCopy abilitato, l’intero archivio dati del file viene appiattito e copiato nel contenitore di migrazione cloud. Se il set di migrazione è più piccolo delle dimensioni dell’archivio dati, l’estrazione AzCopy non è l’approccio ottimale.

* Una volta che AzCopy è stato utilizzato per copiare sull’archivio dati esistente, disattivarlo per le estrazioni delta o integrative.

## Impostazione dell’utilizzo di AzCopy come passaggio di pre-copia {#setting-up-pre-copy-step}

>[!NOTE]
>A partire dalla versione 2.0.16 di CTT, la precopia viene impostata automaticamente quando il bundle viene installato. Inoltre, se la dimensione del set di migrazione è maggiore di 200 GB, il processo di estrazione utilizza automaticamente la funzione di precopia. Il file azcopy.config viene creato nella directory crx-quickstart/cloud-migration/. Se desideri aggiornare manualmente la configurazione del file, consulta le sezioni seguenti.

Segui questa sezione per scoprire come configurare per utilizzare AzCopy come passaggio pre-copia con lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto a AEM as a Cloud Service:

### 0. Determinare la dimensione totale di tutto il contenuto nell’archivio dati {#determine-total-size}

È importante determinare la dimensione totale dell’archivio dati per due motivi:

* Se l&#39;AEM di origine è configurato per l&#39;utilizzo dell&#39;archivio dati File, il sistema locale deve disporre di spazio libero notevolmente superiore a 1/256 delle dimensioni dell&#39;archivio dati di origine.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage}

Dalla pagina delle proprietà del contenitore esistente nel portale di Azure, utilizza **Calcola dimensione** per determinare le dimensioni di tutto il contenuto nel contenitore. Ad esempio:

![immagine](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Archivio dati Amazon S3 {#amazon-data}

Puoi utilizzare la scheda Metriche del contenitore per determinare le dimensioni di tutto il contenuto al suo interno. Ad esempio:


![immagine](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Archivio file di dati {#file-data-store-determine-size}

* Per i sistemi Mac e UNIX®, eseguire il comando du nella directory del datastore per ottenere le dimensioni:
  `du -sh [path to datastore on the instance]`. Ad esempio, se l’archivio dati si trova in `/mnt/author/crx-quickstart/repository/datastore`, il comando seguente consente di ottenere le dimensioni: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Per Windows, utilizza il comando dir nella directory dell’archivio dati per ottenerne le dimensioni:
  `dir /a/s [location of datastore]`.

### 1. Installare AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è uno strumento della riga di comando fornito da Microsoft® che deve essere disponibile nell’istanza di origine per abilitare questa funzione.

In breve, si desidera scaricare il binario Linux® x86-64 dal [Pagina documenti AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e lo sposta in una posizione come /usr/bin.

>[!IMPORTANT]
>Prendere nota della posizione in cui è stato posizionato il binario, in quanto in un passaggio successivo è necessario specificare il percorso completo.

### 2. Installare la versione dello strumento Content Transfer (CTT) con supporto AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Deve essere utilizzata la versione di CTT rilasciata più di recente.

Il supporto di AzCopy per Amazon S3, Azure Blob Storage e File Data Store è incluso nell’ultima versione CTT.
Puoi scaricare l’ultima versione di CTT da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) portale.
È opportuno notare che sono supportate solo le versioni 2.0.0 e successive ed è consigliabile utilizzare la versione più recente.

### 3. Configurare un file azcopy.config {#configure-azcopy-config-file}

Sull’istanza AEM di origine, in `crx-quickstart/cloud-migration`, crea un file denominato `azcopy.config`.

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
> Se l’istanza utilizza i ruoli IAM per consentire a AEM di accedere a S3, devi creare un criterio e un utente con le azioni ListBucket e GetObject abilitate per il bucket S3. Una volta effettuata la configurazione, utilizza la chiave di accesso e la chiave segreta di questo utente.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Archivio file di dati {#file-data-store-azcopy-config}

Il tuo `azcopy.config` deve contenere la proprietà azCopyPath e una proprietà repository.home facoltativa che punti alla posizione dell&#39;archivio dati del file. Utilizza i valori corretti per l’istanza.
Archivio file di dati

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La proprietà azCopyPath deve contenere il percorso completo del percorso in cui è installato lo strumento della riga di comando azCopy nell&#39;istanza AEM di origine. Se manca la proprietà azCopyPath, il passaggio di precopia BLOB non viene eseguito.

Se `repository.home` proprietà mancante in azcopy.config, quindi nel percorso predefinito dell&#39;archivio dati `/mnt/crx/author/crx-quickstart/repository/datastore` viene utilizzato per eseguire la precopia.

### 4. Estrazione con AzCopy {#extracting-azcopy}

Con il file di configurazione di cui sopra attivo, la fase di pre-copia di AzCopy viene eseguita come parte di ogni estrazione successiva. Per evitare che venga eseguito, è possibile rinominare il file o rimuoverlo.

>[!NOTE]
>Se AzCopy non è configurato correttamente, nei registri viene visualizzato il seguente messaggio:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inizia un’estrazione dall’interfaccia utente CTT. Consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) e [Processo di estrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per ulteriori dettagli.

1. Conferma che nel registro di estrazione sia stampata la seguente riga:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Congratulazioni. Questa voce di registro indica che la configurazione è stata considerata valida e che AzCopy sta copiando tutti i BLOB dal contenitore di origine al contenitore di migrazione.

Le voci di registro da AzCopy vengono visualizzate nel registro di estrazione con il prefisso c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pre-copia AzCopy]

>[!CAUTION]
>
> Per i primi minuti di un’estrazione, controlla attentamente i registri di estrazione per individuare eventuali segni di un problema. Ad esempio, di seguito è riportato ciò che verrebbe registrato se non fosse possibile trovare il contenitore Azure di origine:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Se si verifica un problema con AzCopy, l’estrazione non riesce immediatamente e i registri di estrazione contengono i dettagli dell’errore.

Eventuali BLOB copiati prima dell’errore vengono ignorati automaticamente da AzCopy nelle esecuzioni successive e non è necessario copiarli nuovamente.

#### Per archivio dati file {#file-data-store-extract}

Quando AzCopy è in esecuzione per il file di origine dataStore, nei registri dovresti visualizzare messaggi come questi che indicano che le cartelle vengono elaborate:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Acquisizione con AzCopy {#ingesting-azcopy}

Consulta [Acquisizione di contenuti in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
per informazioni generali sull’acquisizione di contenuti nella destinazione da Cloud Acceleration Manager (CAM), incluse istruzioni sull’utilizzo di AzCopy (pre-copia) o meno, nella finestra di dialogo &quot;Nuova acquisizione&quot;.

Per sfruttare AzCopy durante l’acquisizione, Adobe richiede di utilizzare una versione as a Cloud Service dell’AEM che sia almeno la versione 2021.6.5561.

Consulta l’elenco &quot;Processi di acquisizione&quot; in Cloud Acceleration Manager e i registri di acquisizione per visualizzare l’avanzamento. Le voci di registro relative alle attività AzCopy riuscite vengono visualizzate come segue (tenendo conto di alcune differenze). Controllando i registri di tanto in tanto si potrebbe avvisare presto dei problemi, e aiutare a trovare una soluzione rapida a qualsiasi problema.

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

Ora hai imparato a gestire archivi di contenuti di grandi dimensioni per velocizzare le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in as a Cloud Service AEM. Ora puoi imparare il processo di estrazione utilizzando lo strumento Content Transfer (Trasferimento contenuti). Consulta [Estrazione di contenuto dall’origine nello strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per scoprire come estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
