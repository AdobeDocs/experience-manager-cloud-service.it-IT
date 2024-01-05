---
title: Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Scopri le linee guida e le best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 15%

---

# Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#guidelines}

## Linee guida e best practice {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

È disponibile una nuova versione dello strumento Content Transfer (Trasferimento contenuti) che integra il processo di trasferimento dei contenuti con Cloud Acceleration Manager. Si consiglia vivamente di passare a questa nuova versione per sfruttare tutti i vantaggi che offre:

* Modalità self-service per estrarre un set di migrazione in una sola volta e trasferirlo in più ambienti in parallelo
* È stata migliorata l’esperienza dell’utente grazie a migliori stati di caricamento, guardrail e gestione degli errori
* I registri di acquisizione vengono mantenuti e sono sempre disponibili per la risoluzione dei problemi

Per iniziare a utilizzare la nuova versione, disinstalla le versioni precedenti dello strumento Content Transfer (Trasferimento contenuti). Questo è necessario perché la nuova versione viene fornita con un importante cambiamento architettonico. Con la versione 2.x, puoi creare i set di migrazione ed eseguire nuovamente l’estrazione e l’acquisizione sui set.
Le versioni precedenti alla 2.0.0 non sono supportate e si consiglia di utilizzare la versione più recente.

Le seguenti linee guida e best practice sono applicabili alla nuova versione dello strumento Content Transfer (Trasferimento contenuti):

* Esegui [Pulizia revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=it) e [controlli di coerenza dell’archivio dati](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html) il **sorgente** in modo da identificare potenziali problemi e ridurre le dimensioni dell’archivio.

* Nella fase di acquisizione, l’Adobe consiglia di eseguire l’acquisizione utilizzando *a comparsa* è abilitata la modalità in cui viene eliminato l’archivio esistente (di authoring o pubblicazione) nell’ambiente di Cloud Service Adobe Experience Manager (AEM) di destinazione. Quindi, esegui l’aggiornamento con i dati del set di migrazione. Questa modalità è più veloce della modalità in cui la cancellazione è disattivata e il set di migrazione viene applicato al contenuto corrente.

* Al termine dell’attività di trasferimento dei contenuti, nell’ambiente Cloud Service è necessaria la giusta struttura di progetto per garantire il corretto rendering dei contenuti.

* Prima di eseguire lo strumento Content Transfer (Trasferimento contenuti), è necessario assicurarsi che nella sottodirectory `crx-quickstart` dell’istanza AEM sorgente vi sia spazio sufficiente. Questo perché lo strumento Content Transfer (Trasferimento contenuti) crea una copia locale dell’archivio che viene successivamente caricata nel set di migrazione.
La formula generale per calcolare lo spazio libero su disco richiesto è la seguente:
  `data store size + node store size * 1.5`

   * *data store size*: dimensione archivio dati; lo strumento Content Transfer (Trasferimento contenuti) utilizza 64 GB, anche se l’archivio dati effettivo è più grande.
   * *node store size*: dimensione archivio nodi; dimensione della directory dell’archivio segmenti o dimensione del database MongoDB.
Pertanto, per un archivio segmenti di 20 GB, lo spazio libero su disco richiesto è di 94 GB.

* È necessario mantenere un set di migrazione per l’intera durata dell’attività di trasferimento dei contenuti per supportare l’integrazione dei contenuti. È possibile creare e gestire fino a 20 set di migrazione per progetto in Cloud Acceleration Manager alla volta durante l’attività di trasferimento dei contenuti. Se sono necessari più di 20 set di migrazione, crea un secondo progetto in Cloud Acceleration Manager. Tuttavia, questo richiede una gestione del progetto aggiuntiva e una governance out-of-product per evitare la sovrascrittura dei contenuti sul target da parte di più utenti.

* Evitare di modificare la directory di installazione dello strumento CTT. Per impostazione predefinita, l’installazione si svolge nel percorso crx-quickstart/cloud-migration. Questa posizione specifica viene utilizzata internamente da altre librerie. La modifica di questo percorso può causare problemi di estrazione.

## Considerazioni importanti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti) {#important-considerations}

Segui le indicazioni riportate in questa sezione per comprendere le valutazioni importanti durante l’esecuzione dello strumento Content Transfer (Trasferimento contenuti):

* Il requisito minimo di sistema per lo strumento Content Transfer (Trasferimento contenuti) è AEM 6.3 o versione successiva e Java™ 8. Se utilizzi una versione AEM inferiore, aggiorna l’archivio dei contenuti a AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Java™ deve essere configurato nell&#39;ambiente AEM, in modo che `java` può essere eseguito dall&#39;utente che avvia AEM.

* Lo strumento Content Transfer (Trasferimento contenuti) può essere utilizzato con i seguenti tipi di archivio dati: archivio dati file, archivio dati S3, archivio dati S3 condiviso e archivio dati archivio BLOB di Azure.

* Se si utilizza un *Ambiente sandbox*, assicurati che l’ambiente sia aggiornato alla versione più recente. Se utilizzi un *ambiente di produzione*, viene aggiornato automaticamente.

* Per iniziare un’acquisizione, devi appartenere all’AEM locale **amministratori** nell’istanza del Cloud Service a cui stai trasferendo il contenuto. Gli utenti non autorizzati non possono avviare le acquisizioni senza fornire manualmente il token di migrazione.

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** se questa opzione è abilitata, elimina l’intero archivio esistente e crea un nuovo archivio in cui acquisire il contenuto. Ciò significa che vengono ripristinate tutte le impostazioni, comprese le autorizzazioni sull’istanza del Cloud Service di destinazione. È anche vero per un utente amministratore aggiunto al **amministratori** gruppo. L’utente deve essere letto sul **amministratori** per recuperare il token di accesso per lo strumento Content Transfer (Trasferimento contenuti).

* Le acquisizioni non supportano l’unione di contenuti da più origini nell’istanza del Cloud Service target se il contenuto dalle due origini viene spostato negli stessi percorsi sulla destinazione. Per spostare il contenuto da più origini in un’unica istanza del Cloud Service target, assicurati che non vi siano sovrapposizioni dei percorsi del contenuto dalle origini.

* La chiave di estrazione è valida per 14 giorni dal momento in cui è stata creata o rinnovata. Può essere rinnovato in qualsiasi momento. Se la chiave di estrazione è scaduta, non puoi eseguire un’estrazione.

* Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferirlo dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione del contenuto in un ambiente di pubblicazione. Qualsiasi contenuto specificato nel set di migrazione viene acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author, Publish o entrambe. L’Adobe consiglia di installare CTT nell’istanza di authoring di origine per spostare il contenuto nell’istanza di authoring di destinazione durante lo spostamento del contenuto in un’istanza di produzione. Allo stesso modo, installa CTT sull’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza Publish](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) per ulteriori dettagli.

* Gli utenti e i gruppi trasferiti dallo strumento Content Transfer (Trasferimento contenuti) sono solo quelli necessari per il contenuto per soddisfare le autorizzazioni. Il _Estrazione_ processo copia l&#39;intero `/home` nel set di migrazione e esegue la mappatura degli utenti aggiungendo un campo creato dall’indirizzo e-mail di ciascun utente. Per ulteriori informazioni, consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). Il _Acquisizione_ process copia tutti gli utenti e i gruppi a cui si fa riferimento negli ACL dei contenuti migrati. Consulta [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sui gruppi utilizzati in un criterio Gruppo utenti chiuso (CUG).

* Durante la fase di estrazione, lo strumento Content Transfer (Trasferimento contenuti) viene eseguito su un’istanza sorgente di AEM attiva.

* Il *Fase di acquisizione* per l’authoring riduce l’intera implementazione di authoring. Significa che l’AEM dell’autore non è disponibile durante l’intero processo di acquisizione. Inoltre, assicurati che non vengano eseguite pipeline di Cloud Manager mentre esegui il *Acquisizione* fase.

* Quando si utilizza `Amazon S3` o `Azure` come archivio dati sul sistema AEM di origine, l’archivio dati deve essere configurato in modo che i BLOB memorizzati non possano essere eliminati (garbage collection). In questo modo viene garantita l’integrità dei dati di indice e, se non si configura questa modalità, le estrazioni potrebbero non riuscire a causa della mancanza di integrità dei dati di indice.

* Se utilizzi gli indici personalizzati, assicurati di configurarli con `tika` prima di eseguire lo strumento Content Transfer (Trasferimento contenuti). Consulta [Preparazione della nuova definizione dell’indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#preparing-the-new-index-definition) per ulteriori dettagli.

* Se desideri eseguire integrazioni, la struttura del contenuto esistente non deve cambiare dal momento in cui viene effettuata l’estrazione iniziale a quando viene eseguita l’estrazione integrativa. I top-up non possono essere eseguiti su contenuti la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questo passaggio durante il processo di migrazione.

* Se desideri includere le versioni come parte di un set di migrazione ed esegui integrazioni con `wipe=false`, devi quindi disabilitare l’eliminazione della versione a causa di una limitazione corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione delle versioni e stai eseguendo integrazioni in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.

* Un set di migrazione scade dopo un periodo prolungato di inattività, trascorso il quale i relativi dati non sono più disponibili. Revisione [Scadenza set di migrazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) per ulteriori dettagli.

## Passaggio successivo {#whats-next}

Dopo aver appreso le linee guida, le best practice e le considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti), puoi procedere all’installazione e all’utilizzo dello strumento, a partire dalla creazione di un set di migrazione. Consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).
