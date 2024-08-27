---
title: Abilitazione della pipeline front-end
description: Scopri come abilitare la pipeline front-end per i siti esistenti per utilizzare i temi del sito per personalizzarlo più rapidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
source-git-commit: d6ecdae8dd78c3c93a410ca2c8b80322340f439e
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 45%

---

# Abilitazione della pipeline front-end {#enable-front-end-pipeline}

Scopri come abilitare la pipeline front-end per i siti esistenti per utilizzare i temi del sito per personalizzarlo più rapidamente.

## Panoramica {#overview}

La pipeline front-end è un meccanismo che può distribuire rapidamente solo il codice front-end dei siti Web basato sui [temi del sito](site-themes.md) e i [modelli del sito.](site-templates.md)

Questa pipeline gestisce solo il codice front-end, rendendo il processo di distribuzione più rapido rispetto alle distribuzioni full-stack. Consente agli sviluppatori front-end di personalizzare facilmente il sito senza dover conoscere l’AEM.

Per impostazione predefinita, i siti basati sui modelli di sito possono sfruttare la pipeline front-end. Questo documento descrive come adattare i siti esistenti per sfruttare la pipeline front-end.

>[!TIP]
>
>Se non conosci la pipeline front-end e le modalità di distribuzione rapida dei siti che la utilizzano insieme ai modelli, consulta [Percorso per la creazione rapida dei siti](/help/journey-sites/quick-site/overview.md) per un&#39;introduzione.

AEM può configurare il sito per caricare i temi distribuiti con la pipeline front-end, anche se il sito non è stato creato utilizzando modelli e temi del sito, sovrapponendoli a librerie client esistenti.

## Dettagli tecnici {#technical-details}

Quando attivi la pipeline front-end per un sito, AEM apporta le seguenti modifiche alla struttura del sito.

* Tutte le pagine del sito includono un file CSS e JS aggiuntivo, che può essere modificato distribuendo aggiornamenti tramite una pipeline front-end di Cloud Manager dedicata.
* I file CSS e JS aggiunti sono inizialmente vuoti. Tuttavia, puoi scaricare una cartella &quot;sorgenti del tema&quot; per impostare la struttura di cartelle necessaria per distribuire gli aggiornamenti del codice CSS e JS tramite la pipeline.
* Solo uno sviluppatore può annullare la modifica eliminando i nodi `SiteConfig` e `HtmlPageItemsConfig` creati dall&#39;operazione sotto `/conf/<site-name>/sling:configs`.

>[!NOTE]
>
>Questa azione non converte automaticamente le librerie client esistenti del sito per utilizzare la pipeline font-end. Lo spostamento di queste sorgenti dalla cartella della libreria client alla cartella della pipeline front-end richiede il lavoro manuale di uno sviluppatore front-end.

## Requisiti  {#requirements}

AEM puà adattare automaticamente il sito esistente per utilizzare la pipeline front-end. Per poter eseguire questo flusso di lavoro, il sito deve utilizzare [v2 o versione successiva del componente Pagina dei Componenti Core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/page).

## Abilitazione della pipeline front-end {#enabling}

{{add-cm-allowlist-frontend-pipeline}}

L&#39;abilitazione del sito viene eseguita dalla console Sites utilizzando la [barra Sito](site-rail.md).

1. Accedi ad AEM e naviga sul tuo sito tramite la **Navigazione globale** > **Sites**.
1. Seleziona il sito nella console. Seleziona la directory principale del sito e non le pagine figlie.
1. Con il sito selezionato, apri il [selettore della barra](/help/sites-cloud/authoring/basic-handling.md#rail-selector) a sinistra e scegli **Sito**.
1. Nella barra del **Sito**, fai clic sul pulsante **Abilita pipeline front-end**.

   ![Abilita pipeline front-end](/help/sites-cloud/administering/assets/enable-front-end-pipeline.png)

1. L’AEM ti chiede di confermare una panoramica delle modifiche apportate. Una volta confermato, il tuo sito viene adattato.

Ora il tuo sito è pronto per utilizzare la pipeline front-end. Per ulteriori informazioni sulla pipeline front-end e sulla gestione del tema del sito, consulta:

* [Utilizzo della barra Sito per gestire il tema del sito](site-rail.md)
* [Percorso di Creazione Rapida dei Siti](/help/journey-sites/quick-site/overview.md): questo percorso di documentazione offre una panoramica del processo di distribuzione di un sito tramite la pipeline front-end e lo strumento di Creazione Rapida dei Siti.
* [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end): questo documento descrive la pipeline front-end nel contesto dei livelli pipeline full-stack e web.
