---
title: Panoramica sugli strumenti di refactoring
description: Scopri come iniziare a utilizzare gli strumenti di refactoring di AEM
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it" text="Guidelines and Best Practices"

-->

# Panoramica sugli strumenti di refactoring {#refactoring-tools-overview}

**Strumenti di refactoring** semplifica il processo di aggiornamento dei progetti AEM esistenti per renderli compatibili con **AEM as a Cloud Service (AEMaaCS)**. Questi strumenti automatizzano le attività comuni di refactoring e modernizzazione e sono integrati con il **Cloud Acceleration Manager (CAM)** per un&#39;esperienza fluida.

Precedentemente disponibile solo come utility CLI, gli strumenti di refactoring offrono ora un&#39;interfaccia unificata con funzioni quali ispezione automatizzata, generazione della configurazione ed esecuzione dei processi, riducendo il sovraccarico manuale e migliorando la visibilità.

## Flusso di lavoro di ispezione {#inspection-workflow}

Il **flusso di lavoro di ispezione** semplifica il processo di preparazione per l&#39;esecuzione degli strumenti di refactoring.

### Caratteristiche principali:

* **Attivatore automatico** - Il caricamento di un progetto avvia automaticamente l&#39;ispezione.
* **Generazione configurazione** - Gli strumenti controllano il codice sorgente caricato e generano le configurazioni necessarie.
* **Invio payload** - Queste configurazioni vengono passate direttamente agli strumenti selezionati per l&#39;esecuzione.

## Strumenti di refactoring disponibili

### Modernizzatore dell&#39;archivio {#repo-modernizer}

Il **Repository Modernizer** ristruttura il layout e il contenuto dell&#39;archivio del progetto AEM per allinearli agli standard e alle best practice di AEMaaCS. Sostituisce lo strumento di modernizzazione dell’archivio legacy con automazione e precisione migliorate.

### Trasformatore di codice {#code-transformer}

**Code Transformer** utilizza il riconoscimento intelligente dei pattern e l&#39;analisi basata su IA per rilevare e aggiornare segmenti di codice incompatibili con AEMaaCS. Questo strumento semplifica le operazioni di migrazione e riduce le modifiche manuali al codice.

## Fasi del flusso di lavoro di refactoring {#phases-in-refactoring-tools}

Gli strumenti di refactoring seguono un processo strutturato in due fasi:

### Fase 1: Caricare Il Codice Source

* Carica il codice sorgente (in formato ZIP) utilizzando l’interfaccia CAM.
* Una volta caricato, il **flusso di lavoro di ispezione** viene attivato automaticamente per analizzare il progetto e prepararlo per l&#39;esecuzione dello strumento.

>[!NOTE]
>Durante il processo di ispezione non è consentito caricare un altro progetto.

### Fase 2: attivazione di un processo di refactoring

Dopo un&#39;ispezione corretta, è possibile eseguire uno o più strumenti di refactoring:

* **Esegui modernizzatore archivio** - Esegue la modernizzazione dell&#39;archivio.
* **Esegui trasformazione codice** - Esegue la trasformazione del codice in base all&#39;output di ispezione.
* **Esegui tutti gli strumenti insieme** - Esegue tutti gli strumenti disponibili in un&#39;unica operazione.

>[!NOTE]
>I processi di refactoring possono essere avviati solo dopo che il codice sorgente è stato caricato e ispezionato correttamente.

>[!NOTE]
>Gli utenti possono attivare più processi di refactoring in parallelo, ma ogni processo verrà eseguito separatamente.
