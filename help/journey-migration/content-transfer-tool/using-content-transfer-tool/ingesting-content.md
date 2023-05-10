---
title: Inserimento di contenuto in Target
description: Inserimento di contenuto in Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: addfa18ed8fa45b1cfc17d4e35cbdde47b491507
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 12%

---

# Inserimento di contenuto in Target {#ingesting-content}

## Processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti) {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione dei contenuti dal set di migrazione nell’istanza Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=it#top-up-ingestion-process" text="Acquisizione integrativa"

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:

>[!NOTE]
>Ti sei ricordato di registrare un ticket di supporto per questa acquisizione? Vedi [Considerazioni importanti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) per questo e altre considerazioni per rendere l’acquisizione efficace.

1. Vai a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e sulla scheda Content Transfer (Trasferimento contenuti). Passa a **Processi di acquisizione** e fai clic su **Nuovo inserimento**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Rivedi la lista di controllo per l’acquisizione e assicurati che tutti i passaggi siano stati completati. Si tratta di misure necessarie per garantire il successo dell’acquisizione. Potrai procedere alla **Successivo** solo se la checklist è stata completata.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Fornisci le informazioni necessarie per creare una nuova acquisizione.

   * Seleziona il set di migrazione che contiene i dati estratti come Origine.
      * I set di migrazione scadranno dopo un periodo prolungato di inattività, quindi ci si aspetta che l’acquisizione avvenga relativamente presto dopo l’esecuzione dell’estrazione. Revisione [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.
   * Seleziona l’ambiente di destinazione. In questo punto verrà acquisito il contenuto del set di migrazione. Selezionare il livello. (Autore/pubblicazione). Gli ambienti di sviluppo rapido non sono supportati.

   >[!NOTE]
   >Le seguenti note si applicano all’acquisizione del contenuto:
   > Se l’origine era Autore, è consigliabile inserirla nel livello Autore nella destinazione. Analogamente, se l’origine era Pubblica, anche target dovrebbe essere Pubblica.
   > Se il livello di destinazione è `Author`, l’istanza di authoring verrà chiusa durante la durata dell’acquisizione e non sarà disponibile per gli utenti (ad esempio, autori o chiunque esegua la manutenzione, ecc.). In questo modo si protegge il sistema e si evita qualsiasi modifica che possa essere persa o causare un conflitto di acquisizione. Assicurati che il tuo team sia a conoscenza di questo fatto. Inoltre, l’ambiente apparirà in ibernazione durante l’acquisizione dell’autore.
   > Puoi eseguire il passaggio di pre-copia opzionale per velocizzare in modo significativo la fase di acquisizione. Fai riferimento a [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.
   > Se si utilizza l’acquisizione con la pre-copia (per S3 o Azure Data Store), è consigliabile eseguire prima l’acquisizione da parte dell’autore. Questa operazione velocizza l’acquisizione di Publish quando questa viene eseguita in un secondo momento.
   > Le gestioni non supportano una destinazione RDE (Rapid Development Environment). Non verranno visualizzati come una possibile scelta di destinazione, anche se l’utente ha accesso ad essa.

   >[!IMPORTANT]
   > Le seguenti note importanti si applicano all’acquisizione dei contenuti:
   > Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione. Se non riesci a avviare un’acquisizione, consulta [Impossibile avviare l&#39;acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) per ulteriori dettagli.
   > Se l’impostazione **Wipe** viene attivato prima dell’acquisizione, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire i contenuti. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al **amministratori** gruppo. Per avviare un’acquisizione, dovrai essere aggiunto nuovamente al gruppo di amministratori .

1. Fai clic su **Acquisisci**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Puoi quindi monitorare la fase di acquisizione dalla vista a elenco Processi di acquisizione e utilizzare il menu delle azioni di acquisizione per visualizzare il registro mentre l’acquisizione progredisce.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Fai clic su **i)** pulsante nella riga per ottenere ulteriori informazioni sul processo di acquisizione. Puoi visualizzare la durata di ogni passaggio dell’acquisizione quando viene eseguito o completato facendo clic su **...** e poi **Visualizza durate**. Le informazioni provenienti dall’estrazione vengono anche mostrate per comprendere cosa viene acquisito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Acquisizione integrativa {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Acquisizione integrativa"
>abstract="Utilizza la funzione integrativa per spostare solo i contenuti modificati rispetto alla precedente attività di trasferimento dei contenuti. Al termine dell’acquisizione, verifica la presenza di eventuali errori o avvisi nei registri. Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando l’Assistenza clienti di Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=it" text="Visualizzazione dei registri"

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima acquisizione completa, puoi saltare la pre-copia per le successive acquisizioni integrative (se la dimensione del set di migrazione integrativo è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo.

Una volta completato il processo di acquisizione, per acquisire il contenuto delta dovrai eseguire un [Estrazione dall&#39;alto](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) quindi utilizza il metodo di acquisizione integrativa.

A tale scopo, crea un nuovo processo di acquisizione e assicurati di: **Wipe** è disattivato durante la fase di acquisizione, come illustrato di seguito:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Risoluzione dei problemi {#troubleshooting}

### CAM: impossibile recuperare il token di migrazione {#cam-unable-to-retrieve-the-migration-token}

Il recupero automatico del token di migrazione potrebbe non riuscire per diversi motivi, tra cui [configurazione di un elenco consentiti IP tramite Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) nell’ambiente del Cloud Service di destinazione. In questi scenari, quando tenti di avviare un’acquisizione visualizzerai la seguente finestra di dialogo:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Sarà necessario recuperare manualmente il token di migrazione facendo clic sul collegamento &quot;Ottieni token&quot; nella finestra di dialogo. Verrà aperta un’altra scheda che visualizza il token. Puoi quindi copiare il token e incollarlo nel **Input token di migrazione** campo . Ora, dovreste essere in grado di iniziare l&#39;ingestione.

>[!NOTE]
>
>Il token sarà disponibile per gli utenti che appartengono al locale **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione.

### Impossibile avviare l&#39;acquisizione {#unable-to-start-ingestion}

Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al **Amministratori AEM** nel servizio di authoring del Cloud Service di destinazione. Se non appartieni al gruppo di amministratori AEM, quando tenti di avviare un’acquisizione verrà visualizzato un errore come mostrato di seguito. Puoi chiedere all’amministratore di aggiungerti al **Amministratori AEM** oppure chiedi il token stesso, che puoi quindi incollare nel **Input token di migrazione** campo .

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Impossibile raggiungere il servizio di migrazione {#unable-to-reach-migration-service}

Dopo aver richiesto un’acquisizione, può essere presentato all’utente un messaggio come il seguente: &quot;Il servizio di migrazione nell&#39;ambiente di destinazione non è attualmente raggiungibile. Riprova più tardi o contatta il supporto Adobe.&quot;

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Questo indica che Cloud Acceleration Manager non è stato in grado di raggiungere il servizio di migrazione dell’ambiente di destinazione per avviare l’acquisizione. Questo può accadere per una serie di motivi.

>[!NOTE]
> 
> Viene visualizzato il campo &quot;Token di migrazione&quot; perché in alcuni casi il recupero del token è ciò che è effettivamente non consentito. Consentendo di fornirlo manualmente, può consentire all’utente di avviare rapidamente l’acquisizione, senza ulteriore aiuto. Se il token viene fornito e il messaggio continua a essere visualizzato, il problema non è stato il recupero del token.

* AEM as a Cloud Service mantiene lo stato dell’ambiente e occasionalmente può essere necessario riavviare il servizio di migrazione per una serie di motivi normali. Se il servizio viene riavviato, non sarà possibile raggiungerlo, ma sarà presto disponibile.
* È possibile che nell&#39;istanza sia in esecuzione un altro processo. Ad esempio, se Release Orchestrator sta applicando un aggiornamento, il sistema potrebbe essere occupato e il servizio di migrazione potrebbe non essere regolarmente disponibile. Questo, e la possibilità di danneggiare lo stadio o l&#39;istanza di produzione, è il motivo per cui si consiglia vivamente di mettere in pausa gli aggiornamenti durante un&#39;acquisizione.
* Se [È stato applicato l’Inserire nell&#39;elenco Consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) tramite Cloud Manager, impedirà a Cloud Acceleration Manager di raggiungere il servizio di migrazione. Impossibile aggiungere un indirizzo IP per le acquisizioni perché il relativo indirizzo è molto dinamico. Attualmente, l’unica soluzione è quella di disabilitare l’elenco consentiti IP durante l’acquisizione.
* Ci possono essere altri motivi che necessitano di indagini. Se l’acquisizione continua a non riuscire, contatta l’Assistenza clienti Adobe.

### Aggiornamenti automatici tramite Release Orchestrator ancora abilitati

Release Orchestrator mantiene automaticamente gli ambienti aggiornati applicando automaticamente gli aggiornamenti. Se l’aggiornamento viene attivato durante l’esecuzione di un’acquisizione, possono verificarsi risultati imprevedibili, tra cui la corruzione dell’ambiente. Questo è uno dei motivi per cui è necessario registrare un ticket di supporto prima di avviare un’acquisizione (vedi &quot;Nota&quot; sopra), in modo che sia possibile pianificare la disattivazione temporanea di Release Orchestrator.

Se Release Orchestrator è ancora in esecuzione all&#39;avvio di un&#39;acquisizione, l&#39;interfaccia utente presenta questo messaggio. È possibile scegliere di continuare comunque, accettando il rischio, controllando il campo e premendo nuovamente il pulsante.

>[!NOTE]
>
> Release Orchestrator viene ora implementato negli ambienti di sviluppo, pertanto è necessario mettere in pausa anche gli aggiornamenti su tali ambienti.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Errore di acquisizione integrativa

Una causa comune di un [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) l&#39;errore è un conflitto negli ID nodo. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come segue:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Proprietà violata vincolo di univocità [jcr:uuid] aventi valore a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Ogni nodo in AEM deve avere un uuid univoco. Questo errore indica che un nodo da acquisire ha lo stesso uuid di un nodo già esistente in un percorso diverso nell’istanza di destinazione.
Questo può accadere se un nodo viene spostato sull’origine tra un’estrazione e una successiva [Estrazione dall&#39;alto](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Può anche accadere se un nodo sulla destinazione viene spostato tra un’acquisizione e una successiva acquisizione integrativa.

Questo conflitto deve essere risolto manualmente. Un utente che abbia familiarità con il contenuto deve decidere quale dei due nodi deve essere eliminato, tenendo presente altri contenuti che vi fanno riferimento. La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo che lo ha interessato.

## Passaggio successivo {#whats-next}

Una volta completato l’inserimento di contenuto in Target, puoi visualizzare i registri di ogni passaggio (estrazione e acquisizione) e cercare gli errori. Vedi [Visualizzazione dei registri di un set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) per saperne di più.
