---
title: Analisi dei frammenti di contenuto
description: Comprendere la struttura dei frammenti di contenuto. Questo fornisce informazioni rilevanti sia per la distribuzione headless che per l’authoring delle pagine.
feature: Content Fragments
role: User, Developer
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---

# Analisi della struttura dei frammenti di contenuto {#analyzing-content-fragments-structure}

I frammenti di contenuto sono progettati per la [distribuzione headless tramite GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Ciò significa che possono avere una struttura a più livelli.

Experience Manager (AEM) fornisce diversi metodi per visualizzare e analizzare la struttura dei frammenti.

## Riferimenti {#references}

La struttura a più livelli viene creata utilizzando Riferimenti:

* [I tipi di dati per i riferimenti sono definiti nel modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Durante l’authoring è possibile:
   * [Gestisci questi riferimenti](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Trovare i riferimenti principali del frammento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Albero struttura {#structure-tree}

Apri la scheda **Struttura** dalla barra degli strumenti dell&#39;editor per visualizzare la struttura gerarchica del frammento di contenuto e i relativi riferimenti. Utilizza l’icona del collegamento per aprire i riferimenti.

Ad esempio:

![Editor frammento di contenuto - Struttura](assets/cf-authoring-structure-tree.png)
