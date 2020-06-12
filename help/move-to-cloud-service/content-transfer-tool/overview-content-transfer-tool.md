---
title: Panoramica sullo strumento di trasferimento dei contenuti
description: Panoramica sullo strumento di trasferimento dei contenuti
translation-type: tm+mt
source-git-commit: 1ca9b2091befbafad0878d83fc7963c779146b2a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# Panoramica {#overview-content-transfer-tool}

Content Transfer Tool è uno strumento sviluppato da Adobe che può essere utilizzato per spostare il contenuto esistente da un’istanza di AEM di origine (locale o AMS) all’istanza di AEM Cloud Service di destinazione.

Questo strumento trasferisce automaticamente entità (utenti o gruppi).

Il trasferimento di contenuto è associato a due fasi:

1. **Estrazione**:  Per estrazione si intende l’estrazione di contenuto dall’istanza AEM di origine in un’area temporanea denominata set *di* migrazione. Un set *di* migrazione è un&#39;area di archiviazione cloud fornita da Adobe per memorizzare temporaneamente il contenuto trasferito tra l&#39;istanza AEM di origine e l&#39;istanza AEM del servizio cloud.

   Per ulteriori informazioni, consulta Processo di [estrazione in Trasferimento](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) contenuto.

2. **Ingestione**: Per &quot;inserimento&quot; si intende l’assimilazione del contenuto dal set *di* migrazione nell’istanza del servizio Cloud di destinazione.

   Per ulteriori informazioni, consultate Processo di [inserimento in Trasferimento](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) contenuti.

Un set *di* migrazione ha i seguenti attributi:

* Durante l&#39;attività di trasferimento dei contenuti è possibile creare e mantenere fino a quattro set di migrazione alla volta.
* Ogni set di migrazione deve avere un nome univoco.
* Se un set di migrazione è rimasto inattivo per più di 30 giorni, verrà eliminato automaticamente.
* Ogni volta che create un set di migrazione, questo viene associato a un ambiente specifico. Potete inserire solo un’istanza di creazione o pubblicazione dello stesso ambiente.

Content Transfer Tool dispone di una funzione che supporta l&#39;integrazione dei contenuti differenziali dove è possibile trasferire solo le modifiche apportate dall&#39;attività di trasferimento dei contenuti precedente.

>[!NOTE]
> Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti aggiunte differenziali per ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali prima di iniziare a utilizzare il servizio Cloud.

Nella fase di estrazione, per ***completare*** un set di migrazione esistente, l’opzione di *sovrascrittura* deve essere disattivata. Per ulteriori informazioni, consulta [Estrazione](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) dall’alto.

Nella fase di assimilazione, per applicare il contenuto delta sopra al contenuto corrente, l&#39;opzione *wipe* deve essere disattivata. Per ulteriori informazioni, consulta [Ingestione](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) dall’alto.


## Linee guida e best practice {#best-practices}

Seguite la sezione seguente per comprendere le linee guida e le procedure ottimali per l’utilizzo dello strumento di trasferimento dei contenuti:

* È consigliabile eseguire i controlli di compattazione, di coerenza dell&#39;archivio dei dati prima della consegna per individuare potenziali problemi e ridurre anche i rifiuti presenti nel repository.

* Se la configurazione di AEM Cloud Author Content Delivery Network (CDN) è configurata per disporre di una whitelist di IP, è necessario assicurarsi che anche gli IP dell&#39;ambiente di origine vengano aggiunti alla whitelist in modo che l&#39;ambiente di origine e l&#39;ambiente AEM Cloud possano comunicare tra loro.

* Nella fase di assimilazione, si consiglia di eseguire l’assimilazione utilizzando la modalità *wipe* abilitata, in cui l’archivio esistente (autore o pubblicazione) nell’ambiente di destinazione AEM Cloud Service verrà completamente eliminato e quindi aggiornato con i dati del set di migrazione. Questa modalità è molto più veloce della modalità non-wipe, in cui il set di migrazione viene applicato sopra il contenuto corrente.

* Al termine dell&#39;attività di trasferimento del contenuto, nell&#39;ambiente Servizio cloud è necessaria la struttura di progetto corretta per garantire il corretto rendering del contenuto nell&#39;ambiente Servizio Cloud.

* Prima di eseguire lo strumento di trasferimento dei contenuti, è necessario assicurarsi che nella `crx-quickstart` sottodirectory dell’istanza AEM di origine vi sia spazio sufficiente. Questo perché Content Transfer Tool crea una copia locale del repository che viene successivamente caricata nel set di migrazione.
La formula generale per calcolare lo spazio libero richiesto è la seguente:
   `data store size + node store size * 1.5`

   * *dimensione* archivio dati: lo Strumento di trasferimento dei contenuti utilizza 64 GB, anche se l&#39;archivio dati effettivo è più grande.
   * *dimensione*archivio nodi: dimensione della directory dell&#39;archivio segmenti o della dimensione del database MongoDB.
Pertanto, per un segmento di dimensioni dello store pari a 20 GB, lo spazio libero su disco richiesto è di 94 GB.