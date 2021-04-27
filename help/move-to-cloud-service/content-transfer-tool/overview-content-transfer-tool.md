---
title: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
description: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
translation-type: tm+mt
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 79%

---

# Panoramica {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Panoramica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare il contenuto esistente da un’istanza di AEM di origine (on-premise o AMS) all’istanza di Cloud Service AEM di destinazione. Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi)."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Processo di estrazione"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Processo di acquisizione"

Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare i contenuti esistenti da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione.

Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi).

Il trasferimento dei contenuti prevede due fasi:

1. **Estrazione**: per estrazione si intende l’estrazione dei contenuti dall’istanza AEM di origine in un’area temporanea denominata *set di migrazione*. Un *set di migrazione* è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service.

   Per ulteriori informazioni, consulta [Processo di estrazione nel trasferimento dei contenuti](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process).

>[!NOTE]
>
> Si consiglia di eseguire lo strumento di mappatura utente come parte della fase di estrazione. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) .

1. **Acquisizione**: per acquisizione si intende l’acquisizione dei contenuti dal *set di migrazione* nell’istanza Cloud Service di destinazione.

   Per ulteriori informazioni, consulta [Processo di acquisizione nel trasferimento dei contenuti](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process).

Un *set di migrazione* ha i seguenti attributi:

* Durante l’attività di trasferimento dei contenuti è possibile creare e mantenere fino a un massimo di quattro set di migrazione alla volta.
* Ogni set di migrazione deve avere un nome univoco.
* Se un set di migrazione è rimasto inattivo per più di 30 giorni, viene eliminato automaticamente.
* Ogni volta che crei un set di migrazione, questo viene associato a un ambiente specifico. Puoi acquisire solo in un’istanza di authoring o pubblicazione dello stesso ambiente.

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Nella fase di estrazione, per ***integrare*** un set di migrazione esistente, l’opzione di *sovrascrittura* deve essere disattivata. Per ulteriori informazioni, consulta [Estrazione integrativa](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process).

Nella fase di acquisizione, per applicare il contenuto delta sul contenuto corrente, l’opzione *Cancella* deve essere disattivata. Per ulteriori informazioni, consulta [Acquisizione integrativa](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process).


## Linee guida e best practice {#best-practices}

>id=&quot;aemcloud_ctt_Guidelines&quot;
>title=&quot;Linee guida e best practice&quot;
>abstract=&quot;Rivedi le linee guida e le best practice per utilizzare lo strumento Content Transfer (Trasferimento contenuti), incluse le attività di pulizia revisioni, considerazioni sullo spazio su disco e altro ancora.&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs&quot; text=&quot;Considerazioni importanti sull’utilizzo dello strumento Content Transfer&quot;
>additional-url=&quot;https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations&quot; text=&quot;Considerazioni importanti sull&#39;utilizzo dello strumento di mappatura utenti&quot;

Leggi la sezione seguente per comprendere le linee guida e le best practice per utilizzare lo strumento Content Transfer (Trasferimento contenuti):

* È consigliabile eseguire la [pulizia delle revisioni](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/deploying/revision-cleanup.html) e i [controlli di coerenza dell’archivio dati](https://helpx.adobe.com/it/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) nell’archivio **sorgente** per identificare potenziali problemi e ridurre le dimensioni dell’archivio.

* Se la rete CDN (Content Delivery Network) di authoring di AEM Cloud è configurata per disporre di un elenco di indirizzi IP consentiti, è necessario assicurarsi che anche gli IP dell’ambiente sorgente vengano aggiunti all’elenco Consentiti in modo che l’ambiente sorgente e l’ambiente AEM Cloud possano comunicare tra loro.

* Nella fase di acquisizione, si consiglia di eseguire l’acquisizione con la modalità *Cancella* abilitata, affinché l’archivio esistente (di authoring o pubblicazione) nell’ambiente di destinazione AEM Cloud Service venga completamente eliminato e quindi aggiornato con i dati del set di migrazione. Questa modalità è molto più veloce della modalità in cui la cancellazione è disattivata e il set di migrazione viene applicato sul contenuto corrente.

* Al termine dell’attività di trasferimento dei contenuti, nell’ambiente Cloud Service è necessaria la giusta struttura di progetto per garantire il corretto rendering dei contenuti.

* Prima di eseguire lo strumento Content Transfer (Trasferimento contenuti), è necessario assicurarsi che nella sottodirectory `crx-quickstart` dell’istanza AEM sorgente vi sia spazio sufficiente. Questo perché lo strumento Content Transfer (Trasferimento contenuti) crea una copia locale dell’archivio che viene successivamente caricata nel set di migrazione.
La formula generale per calcolare lo spazio libero su disco richiesto è la seguente:
   `data store size + node store size * 1.5`

   * *data store size*: dimensione archivio dati; lo strumento Content Transfer (Trasferimento contenuti) utilizza 64 GB, anche se l’archivio dati effettivo è più grande.
   * *node store size*: dimensione archivio nodi; dimensione della directory dell’archivio segmenti o dimensione del database MongoDB.
Pertanto, per un archivio segmenti di 20 GB, lo spazio libero su disco richiesto è di 94 GB.
