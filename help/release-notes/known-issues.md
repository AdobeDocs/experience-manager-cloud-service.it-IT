---
title: Problemi noti
description: Problemi noti con Adobe Experience Manager as a Cloud Service
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 8ec0ce3425e7cade0a6774a4452d4f47ab971375
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 43%

---

# Problemi noti {#known-issues}

Questo articolo elenca i problemi noti di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] offerta. L’elenco viene rivisto e aggiornato a ogni versione di [!DNL Experience Manager].

Per ulteriori informazioni sui problemi noti, [contatta il supporto](https://experienceleague.adobe.com/?lang=en&amp;support-solution=Experience+Manager#support).

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alcuni problemi noti in [!DNL Assets] sono:

* **Scarica**: Se si scarica una cartella vuota, [!DNL Experience Manager] trasmette un messaggio di successo sulla creazione di un archivio ZIP, ma l’archivio non viene creato.

* **Schema metadati**: il widget di valutazione delle risorse causava un errore di compilazione JSP. È stato rimosso dallo schema metadati. <!-- CQ-4282865, CQ-4284633 -->

Vedi anche [modifiche rilevanti [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md).

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [Modifiche principali apportate a [!DNL Experience Manager]](aem-cloud-changes.md)
>* [Funzioni obsolete e rimosse](deprecated-removed-features.md)
>* [Note sulla versione](home.md)

