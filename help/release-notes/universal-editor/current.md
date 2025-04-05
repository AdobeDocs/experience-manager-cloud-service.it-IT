---
title: Note sulla versione 2025.03.10 dell’editor universale
description: Queste sono le note sulla versione 2025.03.10 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: beab4f94dc6d78c2b1ad87a02b9fe46dd0438bcc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 68%

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

## Nuove estensioni per l’editor universale {#extensions}

Sono state rilasciate diverse nuove estensioni su [Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/) per l&#39;editor universale, che migliorano l&#39;esperienza di authoring.

* **Estensione MSM**: è ora possibile interrompere e creare nuovamente un&#39;istanza dell&#39;ereditarietà di componenti/blocchi utilizzando questa estensione.
* **Estensione proprietà pagina**: consente di accedere alla finestra delle proprietà della pagina direttamente da Universal Editor tramite questa estensione.
* **Estensione flusso di lavoro**: utilizza i flussi di lavoro nelle pagine e nei frammenti di contenuto instrumentati nella pagina utilizzando questa estensione.
* **Estensione blocco pagina**: utilizzare questa estensione per bloccare e sbloccare una pagina direttamente dall&#39;editor universale.

## Altri miglioramenti {#other-improvements}

* Sono state apportate correzioni relative alla convalida per l’area di lavoro headless.

## Obsolescenza {#deprecation}

* La libreria dell’`universal-editor-cors` fornita tramite npm o `https://unviersal-editor-service.experiencecloud.live/corslib/*` non deve più essere utilizzata.
   * Utilizzare invece un tag script che punta a `https://universal-editor-service.adobe.io/cors.js`.
   * Per dettagli su come preparare correttamente la pagina per l’utilizzo con l’editor universale, consulta [Panoramica dell’editor universale per sviluppatori AEM](/help/implementing/universal-editor/developer-overview.md).
   * Utilizzando un metodo errato, gli utenti visualizzeranno un messaggio di obsolescenza una volta al giorno.
