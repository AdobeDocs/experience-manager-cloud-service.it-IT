---
title: Note sulla versione 2025.02.17 dell’editor universale
description: Queste sono le note sulla versione 2025.02.17 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: af04ad7e3f89247580c48c276cb371d78ac56a49
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 22%

---


# Note sulla versione 2025.02.17 dell’editor universale {#release-notes}

Queste sono le note sulla versione di Universal Editor del 17 febbraio 2025.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Pubblica in anteprima** - Quando pubblichi (o annulli la pubblicazione) il contenuto tramite l&#39;editor universale, ora puoi scegliere se pubblicare nell&#39;ambiente di anteprima in aggiunta all&#39;ambiente di pubblicazione
   * Questo consente di rivedere il contenuto prima della pubblicazione pubblica.
* **Il modello e il filtro possono essere definiti nella definizione del componente**. È ora possibile definire il modello e il filtro utilizzati da un componente nella definizione del componente.
   * Queste informazioni possono essere conservate centralmente nella definizione e non è necessario specificare la strumentazione.
   * Questo consente di spostare i componenti tra contenitori diversi.
* **Gli elementi secondari dei contenitori vengono considerati in modo implicito componenti**. Se un elemento con un `data-aue-resource` viene inserito come elemento secondario diretto in un contenitore, viene considerato un componente e può essere spostato senza dover specificare `data-aue-behavior="component"`.

## Altri miglioramenti {#other-improvements}

* **Selettore risorse AEM 6.5** - Il selettore risorse 6.5 ora si apre correttamente quando si esegue l&#39;editor universale con AEM 6.5.

