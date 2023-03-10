---
title: Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti) (legacy)
description: Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti)
hide: true
hidefromtoc: true
exl-id: 03449606-0fb4-4a9f-9abb-6b17c27a6046
source-git-commit: eadcf71aa96298383b05e61251dfeb5f345df6b9
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 14%

---

# Linee guida e best practice per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti) (legacy) {#guidelines}

## Linee guida e best practice {#best-practices}

Leggi la sezione seguente per comprendere le linee guida e le best practice per utilizzare lo strumento Content Transfer (Trasferimento contenuti):

* Esegui [Pulizia revisioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) e [controlli di coerenza dell’archivio dati](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=en) il **sorgente** per identificare potenziali problemi e ridurre le dimensioni dell’archivio.

* Se la rete CDN (Content Delivery Network) di creazione del contenuto di AEM Cloud è configurata per avere un elenco Consentiti di IP di, assicurati che anche gli IP dell’ambiente sorgente vengano aggiunti al elenco Consentiti di. In questo modo l’ambiente sorgente e l’ambiente AEM Cloud possono comunicare tra loro.

* Esegui l’acquisizione utilizzando *a comparsa* è abilitata la modalità in cui l’archivio esistente (di authoring o pubblicazione) nell’ambiente AEM Cloud Service di destinazione verrà eliminato e quindi aggiornato con i dati del set di migrazione. Questa modalità è molto più veloce della modalità in cui la cancellazione è disattivata e il set di migrazione viene applicato sul contenuto corrente.

* Al termine dell’attività di trasferimento dei contenuti, nell’ambiente Cloud Service è necessaria la giusta struttura di progetto per garantire il corretto rendering dei contenuti.

* Prima di eseguire lo strumento Content Transfer (Trasferimento contenuti), è necessario assicurarsi che nella sottodirectory `crx-quickstart` dell’istanza AEM sorgente vi sia spazio sufficiente. Questo perché lo strumento Content Transfer (Trasferimento contenuti) crea una copia locale dell’archivio che viene successivamente caricata nel set di migrazione.
La formula generale per calcolare lo spazio libero su disco richiesto è la seguente:
   `data store size + node store size * 1.5`

   * *data store size*: dimensione archivio dati; lo strumento Content Transfer (Trasferimento contenuti) utilizza 64 GB, anche se l’archivio dati effettivo è più grande.
   * *node store size*: dimensione archivio nodi; dimensione della directory dell’archivio segmenti o dimensione del database MongoDB.
Pertanto, per un archivio segmenti di 20 GB, lo spazio libero su disco richiesto è di 94 GB.

* È necessario mantenere un set di migrazione per l’intera durata dell’attività di trasferimento dei contenuti per supportare l’integrazione dei contenuti. Poiché è possibile creare e mantenere un massimo di dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti, si consiglia di suddividere di conseguenza l’archivio dei contenuti. In questo modo si evita di esaurire i set di migrazione.

## Considerazioni importanti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti) {#important-considerations}

Segui le indicazioni riportate in questa sezione per comprendere le valutazioni importanti durante l’esecuzione dello strumento Content Transfer (Trasferimento contenuti):

* Il requisito minimo di sistema per lo strumento Content Transfer (Trasferimento contenuti) è AEM 6.3 o versione successiva e Java™ 8. Se utilizzi una versione AEM inferiore, devi aggiornare l’archivio dei contenuti a AEM 6.5 per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Java™ deve essere configurato nell&#39;ambiente AEM, in modo che `java` può essere eseguito dall&#39;utente che avvia AEM.

* Disinstalla le versioni precedenti dello strumento Content Transfer (Trasferimento contenuti) durante l’installazione della versione 1.3.0, a causa di una modifica importante dell’architettura dello strumento. Con 1.3.0, devi anche creare i set di migrazione ed eseguire nuovamente l’estrazione e l’acquisizione sui nuovi set di migrazione.

* Lo strumento Content Transfer (Trasferimento contenuti) può essere utilizzato con i seguenti tipi di archivio dati: archivio dati file, archivio dati S3, archivio dati S3 condiviso e archivio dati archivio BLOB di Azure.

* Se si utilizza un *Ambiente sandbox*, assicurati che l’ambiente sia aggiornato alla versione più recente. Se utilizzi un *ambiente di produzione*, viene aggiornato automaticamente.

* Per utilizzare lo strumento Content Transfer (Trasferimento contenuti), devi essere un utente amministratore nell’istanza sorgente e appartenere all’AEM locale **amministratori** nell’istanza del Cloud Service a cui stai trasferendo il contenuto. Gli utenti non autorizzati non possono recuperare il token di accesso per utilizzare lo strumento Content Transfer (Trasferimento contenuti).

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** se questa opzione è abilitata, elimina l’intero archivio esistente e crea un archivio in cui acquisire il contenuto. Questo flusso di lavoro comporta il ripristino di tutte le impostazioni, incluse le autorizzazioni, nell’istanza del Cloud Service di destinazione. Questo risultato è valido anche per un utente amministratore che viene aggiunto al **dell&#39;amministratore** gruppo. L’utente deve essere letto sul **dell&#39;amministratore** per recuperare il token di accesso per lo strumento Content Transfer (Trasferimento contenuti).

* Lo strumento Content Transfer (Trasferimento contenuti) non supporta l’unione di contenuti da più origini nell’istanza del Cloud Service di destinazione se il contenuto dalle due origini viene spostato negli stessi percorsi sulla destinazione. Per spostare il contenuto da più origini in un’unica istanza del Cloud Service target, è necessario assicurarsi che non vi sia alcuna sovrapposizione dei percorsi del contenuto dalle origini.

* Il token di accesso può scadere periodicamente dopo un periodo di tempo specifico o dopo l’aggiornamento dell’ambiente del Cloud Service. Se il token di accesso è scaduto, non è possibile connettersi all’istanza di Cloud Service. In questo caso, devi recuperare il nuovo token di accesso. L’icona di stato associata a un set di migrazione esistente diventa una nuvola rossa e visualizza un messaggio quando ci passi sopra con il cursore.

* Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferirlo dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione del contenuto in un ambiente di pubblicazione. Qualsiasi contenuto specificato nel set di migrazione viene acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author, Publish o entrambe. Durante lo spostamento di contenuti in un’istanza Production, installa CTT nell’istanza Author di origine per spostare i contenuti nell’istanza Author di destinazione. Allo stesso modo, installa CTT sull’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Consulta [Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza Publish](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) per ulteriori dettagli.

* Gli utenti e i gruppi trasferiti dallo strumento Content Transfer (Trasferimento contenuti) sono solo quelli necessari per il contenuto per soddisfare le autorizzazioni. Il *Estrazione* processo copia l&#39;intero `/home` nel set di migrazione e nel *Acquisizione* process copia tutti gli utenti e i gruppi a cui si fa riferimento negli ACL dei contenuti migrati. Per mappare automaticamente gli utenti e i gruppi esistenti ai loro ID IMS, consulta [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).

* Durante la fase di estrazione, lo strumento Content Transfer (Trasferimento contenuti) viene eseguito su un’istanza sorgente di AEM attiva.

* Dopo aver completato *Estrazione* fase del processo di trasferimento dei contenuti e prima di avviare *Fase di acquisizione* per inserire contenuti nell’AEM as a Cloud Service *Fase* o *Produzione* istanze, registra un ticket di supporto. Notifica all&#39;Adobe la tua intenzione di eseguire *Acquisizione* in modo che Adobe possa garantire che non si verifichino interruzioni durante *Acquisizione* processo. Registra il ticket di supporto una settimana prima del periodo pianificato *Acquisizione* data. Dopo aver inviato il ticket di supporto, il team di supporto fornisce indicazioni sui passaggi successivi. Registra un ticket di supporto con i seguenti dettagli:

   * Data esatta e ora stimata (con il fuso orario) in cui intendi avviare il *Acquisizione* fase.
   * Tipo di ambiente (stage o produzione) in cui intendi acquisire i dati.
   * ID programma.

* Il *Fase di acquisizione* per l’authoring riduce l’intera implementazione di authoring. Questo processo significa che l’AEM dell’autore non è disponibile durante l’intero processo di acquisizione. Inoltre, assicurati che non vengano eseguite pipeline di Cloud Manager mentre esegui il *Acquisizione* fase.

* Quando si utilizza `Amazon S3` o `Azure` come archivio dati sul sistema AEM di origine, l’archivio dati deve essere configurato in modo che i BLOB memorizzati non possano essere eliminati (garbage collection). In questo modo viene garantita l’integrità dei dati di indice e, se non si configura questa modalità, le estrazioni potrebbero non riuscire a causa della mancanza di integrità dei dati di indice.

* Se utilizzi gli indici personalizzati, assicurati di configurarli con `tika` prima di eseguire lo strumento Content Transfer (Trasferimento contenuti). Fai riferimento a [Preparazione della nuova definizione dell’indice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en#preparing-the-new-index-definition) per ulteriori dettagli.

* Se desideri eseguire integrazioni, assicurati che la struttura del contenuto esistente non venga modificata dal momento in cui viene eseguita l’estrazione iniziale a quello in cui viene eseguita l’estrazione integrativa. I top up non possono essere eseguiti su contenuti la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questo passaggio durante il processo di migrazione.

* Se desideri includere le versioni come parte di un set di migrazione ed esegui integrazioni con `wipe=false`, devi quindi disabilitare l’eliminazione della versione a causa di una limitazione corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione delle versioni e stai eseguendo integrazioni in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.

## Passaggio successivo {#whats-next}

Dopo aver appreso le linee guida, le best practice e le considerazioni importanti sull’utilizzo dello strumento Content Transfer (Trasferimento contenuti), puoi procedere all’installazione e all’utilizzo dello strumento, a partire dalla creazione di un set di migrazione. Consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it) per ulteriori informazioni.
