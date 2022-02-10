---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.02.0
description: Queste sono le note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.02.0.
feature: Release Information
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2022.02.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2022.02.0 è il 10 febbraio 2022. La prossima versione è prevista per il 10 marzo 2022.

## Novità {#what-is-new}

* Nuova accelerazione [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) sono stati introdotti per distribuire esclusivamente la configurazione HTTPD/dispatcher
   * È necessario utilizzare AEM versione `2021.12.6151.20211217T120950Z` per utilizzare questa funzione.
   * Questa funzione verrà implementata in un approccio graduale nelle due settimane successive al rilascio della versione 2022.02.0.
* L’esperienza della pagina di destinazione di Cloud Manager è stata aggiornata per fornire una navigazione migliore, un passaggio semplice tra le visualizzazioni griglia/riquadro e pop-up per un riepilogo rapido del programma.
* Una nuova soglia di errore (`< D`) è stato aggiunto al [metrica di valutazione dell’affidabilità.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * I clienti con gravi problemi di qualità che influiscono sulla stabilità del sistema, principalmente correlati a indici e processi di flusso di lavoro non validi, non saranno in grado di distribuire fino a quando tali problemi non saranno risolti.
* La gravità del `BannedPath` [regola di qualità](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) è stato modificato da blocker a critico.
* La procedura guidata della pipeline informerà l’utente quando potrebbe essere necessario un aggiornamento dell’ambiente AEM prima di configurare un [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associato.

## Correzioni di bug {#bug-fixes}

* Le password dell’archivio Git precedente ora vengono sempre invalidate quando viene generata una nuova password.
* L’aggiornamento delle variabili di ambiente tramite l’API non interferisce più con l’esecuzione di una pipeline in rare situazioni.
