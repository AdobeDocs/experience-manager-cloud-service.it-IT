---
title: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 91%

---


# Utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#using-content-transfer-tool}

## Valutazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#pre-reqs}

Segui le indicazioni riportate in questa sezione per comprendere le valutazioni importanti durante l’esecuzione dello strumento Content Transfer (Trasferimento contenuti):

* l requisiti di sistema minimi per lo strumento Content Transfer (Trasferimento contenuti) sono AEM 6.3 o versione successiva e JAVA 8. Se utilizzi una precedente versione di AEM, dovrai aggiornare l’archivio dei contenuti ad AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* If you are using a *Sandbox Environment*, ensure that your environment is upgraded to June 10 2020 Release or later. Se utilizzi un *ambiente di produzione*, viene aggiornato automaticamente.

* Per utilizzare lo strumento di trasferimento dei contenuti, devi essere un utente amministratore nell’istanza di origine e appartenere al gruppo di amministratori AEM nell’istanza di Cloud Service a cui trasferisci i contenuti. Gli utenti non autorizzati non potranno recuperare il token di accesso per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Durante la fase di estrazione, lo strumento Content Transfer (Trasferimento contenuti) viene eseguito su un’istanza sorgente di AEM attiva.

* La *fase di acquisizione* per l’istanza di authoring riduce l’intera implementazione di authoring. Questo significa che l’istanza di authoring di AEM non sarà disponibile durante l’intero processo di acquisizione.

* Il limite superiore consigliato per la dimensione del repository supportata da Content Transfer Tool per volta è di 20 GB.

## Disponibilità {#availability}

Content Transfer Tool può essere scaricato come file zip (Content Transfer Tool v1.0.0) dal portale di distribuzione del software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM).

>[!NOTE]
>Scaricate Content Transfer Tool dal portale [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) .

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti) {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)

Segui le indicazioni contenute in questa sezione per apprendere come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione):

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Content Transfer** (Trasferimento contenuti).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Fai clic su **Create Migration Set** (Crea set di migrazione) per creare un nuovo set di migrazione. Vengono visualizzati i **Content Migrations Set details** (Dettagli set di migrazione contenuti).

   >[!NOTE]
   >In questa schermata vengono visualizzati i set di migrazione esistenti e il relativo stato corrente.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Compila i campi nella schermata **Content Migrations Set details** (Dettagli set di migrazione contenuti) come descritto di seguito.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Name** (Nome): inserisci il nome del set di migrazione.
      >[!NOTE]
      >Il nome del set di migrazione non può contenere caratteri speciali.

   1. **Cloud Service Configuration** (Configurazione Cloud Service): inserisci l’URL dell’istanza di authoring di AEM as a Cloud Service di destinazione.

      >[!NOTE]
      >Puoi creare e mantenere un massimo di quattro set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
      >Inoltre, è necessario creare separatamente una migrazione per ciascun ambiente: *Stage*, *Sviluppo* o *Produzione*.

   1. **Access Token** (Token di accesso): inserisci il token di accesso.

      >[!NOTE]
      >Puoi recuperare il token di accesso dell’istanza di authoring in `/libs/granite/migration/token.json`. Il token di accesso viene recuperato dall’istanza di creazione di Cloud Service.

   1. **Parameters** (Parametri): seleziona i seguenti parametri per creare il set di migrazione:

      1. **Include Version** (Includi versione): seleziona in base alle esigenze.

      1. **Paths to be included** (Percorsi da includere): utilizza il browser percorsi per selezionare i percorsi interessati dalla migrazione.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Fai clic su **Save** (Salva) dopo aver compilato tutti i campi nella schermata **Content Migrations Set details** (Dettagli set di migrazione contenuti).

1. Il set di migrazione verrà visualizzato nella pagina *Overview* (Panoramica).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Tutti i set di migrazione esistenti in questa schermata vengono visualizzati nella pagina *Overview* (Panoramica) con il relativo stato corrente e le informazioni sullo stato.

   * Una *nuvola rossa* indica che non puoi completare il processo di estrazione.
   * Una *nuvola verde* indica che puoi completare il processo di estrazione.
   * Un’*icona gialla* indica che non hai creato il set di migrazione esistente e che quello specifico è stato creato da un altro utente nella stessa istanza.

1. Seleziona un set di migrazione dalla pagina della panoramica e fai clic su **Properties** (Proprietà) per visualizzare o modificare le proprietà del set di migrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Processo di estrazione nel trasferimento dei contenuti {#extraction-process}

Per estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:

1. Seleziona un set di migrazione dalla pagina *Overview* (Panoramica) e fai clic su **Extract** (Estrai) per avviare l’estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione). Fai clic su **Extract** (Estrai) per completare la fase di estrazione.

   >[!NOTE]
   >È presente l’opzione per sovrascrivere il contenitore di staging durante la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. Nel campo **EXTRACTION** (ESTRAZIONE) ora viene visualizzato lo stato **RUNNING** (IN ESECUZIONE) per il processo di estrazione in corso.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Una volta completata l’estrazione, lo stato del set di migrazione diventa **FINISHED** (COMPLETATO) e un’icona di nuvola *verde* viene visualizzata nel campo **INFO**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Per visualizzare lo stato aggiornato, aggiorna la pagina.
   >Quando si avvia la fase di estrazione, viene applicato il blocco di scrittura, che viene rilasciato dopo *60 secondi*. Pertanto, se si interrompe un’estrazione, prima di riavviare l’estrazione è necessario attendere un minuto affinché il blocco venga rilasciato.

#### Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’estrazione integrativa.

1. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione).

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Processo di acquisizione nel trasferimento dei contenuti {#ingestion-process}

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:

1. Seleziona un set di migrazione dalla pagina *Overview* (Panoramica) e fai clic su **Ingest** (Acquisisci) per avviare l’acquisizione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   A scopo dimostrativo, l’opzione **Ingest content to Author instance** (Acquisisci contenuto nell’istanza di authoring) è disabilitata. È possibile acquisire contemporaneamente contenuti nelle istanze di authoring e di pubblicazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Fai clic su **Ingest** (Acquisisci) per completare la fase di acquisizione.

1. Una volta completata l’acquisizione, lo stato nel campo **UTHOR INGESTION** (ACQUISIZIONE AUTHORING) diventa **FINISHED** (COMPLETATO) e sotto **INFO** viene visualizzata l’icona di una nuvola verde.
   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Per visualizzare lo stato aggiornato, aggiorna la pagina.

#### Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* dei contenuti differenziali per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa.

1. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   >[!NOTE]
   >Per evitare di eliminare i contenuti esistenti dell’attività di acquisizione precedente, disattiva l’opzione *Wipe* (Cancella).
   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visualizzazione dei registri di un set di migrazione {#viewing-logs-migration-set}

Puoi visualizzare i registri di un set di migrazione esistente nella pagina *Overview* (Panoramica).
Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione da eliminare e fai clic su **View Log** (Visualizza registro) nella barra delle azioni.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Viene visualizzata la finestra di dialogo **Logs** (Registri). Fai clic su **Extraction Logs** (Registri di estrazione) per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
Oppure,

   Puoi visualizzare i registri del set di migrazione anche nella schermata *Overview* (Panoramica). Seleziona il set di migrazione e fai clic sullo stato nel campo **EXTRACTION** (ESTRAZIONE). In questo caso, fai clic su **COMPLETATO** per visualizzare i registri in una nuova scheda.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. Per limitare i file di registro senza utilizzare l’interfaccia utente, puoi effettuare la SSH nell’ambiente AEM di origine e impostare le `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`dimensioni finali.

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
> `--verbose` Questo flag è necessario per segnalare i percorsi dei nodi in cui si fa riferimento ai BLOB.

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

* L’utente crea un set di migrazione per un URL di authoring (Sviluppo/Stage/Produzione) ed esegue correttamente l’estrazione e l’acquisizione.

* L’utente crea quindi un nuovo set di migrazione per lo stesso URL di authoring ed esegue l’estrazione e l’acquisizione nel nuovo set di migrazione. Nell’interfaccia lo stato di acquisizione del primo set di migrazione diventa **FAILED** (NON RIUSCITO) e non sono disponibili registri.

* Ciò non significa che l’acquisizione del primo set di migrazione non sia riuscita. Si osserva questo comportamento perché all’avvio di un nuovo processo di acquisizione viene eliminato il processo di acquisizione precedente. Pertanto, lo stato delle modifiche del primo set di migrazione deve essere ignorato.

* Le icone nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) possono apparire diverse dalle schermate mostrate in questa guida o possono non apparire affatto, a seconda della versione dell’istanza AEM sorgente.


