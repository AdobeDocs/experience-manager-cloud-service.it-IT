---
title: Flusso di attività nella timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse sulla timeline.
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
hide: true
hidefromtoc: true
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 35%

---

# Visualizzare i registri di operazione delle risorse nel flusso di attività {#activity-stream-in-timeline}

Questa funzione visualizza i registri attività per le risorse sulla timeline. Se esegui una delle seguenti operazioni relative alle risorse in [!DNL Experience Manager Assets], la funzione di flusso Attività aggiorna la timeline in modo che rifletta l’attività.

Nel flusso di attività vengono registrate le seguenti operazioni:

* Creare
* Elimina
* Download (incluse le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Spostare

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro.  Inoltre, l’attività timeline viene registrata al caricamento di nuove risorse o quando le risorse esistenti vengono modificate e archiviate [!DNL Experience Manager] tramite [Adobe collegamento risorsa](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) o [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline perché per tali flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, esegui una o più operazioni sulla risorsa, selezionala e scegli **[!UICONTROL Timeline]** dall&#39;elenco GlobalNav.

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
