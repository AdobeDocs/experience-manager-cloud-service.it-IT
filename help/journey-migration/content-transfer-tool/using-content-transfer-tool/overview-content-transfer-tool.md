---
title: Panoramica dello strumento Content Transfer (Trasferimento contenuti)
description: Scopri come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per trasferire contenuti da un’istanza AEM on-premise a AEM as a Cloud Service
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 9c45a46bc50625301529d5433c78fc9c706f8071
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 54%

---

# Panoramica {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Panoramica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) è stato sviluppato da Adobe e può essere utilizzato per spostare i contenuti esistenti da un’istanza AEM di origine (on-Premise o AMS) all’istanza di destinazione AEM Cloud Service. Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi)."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it" text="Linee guida e best practice"

Lo strumento Content Transfer (Trasferimento contenuti) è uno strumento sviluppato da Adobe che può essere utilizzato per avviare la migrazione dei contenuti esistenti da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione.

Questo strumento trasferisce automaticamente anche entità principali (utenti o gruppi).  Consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) per ulteriori informazioni.

Lo strumento Content Transfer (Trasferimento contenuti) integra il processo di trasferimento dei contenuti con Cloud Acceleration Manager. In questo modo l’utente dispone di tutti i vantaggi che offre:

* Modalità self-service per estrarre un set di migrazione in una sola volta e trasferirlo in più ambienti in parallelo
* Miglioramento dell&#39;esperienza utente grazie a migliori stati di caricamento, guardrail e gestione degli errori
* I registri di acquisizione vengono mantenuti e sono sempre disponibili per la risoluzione dei problemi
* I report di convalida e migrazione entità sono disponibili per la convalida

## Fasi nello strumento Content Transfer (Trasferimento contenuti) {#phases-content-transfer-tool}

Il trasferimento dei contenuti prevede due fasi:

1. **Estrazione**: per estrazione si intende l’estrazione dei contenuti dall’istanza AEM di origine in un’area temporanea denominata *set di migrazione*. Un *set di migrazione* è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service.

   Consulta [Processo di estrazione nel trasferimento dei contenuti](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) per ulteriori dettagli.

   >[!NOTE]
   >La mappatura degli utenti viene ora eseguita automaticamente come parte della fase di estrazione sull’autore (ma può essere facoltativamente disabilitata sull’autore o abilitata sulla pubblicazione). Consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) per ulteriori dettagli.

1. **Acquisizione**: per acquisizione si intende l’acquisizione dei contenuti dal *set di migrazione* nell’istanza Cloud Service di destinazione.

   Vedi [Processo di acquisizione nel trasferimento contenuti](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per ulteriori dettagli.

## Attributi di un set di migrazione {#attributes-migration-set}

Un set di migrazione ha i seguenti attributi:

* Con la nuova versione, puoi creare un massimo di venti set di migrazione all’interno di un progetto creato in Cloud Acceleration Manager.
* Ogni set di migrazione deve avere un nome univoco.

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.

Nella fase di estrazione, per ***integrare*** un set di migrazione esistente, l’opzione di *sovrascrittura* deve essere disattivata. Consulta [Estrazione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) per ulteriori dettagli.

Nella fase di acquisizione, per applicare il contenuto delta sul contenuto corrente, l’opzione *Cancella* deve essere disattivata. Consulta [Acquisizione integrativa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) per ulteriori dettagli.

## Scadenza set di migrazione {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="Scadenza di un set di migrazione"
>abstract="Ottieni informazioni sulla scadenza di un set di migrazione."

Tutti i set di migrazione scadranno dopo un periodo prolungato di inattività di circa 90 giorni. Una volta visualizzati gli indicatori sulla scheda del progetto e sulle righe della tabella del processo di migrazione per un periodo di tempo, il set di migrazione scadrà e i relativi dati non saranno più disponibili. Il termine di scadenza può essere facilmente prorogato agendo sulla migrazione impostata da:

* modifica della descrizione
* ottenimento della chiave di estrazione
* esecuzione di un’estrazione
* esecuzione di un’acquisizione da esso

La scadenza di un set di migrazione può essere monitorata nella riga Set di migrazione. Un utile indicatore visivo che un set di migrazione si sta avvicinando alla data di scadenza ha aggiunto anche la scheda del progetto.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## Passaggio successivo {#whats-next}

Dopo aver studiato lo strumento Content Transfer (Trasferimento contenuti), e la panoramica che descrive come lo si può utilizzare per spostare il contenuto esistente da un’istanza di AEM di origine (on-premise o AMS) all’istanza di AEM Cloud Service di destinazione, devi consultare i [Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).
