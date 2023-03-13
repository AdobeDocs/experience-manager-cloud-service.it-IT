---
title: Routing modello SPA
description: Per le applicazioni a pagina singola nell’AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Routing modello SPA{#spa-model-routing}

Per le applicazioni a pagina singola nell’AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.

## Indirizzamento progetto {#project-routing}

L’app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il routing specifico del modello restituito dal server AEM. La struttura dati del modello di pagina espone l’URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di indirizzamento. Quando una route richiede un frammento di modello, invia una chiamata al `PageModelManager.getData()` funzione. Quando viene modificata una route di modello, deve essere attivato un evento per avvisare le librerie in ascolto, come l’Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, fare riferimento al [PageModelManager](blueprint.md#pagemodelmanager) sezione del documento Blueprint dell’SPA.

## ModelRouter {#modelrouter}

Il `ModelRouter` - quando abilitato - incapsula le funzioni API della cronologia di HTML5 `pushState` e `replaceState` per garantire che un determinato frammento di modello sia preacquisito e accessibile. Notifica quindi al componente front-end registrato che il modello è stato modificato.

## Routing modello manuale e automatico {#manual-vs-automatic-model-routing}

Il `ModelRouter` automatizza il recupero dei frammenti del modello. Ma come qualsiasi strumento automatizzato è dotato di limitazioni. Quando necessario, il `ModelRouter` possono essere disattivati o configurati per ignorare i percorsi che utilizzano le metaproprietà (vedi la sezione Meta Properties della sezione [Componente pagina SPA](page-component.md) documento). Gli sviluppatori front-end possono quindi implementare il proprio livello di routing del modello richiedendo `PageModelManager` per caricare un determinato frammento di modello utilizzando `getData()` funzione.

>[!CAUTION]
>
>La versione corrente del `ModelRouter` supporta solo l’utilizzo di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’utilizzo di URL personalizzati o alias.

## Contratto ciclo {#routing-contract}

L’implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l’API Cronologia HTML5 per il routing alle diverse pagine dell’applicazione.

### Configurazione {#configuration}

Il `ModelRouter` supporta il concetto di instradamento del modello mentre ascolta `pushState` e `replaceState` chiamate a frammenti di modello di preacquisizione. Internamente attiva il `PageModelManager` per caricare il modello che corrisponde a un determinato URL e genera un `cq-pagemodel-route-changed` che altri moduli possono ascoltare.

Per impostazione predefinita, questo comportamento viene attivato automaticamente. Per disattivarla, l’SPA deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Ogni via del SPA deve corrispondere a una risorsa accessibile nell&#39;AEM (ad esempio, &quot; `/content/mysite/mypage"`) dal `PageModelManager` tenta automaticamente di caricare il modello di pagina corrispondente una volta selezionato il percorso. Tuttavia, se necessario, l&#39;SPA può anche definire un &quot;elenco Bloccati&quot; di vie che devono essere ignorate dall&#39;Autorità `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
