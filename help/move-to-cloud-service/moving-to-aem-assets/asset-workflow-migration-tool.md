---
title: Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse)
description: 'Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 100%

---


# Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) {#asset-workflow-migration}

Lo strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) è utilizzato per migrare automaticamente i flussi di lavoro per l’elaborazione delle risorse dalle implementazioni AEM on-premise o AMS ai profili di elaborazione e alle configurazioni OSGi da utilizzare in AEM Assets as a Cloud Service.

## Introduzione {#introduction}

Questa sezione descrive le risorse e i dettagli di implementazione dello strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse).

Questa utility consente agli sviluppatori AEM di migrare ad AEM as a Cloud Service i flussi di lavoro AEM esistenti per l’elaborazione delle risorse.

## Flussi di lavoro supportati {#migration-support-for-workflows}

I vari flussi di lavoro supportano la migrazione in modo diverso. Consulta questo [elenco di flussi di lavoro specifici](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). I flussi di lavoro sono suddivisi nelle seguenti categorie in base al supporto fornito. Adobe supporta la migrazione dei flussi di lavoro elencati nelle categorie `SUPPORTED`, `REQUIRED` o `OPTIONAL`. I passaggi del flusso di lavoro indicati nelle altre categorie non sono supportati.

* `SUPPORTED`: funzionalità supportata in [!DNL Experience Manager Assets] as a Cloud Service.
* `OPTIONAL`: funzionalità opzionale in [!DNL Experience Manager Assets] as a Cloud Service.
* `REQUIRED`: passaggio obbligatorio che viene aggiunto al flusso di lavoro.
* `UNNECESSARY`: funzionalità non necessaria in [!DNL Experience Manager Assets] as a Cloud Service.
* `NUI_OOTB`: funzionalità fornita da [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: funzionalità fornita dai connettori [!DNL Dynamic Media] predefiniti.
* `NUI_MIGRATED`: migrazione a un [profilo di elaborazione per Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: attualmente non supportato in [!DNL Experience Manager Assets] as a Cloud Service.

## Installazione dello strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) {#installing-tool}

Consulta **[Git Resource: AEM Assets as a Cloud Service - Workflow Migration](https://github.com/adobe/aem-cloud-migration)** per informazioni sull’installazione e la compilazione del codice dalla sorgente.
