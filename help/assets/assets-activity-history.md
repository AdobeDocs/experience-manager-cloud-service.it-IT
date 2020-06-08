---
title: Flusso di attività nella timeline
description: Questo articolo descrive come visualizzare i registri attività per le risorse nella timeline.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 40%

---


# Visualizzare i registri delle operazioni della risorsa nel flusso di attività {#activity-stream-in-timeline}

Questa funzione consente di visualizzare i registri attività per le risorse nella timeline. Se esegui una delle seguenti operazioni relative alle risorse in Risorse Adobe Experience Manager (AEM), la funzione Flusso di attività aggiorna la timeline per riflettere l’attività.

Le seguenti operazioni vengono registrate nel flusso di attività:

* Crea
* Elimina
* Download (comprese le rappresentazioni)
* Pubblicazione
* Annulla pubblicazione
* Approva
* Rifiuta
* Sposta

I registri attività da visualizzare nella timeline vengono recuperati dalla posizione `/var/audit/com.day.cq.dam/content/dam` di CRX, dove vengono memorizzati i file di registro.  Inoltre, l’attività timeline viene registrata al caricamento di nuove risorse o quando le risorse esistenti vengono modificate e archiviate in AEM tramite [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) o l’[app desktop AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>I flussi di lavoro transitori non vengono visualizzati nella timeline, perché per questi flussi di lavoro non vengono salvate informazioni sulla cronologia.

Per visualizzare il flusso di attività, eseguite una o più operazioni sulla risorsa, selezionate la risorsa, quindi scegliete **[!UICONTROL Timeline]** dall&#39;elenco Navigazione globale.

<!-- ![timeline-2](assets/timeline-2.png) -->

La timeline mostra il flusso di attività per le operazioni eseguite sulle risorse.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>La posizione predefinita dell’archivio del registro per le attività di tipo **[!UICONTROL Pubblica]** e **[!UICONTROL Annulla pubblicazione]** è `/var/audit/com.day.cq.replication/content`. Per le attività di tipo **[!UICONTROL Sposta]**, la posizione predefinita è `/var/audit/com.day.cq.wcm.core.page`.
