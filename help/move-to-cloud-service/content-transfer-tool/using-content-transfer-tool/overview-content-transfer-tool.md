---
title: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
description: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 74%

---

# Panoramica {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Panoramica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare il contenuto esistente da un’istanza di AEM di origine (on-premise o AMS) all’istanza di AEM Cloud Service di destinazione. Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi)."
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

* È possibile creare e mantenere fino a dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
* Ogni set di migrazione deve avere un nome univoco.
* Se un set di migrazione è rimasto inattivo per più di 30 giorni, viene eliminato automaticamente.
* Ogni volta che crei un set di migrazione, questo viene associato a un ambiente specifico. Puoi acquisire solo in un’istanza di authoring o pubblicazione dello stesso ambiente.


Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Nella fase di estrazione, per ***integrare*** un set di migrazione esistente, l’opzione di *sovrascrittura* deve essere disattivata. Per ulteriori informazioni, consulta [Estrazione integrativa](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process).

Nella fase di acquisizione, per applicare il contenuto delta sul contenuto corrente, l’opzione *Cancella* deve essere disattivata. Per ulteriori informazioni, consulta [Acquisizione integrativa](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process).


