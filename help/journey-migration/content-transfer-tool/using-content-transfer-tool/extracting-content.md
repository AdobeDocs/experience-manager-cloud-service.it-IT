---
title: Estrazione del contenuto dall’origine
description: Scopri come estrarre il contenuto da un’istanza Adobe Experience Manager (AEM) di origine per trasferirlo successivamente a un’istanza AEM di Cloud Service.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: d568619bd8ebb42a6914211401df680352c921ab
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 17%

---

# Estrazione del contenuto dall’origine {#extracting-content}

## Processo di estrazione nello strumento di trasferimento contenuti {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Estrazione dei contenuti"
>abstract="Per estrazione si intende l’estrazione dei contenuti dall’istanza AEM di origine di Adobe Experience Manager in un’area temporanea denominata set di migrazione. Un set di migrazione è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it#top-up-extraction-process" text="Estrazione integrativa"


Per estrarre il set di migrazione dallo strumento di trasferimento contenuti, effettua le seguenti operazioni:

>[!NOTE]
>Se come tipo di archivio dati viene utilizzato Amazon S3, Azure Data Store o File Data Store, puoi eseguire il passaggio di pre-copia facoltativo per aumentare la velocità della fase di estrazione. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione complete. Per ulteriori dettagli, consulta [Gestione di archivi di contenuti di grandi dimensioni](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md).

1. Seleziona un set di migrazione dalla procedura guidata **Trasferimento contenuti** e fai clic su **Estrai** per avviare l&#39;estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Ora è possibile pianificare l’avvio automatico di un’acquisizione subito dopo la riuscita di un’estrazione. Per ulteriori informazioni, vedere [Inserimento di contenuto in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

   >[!IMPORTANT]
   >
   >Assicurati che la chiave di estrazione sia valida e non vicina alla scadenza. Se è vicina alla data di scadenza, puoi rinnovare il tasto Estrazione selezionando il set di migrazione e facendo clic su Proprietà. Fare clic su **Rinnova**. Viene visualizzato il Cloud Acceleration Manager in cui è possibile fare clic su **Copia chiave di estrazione**. Ogni volta che si fa clic su **Copia chiave di estrazione**, viene generata una nuova chiave di estrazione valida per 14 giorni dalla creazione.
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetDetails.png)

1. Viene visualizzata la finestra di dialogo Estrazione. Fai clic su **Estrai** per avviare la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/migrationSetExtraction.png)

   >[!NOTE]
   >Facoltativamente, puoi sovrascrivere il contenitore di staging durante la fase di estrazione. Se **Sovrascrivi contenitore di staging** è disabilitato, le estrazioni per le migrazioni successive in cui i percorsi di contenuto o le impostazioni delle versioni di inclusione non sono stati modificati possono essere più rapide. Tuttavia, se le impostazioni dei percorsi di contenuto o delle versioni di inclusione sono state modificate, **Sovrascrivi contenitore di staging** deve essere abilitato.

1. Nel campo **Estrazione** viene ora visualizzato lo stato **IN ESECUZIONE** per indicare che l&#39;estrazione è in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Puoi fare clic su **Visualizza avanzamento** per ottenere una visualizzazione granulare dell&#39;estrazione in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/viewProgress.png)

   È inoltre possibile monitorare l&#39;avanzamento della fase di estrazione da Cloud Acceleration Manager visitando la pagina Content Transfer (Trasferimento contenuti) e visualizzarla in modo più dettagliato facendo clic su **...** > **Visualizza dettagli**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Al termine dell&#39;estrazione, esaminare le altre colonne come **Source** e **Paths** per i dettagli del set di migrazione popolato. Fai clic su **...** > **Visualizza dettagli** per visualizzare i dettagli, inclusa la durata di ogni passaggio dell&#39;estrazione. Visualizza questa finestra di dialogo durante l’estrazione per vedere come procedono i passaggi.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Estrazione integrativa {#top-up-extraction-process}

Lo strumento di trasferimento contenuti dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima estrazione completa, puoi saltare la pre-copia per le successive estrazioni integrative (se la dimensione del set di migrazione integrativo è inferiore a 200 GB). Il motivo è che potrebbe aggiungere tempo all&#39;intero processo.
>&#x200B;>Inoltre, è essenziale che la struttura del contenuto esistente non venga modificata dal momento in cui viene effettuata l’estrazione iniziale a quello in cui viene eseguita l’estrazione integrativa. I top-up non possono essere eseguiti su contenuti la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questo passaggio durante il processo di migrazione.

>[!NOTE]
>Dopo la migrazione dei percorsi di contenuto al contenitore di staging, non è possibile rimuovere o escludere tali percorsi o eventuali percorsi secondari al loro interno dalle migrazioni integrative successive.
>&#x200B;>Esempio: Migrazione iniziale: content/dam/weRetail,
>&#x200B;>Prossimo tentativo di esclusione integrativa: content/dam/weRetail/ab.
>&#x200B;>In questo scenario, l’esclusione di contenuto/dam/weRetail/ab non è possibile perché i dati sono già stati migrati nel contenitore di staging.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa.

Effettua le seguenti operazioni:

1. Passare alla procedura guidata **Trasferimento contenuti** e selezionare il set di migrazione per il quale si desidera eseguire l&#39;estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione). Fai clic su **Estrai**.

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/overwriteStagingContainer.png)


## Passaggio successivo {#whats-next}

Dopo aver appreso l’estrazione dei contenuti da Source nello strumento Content Transfer (Trasferimento contenuti), ora puoi imparare il processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti). Consulta [Acquisizione del contenuto in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per scoprire come acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
