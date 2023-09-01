---
title: Analisi dei frammenti di contenuto
description: Comprendere la struttura e la distribuzione dei contenuti dei frammenti di contenuto. Questo fornisce informazioni sia sulla distribuzione headless che sull’authoring delle pagine.
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# Analisi della struttura dei frammenti di contenuto {#analyzing-content-fragments-structure}

I frammenti di contenuto sono progettati per [Distribuzione headless tramite GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Ciò significa che possono avere una struttura a più livelli.

L’Experience Manager (AEM) fornisce diversi metodi per visualizzare e analizzare la struttura dei frammenti.

## Riferimenti {#references}

La struttura viene creata utilizzando Riferimenti:

* [I tipi di dati per i riferimenti sono definiti nel modello per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Durante l’authoring è possibile:
   * [Gestisci questi riferimenti](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Trovare i riferimenti principali del frammento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Struttura ad albero {#structure-tree}

Apri **Struttura ad albero** dalla barra degli strumenti dell’editor per visualizzare la struttura gerarchica del frammento di contenuto e i relativi riferimenti. Utilizza l’icona del collegamento per aprire i riferimenti.

Ad esempio:

![Editor frammento di contenuto - Struttura](assets/cf-authoring-structure-tree.png)