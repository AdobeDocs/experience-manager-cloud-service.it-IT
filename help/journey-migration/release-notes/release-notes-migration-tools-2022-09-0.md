---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.9.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.9.0
feature: Release Information
source-git-commit: d6c47c3b8fe4ac994ee9f2db365888f496be12f0
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.9.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.9.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.34 è il 12 settembre 2022.

### Novità {#what-is-new-bpa}

* BPA ora può rilevare e segnalare se il cliente ha aggiunto una configurazione di logger personalizzata. AEM as a Cloud Service non supporta i file di registro personalizzati. Tutti i file di registro devono essere inviati a `error.log`
* BPA può ora generare rapporti sui diversi tipi MIME binari presenti nell’archivio del cliente e sui conteggi associati ad essi.

### Correzioni di bug {#bug-fixes-bpa}

* L’interfaccia utente BPA ha avuto problemi di rendering durante la visualizzazione di un gran numero di risultati in un unico pattern. Questo problema è stato risolto.
* BPA segnalava erroneamente alcuni risultati come modifiche non compatibili con gravità critica. Questo problema è stato risolto.
