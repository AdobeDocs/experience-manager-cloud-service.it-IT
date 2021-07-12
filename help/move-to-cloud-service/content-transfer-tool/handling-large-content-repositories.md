---
title: Gestione di archivi di contenuti di grandi dimensioni
description: Questa sezione descrive la gestione degli archivi di contenuti di grandi dimensioni
source-git-commit: c19878b41970f4cd34083395ab11cf82c1db667e
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# Gestione di archivi di contenuti di grandi dimensioni {#handling-large-content-repositories}

## Panoramica {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Gestione di archivi di contenuti di grandi dimensioni"
>abstract="Per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM come Cloud Service, CTT può sfruttare AzCopy come passaggio opzionale di pre-copia. Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB da Amazon S3 o Azure Blob Storage nell’archivio BLOB del set di migrazione. Nella fase di acquisizione, AzCopy copia i BLOB dall’archivio BLOB del set di migrazione al AEM di destinazione come archivio BLOB di Cloud Service."
>additional-url="https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10" text="Guida introduttiva ad AzCopy"

La copia di un numero elevato di BLOB con lo strumento Content Transfer (CTT) può richiedere più giorni.
Per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM come Cloud Service, CTT può sfruttare [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) come passaggio opzionale di pre-copia. Questo passaggio di pre-copia può essere utilizzato quando l’istanza AEM di origine è configurata per utilizzare un archivio dati di archiviazione BLOB di Amazon S3 o Azure.  Una volta configurato questo passaggio preliminare, nella fase di estrazione, AzCopy copia i BLOB da Amazon S3 o Azure Blob Storage nell’archivio BLOB del set di migrazione. Nella fase di acquisizione, AzCopy copia i BLOB dall’archivio BLOB del set di migrazione al AEM di destinazione come archivio BLOB di Cloud Service.

>[!NOTE]
> Questa funzionalità è stata introdotta nella versione CTT 1.5.4.

## Considerazioni importanti prima di iniziare {#important-considerations}

Leggi la sezione seguente per comprendere le considerazioni importanti prima di iniziare:

* La versione di AEM di origine deve essere 6.3 - 6.5
* L&#39;archivio dati AEM origine è configurato per utilizzare Amazon S3 o Azure Blob Storage. Per ulteriori dettagli, consulta [Configurazione degli archivi di nodi e degli archivi di dati in AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).
* L’intero archivio dati verrà copiato durante l’estrazione. Poiché è presente un costo associato al trasferimento di dati da Amazon S3 e Azure Blob Storage, il costo di trasferimento sarà relativo alla quantità totale di dati nel contenitore di archiviazione (a cui si fa riferimento in AEM o meno). Per ulteriori informazioni, consulta [Amazon S3](https://aws.amazon.com/s3/pricing/) e [Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) .
* Ogni set di migrazione copierà l’intero archivio dati, quindi deve essere utilizzato un solo set di migrazione.
* Sarà necessario l&#39;accesso per installare [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) sull&#39;istanza (o VM) che esegue l&#39;istanza AEM di origine.
* Sarà necessario disporre di una coppia chiave di accesso e chiave segreta per il bucket Amazon S3 di origine o di un URI SAS per il contenitore di archiviazione BLOB di Azure di origine (l&#39;accesso in sola lettura è corretto).
* Data Store Garbage Collection è stato eseguito nei 7 giorni precedenti sull&#39;origine. Per ulteriori dettagli, consulta [Raccolta rifiuti dell&#39;archivio dati](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).
* La maggior parte dei dati sull’istanza sorgente verrà inclusa nella migrazione.

## Impostazione per utilizzare AzCopy come passaggio di pre-copia {#setting-up-pre-copy-step}

Leggi questa sezione per scoprire come configurare per utilizzare AzCopy come passaggio di pre-copia con lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM come Cloud Service:

### 0. Determinare la dimensione totale di tutto il contenuto nell&#39;archivio dati {#determine-total-size}

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage}

Dalla pagina delle proprietà del contenitore nel portale di Azure, utilizza il pulsante **Calcola dimensioni** per determinare la dimensione di tutto il contenuto nel contenitore. Esempio:

![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Archivio dati Amazon S3 {#amazon-data}

Puoi utilizzare la scheda Metriche del contenitore per determinare la dimensione di tutto il contenuto del contenitore. Esempio:


![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. Installa AzCopy {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopy è uno strumento a riga di comando fornito da Microsoft che deve essere disponibile nell’istanza sorgente per abilitare questa funzione.

In breve, molto probabilmente vorrai scaricare il binario Linux x86-64 dalla pagina dei documenti [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) e cancellarlo in una posizione come /usr/bin. Prendi nota di dove hai posizionato il binario, in quanto ti servirà il percorso completo in un passaggio successivo.

### 2. Installare una versione dello strumento Content Transfer (CTT) con il supporto AzCopy {#install-ctt-azcopy-support}

Il supporto di AzCopy è incluso nella versione CTT 1.5.4. Puoi scaricare l’ultima versione di CTT dal portale [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) .

### 3. Configurare un file azcopy.config {#configure-azcopy-config-file}

Nell&#39;istanza di AEM sorgente, in crx-quickstart/cloud-migration , crea un nuovo file chiamato azcopy.config .

Il contenuto di questo file di configurazione sarà diverso a seconda che l’istanza AEM di origine utilizzi un archivio dati di Azure o Amazon S3.

#### Archivio dati archiviazione BLOB di Azure {#azure-blob-storage-data}

Il file azcopy.config deve includere le seguenti proprietà (assicurati di utilizzare le proprietà azCopyPath e azureSas corrette per la tua istanza).

>[!NOTE]
>
> Se si preferisce non concedere l&#39;accesso in scrittura al contenitore di archiviazione BLOB, è possibile generare un nuovo URI SAS che dispone solo delle autorizzazioni di lettura ed elenco.

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

### 4. Estrazione con AzCopy {#extracting-azcopy}

Con il file di configurazione sopra riportato, la fase di pre-copia di AzCopy verrà eseguita come parte di ogni estrazione successiva. Per evitare che venga eseguito, è possibile rinominare o rimuovere il file.

1. Inizia un’estrazione dall’interfaccia utente CTT. Per ulteriori informazioni, consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti)](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool) e [Processo di estrazione](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) .
1. Conferma che la seguente riga venga stampata nel registro di estrazione:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Congratulazioni! Questa voce di registro indica che la configurazione è stata considerata valida e che AzCopy sta attualmente copiando tutti i BLOB dal contenitore di origine al contenitore di migrazione.

Le voci di registro da AzCopy appariranno nel registro di estrazione e avranno il prefisso c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy]

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

### 5. Acquisizione con AzCopy {#ingesting-azcopy}

Con il rilascio dello strumento Content Transfer (Trasferimento contenuti) 1.5.4, è stato aggiunto il supporto AzCopy all’acquisizione di autori.

>[!NOTE]
>Si consiglia di eseguire prima l’acquisizione dell’autore da sola. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.

Per sfruttare AzCopy durante l’acquisizione, è necessario che tu sia su un AEM come versione di Cloud Service che sia almeno la versione 2021.6.5561.

Inizia l’acquisizione dell’autore dall’interfaccia utente CTT. Per ulteriori informazioni, consulta [Processo di acquisizione](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) .
Le voci di registro da AzCopy verranno visualizzate nel registro di acquisizione. Avranno questo aspetto:

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
