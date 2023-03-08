---
title: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
description: Panoramica sullo strumento Content Transfer (Trasferimento contenuti)
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 5a4592531377109fba88b5cdc9df027803feca7a
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 47%

---

# Panoramica {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Panoramica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare il contenuto esistente da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione. Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi)."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="Linee guida e best practice"

Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per spostare i contenuti esistenti da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione.

Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi).

È disponibile una nuova versione dello strumento Content Transfer (Trasferimento contenuti) che integra il processo di trasferimento dei contenuti con Cloud Acceleration Manager. Si consiglia vivamente di passare a questa nuova versione per sfruttare tutti i vantaggi che offre:

* Metodo self-service per estrarre un set di migrazione una volta e acquisirlo in più ambienti in parallelo
* Miglioramento dell&#39;esperienza utente grazie a migliori stati di caricamento, guardrail e gestione degli errori
* I registri di acquisizione sono persistenti e sono sempre disponibili per la risoluzione dei problemi

Per iniziare a utilizzare la nuova versione, è necessario disinstallare le versioni precedenti dello strumento Content Transfer (Trasferimento contenuti), a causa di una modifica importante dell’architettura dello strumento.

>[!NOTE]
>
> Per le situazioni in cui è già in corso una migrazione, puoi continuare a utilizzare la versione precedente di CTT fino al completamento della migrazione. Per la documentazione relativa alla versione precedente di CTT, consulta [documentazione legacy](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## Fasi nello strumento Content Transfer (Trasferimento contenuti) {#phases-content-transfer-tool}

Il trasferimento dei contenuti prevede due fasi:

1. **Estrazione**: per estrazione si intende l’estrazione dei contenuti dall’istanza AEM di origine in un’area temporanea denominata *set di migrazione*. Un *set di migrazione* è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service.

   Per ulteriori informazioni, consulta [Processo di estrazione nel trasferimento dei contenuti](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md).

   >[!NOTE]
   >La mappatura degli utenti viene ora eseguita automaticamente come parte della fase di estrazione sull’autore (ma può essere facoltativamente disabilitata sull’autore o abilitata sulla pubblicazione). Consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) per ulteriori dettagli.

1. **Acquisizione**: per acquisizione si intende l’acquisizione dei contenuti dal *set di migrazione* nell’istanza Cloud Service di destinazione.

   Consulta [Processo di acquisizione nel trasferimento dei contenuti](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per ulteriori dettagli.

## Attributi di un set di migrazione {#attributes-migration-set}

Un set di migrazione ha i seguenti attributi:

* Con la nuova versione, puoi creare un massimo di cinque set di migrazione all’interno di un progetto creato in Cloud Acceleration Manager.
* Ogni set di migrazione deve avere un nome univoco.

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Nella fase di estrazione, per ***integrare*** un set di migrazione esistente, l’opzione di *sovrascrittura* deve essere disattivata. Per ulteriori informazioni, consulta [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).

Nella fase di acquisizione, per applicare il contenuto delta sul contenuto corrente, l’opzione *Cancella* deve essere disattivata. Per ulteriori informazioni, consulta [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process).

## Passaggio successivo {#whats-next}

Dopo aver appreso le informazioni sullo strumento Content Transfer (Trasferimento contenuti) e la relativa panoramica, che descrive questo strumento, puoi spostare il contenuto esistente da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione. [Prerequisiti per lo strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).
