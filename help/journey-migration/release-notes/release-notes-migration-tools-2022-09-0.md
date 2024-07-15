---
title: Note sulla versione 2022.9.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.9.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---

# Note sulla versione 2022.9.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2022.9.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di pubblicazione di Best Practices Analyzer v2.1.34 è il 12 settembre 2022.

### Novità {#what-is-new-bpa}

* BPA ora può rilevare e segnalare se il cliente ha aggiunto una configurazione di logger personalizzata. AEM as a Cloud Service non supporta i file di registro personalizzati. Tutti i file di registro devono essere reindirizzati a `error.log`
* BPA ora può creare rapporti sui diversi tipi MIME binari presenti nell’archivio del cliente e sui conteggi ad essi associati.

### Correzioni di bug {#bug-fixes-bpa}

* Nell’interfaccia utente BPA si sono verificati problemi di rendering quando si visualizzava un numero elevato di risultati in un singolo modello. Questo problema è stato risolto.
* BPA riportava erroneamente alcuni risultati come modifiche non compatibili con gravità critica. Questo problema è stato risolto.
