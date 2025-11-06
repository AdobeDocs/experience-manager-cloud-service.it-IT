---
title: Guida introduttiva alle applicazioni a pagina singola in AEM con Angular
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale con il framework Angular.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 7%

---


# Guida introduttiva alle applicazioni a pagina singola in AEM con Angular {#getting-started-with-spas-in-aem-using-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring di applicazioni a pagina singola offre una soluzione completa per il supporto di applicazioni a pagina singola in AEM. Questo articolo presenta un’applicazione SPA semplificata sul framework Angular, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale.

>[!NOTE]
>
>Questo articolo si basa sul framework Angular. Per il documento corrispondente per il framework React vedi [Guida introduttiva alle applicazioni a pagina singola in AEM - React](getting-started-react.md).

{{ue-over-spa}}

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di una semplice applicazione a pagina singola e il minimo che è necessario sapere per eseguire l’operazione.

Per ulteriori dettagli sul funzionamento delle applicazioni a pagina singola in AEM, consulta i seguenti documenti:

* [Introduzione alla SPA e procedura dettagliata](introduction.md)
* [Panoramica dell’editor di SPA](editor-overview.md)
* [Blueprint SPA](blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un’applicazione a pagina singola, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un’applicazione a pagina singola sviluppata al di fuori di AEM non sarà autorizzabile se non rispetta il contratto del modello di contenuto.

Questo documento illustra la struttura di un’applicazione a pagina singola semplificata e il suo funzionamento, consentendoti di applicare questa conoscenza all’applicazione a pagina singola.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza prevista da Angular, l’applicazione a pagina singola di esempio può utilizzare librerie aggiuntive per rendere più efficiente la creazione dell’applicazione a pagina singola.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze minime richieste da AEM sono elencate qui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

### Generazione in corso {#building}

In realtà, la creazione dell&#39;app utilizza [Webpack](https://webpack.js.org/) per la transpilazione oltre a aem-clientlib-generator per la creazione automatica della libreria client. Pertanto, il comando build sarà simile al seguente:

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta generato, il pacchetto può essere caricato in un’istanza di AEM.

### Archetipo di progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

Se includi le dipendenze e crei l’app come descritto in precedenza, riceverai un pacchetto di applicazioni a pagina singola funzionante che puoi caricare nell’istanza di AEM.

La sezione successiva di questo documento illustra come è strutturata un’applicazione a pagina singola in AEM, i file importanti che guidano l’applicazione e come funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nell&#39;applicazione a pagina singola è il file `app.module.ts` qui mostrato semplificato per concentrarsi sul contenuto importante.

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

Il file `app.module.ts` è il punto iniziale dell&#39;app e contiene la configurazione iniziale del progetto e utilizza `AppComponent` per avviare l&#39;app.

#### Creazione di istanze statiche {#static-instantiation}

Quando il componente viene creato in modo statico utilizzando la maschera del componente, il valore deve essere passato dal modello alle proprietà del componente. I valori del modello vengono passati come attributi, per poi essere disponibili come proprietà dei componenti.

### app.component.ts {#app-component-ts}

Una volta avviato `app.module.ts`, `AppComponent` può inizializzare l&#39;app, che viene qui mostrata in una versione semplificata per concentrarsi sul contenuto importante.

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

Elaborando la pagina, `app.component.ts` chiama `main-content.component.ts` elencato qui in una versione semplificata.

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

`MainComponent` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli su `Page` sono disponibili nel documento [Blueprint SPA](blueprint.md).

### image.component.ts {#image-component-ts}

`Page` è composto da componenti. Con il JSON acquisito, `Page` può elaborare tali componenti come `image.component.ts`, come mostrato qui.

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

L’idea centrale delle applicazioni a pagina singola in AEM è quella di mappare i componenti delle applicazioni a pagina singola ai componenti di AEM e di aggiornare il componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [Panoramica dell&#39;editor SPA](editor-overview.md).

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

Il metodo `MapTo` associa il componente SPA al componente AEM. Supporta l’utilizzo di una singola stringa o di un array di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di creazione di un componente fornendo i metadati necessari all&#39;editor per generare segnaposto

Se non è presente alcun contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà passate dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati dinamicamente come proprietà del componente.

### image.component.html {#image-component-html}

Infine, è possibile eseguire il rendering dell&#39;immagine in `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione di informazioni tra i componenti SPA {#sharing-information-between-spa-components}

La condivisione delle informazioni è regolarmente necessaria per i componenti di un’applicazione a pagina singola. Esistono diversi modi consigliati per farlo, elencati di seguito in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio, utilizzando una classe util come soluzione puramente orientata agli oggetti.
* **Opzione 2:** condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

* [La Guida introduttiva alle applicazioni a pagina singola in AEM con React](getting-started-react.md) mostra come un&#39;applicazione a pagina singola di base viene creata per funzionare con l&#39;editor di applicazioni a pagina singola in AEM con React.
* La [Panoramica dell’editor di SPA](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [Il progetto SPA WKND](wknd-tutorial.md) è un tutorial dettagliato sull&#39;implementazione di un semplice progetto SPA in AEM.
* [Mappatura da modello dinamico a componente per applicazioni a pagina singola](model-to-component-mapping.md) spiega il modello dinamico alla mappatura dei componenti e come funziona all&#39;interno delle applicazioni a pagina singola in AEM.
* [Blueprint per applicazioni a pagina singola](blueprint.md) offre informazioni approfondite sul funzionamento di SPA SDK per AEM nel caso in cui si desideri implementare SPA in AEM per un framework diverso da React o Angular o semplicemente desideri una comprensione più approfondita.
