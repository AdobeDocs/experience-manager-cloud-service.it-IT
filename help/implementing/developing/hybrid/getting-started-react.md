---
title: Guida introduttiva dell’SPA nell’AEM con React
description: Questo articolo illustra un esempio di applicazione per l’SPA, spiega come viene creata e come iniziare a utilizzare il proprio SPA in modo rapido utilizzando il framework React.
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 6%

---

# Guida introduttiva dell’SPA nell’AEM con React {#getting-started-with-spas-in-aem-using-react}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno dell’AEM per un sito creato utilizzando framework SPA.

La funzione di authoring dell’SPA offre una soluzione completa per il supporto dell’SPA nell’ambito dell’AEM. Questo articolo presenta un’applicazione SPA semplificata sul framework React, spiega come viene creato e come iniziare a utilizzare il proprio SPA in modo rapido.

>[!NOTE]
>
>Questo articolo si basa sul framework React. Per il documento corrispondente per il framework Angular, vedi [Guida introduttiva all&#39;SPA nell&#39;AEM - Angular](getting-started-angular.md).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un semplice SPA e il minimo che è necessario sapere per rendere il vostro funzionamento.

Per maggiori dettagli sul funzionamento dell’SPA nell’AEM, consulta i seguenti documenti:

* [Introduzione alla SPA e procedura dettagliata](introduction.md)
* [Panoramica dell’editor di SPA](editor-overview.md)
* [Blueprint SPA](blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, questi devono essere memorizzati nell’AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori dell&#39;AEM non sarà credibile se non rispetta il contratto tipo di contenuto.

Questo documento illustra la struttura di un SPA semplificato creato utilizzando il framework React e il suo funzionamento, per consentirti di applicare questa conoscenza al tuo SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla prevista dipendenza da React, l&#39;SPA di esempio può utilizzare librerie aggiuntive per rendere più efficiente la creazione dell&#39;SPA.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze minime dell’AEM per un SPA funzionante sono elencate qui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Poiché questo esempio si basa sul framework React, nel file `package.json` sono obbligatorie due dipendenze specifiche di React:

```
 react
 react-dom
```

`aem-clientlib-generator` viene utilizzato per rendere automatica la creazione di librerie client come parte del processo di compilazione.

`"aem-clientlib-generator": "^1.4.1",`

Per ulteriori dettagli vedi [aem-clientlib-generator su GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

`aem-clientlib-generator` è configurato nel file `clientlib.config.js` come segue.

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

### Generazione in corso {#building}

In realtà, la creazione dell&#39;app utilizza [Webpack](https://webpack.js.org/) per la transpilazione oltre a aem-clientlib-generator per la creazione automatica della libreria client. Pertanto, il comando build sarà simile al seguente:

`"build": "webpack && clientlib --verbose"`

Una volta generato, il pacchetto può essere caricato in un’istanza AEM.

### Archetipo progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

L’inclusione delle dipendenze e la creazione dell’app come descritto in precedenza ti lasceranno con un pacchetto SPA funzionante che puoi caricare nell’istanza AEM.

La sezione successiva di questo documento illustra come è strutturato un SPA nell’AEM, i file importanti che guidano l’applicazione e come funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### index.js {#index-js}

Il punto di ingresso nell&#39;SPA è il file `index.js` qui mostrato semplificato per concentrarsi sul contenuto importante.

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

La funzione principale di `index.js` consiste nell&#39;utilizzare la funzione `ReactDOM.render` per determinare dove inserire l&#39;applicazione nel DOM.

Si tratta di un utilizzo standard di questa funzione, non specifico di questa app di esempio.

#### Creazione di istanze statiche {#static-instantiation}

Quando il componente viene creato in modo statico utilizzando il modello di componente (ad esempio, JSX), il valore deve essere trasmesso dal modello alle proprietà del componente.

### App.js {#app-js}

Tramite il rendering dell&#39;app, `index.js` chiama `App.js`, che viene mostrato qui in una versione semplificata per concentrarsi sul contenuto importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` serve principalmente per eseguire il wrapping dei componenti radice che compongono l&#39;app. Il punto di ingresso di qualsiasi app è la pagina.

### Page.js {#page-js}

Tramite il rendering della pagina, `App.js` chiama `Page.js` elencato qui in una versione semplificata.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In questo esempio la classe `AppPage` estende `Page`, che contiene i metodi di contenuto interno che possono quindi essere utilizzati.

`Page` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli su `Page` sono disponibili nel documento [Blueprint SPA.](blueprint.md)

### Image.js {#image-js}

Con il rendering della pagina, è possibile eseguire il rendering dei componenti come `Image.js`, come mostrato di seguito.

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

L&#39;idea centrale dell&#39;SPA nell&#39;AEM è l&#39;idea di mappare i componenti dell&#39;SPA ai componenti dell&#39;AEM e di aggiornare il componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [Panoramica dell&#39;editor SPA](editor-overview.md).

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Il metodo `MapTo` mappa il componente SPA al componente AEM. Supporta l’utilizzo di una singola stringa o di un array di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di creazione di un componente fornendo i metadati necessari all&#39;editor per generare segnaposto

Se non è presente alcun contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà passate dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati dinamicamente come proprietà del componente.

## Esportazione di contenuti modificabili {#exporting-editable-content}

Puoi esportare un componente e mantenerlo modificabile.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La funzione `MapTo` restituisce un `Component` che è il risultato di una composizione che estende il `PageClass` fornito con i nomi e gli attributi della classe che abilitano l&#39;authoring. Questo componente può essere esportato in un secondo momento e istanziato nel markup dell’applicazione.

Quando viene esportato utilizzando le funzioni `MapTo` o `withModel`, il componente `Page` è racchiuso in un componente `ModelProvider` che fornisce l&#39;accesso ai componenti standard alla versione più recente del modello di pagina o a una posizione precisa nel modello di pagina.

Per ulteriori informazioni, consulta il [documento Blueprint per SPA](blueprint.md).

>[!NOTE]
>
>Per impostazione predefinita, quando si utilizza la funzione `withModel` si riceve l&#39;intero modello del componente.

## Condivisione di informazioni tra i componenti dell’SPA {#sharing-information-between-spa-components}

La condivisione delle informazioni è regolarmente necessaria per i componenti di un’applicazione a pagina singola. Esistono diversi modi consigliati per farlo, elencati di seguito in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio, utilizzando React Context.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come Redux.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

* [La Guida introduttiva all&#39;SPA nell&#39;AEM mediante l&#39;Angular](getting-started-angular.md) mostra come un SPA di base viene creato per funzionare con l&#39;editor SPA nell&#39;AEM mediante l&#39;Angular.
* La [Panoramica dell’editor di SPA](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [Progetto WKND SPA](wknd-tutorial.md) è un&#39;esercitazione passo passo che implementa un semplice progetto SPA nell&#39;AEM.
* [Mappatura dinamica da modello a componente per SPA](model-to-component-mapping.md) spiega il modello dinamico alla mappatura dei componenti e come funziona all&#39;interno dell&#39;SPA nell&#39;AEM.
* [Blueprint SPA](blueprint.md) offre informazioni approfondite sul funzionamento dell&#39;SDK SPA per AEM nel caso in cui si desideri implementare l&#39;SPA in AEM per un framework diverso da React o Angular o semplicemente desideri una comprensione più approfondita.
