---
title: Mappatura da modello dinamico a componente per SPA
description: In questo articolo viene descritto in che modo si verifica la mappatura del modello dinamico al componente nell’SDK Javascript SPA per AEM.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Mappatura da modello dinamico a componente per SPA {#dynamic-model-to-component-mapping-for-spas}

In questo documento viene descritto in che modo si verifica la mappatura del modello dinamico al componente nell’SDK Javascript SPA per AEM.

## Modulo di mappatura dei componenti {#componentmapping-module}

Il `ComponentMapping` modulo viene fornito come pacchetto NPM al progetto front-end. memorizza i componenti front-end e consente all’applicazione a pagina singola di mappare i componenti front-end sui tipi di risorse AEM. Questo consente una risoluzione dinamica dei componenti durante l&#39;analisi del modello JSON dell&#39;applicazione.

Ogni elemento presente nel modello contiene un `:type` campo che espone un tipo di risorsa AEM. Quando è montato, il componente front-end può eseguire il rendering utilizzando il frammento del modello ricevuto dalle librerie sottostanti.

Per ulteriori informazioni sull&#39;analisi dei modelli e sull&#39;accesso al modello dei componenti front-end, consultare il documento [SPA Blueprint](blueprint.md) .

Vedete anche il pacchetto npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Applicazione a pagina singola basata su modello {#model-driven-single-page-application}

Le applicazioni a pagina singola che sfruttano l’SDK Javascript SPA per AEM sono basate su modelli:

1. I componenti front-end si registrano nell’archivio [di mappatura dei](#componentmapping-module)componenti.
1. Quindi il [Contenitore](blueprint.md#container), una volta fornito con un modello dal fornitore [di](blueprint.md#the-model-provider)modelli, esegue un&#39;iterazione sul contenuto del modello (`:items`).

1. Nel caso di una pagina, i relativi elementi secondari (`:children`) ottengono prima una classe di componenti dalla mappatura [](blueprint.md#componentmapping) dei componenti e quindi la creano in un&#39;istanza.

## Inizializzazione app {#app-initialization}

Ogni componente viene esteso con le funzionalità del [`ModelProvider`](blueprint.md#the-model-provider). L&#39;inizializzazione assume pertanto la seguente forma generale:

1. Ogni provider di modelli si inizializza e ascolta le modifiche apportate al pezzo di modello che corrisponde al suo componente interno.
1. L&#39;inizializzazione [`PageModelManager`](blueprint.md#pagemodelmanager) deve essere rappresentata dal flusso [di](blueprint.md)inizializzazione.

1. Una volta memorizzato, il gestore modelli pagina restituisce il modello completo dell&#39;app.
1. Questo modello viene quindi passato al componente [Contenitore](blueprint.md#container) principale front-end dell’applicazione.
1. I pezzi del modello vengono infine propagati a ogni singolo componente secondario.

![Inizializzazione modello app](assets/app-model-initialization.png)
