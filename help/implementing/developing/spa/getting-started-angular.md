---
title: Guida introduttiva alle SPA in AEM Utilizzo di Angular
description: Questo articolo presenta un esempio SPA applicazione, spiega come viene messa insieme e consente di iniziare a usare rapidamente il proprio SPA utilizzando la cornice Angular.
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---


# Guida introduttiva alle SPA in AEM Utilizzo di Angular {#getting-started-with-spas-in-aem-using-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando SPA framework e gli autori desiderano modificare i contenuti all&#39;interno di AEM per un sito creato utilizzando SPA framework.

La funzione di authoring SPA offre una soluzione completa per SPA di supporto in AEM. Questo articolo presenta un&#39;applicazione SPA semplificata sul framework Angular, spiega come viene assemblato, consentendo di iniziare rapidamente a usare i propri SPA.

>[!NOTE]
>
>Questo articolo si basa sulla cornice angolare. Per il documento corrispondente per il framework React, consultate [Guida introduttiva alle SPA in AEM - React](getting-started-react.md)(Reazione).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un semplice SPA e il minimo che devi sapere per far funzionare il tuo.

Per maggiori dettagli sul funzionamento SPA in AEM, consulta i documenti seguenti:

* [Introduzione SPA e Procedura dettagliata](introduction.md)
* [Panoramica dell’editor SPA](editor-overview.md)
* [Blueprint SPA](blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori di AEM non sarà autorizzabile se non rispetta il contratto per il modello di contenuto.

Questo documento illustra la struttura di un SPA semplificato e illustra come funziona in modo da poter applicare questa comprensione ai propri SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza Angular prevista, il SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione del SPA.

### Dipendenze {#dependencies}

Il `package.json` file definisce i requisiti del pacchetto SPA complessivo. Le dipendenze AEM minime richieste sono elencate di seguito.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta creato, il pacchetto può essere caricato in un&#39;istanza AEM.

### AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l’SDK SPA.

## Struttura dell&#39;applicazione {#application-structure}

L&#39;inclusione delle dipendenze e la creazione dell&#39;app come descritto in precedenza vi lasceranno con un pacchetto SPA funzionante che potete caricare nell&#39;istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA in AEM, i file importanti che guidano l&#39;applicazione e la modalità di funzionamento dell&#39;applicazione.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione si basano sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nel SPA è il `app.module.ts` file mostrato qui semplificato per concentrarsi sul contenuto importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

Il `app.module.ts` file è il punto di partenza dell&#39;app e contiene la configurazione di progetto iniziale e viene utilizzato `AppComponent` per avviare l&#39;app.

#### Istanziazione statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente, il valore deve essere passato dal modello alle proprietà del componente. I valori del modello vengono passati come attributi per essere successivamente disponibili come proprietà del componente.

### app.component.ts {#app-component-ts}

Una volta `app.module.ts` avviati `AppComponent`, l&#39;app può quindi essere inizializzata, come illustrato in una versione semplificata per concentrarsi sul contenuto importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Elaborando la pagina, `app.component.ts` le chiamate elencate `main-content.component.ts` qui in una versione semplificata.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

Consente di `MainComponent` acquisire la rappresentazione JSON del modello di pagina ed elaborare il contenuto da racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli sul documento `Page` sono disponibili nel documento [SPA Blueprint](blueprint.md).

### image.component.ts {#image-component-ts}

Il componente `Page` è composto da componenti. Con l’assimilazione del JSON, il gruppo `Page` può elaborare tali componenti, come `image.component.ts` illustrato di seguito.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

L’idea centrale di SPA in AEM è la mappatura SPA componenti a componenti AEM e l’aggiornamento del componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [SPA Panoramica](editor-overview.md) dell&#39;editor.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

Il `MapTo` metodo mappa il componente SPA al componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce a abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi i segnaposto

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati in modo dinamico come proprietà del componente.

### image.component.html {#image-component-html}

Infine, l’immagine può essere riprodotta in `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione Di Informazioni Tra SPA Componenti {#sharing-information-between-spa-components}

È necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi consigliati di fare questo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzate la logica e la trasmissione ai componenti necessari, ad esempio utilizzando una classe util come soluzione orientata agli oggetti.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfruttare la gerarchia di oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

* [La Guida introduttiva alle SPA in AEM con React](getting-started-react.md) mostra come è stato creato un SPA di base per lavorare con l’Editor SPA in AEM con React.
* [SPA Editor Overview (Panoramica](editor-overview.md) dell’editor) approfondisce il modello di comunicazione tra AEM e SPA.
* [WKND SPA Project](wknd-tutorial.md) è un&#39;esercitazione passo-passo che implementa un semplice progetto SPA in AEM.
* [La mappatura dinamica da modello a componente per SPA](model-to-component-mapping.md) spiega il modello dinamico alla mappatura del componente e come funziona all&#39;interno SPA in AEM.
* [SPA Blueprint](blueprint.md) offre informazioni approfondite sul funzionamento dell’SDK SPA per AEM nel caso in cui desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente una comprensione più approfondita.
