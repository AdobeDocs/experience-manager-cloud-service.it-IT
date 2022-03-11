---
title: Inserimento di contenuto in Target
description: Inserimento di contenuto in Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 31%

---

# Inserimento di contenuto in Target {#ingesting-content}

## Processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti) {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione del contenuto dal set di migrazione nell’istanza del Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Acquisizione integrativa"

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Puoi eseguire il passaggio di pre-copia opzionale per velocizzare in modo significativo la fase di acquisizione. Fai riferimento a [Acquisizione con AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) per ulteriori dettagli.

1. Seleziona un set di migrazione da **Trasferimento dei contenuti** e fai clic su **Acquisisci** per iniziare l&#39;acquisizione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione). Il contenuto può essere acquisito nell’istanza Author o Publish alla volta. Seleziona l’istanza in cui inserire il contenuto. Fai clic su **Acquisisci** per avviare la fase di acquisizione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Se si utilizza l’acquisizione con la pre-copia (per S3 o Azure Data Store), è consigliabile eseguire prima l’acquisizione da parte dell’autore. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >Quando il **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** viene abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire il contenuto. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al **amministratori** gruppo.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Inoltre, fai clic su **Assistenza clienti** per registrare un biglietto, come illustrato nella figura riportata di seguito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Inoltre, fai riferimento a [Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) per saperne di più.

1. Una volta completata l’acquisizione, lo stato in **Acquisizione di autori** aggiornamenti a **COMPLETATO**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Acquisizione integrativa {#top-up-ingestion-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Una volta completato il processo di acquisizione, puoi utilizzare il contenuto delta utilizzando il metodo di acquisizione integrativa. Effettua le seguenti operazioni:

1. Passa a **Trasferimento dei contenuti** e seleziona il set di migrazione per il quale desideri eseguire l’acquisizione integrativa. Fai clic su **Ingest (Acquisisci)** per avviare l’acquisizione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. Viene visualizzata la finestra di dialogo **Migration Set ingestion** (Acquisizione set di migrazione).

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >Disattiva la **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** per evitare di eliminare il contenuto esistente dall’attività di acquisizione precedente. Inoltre, fai clic su **Assistenza clienti** per registrare un biglietto, come illustrato nella figura precedente.

## Novità {#whats-next}

Dopo aver appreso l’inserimento di contenuti in Target nello strumento Content Transfer (Trasferimento contenuti), puoi visualizzare i registri al termine di ogni passaggio (estrazione e acquisizione) e cercare gli errori. Vedi [Visualizzazione dei registri di un set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) per saperne di più.
