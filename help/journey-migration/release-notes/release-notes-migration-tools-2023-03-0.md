---
title: Note sulla versione 2023.03.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2023.03.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 7%

---

# Note sulla versione 2023.03.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2023.03.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.40 è il 3 marzo 2023.

### Novità {#what-is-new-bpa}

* BPA ora può rilevare e segnalare i nodi in conflitto: nodi con lo stesso `jcr:uuid`. Tali risultati sono contrassegnati come critici in quanto possono causare errori di acquisizione dei contenuti durante lo spostamento dei contenuti in AEM as a Cloud Service.
* BPA è ora in grado di rilevare e creare rapporti sull’utilizzo dei listener di eventi. Si consiglia di eseguire il refactoring di questo tipo di meccanismo di gestione degli eventi ai processi sling durante il passaggio ad AEM as a Cloud Service.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava falsi positivi su `grouprendercondition`. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v2.0.16 è il 8 marzo 2023.

### Novità {#what-is-new-ctt}

* La mappatura utente è stata semplificata e integrata nel passaggio di estrazione dei contenuti. Non è necessaria alcuna configurazione e, per impostazione predefinita, la mappatura utente viene eseguita automaticamente quando l’utente avvia l’estrazione del contenuto. L’utente ha la possibilità di disabilitare la mappatura utente, se necessario. Ulteriori informazioni [qui.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html#user-mapping-detail)
* Il passaggio di precopia con [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è stato integrato con lo strumento Content Transfer per velocizzare notevolmente le estrazioni di contenuto. La precopia viene configurata e installata automaticamente quando questa versione del CTT viene installata. Per impostazione predefinita, quando viene avviata l’estrazione, la precopia viene eseguita automaticamente per set di migrazione di dimensioni superiori a 200 GB. L’utente ha la possibilità di disattivarla, se necessario. Ulteriori informazioni [qui.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html)
* CTT può ora essere utilizzato sui server Windows.

### Correzioni di bug {#bug-fixes-ctt}

* Sono state apportate diverse correzioni di bug per migliorare la resilienza dell’estrazione dei contenuti.
