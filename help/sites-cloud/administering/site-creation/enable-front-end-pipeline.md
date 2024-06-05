---
title: Abilitazione della pipeline front-end
description: Scopri come abilitare la pipeline front-end per i siti esistenti, per utilizzare i temi per personalizzare più rapidamente il tuo sito.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 98%

---

# Abilitazione della pipeline front-end {#enable-front-end-pipeline}

Scopri come abilitare la pipeline front-end per i siti esistenti, per utilizzare i temi per personalizzare più rapidamente il tuo sito.

## Panoramica {#overview}

La pipeline front-end è un meccanismo che può distribuire rapidamente solo il codice front-end dei siti Web basato sui [temi del sito](site-themes.md) e i [modelli del sito.](site-templates.md)

Invece di distribuire l’intero stack, questa pipeline gestisce solo il codice front-end, rendendo il processo più veloce e consentendo agli sviluppatori di personalizzare facilmente e rapidamente il sito senza conoscere AEM.

Per impostazione predefinita, i siti basati sui modelli di sito possono sfruttare la pipeline front-end. Questo documento descrive come adattare i siti esistenti per sfruttare la pipeline front-end.

>[!TIP]
>
>Se non conosci la pipeline front-end e le modalità di distribuzione rapida dei siti che la utilizzano insieme ai modelli, consulta la sezione [Percorso di creazione rapida dei siti](/help/journey-sites/quick-site/overview.md) per una panoramica.

Se non hai creato il sito esistente in base a modelli e temi del sito, AEM può configurarlo per caricare i temi distribuiti con la pipeline front-end sopra le librerie client esistenti.

## Dettagli tecnici {#technical-details}

Quando attivi la pipeline front-end per un sito, AEM apporta le seguenti modifiche alla struttura del sito.

* Tutte le pagine del sito includeranno un ulteriore file CSS e JS, che può essere modificato distribuendo aggiornamenti tramite una pipeline front-end di Cloud Manager dedicata.
* I file CSS e JS aggiunti saranno inizialmente vuoti, ma può essere scaricata una cartella &quot;sorgenti del tema&quot; per avviare la struttura delle cartelle che consente di distribuire gli aggiornamenti del codice CSS e JS tramite tale pipeline.
* Questa modifica può essere annullata solo da uno sviluppatore, eliminando i nodi `SiteConfig` e `HtmlPageItemsConfig` creati dall&#39;operazione `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Questa azione non converte automaticamente le librerie client del sito esistenti per utilizzare la pipeline di tipo font-end. Lo spostamento di queste sorgenti dalla cartella della libreria client alla cartella della pipeline front-end richiede il lavoro manuale di uno sviluppatore front-end.

## Requisiti  {#requirements}

AEM puà adattare automaticamente il sito esistente per utilizzare la pipeline front-end. Per eseguire questa operazione, il sito deve utilizzare [v2 o versioni successive del Componente Pagina dei Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/page.html?lang=it)

## Abilitazione della pipeline front-end {#enabling}

L’abilitazione del sito viene eseguita dalla console Sites utilizzando la [Barra del sito.](site-rail.md)

1. Accedi ad AEM e naviga sul tuo sito tramite la **Navigazione globale** > **Sites**.
1. Seleziona il sito nella console. Seleziona la directory principale del sito e non le pagine figlie.
1. Con il sito selezionato, apri il [selettore della barra](/help/sites-cloud/authoring/basic-handling.md#rail-selector) a sinistra e scegli **Sito**.
1. Nella barra del **Sito**, fai clic sul pulsante **Abilita pipeline front-end**.

   ![Abilita pipeline front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. AEM ti chiederà di confermare una panoramica delle modifiche che verranno apportate. Una volta confermato, il tuo sito viene adattato.

Ora il tuo sito è pronto per utilizzare la pipeline front-end. Per ulteriori informazioni sulla pipeline front-end e sulla gestione del tema del sito, consulta:

* [Utilizzo della barra Sito per gestire il tema del sito](site-rail.md)
* [Percorso di Creazione Rapida dei Siti](/help/journey-sites/quick-site/overview.md): questo percorso di documentazione offre una panoramica del processo di distribuzione di un sito tramite la pipeline front-end e lo strumento di Creazione Rapida dei Siti.
* [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end): questo documento descrive la pipeline front-end nel contesto dei livelli pipeline full-stack e web.
