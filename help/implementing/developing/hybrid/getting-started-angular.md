---
title: Guida introduttiva a SPA in AEM Utilizzo di Angular
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene assemblato e ti consente di iniziare rapidamente a usare il tuo SPA utilizzando il framework di Angular.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 4%

---

# Guida introduttiva a SPA in AEM Utilizzo di Angular {#getting-started-with-spas-in-aem-using-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare SPA all’interno di AEM. Questo articolo presenta un&#39;applicazione SPA semplificata sul framework di Angular, spiega come viene messo insieme, che ti permette di iniziare a lavorare rapidamente con il tuo SPA.

>[!NOTE]
>
>Questo articolo si basa sul quadro Angular. Per il documento corrispondente per il quadro React vedi [Guida introduttiva a SPA in AEM - React](getting-started-react.md).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un SPA semplice e il minimo che devi sapere per far funzionare il tuo.

Per ulteriori dettagli sul funzionamento SPA in AEM, consulta i seguenti documenti:

* [Introduzione a SPA e procedura dettagliata](introduction.md)
* [Panoramica dell’editor di SPA](editor-overview.md)
* [Blueprint SPA](blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori di AEM non sarà autorizzabile se non rispetta il contratto relativo al modello di contenuto.

Questo documento illustra la struttura di un SPA semplificato e illustra come funziona in modo da poter applicare questa comprensione al proprio SPA.

## Dipendenze, configurazione e creazione {#dependencies-configuration-and-building}

Oltre alla dipendenza prevista dall’Angular, l’SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione dell’SPA.

### Dipendenze {#dependencies}

La `package.json` Il file definisce i requisiti del pacchetto SPA globale. Le dipendenze AEM minime richieste sono elencate qui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

La `aem-clientlib-generator` viene sfruttato per rendere automatica la creazione di librerie client come parte del processo di compilazione.

`"aem-clientlib-generator": "^1.4.1",`

Maggiori dettagli sono disponibili [su GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

La `aem-clientlib-generator` è configurato in `clientlib.config.js` file come segue.

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

In realtà, la creazione di app sfrutta [Webpack](https://webpack.js.org/) per la trasformazione in aggiunta al generatore aem-clientlib-per la creazione automatica della libreria client. Pertanto, il comando di compilazione sarà simile a:

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta generato, il pacchetto può essere caricato in un&#39;istanza AEM.

### Archetipo progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve sfruttare [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

L’inclusione delle dipendenze e la creazione dell’app come descritto in precedenza ti lasceranno con un pacchetto di SPA funzionante che puoi caricare nella tua istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA in AEM, i file importanti che guidano l&#39;applicazione e il modo in cui funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nel SPA è il `app.module.ts` il file mostrato qui è stato semplificato per concentrarsi sul contenuto importante.

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

La `app.module.ts` è il punto iniziale dell’app e contiene la configurazione iniziale del progetto e utilizza `AppComponent` per avviare l&#39;app.

#### Istanza statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente, il valore deve essere trasmesso dal modello alle proprietà del componente. I valori del modello vengono passati come attributi per essere successivamente disponibili come proprietà del componente.

### app.component.ts {#app-component-ts}

Una volta `app.module.ts` bootstrap `AppComponent`, può quindi inizializzare l’app, che viene visualizzata qui in una versione semplificata per concentrarti sul contenuto importante.

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

Elaborando la pagina, `app.component.ts` chiama `main-content.component.ts` elencati in una versione semplificata.

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

La `MainComponent` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Maggiori dettagli `Page` disponibile nel documento [Blueprint SPA](blueprint.md).

### image.component.ts {#image-component-ts}

La `Page` è composto da componenti. Con il JSON acquisito, il `Page` può elaborare componenti quali `image.component.ts` come mostrato qui.

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

L’idea centrale di SPA in AEM è quella di mappare SPA componenti ai componenti AEM e aggiornare il componente quando il contenuto viene modificato (e viceversa). Vedere il documento [Panoramica dell’editor di SPA](editor-overview.md) per una sintesi di questo modello di comunicazione.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

La `MapTo` mappa il componente SPA al componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi segnaposti

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono trasmessi dinamicamente come proprietà del componente.

### image.component.html {#image-component-html}

Infine, è possibile eseguire il rendering dell&#39;immagine `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione Di Informazioni Tra I Componenti SPA {#sharing-information-between-spa-components}

È regolarmente necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi raccomandati per farlo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzare la logica e la trasmissione ai componenti necessari, ad esempio utilizzando una classe util come soluzione puramente orientata agli oggetti.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore .

## Passaggi successivi {#next-steps}

* [Guida introduttiva a SPA in AEM utilizzando React](getting-started-react.md) mostra come viene creata una SPA di base per lavorare con l’editor di SPA in AEM utilizzando React.
* [Panoramica dell’editor di SPA](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [Progetto SPA WKND](wknd-tutorial.md) è un tutorial dettagliato che implementa un semplice progetto SPA in AEM.
* [Mappatura dinamica da modello a componente per SPA](model-to-component-mapping.md) spiega il modello dinamico alla mappatura dei componenti e come funziona all’interno di SPA in AEM.
* [Blueprint SPA](blueprint.md) offre informazioni approfondite sul funzionamento dell’SDK SPA per AEM nel caso in cui desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente una comprensione più approfondita.
