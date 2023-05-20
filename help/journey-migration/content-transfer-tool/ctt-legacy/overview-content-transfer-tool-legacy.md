---
title: Panoramica dello strumento Content Transfer (Trasferimento contenuti) (precedente)
description: Panoramica dello strumento Content Transfer (Trasferimento contenuti)
hide: true
hidefromtoc: true
exl-id: dd031580-e9d7-461e-8689-9bc3dbb2121b
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 70%

---

# Panoramica dello strumento Content Transfer (Trasferimento contenuti) (precedente) {#overview-content-transfer-tool}

Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare i contenuti esistenti da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione.

Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi).

## Fasi nello strumento Content Transfer (Trasferimento contenuti) {#phases-content-transfer-tool}

Il trasferimento dei contenuti prevede due fasi:

1. **Estrazione**: per estrazione si intende l’estrazione dei contenuti dall’istanza AEM di origine in un’area temporanea denominata *set di migrazione*. Un *set di migrazione* è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service.

   Per ulteriori informazioni, consulta [Processo di estrazione nel trasferimento dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=it).

   >[!NOTE]
   >Eseguite lo strumento di mappatura utente durante la fase di estrazione. Vedi [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) per ulteriori dettagli.

1. **Acquisizione**: per acquisizione si intende l’acquisizione dei contenuti dal *set di migrazione* nell’istanza Cloud Service di destinazione.

   Vedi [Processo di acquisizione nel trasferimento contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) per ulteriori dettagli.

## Attributi di un set di migrazione {#attributes-migration-set}

Un set di migrazione ha i seguenti attributi:

* Durante l’attività di trasferimento dei contenuti è possibile creare e mantenere fino a un massimo di dieci set di migrazione alla volta.
* Ogni set di migrazione deve avere un nome univoco.
* Se un set di migrazione è inattivo da più di 30 giorni, viene eliminato automaticamente.
* Ogni volta che crei un set di migrazione, questo viene associato a un ambiente specifico. Puoi acquisire solo in un’istanza di authoring o pubblicazione dello stesso ambiente.


Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Nella fase di estrazione, per ***top up*** un set di migrazione esistente, il *sovrascrivi* L&#39;opzione deve essere disabilitata. Per ulteriori informazioni, consulta [Estrazione integrativa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process).

Nella fase di acquisizione, per applicare il contenuto delta sul contenuto corrente, l’opzione *Cancella* deve essere disattivata. Per ulteriori informazioni, consulta [Acquisizione integrativa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process).

## Passaggio successivo {#whats-next}

Dopo aver ricevuto informazioni sullo strumento Content Transfer (Trasferimento contenuti) e sulla relativa panoramica, puoi utilizzare questo strumento per spostare il contenuto esistente da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione. Revisione [Prerequisiti per lo strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
