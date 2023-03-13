---
title: Gestione di archivi di contenuti di grandi dimensioni (legacy)
description: Questa sezione descrive la gestione di archivi di contenuti di grandi dimensioni
hide: true
hidefromtoc: true
exl-id: 19021f40-d0a5-4e0c-a213-c421338cedeb
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 2%

---

# Gestione di archivi di contenuti di grandi dimensioni (legacy) {#handling-large-content-repositories}

## Panoramica {#overview}

La copia di un numero elevato di BLOB con lo strumento Content Transfer (CTT) può richiedere diversi giorni.
Per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti e spostare i contenuti in AEM as a Cloud Service, la tecnologia CTT può sfruttare [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) come passaggio pre-copia facoltativo. Questo passaggio di pre-copia può essere utilizzato quando l’istanza AEM di origine è configurata per utilizzare un archivio dati di Amazon S3, Azure Blob Storage o File Data Store. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB dall’archivio dati di Amazon S3, Azure Blob Storage o File nell’archivio BLOB del set di migrazione. Nella fase di acquisizione, AzCopy copia i BLOB dall’archivio BLOB del set di migrazione all’archivio BLOB di destinazione as a Cloud Service per AEM.

>[!NOTE]
> Questa funzionalità è stata introdotta con la versione CTT 1.5.4.

## Considerazioni importanti prima di iniziare {#important-considerations}

Prima di iniziare, segui la sezione seguente per comprendere le considerazioni importanti:

* La versione dell’AEM di origine deve essere 6.3 - 6.5.

* L’archivio dati dell’AEM di origine è configurato per l’utilizzo dell’archiviazione BLOB di Amazon S3 o Azure. Per ulteriori informazioni, consulta [Configurazione degli archivi dei nodi e dei dati in AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* Ogni set di migrazione copierà l’intero archivio dati, pertanto deve essere utilizzato un solo set di migrazione.

* Per installare è necessario disporre dell&#39;accesso [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) sull&#39;istanza (o VM) che esegue l&#39;istanza AEM di origine.

* La raccolta oggetti inattivi dell’archivio dati è stata eseguita nei 7 giorni precedenti sull’origine. Per ulteriori informazioni, consulta [Raccolta oggetti inattivi dell’archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).


### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare un archivio dati di archiviazione Amazon S3 o Azure Blob {#additional-considerations-amazons3-azure}

* Poiché esiste un costo associato al trasferimento dei dati da Amazon S3 e Azure Blob Storage, il costo del trasferimento sarà relativo alla quantità totale di dati nel contenitore di archiviazione (a prescindere dal fatto che si faccia riferimento o meno all’AEM). Fai riferimento a [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Archiviazione BLOB di Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) per ulteriori dettagli.

* Sarà necessaria una coppia chiave di accesso e chiave segreta per il bucket Amazon S3 di origine o un URI SAS per il contenitore Archiviazione BLOB di Azure di origine (l’accesso in sola lettura va bene).

### Considerazioni aggiuntive se l’istanza AEM di origine è configurata per utilizzare l’archivio dati dei file {#additional-considerations-aem-instance-filedatastore}

* Il sistema locale deve disporre di uno spazio libero notevolmente maggiore di 1/256 delle dimensioni dell’archivio dati di origine. Ad esempio, se la dimensione del datastore è di 3 TB, lo spazio libero deve essere maggiore di 11,72 GB `crx-quickstart/cloud-migration` nella cartella di origine di AzCopy. Il sistema di origine deve disporre almeno di 1 GB di spazio libero. Lo spazio disponibile può essere ottenuto utilizzando `df -h` sulle istanze Linux e dir nelle istanze Windows.

* Ogni volta che l’estrazione viene eseguita con AzCopy abilitato, l’intero archivio dati del file viene appiattito e copiato nel contenitore di migrazione cloud. Se il set di migrazione è notevolmente inferiore alle dimensioni dell’archivio dati, l’approccio non è ottimale.

* Una volta che AzCopy è stato utilizzato per copiare sull’archivio dati, disattivalo per le estrazioni delta o integrative.

## Impostazione dell’utilizzo di AzCopy come passaggio di pre-copia {#setting-up-pre-copy-step}

Segui questa sezione per scoprire come configurare l’utilizzo di AzCopy come passaggio pre-copia con lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti a AEM as a Cloud Service:

### 0. Determinare la dimensione totale di tutto il contenuto nell’archivio dati {#determine-total-size}

È importante determinare la dimensione totale dell’archivio dati per due motivi:

* Se l&#39;AEM di origine è configurato per l&#39;utilizzo dell&#39;archivio dati File, il sistema locale deve disporre di spazio libero notevolmente superiore a 1/256 delle dimensioni dell&#39;archivio dati di origine.

* Conoscere la dimensione totale dell’archivio dati aiuterà a stimare i tempi di estrazione e acquisizione. Utilizza il [Calcolatore dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) per ottenere una stima dei tempi di estrazione e di acquisizione.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage}

Dalla pagina delle proprietà del contenitore nel portale di Azure, utilizza **Calcola dimensione** per determinare le dimensioni di tutto il contenuto nel contenitore. Esempio:

![immagine](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Archivio dati Amazon S3 {#amazon-data}

Puoi utilizzare la scheda Metriche del contenitore per determinare le dimensioni di tutto il contenuto al suo interno. Esempio:


![immagine](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Archivio file di dati {#file-data-store-determine-size}

* Per i sistemi mac, UNIX, eseguire il comando du sulla directory del datastore per ottenere le dimensioni:
   `du -sh [path to datastore on the instance]`. Ad esempio, se l’archivio dati si trova in `/mnt/author/crx-quickstart/repository/datastore`, il comando seguente ti consente di visualizzarne le dimensioni: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Per Windows, utilizza il comando dir nella directory dell’archivio dati per ottenerne le dimensioni:
   `dir /a/s [location of datastore]`.

### 1. Installare AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è uno strumento della riga di comando fornito da Microsoft che deve essere disponibile nell’istanza sorgente per abilitare questa funzione.

In breve, è molto probabile che si desidera scaricare il binario Linux x86-64 dal [Pagina documenti AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e rimuoverlo da una posizione come /usr/bin.

>[!IMPORTANT]
>Prendi nota di dove hai posizionato il binario, poiché in un passaggio successivo ti servirà il percorso completo.

### 2. Installare una versione dello strumento Content Transfer (CTT) con supporto AzCopy {#install-ctt-azcopy-support}

Il supporto di AzCopy per Amazon S3 e Azure Blob Storage è incluso nella versione CTT 1.5.4.
Il supporto per l’archivio dati dei file è incluso nella versione CTT 1.7.2. Puoi scaricare l’ultima versione di CTT da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) portale.


### 3. Configurare un file azcopy.config {#configure-azcopy-config-file}

Sull’istanza AEM di origine, in `crx-quickstart/cloud-migration`, crea un nuovo file denominato `azcopy.config`.

>[!NOTE]
>Il contenuto di questo file di configurazione sarà diverso a seconda che l’istanza AEM di origine utilizzi un archivio dati di Azure o Amazon S3 o un archivio dati di file.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage-data}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare i valori azCopyPath e azureSas corretti per la tua istanza).

>[!NOTE]
>
> Se non si desidera concedere l&#39;accesso in scrittura al contenitore di archiviazione BLOB, è possibile generare un nuovo URI SAS che dispone solo delle autorizzazioni di lettura ed elenco.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Archivio dati Amazon S3 {#amazon-sdata-store}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare i valori corretti per l’istanza).

>[!NOTE]
>
> Se l’istanza utilizza i ruoli IAM per consentire a AEM di accedere a S3, dovrai creare un criterio e un utente con le azioni ListBucket e GetObject abilitate per il bucket S3. Una volta effettuata la configurazione, utilizza la chiave di accesso e la chiave segreta di questo utente.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Archivio file di dati {#file-data-store-azcopy-config}

Il tuo `azcopy.config` il file deve contenere la proprietà azcopyPath e una proprietà repository.home facoltativa che punti alla posizione dell&#39;archivio dati del file. Utilizza i valori corretti per l’istanza.
Archivio file di dati

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La proprietà azcopyPath deve contenere il percorso completo del percorso in cui è installato lo strumento della riga di comando azCopy nell&#39;istanza AEM di origine. Se manca la proprietà azCopyPath, il passaggio di precopia BLOB non verrà eseguito.

Se `repository.home` proprietà mancante in azcopy.config, quindi nel percorso predefinito dell&#39;archivio dati `/mnt/crx/author/crx-quickstart/repository/datastore` per eseguire la precopia.

### 4. Estrazione con AzCopy {#extracting-azcopy}

Con il file di configurazione di cui sopra attivo, la fase di pre-copia di AzCopy verrà eseguita come parte di ogni estrazione successiva. Per evitare che venga eseguito, è possibile rinominare il file o rimuoverlo.

>[!NOTE]
>Se AzCopy non è configurato correttamente, visualizzerai questo messaggio nei registri:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inizia un’estrazione dall’interfaccia utente CTT. Fai riferimento a [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) e [Processo di estrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=it) per ulteriori dettagli.

1. Conferma che nel registro di estrazione sia stampata la seguente riga:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Congratulazioni. Questa voce di registro indica che la configurazione è stata considerata valida e che AzCopy sta attualmente copiando tutti i BLOB dal contenitore di origine al contenitore di migrazione.

Le voci di registro da AzCopy verranno visualizzate nel registro di estrazione e avranno il prefisso c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pre-copia AzCopy]

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

In caso di un problema con AzCopy, l’estrazione non riuscirà immediatamente e i registri di estrazione conterranno i dettagli dell’errore.

Eventuali BLOB copiati prima dell’errore verranno ignorati automaticamente da AzCopy nelle esecuzioni successive e non sarà necessario copiarli nuovamente.

#### Per archivio dati file {#file-data-store-extract}

Quando AzCopy è in esecuzione per il file di origine dataStore, nei registri dovresti visualizzare messaggi come questi che indicano che le cartelle vengono elaborate:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Acquisizione con AzCopy {#ingesting-azcopy}

Con il rilascio della versione 1.5.4 dello strumento Content Transfer (Trasferimento contenuti) è stato aggiunto il supporto di AzCopy per l’acquisizione dell’autore.

>[!NOTE]
>Ti consigliamo di eseguire prima l’acquisizione dell’authoring. In questo modo l’acquisizione Publish sarà più rapida quando viene eseguita in un secondo momento.

Per sfruttare AzCopy durante l’acquisizione, è necessario utilizzare una versione di AEM as a Cloud Service che sia almeno la versione 2021.6.5561.

Inizia l’acquisizione dell’autore dall’interfaccia utente CTT. Consulta la sezione [Processo di acquisizione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=it) per ulteriori dettagli.
Le voci di registro da AzCopy verranno visualizzate nel registro di acquisizione. Avranno un aspetto simile al seguente:

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
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

## Disabilitazione di AzCopy {#disable-azcopy}

Per disattivare AzCopy, rinominate o eliminate la `azcopy.config` file.

Ad esempio, l’estrazione azcopy può essere disabilitata con: `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## Passaggio successivo {#whats-next}

Dopo aver appreso come gestire archivi di contenuti di grandi dimensioni per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti nell’as a Cloud Service AEM, ora puoi iniziare a utilizzare il processo di estrazione con lo strumento Trasferimento contenuti. Consulta [Estrazione di contenuto dall’origine nello strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per scoprire come estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
