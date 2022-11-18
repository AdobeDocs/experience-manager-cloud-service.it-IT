---
title: Inserimento di contenuto in Target
description: Inserimento di contenuto in Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 4b716f3a41e431b47c8f439d4d24610b79f22736
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 13%

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
>Puoi eseguire il passaggio di pre-copia opzionale per velocizzare in modo significativo la fase di acquisizione. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione completa. Fai riferimento a [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.

1. Vai a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e sulla scheda Content Transfer (Trasferimento contenuti). Passa a **Processi di acquisizione** e fai clic su **Nuovo inserimento**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. Rivedi la lista di controllo per l’acquisizione e assicurati che tutti i passaggi siano stati completati. Si tratta di misure necessarie per garantire il successo dell’acquisizione. Potrai procedere alla **Successivo** solo se la checklist è stata completata.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Fornisci le informazioni necessarie per creare una nuova acquisizione.

   * Seleziona il set di migrazione appena estratto come origine
   * Seleziona l’ambiente di destinazione. In questo punto verrà acquisito il contenuto del set di migrazione. Selezionare il livello. (Autore/pubblicazione).

   >[!NOTE]
   >
   >Se l’origine era Autore, è consigliabile inserirla nel livello Autore nella destinazione. Analogamente, se l’origine era Pubblica, anche target dovrebbe essere Pubblica.

   >[!NOTE]
   >
   >Puoi eseguire il passaggio di pre-copia opzionale per velocizzare in modo significativo la fase di acquisizione. Fai riferimento a [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.
   > 
   >Se si utilizza l’acquisizione con la pre-copia (per S3 o Azure Data Store), è consigliabile eseguire prima l’acquisizione da parte dell’autore. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >
   >Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni alla pagina locale **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione. Se non riesci a avviare un’acquisizione, consulta [Impossibile avviare l&#39;acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) per ulteriori dettagli.

   >[!IMPORTANT]
   >
   >Se l’impostazione **Wipe** viene attivato prima dell’acquisizione, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire i contenuti. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al **amministratori** gruppo. Per avviare un’acquisizione, dovrai essere aggiunto nuovamente al gruppo di amministratori .

1. Fai clic su **Acquisisci**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Puoi quindi monitorare la fase di acquisizione dalla vista a elenco Processi di acquisizione e utilizzare il menu delle azioni di acquisizione per visualizzare il registro mentre l’acquisizione progredisce.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Una volta completata l’acquisizione, fai clic sul pulsante (i) nell’angolo in alto a destra dello schermo per ottenere ulteriori informazioni sul processo di acquisizione.

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Acquisizione integrativa {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="Utilizza la funzione di integrazione per spostare il contenuto modificato rispetto all’attività precedente di trasferimento dei contenuti. Al termine dell’acquisizione, controlla i registri per eventuali errori/avvisi. Gli eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando l’Assistenza clienti Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visualizzazione dei registri"

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima acquisizione completa, puoi saltare la pre-copia per le successive acquisizioni integrative (se la dimensione del set di migrazione integrativo è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo.

Una volta completato il processo di acquisizione, per acquisire il contenuto delta dovrai eseguire un [Estrazione dall&#39;alto](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) quindi utilizza il metodo di acquisizione integrativa.

A tale scopo, crea un nuovo processo di acquisizione e assicurati di: **Wipe** è disattivato durante la fase di acquisizione, come illustrato di seguito:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Risoluzione dei problemi {#troubleshooting}

### CAM: impossibile recuperare il token di migrazione {#cam-unable-to-retrieve-the-migration-token}

Il recupero automatico del token di migrazione potrebbe non riuscire per diversi motivi, tra cui [configurazione di un elenco consentiti IP tramite Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) nell’ambiente del Cloud Service di destinazione.  In questi scenari, quando tenti di avviare un’acquisizione visualizzerai la seguente finestra di dialogo:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Sarà necessario recuperare manualmente il token di migrazione facendo clic sul collegamento &quot;Ottieni token&quot; nella finestra di dialogo. Verrà aperta un’altra scheda che visualizza il token. Puoi quindi copiare il token e incollarlo nel **Input token di migrazione** campo . Ora, dovreste essere in grado di iniziare l&#39;ingestione.

>[!NOTE]
>
>Il token sarà disponibile per gli utenti che appartengono al locale **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione.

### Impossibile avviare l&#39;acquisizione {#unable-to-start-ingestion}

Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni alla pagina locale **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione. Se non appartieni al gruppo di amministratori AEM, quando tenti di avviare un’acquisizione verrà visualizzato un errore come mostrato di seguito. Puoi chiedere all’amministratore di aggiungerti al **Amministratori AEM** oppure chiedi il token stesso, che puoi quindi incollare nel **Input token di migrazione** campo .

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

## Passaggio successivo {#whats-next}

Una volta completato l’inserimento di contenuto in Target, puoi visualizzare i registri di ogni passaggio (estrazione e acquisizione) e cercare gli errori. Vedi [Visualizzazione dei registri di un set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) per saperne di più.
