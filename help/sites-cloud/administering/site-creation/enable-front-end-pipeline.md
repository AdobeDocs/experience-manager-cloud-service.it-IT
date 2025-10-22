---
title: Abilitazione della pipeline front-end
description: Scopri come abilitare la pipeline front-end per i siti di authoring AEM tradizionali esistenti con distribuzione di pubblicazione per utilizzare i temi del sito per personalizzarlo più rapidamente.
feature: Administering
role: Admin
exl-id: 55d54d72-f87b-47c9-955f-67ec5244dd6e
solution: Experience Manager Sites
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 24%

---


# Abilitazione della pipeline front-end {#enable-front-end-pipeline}

{{traditional-aem}}

Scopri come abilitare la pipeline front-end per i siti di authoring AEM tradizionali esistenti con distribuzione di pubblicazione per utilizzare i temi del sito per personalizzarlo più rapidamente.

## Panoramica {#overview}

La pipeline front-end è un meccanismo per i progetti di authoring AEM tradizionali con [distribuzione pubblicazione](/help/sites-cloud/authoring/author-publish.md) che può distribuire rapidamente solo il codice front-end dei siti Web in base a [temi del sito](site-themes.md) e [modelli del sito.](site-templates.md)

Questa pipeline gestisce solo il codice front-end, rendendo il processo di distribuzione più rapido rispetto alle distribuzioni full-stack. Consente agli sviluppatori front-end di personalizzare facilmente il sito senza dover conoscere AEM.

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

1. AEM richiede di confermare una panoramica delle modifiche apportate. Una volta confermato, il tuo sito viene adattato.

Ora il tuo sito è pronto per utilizzare la pipeline front-end. Per ulteriori informazioni sulla pipeline front-end e sulla gestione del tema del sito, consulta:

* [Utilizzo della barra Sito per gestire il tema del sito](site-rail.md)
* [Percorso di Creazione Rapida dei Siti](/help/journey-sites/quick-site/overview.md): questo percorso di documentazione offre una panoramica del processo di distribuzione di un sito tramite la pipeline front-end e lo strumento di Creazione Rapida dei Siti.
* [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end): questo documento descrive la pipeline front-end nel contesto dei livelli pipeline full-stack e web.

## Pipeline front-end e domini personalizzati {#custom-domains}

La pipeline front-end può essere utilizzata con [funzionalità domini personalizzati di Cloud Manager,](/help/implementing/cloud-manager/custom-domain-names/introduction.md) ma tieni presente i seguenti requisiti quando utilizzi le due funzionalità insieme.

### File front-end statici {#static-files}

Le risorse front-end statiche distribuite tramite la pipeline front-end verranno servite, per impostazione predefinita, dal dominio statico predefinito di Adobe.

Se hai bisogno di un dominio personalizzato per le risorse front-end, puoi installare un dominio personalizzato sul livello di pubblicazione e configurare Dispatcher per instradare percorsi specifici (ad esempio `/static/`) alla posizione di hosting statica di Adobe. Questo metodo richiede l&#39;aggiornamento delle [regole Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher) per inoltrare e memorizzare in cache correttamente le richieste di risorse statiche.

Dopo aver configurato il dominio personalizzato e Dispatcher, puoi configurare AEM per distribuire le risorse front-end dal dominio statico.

### Configurazione {#configuration}

Come descritto nella sezione [Dettagli tecnici](#technical-details), l&#39;attivazione della funzione Pipeline front-end per un sito crea un nodo `SiteConfig` e `HtmlPageItemsConfig` sotto `/conf/<site-name>/sling:configs`.

Se desideri utilizzare la funzione domini personalizzati di Cloud Manager per il sito insieme alla pipeline front-end per le risorse di stato, è necessario aggiungere proprietà aggiuntive a questi nodi.

1. Impostare la proprietà `customFrontendPrefix` in `SiteConfig` per il sito.
   1. Accedi a `/conf/<site-name>/sling:configs/com.adobe.aem.wcm.site.manager.config.SiteConfig`.
   1. Aggiungere o aggiornare la proprietà `customFrontendPrefix = "https://your-custom-domain.com/static/"`.
1. Il valore `prefixPath` di `HtmlPageItemsConfig` viene aggiornato con il dominio personalizzato.
   1. Accedi a `/conf/<site-name>/sling:configs/com.adobe.cq.wcm.core.components.config.HtmlPageItemsConfig`.
   1. Verificare che `prefixPath` rifletta il dominio personalizzato, ad esempio `prefixPath = "https://your-custom-domain.com/static/<hash>/..."`.
   * Se necessario, è anche possibile sovrascrivere manualmente questo valore.
1. Verifica la configurazione.
   1. Dopo la distribuzione, verifica che le pagine facciano riferimento correttamente agli artefatti del tema del dominio personalizzato.
   1. Apri gli strumenti per sviluppatori del browser e controlla i percorsi dei file `theme.css` e `theme.js` per verificare che siano caricati dal dominio corretto.

Le pagine del sito fanno quindi riferimento agli artefatti del tema da tale URL aggiornato. Il dispatcher indirizza quindi le richieste di tali risorse al dominio statico.

## Best practice per gli sviluppatori front-end {#best-practices}

Se devi sviluppare e testare le risorse front-end localmente prima di distribuirle tramite la pipeline front-end, considera i seguenti approcci:

* Utilizza la modalità proxy di [Site Theme Builder](https://github.com/adobe/aem-site-theme-builder?tab=readme-ov-file#proxy) per ignorare gli artefatti del tema a livello locale per il test.
* Distribuisci manualmente i file dei temi da un server di sviluppo locale e aggiorna `prefixPath` in `HtmlPageItemsConfig` in modo che corrispondano all&#39;indirizzo del server locale.
* Assicurati che la memorizzazione nella cache del browser sia disabilitata durante il test per visualizzare gli aggiornamenti live.

Per ulteriori dettagli sullo sviluppo front-end locale, consulta la [documentazione di Site Theme Builder.](https://github.com/adobe/aem-site-theme-builder)
