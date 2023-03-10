---
title: Inserimento di contenuto in Target
description: Inserimento di contenuto in Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 7e5a966693b139efa42111d8b6d675674516cfc6
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 7%

---

# Inserimento di contenuto in Target {#ingesting-content}

## Processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti) {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione dei contenuti dal set di migrazione nell’istanza del Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="Acquisizione integrativa"

Per acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Puoi eseguire il passaggio di pre-copia opzionale per velocizzare notevolmente la fase di acquisizione. Il passaggio di pre-copia è più efficace per la prima estrazione e acquisizione complete. Fai riferimento a [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.

>[!NOTE]
>Ti sei ricordato di registrare un ticket di supporto per questa acquisizione? Consulta [Considerazioni importanti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) affinché questa e altre considerazioni possano contribuire al successo dell’acquisizione.

1. Passa a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e poi sulla scheda Content Transfer (Trasferimento contenuti). Accedi a **Processi di acquisizione** e fai clic su **Nuova acquisizione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. Controlla l’elenco di controllo per l’acquisizione e assicurati che tutti i passaggi siano stati completati. Questi passaggi sono necessari per garantire un’acquisizione corretta. Potrai passare alla **Successivo** solo se l’elenco di controllo è stato completato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Fornisci le informazioni necessarie per creare una nuova acquisizione.

   * Seleziona come Origine il set di migrazione contenente i dati estratti.
      * I set di migrazione scadranno dopo un periodo prolungato di inattività, pertanto si prevede che l’acquisizione avvenga relativamente presto dopo l’esecuzione dell’estrazione. Revisione [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.
   * Seleziona l’ambiente di destinazione. Qui verrà acquisito il contenuto del set di migrazione. Seleziona il livello. (Autore/Pubblicazione).

   >[!NOTE]
   >
   >Se l’origine era Author, si consiglia di acquisirla nel livello Author sulla destinazione. Analogamente, se l’origine è Pubblica, anche la destinazione deve essere Pubblica.

   >[!NOTE]
   >
   >Se il livello di destinazione è `Author`, l’istanza di authoring verrà chiusa per tutta la durata dell’acquisizione e non sarà disponibile per gli utenti (ad esempio, autori o utenti che eseguono attività di manutenzione, ecc.). Questo consente di proteggere il sistema e di evitare eventuali modifiche che potrebbero andare perse o causare un conflitto di acquisizione. Assicurati che il tuo team sia a conoscenza di questo fatto. Inoltre, l’ambiente risulterà ibernato durante l’acquisizione dell’autore.

   >[!NOTE]
   >
   >Puoi eseguire il passaggio di pre-copia opzionale per velocizzare notevolmente la fase di acquisizione. Fai riferimento a [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.
   > 
   >Se si utilizza l’acquisizione con pre-copia (per S3 o Azure Data Store), si consiglia di eseguire prima l’acquisizione dell’authoring. In questo modo l’acquisizione Publish sarà più rapida quando viene eseguita in un secondo momento.

   >[!IMPORTANT]
   >
   >Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al dominio **Amministratori AEM** nel servizio Author del Cloud Service di destinazione. Se non riesci ad avviare un’acquisizione, consulta [Impossibile avviare l’acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) per ulteriori dettagli.

   >[!IMPORTANT]
   >
   >Se l&#39;impostazione **A comparsa** viene abilitato prima dell’acquisizione, elimina l’intero archivio esistente e crea un nuovo archivio in cui acquisire il contenuto. Ciò significa che vengono ripristinate tutte le impostazioni, comprese le autorizzazioni sull’istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al **amministratori** gruppo. Per avviare un’acquisizione, devi essere aggiunto nuovamente al gruppo degli amministratori.

1. Fai clic su **Acquisisci**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Puoi quindi monitorare la fase di acquisizione dalla vista a elenco Processi di acquisizione e utilizzare il menu Azioni di acquisizione per visualizzare il registro man mano che l’acquisizione procede.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Al termine dell’acquisizione, fai clic sul pulsante (i) nell’angolo in alto a destra dello schermo per ottenere ulteriori informazioni sul processo di acquisizione.

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
>abstract="Utilizza la funzione integrativa per spostare il contenuto modificato dall’ultima attività di trasferimento dei contenuti. Al termine dell’acquisizione, controlla i registri per eventuali errori/avvisi. Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando l’Assistenza clienti di Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visualizzazione dei registri"

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’*integrazione* di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima acquisizione completa, puoi saltare la pre-copia per le successive acquisizioni integrative (se la dimensione del set di migrazione integrativa è inferiore a 200 GB) perché potrebbe aggiungere tempo all’intero processo.

Una volta completato il processo di acquisizione, per acquisire il contenuto delta dovrai eseguire una [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) e quindi utilizza il metodo di acquisizione integrativa.

Per farlo, crea un nuovo processo di acquisizione e assicurati che **A comparsa** è disattivato durante la fase di acquisizione, come illustrato di seguito:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Risoluzione dei problemi {#troubleshooting}

### CAM: impossibile recuperare il token di migrazione {#cam-unable-to-retrieve-the-migration-token}

Il recupero automatico del token di migrazione potrebbe non riuscire per diversi motivi, tra cui [configurazione di un elenco consentiti IP tramite Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) nell&#39;ambiente del Cloud Service di destinazione. In questi scenari, quando tenti di avviare un’acquisizione viene visualizzata la seguente finestra di dialogo:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Per recuperare manualmente il token di migrazione, fai clic sul collegamento &quot;Ottieni token&quot; nella finestra di dialogo. Verrà aperta un’altra scheda in cui viene visualizzato il token. Puoi quindi copiare il token e incollarlo nella **Input token di migrazione** campo. Ora, dovresti essere in grado di iniziare l’acquisizione.

>[!NOTE]
>
>Il token sarà disponibile per gli utenti che appartengono al **Amministratori AEM** nel servizio Author del Cloud Service di destinazione.

### Impossibile avviare l’acquisizione {#unable-to-start-ingestion}

Potrai avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al dominio **Amministratori AEM** nel servizio Author del Cloud Service di destinazione. Se non appartieni al gruppo di amministratori AEM, all’inizio di un’acquisizione visualizzerai un errore come mostrato di seguito. È possibile chiedere all&#39;amministratore di aggiungerti al **Amministratori AEM** oppure richiedi il token stesso, che potrai incollare nella **Input token di migrazione** campo.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Impossibile raggiungere il servizio di migrazione {#unable-to-reach-migration-service}

Dopo aver richiesto un’acquisizione, è possibile che venga visualizzato all’utente un messaggio simile al seguente: &quot;Il servizio di migrazione nell’ambiente di destinazione non è attualmente raggiungibile. Riprova più tardi o contatta l’assistenza di Adobe.&quot;

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Questo indica che Cloud Acceleration Manager non è riuscito a raggiungere il servizio di migrazione dell’ambiente di destinazione per avviare l’acquisizione. Questo può accadere per una serie di motivi.

>[!NOTE]
> 
> Viene visualizzato il campo &quot;Token di migrazione&quot; perché in alcuni casi è ciò che non è consentito recuperare il token. Consentendo la trasmissione manuale, può consentire all’utente di avviare l’acquisizione rapidamente, senza alcun aiuto aggiuntivo. Se il token è fornito e il messaggio viene ancora visualizzato, il problema non era il recupero del token.

* AEM as a Cloud Service mantiene lo stato dell’ambiente e occasionalmente può essere necessario riavviare il servizio di migrazione per una serie di motivi normali. Se il servizio viene riavviato, non sarà possibile raggiungerlo, ma sarà disponibile a breve.
* È possibile che nell’istanza sia in esecuzione un altro processo. Ad esempio, se Release Orchestrator applica un aggiornamento, il sistema potrebbe essere occupato e il servizio di migrazione regolarmente non disponibile. Per questo motivo, e con la possibilità di danneggiare l’istanza di stage o produzione, si consiglia vivamente di sospendere gli aggiornamenti durante un’acquisizione.
* Se un [È stato applicato il Inserisco nell&#39;elenco Consentiti di IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) tramite Cloud Manager, impedirà a Cloud Acceleration Manager di raggiungere il servizio di migrazione. Non è possibile aggiungere un indirizzo IP per le acquisizioni perché è molto dinamico. Attualmente, l’unica soluzione consiste nel disattivare l’elenco consentiti IP mentre l’acquisizione è in esecuzione.
* Ci possono essere altri motivi che richiedono un&#39;indagine. Se l’acquisizione continua a non riuscire, contatta l’Assistenza clienti di Adobe.

### Aggiornamenti automatici tramite Release Orchestrator è ancora abilitato

Release Orchestrator mantiene automaticamente gli ambienti aggiornati applicando automaticamente gli aggiornamenti. Se l’aggiornamento viene attivato durante l’esecuzione di un’acquisizione, possono verificarsi risultati imprevedibili, incluso il danneggiamento dell’ambiente. Questo è uno dei motivi per cui un ticket di supporto deve essere registrato prima di iniziare un’acquisizione (vedi &quot;Nota&quot; sopra), in modo da poter pianificare la disattivazione temporanea di Release Orchestrator.

Se Release Orchestrator è ancora in esecuzione all’avvio di un’acquisizione, questo messaggio viene visualizzato nell’interfaccia utente. È possibile scegliere di continuare comunque, accettando il rischio, selezionando il campo e premendo nuovamente il pulsante.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Acquisizione integrativa non riuscita

Una causa comune di [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) errore è un conflitto negli id dei nodi. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come quella seguente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: proprietà violata dal vincolo di unicità [jcr:uuid] con valore a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Ogni nodo in AEM deve avere un UUID univoco. Questo errore indica che un nodo da acquisire ha lo stesso UUID di uno già esistente in un percorso diverso nell’istanza di destinazione.
Questo può accadere se un nodo viene spostato sull’origine tra un’estrazione e una successiva [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Può anche accadere se un nodo sul target viene spostato tra un’acquisizione e una successiva acquisizione integrativa.

Questo conflitto deve essere risolto manualmente. Chi ha familiarità con il contenuto deve decidere quale dei due nodi deve essere eliminato, tenendo presente gli altri contenuti che vi fanno riferimento. La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo problematico.

## Passaggio successivo {#whats-next}

Una volta completato l’inserimento del contenuto in Target, puoi visualizzare i registri di ciascun passaggio (estrazione e acquisizione) e cercare gli errori. Consulta [Visualizzazione dei registri di un set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) per ulteriori informazioni.
