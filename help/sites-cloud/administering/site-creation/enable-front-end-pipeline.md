---
title: Abilitazione della pipeline front-end
description: Scopri come abilitare la pipeline front-end per i siti esistenti per sfruttare i temi del sito per personalizzare più rapidamente il sito.
feature: Administering
role: Admin
source-git-commit: 002b95212d682c41a601a483df9b4365a553b669
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# Abilitazione della pipeline front-end {#enable-front-end-pipeline}

Scopri come abilitare la pipeline front-end per i siti esistenti per sfruttare i temi del sito per personalizzare più rapidamente il sito.

## Panoramica {#overview}

La pipeline front-end è un meccanismo che può distribuire rapidamente solo il codice front-end dei siti web in base a [temi del sito](site-themes.md) e [modelli di sito.](site-templates.md)

Invece di distribuire l’intero stack, solo il codice front-end viene gestito da questa pipeline, rendendo il processo più veloce e consentendo agli sviluppatori front-end di personalizzare facilmente e rapidamente il sito senza conoscere AEM.

Per impostazione predefinita, i siti basati sui modelli di sito possono sfruttare la pipeline front-end. Questo documento descrive come adattare i siti esistenti per sfruttare la pipeline front-end.

>[!TIP]
>
>Se non conosci la pipeline front-end e le modalità di distribuzione rapida dei siti che la utilizzano e i modelli di sito, consulta la sezione [Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per un’introduzione.

Se non hai creato il sito esistente in base a modelli e temi del sito, AEM configurare il sito per caricare i temi distribuiti con la pipeline Front End sopra le librerie client esistenti.

## Dettagli tecnici {#technical-details}

Quando attivi la pipeline front-end per un sito, AEM apporta le seguenti modifiche alla struttura del sito.

* Tutte le pagine del sito includeranno un ulteriore file CSS e JS, che può essere modificato distribuendo aggiornamenti tramite una pipeline front-end di Cloud Manager dedicata.
* I file CSS e JS aggiunti saranno inizialmente vuoti, ma una cartella &quot;origini tema&quot; può essere scaricata per avviare la struttura delle cartelle che consente di distribuire gli aggiornamenti del codice CSS e JS tramite tale pipeline.
* Questa modifica può essere annullata solo da uno sviluppatore, eliminando `SiteConfig` e `HtmlPageItemsConfig` nodi sotto creati dall&#39;operazione `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Questa azione non converte automaticamente le librerie client esistenti del sito per utilizzare la pipeline di tipo font-end. Lo spostamento di queste origini dalla cartella della libreria client alla cartella della pipeline front-end richiede il lavoro manuale di uno sviluppatore front-end.

## Requisiti {#requirements}

AEM adattare automaticamente il sito esistente per utilizzare la pipeline front-end. Per eseguire questa operazione, il sito deve utilizzare [v2 o versioni successive del componente Pagina dei componenti core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html)

## Abilitazione della pipeline front-end {#enabling}

L’abilitazione del sito viene eseguita dalla console Sites utilizzando [Barra del sito.](site-rail.md)

1. Accedi a AEM e naviga sul tuo sito tramite **Navigazione globale** > **Sites**.
1. Seleziona il sito nella console. È necessario selezionare la directory principale del sito e non le pagine figlie.
1. Con il sito selezionato, apri la [selettore della barra](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) a sinistra e scegli **Sito**.
1. In **Sito** fai clic sul pulsante **Abilita pipeline front-end**.

   ![Abilita pipeline front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM chiede di confermare con una panoramica delle modifiche che verranno apportate. Conferma e il tuo sito è adattato.

Ora il tuo sito è pronto per utilizzare la pipeline front-end. Per ulteriori informazioni sulla pipeline front-end e sulla gestione del tema del sito, consulta:

* [Utilizzo della barra del sito per gestire il tema del sito](site-rail.md)
* [Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) - Questo percorso di documentazione offre una panoramica del processo di distribuzione rapida di un sito tramite la pipeline front-end e lo strumento di creazione rapida del sito.
* [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) - Questo documento descrive la pipeline front-end nel contesto delle pipeline full-stack e web.
