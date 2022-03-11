---
title: Mappatura dinamica da modello a componente per SPA
description: Questo articolo descrive come avviene la mappatura del modello dinamico ai componenti nell'SDK Javascript SPA per AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Mappatura dinamica da modello a componente per SPA {#dynamic-model-to-component-mapping-for-spas}

Questo documento descrive come avviene la mappatura del modello dinamico ai componenti nell&#39;SDK Javascript SPA per AEM.

## Modulo di mappatura componenti {#componentmapping-module}

La `ComponentMapping` Il modulo viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente all’applicazione a pagina singola di mappare i componenti front-end sui tipi di risorse AEM. In questo modo si abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un `:type` campo che espone un tipo di risorsa AEM. Quando è montato, il componente front-end può renderizzarsi utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

Fai riferimento alla [Blueprint SPA](blueprint.md) per ulteriori informazioni sull&#39;analisi dei modelli e sull&#39;accesso al modello dei componenti front-end.

Vedi anche il pacchetto npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Applicazione a pagina singola basata su modello {#model-driven-single-page-application}

Le applicazioni a pagina singola che sfruttano l’SDK SPA Javascript per AEM sono basate su modelli:

1. I componenti front-end si registrano al [Archivio di mappatura dei componenti](#componentmapping-module).
1. Quindi il [Contenitore](blueprint.md#container)una volta fornito con un modello [Provider di modelli](blueprint.md#the-model-provider), esegue iterazioni sul contenuto del modello (`:items`).

1. Nel caso di una pagina, i relativi elementi secondari (`:children`) per prima cosa, ottieni una classe di componente dal [Mappatura dei componenti](blueprint.md#componentmapping) e poi istanziarlo.

## Inizializzazione app {#app-initialization}

Ogni componente viene esteso con le funzionalità del [`ModelProvider`](blueprint.md#the-model-provider). L&#39;inizializzazione assume pertanto la seguente forma generale:

1. Ogni provider di modelli si inizializza e ascolta le modifiche apportate al pezzo di modello che corrisponde al suo componente interno.
1. La [`PageModelManager`](blueprint.md#pagemodelmanager) deve essere inizializzato come rappresentato dal [flusso di inizializzazione](blueprint.md).

1. Una volta memorizzato, il gestore dei modelli di pagina restituisce il modello completo dell’app.
1. Questo modello viene quindi trasmesso alla radice front-end [Contenitore](blueprint.md#container) componente dell&#39;applicazione.
1. I pezzi del modello vengono infine propagati a ogni singolo componente figlio.

![Inizializzazione del modello di app](assets/app-model-initialization.png)
