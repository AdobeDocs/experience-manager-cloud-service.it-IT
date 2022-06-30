---
title: Problemi noti
description: Problemi noti con Adobe Experience Manager as a Cloud Service
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 66%

---

# Problemi noti {#known-issues}

In questo articolo sono elencati i problemi noti relativi all’offerta [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. L’elenco viene rivisto e aggiornato a ogni versione di [!DNL Experience Manager].

Per ulteriori informazioni sui problemi noti, [contatta il supporto](https://experienceleague.adobe.com/?lang=it&amp;support-solution=Experience+Manager#support).

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

Alcuni problemi noti in [!DNL Sites] includono:

* Nell’IDE GraphQL è possibile: [gestire la cache per le query persistenti](/help/headless/graphql-api/graphiql-ide.md##managing-cache).
   * Al primo salvataggio i valori salvati per le intestazioni sono impostati su `0` (anziché i valori predefiniti) - se l’utente non ha modificato tali valori nella finestra di dialogo.
   * Nei successivi salvataggi, i valori vengono salvati correttamente.
   * Pertanto, l&#39;utente deve salvare le intestazioni due volte.

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alcuni problemi noti in [!DNL Assets] includono:

* **Download**: se si scarica una cartella vuota, [!DNL Experience Manager] trasmette un messaggio di operazione riuscita della creazione di un archivio ZIP, ma l’archivio non viene creato.

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
>* [Modifiche principali [!DNL Experience Manager]](aem-cloud-changes.md)
>* [Funzioni obsolete e rimosse](deprecated-removed-features.md)
>* [Note sulla versione](home.md)

