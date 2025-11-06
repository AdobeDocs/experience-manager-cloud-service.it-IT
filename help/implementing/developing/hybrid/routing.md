---
title: Indirizzamento del modello SPA
description: Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# Indirizzamento del modello SPA{#spa-model-routing}

Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.

{{ue-over-spa}}

## Indirizzamento progetto {#project-routing}

L’app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il routing specifico per il modello restituito dal server AEM. La struttura dati del modello di pagina espone l’URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di indirizzamento. Quando una route prevede un frammento di modello, è possibile effettuare una chiamata alla funzione `PageModelManager.getData()`. Quando viene modificata una route di modello, deve essere attivato un evento per avvisare le librerie in ascolto, come l’Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, consulta la sezione [PageModelManager](blueprint.md#pagemodelmanager) del documento Blueprint SPA.

## ModelRouter {#modelrouter}

`ModelRouter` - se abilitato - incapsula le funzioni API della cronologia di HTML5 `pushState` e `replaceState` per garantire che un determinato frammento di modello sia preacquisito e accessibile. Notifica quindi al componente front-end registrato che il modello è stato modificato.

## Routing modello manuale e automatico {#manual-vs-automatic-model-routing}

`ModelRouter` automatizza il recupero dei frammenti del modello. Ma come qualsiasi strumento automatizzato è dotato di limitazioni. Se necessario, è possibile disabilitare o configurare `ModelRouter` per ignorare i percorsi che utilizzano le proprietà meta (vedere la sezione Proprietà Meta del documento [Componente pagina SPA](page-component.md)). Gli sviluppatori front-end possono quindi implementare il proprio livello di routing del modello richiedendo a `PageModelManager` di caricare un determinato frammento di modello utilizzando la funzione `getData()`.

>[!CAUTION]
>
>La versione corrente di `ModelRouter` supporta solo l&#39;utilizzo di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’utilizzo di URL personalizzati o alias.

## Contratto ciclo {#routing-contract}

L’implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l’API della cronologia di HTML5 per il routing alle diverse pagine dell’applicazione.

### Configurazione {#configuration}

`ModelRouter` supporta il concetto di routing del modello in quanto ascolta le chiamate `pushState` e `replaceState` per la preacquisizione dei frammenti del modello. Internamente, attiva `PageModelManager` per caricare il modello corrispondente a un determinato URL e genera un evento `cq-pagemodel-route-changed` a cui altri moduli possono fare da listener.

Per impostazione predefinita, questo comportamento viene attivato automaticamente. Per disattivarla, l’applicazione a pagina singola deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Ogni route dell&#39;applicazione a pagina singola deve corrispondere a una risorsa accessibile in AEM (ad esempio, &quot; `/content/mysite/mypage"`) poiché `PageModelManager` tenterà automaticamente di caricare il modello di pagina corrispondente una volta selezionata la route. Tuttavia, se necessario, l&#39;applicazione a pagina singola può anche definire un &quot;elenco Bloccati&quot; di route che devono essere ignorate da `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
