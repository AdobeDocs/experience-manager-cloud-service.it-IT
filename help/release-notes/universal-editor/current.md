---
title: Note sulla versione 2025.03.10 dell’editor universale
description: Queste sono le note sulla versione 2025.03.10 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 23%

---


# Note sulla versione 2025.03.10 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 10 marzo 2025 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Spostamento di componenti:** [Lo spostamento di componenti tra contenitori](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) ora osserva il filtro dei componenti del contenitore di destinazione.
   * Non è più necessario disporre della stessa [definizione filtro](/help/implementing/universal-editor/filtering.md) sia per i contenitori di destinazione che per quelli di destinazione per spostare il componente tra i contenitori.
* **Pagine bloccate:** il servizio Universal Editor osserva lo stato di [blocco di una pagina](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) e scrive solo nelle pagine non bloccate o bloccate dall&#39;utente.

## Altri miglioramenti {#other-improvements}

* Sono state apportate correzioni per correggere la convalida per l’area di lavoro headless.

## Obsolescenza {#deprecation}

* La libreria `universal-editor-cors` fornita tramite npm o `https://unviersal-editor-service.experiencecloud.live/corslib/*` non deve più essere utilizzata.
   * Utilizzare un tag script che punta a `https://universal-editor-service.adobe.io/cors.js`.
   * Per informazioni dettagliate su come dotare la pagina di uno strumento appropriato per l&#39;utilizzo con l&#39;editor universale, vedere la [Panoramica dell&#39;editor universale per sviluppatori di AEM](/help/implementing/universal-editor/developer-overview.md).
   * Se si utilizza il metodo sbagliato, gli utenti visualizzeranno un messaggio di obsolescenza una volta al giorno.
