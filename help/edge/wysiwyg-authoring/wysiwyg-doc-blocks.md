---
title: Blocchi per l’authoring WYSIWYG e basato su documenti
description: Scopri come creare blocchi che possono essere utilizzati sia per l’authoring WYSIWYG che per l’authoring basato su documenti.
feature: Edge Delivery Services
role: User
source-git-commit: 3419fa943eb865d87467443527ea97fcd64909c2
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---


# Blocchi per l’authoring WYSIWYG e basato su documenti {#wysiwyg-and-doc-blocks}

Scopri come creare blocchi che possono essere utilizzati sia per l’authoring WYSIWYG che per l’authoring basato su documenti.

## Panoramica {#overview}

In alcuni progetti, potresti voler supportare sia l’authoring [WYSIWYG tramite l’editor universale](/help/edge/wysiwyg-authoring/authoring.md) che l’[authoring basato su documenti.](/help/edge/docs/authoring.md) Per ridurre al minimo il tempo di sviluppo e garantire la stessa esperienza del sito, puoi creare un set di blocchi per supportare entrambi i casi d’uso.

A tal fine, devi utilizzare lo stesso approccio di modellazione dei contenuti sia per la configurazione di authoring di WYSIWYG che per quello basata sui documenti.

## Approccio {#approach}

Nell’authoring di WYSIWYG in AEM, [dichiari un modello](/help/edge/wysiwyg-authoring/content-modeling.md) e fornisci le convenzioni di denominazione. I dati vengono quindi sottoposti a rendering in strutture di blocchi simili a tabelle utilizzando Edge Delivery come se la tabella fosse stata creata manualmente utilizzando l’authoring basato su documenti.

A tal fine, vengono fatte alcune ipotesi, ad esempio per un blocco semplice come un teaser, secondo cui tutte le proprietà e i gruppi di proprietà vengono sottoposti a rendering in 1.n righe con una singola colonna ciascuna. Per i blocchi che ne hanno 1.elemento (come carosello e schede), gli elementi vengono aggiunti dopo queste righe con una riga ciascuna e una colonna per ogni proprietà/gruppo di proprietà.

Se utilizzi lo stesso approccio per l’authoring basato su documenti, puoi riutilizzare i blocchi di WYSIWYG.
