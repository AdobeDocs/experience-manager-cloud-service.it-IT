---
title: Indirizzamento modello SPA
description: Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Indirizzamento modello SPA{#spa-model-routing}

Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.

## Indirizzamento del progetto {#project-routing}

L’app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il ciclo specifico del modello restituito dal server AEM. La struttura dati del modello di pagina espone l’URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di routing. Una volta che una route richiede un frammento di modello, una chiamata al `PageModelManager.getData()` può essere fatto. Quando una route del modello è cambiata, deve essere attivato un evento per avvertire le librerie di ascolto come Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, fai riferimento al [PageModelManager](blueprint.md#pagemodelmanager) sezione del documento Blueprint SPA.

## ModelRouter {#modelrouter}

La `ModelRouter` - se attivato - incapsula le funzioni dell’API di cronologia di HTML5 `pushState` e `replaceState` per garantire che un dato frammento di modello sia preacquisito e accessibile. Successivamente, notifica al componente front-end registrato che il modello è stato modificato.

## Routing del modello manuale e automatico {#manual-vs-automatic-model-routing}

La `ModelRouter` automatizza il recupero dei frammenti del modello. Ma come ogni attrezzo automatizzato è dotato di limitazioni. Quando necessario, `ModelRouter` può essere disabilitato o configurato per ignorare i percorsi che utilizzano le proprietà metadati (consulta la sezione Meta Properties del [Componente pagina SPA](page-component.md) documento). Gli sviluppatori front-end possono quindi implementare il proprio livello di routing del modello richiedendo `PageModelManager` per caricare un dato frammento di modello utilizzando `getData()` funzione .

>[!CAUTION]
>
>La versione corrente del `ModelRouter` supporta solo l’uso di URL che puntano al percorso effettivo della risorsa dei punti di ingresso del modello Sling. Non supporta l’utilizzo di URL personalizzati o alias.

## Contratto di distribuzione {#routing-contract}

L’implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l’API History di HTML5 per l’indirizzamento alle diverse pagine dell’applicazione.

### Configurazione {#configuration}

La `ModelRouter` supporta il concetto di indirizzamento del modello in attesa di `pushState` e `replaceState` chiamate ai frammenti del modello di preacquisizione. Internamente attiva il `PageModelManager` per caricare il modello che corrisponde a un determinato URL e genera un `cq-pagemodel-route-changed` evento che altri moduli possono ascoltare.

Per impostazione predefinita, questo comportamento è abilitato automaticamente. Per disattivarlo, il SPA deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Tieni presente che ogni percorso del SPA deve corrispondere a una risorsa accessibile in AEM (ad esempio, &quot; `/content/mysite/mypage"`) dal `PageModelManager` cercherà automaticamente di caricare il modello di pagina corrispondente una volta selezionato il percorso. Anche se, se necessario, il SPA può anche definire un &quot;elenco Bloccati&quot; di rotte che devono essere ignorate dal `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
