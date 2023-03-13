---
title: Componente pagina SPA
description: In un SPA il componente page non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. Questo documento spiega come questo renda univoco il componente page di un SPA.
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 8%

---

# Componente pagina SPA {#spa-page-component}

Il componente page di un SPA non fornisce gli elementi HTML dei suoi componenti secondari tramite un file JSP o HTL e oggetti risorsa. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti figlio viene recuperata come struttura di dati JSON (ovvero il modello). I componenti SPA vengono quindi aggiunti alla pagina in base al modello JSON fornito. Di conseguenza, la composizione del corpo iniziale del componente Pagina è diversa dalle controparti HTML sottoposte a rendering preliminare.

## Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a un [`PageModelManager`](blueprint.md#pagemodelmanager) modulo. L&#39;SPA deve interagire con `PageModelManager` modulo quando viene inizializzato per recuperare il modello della pagina iniziale e registrarsi per gli aggiornamenti del modello, per lo più prodotto quando l’autore modifica la pagina tramite l’Editor pagina. Il `PageModelManager` è accessibile dal progetto SPA come pacchetto npm. Interprete tra l&#39;AEM e l&#39;SPA, il `PageModelManager` deve accompagnare l’SPA.

Per consentire l’authoring della pagina, una libreria client denominata `cq.authoring.pagemodel.messaging` per fornire un canale di comunicazione tra l’SPA e l’editor pagina. Se il componente Pagina SPA eredita dalla pagina wcm/core, allora sono disponibili le seguenti opzioni per rendere `cq.authoring.pagemodel.messaging` categoria librerie client disponibile:

* Se il modello è modificabile, aggiungi la categoria della libreria client al criterio della pagina.
* Aggiungere la categoria di librerie client utilizzando `customfooterlibs.html` del componente Pagina.

Non dimenticare di limitare l&#39;inclusione di `cq.authoring.pagemodel.messaging` al contesto dell’editor pagina.

## Tipo di dati di comunicazione {#communication-data-type}

Il tipo di dati di comunicazione viene impostato come elemento HTML all’interno del componente Pagina AEM utilizzando `data-cq-datatype` attributo. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste GET raggiungono gli endpoint del modello Sling di un componente. Dopo che si verifica un aggiornamento nell’editor di pagine, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello di pagina. La libreria Modello pagina avvisa quindi l’SPA in merito agli aggiornamenti.

**Componente pagina SPA -`body.html`**

```
<div id="page"></div>
```

Oltre a essere una buona pratica per non ritardare la generazione del DOM, il framework SPA richiede che gli script vengano aggiunti alla fine del corpo.

**Componente pagina SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Le proprietà delle metarisorse che descrivono il contenuto dell’SPA:

**Componente pagina SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Il selettore del modello di default è impostato in modo statico quando si richiede la rappresentazione del modello Sling di un componente.

## Metaproprietà {#meta-properties}

* `cq:wcmmode`: modalità WCM degli editor (ad esempio, pagina, modello)
* `cq:pagemodel_root_url`: URL del modello principale dell’app. Fondamentale quando si accede direttamente a una pagina figlio, poiché il modello di pagina figlio è un frammento del modello principale dell’app. Il `PageModelManager` quindi ricompone sistematicamente il modello iniziale dell&#39;applicazione come ingresso nell&#39;applicazione dal relativo punto di ingresso principale.
* `cq:pagemodel_router`: attiva o disattiva la [`ModelRouter`](routing.md) del `PageModelManager` libreria
* `cq:pagemodel_route_filters`: elenco separato da virgole o espressioni regolari per fornire percorsi [`ModelRouter`](routing.md) deve ignorare.

## Sincronizzazione sovrapposizione editor pagina {#page-editor-overlay-synchronization}

La sincronizzazione delle sovrapposizioni è garantita dallo stesso Mutation Observer fornito da `cq.authoring.page` categoria.

## Configurazione della struttura esportata JSON del modello Sling {#sling-model-json-exported-structure-configuration}

Quando le funzionalità di routing sono abilitate, si presume che l’esportazione JSON dell’SPA contenga le diverse route dell’applicazione grazie all’esportazione JSON del componente di navigazione AEM. L’output JSON del componente di navigazione AEM può essere configurato nel criterio del contenuto della pagina principale dell’SPA tramite le due proprietà seguenti:

* `structureDepth`: numero corrispondente alla profondità della struttura esportata
* `structurePatterns`: Regex dell’array di regex corrispondenti alla pagina da esportare
