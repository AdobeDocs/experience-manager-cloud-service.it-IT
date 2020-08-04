---
title: Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse)
description: 'Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# Strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) {#asset-workflow-migration}

Lo strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) è utilizzato per migrare automaticamente i flussi di lavoro per l’elaborazione delle risorse dalle implementazioni AEM on-premise o AMS ai profili di elaborazione e alle configurazioni OSGi da utilizzare in AEM Assets as a Cloud Service.

## Introduzione {#introduction}

Questa sezione descrive le risorse e i dettagli di implementazione dello strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse).

Questa utility consente agli sviluppatori AEM di migrare ad AEM as a Cloud Service i flussi di lavoro AEM esistenti per l’elaborazione delle risorse.

## Flussi di lavoro supportati {#migration-support-for-workflows}

I flussi di lavoro hanno un livello di supporto per la migrazione variabile. Consultate questo [elenco di flussi di lavoro](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)specifici. I flussi di lavoro sono organizzati per categorie nelle seguenti categorie in base al supporto fornito.  Adobe supporta la migrazione dei flussi di lavoro elencati in `SUPPORTED`, `REQUIRED`o `OPTIONAL` categorie. I passaggi del flusso di lavoro indicati nelle altre categorie non sono supportati.

* `SUPPORTED`: Funzionalità supportata in [!DNL Experience Manager Assets] come Cloud Service.
* `OPTIONAL`: Funzionalità opzionale in [!DNL Experience Manager Assets] come Cloud Service.
* `REQUIRED`: Un passaggio obbligatorio che viene aggiunto al flusso di lavoro.
* `UNNECESSARY`: La funzionalità non è necessaria in [!DNL Experience Manager Assets] quanto Cloud Service.
* `NUI_OOTB`: Funzionalità fornita da [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funzionalità fornita dai [!DNL Dynamic Media] connettori predefiniti.
* `NUI_MIGRATED`: Migrazione a un profilo di [elaborazione per il servizio](/help/assets/asset-microservices-configure-and-use.md)di elaborazione risorse.
* `UNSUPPORTED`: Attualmente non supportato in [!DNL Experience Manager Assets] come Cloud Service.

## Installazione dello strumento Asset Workflow Migration (Migrazione flussi di lavoro per risorse) {#installing-tool}

Consulta **[Git Resource: AEM Assets as a Cloud Service - Workflow Migration](https://github.com/adobe/aem-cloud-migration)**per informazioni sull’installazione e la compilazione del codice dalla sorgente.
