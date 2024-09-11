---
title: Note sulla versione 2024.05.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2024.05.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 6%

---

# Note sulla versione 2024.05.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2024.05.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.50 è maggio 2024.

### Novità {#what-is-new-bpa}

* Best Practices Analyzer (BPA) ora supporta il caricamento automatico dei rapporti generati da BPA direttamente in Cloud Acceleration Manager (CAM). Gli utenti non dovranno più scaricare manualmente il rapporto e caricarlo in CAM. Per ulteriori dettagli, vedi [Utilizzo di Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### Correzioni di bug {#bug-fixes-bpa}

* Best Practices Analyzer ora rileva tutti i nodi di dimensioni superiori a 16 MB
* È stata risolta una situazione di tipo &quot;race condition&quot; che causava occorrenze sproradiche di reperti NCC.

## Cloud Acceleration Manager {#cam-release}

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager (CAM) ora supporta il caricamento automatico dei rapporti generati da BPA direttamente in CAM. Per ulteriori informazioni, consulta [Fase di preparazione in Cloud Acceleration Manager - Utilizzo della scheda di analisi delle best practice](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* Cloud Acceleration Manager ora fornisce una stima della durata di un’acquisizione, in base a fattori quali il conteggio dei nodi, le dimensioni dell’archivio dati e così via. Ulteriori informazioni con [Acquisizione del contenuto nel Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
