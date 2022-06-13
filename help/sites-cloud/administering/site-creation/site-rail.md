---
title: Utilizzo della barra del sito per gestire il tema del sito
description: Scopri le potenti funzioni della barra del sito per personalizzare e gestire facilmente il tema del sito.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
source-git-commit: 3e4c6fce54fe336c145d533c05e68e3a1f64c144
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Utilizzo della barra del sito per gestire il tema del sito {#site-rail}

Scopri le potenti funzioni della barra del sito per personalizzare e gestire facilmente il tema del sito.

## Panoramica {#overview}

La barra Sito consente di gestire le risorse del tema e del modello del sito. [Come altri binari](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) ad esempio Struttura contenuto, Riferimenti o barre laterali Timeline, la barra Sito viene visualizzata come pannello più a sinistra nella console Sites e contiene informazioni sull’elemento selezionato. A differenza di altre barre verticali, la barra Sito si applica solo alle directory principali del sito.

La barra Sito consente di gestire le informazioni relative a temi e modelli per il sito, tra cui:

* [Download di origini tema](#downloading-theme-sources)
* [Download di risorse modello come wireframe](#downloading-template-resources)
* [Visualizzazione e modifica delle versioni dei temi](#theme-vrsions)
* [Abilitazione della pipeline front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Consulta la sezione [Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per acquisire familiarità con lo strumento Creazione rapida sito e la pipeline front-end per personalizzare facilmente il tema del sito.

## Download di origini tema {#downloading-theme-sources}

Quando crei un sito in AEM basato su un [modello di sito,](site-templates.md) è possibile scaricare [tema del sito](site-themes.md) mediante la barra Sito.

Con la barra Sito visualizzata nella console Sites, seleziona la directory principale del sito per visualizzare informazioni sul tema del sito.

![Scaricare origini tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Tocca o fai clic su **Scaricare le origini dei temi** per scaricare una copia locale del tema del sito come `.zip` file a scopo di personalizzazione.

## Download delle risorse dei modelli {#downloading-template-resources}

[Modelli di sito](site-templates.md) può contenere informazioni oltre alla struttura del contenuto del sito e [tema del sito.](site-themes.md) Ad esempio, i modelli di sito possono contenere progetti wireframe o altri file relativi al sito.

Se il sito è basato su un modello di sito, con la barra Sito visualizzata nella console Sites , seleziona la directory principale del sito per visualizzare informazioni sul tema del sito, incluse ulteriori risorse sul sito.

![Scaricare origini tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Tocca o fai clic sul pulsante o sui pulsanti sotto l’intestazione **Scaricare risorse aggiuntive sui modelli** per scaricare una copia locale dei file disponibili.

## Visualizzazione e modifica delle versioni dei temi {#them-versions}

Se il sito è basato su un modello di sito, è possibile che il relativo tema sia già stato personalizzato dallo sviluppatore front-end. Utilizzando la barra Sito, puoi visualizzare quale versione del tema del sito è attualmente distribuita e passare alle versioni precedenti.

Con la barra Sito visualizzata nella console Sites, seleziona la directory principale del sito per visualizzare informazioni sul tema del sito.

![Versioni del sito nella barra](/help/sites-cloud/administering/assets/theme-versions.png)

La versione corrente del tema viene visualizzata con il relativo hash di commit e la marca temporale dell’ultimo aggiornamento.

Tocca o fai clic su **Seleziona versione** per visualizzare le versioni precedenti del tema.

![Seleziona versione tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Tocca o fai clic sulla versione in cui desideri modificare, quindi tocca o fai clic su **Applica** per apportare il cambiamento.

Se AEM rileva che una versione più recente del tema è stata distribuita tramite la pipeline front-end ma non applicata al sito, viene visualizzata un’icona di notifica.

![Nuova versione dell&#39;indicatore del tema](/help/sites-cloud/administering/assets/new-theme-version.png)

È possibile utilizzare **Seleziona versione** per aggiornare alla nuova versione del tema.

## Abilitazione della pipeline front-end {#enabling-front-end-pipeline}

Se il sito non è stato creato utilizzando un modello di sito, non è possibile utilizzare la pipeline front-end per personalizzare e distribuire il tema.

Tuttavia puoi abilitare la pipeline front-end per il sito utilizzando la barra Sito .

Con la barra Sito visualizzata nella console Sites, seleziona la directory principale del sito per visualizzare informazioni sul tema del sito, quindi tocca o fai clic su **Abilita pipeline front-end**.

![Abilitazione della pipeline front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Per ulteriori informazioni, consulta il documento [Abilitazione della pipeline front-end.](enable-front-end-pipeline.md)
