---
title: Release Notes for Cloud Manager in AEM as a Cloud Service Release 2022.02.0
description: These are the release notes for Cloud Manager in AEM as a Cloud Service release 2022.02.0.
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 8162d1d6ddeff867507f749f223c0111b6856122
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2022.02.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

The release date for Cloud Manager in AEM as a Cloud Service 2022.02.0 is 10 February 2022. La prossima versione è prevista per il 10 marzo 2022.

## Novità {#what-is-new}

* New accelerated [Web Tier Config pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) have been introduced to exclusively deploy HTTPD/dispatcher configuration.
   * È necessario utilizzare AEM versione `2021.12.6151.20211217T120950Z` o più recenti e [consenso alla modalità flessibile degli strumenti del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per utilizzare questa funzione.
   * This feature will be rolled out in a phased approach over the two weeks following the 2022.02.0 release.
* The Cloud Manager landing page experience has been refreshed to deliver improved navigation, easy switching between grid/tile views, and pop-overs for quick program summary.
* Una nuova soglia di errore (`< D`) è stato aggiunto al [metrica di valutazione dell’affidabilità.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Customers with severe quality issues that impact system stability, primarily related to invalid indexes and workflow processes, will not be able to deploy until those issues are resolved.
* La gravità del `BannedPath` [regola di qualità](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) è stato modificato da blocker a critico.
* La procedura guidata della pipeline informerà l’utente quando potrebbe essere necessario un aggiornamento dell’ambiente AEM prima di configurare un [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associato.

## Correzioni di bug {#bug-fixes}

* Le password dell’archivio Git precedente ora vengono sempre invalidate quando viene generata una nuova password.
* Updating environment variables through the API no longer interferes with a pipeline execution in rare situations.
