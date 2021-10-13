---
title: Inserimento di contenuti in Target nello strumento Content Transfer (Trasferimento contenuti)
description: Inserimento di contenuti in Target nello strumento Content Transfer (Trasferimento contenuti)
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 34%

---


# Inserimento di contenuti in Target nello strumento Content Transfer (Trasferimento contenuti) {#ingesting-content}

## Processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti) {#ingestion-process}

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

   Inoltre, fai clic su **Assistenza clienti** per registrare un ticket, come mostrato nella figura precedente. Per ulteriori informazioni, consulta anche [Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) .

1. Una volta completata l’acquisizione, lo stato viene aggiornato a **FINISHED**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

## Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Nella pagina *Overview* (Panoramica), seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-02.png)

   >[!IMPORTANT]
   >Per evitare di eliminare il contenuto esistente dall’attività di acquisizione precedente, disattiva l’opzione **Cancella contenuto esistente nell’istanza Cloud prima dell’acquisizione** . Inoltre, fai clic su **Assistenza clienti** per registrare un ticket, come mostrato nella figura precedente.
