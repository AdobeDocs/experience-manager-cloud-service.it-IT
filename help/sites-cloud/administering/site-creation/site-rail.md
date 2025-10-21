---
title: Utilizzo del pannello Sito per gestire il tema del sito
description: Scopri le potenti funzioni del pannello Sito per personalizzare e gestire facilmente il tema del sito per i progetti di authoring tradizionali di AEM con distribuzione di pubblicazioni.
feature: Administering
role: Admin
exl-id: 45785e5a-4fa2-4cf2-a300-f1865f6f5807
solution: Experience Manager Sites
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 36%

---


# Utilizzo del pannello Sito per gestire il tema del sito {#site-panel}

{{traditional-aem}}

Scopri le potenti funzioni del pannello Sito per personalizzare e gestire facilmente il tema del sito per i progetti di authoring tradizionali di AEM con distribuzione di pubblicazioni.

## Panoramica {#overview}

Il pannello Sito consente di gestire le risorse del tema e del modello del sito per i progetti di authoring tradizionali di AEM con [distribuzione di pubblicazione.](/help/sites-cloud/authoring/author-publish.md) [Come altri pannelli](/help/sites-cloud/authoring/sites-console/console-side-panel.md) quali Struttura contenuto, Riferimenti o Timeline, il pannello Sito viene visualizzato come pannello più a sinistra nella console Sites e contiene informazioni sull&#39;elemento selezionato. A differenza di altri pannelli, il pannello Sito si applica solo alle directory principali del sito.

Il pannello Sito consente di gestire le informazioni relative a temi e modelli per il sito, tra cui:

* [Download di origini tema](#downloading-theme-sources)
* [Download di risorse modello come wireframe](#downloading-template-resources)
* [Visualizzazione e modifica delle versioni dei temi](#theme-vrsions)
* [Abilitazione della pipeline front-end](#enabling-the-front-end-pipeline)

>[!TIP]
>
>Consulta la sezione [Percorso di creazione rapida sito](/help/journey-sites/quick-site/overview.md) per acquisire familiarità con lo strumento Creazione rapida sito e la pipeline front-end per personalizzare facilmente il tema del sito.

## Download di origini tema {#downloading-theme-sources}

Quando crei un sito in AEM basato su un [modello di sito,](site-templates.md) puoi scaricare il [tema del sito](site-themes.md) utilizzando il pannello Sito.

Con il pannello Sito visualizzato nella console Sites, seleziona la pagina principale del sito per visualizzare informazioni sul tema.

![Scarica sorgenti del tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Selezionare **Scarica origini tema** per scaricare una copia locale del tema del sito come file `.zip` a scopo di personalizzazione.

## Scaricare le risorse dei modelli {#downloading-template-resources}

[Modelli di sito](site-templates.md) può contenere informazioni oltre alla struttura del contenuto del sito e al [tema del sito.](site-themes.md) Ad esempio, i modelli di sito possono contenere progetti wireframe o altri file relativi al sito.

Se il sito è basato su un modello, con il pannello Sito visualizzato nella console Sites, seleziona la pagina principale del sito per visualizzare informazioni sul tema, incluse ulteriori risorse.

![Scarica sorgenti del tema](/help/sites-cloud/administering/assets/download-theme-wireframe.png)

Selezionare il pulsante o i pulsanti sotto l&#39;intestazione **Scarica risorse aggiuntive** per scaricare una copia locale dei file disponibili.

## Visualizzazione e modifica delle versioni dei temi {#them-versions}

Se il sito è basato su un modello, è possibile che il relativo tema sia già stato personalizzato dallo sviluppatore front-end. Utilizzando il pannello Sito, potete visualizzare quale versione del tema del sito è attualmente distribuita e passare alle versioni precedenti.

Con il pannello Sito visualizzato nella console Sites, seleziona la pagina principale del sito per visualizzare informazioni sul tema.

![Versioni del sito nel pannello](/help/sites-cloud/administering/assets/theme-versions.png)

La versione corrente del tema viene visualizzata con il relativo hash di commit e la marca temporale dell’ultimo aggiornamento.

Seleziona **Seleziona versione** per visualizzare le versioni precedenti del tema.

![Seleziona versione tema](/help/sites-cloud/administering/assets/select-theme-versions.png)

Selezionare la versione che si desidera modificare, quindi selezionare **Applica** per apportare la modifica.

Se AEM rileva che una versione più recente del tema è stata distribuita tramite la pipeline front-end ma non applicata al sito, viene visualizzata un’icona di notifica.

![Nuova versione dell’indicatore del tema](/help/sites-cloud/administering/assets/new-theme-version.png)

È possibile utilizzare il pulsante **Seleziona versione** per aggiornare alla nuova versione del tema.

## Abilitazione della pipeline front-end {#enabling-front-end-pipeline}

Se il sito non è stato creato utilizzando un modello, non è possibile utilizzare la pipeline front-end per personalizzare e distribuire il tema.

Tuttavia, puoi abilitare la pipeline front-end per il sito utilizzando il pannello Sito.

Con il pannello Sito visualizzato nella console Sites, seleziona la pagina principale del sito per visualizzare informazioni sul tema, quindi seleziona **Abilita pipeline front-end**.

![Abilitazione pipeline front-end](/help/sites-cloud/administering/assets/enable-fep.png)

Per ulteriori informazioni, consulta il documento [Abilitazione pipeline front-end.](enable-front-end-pipeline.md)
