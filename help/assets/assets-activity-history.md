---
title: Flusso di attività nella timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse sulla timeline.
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
hide: true
hidefromtoc: true
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 35%

---

# Visualizzare i registri di operazione delle risorse nel flusso di attività {#activity-stream-in-timeline}

Questa funzione visualizza i registri attività per le risorse sulla timeline. Se in [!DNL Experience Manager Assets] si esegue una delle seguenti operazioni relative alle risorse, la funzione Flusso di attività aggiorna la timeline in modo che rifletta l&#39;attività.

Nel flusso di attività vengono registrate le seguenti operazioni:

* Creare
* Eliminare
* Download (incluse le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approvazione
* Rifiuta
* Spostare

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro.  Inoltre, l&#39;attività timeline viene registrata al caricamento di nuove risorse o quando le risorse esistenti vengono modificate e archiviate in [!DNL Experience Manager] tramite [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) o [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=it).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline perché per tali flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, esegui una o più operazioni sulla risorsa, seleziona la risorsa, quindi scegli **[!UICONTROL Timeline]** dall&#39;elenco GlobalNav.

<!-- ![timeline-2](assets/timeline-2.png) -->

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>La posizione predefinita dell’archivio del registro per le attività di tipo **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività di tipo **[!UICONTROL Sposta]**, la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
