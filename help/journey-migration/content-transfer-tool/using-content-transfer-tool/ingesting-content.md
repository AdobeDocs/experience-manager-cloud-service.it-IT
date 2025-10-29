---
title: Acquisizione di contenuti in Cloud Service
description: Scopri come utilizzare Cloud Acceleration Manager per acquisire i contenuti dal set di migrazione in un’istanza Cloud Service di destinazione.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 54829a232b4b918a525b25f9bca475d7856faa46
workflow-type: tm+mt
source-wordcount: '3616'
ht-degree: 12%

---

# Acquisizione di contenuti in Cloud Service {#ingesting-content}

## Processo di acquisizione in Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione dei contenuti dal set di migrazione nell’istanza Cloud Service di destinazione. Lo strumento di trasferimento contenuti dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content#top-up-extraction-process" text="Estrazione integrativa"

Per acquisire il set di migrazione utilizzando Cloud Acceleration Manager, effettua le seguenti operazioni:

1. Passa a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e poi sulla scheda Content Transfer (Trasferimento contenuti). Passa a **Processi di acquisizione** e fai clic su **Nuova acquisizione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Controlla l’elenco di controllo per l’acquisizione e assicurati che tutti i passaggi siano stati completati. Questi passaggi sono necessari per garantire un’acquisizione corretta. Procedi al passaggio **Successivo** solo se l&#39;elenco di controllo è stato completato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Fornisci le informazioni necessarie per creare un’acquisizione.

   * **Set di migrazione:** Selezionare il set di migrazione che contiene i dati estratti come Source.
      * I set di migrazione scadranno dopo un periodo prolungato di inattività, pertanto si prevede che l’acquisizione avvenga relativamente presto dopo l’esecuzione dell’estrazione. Rivedi [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.

   >[!TIP]
   > Se l’estrazione è in esecuzione, la finestra di dialogo lo indica. Una volta completata correttamente l’estrazione, l’acquisizione viene avviata automaticamente. Se l’estrazione non riesce o viene interrotta, il processo di acquisizione verrà annullato.

   * **Destinazione:** Selezionare l&#39;ambiente di destinazione. In questo ambiente viene acquisito il contenuto del set di migrazione.
      * Le acquisizioni non supportano destinazioni di tipo RDE (Rapid Development Environment) o Anteprima e non vengono visualizzate come possibile scelta di destinazione, anche se l’utente ha accesso a esse.
      * Anche se un set di migrazione può essere acquisito in più destinazioni contemporaneamente, una destinazione può essere la destinazione di una sola acquisizione in esecuzione o in attesa alla volta.

   * **Livello:** Selezionare il livello. (Autore/Pubblicazione).
      * Se l&#39;origine era `Author`, si consiglia di acquisirla nel livello `Author` sulla destinazione. Analogamente, se l&#39;origine è `Publish`, anche la destinazione dovrebbe essere `Publish`.

   >[!NOTE]
   > Se il livello di destinazione è `Author`, l&#39;istanza di authoring viene chiusa per tutta la durata dell&#39;acquisizione e diventa non disponibile per gli utenti (ad esempio, autori o utenti che eseguono attività di manutenzione). Il motivo è proteggere il sistema e impedire eventuali modifiche che potrebbero andare perse o causare un conflitto di acquisizione. Assicurati che il tuo team sia a conoscenza di questo fatto. Inoltre, l’ambiente risulta ibernato durante l’acquisizione dell’autore.

   >[!NOTE]
   > Se il livello di destinazione è `Publish`, l&#39;istanza di pubblicazione rimane in esecuzione durante l&#39;acquisizione.  Tuttavia, se il processo di compattazione è in esecuzione durante l’acquisizione, è probabile che si verifichi un conflitto tra i due processi.  Per questo motivo, il processo di acquisizione 1) disabilita lo script di compattazione temporizzata, in modo che la compattazione non venga avviata durante l’acquisizione, e 2) verifica se la compattazione è attualmente in esecuzione e, in caso affermativo, attende il completamento prima che l’acquisizione proceda.  Se l’acquisizione per la pubblicazione richiede più tempo del previsto, controlla i registri di acquisizione per individuare le istruzioni di registro correlate.

   * **Cancellazione:** Scegliere il valore `Wipe`
      * L&#39;opzione **Cancella** imposta il punto iniziale della destinazione per l&#39;acquisizione. Se **Cancella** è abilitato, la destinazione, incluso tutto il suo contenuto, verrà reimpostata sulla versione di AEM specificata in Cloud Manager. Se non è abilitata, la destinazione mantiene il contenuto corrente come punto di partenza.
      * Questa opzione **NON** influisce sul modo in cui verrà eseguita l&#39;acquisizione del contenuto. L&#39;acquisizione utilizza sempre una strategia di sostituzione dei contenuti e _non_ una strategia di unione dei contenuti. Pertanto, nei casi **Cancella** e **Non Cancella**, l&#39;acquisizione di un set di migrazione sovrascriverà i contenuti nello stesso percorso sulla destinazione. Ad esempio, se il set di migrazione contiene `/content/page1` e la destinazione contiene già `/content/page1/product1`, l&#39;acquisizione rimuove l&#39;intero percorso `page1` e le relative pagine secondarie, incluso `product1`, e lo sostituisce con il contenuto nel set di migrazione. Ciò significa che è necessario eseguire un&#39;attenta pianificazione durante l&#39;esecuzione di un&#39;acquisizione **Non-Wipe** in una destinazione che contiene qualsiasi contenuto che deve essere mantenuto.
      * Le acquisizioni non wipe sono progettate appositamente per il caso d’uso di acquisizione integrativa. Queste acquisizioni mirano ad avere una quantità incrementale di nuovi contenuti che sono cambiati rispetto all’ultima acquisizione in un set di migrazione esistente. Al di fuori di questo caso d’uso, l’esecuzione di acquisizioni senza cancellazione potrebbe richiedere tempi di acquisizione molto lunghi.

   >[!IMPORTANT]
   > Se l&#39;impostazione **Cancella** è abilitata per l&#39;acquisizione, verrà ripristinato l&#39;intero archivio esistente, incluse le autorizzazioni utente sull&#39;istanza di Cloud Service di destinazione. La reimpostazione è vera anche per un utente amministratore aggiunto al gruppo **amministratori** e tale utente deve essere aggiunto nuovamente al gruppo amministratori per avviare un&#39;acquisizione.

   * **Pre-copia:** Scegli il valore `Pre-copy`
      * Puoi eseguire il passaggio di pre-copia opzionale per velocizzare notevolmente l’acquisizione. Per ulteriori dettagli, vedi [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy).
      * Se si utilizza l’acquisizione con pre-copia (per S3 o Azure Data Store), si consiglia di eseguire prima l’acquisizione `Author` da sola. In questo modo l&#39;acquisizione di `Publish` risulta più rapida quando viene eseguita in un secondo momento.

   >[!IMPORTANT]
   > Puoi avviare un&#39;acquisizione nell&#39;ambiente di destinazione solo se appartieni al gruppo **amministratori AEM** locale nel servizio Cloud Service Author di destinazione. Se non riesci ad avviare un&#39;acquisizione, vedi [Impossibile avviare l&#39;acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) per ulteriori dettagli.

1. Una volta selezionate le opzioni di acquisizione, è possibile visualizzarne una stima della durata. Si tratta di una stima ottimale basata su dati storici di acquisizioni simili.

   * Questa stima non viene calcolata o visualizzata per **acquisizioni non wipe**, poiché CAM non sa quanti contenuti sono presenti nel sistema di destinazione in questo caso.
   * Questa stima viene calcolata e visualizzata solo se sono stati raccolti e sono disponibili i valori &quot;Verifica dimensione&quot; dell’estrazione.
   * Questo valore è una stima e, anche se viene calcolato in modo intelligente, non deve essere considerato esatto. Vari fattori possono modificare la durata effettiva.
   * Durante l&#39;acquisizione, questo valore sarà disponibile anche nella finestra di dialogo delle durate, a cui è possibile accedere tramite l&#39;azione &quot;**Visualizza durate**&quot; dell&#39;acquisizione.

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="Stima della durata di acquisizione"
>abstract="È possibile visualizzare la durata approssimativa di una particolare acquisizione per fornire un’idea generale del tempo necessario. Esistono dei limiti alla sua precisione."

![immagine](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. Fai clic su **Ingest** (Acquisisci).

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Puoi quindi monitorare l’acquisizione dalla vista a elenco Processi di acquisizione e utilizzare il menu Azioni dell’acquisizione per visualizzare le durate e registrare nel momento in cui l’acquisizione procede.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Per ulteriori informazioni sul processo di acquisizione, fai clic sul pulsante **(i)** nella riga. È possibile visualizzare la durata di ogni passaggio dell&#39;acquisizione quando è in esecuzione o completato facendo clic su **...** e quindi su **Visualizza durate**. Le informazioni provenienti dall’estrazione vengono anche mostrate per realizzare ciò che viene acquisito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Acquisizione integrativa {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Acquisizione integrativa"
>abstract="Utilizza la funzione integrativa per spostare il contenuto modificato dall’ultima attività di trasferimento dei contenuti. Al termine dell’acquisizione, verifica la presenza di eventuali errori o avvisi nei registri. Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando l’Assistenza clienti di Adobe."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs" text="Visualizzazione dei registri"

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che consente l&#39;estrazione di contenuti differenziali eseguendo una *integrazione* del set di migrazione. Questo consente di modificare il set di migrazione in modo da includere solo il contenuto modificato rispetto all’estrazione precedente, senza dover estrarre nuovamente tutto il contenuto.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima acquisizione, puoi saltare la pre-copia per le successive acquisizioni integrative (se la dimensione del set di migrazione integrativa è inferiore a 200 GB). Il motivo è che potrebbe aggiungere tempo all&#39;intero processo.

Per acquisire il contenuto differenziale dopo il completamento di alcune acquisizioni, è necessario eseguire una [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process), quindi utilizzare il metodo di acquisizione con l&#39;opzione **Cancella** **disabilitata**. Assicurati di leggere la spiegazione **Cancella** qui sopra per evitare di perdere il contenuto già nella destinazione.

Inizia creando un processo di acquisizione e assicurati che **Cancella** sia disabilitato durante l&#39;acquisizione, come illustrato di seguito:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Risoluzione di problemi {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Risoluzione dei problemi di acquisizione dei contenuti"
>abstract="Consulta i registri di acquisizione e la documentazione per trovare soluzioni ai motivi comuni dell’esito negativo di un’acquisizione e trova il modo di risolvere il problema. Una volta risolto il problema, l’acquisizione può essere eseguita nuovamente."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers" text="Convalida dei trasferimenti di contenuto"

### CAM: impossibile recuperare il token di migrazione {#cam-unable-to-retrieve-the-migration-token}

Il recupero automatico del token di migrazione potrebbe non riuscire per diversi motivi, inclusa la [configurazione di un elenco consentiti IP tramite Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) nell&#39;ambiente Cloud Service di destinazione. In questi scenari, quando tenti di avviare un’acquisizione viene visualizzata la seguente finestra di dialogo:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupera manualmente il token di migrazione facendo clic sul collegamento &quot;Ottieni token&quot; nella finestra di dialogo. Viene aperta un’altra scheda che mostra il token. È quindi possibile copiare il token e incollarlo nel campo **Input token di migrazione**. Ora, dovresti essere in grado di iniziare l’acquisizione.

>[!NOTE]
>
>Il token è disponibile per gli utenti che appartengono al gruppo **amministratori AEM** locale nel servizio Cloud Service Author di destinazione.

### Impossibile avviare l’acquisizione {#unable-to-start-ingestion}

Puoi avviare un&#39;acquisizione nell&#39;ambiente di destinazione solo se appartieni al gruppo **amministratori AEM** locale nel servizio Cloud Service Author di destinazione. Se non appartieni al gruppo amministratori di AEM, quando tenti di avviare un’acquisizione viene visualizzato un errore come mostrato di seguito. Puoi chiedere all&#39;amministratore di aggiungerti agli **amministratori AEM** locali oppure di richiedere il token stesso, che potrai quindi incollare nel campo **Input token di migrazione**.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Impossibile raggiungere il servizio di migrazione {#unable-to-reach-migration-service}

Dopo aver richiesto un’acquisizione, è possibile che venga visualizzato all’utente un messaggio simile al seguente: &quot;Il servizio di migrazione nell’ambiente di destinazione non è raggiungibile. In tal caso, riprova più tardi o contatta il supporto Adobe.&quot;

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Questo messaggio indica che Cloud Acceleration Manager non è riuscito a raggiungere il servizio di migrazione dell’ambiente di destinazione per avviare l’acquisizione. Questa situazione può verificarsi per vari motivi.

>[!NOTE]
> 
> Viene visualizzato il campo &quot;Token di migrazione&quot; perché in alcuni casi è ciò che non è consentito recuperare il token. Consentendo la trasmissione manuale, può consentire all’utente di avviare l’acquisizione rapidamente, senza alcun aiuto aggiuntivo. Se il token è fornito e il messaggio viene ancora visualizzato, il problema non era il recupero del token.

* AEM as a Cloud Service mantiene lo stato dell’ambiente e, occasionalmente, deve riavviare il servizio di migrazione per vari motivi normali. Se il servizio viene riavviato, non potrà essere raggiunto, ma sarà disponibile alla fine.
* È possibile che nell’istanza sia in esecuzione un altro processo. Se ad esempio [Aggiornamenti della versione di AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) applica un aggiornamento, è possibile che il sistema sia occupato e che il servizio di migrazione non sia regolarmente disponibile. Al termine di questo processo, è possibile tentare di nuovo l’inizio dell’acquisizione.
* Se è stato applicato un Inserisco nell&#39;elenco Consentiti di [IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) tramite Cloud Manager, Cloud Acceleration Manager non potrà raggiungere il servizio di migrazione. Non è possibile aggiungere un indirizzo IP per le acquisizioni perché il relativo indirizzo è dinamico. Attualmente, l&#39;unica soluzione consiste nel disabilitare il inserire nell&#39;elenco Consentiti inserisco nell&#39;elenco Consentiti di acquisizione e indicizzazione dell&#39;IP durante il processo di acquisizione e indicizzazione aggiungendo temporaneamente 0.0.0.0/0 al processo di acquisizione e indicizzazione durante l&#39;esecuzione del processo di acquisizione e indicizzazione.
* Ci possono essere altri motivi che richiedono un&#39;indagine. Se l’acquisizione o l’indicizzazione continua a non riuscire, contatta l’Assistenza clienti di Adobe.

### Aggiornamenti e acquisizioni delle versioni di AEM {#aem-version-updates-and-ingestions}

[Gli aggiornamenti della versione di AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) vengono applicati automaticamente agli ambienti per mantenerli aggiornati con la versione di AEM as a Cloud Service più recente. Se l’aggiornamento viene attivato quando viene eseguita un’acquisizione, possono verificarsi risultati imprevedibili, incluso il danneggiamento dell’ambiente.

Se nel programma di destinazione è stato effettuato l’onboarding di &quot;Aggiornamenti della versione di AEM&quot;, il processo di acquisizione tenta di disabilitare la coda prima dell’avvio. Al termine dell’acquisizione, lo stato del programma di aggiornamento della versione viene ripristinato come era prima dell’inizio delle acquisizioni.

>[!NOTE]
>
> Non è più necessario registrare un ticket di supporto per disabilitare &quot;Aggiornamenti della versione di AEM&quot;.

Se &quot;Aggiornamenti della versione di AEM&quot; è attivo (ovvero, gli aggiornamenti sono in esecuzione o sono in coda per l’esecuzione), l’acquisizione non inizierà e l’interfaccia utente visualizza il seguente messaggio. Una volta completati gli aggiornamenti, è possibile avviare l’acquisizione. Cloud Manager può essere utilizzato per visualizzare lo stato corrente delle pipeline del programma.

>[!NOTE]
>
> &quot;Aggiornamenti della versione di AEM&quot; viene eseguito nella pipeline dell’ambiente e attende che la pipeline sia pulita. Se gli aggiornamenti vengono messi in coda per un periodo più lungo del previsto, accertati che in un flusso di lavoro personalizzato la pipeline non sia bloccata involontariamente.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Errore di acquisizione a causa di un ambiente cloud che non presenta lo stato Pronto {#ingestion-failure-due-to-cloud-environment-not-in-ready-state}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_cloud_environment_not_in_ready_state"
>title="Ambiente cloud che non presenta lo stato Pronto"
>abstract="In rare istanze, nell’ambiente cloud di destinazione potrebbero verificarsi problemi imprevisti che causano il fallimento dell’acquisizione."

In rari casi, nell’ambiente Cloud Service di destinazione dell’acquisizione potrebbero verificarsi problemi imprevisti. Di conseguenza, l’acquisizione non riuscirà perché l’ambiente non è nello stato &quot;ready&quot; previsto. Controlla il registro di acquisizione per visualizzare ulteriori dettagli sullo stato di errore riscontrato.

Assicurati che l’ambiente di authoring sia disponibile e attendi alcuni minuti prima di ripetere l’acquisizione. Se il problema persiste, contatta l’assistenza clienti segnalando lo stato di errore riscontrato.

### Errore di acquisizione integrativa a causa della violazione del vincolo di unicità {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="Violazione vincolo di unicità"
>abstract="Una causa comune dell’errore di acquisizione senza cancellazione è un conflitto negli ID dei nodi. Può esistere soltanto uno dei nodi in conflitto."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Acquisizione integrativa"

Una causa comune di un errore di [acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) è un conflitto negli ID dei nodi. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come quella seguente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: il vincolo di unicità ha violato la proprietà [jcr:uuid] con valore a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Ogni nodo in AEM deve avere un UUID univoco. Questo errore indica che un nodo che viene acquisito ha lo stesso UUID di quello esistente in un percorso diverso nell’istanza di destinazione. Questa situazione può verificarsi per due motivi:

* Un nodo viene spostato sull&#39;origine tra un&#39;estrazione e una successiva [estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
   * _RICORDA_: per le estrazioni integrative, il nodo esisterà ancora nel set di migrazione, anche se non esiste più nell&#39;origine.
* Un nodo sulla destinazione viene spostato tra un’acquisizione e una successiva acquisizione integrativa.

Questo conflitto deve essere risolto manualmente. Chi ha familiarità con il contenuto deve decidere quale dei due nodi deve essere eliminato, tenendo presente gli altri contenuti che vi fanno riferimento. La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo problematico.

### Acquisizione integrativa non riuscita a causa dell’impossibilità di eliminare il nodo di riferimento {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="Impossibile eliminare il nodo di riferimento"
>abstract="Una causa comune dell’errore di acquisizione senza cancellazione è un conflitto di versione per un particolare nodo nell’istanza di destinazione. È necessario correggere le versioni del nodo."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Acquisizione integrativa"

Un&#39;altra causa comune di un errore di [acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) è un conflitto di versione per un particolare nodo nell&#39;istanza di destinazione. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come quella seguente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity001: impossibile eliminare il nodo a cui si fa riferimento: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Ciò può verificarsi se un nodo sulla destinazione viene modificato tra un&#39;acquisizione e una successiva acquisizione **Non-Wipe** in modo che sia stata creata una nuova versione. Se il set di migrazione è stato estratto con &quot;includi versioni&quot; abilitato, si potrebbe verificare un conflitto in quanto la destinazione dispone ora di una versione più recente a cui fa riferimento la cronologia delle versioni e altro contenuto. Il processo di acquisizione non è in grado di eliminare il nodo della versione che causa l’errore perché vi si fa riferimento.

La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo problematico. Oppure, creando un piccolo set di migrazione del nodo problematico, ma con &quot;include versions&quot; disabilitato.

Le best practice indicano che, se è necessario eseguire un&#39;acquisizione **Non-Wipe** utilizzando un set di migrazione che include versioni, è fondamentale che il contenuto della destinazione venga modificato il meno possibile, fino al completamento del percorso di migrazione. In caso contrario, possono verificarsi tali conflitti.

### Errore di acquisizione a causa dei valori delle proprietà del nodo di grandi dimensioni {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="Proprietà del nodo di grandi dimensioni"
>abstract="Una causa comune di errore di acquisizione è il superamento della dimensione massima dei valori delle proprietà del nodo. Per risolvere il problema, segui la documentazione, compresa quella relativa al rapporto BPA."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool" text="Prerequisiti per la migrazione"

I valori delle proprietà del nodo memorizzati in MongoDB non possono superare i 16 MB. Se un valore di nodo supera le dimensioni supportate, l’acquisizione non riesce e il registro conterrà:

* un errore `BSONObjectTooLarge` e specificare quale nodo ha superato il massimo consentito oppure
* un errore `BsonMaximumSizeExceededException`, che indica che è probabile che un nodo contenente caratteri unicode superi la dimensione massima **

Questa è una restrizione di MongoDB.

Per ulteriori informazioni e un collegamento a uno strumento Oak che consenta di trovare tutti i nodi di grandi dimensioni, vedere la nota `Node property value in MongoDB` in [Prerequisiti per lo strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md). Dopo aver risolto tutti i nodi con dimensioni elevate, esegui di nuovo l’estrazione e l’acquisizione.

Per evitare questa restrizione, esegui [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) sull&#39;istanza AEM di origine e controlla i risultati che presenta, in particolare il pattern [&quot;Unsupported Repository Structure&quot; (URS)](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/urs).

>[!NOTE]
>
>[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) versione 2.1.50+ genererà rapporti sui nodi di grandi dimensioni contenenti caratteri Unicode che superano le dimensioni massime. Assicurati di eseguire la versione più recente. Le versioni BPA precedenti al 2.1.50 non identificano e generano rapporti su questi nodi di grandi dimensioni e devono essere individuate separatamente utilizzando il prerequisito per lo strumento Oak indicato sopra.

### Acquisizione non riuscita a causa di errori intermittenti imprevisti {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="Errori intermittenti imprevisti"
>abstract="A volte si possono verificare errori intermittenti imprevisti del servizio a valle e sfortunatamente l’unico rimedio è quello di ritentare semplicemente l’acquisizione."

Talvolta, problemi intermittenti inattesi potrebbero prestarsi a acquisizioni non riuscite, dove purtroppo l’unico ricorso è quello di ritentare l’acquisizione. Esamina il registro di acquisizione per individuare la causa dell’errore e verificare se è in linea con uno degli errori elencati di seguito, dove deve essere effettuato un nuovo tentativo.

#### Problemi MongoDB {#mongo-db-issues}

* `Atlas prescale timeout error` - La fase di acquisizione tenterà di prescrivere il database cloud di destinazione a una dimensione appropriata che sia allineata alle dimensioni del contenuto del set di migrazione da acquisire. Di rado, questa operazione non viene completata entro il periodo di tempo previsto.
* `Exhausted mongo restore retries` - I tentativi di ripristinare un dump locale del contenuto del set di migrazione acquisito nel database cloud sono stati esauriti. Questo indica un problema generale di salute/rete con MongoDB, che spesso guarisce se stesso dopo pochi minuti.
* `Mongo network error` - A volte, stabilire una connessione a MongoDB può non riuscire, causando l’uscita anticipata del processo di acquisizione e la segnalazione di errore. Deve essere effettuato un semplice nuovo tentativo di acquisizione.
* `Mongo server selection error` - Si tratta di un raro errore di timeout lato client di mongo che può verificarsi per una serie di motivi sottostanti. Un nuovo tentativo successivo molto probabilmente correggerà il problema.
* `Mongo took too long to start` - In casi estremamente rari, l’avvio del MongoDB locale utilizzato nel flusso di lavoro di acquisizione potrebbe non riuscire. Un nuovo tentativo successivo molto probabilmente correggerà il problema.

### Acquisizione annullata {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="Acquisizione annullata"
>abstract="L’estrazione attesa per l’acquisizione non è stata completata correttamente. L’acquisizione è stata annullata perché non è stato possibile eseguirla."

Un’acquisizione creata con un’estrazione in esecuzione come set di migrazione di origine attende pazientemente che l’estrazione abbia esito positivo e a quel punto inizia normalmente. Se l’estrazione non riesce o viene interrotta, l’acquisizione e il relativo processo di indicizzazione non iniziano ma vengono annullati. In questo caso, controlla l’estrazione per determinare il motivo dell’errore, risolvi il problema e avvia di nuovo l’estrazione. Una volta eseguita l’estrazione fissa, è possibile pianificare una nuova acquisizione.

### Impossibile avviare l’acquisizione in attesa {#waiting-ingestion-not-started}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_waiting_ingestion_not_started"
>title="Acquisizione in attesa non avviata"
>abstract="Impossibile avviare l’acquisizione dopo aver atteso il completamento di un’estrazione."

Un’acquisizione creata con un’estrazione in esecuzione come set di migrazione di origine attende finché l’estrazione non riesce e a quel punto l’acquisizione tenta di avviarsi normalmente. Se l’acquisizione non viene avviata correttamente, viene contrassegnata come non riuscita. I possibili motivi del mancato avvio sono: un Elenco consentiti IP è configurato nell’ambiente di authoring di destinazione; l’ambiente di destinazione non è disponibile per altri motivi.  In questo caso, verifica il motivo per cui l’acquisizione non è riuscita, risolve il problema e avvia di nuovo l’acquisizione (non è necessario ripetere l’estrazione).

### La risorsa eliminata non è presente dopo la nuova acquisizione

In generale, non è consigliabile modificare i dati dell’ambiente cloud tra una acquisizione e l’altra.

Quando una risorsa viene eliminata dalla destinazione Cloud Service tramite l’interfaccia utente Assets Touch, i dati del nodo vengono eliminati, ma il BLOB della risorsa con l’immagine non viene eliminato immediatamente. Viene contrassegnato per l’eliminazione in modo che non venga più visualizzato nell’interfaccia utente; tuttavia, rimane nell’archivio dati fino a quando non si verifica la raccolta di oggetti inattivi e il BLOB viene rimosso.

Se una risorsa migrata in precedenza viene eliminata e l’acquisizione successiva viene eseguita prima che il Garbage Collector abbia completato l’eliminazione della risorsa, l’acquisizione dello stesso set di migrazione non ripristinerà la risorsa eliminata. Quando l’acquisizione controlla l’ambiente cloud della risorsa, non sono presenti dati del nodo; pertanto, l’acquisizione copia i dati del nodo nell’ambiente cloud. Tuttavia, quando controlla l’archivio BLOB, vede che il BLOB è presente e salta la copia del BLOB. Per questo motivo i metadati sono presenti dopo l’acquisizione quando la risorsa viene esaminata dall’interfaccia utente touch, ma l’immagine no. I set di migrazione e l’acquisizione dei contenuti non sono stati progettati per gestire questo caso. Hanno lo scopo di aggiungere nuovi contenuti all’ambiente cloud e non ripristinare i contenuti migrati in precedenza.

## Passaggio successivo {#whats-next}

Una volta completata l’acquisizione, l’indicizzazione AEM viene avviata automaticamente. Per ulteriori informazioni, vedere [Indicizzazione dopo la migrazione del contenuto](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md).

Una volta completato l’inserimento dei contenuti in Cloud Service, puoi visualizzare i registri di ogni passaggio (estrazione e acquisizione) e cercare gli errori. Per ulteriori informazioni, consulta [Visualizzazione dei registri per un set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md).
