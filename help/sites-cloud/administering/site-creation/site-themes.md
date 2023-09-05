---
title: Temi del sito
description: Scopri come utilizzare i temi del sito AEM per personalizzare lo stile e la progettazione del sito.
feature: Administering
role: Admin
exl-id: 53d4afb3-d091-47a1-ba12-5bcec99f46b9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '353'
ht-degree: 100%

---

# Temi del sito {#site-themes}

Scopri come utilizzare i temi del sito AEM per personalizzare lo stile e la progettazione del sito.

## Panoramica {#overview}

Un tema del sito AEM è un pacchetto contenente le risorse CSS, JavaScript e statiche che definiscono lo stile del sito AEM e ne rispettano la struttura.

I siti creati con modelli AEM consentono di scaricare, personalizzare e applicare facilmente i temi.

>[!NOTE]
>
>I temi del sito AEM non devono essere confusi con i [modelli del sito AEM](site-templates.md). I temi del sito AEM contengono solo le informazioni sullo stile di un sito AEM. I modelli di sito AEM definiscono la struttura del sito e il contenuto iniziale e inoltre contengono un tema del sito AEM per consentire una [creazione rapida del sito](create-site.md).

## Utilizzo dei temi del sito {#using-themes}

I temi del sito vengono utilizzati in due modi diversi:

* Vengono utilizzati come parte di un modello del sito per definire lo stile durante la [creazione di un sito.](create-site.md)
* Vengono scaricati dopo la creazione di un sito basato su un modello in modo che uno sviluppatore front-end possa personalizzare ulteriormente lo stile.

>[!TIP]
>
>Per una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema, consulta [Percorso di creazione rapida dei siti](/help/journey-sites/quick-site/overview.md).

## Struttura del tema del sito {#structure}

I temi del sito sono semplicemente pacchetti con una struttura logica che riflette chiaramente lo scopo del contenuto. Un tema del sito ha la seguente struttura, tipica di un progetto front-end.

* `src/main.ts`: il punto di ingresso principale del tema JS &amp; CSS
* `src/site`: file JS &amp; CSS applicabili all’intero sito
* `src/components`: file JS &amp; CSS specifici per i componenti AEM
* `src/resources`: file statici come icone, loghi e font

## Tema del sito standard {#standard-site-theme}

Adobe fornisce un tema corredato delle best practice da utilizzare come base per la creazione di un tema personalizzato. [Il tema del sito standard è disponibile su GitHub](https://github.com/adobe/aem-site-template-standard/tree/main/theme).

## Sviluppo di temi del sito {#developing-themes}

Adobe fornisce un generatore di temi del sito AEM come set di script per la creazione di nuovi temi.

[Il generatore di temi del sito AEM è disponibile su GitHub insieme alla relativa documentazione di utilizzo](https://github.com/adobe/aem-site-theme-builder). Per personalizzare il tema è necessaria un’esperienza di sviluppo front-end.
