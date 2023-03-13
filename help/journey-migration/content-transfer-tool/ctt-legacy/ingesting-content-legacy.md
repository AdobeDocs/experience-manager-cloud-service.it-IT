---
title: Acquisizione di contenuti in Target (legacy)
description: Inserimento di contenuto in Target
hide: true
hidefromtoc: true
exl-id: 326b3e98-5055-49b5-a005-63fd3ca35202
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 27%

---

# Acquisizione di contenuti in Target (legacy) {#ingesting-content}

## Processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti) {#ingestion-process}

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Puoi eseguire il passaggio di pre-copia opzionale per velocizzare notevolmente la fase di acquisizione. Fai riferimento a [Acquisizione con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) per ulteriori dettagli.

1. Seleziona un set di migrazione da **Trasferimento dei contenuti** pagina e fai clic su **Acquisisci** per avviare l’acquisizione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione). Il contenuto può essere acquisito nell’istanza di authoring o di pubblicazione alla volta. Seleziona l’istanza in cui acquisire il contenuto. Fai clic su **Acquisisci** per avviare la fase di acquisizione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Se si utilizza l’acquisizione con pre-copia (per S3 o Azure Data Store), si consiglia di eseguire prima l’acquisizione dell’authoring. In questo modo l’acquisizione Publish sarà più rapida quando viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >Quando **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** se questa opzione è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui acquisire il contenuto. Ciò significa che vengono ripristinate tutte le impostazioni, comprese le autorizzazioni sull’istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al **amministratori** gruppo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Fai clic su **Assistenza clienti** per registrare un ticket, come illustrato nella figura seguente.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Inoltre, fai riferimento a [Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) per ulteriori informazioni.

1. Una volta completata l’acquisizione, lo stato in **Acquisizione dell’autore** aggiornamenti a **COMPLETATO**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Accedi a **Trasferimento dei contenuti** e seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >È necessario disattivare **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** per evitare di eliminare il contenuto esistente dall’attività di acquisizione precedente. Fai clic su **Assistenza clienti** per registrare un ticket, come illustrato nella figura precedente.

## Passaggio successivo {#whats-next}

Dopo aver appreso come inserire contenuti in Target nello strumento Content Transfer (Trasferimento contenuti), puoi visualizzare i registri al completamento di ogni passaggio (estrazione e acquisizione) e cercare gli errori. Consulta [Visualizzazione dei registri di un set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) per ulteriori informazioni.
