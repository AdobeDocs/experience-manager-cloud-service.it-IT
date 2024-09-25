---
title: Blocchi per l’authoring basato su documenti e WYSIWYG
description: Scopri come creare blocchi che possono essere utilizzati sia per l’authoring WYSIWYG che per l’authoring basato su documenti.
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Blocchi per l’authoring basato su documenti e WYSIWYG {#wysiwyg-and-doc-blocks}

Scopri come creare blocchi che possono essere utilizzati sia per l’authoring WYSIWYG che per l’authoring basato su documenti.

## Panoramica {#overview}

In alcuni progetti, è possibile supportare sia l&#39;authoring di [WYSIWYG tramite Universal Editor](/help/edge/wysiwyg-authoring/authoring.md) che l&#39;authoring di [documenti.](/help/edge/docs/authoring.md) Per ridurre al minimo il tempo di sviluppo e garantire la stessa esperienza del sito, puoi creare un set di blocchi per supportare entrambi i casi d&#39;uso.

A tal fine, è necessario utilizzare lo stesso approccio di modellazione dei contenuti sia per la configurazione di authoring di WYSIWYG che per quella basata sui documenti.

## Approccio {#approach}

Nella creazione di WYSIWYG nell&#39;AEM, [dichiari un modello](/help/edge/wysiwyg-authoring/content-modeling.md) e fornisci le convenzioni di denominazione. I dati vengono quindi sottoposti a rendering in strutture di blocchi simili a tabelle utilizzando Edge Delivery come se la tabella fosse stata creata manualmente utilizzando l’authoring basato su documenti.

A tal fine, vengono fatte alcune ipotesi, ad esempio per un blocco semplice come un teaser, secondo cui tutte le proprietà e i gruppi di proprietà vengono renderizzati in 1.n righe con una singola colonna ciascuna. Per i blocchi che hanno 1..In elementi (come carosello e schede) gli elementi vengono aggiunti dopo queste righe con una riga ciascuna e una colonna per ogni proprietà/gruppo di proprietà.

Se utilizzi lo stesso approccio per l’authoring basato su documenti, puoi riutilizzare i blocchi di WYSIWYG.
