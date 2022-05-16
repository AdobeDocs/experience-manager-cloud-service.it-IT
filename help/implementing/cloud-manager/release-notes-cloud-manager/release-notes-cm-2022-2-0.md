---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.02.0
description: Queste sono le note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.02.0.
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2022.02.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2022.02.0 è il 10 febbraio 2022. La prossima versione è prevista per il 10 marzo 2022.

## Novità {#what-is-new}

* Sono state introdotte nuove [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) accelerate per distribuire esclusivamente la configurazione HTTPD/dispatcher.
   * È necessario utilizzare AEM versione `2021.12.6151.20211217T120950Z` o più recente e [dare il consenso alla modalità flessibile degli strumenti del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per utilizzare questa funzione.
   * Questa funzione verrà implementata gradualmente nelle due settimane successive al rilascio della versione 2022.02.0.
* L’esperienza della pagina di destinazione di Cloud Manager è stata aggiornata per migliorarne la navigazione e facilitare il passaggio tra le visualizzazioni a griglia o a schede. Inoltre fornisce delle informazioni a comparsa per un rapido riepilogo del programma.
* Una nuova soglia di errore (`< D`) è stata aggiunta alla [metrica di valutazione dell’affidabilità.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * I clienti che riscontrano gravi problemi di qualità che influiscono sulla stabilità del sistema, principalmente dovuti a indici e processi di flusso di lavoro non validi, potranno procedere alla distribuzione solo dopo che tali problemi saranno stati risolti.
* La gravità della `BannedPath` [regola di qualità](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)  è stata modificata da bloccante a critica.
* La procedura guidata della pipeline informerà l’utente quando potrebbe essere necessario un aggiornamento dell’ambiente AEM prima di configurare una [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associata.

## Correzioni di bug {#bug-fixes}

* Le password dell’archivio Git precedente ora vengono sempre invalidate quando viene generata una nuova password.
* L’aggiornamento delle variabili di ambiente tramite l’API non interferisce più con l’esecuzione di una pipeline in rare situazioni.
