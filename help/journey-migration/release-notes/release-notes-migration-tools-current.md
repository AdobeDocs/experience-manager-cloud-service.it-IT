---
title: Note sulla versione 2023.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2022.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 586fbc136b866be149db1d4fcdd6ea2ef18a97b1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 9%

---

# Note sulla versione 2023.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.03.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.40 è il 03 marzo 2023.

### Novità {#what-is-new-bpa}

* BPA è ora in grado di rilevare e segnalare i nodi in conflitto, ovvero i nodi con lo stesso `jcr:uuid`. Tali risultati sono contrassegnati come critici in quanto possono causare errori di acquisizione dei contenuti durante lo spostamento dei contenuti a AEM as a Cloud Service.
* BPA è ora in grado di rilevare e creare rapporti sull’utilizzo dei listener di eventi. Si consiglia di rieseguire il factoring di questo tipo di meccanismo di gestione degli eventi sui processi sling durante il passaggio a AEM as a Cloud Service.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava falsi positivi per `grouprendercondition`. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v2.0.16 è il 8 marzo 2022.

### Novità {#what-is-new-ctt}

* La mappatura utente è stata semplificata e integrata nel passaggio di estrazione dei contenuti. Non è necessaria alcuna configurazione e, per impostazione predefinita, la mappatura utente viene eseguita automaticamente quando l’utente avvia l’estrazione del contenuto. L’utente ha la possibilità di disabilitare la mappatura utente, se necessario. Ulteriori informazioni [qui.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* Il passaggio di precopia tramite [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) è stato integrato con lo strumento Content Transfer (Trasferimento contenuti) per velocizzare notevolmente le estrazioni di contenuti. La precopia viene configurata e installata automaticamente quando questa versione del CTT viene installata. Per impostazione predefinita, quando viene avviata l’estrazione, la precopia viene eseguita automaticamente per set di migrazione di dimensioni superiori a 200 GB. L’utente ha la possibilità di disattivarla, se necessario. Ulteriori informazioni [qui.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* CTT può ora essere utilizzato sui server Windows.

### Correzioni di bug {#bug-fixes-ctt}

* Sono state apportate diverse correzioni di bug per migliorare la resilienza dell’estrazione dei contenuti.
