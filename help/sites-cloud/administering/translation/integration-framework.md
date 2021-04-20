---
title: Configurazione del framework di integrazione della traduzione
description: Scopri come configurare il framework di integrazione della traduzione per l’integrazione con i servizi di traduzione di terze parti.
feature: Language Copy
role: Administrator
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 2%

---


# Configurazione del framework di integrazione della traduzione {#configuring-the-translation-integration-framework}

Il framework di integrazione della traduzione si integra con servizi di traduzione di terze parti per orchestrare la traduzione dei contenuti AEM. Si tratta di tre passaggi fondamentali.

1. [Connettiti al provider di servizi di traduzione.](#connecting-to-a-translation-service-provider)
1. [Creare una configurazione di Translation Integration Framework.](#creating-a-translation-integration-configuration)
1. [Associa le configurazioni cloud alle pagine.](#configuring-pages-for-translation)

Per una panoramica delle funzioni di traduzione dei contenuti in AEM, consulta [Traduzione di contenuti per siti multilingue](overview.md).

## Connessione a un provider di servizi di traduzione {#connecting-to-a-translation-service-provider}

Crea una configurazione cloud che si connette AEM al provider di servizi di traduzione. AEM include la funzionalità di [connessione a Microsoft Translator](connect-ms-translator.md) per impostazione predefinita.

I seguenti fornitori di traduzione forniscono un’implementazione dell’API AEM per i progetti di traduzione.

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)  (Adobe Exchange Premier Partner)
* [Tecnologie del Tablet argilla](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartphone](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Sistro](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

Dopo aver installato un pacchetto di connettore, puoi creare una configurazione cloud per il connettore. In genere, è necessario fornire le credenziali per l&#39;autenticazione con il servizio di traduzione. Per informazioni sull&#39;aggiunta di una configurazione cloud per il connettore Microsoft Translator, vedere [Integrazione con Microsoft Translator](connect-ms-translator.md).

Se necessario, puoi creare più configurazioni cloud per lo stesso connettore. Ad esempio, crea una configurazione per ciascuno degli account o dei progetti che hai con lo stesso fornitore.

Dopo aver configurato una connessione, puoi creare la configurazione del framework di integrazione di traduzione che la utilizza.

## Creazione di una configurazione dell&#39;integrazione di traduzione {#creating-a-translation-integration-configuration}

Crea una configurazione del framework di integrazione della traduzione per specificare come tradurre il contenuto. La configurazione include le seguenti informazioni:

* Quale provider di servizi di traduzione utilizzare
* Se la traduzione umana o automatica deve essere eseguita
* Se tradurre altro contenuto associato a una pagina o a una risorsa, ad esempio i tag

Dopo aver creato una configurazione di framework, associ la configurazione cloud alle pagine che desideri tradurre in base alla configurazione. Quando il processo di traduzione viene avviato, il flusso di lavoro di traduzione procede in base alla configurazione del framework associato.

Quando diverse sezioni del sito web hanno requisiti di traduzione diversi, crea di conseguenza configurazioni di framework multiple. Ad esempio, un sito web multilingue potrebbe includere copie in lingua inglese, spagnola e giapponese. Il proprietario del sito utilizza due diversi fornitori di servizi di traduzione per le traduzioni in spagnolo e giapponese. Pertanto, sono configurate due configurazioni del framework. Ogni configurazione utilizza un provider di servizi di traduzione diverso.

Dopo aver configurato un framework di integrazione della traduzione, è possibile [associarlo alle pagine](preparation.md) che lo utilizzano.

>[!TIP]
>
>Per una panoramica delle funzioni di traduzione dei contenuti in AEM, consulta [Traduzione di contenuti per siti multilingue](overview.md).

Una singola configurazione del framework controlla come tradurre il contenuto e le risorse della pagina.

![Configurazione della traduzione](../assets/translation-configuration.png)

Per creare una nuova configurazione di traduzione:

1. Nel menu di navigazione [globale,](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) tocca o fai clic su **Strumenti -> Cloud Services - e Cloud Services di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione nella struttura del contenuto. Questo è spesso basato su un sito specifico o può essere globale.
1. Fornisci le seguenti informazioni nei campi, quindi tocca o fai clic su **Crea**:
   1. Seleziona **Tipo di configurazione** nel menu a discesa.
   1. Immetti un **Titolo** per la configurazione. La **Titolo** identifica la configurazione nella console **Cloud Services** e negli elenchi a discesa delle proprietà della pagina.
   1. Facoltativamente, digita un **Nome** da utilizzare per il nodo del repository che memorizza la configurazione.
1. Nella finestra **Modifica configurazione**, configura le proprietà nelle schede **Siti** e **Risorse**, quindi tocca o fai clic su **Salva e chiudi**.

### Proprietà di configurazione dei siti {#sites-configuration-properties}

La scheda **Sites** controlla le modalità di esecuzione della traduzione del contenuto della pagina.

| Proprietà | Descrizione |
|---|---|
| Flusso di lavoro per traduzione | Questa proprietà definisce il metodo di traduzione eseguito dal framework per il contenuto del sito:<br>- Traduzione automatica: Il provider di traduzione esegue la traduzione utilizzando la traduzione automatica in tempo reale.<br>- Traduzione umana: Il contenuto viene inviato al provider di traduzione per essere tradotto dai traduttori.<br>- Non Tradurre: Il contenuto non viene inviato per la traduzione. Questo consente di saltare alcuni rami di contenuto che non sarebbero tradotti ma che potrebbero essere aggiornati con i contenuti più recenti. |
| Provider traduzione | Questa proprietà definisce il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell&#39;elenco quando è installato il connettore corrispondente. |
| Categoria contenuto | (Solo traduzione automatica) Questa proprietà è una categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti. |
| Traduci tag | Questa opzione consente di tradurre i tag associati alla pagina. |
| Traduci risorse di pagina | Questa proprietà definisce come tradurre le risorse aggiunte ai componenti dal file system o a cui si fa riferimento dalle risorse:<br>- Non tradurre: Le risorse di pagina non sono tradotte.<br>- Utilizzo del flusso di lavoro di traduzione dei siti: Le risorse vengono gestite in base alle proprietà di configurazione nella scheda  **** Sitestab.<br>- Utilizzo del flusso di lavoro di traduzione delle risorse: Le risorse vengono gestite in base alle proprietà configurate nella scheda  **** Attività. |
| Esegui automaticamente traduzione | Abilita questa proprietà per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Non è possibile esaminare e ampliare il processo di traduzione quando si seleziona questa opzione. |

### Proprietà di configurazione delle risorse {#assets-configuration-properties}

Le proprietà delle risorse controllano come configurare le risorse. Per ulteriori informazioni sulla traduzione delle risorse, consulta [Creazione di copie per lingua per le risorse](/help/assets/translate-assets.md).

| Proprietà | Descrizione |
|---|---|
| Flusso di lavoro per traduzione | Questa proprietà seleziona il tipo di traduzione eseguito dal framework per le risorse:<br>- Traduzione automatica: Il provider di traduzione esegue la traduzione immediatamente utilizzando la traduzione automatica.<br>- Traduzione umana: Il contenuto viene inviato automaticamente al provider di traduzione per essere tradotto manualmente.<br>-Non tradurre: Le risorse non vengono inviate per la traduzione. |
| Provider traduzione | Questa proprietà definisce il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell&#39;elenco quando è installato il connettore corrispondente. |
| Categoria contenuto | (Solo traduzione automatica) Questa proprietà descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti. |
| Traduci risorse | Attiva questa proprietà per includere le risorse nel progetto di traduzione. |
| Traduci metadati | Attiva questa proprietà per tradurre i metadati della risorsa. |
| Traduci tag | Attiva questa proprietà per tradurre i tag associati alla risorsa. |
| Esegui automaticamente traduzione | Selezionare questa proprietà per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Non è possibile rivedere o ampliare il processo di traduzione quando si seleziona questa opzione. |

## Configurazione delle pagine per la traduzione {#configuring-pages-for-translation}

Per configurare la traduzione delle pagine sorgente in altre lingue, associa le pagine alle seguenti configurazioni cloud:

* Configurazione cloud che si connette AEM al provider di traduzione.
* Il framework di integrazione della traduzione che configura i dettagli della traduzione.

La configurazione cloud del framework di integrazione della traduzione identifica la configurazione cloud da utilizzare per la connessione al provider di servizi. Quando si associa una pagina sorgente a una configurazione cloud del framework, questa deve essere associata alla configurazione cloud del provider di servizi utilizzata dalla configurazione cloud del framework.

Quando si associa una pagina a una configurazione cloud, i discendenti della pagina ereditano l’associazione. Ad esempio, se associ la pagina `/content/wknd/language-masters/en/magazine` a un framework di integrazione della traduzione, la pagina `magazine` e le pagine figlie sottostanti vengono tradotte in base al framework.

Se necessario, è possibile modificare l’associazione in una pagina decrescente. Ad esempio, il contenuto di un sito web riguarda principalmente i viaggi e lo stile di vita. Tuttavia, un ramo di pagine descrive l’azienda. In questo caso, la pagina principale del sito potrebbe essere associata a un framework di integrazione della traduzione che specifica la traduzione automatica utilizzando la categoria Stile di vita, mentre il ramo che descrive la società utilizzerebbe un framework che esegue la traduzione automatica utilizzando la categoria Generale.

### Associazione di una pagina a un provider di traduzione {#associating-a-page-with-a-translation-provider}

Associa una pagina al provider di traduzione utilizzato per tradurre la pagina e le pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e tocca o fai clic su **Visualizza proprietà**.
1. Tocca o fai clic sulla scheda **Cloud Services** .
1. Nel menu a discesa **Aggiungi configurazione** , seleziona la configurazione.
1. Tocca o fai clic su **Salva e chiudi**.

### Associazione di pagine a un framework di integrazione della traduzione {#associating-pages-with-a-translation-integration-framework}

Associare una pagina a Translation Integration Framework che definisce come eseguire la traduzione della pagina e delle pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e tocca o fai clic su **Visualizza proprietà**.
1. Tocca o fai clic sulla scheda **Cloud Services** .
1. Nel menu a discesa **Aggiungi configurazione** , seleziona la configurazione.
1. Tocca o fai clic su **Salva e chiudi**.
