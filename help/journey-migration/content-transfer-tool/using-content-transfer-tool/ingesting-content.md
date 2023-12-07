---
title: Acquisizione di contenuti nel Cloud Service
description: Scopri come utilizzare Cloud Acceleration Manager per acquisire i contenuti dal set di migrazione in un’istanza del Cloud Service di destinazione.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: a66724cf76e4562710e458aeeea0d54ea9efb9aa
workflow-type: tm+mt
source-wordcount: '2315'
ht-degree: 4%

---

# Acquisizione di contenuti nel Cloud Service {#ingesting-content}

## Processo di acquisizione in Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Acquisizione dei contenuti"
>abstract="Per acquisizione si intende l’acquisizione dei contenuti dal set di migrazione nell’istanza Cloud Service di destinazione. Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=it#top-up-extraction-process" text="Estrazione integrativa"

Per acquisire il set di migrazione utilizzando Cloud Acceleration Manager, effettua le seguenti operazioni:

1. Passa a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e poi sulla scheda Content Transfer (Trasferimento contenuti). Accedi a **Processi di acquisizione** e fai clic su **Nuova acquisizione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Controlla l’elenco di controllo per l’acquisizione e assicurati che tutti i passaggi siano stati completati. Questi passaggi sono necessari per garantire un’acquisizione corretta. Procedi al **Successivo** solo se l&#39;elenco di controllo è stato completato.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Fornisci le informazioni necessarie per creare un’acquisizione.

   * **Set di migrazione:** Seleziona come Origine il set di migrazione contenente i dati estratti.
      * I set di migrazione scadranno dopo un periodo prolungato di inattività, pertanto si prevede che l’acquisizione avvenga relativamente presto dopo l’esecuzione dell’estrazione. Revisione [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.

   >[!TIP]
   > Se l’estrazione è attualmente in esecuzione, la finestra di dialogo lo indicherà. Una volta completata l’estrazione, l’acquisizione viene avviata automaticamente. Se l’estrazione non riesce o viene interrotta, il processo di acquisizione verrà annullato.

   * **Destinazione:** Seleziona l’ambiente di destinazione. In questo ambiente viene acquisito il contenuto del set di migrazione.
      * Le acquisizioni non supportano una destinazione RDE (Rapid Development Environment) e non vengono visualizzate come possibile scelta di destinazione, anche se l’utente ha accesso a tale destinazione.
      * Anche se un set di migrazione può essere acquisito in più destinazioni contemporaneamente, una destinazione può essere la destinazione di una sola acquisizione in esecuzione o in attesa alla volta.

   * **Livello:** Seleziona il livello. (Autore/Pubblicazione).
      * Se la sorgente era `Author`, si consiglia di acquisirlo nel `Author` livello sul target. Analogamente, se la sorgente era `Publish`, il target deve essere `Publish` anche.

   >[!NOTE]
   > Se il livello di destinazione è `Author`, l’istanza di authoring viene chiusa per tutta la durata dell’acquisizione e diventa non disponibile per gli utenti (ad esempio, autori o chiunque esegua attività di manutenzione). Il motivo è proteggere il sistema ed evitare eventuali modifiche che potrebbero andare perse o causare un conflitto di acquisizione. Assicurati che il tuo team sia a conoscenza di questo fatto. Inoltre, l’ambiente risulta ibernato durante l’acquisizione dell’autore.

   * **A comparsa:** Scegli la `Wipe` valore
      * Il **A comparsa** imposta il punto iniziale della destinazione dell’acquisizione. Se **A comparsa** è abilitato, la destinazione, compreso tutto il suo contenuto, viene reimpostata sulla versione dell’AEM specificata in Cloud Manager. Se non è abilitata, la destinazione mantiene il contenuto corrente come punto di partenza.
      * Questa opzione funziona **NOT** influenzano il modo in cui verrà eseguita l’acquisizione del contenuto. L’acquisizione utilizza sempre una strategia di sostituzione dei contenuti e _non_ una strategia di unione dei contenuti in modo tale che, in entrambi **A comparsa** e **Non Cancellato** In alcuni casi, l’acquisizione di un set di migrazione sovrascriverà i contenuti nello stesso percorso sulla destinazione. Ad esempio, se il set di migrazione contiene `/content/page1` e la destinazione contiene già `/content/page1/product1`, l’acquisizione rimuoverà l’intero `page1` percorso e relative pagine secondarie, inclusi `product1`e sostituirlo con il contenuto nel set di migrazione. Ciò significa che è necessario eseguire un’attenta pianificazione quando si esegue una **Non Cancellato** acquisizione in una destinazione che contiene qualsiasi contenuto che deve essere mantenuto.

   >[!IMPORTANT]
   > Se l&#39;impostazione **A comparsa** è abilitato per l’acquisizione, ripristina l’intero archivio esistente, incluse le autorizzazioni utente sull’istanza del Cloud Service di destinazione. Questo ripristino è valido anche per un utente amministratore aggiunto al **amministratori** e tale utente deve essere aggiunto nuovamente al gruppo amministratori per avviare un’acquisizione.

   * **Pre-copia:** Scegli la `Pre-copy` valore
      * Puoi eseguire il passaggio di pre-copia opzionale per velocizzare notevolmente l’acquisizione. Consulta [Acquisizione con AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) per ulteriori dettagli.
      * Se si utilizza l’acquisizione con pre-copia (per S3 o Azure Data Store), si consiglia di eseguire `Author` prima l’acquisizione da sola. In questo modo si accelera la `Publish` acquisizione quando viene eseguita in un secondo momento.

   >[!IMPORTANT]
   > Puoi avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al gruppo locale **Amministratori AEM** nel servizio Author del Cloud Service di destinazione. Se non riesci ad avviare un’acquisizione, consulta [Impossibile avviare l’acquisizione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) per ulteriori dettagli.

1. Clic **Acquisisci**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Puoi quindi monitorare l’acquisizione dalla vista a elenco Processi di acquisizione e utilizzare il menu Azioni dell’acquisizione per visualizzare le durate e registrare nel momento in cui l’acquisizione procede.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Fai clic su **i) IT** nella riga per ulteriori informazioni sul processo di acquisizione. Puoi visualizzare la durata di ciascun passaggio dell’acquisizione quando è in esecuzione o completata facendo clic su **...** e quindi clic su **Visualizza durate**. Le informazioni provenienti dall’estrazione vengono anche mostrate per realizzare ciò che viene acquisito.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Acquisizione integrativa {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Acquisizione integrativa"
>abstract="Utilizza la funzione integrativa per spostare il contenuto modificato dall’ultima attività di trasferimento dei contenuti. Al termine dell’acquisizione, verifica la presenza di eventuali errori o avvisi nei registri. Eventuali errori devono essere risolti immediatamente affrontando i problemi segnalati o contattando l’Assistenza clienti di Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=it" text="Visualizzazione dei registri"

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che consente l’estrazione di contenuti differenziali eseguendo una *integrativo* del set di migrazione. Questo consente di modificare il set di migrazione in modo da includere solo il contenuto modificato rispetto all’estrazione precedente, senza dover estrarre nuovamente tutto il contenuto.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service. Se hai utilizzato il passaggio di pre-copia per la prima acquisizione, puoi saltare la pre-copia per le successive acquisizioni integrative (se la dimensione del set di migrazione integrativa è inferiore a 200 GB). Il motivo è che potrebbe aggiungere tempo all&#39;intero processo.

Per acquisire il contenuto differenziale al termine di alcune acquisizioni, è necessario eseguire una [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process), quindi utilizza il metodo di acquisizione con il **A comparsa** opzione **disabilitato**. Assicurati di leggere **A comparsa** per evitare di perdere contenuti già presenti nella destinazione.

Per prima cosa, crea un processo di acquisizione e assicurati che **A comparsa** è disattivato durante l’acquisizione, come illustrato di seguito:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Risoluzione dei problemi {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Risoluzione dei problemi di acquisizione dei contenuti"
>abstract="Consulta i registri di acquisizione e la documentazione per trovare soluzioni ai motivi comuni per cui un’acquisizione può non riuscire, trovare il modo di risolvere il problema ed eseguire di nuovo l’acquisizione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html" text="Convalida dei trasferimenti di contenuto"

### CAM: impossibile recuperare il token di migrazione {#cam-unable-to-retrieve-the-migration-token}

Il recupero automatico del token di migrazione potrebbe non riuscire per diversi motivi, tra cui [configurazione di un elenco consentiti IP tramite Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) nell&#39;ambiente del Cloud Service di destinazione. In questi scenari, quando tenti di avviare un’acquisizione viene visualizzata la seguente finestra di dialogo:

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Recupera manualmente il token di migrazione facendo clic sul collegamento &quot;Ottieni token&quot; nella finestra di dialogo. Viene aperta un’altra scheda che mostra il token. Puoi quindi copiare il token e incollarlo nella **Input token di migrazione** campo. Ora, dovresti essere in grado di iniziare l’acquisizione.

>[!NOTE]
>
>Il token è disponibile per gli utenti che appartengono al **Amministratori AEM** nel servizio Author del Cloud Service di destinazione.

### Impossibile avviare l’acquisizione {#unable-to-start-ingestion}

Puoi avviare un’acquisizione nell’ambiente di destinazione solo se appartieni al gruppo locale **Amministratori AEM** nel servizio Author del Cloud Service di destinazione. Se non appartieni al gruppo di amministratori AEM, quando tenti di avviare un’acquisizione viene visualizzato un errore come mostrato di seguito. È possibile chiedere all&#39;amministratore di aggiungerti al **Amministratori AEM** oppure richiedi il token stesso, che potrai incollare nella **Input token di migrazione** campo.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Impossibile raggiungere il servizio di migrazione {#unable-to-reach-migration-service}

Dopo aver richiesto un’acquisizione, è possibile che venga visualizzato all’utente un messaggio simile al seguente: &quot;Il servizio di migrazione nell’ambiente di destinazione non è raggiungibile. In tal caso, riprova più tardi o contatta il supporto Adobe.&quot;

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Questo messaggio indica che Cloud Acceleration Manager non è riuscito a raggiungere il servizio di migrazione dell’ambiente di destinazione per avviare l’acquisizione. Questa situazione può verificarsi per vari motivi.

>[!NOTE]
> 
> Viene visualizzato il campo &quot;Token di migrazione&quot; perché in alcuni casi è ciò che non è consentito recuperare il token. Consentendo la trasmissione manuale, può consentire all’utente di avviare l’acquisizione rapidamente, senza alcun aiuto aggiuntivo. Se il token è fornito e il messaggio viene ancora visualizzato, il problema non era il recupero del token.

* AEM as a Cloud Service mantiene lo stato dell’ambiente e occasionalmente deve riavviare il servizio di migrazione per vari motivi normali. Se il servizio viene riavviato, non potrà essere raggiunto, ma sarà disponibile alla fine.
* È possibile che nell’istanza sia in esecuzione un altro processo. Ad esempio, se [Aggiornamenti delle versioni AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) sta applicando un aggiornamento, il sistema potrebbe essere occupato e il servizio di migrazione regolarmente non disponibile. Al termine di questo processo, è possibile tentare di nuovo l’inizio dell’acquisizione.
* Se un [È stato applicato il Inserisco nell&#39;elenco Consentiti di IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) Tramite Cloud Manager, impedisce a Cloud Acceleration Manager di raggiungere il servizio di migrazione. Non è possibile aggiungere un indirizzo IP per le acquisizioni perché il relativo indirizzo è dinamico. Attualmente, l’unica soluzione consiste nel disattivare l’elenco consentiti IP durante il processo di acquisizione e indicizzazione.
* Ci possono essere altri motivi che richiedono un&#39;indagine. Se l’acquisizione o l’indicizzazione continua a non riuscire, contatta l’Assistenza clienti di Adobe.

### Aggiornamenti e acquisizioni delle versioni di AEM

[Aggiornamenti delle versioni AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) vengono applicati automaticamente agli ambienti per mantenerli aggiornati con la versione più recente di AEM as a Cloud Service. Se l’aggiornamento viene attivato quando viene eseguita un’acquisizione, possono verificarsi risultati imprevedibili, incluso il danneggiamento dell’ambiente.

Se nel programma di destinazione è stato effettuato l’onboarding di &quot;Aggiornamenti della versione dell’AEM&quot;, il processo di acquisizione tenterà di disabilitare la coda prima dell’avvio. Al termine dell’acquisizione, lo stato del programma di aggiornamento della versione viene ripristinato come era prima dell’avvio delle acquisizioni.

>[!NOTE]
>
> Non è più necessario registrare un ticket di supporto per disabilitare &quot;Aggiornamenti della versione AEM&quot;.

Se &quot;Aggiornamenti della versione dell’AEM&quot; è attivo (ovvero, gli aggiornamenti sono in esecuzione o sono in coda per l’esecuzione), l’acquisizione non inizierà e l’interfaccia utente visualizza il seguente messaggio. Una volta completati gli aggiornamenti, è possibile avviare l’acquisizione. Cloud Manager può essere utilizzato per visualizzare lo stato corrente delle pipeline del programma.

>[!NOTE]
>
> &quot;Aggiornamenti della versione dell’AEM&quot; viene eseguito nella pipeline dell’ambiente e attenderà che la pipeline sia pulita. Se gli aggiornamenti vengono messi in coda per un periodo più lungo del previsto, assicurati che la pipeline non sia bloccata involontariamente in un flusso di lavoro personalizzato.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Errore di acquisizione integrativa a causa di violazione del vincolo di unicità

Una causa comune di [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) errore è un conflitto negli id dei nodi. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come quella seguente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: proprietà violata dal vincolo di unicità [jcr:uuid] con valore a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Ogni nodo in AEM deve avere un UUID univoco. Questo errore indica che un nodo che viene acquisito ha lo stesso UUID di uno esistente altrove in un percorso diverso nell’istanza di destinazione.
Questa situazione può verificarsi se un nodo viene spostato sull’origine tra un’estrazione e una successiva [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Può anche accadere se un nodo della destinazione viene spostato tra un’acquisizione e una successiva acquisizione integrativa.

Questo conflitto deve essere risolto manualmente. Chi ha familiarità con il contenuto deve decidere quale dei due nodi deve essere eliminato, tenendo presente gli altri contenuti che vi fanno riferimento. La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo problematico.

### Acquisizione integrativa non riuscita a causa dell’impossibilità di eliminare il nodo di riferimento

Un’altra causa comune di [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) errore è un conflitto di versione per un particolare nodo nell’istanza di destinazione. Per identificare questo errore, scarica il registro di acquisizione utilizzando l’interfaccia utente di Cloud Acceleration Manager e cerca una voce come quella seguente:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity001: impossibile eliminare il nodo a cui si fa riferimento: 8a2289f4-b904-4bd0-8410-15e41e0976a8

Questo può accadere se un nodo sulla destinazione viene modificato tra un’acquisizione e una successiva **Non Cancellato** acquisizione tale da aver creato una nuova versione. Se il set di migrazione è stato estratto con &quot;includi versioni&quot; abilitato, si potrebbe verificare un conflitto in quanto la destinazione dispone ora di una versione più recente a cui fa riferimento la cronologia delle versioni e altro contenuto. Il processo di acquisizione non sarà in grado di eliminare il nodo della versione che genera l’infrazione perché vi si fa riferimento.

La soluzione può richiedere che l’estrazione integrativa venga eseguita nuovamente senza il nodo problematico. Oppure, creando un piccolo set di migrazione del nodo problematico, ma con &quot;include versions&quot; disabilitato.

Le best practice indicano che se un **Non Cancellato** l’acquisizione deve essere eseguita utilizzando un set di migrazione che include le versioni (ovvero, estratte con &quot;include versions&quot;=true). È fondamentale che il contenuto nella destinazione venga modificato il meno possibile, fino al completamento del percorso di migrazione. In caso contrario, possono verificarsi tali conflitti.

### Acquisizione limitata

Un’acquisizione creata con un’estrazione in esecuzione come set di migrazione di origine attende pazientemente che l’estrazione abbia esito positivo e a quel punto inizierà normalmente. Se l’estrazione non riesce o viene interrotta, l’acquisizione e il relativo processo di indicizzazione non iniziano ma vengono annullati. In questo caso, controlla l’estrazione per determinare il motivo dell’errore, risolvi il problema e avvia di nuovo l’estrazione. Una volta eseguita l’estrazione fissa, è possibile pianificare una nuova acquisizione.

## Passaggio successivo {#whats-next}

Quando l’acquisizione viene completata correttamente, l’indicizzazione AEM viene avviata automaticamente. Consulta [Indicizzazione dopo la migrazione del contenuto](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) per ulteriori informazioni.

Una volta completato l’inserimento del contenuto nel Cloud Service, puoi visualizzare i registri di ciascun passaggio (estrazione e acquisizione) e cercare gli errori. Consulta [Visualizzazione dei registri di un set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) per ulteriori informazioni.
