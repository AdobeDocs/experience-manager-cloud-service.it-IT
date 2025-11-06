---
title: Mappatura di un modello dinamico a un componente per SPA
description: Questo articolo descrive come si verifica il modello dinamico per la mappatura dei componenti in JavaScript SPA SDK for AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 4%

---


# Mappatura di un modello dinamico a un componente per SPA {#dynamic-model-to-component-mapping-for-spas}

Questo documento descrive come si verifica il modello dinamico per la mappatura dei componenti in JavaScript SPA SDK for AEM.

{{ue-over-spa}}

## Modulo ComponentMapping {#componentmapping-module}

Il modulo `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente all’applicazione a pagina singola di mappare i componenti front-end ai tipi di risorse AEM. Il modulo abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un campo `:type` che espone un tipo di risorsa AEM. Una volta montato, il componente front-end può eseguire il rendering utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

Per ulteriori informazioni sull&#39;analisi del modello e sull&#39;accesso al componente front-end del modello, consulta il documento [Blueprint SPA](blueprint.md).

Vedi anche il pacchetto npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Applicazione a pagina singola basata su modello {#model-driven-single-page-application}

Le applicazioni a pagina singola che utilizzano JavaScript SPA SDK per AEM sono basate su modelli:

1. I componenti front-end si registrano nell&#39;[archivio mappature componenti](#componentmapping-module).
1. Il [contenitore](blueprint.md#container), una volta fornito con un modello dal [provider di modelli](blueprint.md#the-model-provider), scorre il contenuto del modello (`:items`).

1. Se è presente una pagina, i relativi elementi secondari (`:children`) ottengono prima una classe di componente da [Mappatura componente](blueprint.md#componentmapping) e quindi creano un&#39;istanza.

## Inizializzazione app {#app-initialization}

Ogni componente viene esteso con le funzionalità di [`ModelProvider`](blueprint.md#the-model-provider). L&#39;inizializzazione assume pertanto la seguente forma generale:

1. Ogni provider di modelli si inizializza e ascolta le modifiche apportate al pezzo di modello che corrisponde al relativo componente interno.
1. [`PageModelManager`](blueprint.md#pagemodelmanager) deve essere inizializzato come rappresentato dal [flusso di inizializzazione](blueprint.md).

1. Una volta memorizzata, il gestore modelli della pagina restituisce il modello completo dell’app.
1. Questo modello viene quindi passato al componente principale front-end [Container](blueprint.md#container) dell&#39;applicazione.
1. I pezzi del modello vengono infine propagati a ogni singolo componente figlio.

![Inizializzazione modello app](assets/app-model-initialization.png)
