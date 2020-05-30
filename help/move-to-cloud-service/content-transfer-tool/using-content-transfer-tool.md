---
title: Utilizzo dello strumento di trasferimento dei contenuti
description: Utilizzo dello strumento di trasferimento dei contenuti
translation-type: tm+mt
source-git-commit: f154ffacbeeee1993a9cc3bd3bd274be33dca7a7
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 1%

---


# Utilizzo dello strumento di trasferimento dei contenuti {#using-content-transfer-tool}

## Considerazioni importanti sull&#39;utilizzo dello strumento di trasferimento dei contenuti {#pre-reqs}

Seguite la sezione seguente per comprendere le considerazioni importanti durante l&#39;esecuzione dello strumento di trasferimento dei contenuti:

* Il requisito minimo di sistema per lo strumento di trasferimento dei contenuti è AEM 6.3 + e JAVA 8. Se si utilizza una versione di AEM inferiore, sarà necessario aggiornare l’archivio dei contenuti ad AEM 6.5 per utilizzare lo strumento di trasferimento dei contenuti.

* Se utilizzate un ambiente *sandbox*, accertatevi che l&#39;ambiente sia aggiornato alla versione del 29 maggio 2020 o successiva. Se si utilizza un ambiente *di* produzione, questo viene aggiornato automaticamente.

* Per utilizzare lo strumento di trasferimento dei contenuti, è necessario essere un utente amministratore nell&#39;istanza di origine e appartenere al gruppo di amministrazione nell&#39;istanza del servizio cloud a cui si sta trasferendo il contenuto. Gli utenti non privilegiati non potranno recuperare il token di accesso per utilizzare lo strumento di trasferimento dei contenuti.

* Durante la fase di estrazione, lo strumento di trasferimento dei contenuti viene eseguito su un’istanza sorgente AEM attiva.

* La fase *di* inserimento dell’autore riduce l’intera distribuzione dell’autore. Questo significa che l’autore AEM non sarà disponibile durante l’intero processo di assimilazione.

## Disponibilità {#availability}

Content Transfer Tool può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Package Manager nella tua istanza sorgente Adobe Experience Manager (AEM).

>[!NOTE]
>Scarica Content Transfer Tool da [Adobe Experience Cloud](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Esecuzione dello strumento di trasferimento dei contenuti {#running-tool}

Seguite questa sezione per apprendere come utilizzare lo strumento di trasferimento dei contenuti per migrare il contenuto in AEM come servizio cloud (Autore/Pubblica):

1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Trasferimento** contenuti.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. Fate clic su **Crea set** di migrazione per creare un nuovo set di migrazione. Vengono visualizzati i dettagli **del set di migrazioni dei** contenuti.

   >[!NOTE]
   >I set di migrazione esistenti verranno visualizzati su questa schermata con il relativo stato corrente.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. Compilate i campi nella schermata Dettagli **set di migrazioni dei** contenuti, come descritto di seguito.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **Nome**: Immettere il nome del set di migrazione.
      >[!NOTE]
      >Non sono consentiti caratteri speciali per il nome del set di migrazione.

   1. **Configurazione** servizio cloud: Immettete AEM di destinazione come URL di Cloud Service Author.

      >[!NOTE]
      >Potete creare e mantenere un massimo di quattro set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
      >Inoltre, è necessario creare una migrazione separatamente per ciascuno degli ambienti specifici: *Stage*, *Sviluppo* o *Produzione*.

   1. **Token** di accesso: Immettete il token di accesso.

      >[!NOTE]
      >Per recuperare il token di accesso dall’istanza di creazione, passate a `/libs/granite/migration/token.json`.

   1. **Parametri**: Selezionate i seguenti parametri per creare il set di migrazione:

      1. **Includi versione**: Selezionate come necessario.

      1. **Percorsi da includere**: Utilizza il browser dei percorsi per selezionare i percorsi per i quali è necessario eseguire la migrazione.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. Fate clic su **Salva** dopo aver compilato tutti i campi nella schermata Dettagli **set di migrazioni** contenuto.

1. Il set di migrazione verrà visualizzato nella pagina *Panoramica* .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   Tutti i set di migrazione esistenti in questa schermata vengono visualizzati nella pagina *Panoramica* con le informazioni sullo stato e lo stato correnti.

   * Una nuvola ** rossa indica che non è possibile completare il processo di estrazione.
   * Una nuvola ** verde indica che è possibile completare il processo di estrazione.
   * Un&#39;icona ** gialla indica che non è stato creato il set di migrazione esistente e quello specifico viene creato da un altro utente nella stessa istanza.

1. Selezionate un set di migrazione dalla pagina della panoramica e fate clic su **Proprietà** per visualizzare o modificare le proprietà del set di migrazione.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### Processo di estrazione nel trasferimento dei contenuti {#extraction-process}

Per estrarre il set di migrazione dallo strumento di trasferimento dei contenuti, effettuate le seguenti operazioni:

1. Selezionate un set di migrazione dalla pagina *Panoramica* e fate clic su **Estrai** per avviare l’estrazione.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Viene visualizzata la finestra di dialogo di estrazione **del set di** migrazione e fate clic su **Estrai** per completare la fase di estrazione.

   >[!NOTE]
   >È possibile sovrascrivere il contenitore di staging durante la fase di estrazione.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. Il campo **EXTRACTION** ora visualizza lo stato **RUNNING** per il processo di estrazione in corso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   Una volta completata l&#39;estrazione, lo stato del set di migrazione si aggiorna a **FINISHED** e un&#39;icona *solida verde* cloud viene visualizzata sotto il campo **INFO** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >Sarà necessario aggiornare la pagina per visualizzare lo stato aggiornato.
   >Quando si avvia la fase di estrazione, viene creato il blocco di scrittura e rilasciato dopo *60 secondi*. Quindi, se si arresta un&#39;estrazione, è necessario attendere un minuto prima che il blocco venga rilasciato prima di riavviare l&#39;estrazione.

#### Estrazione In Alto {#top-up-extraction-process}

Content Transfer Tool dispone di una funzione che supporta l&#39;integrazione dei contenuti differenziali dove è possibile trasferire solo le modifiche apportate dall&#39;attività di trasferimento dei contenuti precedente.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti aggiunte differenziali per ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali prima di iniziare a utilizzare il servizio Cloud.

Una volta completato il processo di estrazione, potete trasferire il contenuto delta utilizzando il metodo di estrazione dall’alto. Effettuate le seguenti operazioni:

1. Passate alla pagina *Panoramica* e selezionate il set di migrazione per il quale desiderate eseguire l&#39;estrazione dall&#39;alto.

1. Fate clic su **Estrai** per avviare l’estrazione dall’alto.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. Viene visualizzata la finestra di dialogo di estrazione **del set di** migrazione.

   >[!IMPORTANT]
   >È consigliabile disattivare l&#39;opzione **Sovrascrivi contenitore di staging durante l&#39;estrazione** .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### Processo di inserimento nel trasferimento dei contenuti {#ingestion-process}

Seguite i passaggi indicati di seguito per assimilare il set di migrazione dallo strumento di trasferimento dei contenuti:

1. Selezionate un set di migrazione dalla pagina *Panoramica* e fate clic su **Assegna** per avviare l’estrazione.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Viene visualizzata la finestra di dialogo di assimilazione del set di **migrazione** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   A scopo dimostrativo, l&#39;opzione **Assegna contenuto all&#39;istanza** Autore è disabilitata. È possibile caricare contemporaneamente contenuti su Autore e Pubblica.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   Fate clic su **Assegna** per completare la fase di assimilazione.

1. Una volta completata l&#39;assimilazione, lo stato nel campo **AUTHOR INGESTION** si aggiorna a **FINISHED** e sotto **INFO**viene visualizzata un&#39;icona di nuvola verde.
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > Sarà necessario aggiornare la pagina per visualizzare lo stato aggiornato.

#### Ingestione superiore {#top-up-ingestion-process}

Content Transfer Tool dispone di una funzione che supporta l&#39; *integrazione* dei contenuti differenziali dove è possibile trasferire solo le modifiche apportate dall&#39;attività di trasferimento dei contenuti precedente.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti aggiunte differenziali per ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali prima di iniziare a utilizzare il servizio Cloud.

Una volta completato il processo di assimilazione, potete utilizzare il contenuto delta, utilizzando il metodo di inserimento top-up. Effettuate le seguenti operazioni:

1. Passate alla pagina *Panoramica* e selezionate il set di migrazione per il quale desiderate eseguire l&#39;assimilazione superiore.

1. Fate clic su **Assegna** per avviare l’estrazione dall’alto.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. Viene visualizzata la finestra di dialogo **Migrazione impostazione inserimento** .

   >[!NOTE]
   >Per evitare di eliminare il contenuto esistente dall’attività di assimilazione precedente, disattivate l’opzione *Comparsa* .
   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### Visualizzazione dei registri per un set di migrazione {#viewing-logs-migration-set}

Puoi visualizzare i registri di un set di migrazione esistente dalla pagina *Panoramica* .
Effettuate le seguenti operazioni:

1. Passate alla pagina *Panoramica* e selezionate il set di migrazione da eliminare, quindi fate clic su **Visualizza registro** dalla barra delle azioni.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. Viene visualizzata la finestra di dialogo **Registri** . Fate clic su Registri **** estrazione per visualizzare i registri in una nuova scheda.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)Or,

   Dalla schermata *Panoramica* potete anche visualizzare i registri per il set di migrazione. Selezionate il set di migrazione e fate clic sullo stato sotto il campo **EXTRACTION** . In questo caso, fare clic su **FINISHED** per visualizzare i registri in una nuova scheda.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### Eliminazione di un set di migrazione {#deleting-migration-set}

Puoi eliminare il set di migrazione dalla pagina *Panoramica* .
Effettuate le seguenti operazioni:

1. Andate alla pagina *Panoramica* e selezionate il set di migrazione da eliminare, quindi fate clic su **Elimina** dalla barra delle azioni.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. Fate clic su **Elimina** dalla finestra di dialogo **Elimina set** di migrazione per confermare l’eliminazione.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## Risoluzione dei problemi {#troubleshooting}

### ID BLOB mancanti {#missing-blobs}

Se mancano ID BLOB segnalati, come indicato di seguito, è necessario eseguire una verifica di coerenza nel repository esistente e ripristinare i BLOB mancanti.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Viene eseguito il comando seguente

>[!NOTE]
> `--verbose` è necessario per segnalare i percorsi dei nodi da cui si fa riferimento alle BLOB.

**Per i repository AEM 6.5 (Oak 1.8 e versioni successive)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Per i repository con Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Per ulteriori informazioni, fare riferimento a [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) .

I file creati in *OUT_DIR* sopra per coerenza possono quindi essere controllati per individuare percorsi binari mancanti e azioni appropriate, come il ripristino da un backup, l&#39;eliminazione dei percorsi, il reindicizzazione e così via.

### Comportamento interfaccia utente {#ui-behavior}

Come utente, nell’interfaccia utente (UI) di Content Transfer Tool potrebbero essere visualizzate le seguenti modifiche comportamentali:

* L’utente crea un set di migrazione per un URL autore (Sviluppo/Fase/Produzione) ed esegue correttamente l’estrazione e l’assimilazione.

* L’utente crea quindi un nuovo set di migrazione per lo stesso URL autore ed esegue l’estrazione e l’inserimento nel nuovo set di migrazione. L’interfaccia utente mostra che lo stato di inserimento del primo set di migrazione cambia in **NON RIUSCITO** e non sono disponibili registri.

* Ciò non significa che l&#39;assimilazione del primo set di migrazione non sia riuscita. Questo comportamento è visibile perché all’avvio di un nuovo processo di assimilazione viene eliminato il processo di assimilazione precedente. Pertanto, lo stato delle modifiche nel primo set di migrazione deve essere ignorato.

* Le icone nell’interfaccia utente dello strumento di trasferimento dei contenuti possono apparire diverse dalle schermate mostrate in questa guida o non vengono visualizzate a seconda della versione dell’istanza AEM di origine.


