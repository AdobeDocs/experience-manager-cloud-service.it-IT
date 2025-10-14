---
title: Configurazione del framework di integrazione della traduzione
description: Scopri come configurare il Translation Integration Framework per integrarlo con servizi di traduzione di terze parti..
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 69%

---

# Configurazione del framework di integrazione della traduzione {#configuring-the-translation-integration-framework}

Il Translation Integration Framework si integra con servizi di traduzione di terze parti per orchestrare la traduzione dei contenuti AEM. Comporta tre passaggi fondamentali.

1. [Connettiti al tuo provider di servizi di traduzione](#connecting-to-a-translation-service-provider).
1. [Creare una configurazione del framework di integrazione della traduzione](#creating-a-translation-integration-configuration).
1. [Associa le configurazioni cloud alle pagine](#configuring-pages-for-translation).

Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](overview.md).

>[!TIP]
>
>Se non hai ancora tradotto i contenuti, consulta [Percorso di traduzione siti](/help/journey-sites/translation/overview.md), per una guida attraverso la traduzione dei contenuti AEM Sites tramite i potenti strumenti di traduzione dell&#39;AEM, ideali per chi non ha esperienza di AEM o traduzione.

## Connessione a un fornitore di servizi di traduzione {#connecting-to-a-translation-service-provider}

Crea una configurazione cloud che connette l’AEM al provider di servizi di traduzione.

Per impostazione predefinita, AEM include la funzionalità per [connettersi a Microsoft® Translator](connect-ms-translator.md). Altri fornitori di tecnologie di traduzione con connettori AEM che sono membri del programma partner Adobe Exchange sono disponibili [qui](https://exchange.adobe.com/apps/browse/ec?page=1&partnerLevel=All&product=AEM&q=experience+manager+translation&sort=RELEVANCE).

Dopo aver installato un pacchetto di connettori, puoi crearne una configurazione cloud. In genere, è necessario fornire le credenziali per l’autenticazione con il servizio di traduzione. Per informazioni sull&#39;aggiunta di una configurazione cloud per il connettore Microsoft® Translator, vedere [Integrazione con Microsoft® Translator](connect-ms-translator.md).

Se necessario, puoi creare più configurazioni cloud per lo stesso connettore. Ad esempio, crea una configurazione per ciascuno degli account o dei progetti che hai con lo stesso fornitore.

Dopo aver configurato una connessione, potete creare la configurazione del Translation Integration Framework che la utilizza.

## Creazione di una configurazione dell’integrazione di traduzione {#creating-a-translation-integration-configuration}

Crea una configurazione del framework di integrazione della traduzione per specificare come tradurre il contenuto. La configurazione include le seguenti informazioni:

* Quale fornitore di servizi di traduzione utilizzare
* Se deve essere eseguita la traduzione umana o automatica
* Ad esempio, se tradurre altri contenuti associati a una pagina o a una risorsa, come i tag.

Dopo aver creato una configurazione del framework, associa la configurazione cloud alle pagine che desideri tradurre. Quando il processo di traduzione viene avviato, il flusso di lavoro di traduzione procede in base alla configurazione del framework associato.

Quando diverse sezioni del sito Web hanno requisiti di traduzione diversi, crea di conseguenza configurazioni di framework multiple. Ad esempio, un sito Web multilingue potrebbe includere copie in lingua inglese, spagnola e giapponese. Il proprietario del sito utilizza due diversi fornitori di servizi di traduzione per le versioni in spagnolo e giapponese. Pertanto, sono attive due configurazioni del framework. Ogni configurazione utilizza un provider di servizi di traduzione diverso.

Dopo aver configurato un Translation Integration Framework, puoi [associarlo alle pagine](preparation.md) che lo usano.

>[!TIP]
>
>Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](overview.md).

Una singola configurazione del framework controlla come vengono tradotti il contenuto e le risorse della pagina. Per creare una configurazione di traduzione:

1. Nel [menu di navigazione globale](/help/sites-cloud/authoring/basic-handling.md#global-navigation), seleziona **Strumenti > Cloud Service e Cloud Service di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione nella struttura del contenuto. Questo è spesso basato su un sito specifico o può essere globale.
1. Fornisci le seguenti informazioni nei campi, quindi seleziona **Crea**.:
   1. Seleziona **Tipo di configurazione** nel menu a discesa.
   1. Inserisci un **Titolo** per la configurazione. Il **Titolo** identifica la configurazione nella console **Cloud Services** così come negli elenchi a discesa delle proprietà della pagina.
   1. Facoltativamente, digita un **Nome** da utilizzare per il nodo dell’archivio che memorizza la configurazione.
1. Nella finestra **Modifica configurazione**, configura le proprietà nelle schede **Sites** e **Assets**, quindi seleziona **Salva e chiudi**.

### Proprietà di configurazione Sites {#sites-configuration-properties}

La scheda **Sites** controlla come viene eseguita la traduzione del contenuto della pagina.

![Configurazione della traduzione per Sites](../assets/translation-configuration.png)

| Proprietà | Descrizione |
|---|---|
| Metodo di traduzione | Questa proprietà definisce il metodo di traduzione applicato dal framework per il contenuto del sito:<br>- Traduzione automatica: il fornitore di traduzione esegue la traduzione utilizzando la traduzione automatica in tempo reale.<br>- Traduzione umana: il contenuto viene inviato al team di traduttori del fornitore di traduzione.<br>- Non tradurre: il contenuto non viene inviato per la traduzione. Questo consente di saltare alcune parti di contenuto che non sarebbero tradotte, ma che potrebbero essere aggiornate con i contenuti più recenti. |
| Provider traduzione | Questa proprietà definisce il fornitore di traduzione per eseguire la traduzione. Il fornitore viene visualizzato nell’elenco quando è installato il connettore corrispondente. |
| Categoria contenuto | (Solo traduzione automatica) Questa proprietà è una categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti. |
| Traduci tag | Questa opzione consente di tradurre i tag associati alla pagina. |
| Traduci risorse di pagina | Questa proprietà definisce come tradurre le risorse aggiunte ai componenti dal file system o a cui le risorse fanno riferimento:<br>- Non tradurre: le risorse di pagina non sono tradotte.<br>- Utilizzo del flusso di lavoro di traduzione dei siti: le risorse vengono gestite in base alle proprietà di configurazione nella scheda **Sites**.<br>- Utilizzo del flusso di lavoro di traduzione delle risorse: le risorse vengono gestite in base alle proprietà configurate nella scheda **Assets**. |
| Esegui traduzione automatica | Abilita questa proprietà per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Quando si seleziona questa opzione, non è possibile rivedere e modificare l’ambito del processo di traduzione. |
| Disattiva la traduzione di solo aggiornamento | Quando questa opzione è selezionata, l’aggiornamento del progetto di traduzione invia tutti i campi traducibili per la traduzione, non solo quelli modificati dall’ultima traduzione. |

### Proprietà di configurazione Assets {#assets-configuration-properties}

Le proprietà di Assets controllano la modalità di configurazione delle risorse. Per ulteriori informazioni sulla traduzione delle risorse, consulta [Creazione di copie per lingua per Assets](/help/assets/translate-assets.md).

![Configurazione traduzione per Sites](../assets/translation-configuration-assets.png)

| Proprietà | Descrizione |
|---|---|
| Metodo di traduzione | Questa proprietà seleziona il tipo di traduzione eseguito dal framework per le risorse:<br>- Traduzione automatica: il fornitore di traduzione avvia immediatamente la traduzione automatica.<br>- Traduzione umana: il contenuto viene inviato automaticamente al fornitore di traduzione per essere tradotto manualmente.<br>-Non tradurre: le risorse non vengono inviate per la traduzione. |
| Provider traduzione | Questa proprietà definisce il fornitore di traduzione per eseguire la traduzione. Il fornitore viene visualizzato nell’elenco quando è installato il connettore corrispondente. |
| Categoria contenuto | (Solo traduzione automatica) Questa proprietà descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti. |
| Traduci risorse | Attiva questa proprietà per includere le risorse nel progetto di traduzione. |
| Traduci metadati | Attiva questa proprietà per tradurre i metadati della risorsa. |
| Traduci tag | Attiva questa proprietà per tradurre i tag associati alla risorsa. |
| Esegui traduzione automatica | Seleziona questa proprietà per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Quando si seleziona questa opzione, non è possibile rivedere o modificare l’ambito del processo di traduzione. |
| Disattiva la traduzione di solo aggiornamento | Quando questa opzione è selezionata, l’aggiornamento del progetto di traduzione invia tutti i campi traducibili per la traduzione, non solo quelli modificati dall’ultima traduzione. |
| Abilita campi modello di contenuto per la traduzione | L&#39;abilitazione di questa opzione utilizza il campo **Traducibile** nei [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties) per determinare se il campo è tradotto e crea automaticamente [regole di traduzione](rules.md) di conseguenza. Questa opzione sostituisce eventuali regole di traduzione create dall’utente. |

## Configurazione pagine per la traduzione {#configuring-pages-for-translation}

Per configurare la traduzione delle pagine sorgente in altre lingue, associa le pagine alle seguenti configurazioni cloud:

* La configurazione cloud che connette AEM al fornitore di traduzione.
* Il framework di integrazione della traduzione che configura i dettagli della traduzione.

La configurazione cloud del framework di integrazione della traduzione identifica la configurazione cloud da utilizzare per la connessione al provider di servizi. Quando si associa una pagina origine a una configurazione cloud del framework, la pagina deve essere associata alla configurazione cloud del fornitore del servizio utilizzato dalla configurazione cloud del framework.

Quando si associa una pagina a una configurazione cloud, i discendenti della pagina ereditano tale associazione. Ad esempio, se hai associato la pagina `/content/wknd/language-masters/en/magazine` a un framework di integrazione della traduzione, la pagina `magazine` e le sue pagine secondarie vengono tradotte in base al framework.

Se necessario, è possibile sovrascrivere tale associazione in una pagina discendente. Prendiamo ad esempio il contenuto di un sito web che tratta principalmente argomenti di viaggi e lifestyle. Alcune pagine del sito sono tuttavia dedicate alla descrizione dell’azienda. In questo caso, la pagina principale del sito può essere associata a un framework di integrazione della traduzione che specifica la traduzione automatica utilizzando la categoria Lifestyle. Il ramo che descrive l’azienda utilizza un framework che esegue la traduzione automatica utilizzando la categoria Generale.

### Associazione di una pagina a un fornitore di traduzione {#associating-a-page-with-a-translation-provider}

Associa una pagina al fornitore di traduzione utilizzato per tradurre tale pagina e le relative pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e seleziona **Visualizza proprietà**.
1. Seleziona la scheda **Servizi cloud**.
1. Selezionare la configurazione nell&#39;elenco a discesa **Aggiungi configurazione**.
1. Seleziona **Salva e chiudi**.

### Associazione di pagine a un framework di integrazione della traduzione {#associating-pages-with-a-translation-integration-framework}

Associa una pagina a un framework di integrazione della traduzione che definisce come eseguire la traduzione della pagina e delle relative pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e seleziona **Visualizza proprietà**.
1. Seleziona la scheda **Servizi cloud**.
1. Selezionare la configurazione nell&#39;elenco a discesa **Aggiungi configurazione**.
1. Seleziona **Salva e chiudi**.
