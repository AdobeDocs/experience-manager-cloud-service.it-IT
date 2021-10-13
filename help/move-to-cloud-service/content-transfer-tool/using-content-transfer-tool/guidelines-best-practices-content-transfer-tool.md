---
title: Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)
source-git-commit: b421cc5e6078112adecb856d723a1bae628d8ec7
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 25%

---


# Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#guidelines}

## Linee guida e best practice {#best-practices}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Linee guida e best practice"
>abstract="Rivedi le linee guida e le best practice per utilizzare lo strumento Content Transfer (Trasferimento contenuti), incluse le attività di pulizia revisioni, considerazioni sullo spazio su disco e altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti)"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerazioni importanti sull’utilizzo dello strumento di mappatura utente"

Leggi la sezione seguente per comprendere le linee guida e le best practice per utilizzare lo strumento Content Transfer (Trasferimento contenuti):

* È consigliabile eseguire la [pulizia delle revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e i [controlli di coerenza dell’archivio dati](https://helpx.adobe.com/it/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) nell’archivio **sorgente** per identificare potenziali problemi e ridurre le dimensioni dell’archivio.

* Se la rete CDN (Content Delivery Network) di authoring di AEM Cloud è configurata per disporre di un elenco di indirizzi IP consentiti, è necessario assicurarsi che anche gli IP dell’ambiente sorgente vengano aggiunti all’elenco Consentiti in modo che l’ambiente sorgente e l’ambiente AEM Cloud possano comunicare tra loro.

* Nella fase di acquisizione, si consiglia di eseguire l’acquisizione con la modalità *Cancella* abilitata, affinché l’archivio esistente (di authoring o pubblicazione) nell’ambiente di destinazione AEM Cloud Service venga completamente eliminato e quindi aggiornato con i dati del set di migrazione. Questa modalità è molto più veloce della modalità in cui la cancellazione è disattivata e il set di migrazione viene applicato sul contenuto corrente.

* Al termine dell’attività di trasferimento dei contenuti, nell’ambiente Cloud Service è necessaria la giusta struttura di progetto per garantire il corretto rendering dei contenuti.

* Prima di eseguire lo strumento Content Transfer (Trasferimento contenuti), è necessario assicurarsi che nella sottodirectory `crx-quickstart` dell’istanza AEM sorgente vi sia spazio sufficiente. Questo perché lo strumento Content Transfer (Trasferimento contenuti) crea una copia locale dell’archivio che viene successivamente caricata nel set di migrazione.
La formula generale per calcolare lo spazio libero su disco richiesto è la seguente:
   `data store size + node store size * 1.5`

   * *data store size*: dimensione archivio dati; lo strumento Content Transfer (Trasferimento contenuti) utilizza 64 GB, anche se l’archivio dati effettivo è più grande.
   * *node store size*: dimensione archivio nodi; dimensione della directory dell’archivio segmenti o dimensione del database MongoDB.
Pertanto, per un archivio segmenti di 20 GB, lo spazio libero su disco richiesto è di 94 GB.

* È necessario mantenere un set di migrazione in tutta l’attività di trasferimento dei contenuti per supportare le integrazioni dei contenuti. Poiché è possibile creare e mantenere fino a dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti, è consigliabile suddividere di conseguenza l’archivio dei contenuti per evitare di esaurire i set di migrazione.

## Considerazioni importanti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti) {#important-considerations}

Segui le indicazioni riportate in questa sezione per comprendere le valutazioni importanti durante l’esecuzione dello strumento Content Transfer (Trasferimento contenuti):

* l requisiti di sistema minimi per lo strumento Content Transfer (Trasferimento contenuti) sono AEM 6.3 o versione successiva e JAVA 8. Se si utilizza una versione AEM inferiore, è necessario aggiornare l’archivio dei contenuti a AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Java deve essere configurato nell&#39;ambiente AEM in modo che il comando `java` possa essere eseguito dall&#39;utente che avvia AEM.

* Si consiglia di disinstallare le versioni precedenti dello strumento Content Transfer (Trasferimento contenuti) durante l’installazione della versione 1.3.0, in quanto lo strumento ha subito una modifica importante dell’architettura. Con la versione 1.3.0, devi anche creare nuovi set di migrazione ed eseguire nuovamente l’estrazione e l’acquisizione sui nuovi set di migrazione.

* Lo strumento Content Transfer (Trasferimento contenuti) può essere utilizzato con i seguenti tipi di archivio dati: Archivio dati file, archivio dati S3, archivio dati S3 condiviso e archivio dati Azure Blob.

* Se utilizzi un *ambiente Sandbox*, assicurati che l’ambiente sia corrente e aggiornato alla versione più recente. Se utilizzi un *ambiente di produzione*, viene aggiornato automaticamente.

* Per utilizzare lo strumento Content Transfer (Trasferimento contenuti), devi essere un utente amministratore nell’istanza sorgente e appartenere al gruppo di AEM **amministratori** nell’istanza di Cloud Service a cui stai trasferendo i contenuti. Gli utenti non autorizzati non potranno recuperare il token di accesso per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Se l’impostazione **Cancella il contenuto esistente nell’istanza Cloud prima dell’acquisizione** è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui inserire il contenuto. Questo significa che reimposta tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione. Questo vale anche per un utente amministratore aggiunto al gruppo **administrators** . Per recuperare il token di accesso per CTT, è necessario che l’utente sia aggiunto nuovamente al gruppo **administrators** .

* Il token di accesso può scadere periodicamente dopo un determinato periodo di tempo o dopo l’aggiornamento dell’ambiente di Cloud Service. Se il token di accesso è scaduto, non sarà possibile connettersi all’istanza di Cloud Service e sarà necessario recuperare il nuovo token di accesso. L’icona di stato associata a un set di migrazione esistente si trasforma in un cloud rosso e viene visualizzato un messaggio al passaggio del mouse.

* Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferire il contenuto dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione di contenuto in un ambiente di pubblicazione. Qualsiasi contenuto sia specificato nel set di migrazione verrà acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author o Publish o in entrambe. Si consiglia di installare CTT durante lo spostamento del contenuto in un’istanza Production nell’istanza Author di origine per spostare il contenuto nell’istanza Author di destinazione e, allo stesso modo, di installare CTT nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Per ulteriori informazioni, consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un&#39;istanza Publish](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-ctt-on-publish) .

* Gli utenti e i gruppi trasferiti dallo strumento Content Transfer (Trasferimento contenuti) sono solo quelli richiesti dal contenuto per soddisfare le autorizzazioni. Il processo *Estrazione* copia l&#39;intero `/home` nel set di migrazione e il processo *Acquisizione* copia tutti gli utenti e i gruppi a cui si fa riferimento nelle ACL del contenuto migrato. Per mappare automaticamente gli utenti e i gruppi esistenti ai loro ID IMS, fai riferimento a [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration).

* Durante la fase di estrazione, lo strumento Content Transfer (Trasferimento contenuti) viene eseguito su un’istanza sorgente di AEM attiva.

* Dopo aver completato la fase *Estrazione* del processo di trasferimento dei contenuti e prima di avviare la fase di acquisizione *Ingestion* per acquisire contenuti nelle istanze as a Cloud Service *Stage* o *Produzione*, dovrai registrare un ticket di supporto per notificare all&#39;Adobe l&#39;intenzione di eseguire *Acquisizione* in modo che l&#39;Adobe possa garantire che non si verifichino interruzioni durante il processo *Ingestion*. Sarà necessario registrare il ticket di supporto 1 settimana prima della data *di acquisizione* pianificata. Dopo aver inviato il ticket di assistenza, il team di supporto fornirà indicazioni sui passaggi successivi. Puoi registrare un ticket di supporto con i seguenti dettagli:

   * Data esatta e ora stimata (con il tuo fuso orario) quando intendi avviare la fase *Acquisizione*.
   * Tipo di ambiente (Stage o Produzione) in cui si intende inserire i dati.
   * ID programma.

* La *fase di acquisizione* per l’autore riduce l’intera distribuzione dell’autore. Questo significa che l’istanza di authoring di AEM non sarà disponibile durante l’intero processo di acquisizione. Assicurati anche che nessuna pipeline di Cloud Manager venga eseguita durante la fase *Acquisizione*.

* Quando utilizzi `Amazon S3` o `Azure` come archivio dati nel sistema di AEM di origine, l’archivio dati deve essere configurato in modo che i BLOB memorizzati non possano essere eliminati (raccolta rifiuti). In questo modo si garantisce l&#39;integrità dei dati dell&#39;indice e la mancata configurazione di questo modo può causare estrazioni non riuscite a causa della mancanza di integrità dei dati dell&#39;indice.

* Se utilizzi indici personalizzati, assicurati di configurare gli indici personalizzati con il nodo `tika` prima di eseguire lo strumento Content Transfer (Trasferimento contenuti). Per ulteriori informazioni, consulta [Preparazione della nuova definizione di indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition) .

* Se intendi eseguire operazioni di integrazione, è essenziale che la struttura del contenuto del contenuto esistente non venga modificata dal momento in cui l’estrazione iniziale viene portata al momento dell’esecuzione dell’estrazione integrativa. Non è possibile eseguire i top-up su contenuto la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questa limitazione durante il processo di migrazione.

* Se intendi includere versioni come parte di un set di migrazione e stai eseguendo integrazioni con `wipe=false`, devi disattivare l’eliminazione della versione a causa di un limite corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione della versione e stai eseguendo i top-up in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.

## Novità {#whats-next}

Dopo aver appreso le linee guida, le best practice e le considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti), puoi installare e utilizzare lo strumento, a partire dalla creazione di un set di migrazione. Per ulteriori informazioni, consulta [Guida introduttiva al trasferimento di contenuti ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) .
