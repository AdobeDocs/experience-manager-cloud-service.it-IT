---
title: Routing modello SPA
description: Per le applicazioni a pagina singola in AEM, l'app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Routing modello SPA{#spa-model-routing}

Per le applicazioni a pagina singola in AEM, l&#39;app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.

## Routing del progetto {#project-routing}

L&#39;app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il ciclo specifico per il modello restituito dal server AEM. La struttura dati del modello di pagina espone l&#39;URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di routing. Una volta che una route prevede un frammento di modello, è possibile effettuare una chiamata alla `PageModelManager.getData()` funzione. Quando un ciclo di lavorazione del modello ha modificato un evento deve essere attivato per avvertire le librerie di ascolto come Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, fare riferimento alla sezione [PageModelManager](blueprint.md#pagemodelmanager) del documento Blueprint SPA.

## ModelRouter {#modelrouter}

L&#39;API `ModelRouter` - se attivata - racchiude le funzioni API HTML5 History `pushState` e `replaceState` per garantire che un dato frammento di modello sia preacquisito e accessibile. Quindi, notifica al componente front-end registrato che il modello è stato modificato.

## Routing manuale e automatico del modello {#manual-vs-automatic-model-routing}

Il modello `ModelRouter` automatizza il recupero dei frammenti del modello. Ma come ogni attrezzo automatizzato è dotato di limitazioni. Se necessario, `ModelRouter` è possibile disabilitare o configurare in modo da ignorare i percorsi utilizzando le proprietà meta (vedere la sezione Meta Properties del documento del componente [pagina](page-component.md) SPA). Gli sviluppatori front-end possono quindi implementare un proprio livello di routing del modello richiedendo `PageModelManager` di caricare qualsiasi frammento del modello utilizzando la `getData()` funzione.

>[!CAUTION]
>
>La versione corrente dell&#39; `ModelRouter` unico supporto per l&#39;uso di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’uso di URL personalizzati o alias.

## Contratto di routing {#routing-contract}

L&#39;implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l&#39;API HTML5 History per il routing alle diverse pagine dell&#39;applicazione.

### Configurazione {#configuration}

Supporta `ModelRouter` il concetto di indirizzamento dei modelli in quanto ascolta `pushState` e `replaceState` richiama i frammenti dei modelli di preacquisizione. Internamente attiva la modalità `PageModelManager` di caricamento del modello che corrisponde a un determinato URL e attiva un `cq-pagemodel-route-changed` evento che può essere ascoltato da altri moduli.

Per impostazione predefinita, questo comportamento è attivato automaticamente. Per disattivarlo, il SPA deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Tenere presente che ogni route del SPA deve corrispondere a una risorsa accessibile in AEM (ad es., &quot; `/content/mysite/mypage"`), poiché `PageModelManager` cercherà automaticamente di caricare il modello di pagina corrispondente dopo che la route è selezionata. Anche se necessario, il SPA può anche definire un &quot;elenco Bloccati &quot; di route che deve essere ignorato dai `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
