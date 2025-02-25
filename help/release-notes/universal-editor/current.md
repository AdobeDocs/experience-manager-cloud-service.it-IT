---
title: Note sulla versione 2025.02.17 dell’editor universale
description: Queste sono le note sulla versione 2025.02.17 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c88aa13c6bc75c8f9cd624d00ef768290981c840
workflow-type: ht
source-wordcount: '206'
ht-degree: 100%

---


# Note sulla versione 2025.02.17 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 17 febbraio 2025 dell’editor universale.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Pubblica in anteprima** - [Quando pubblichi contenuti (o ne annulli la pubblicazione)](/help/sites-cloud/authoring/universal-editor/publishing.md) tramite l’editor universale, ora puoi scegliere se pubblicare non solo nell’ambiente di pubblicazione, ma anche nell’[ambiente di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md)
   * In questo modo potrai rivedere i contenuti prima di renderli pubblici.
* **Il modello e il filtro possono essere specificati nella definizione del componente** - È ora possibile specificare il modello e il filtro utilizzati da un componente [nella definizione del componente.](/help/implementing/universal-editor/component-definition.md#template)
   * Queste informazioni possono essere mantenute centralmente nella definizione e non sarà necessario specificarle nella strumentazione.
   * In questo modo, inoltre, sarà possibile spostare i componenti tra contenitori diversi.
* **Gli elementi secondari dei contenitori vengono implicitamente considerati componenti**. Se [un elemento con `data-aue-resource`](/help/implementing/universal-editor/attributes-types.md#data-properties) viene inserito come elemento secondario diretto in un contenitore, verrà considerato come un componente e potrà essere spostato senza dover specificare `data-aue-behavior="component"`.

## Altri miglioramenti {#other-improvements}

* **Selettore risorse di AEM 6.5** - Il selettore risorse 6.5 si apre ora correttamente quando [si esegue l’editor universale con AEM 6.5.](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
