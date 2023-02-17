---
title: Gestione di archivi di contenuti di grandi dimensioni
description: Questa sezione descrive la gestione di archivi di contenuti di grandi dimensioni
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: d07a4fd0a335295d399057ea1eef567e757e2d92
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 2%

---

# Gestione di archivi di contenuti di grandi dimensioni {#handling-large-content-repositories}

## Panoramica {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestione di archivi di contenuti di grandi dimensioni"
>abstract="Per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service, CTT può sfruttare AzCopy come passaggio opzionale di pre-copia. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB da Amazon S3 o Azure Blob Storage nell’archivio BLOB del set di migrazione. Nella fase di acquisizione, AzCopy copia i BLOB dall’archivio BLOB del set di migrazione alla destinazione AEM archivio BLOB as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="Guida introduttiva ad AzCopy come passaggio Pre-Copy"

La copia di un numero elevato di BLOB con lo strumento Content Transfer (CTT) può richiedere più giorni.
Per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service, il CTT può sfruttare [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) come passaggio di pre-copia facoltativo. Questo passaggio di pre-copia può essere utilizzato quando l&#39;istanza AEM di origine è configurata per utilizzare un archivio dati Amazon S3, Azure Blob Storage o File Data Store. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione completa. Tuttavia, non è consigliabile utilizzare la precopia per gli integratori successivi (se la dimensione dell’integrazione è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB da Amazon S3, Azure Blob Storage o dall’archivio dati File nell’archivio BLOB del set di migrazione. Nella fase di acquisizione, AzCopy copia i BLOB dall’archivio BLOB del set di migrazione alla destinazione AEM archivio BLOB as a Cloud Service.

## Considerazioni importanti prima di iniziare {#important-considerations}

Leggi la sezione seguente per comprendere le considerazioni importanti prima di iniziare:

* La versione di AEM di origine deve essere 6.3 - 6.5.

* L&#39;archivio dati AEM origine è configurato per utilizzare Amazon S3 o Azure Blob Storage. Per ulteriori dettagli, consulta [Configurazione degli archivi di nodi e degli archivi di dati nel AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* Ogni set di migrazione copierà l’intero archivio dati, quindi deve essere utilizzato un solo set di migrazione.

* Sarà necessario accedere all&#39;installazione [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) sull&#39;istanza (o VM) che esegue l&#39;istanza di AEM sorgente.

* Data Store Garbage Collection è stato eseguito nei 7 giorni precedenti sull&#39;origine. Per ulteriori informazioni, consulta [Raccolta rifiuti dell&#39;archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).

### Considerazioni aggiuntive relative all’utilizzo di AzCopy

La pre-copia con AzCopy non è attualmente supportata su Windows durante l’estrazione CTT.

### Considerazioni aggiuntive se l’istanza di AEM di origine è configurata per l’utilizzo di un archivio dati di archiviazione BLOB di Amazon S3 o Azure {#additional-considerations-amazons3-azure}

* Poiché è presente un costo associato al trasferimento di dati da Amazon S3 e Azure Blob Storage, il costo di trasferimento sarà relativo alla quantità totale di dati nel contenitore di archiviazione esistente (a cui si fa riferimento in AEM o meno). Fai riferimento a [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Archiviazione BLOB di Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) per ulteriori dettagli.

* Sarà necessario disporre di una coppia chiave di accesso e chiave segreta per il bucket Amazon S3 di origine esistente oppure di un URI SAS per il contenitore di archiviazione BLOB di Azure di origine esistente (l&#39;accesso in sola lettura va bene).

### Considerazioni aggiuntive se l&#39;istanza AEM di origine è configurata per l&#39;utilizzo di File Data Store {#additional-considerations-aem-instance-filedatastore}

* Il sistema locale deve avere spazio libero strettamente superiore a 1/256 dimensioni del datastore sorgente. Ad esempio, se la dimensione del datastore è di 3 TB, deve esistere spazio libero superiore a 11,72 GB nel `crx-quickstart/cloud-migration` nella cartella di origine di AzCopy per il funzionamento. Come minimo, il sistema di origine deve avere 1 GB di spazio libero. Lo spazio libero può essere ottenuto utilizzando `df -h` comando sulle istanze Linux e comando dir nelle istanze Windows.

* Ogni volta che l’estrazione viene eseguita con AzCopy abilitato, l’intero datastore del file viene appiattito e copiato nel contenitore di migrazione cloud. Se il set di migrazione è significativamente più piccolo della dimensione del datastore, l’estrazione di AzCopy non è l’approccio ottimale.

* Una volta che AzCopy è stato utilizzato per copiare il datastore esistente, disabilitarlo per le estrazioni delta o top-up.

## Impostazione per utilizzare AzCopy come passaggio di pre-copia {#setting-up-pre-copy-step}

Leggi questa sezione per scoprire come configurare per utilizzare AzCopy come passaggio di pre-copia con lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM as a Cloud Service:

### 0. Determinare la dimensione totale di tutto il contenuto nell&#39;archivio dati {#determine-total-size}

È importante determinare la dimensione totale dell’archivio dati per due motivi:

* Se l&#39;AEM di origine è configurata per l&#39;utilizzo dell&#39;archivio dati File, lo spazio libero del sistema locale deve essere strettamente maggiore di 1/256 dimensioni dell&#39;archivio dati di origine.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage}

Dalla pagina delle proprietà del contenitore esistente nel portale di Azure, utilizza **Calcola dimensioni** per determinare le dimensioni di tutto il contenuto del contenitore. Esempio:

![immagine](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Archivio dati Amazon S3 {#amazon-data}

Puoi utilizzare la scheda Metriche del contenitore per determinare la dimensione di tutto il contenuto del contenitore. Esempio:


![immagine](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Archivio file di dati {#file-data-store-determine-size}

* Per i sistemi mac, UNIX, eseguire il comando du nella directory del datastore per ottenere le sue dimensioni:
   `du -sh [path to datastore on the instance]`. Ad esempio, se il datastore si trova in `/mnt/author/crx-quickstart/repository/datastore`, il seguente comando ti darà le sue dimensioni: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* Per Windows, utilizza il comando dir nella directory del datastore per ottenere le sue dimensioni:
   `dir /a/s [location of datastore]`.

### 1. Installa AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è uno strumento a riga di comando fornito da Microsoft che deve essere disponibile nell’istanza sorgente per abilitare questa funzione.

In breve, molto probabilmente si desidera scaricare il binario Linux x86-64 dal [Pagina docs di AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e cancellalo in una posizione come /usr/bin.

>[!IMPORTANT]
>Prendi nota di dove hai posizionato il binario, in quanto ti servirà il percorso completo in un passaggio successivo.

### 2. Installare la versione dello strumento Content Transfer (CTT) con il supporto AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Deve essere utilizzata la versione più recente del CTT.

Il supporto di AzCopy per Amazon S3, Azure Blob Storage e File Data Store è incluso nella versione più recente del CTT.
Puoi scaricare l’ultima versione di CTT dal [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) portale.
È opportuno notare che saranno supportate solo le versioni 2.0.0 e successive ed è consigliabile utilizzare la versione più recente.

### 3. Configurare un file azcopy.config {#configure-azcopy-config-file}

Nell&#39;istanza AEM di origine, in `crx-quickstart/cloud-migration`, crea un nuovo file denominato `azcopy.config`.

>[!NOTE]
>Il contenuto di questo file di configurazione sarà diverso a seconda che l’istanza AEM di origine utilizzi un archivio dati o un archivio dati di Azure o Amazon S3 o File.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage-data}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare le proprietà azCopyPath e azureSas corrette per la tua istanza).

>[!NOTE]
>
> Se si preferisce non concedere l&#39;accesso in scrittura al contenitore di archiviazione BLOB esistente, è possibile generare un nuovo URI SAS che dispone solo delle autorizzazioni di lettura ed elenco.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Archivio dati Amazon S3 {#amazon-sdata-store}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare i valori corretti per la tua istanza).

>[!NOTE]
>
> Se la tua istanza utilizza Ruoli IAM per consentire AEM di accedere a S3, dovrai creare un criterio e un utente con le azioni ListBucket e GetObject abilitate per il bucket S3. Una volta configurato, utilizza la chiave di accesso e la chiave segreta di questo utente.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### Archivio file di dati {#file-data-store-azcopy-config}

Le `azcopy.config` Il file deve contenere la proprietà azCopyPath e una proprietà repository.home opzionale che punta alla posizione del datastore del file. Utilizza i valori corretti per la tua istanza.
Archivio file di dati

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

La proprietà azCopyPath deve contenere il percorso completo della posizione in cui lo strumento della riga di comando azCopy è installato nell&#39;istanza di AEM di origine. Se la proprietà azCopyPath è mancante, il passaggio di precopia BLOB non verrà eseguito.

Se `repository.home` manca la proprietà da azcopy.config, quindi la posizione predefinita del datastore `/mnt/crx/author/crx-quickstart/repository/datastore` viene utilizzato per eseguire la precopia.

### 4. Estrazione con AzCopy {#extracting-azcopy}

Con il file di configurazione sopra riportato, la fase di pre-copia di AzCopy verrà eseguita come parte di ogni estrazione successiva. Per evitare che venga eseguito, è possibile rinominare o rimuovere il file.

>[!NOTE]
>Se AzCopy non è configurato correttamente, visualizzerai questo messaggio nei registri:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Inizia un’estrazione dall’interfaccia utente CTT. Fai riferimento a [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) e [Processo di estrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) per ulteriori dettagli.

1. Conferma che la seguente riga venga stampata nel registro di estrazione:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Congratulazioni. Questa voce di registro indica che la configurazione è stata considerata valida e che AzCopy sta attualmente copiando tutti i BLOB dal contenitore di origine al contenitore di migrazione.

Le voci di registro da AzCopy appariranno nel registro di estrazione e avranno il prefisso c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [Pre-copia di AzCopy]

>[!CAUTION]
>
> Per i primi minuti di un’estrazione, guarda attentamente i registri di estrazione per eventuali segnali di un problema. Ad esempio, ecco cosa verrebbe registrato se non fosse stato possibile trovare il contenitore di origine Azure:

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

In caso di problemi con AzCopy, l’estrazione avrà esito negativo immediatamente e i log di estrazione conterranno dettagli sull’errore.

Eventuali BLOB copiati prima dell’errore verranno ignorati automaticamente da AzCopy nelle esecuzioni successive e non sarà necessario copiarli di nuovo.

#### Per archivio dati file {#file-data-store-extract}

Quando AzCopy è in esecuzione per il file di origine dataStore, è necessario visualizzare messaggi come questi nei registri che indicano che le cartelle sono in fase di elaborazione:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Acquisizione con AzCopy {#ingesting-azcopy}

Fai riferimento a [Inserimento di contenuto in Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html)
per informazioni generali sull’acquisizione di contenuti nel target da Cloud Acceleration Manager (CAM), incluse istruzioni sull’utilizzo di AzCopy (pre-copia) o meno, nella finestra di dialogo &quot;Nuova acquisizione&quot;.

Per sfruttare AzCopy durante l’acquisizione, è necessario disporre di una versione AEM as a Cloud Service che sia almeno la versione 2021.6.5561.

Per informazioni sull’avanzamento, consulta l’elenco &quot;Processi di acquisizione&quot; in Cloud Acceleration Manager e i registri di acquisizione.  Le voci di registro relative alle attività AzCopy riuscite verranno visualizzate come segue (tenendo conto di alcune differenze). Controllando occasionalmente i log potrebbe avvisarti di problemi in anticipo e aiutare a trovare una soluzione rapida a qualsiasi problema.

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

## Passaggio successivo {#whats-next}

Dopo aver imparato a gestire archivi di contenuti di grandi dimensioni per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service, ora puoi imparare il processo di estrazione utilizzando lo strumento Content Transfer (Trasferimento contenuti). Vedi [Estrazione di contenuti dall’origine nello strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per scoprire come estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
