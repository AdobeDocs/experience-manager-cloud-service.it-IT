---
title: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 04494e116fcdd38622ae2d4434d7cf8e4034d5aa
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 52%

---

# Utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#using-content-transfer-tool}

## Processo di estrazione nel trasferimento dei contenuti {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Estrazione dei contenuti"
>abstract="Per estrazione si intende l’estrazione del contenuto dall’istanza AEM di origine in un’area temporanea denominata set di migrazione. Un set di migrazione è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Estrazione dall&#39;alto verso l&#39;alto"

Per estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Se Amazon S3 o Azure Data Store viene utilizzato come tipo di archivio dati, puoi eseguire il passaggio facoltativo di pre-copia per accelerare in modo significativo la fase di estrazione. A questo scopo, devi configurare un file `azcopy.config` prima di eseguire l’estrazione. Per ulteriori informazioni, consulta [Gestione degli archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) .

1. Seleziona un set di migrazione dalla pagina *Overview* (Panoramica) e fai clic su **Extract** (Estrai) per avviare l’estrazione. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione) e fai clic su **Extract** (Estrai) per avviare la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >È presente l’opzione per sovrascrivere il contenitore di staging durante la fase di estrazione.


1. Il campo **EXTRACTION** visualizza lo stato **RUNNING** per indicare che l’estrazione è in corso.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   Una volta completata l’estrazione, lo stato del set di migrazione diventa **FINISHED** (COMPLETATO) e un’icona di nuvola *verde* viene visualizzata nel campo **INFO**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >L’interfaccia utente dispone di una funzione di ricaricamento automatico che ricarica la pagina della panoramica ogni 30 secondi.
   >Quando si avvia la fase di estrazione, viene applicato il blocco di scrittura, che viene rilasciato dopo *60 secondi*. Pertanto, se si interrompe un’estrazione, prima di riavviare l’estrazione è necessario attendere un minuto affinché il blocco venga rilasciato.

### Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.
>Inoltre, è essenziale che la struttura del contenuto esistente non venga modificata dal momento in cui l’estrazione iniziale viene portata al momento dell’esecuzione dell’estrazione integrativa. Non è possibile eseguire i top-up su contenuto la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questa limitazione durante il processo di migrazione.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione).

   >[!IMPORTANT]
   >
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >
   >![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

## Processo di acquisizione nel trasferimento dei contenuti {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione del contenuto dal set di migrazione nell’istanza del Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Acquisizione integrativa"

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Se Amazon S3 o Azure Data Store viene utilizzato come tipo di archivio dati, puoi eseguire il passaggio facoltativo di pre-copia per accelerare in modo significativo la fase di acquisizione. Per ulteriori informazioni, consulta [Acquisizione con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) .

1. Seleziona un set di migrazione dalla pagina *Overview* e fai clic su **Ingest** per avviare l’acquisizione. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione). Il contenuto può essere acquisito nell’istanza Author o Publish alla volta. Seleziona l’istanza in cui inserire il contenuto. Fai clic su **Ingest** per avviare la fase di acquisizione.

   >[!IMPORTANT]
   >Se si utilizza l’acquisizione con la pre-copia (per S3 o Azure Data Store), è consigliabile eseguire prima l’acquisizione da parte dell’autore. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >Quando l’opzione **Cancella il contenuto esistente nell’istanza Cloud prima dell’acquisizione** è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire il contenuto. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al gruppo **administrators** .

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-03.png)

   Inoltre, fai clic su **Assistenza clienti** per registrare un ticket, come mostrato nella figura precedente. Per ulteriori informazioni, consulta anche [Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) .

1. Una volta completata l’acquisizione, lo stato viene aggiornato a **FINISHED**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

### Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Per evitare di eliminare il contenuto esistente dall’attività di acquisizione precedente, disattiva l’opzione **Cancella contenuto esistente nell’istanza Cloud prima dell’acquisizione** . Inoltre, fai clic su **Assistenza clienti** per registrare un ticket, come mostrato nella figura precedente.


### Visualizzazione dei registri di un set di migrazione {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="Visualizzazione dei registri"
>abstract="Al termine dell’estrazione dell’acquisizione, controlla i registri per eventuali errori/avvisi. Eventuali errori devono essere risolti immediatamente sia affrontando i problemi segnalati sia contattando il supporto Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="Risoluzione dei problemi"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="Contattare il supporto Adobe"

Al completamento di ogni passaggio (estrazione e acquisizione) controlla i registri e cerca gli errori.  Eventuali errori devono essere risolti immediatamente sia affrontando i problemi segnalati sia contattando il supporto Adobe.

Puoi visualizzare i registri di un set di migrazione esistente nella pagina *Overview* (Panoramica).
Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione da eliminare e fai clic su **View Log** (Visualizza registro) nella barra delle azioni.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Viene visualizzata la finestra di dialogo **Logs** (Registri). Fai clic su **Extraction Logs** (Registri di estrazione) per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Oppure,

   Puoi visualizzare i registri del set di migrazione anche nella schermata *Overview* (Panoramica). Seleziona il set di migrazione e fai clic sullo stato nel campo **EXTRACTION** (ESTRAZIONE). In questo caso, fai clic su **COMPLETATO** per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Per visualizzare i registri senza utilizzare l’interfaccia utente, puoi accedere all’ambiente AEM sorgente tramite SSH e visualizzare il `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`.

### Eliminazione di un set di migrazione {#deleting-migration-set}

Puoi eliminare il set di migrazione dalla pagina *Overview* (Panoramica).
Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione da eliminare e fai clic su **Delete** (Elimina) nella barra delle azioni.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Fai clic su **Delete** (Elimina) nella finestra di dialogo **Delete Migration Set** (Elimina set di migrazione) per confermare l’eliminazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza Publish {#running-ctt-on-publish}

Durante lo spostamento del contenuto in un’istanza Publish, è consigliabile installare CTT nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Segui l’approccio consigliato come descritto di seguito:

* Utilizza la stessa versione del CTT utilizzata nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Quando crei il set di migrazione, utilizza l’URL dell’ambiente AEMaaCS di authoring.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione NON viene ridimensionato (a differenza dell’autore). Per precauzione, evitare operazioni di scrittura avviate dall’utente quali:

   * Distribuzione dei contenuti da AEMaaCS Author a Publish in tale ambiente
   * Sincronizzazione utente tra istanze di pubblicazione


## Risoluzione dei problemi {#troubleshooting}

### ID BLOB mancanti {#missing-blobs}

Se vengono segnalati degli ID BLOB mancanti, come indicato di seguito, è necessario eseguire una verifica di coerenza nell’archivio esistente e ripristinarli.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Viene eseguito il comando seguente

>[!NOTE]
>
>`--verbose` Questo flag è necessario per segnalare i percorsi dei nodi in cui si fa riferimento ai BLOB.

**Per archivi AEM 6.5 (Oak 1.8 e versioni precedenti)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Per archivi con Oak successivo alla versione 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Per ulteriori informazioni, consulta [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run).

I file creati per coerenza nel percorso *OUT_DIR* indicato sopra possono quindi essere controllati per individuare percorsi con binary mancanti e possono essere intraprese azioni appropriate come il ripristino da un backup, l’eliminazione dei percorsi, la reindicizzazione e così via.


### Comportamento dell’interfaccia {#ui-behavior}

Come utente, nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) potresti osservare le seguenti modifiche comportamentali:

* Le icone nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) possono apparire diverse dalle schermate mostrate in questa guida o possono non apparire affatto, a seconda della versione dell’istanza AEM sorgente.
