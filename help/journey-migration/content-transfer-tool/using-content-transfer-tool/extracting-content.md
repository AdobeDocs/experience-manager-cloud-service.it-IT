---
title: Estrazione del contenuto dall’origine
description: Scopri come estrarre il contenuto da un’istanza Adobe Experience Manager (AEM) di origine per trasferirlo successivamente a un’istanza AEM di Cloud Service.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 44a3f3c4ca08cffa06056ea85adc58e3cf1f2f1c
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 25%

---

# Estrazione del contenuto dall’origine {#extracting-content}

## Processo di estrazione nello strumento Content Transfer {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Estrazione dei contenuti"
>abstract="Per estrazione si intende l’estrazione dei contenuti dall’istanza Adobe Experience Manager (AEM) di origine in un’area temporanea denominata set di migrazione. Un set di migrazione è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it#top-up-extraction-process" text="Estrazione integrativa"


Per estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:

>[!NOTE]
>Se come tipo di archivio dati viene utilizzato Amazon S3, Azure Data Store o File Data Store, puoi eseguire il passaggio di pre-copia facoltativo per aumentare la velocità della fase di estrazione. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione complete. Consulta [Gestione di archivi di contenuti di grandi dimensioni](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per ulteriori dettagli.

1. Seleziona un set di migrazione da **Trasferimento dei contenuti** e fai clic su **Extract** per avviare l’estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >Assicurati che la chiave di estrazione sia valida e non vicina alla scadenza. Se è vicina alla data di scadenza, puoi rinnovare il tasto Estrazione selezionando il set di migrazione e facendo clic su Proprietà. Clic **Rinnova**. Viene visualizzato Cloud Acceleration Manager, su cui è possibile fare clic **Copia chiave di estrazione**. Ogni volta che fai clic su **Copia chiave di estrazione**, viene generata una nuova chiave di estrazione valida per 14 giorni dalla creazione.
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Viene visualizzata la finestra di dialogo Estrazione. Clic **Extract** per avviare la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >Facoltativamente, puoi sovrascrivere il contenitore di staging durante la fase di estrazione. Se **Sovrascrivi contenitore di staging** è disattivato, può velocizzare le estrazioni per le migrazioni successive in cui le impostazioni dei percorsi di contenuto o delle versioni di inclusione non sono state modificate. Tuttavia, se le impostazioni dei percorsi di contenuto o delle versioni di inclusione sono state modificate, **Sovrascrivi contenitore di staging** deve essere abilitato.

1. Il **Estrazione** ora visualizza il campo **IN ESECUZIONE** stato per indicare che l’estrazione è in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Puoi fare clic su **Visualizza avanzamento** per ottenere una visualizzazione granulare dell’estrazione in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Puoi anche monitorare l’avanzamento della fase di estrazione da Cloud Acceleration Manager visitando la pagina Content Transfer (Trasferimento contenuti) e visualizzarlo più dettagliatamente facendo clic su **...** > **Visualizza dettagli**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Al termine dell’estrazione, controlla le altre colonne come **Sorgente** e **Percorsi** per informazioni dettagliate sul set di migrazione popolato. Clic **...** > **Visualizza dettagli** per visualizzare i dettagli, inclusa la durata di ogni fase dell’estrazione. Visualizza questa finestra di dialogo durante l’estrazione per vedere come procedono i passaggi.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima estrazione completa, puoi saltare la pre-copia per le successive estrazioni integrative (se la dimensione del set di migrazione integrativo è inferiore a 200 GB). Il motivo è che potrebbe aggiungere tempo all&#39;intero processo.
>Inoltre, è essenziale che la struttura del contenuto esistente non venga modificata dal momento in cui viene effettuata l’estrazione iniziale a quello in cui viene eseguita l’estrazione integrativa. I top-up non possono essere eseguiti su contenuti la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questo passaggio durante il processo di migrazione.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa.

Effettua le seguenti operazioni:

1. Accedi a **Trasferimento dei contenuti** e selezionare il set di migrazione per il quale si desidera eseguire l’estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione). Clic **Extract**.

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## Passaggio successivo {#whats-next}

Dopo aver appreso l’estrazione del contenuto dall’origine nello strumento Content Transfer (Trasferimento contenuti), ora puoi imparare il processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti). Consulta [Acquisizione di contenuti in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) dove puoi imparare a acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
