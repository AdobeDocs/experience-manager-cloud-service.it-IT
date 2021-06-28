---
title: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: d08fc076306c54f8551c9df499efa0ded7bcc131
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 40%

---

# Utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#using-content-transfer-tool}

## Valutazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)  {#pre-reqs}

Segui le indicazioni riportate in questa sezione per comprendere le valutazioni importanti durante l’esecuzione dello strumento Content Transfer (Trasferimento contenuti):

* l requisiti di sistema minimi per lo strumento Content Transfer (Trasferimento contenuti) sono AEM 6.3 o versione successiva e JAVA 8. Se si utilizza una versione AEM inferiore, è necessario aggiornare l’archivio dei contenuti a AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Java deve essere configurato nell&#39;ambiente AEM in modo che il comando `java` possa essere eseguito dall&#39;utente che avvia AEM.

* Si consiglia di disinstallare le versioni precedenti dello strumento Content Transfer (Trasferimento contenuti) durante l’installazione della versione 1.3.0, in quanto lo strumento ha subito una modifica importante dell’architettura. Con la versione 1.3.0, devi anche creare nuovi set di migrazione ed eseguire nuovamente l’estrazione e l’acquisizione sui nuovi set di migrazione.

* Lo strumento Content Transfer (Trasferimento contenuti) può essere utilizzato con i seguenti tipi di archivio dati: Archivio dati file, archivio dati S3, archivio dati S3 condiviso e archivio dati Azure Blob.

* Se utilizzi un *ambiente Sandbox*, assicurati che l’ambiente sia corrente e aggiornato alla versione più recente. Se utilizzi un *ambiente di produzione*, viene aggiornato automaticamente.

* Per utilizzare lo strumento Content Transfer (Trasferimento contenuti), devi essere un utente amministratore nell’istanza sorgente e appartenere al gruppo di AEM **amministratori** nell’istanza di Cloud Service a cui stai trasferendo i contenuti. Gli utenti non autorizzati non potranno recuperare il token di accesso per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Se l’impostazione **Cancella il contenuto esistente nell’istanza Cloud prima dell’acquisizione** è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire il contenuto. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al gruppo **administrators** . Per recuperare il token di accesso per CTT, è necessario che l’utente sia aggiunto nuovamente al gruppo **administrators** .

* Il token di accesso può scadere periodicamente dopo un determinato periodo di tempo o dopo l’aggiornamento dell’ambiente di Cloud Service. Se il token di accesso è scaduto, non sarà possibile connettersi all’istanza di Cloud Service e sarà necessario recuperare il nuovo token di accesso. L’icona di stato associata a un set di migrazione esistente si trasforma in un cloud rosso e viene visualizzato un messaggio al passaggio del mouse.

* Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferire il contenuto dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione di contenuto in un ambiente di pubblicazione. Qualsiasi contenuto sia specificato nel set di migrazione verrà acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author o Publish o in entrambe. Si consiglia di installare CTT durante lo spostamento del contenuto in un’istanza Production nell’istanza Author di origine per spostare il contenuto nell’istanza Author di destinazione e, allo stesso modo, di installare CTT nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione.

* Gli utenti e i gruppi trasferiti dallo strumento Content Transfer (Trasferimento contenuti) sono solo quelli richiesti dal contenuto per soddisfare le autorizzazioni. Il processo *Estrazione* copia l&#39;intero `/home` nel set di migrazione e il processo *Acquisizione* copia tutti gli utenti e i gruppi a cui si fa riferimento nelle ACL del contenuto migrato. Per mappare automaticamente gli utenti e i gruppi esistenti ai loro ID IMS, fai riferimento a [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante la fase di estrazione, lo strumento Content Transfer (Trasferimento contenuti) viene eseguito su un’istanza sorgente di AEM attiva.

* Dopo aver completato la fase *Estrazione* del processo di trasferimento dei contenuti e prima di avviare la fase di acquisizione *Ingestion* per acquisire contenuti nel AEM come Cloud Service *Stage* o *Produzione*, dovrai registrare un ticket di supporto per notificare all&#39;Adobe l&#39;intenzione di eseguire *Acquisizione&lt;a7 a9/> in modo che l&#39;Adobe possa garantire che non si verifichino interruzioni durante il processo* Ingestion *.* Sarà necessario registrare il ticket di supporto 1 settimana prima della data *di acquisizione* pianificata. Dopo aver inviato il ticket di assistenza, il team di supporto fornirà indicazioni sui passaggi successivi. Puoi registrare un ticket di supporto con i seguenti dettagli:

   * Data esatta e ora stimata (con il tuo fuso orario) quando intendi avviare la fase *Acquisizione*.
   * Tipo di ambiente (Stage o Produzione) in cui si intende inserire i dati.
   * ID programma.

* La *fase di acquisizione* per l’autore riduce l’intera distribuzione dell’autore. Questo significa che l’istanza di authoring di AEM non sarà disponibile durante l’intero processo di acquisizione. Assicurati anche che nessuna pipeline di Cloud Manager venga eseguita durante la fase *Acquisizione*.

* Quando utilizzi `Amazon S3` o `Azure` come archivio dati nel sistema di AEM di origine, l’archivio dati deve essere configurato in modo che i BLOB memorizzati non possano essere eliminati (raccolta rifiuti). In questo modo si garantisce l&#39;integrità dei dati dell&#39;indice e la mancata configurazione di questo modo può causare estrazioni non riuscite a causa della mancanza di integrità dei dati dell&#39;indice.

* Se utilizzi indici personalizzati, assicurati di configurare gli indici personalizzati con il nodo `tika` prima di eseguire lo strumento Content Transfer (Trasferimento contenuti). Per ulteriori informazioni, consulta [Preparazione della nuova definizione di indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) .

* Se intendi eseguire operazioni di integrazione, è essenziale che la struttura del contenuto del contenuto esistente non venga modificata dal momento in cui l’estrazione iniziale viene portata al momento dell’esecuzione dell’estrazione integrativa. Non è possibile eseguire i top-up su contenuto la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questa limitazione durante il processo di migrazione.

## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Scarica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Note sulla versione"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portale di distribuzione software"

Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente. Per ulteriori informazioni sull&#39;ultima versione, consulta [Note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti)  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Esecuzione dello strumento Content Transfer (Trasferimento contenuti)"
>abstract="Scopri come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM come Cloud Service (authoring/pubblicazione)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Vedere Demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial: utilizzo dello strumento Content Transfer (Trasferimento contenuti)"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Segui le indicazioni contenute in questa sezione per apprendere come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione):

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. Seleziona l’opzione **Trasferimento contenuti** dalla procedura guidata **Migrazione contenuti**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. La console seguente viene visualizzata quando crei il primo set di migrazione. Fai clic su **Create Migration Set** (Crea set di migrazione) per creare un nuovo set di migrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >Se disponi di set di migrazione esistenti, nella console viene visualizzato l’elenco dei set di migrazione esistenti con il relativo stato corrente.

   Inoltre, fai clic su **Crea configurazione di mappatura utente** per accedere allo [strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).

1. Compila i campi nella schermata **Crea set di migrazione** come descritto di seguito.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **Name** (Nome): inserisci il nome del set di migrazione.
      >[!NOTE]
      >Il nome del set di migrazione non può contenere caratteri speciali.

   1. **Cloud Service Configuration** (Configurazione Cloud Service): inserisci l’URL dell’istanza di authoring di AEM as a Cloud Service di destinazione.

      >[!NOTE]
      >Puoi creare e mantenere un massimo di dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
      >Inoltre, è necessario creare separatamente una migrazione per ciascun ambiente: *Stage*, *Sviluppo* o *Produzione*.

   1. **Access Token** (Token di accesso): inserisci il token di accesso.

      >[!NOTE]
      >Puoi recuperare il token di accesso utilizzando il pulsante **Open access token** . Devi accertarti di appartenere al gruppo di amministratori di AEM nell’istanza di Cloud Service di destinazione.

   1. **Parameters** (Parametri): seleziona i seguenti parametri per creare il set di migrazione:

      1. **Include Version** (Includi versione): seleziona in base alle esigenze.

      1. **Includi mapping da utenti e gruppi** IMS: Seleziona l’opzione per includere la mappatura da utenti e gruppi IMS.
Per ulteriori informazioni, consulta [Strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) .

      1. **Paths to be included** (Percorsi da includere): utilizza il browser percorsi per selezionare i percorsi interessati dalla migrazione. Il selettore del percorso accetta l’input digitando o selezionando.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alcuni  `/etc` percorsi possono essere selezionati in CTT)


1. Fai clic su **Salva** dopo aver compilato tutti i campi nella schermata dei dettagli **Crea set di migrazione** .

1. Il set di migrazione verrà visualizzato nella pagina *Overview* (Panoramica).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Tutti i set di migrazione esistenti in questa schermata vengono visualizzati nella pagina *Panoramica* con il relativo stato corrente e le informazioni sullo stato. Puoi vedere alcune di queste icone descritte di seguito.

   * Una *nuvola rossa* indica che non puoi completare il processo di estrazione.
   * Una *nuvola verde* indica che puoi completare il processo di estrazione.
   * Un’*icona gialla* indica che non hai creato il set di migrazione esistente e che quello specifico è stato creato da un altro utente nella stessa istanza.

1. Seleziona un set di migrazione dalla pagina della panoramica e fai clic su **Properties** (Proprietà) per visualizzare o modificare le proprietà del set di migrazione. Durante la modifica delle proprietà, non è possibile modificare il nome del contenitore o l&#39;URL del servizio.


### Processo di estrazione nel trasferimento dei contenuti {#extraction-process}

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

#### Estrazione integrativa {#top-up-extraction-process}

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

### Processo di acquisizione nel trasferimento dei contenuti {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione del contenuto dal set di migrazione nell’istanza del Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Acquisizione integrativa"

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Se Amazon S3 o Azure Data Store viene utilizzato come tipo di archivio dati, puoi eseguire il passaggio facoltativo di pre-copia per accelerare in modo significativo la fase di acquisizione. Per ulteriori informazioni, consulta [Acquisizione con AzCopy] .

1. Seleziona un set di migrazione dalla pagina *Overview* e fai clic su **Ingest** per avviare l’acquisizione. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione). Fai clic su **Ingest** per avviare la fase di acquisizione. È possibile acquisire contemporaneamente contenuti nelle istanze di authoring e di pubblicazione.

   >[!IMPORTANT]
   >Se si utilizza l’acquisizione con la pre-copia (per S3 o Azure Data Store), è consigliabile eseguire prima l’acquisizione da parte dell’autore. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >Quando l’opzione **Cancella il contenuto esistente nell’istanza Cloud prima dell’acquisizione** è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire il contenuto. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al gruppo **administrators** .

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   Inoltre, fai clic su **Assistenza clienti** per registrare un ticket, come mostrato nella figura precedente. Per ulteriori informazioni, consulta anche [Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs) .

1. Una volta completata l&#39;acquisizione, lo stato nel campo **PUBLISH INGESTION** viene aggiornato a **FINISHED**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

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
