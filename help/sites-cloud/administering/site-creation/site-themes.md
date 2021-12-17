---
title: Temi del sito
description: Scopri come utilizzare AEM temi del sito per personalizzare lo stile e la progettazione del sito.
feature: Administering
role: Admin
source-git-commit: 0b00d579886a106f5f66cfc54d90eab9563724cd
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---


# Temi del sito {#site-themes}

Scopri come utilizzare AEM temi del sito per personalizzare lo stile e la progettazione del sito.

## Panoramica {#overview}

Un tema del sito AEM è un pacchetto contenente le risorse CSS, JavaScript e statiche che definiscono lo stile del sito AEM e rispetta la struttura di un tema del sito AEM.

I siti creati con modelli di sito AEM consentono di scaricare, personalizzare e ridistribuire facilmente i temi.

>[!NOTE]
>
>AEM temi del sito non devono essere confusi con [AEM modelli di sito.](site-templates.md) AEM temi del sito contengono solo le informazioni sullo stile di un sito AEM. AEM modelli di sito definiscono la struttura del sito e il contenuto iniziale, nonché contengono un tema del sito AEM per consentire [creazione rapida del sito.](create-site.md)

## Utilizzo dei temi del sito {#using-themes}

I temi del sito vengono utilizzati in due modi diversi:

* Vengono utilizzati come parte di un modello di sito per definire lo stile quando [creazione di un sito.](create-site.md)
* Vengono scaricati dopo la creazione di un sito basato su un modello di sito in modo che uno sviluppatore front-end possa personalizzare ulteriormente lo stile.

>[!TIP]
>
>Una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema si trova nella [Percorso di creazione rapida del sito.](/help/journey-sites/quick-site/overview.md)

## Struttura del tema del sito {#structure}

I temi del sito sono semplicemente pacchetti con una struttura logica che riflette chiaramente lo scopo del contenuto del pacchetto. Un tema del sito ha la seguente struttura tipica di un progetto front-end.

* `src/main.ts`: Il punto di ingresso principale del tema JS e CSS
* `src/site`: File JS e CSS applicabili all’intero sito
* `src/components`: File JS e CSS specifici per i componenti AEM
* `src/resources`: File statici come icone, loghi e font

## Tema sito standard {#standard-site-theme}

Adobe fornisce un tema di riferimento sulle best practice da utilizzare come base per la creazione di un tema personalizzato. [Il tema del sito standard è disponibile su GitHub.](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## Sviluppo di temi del sito {#developing-themes}

Adobe fornisce un Generatore di temi AEM sito come set di script per la creazione di nuovi temi del sito.

[È disponibile AEM Site Theme Builder e la relativa documentazione di utilizzo su GitHub.](https://github.com/adobe/aem-site-theme-builder) Per personalizzare il tema è necessaria un’esperienza di sviluppo front-end.
