---
title: Guida introduttiva alle app SPA in AEM Utilizzo di React
description: Questo articolo presenta un'applicazione SPA di esempio, spiega come viene assemblata e consente di iniziare a utilizzare rapidamente la propria SPA utilizzando la struttura React.
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# Guida introduttiva alle app SPA in AEM Utilizzo di React {#getting-started-with-spas-in-aem-using-react}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare i contenuti all&#39;interno AEM per un sito creato utilizzando i framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare gli SPA in AEM. Questo articolo presenta un&#39;applicazione SPA semplificata nel framework React, spiega come viene assemblata, consentendo di iniziare rapidamente a utilizzare la propria SPA.

>[!NOTE]
>
>Questo articolo si basa sul quadro di React. Per il documento corrispondente per il framework Angular, consulta [Guida introduttiva alle app SPA in AEM - Angular](getting-started-angular.md).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di una semplice SPA e il minimo che devi sapere per far funzionare il tuo.

Per maggiori dettagli sul funzionamento degli SPA in AEM, consulta i documenti seguenti:

* [Introduzione e introduzione SPA](introduction.md)
* [Panoramica di SPA Editor](editor-overview.md)
* [Blueprint SPA](blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un’app SPA, i contenuti devono essere memorizzati in AEM ed esposti mediante il modello di contenuti.
>
>Una SPA sviluppata al di fuori di AEM non sarà autorizzabile se non rispetta il contratto per i modelli di contenuto.

Questo documento illustra la struttura di un&#39;app SPA semplificata creata con la struttura React e illustra il suo funzionamento, in modo da poter applicare questa comprensione all&#39;SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza prevista dal programma React, l&#39;area SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione dell&#39;area SPA.

### Dipendenze {#dependencies}

Il `package.json` file definisce i requisiti del pacchetto SPA complessivo. Le dipendenze AEM minime per un&#39;app SPA funzionante sono elencate qui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Poiché questo esempio è basato sul quadro React, nel `package.json` file sono presenti due dipendenze specifiche di React:

```
 react
 react-dom
```

La funzione `aem-clientlib-generator` viene utilizzata per rendere automatica la creazione di librerie client nel processo di creazione.

`"aem-clientlib-generator": "^1.4.1",`

Maggiori dettagli sono disponibili [su GitHub qui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

Il file `aem-clientlib-generator` è configurato nel `clientlib.config.js` modo seguente.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Creazione di {#building}

In realtà, la creazione dell&#39;app si basa su [Webpack](https://webpack.js.org/) per la traslazione oltre al generatore aem-clientlib-generator per la creazione automatica della libreria client. Il comando build sarà quindi simile a:

`"build": "webpack && clientlib --verbose"`

Una volta creato, il pacchetto può essere caricato in un&#39;istanza AEM.

### AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK SPA.

## Struttura dell&#39;applicazione {#application-structure}

L&#39;inclusione delle dipendenze e la creazione dell&#39;app come descritto in precedenza vi lasceranno con un pacchetto SPA funzionante che potete caricare nell&#39;istanza AEM.

La sezione successiva di questo documento illustra la struttura di un&#39;app in AEM, i file importanti che guidano l&#39;applicazione e il modo in cui lavorano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione si basano sullo stesso concetto.

### index.js {#index-js}

Il punto di ingresso nell&#39;SPA è ovviamente il `index.js` file qui mostrato semplificato per concentrarsi sul contenuto importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La funzione principale di `index.js` è quella di sfruttare la `ReactDOM.render` funzione per determinare dove nel DOM inserire l&#39;applicazione.

Si tratta di un utilizzo standard di questa funzione, non univoco per questa app di esempio.

#### Istanziazione statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente (ad esempio, JSX), il valore deve essere passato dal modello alle proprietà del componente.

### App.js {#app-js}

Eseguendo il rendering dell&#39;app, `index.js` le chiamate `App.js`, che vengono visualizzate in una versione semplificata per concentrarvi sul contenuto importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` Serve principalmente a racchiudere i componenti principali che compongono l&#39;app. Il punto di ingresso di qualsiasi app è la pagina.

### Page.js {#page-js}

Mediante il rendering della pagina, `App.js` le chiamate elencate `Page.js` qui in una versione semplificata.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In questo esempio la `AppPage` classe si estende `Page`, che contiene i metodi di contenuto interno che possono essere utilizzati.

Consente di `Page` acquisire la rappresentazione JSON del modello di pagina ed elaborare il contenuto da racchiudere/decorare ogni elemento della pagina. Per maggiori informazioni, `Page` consulta il documento [SPA Blueprint.](blueprint.md)

### Image.js {#image-js}

Con la pagina sottoposta a rendering, è possibile eseguire il rendering dei componenti come `Image.js` mostrato qui.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

L&#39;idea centrale di SPA in AEM è la mappatura dei componenti SPA ai componenti AEM e l&#39;aggiornamento del componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, consulta Panoramica [sull’editor](editor-overview.md) SPA.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Il `MapTo` metodo mappa il componente SPA sul componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce a abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi i segnaposto

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati in modo dinamico come proprietà del componente.

## Esportazione di contenuti modificabili {#exporting-editable-content}

Potete esportare un componente e mantenerlo modificabile.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La `MapTo` funzione restituisce un risultato `Component` che è il risultato di una composizione che estende il contenuto fornito `PageClass` con i nomi e gli attributi di classe che consentono l&#39;authoring. Questo componente può essere esportato in un secondo momento per essere istanziato nella marcatura dell’applicazione.

Quando viene esportato utilizzando la `MapTo` o `withModel` le funzioni, il `Page` componente viene racchiuso con un `ModelProvider` componente che consente ai componenti standard di accedere alla versione più recente del modello di pagina o a una posizione precisa nel modello di pagina.

Per ulteriori informazioni, consultate il documento [](blueprint.md)SPA Blueprint.

>[!NOTE]
>
>Per impostazione predefinita, quando si utilizza la `withModel` funzione si riceve l’intero modello del componente.

## Condivisione delle informazioni tra i componenti SPA {#sharing-information-between-spa-components}

È necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi consigliati di fare questo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzate la logica e la trasmissione ai componenti necessari, ad esempio utilizzando React Context.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come Redux.
* **Opzione 3:** Sfruttare la gerarchia di oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

* [Guida introduttiva alle app SPA in AEM con Angular](getting-started-angular.md) mostra come è stata creata una piattaforma SPA di base per lavorare con l&#39;editor SPA in AEM con Angular.
* [SPA Editor Overview](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [WKND SPA Project](wknd-tutorial.md) è un&#39;esercitazione passo-passo che implementa un semplice progetto SPA in AEM.
* [La mappatura da modello dinamico a componente per gli SPA](model-to-component-mapping.md) spiega il modello dinamico alla mappatura dei componenti e come funziona all&#39;interno degli SPA in AEM.
* [SPA Blueprint](blueprint.md) offre informazioni approfondite sul funzionamento di SPA SDK per AEM nel caso in cui desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente una comprensione più approfondita.
