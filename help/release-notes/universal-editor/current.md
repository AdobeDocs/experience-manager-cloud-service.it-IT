---
title: Note sulla versione 2025.03.10 dell’editor universale
description: Queste sono le note sulla versione 2025.03.10 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: ht
source-wordcount: '200'
ht-degree: 100%

---


# Note sulla versione 2025.03.10 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 10 marzo 2025 dell’editor universale.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Spostamento di componenti:** [lo spostamento di componenti tra contenitori](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) ora considera il filtro del componente del contenitore target.
   * Non è più necessario disporre della stessa [definizione di filtro](/help/implementing/universal-editor/filtering.md) sia per i contenitori target che per quelli di destinazione per spostare il componente tra i contenitori.
* **Pagine bloccate:** il servizio editor universale considera lo [stato di blocco di una pagina](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) e scrive solo su pagine non bloccate o bloccate dall’utente.

## Altri miglioramenti {#other-improvements}

* Sono state apportate correzioni relative alla convalida per l’area di lavoro headless.

## Obsolescenza {#deprecation}

* La libreria dell’`universal-editor-cors` fornita tramite npm o `https://unviersal-editor-service.experiencecloud.live/corslib/*` non deve più essere utilizzata.
   * Utilizzare invece un tag script che punta a `https://universal-editor-service.adobe.io/cors.js`.
   * Per dettagli su come preparare correttamente la pagina per l’utilizzo con l’editor universale, consulta [Panoramica dell’editor universale per sviluppatori AEM](/help/implementing/universal-editor/developer-overview.md).
   * Utilizzando un metodo errato, gli utenti visualizzeranno un messaggio di obsolescenza una volta al giorno.
