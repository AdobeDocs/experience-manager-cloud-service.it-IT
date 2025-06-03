---
title: Guida introduttiva agli strumenti di refactoring
description: Scopri come iniziare a utilizzare gli strumenti di refactoring di AEM
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: fa65b489d54d5333811145a1875a8f6fc89317bc
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---


>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Panoramica"
>abstract="Strumenti di refactoring è una soluzione sviluppata da Adobe per facilitare il refactoring dei progetti AEM esistenti al fine di garantirne la compatibilità con AEM as a Cloud Service. Gli strumenti vengono eseguiti tramite Cloud Acceleration Manager (CAM) e automatizzano le principali attività di modernizzazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=it" text="Linee guida e best practice"

# Guida introduttiva agli strumenti di refactoring {#getting-started-refactoring-tools}

**Strumenti di refactoring** semplifica il processo di aggiornamento dei progetti AEM esistenti per renderli compatibili con **AEM as a Cloud Service (AEMaaCS)**. Questi strumenti automatizzano le attività comuni di refactoring e modernizzazione e sono integrati con il **Cloud Acceleration Manager (CAM)** per un&#39;esperienza fluida.

Precedentemente disponibile solo come utility CLI, gli strumenti di refactoring offrono ora un&#39;interfaccia unificata con funzioni quali ispezione automatizzata, generazione della configurazione ed esecuzione dei processi, riducendo il sovraccarico manuale e migliorando la visibilità.

&#x200B;---

## Flusso di lavoro di ispezione {#inspection-workflow}

Il **flusso di lavoro di ispezione** semplifica il processo di preparazione per l&#39;esecuzione degli strumenti di refactoring.

### Caratteristiche principali:

* **Attivatore automatico** - Il caricamento di un progetto avvia automaticamente l&#39;ispezione.
* **Generazione configurazione** - Gli strumenti controllano il codice sorgente caricato e generano le configurazioni necessarie.
* **Invio payload** - Queste configurazioni vengono passate direttamente agli strumenti selezionati per l&#39;esecuzione.

&#x200B;---

## Strumenti di refactoring disponibili

### Modernizzatore dell&#39;archivio {#repo-modernizer}

Il **Repository Modernizer** ristruttura il layout e il contenuto dell&#39;archivio del progetto AEM per allinearli agli standard e alle best practice di AEMaaCS. Sostituisce lo strumento di modernizzazione dell’archivio legacy con automazione e precisione migliorate.

### Trasformatore di codice {#code-transformer}

**Code Transformer** utilizza il riconoscimento intelligente dei pattern e l&#39;analisi basata su IA per rilevare e aggiornare segmenti di codice incompatibili con AEMaaCS. Questo strumento semplifica le operazioni di migrazione e riduce le modifiche manuali al codice.

&#x200B;---

## Fasi del flusso di lavoro di refactoring {#phases-in-refactoring-tools}

Gli strumenti di refactoring seguono un processo strutturato in due fasi:

### Fase 1: Caricare Il Codice Source

* Carica il codice sorgente (in formato ZIP) utilizzando l’interfaccia CAM.
* Una volta caricato, il **flusso di lavoro di ispezione** viene attivato automaticamente per analizzare il progetto e prepararlo per l&#39;esecuzione dello strumento.

>[!NOTE]
>Durante il processo di ispezione non è consentito caricare un altro progetto.

&#x200B;---

### Fase 2: attivazione di un processo di refactoring

Dopo un&#39;ispezione corretta, è possibile eseguire uno o più strumenti di refactoring:

* **Esegui modernizzatore archivio** - Esegue la modernizzazione dell&#39;archivio.
* **Esegui trasformazione codice** - Esegue la trasformazione del codice in base all&#39;output di ispezione.
* **Esegui tutti gli strumenti insieme** - Esegue tutti gli strumenti disponibili in un&#39;unica operazione.

>[!NOTE]
>I processi di refactoring possono essere avviati solo dopo che il codice sorgente è stato caricato e ispezionato correttamente.

>[!NOTE]
>Gli utenti possono attivare più processi di refactoring in parallelo, ma ogni processo verrà eseguito separatamente.
