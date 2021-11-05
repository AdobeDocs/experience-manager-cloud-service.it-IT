---
title: Temi del sito
description: Scopri come utilizzare AEM temi del sito per personalizzare lo stile e la progettazione del sito.
feature: Administering
role: Admin
source-git-commit: 9e7ad4a640f1783be5aed75e01e860b647662f52
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---


# Temi del sito {#site-themes}

Learn how AEM site themes can be used to customize the style and design of your site.

>[!CAUTION]
>
>Lo strumento di creazione rapida del sito è attualmente un&#39;anteprima tecnica. It is made available for testing and evaluation purposes and is not intended for production use unless agreed with Adobe Support.

## Panoramica {#overview}

Un tema del sito AEM è un pacchetto contenente le risorse CSS, JavaScript e statiche che definiscono lo stile del sito AEM e rispetta la struttura di un tema del sito AEM.

Sites created with AEM site templates allow for the easy download, customization, and redeployment of the themes.

>[!NOTE]
>
>AEM temi del sito non devono essere confusi con [AEM modelli di sito.](site-templates.md) AEM temi del sito contengono solo le informazioni sullo stile di un sito AEM. AEM modelli di sito definiscono la struttura del sito e il contenuto iniziale, nonché contengono un tema del sito AEM per consentire [creazione rapida del sito.](create-site.md)

## Utilizzo dei temi del sito {#using-themes}

I temi del sito vengono utilizzati in due modi diversi:

* Vengono utilizzati come parte di un modello di sito per definire lo stile quando [creazione di un sito.](create-site.md)
* They are downloaded after creating a site based on a site template so a front-end developer can further customize the styling.

>[!TIP]
>
>Una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema si trova nella [Percorso di creazione rapida del sito.](/help/journey-sites/quick-site/overview.md)

## Site Theme Structure {#structure}

Site themes are simply packages with a logical structure that clearly reflects the purpose of the package content. Un tema del sito ha la seguente struttura tipica di un progetto front-end.

* `src/main.ts`: Il punto di ingresso principale del tema JS e CSS
* `src/site`: JS &amp; CSS files that apply to the entire site
* `src/components`: File JS e CSS specifici per i componenti AEM
* `src/resources`: File statici come icone, loghi e font

## Tema sito standard {#standard-site-theme}

Adobe fornisce un tema di riferimento sulle best practice da utilizzare come base per la creazione di un tema personalizzato. [Il tema del sito standard è disponibile su GitHub.](https://github.com/adobe/aem-site-template-standard-theme-e2e)

## Sviluppo di temi del sito {#developing-themes}

Adobe fornisce e AEM Site Theme Builder come set di script per la creazione di nuovi temi del sito.

[The AEM Site Theme Builder is available along with usage documentation on GitHub.](https://github.com/adobe/aem-site-theme-builder) Front-end development experience is required for customizing the theme.
