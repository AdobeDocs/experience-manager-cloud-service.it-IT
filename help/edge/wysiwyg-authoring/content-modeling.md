---
title: Modellazione dei contenuti per l’authoring WYSIWYG con progetti Edge Delivery Services
description: Scopri come funziona la modellazione dei contenuti per l’authoring WYSIWYG con progetti Edge Delivery Services e come modellare i tuoi contenuti.
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: ht
source-wordcount: '2160'
ht-degree: 100%

---


# Modellazione dei contenuti per l’authoring WYSIWYG con progetti Edge Delivery Services {#content-modeling}

Scopri come funziona la modellazione dei contenuti per l’authoring WYSIWYG con progetti Edge Delivery Services e come modellare i tuoi contenuti.

## Prerequisiti {#prerequisites}

I progetti che utilizzano l’authoring WYSIWYG con Edge Delivery Services ereditano la maggior parte dei meccanismi di qualsiasi altro progetto di Edge Delivery Services, indipendentemente dall’origine dei contenuti o dal [metodo di authoring](/help/edge/wysiwyg-authoring/authoring.md).

Prima di iniziare a modellare il contenuto per il progetto, assicurati di aver letto la seguente documentazione.

* [Guida introduttiva: tutorial per sviluppatori](/help/edge/developer/tutorial.md)
* [Markup, sezioni, blocchi e blocco automatico](/help/edge/developer/markup-sections-blocks.md)
* [Bloccare una raccolta](/help/edge/developer/block-collection.md)

È essenziale comprendere tali concetti per trovare un modello di contenuto convincente che funzioni in modo indipendente dall’origine dei contenuti. Questo documento fornisce dettagli sui meccanismi implementati specificamente per l’authoring WYSIWYG.

## Contenuto predefinito {#default-content}

Il **contenuto predefinito** sono gli elementi che un autore può inserire in modo intuitivo in una pagina senza aggiungere alcuna ulteriore semantica. Sono inclusi testo, intestazioni, collegamenti e immagini. La funzione e lo scopo di tale contenuto sono auto-esplicativi.

In AEM, questo contenuto viene implementato come componenti con modelli predefiniti molto semplici, che includono tutto ciò che può essere serializzato nel markdown e in HTML.

* **Testo**: testo formattato (inclusi gli elementi dell’elenco e testo forte o in corsivo)
* **Titolo**: testo, tipo (h1-h6)
* **Immagine**: origine, descrizione
* **Pulsante**: testo, titolo, URL, tipo (predefinito, primario, secondario)

Il modello di questi componenti fa parte degli [standard per l’authoring WYSIWYG con Edge Delivery Services](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112).

## Blocchi {#blocks}

I blocchi vengono utilizzati per creare contenuti più complessi con stili e funzionalità specifici. A differenza del contenuto predefinito, i blocchi richiedono una semantica aggiuntiva.

I blocchi sono essenzialmente parti di contenuto arricchite da JavaScript e formattate con un foglio di stile.

### Definizione modello del blocco {#model-definition}

Quando si utilizza l’authoring WYSIWYG con Edge Delivery Services, il contenuto dei blocchi deve essere modellato esplicitamente per fornire all’autore l’interfaccia per la creazione dei contenuti. In sostanza, è necessario creare un modello in modo che l’interfaccia utente di authoring sappia quali opzioni presentare all’autore in base al blocco.

Il file [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) definisce il modello dei blocchi. I campi definiti nel modello del componente vengono mantenuti come proprietà in AEM e sottoposti a rendering come celle nella tabella che costituisce un blocco.

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

Tieni presente che non tutti i blocchi devono avere un modello. Alcuni blocchi sono semplicemente [contenitori](#container) per un elenco di elementi secondari, in cui ognuno di essi ha un proprio modello.

È inoltre necessario definire quali blocchi esistono e possono essere aggiunti a una pagina utilizzando l’Editor universale. Il file [`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) elenca i componenti man mano che vengono resi disponibili dall’Editor universale.

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

È possibile utilizzare un modello per diversi blocchi. Ad esempio, alcuni blocchi possono condividere un modello che definisce un testo e un’immagine.

Per ogni blocco, lo sviluppatore:

* deve utilizzare il tipo di risorsa `core/franklin/components/block/v1/block`, l’implementazione generica della logica di blocco in AEM;
* deve definire il nome del blocco, che verrà sottoposto a rendering nell’intestazione della tabella del blocco;
   * Il nome del blocco viene utilizzato per recuperare lo stile e lo script corretti per decorare il blocco.
* Può definire un [ID modello](/help/implementing/universal-editor/field-types.md#model-structure).
   * L’ID modello è un riferimento al modello del componente, che definisce i campi disponibili per l’autore nel pannello delle proprietà.
* Può definire un [ID filtro](/help/implementing/universal-editor/filtering.md).
   * L’ID filtro è un riferimento al filtro del componente che consente di modificare il comportamento di authoring, ad esempio limitando quali elementi secondari possono essere aggiunti al blocco o alla sezione o quali funzioni dell’editor Rich Text sono abilitate.

Tutte queste informazioni vengono memorizzate in AEM quando un blocco viene aggiunto a una pagina. Se manca il tipo di risorsa o il nome del blocco, il blocco non verrà riprodotto sulla pagina.

>[!WARNING]
>
>Sebbene sia possibile, non è necessario, né consigliato implementare componenti AEM personalizzati. I componenti per Edge Delivery Services forniti da AEM sono sufficienti e offrono alcuni guardrail per facilitare lo sviluppo.
>
>I componenti forniti da AEM restituiscono un markup che può essere utilizzato da [helix-html2md](https://github.com/adobe/helix-html2md) durante la pubblicazione su Edge Delivery Services e da [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) durante il caricamento di una pagina nell’Editor universale. Il markup è il contratto stabile tra AEM e le altre parti del sistema e non consente personalizzazioni. Per questo motivo, i progetti non devono modificare i componenti, né utilizzare componenti personalizzati.

### Struttura del blocco {#block-structure}

Le proprietà dei blocchi sono [definite nei modelli di componenti](#model-definition) e persistevano in quanto tali in AEM. Le proprietà vengono sottoposte a rendering come celle nella struttura di tipo tabella del blocco.

#### Blocchi semplici {#simple}

Nella forma più semplice, un blocco esegue il rendering di ogni proprietà in una singola riga/colonna nell’ordine in cui sono definite nel modello.

Nell’esempio seguente, l’immagine viene definita prima nel modello e poi nel testo. Viene quindi eseguito il rendering prima dell’immagine e poi del testo.

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB Markup]

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

>[!TAB Tabella]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

Noterai che alcuni tipi di valori consentono di dedurre la semantica nel markup e che le proprietà vengono combinate in celle singole. Questo comportamento è descritto nella sezione [Tipo di inferenza](#type-inference).

#### Blocco chiave-valore {#key-value}

In molti casi, si consiglia di arricchire il markup semantico sottoposto a rendering, aggiungere nomi di classi CSS, aggiungere nuovi nodi o spostarli nel DOM e applicare stili.

In altri casi, tuttavia, il blocco viene letto come una configurazione di tipo coppia chiave-valore.

Un esempio sono i [metadati della sezione](/help/edge/developer/markup-sections-blocks.md#sections). In questo caso d’uso, il blocco può essere configurato per eseguire il rendering come tabella di coppia chiave-valore. Per ulteriori informazioni, consulta la sezione [Sezioni e metadati della sezione](#sections-metadata).

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

>[!TAB Markup]

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

>[!TAB Tabella]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### Blocchi contenitore {#container}

Entrambe le strutture precedenti hanno una singola dimensione: l’elenco delle proprietà. I blocchi contenitore consentono di aggiungere elementi secondari (di solito dello stesso tipo o modello) e sono quindi bidimensionali. Questi blocchi supportano ancora le relative proprietà sottoposte a rendering come righe con una singola colonna. Tuttavia, consentono anche di aggiungere elementi secondari, per i quali ogni elemento viene riprodotto come riga e ogni proprietà come colonna all’interno di tale riga.

Nell’esempio seguente, un blocco accetta un elenco di icone collegate come elementi secondari, dove ogni icona collegata ha un’immagine e un collegamento. Osserva l’[ID filtro](/help/implementing/universal-editor/filtering.md) impostato nei dati del blocco per fare riferimento alla configurazione del filtro.

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

>[!TAB Markup]

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

>[!TAB Tabella]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### Creazione di modelli di contenuto semantico per blocchi {#creating-content-models}

Con le [spiegazioni sulle meccaniche della struttura del blocco](#block-structure), è possibile creare un modello di contenuto che mappa uno a uno al livello di distribuzione i contenuti persistenti in AEM.

All’inizio di ogni progetto, è necessario prendere in considerazione attentamente un modello di contenuto per ogni blocco. Deve essere indipendente dall’origine del contenuto e dall’esperienza di authoring per consentire agli autori di passare a un’altra origine o di combinarle riutilizzando al contempo le implementazioni e gli stili dei blocchi. Maggiori dettagli e indicazioni generali sono disponibili nel [modello di David (seconda versione)](https://www.aem.live/docs/davidsmodel). In particolare, la [raccolta blocchi](/help/edge/developer/block-collection.md) contiene un ampio set di modelli di contenuto per casi d’uso specifici con modelli di interfaccia utente comuni.

Per quanto riguarda l’authoring WYSIWYG con Edge Delivery Services, questo solleva la questione della modalità di distribuzione di un modello di contenuto semantico coinvolgente quando le informazioni vengono create con moduli composti da più campi invece che con la modifica del markup semantico in un contesto come il testo in formato RTF.

Per risolvere questo problema, esistono tre metodi che facilitano la creazione di un modello di contenuto convincente:

* [Inferenza tipo](#type-inference)
* [Comprimi campo](#field-collapse)
* [Raggruppamento elementi](#element-grouping)

>[!NOTE]
>
>Le implementazioni di blocco possono destrutturare il contenuto e sostituire il blocco con un DOM sottoposto a rendering lato client. Anche se tale pratica è possibile e intuitiva per uno sviluppatore, non è la best practice per Edge Delivery Services.

#### Inferenza tipo {#type-inference}

Per alcuni valori possiamo dedurre il significato semantico dagli stessi. Tali valori includono:

* **Immagini**: se un riferimento a una risorsa in AEM è una risorsa di tipo MIME che inizia con `image/`, il riferimento viene sottoposto a rendering come `<picture><img src="${reference}"></picture>`.
* **Collegamenti**: se esiste un riferimento in AEM e non è un’immagine, o se il valore inizia con `https?://` o `#`, il riferimento viene sottoposto a rendering come `<a href="${reference}">${reference}</a>`.
* **Rich Text**: se un valore troncato inizia con un paragrafo (`p`, `ul`, `ol`, `h1`-`h6`, ecc.), il valore viene sottoposto a rendering come testo RTF.
* **Nomi di classe**: la proprietà `classes` viene trattata come [opzioni di blocco](/help/edge/developer/markup-sections-blocks.md#block-options) e ne viene eseguito il rendering nell’intestazione della tabella per [blocchi semplici](#simple) o come elenco valore per gli elementi in un [blocco contenitore](#container). È utile se desideri [applicare uno stile diverso a un blocco](/help/edge/wysiwyg-authoring/create-block.md#block-options), ma non è necessario creare un blocco completamente nuovo.
* **Elenchi valore**: se un valore è una proprietà con più valori e il primo valore non è nessuno dei precedenti, tutti i valori vengono concatenati come elenco separato da virgole.

Tutto il resto verrà riprodotto come testo normale.

#### Comprimi campo {#field-collapse}

La compressione del campo è il meccanismo che consente di combinare più valori di campo in un singolo elemento semantico basato su una convenzione di denominazione che utilizza i suffissi `Title`, `Type`, `MimeType`, `Alt` e `Text` (con distinzione maiuscole/minuscole). Qualsiasi proprietà che termina con uno qualsiasi di questi suffissi non sarà considerata un valore, ma piuttosto un attributo di un’altra proprietà.

##### Immagini {#image-collapse}

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB Markup]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB Tabella]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### Collegamenti e pulsanti {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB Markup]

No `linkType` o `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

>[!TAB Tabella]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### Titoli {#headings-collapse}

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB Markup]

```html
<h2>Getting started</h2>
```

>[!TAB Tabella]

```text
## Getting started
```

>[!ENDTABS]

#### Raggruppamento elementi {#element-grouping}

Mentre la [compressione campo](#field-collapse) riguarda la combinazione di più proprietà in un singolo elemento semantico, il raggruppamento di elementi riguarda la concatenazione di più elementi semantici in una singola cella. Ciò è particolarmente utile per i casi d’uso in cui l’autore deve essere limitato nel tipo e nel numero di elementi che può creare.

Ad esempio, un componente teaser permette all’autore di creare solo un sottotitolo, un titolo e una singola descrizione di paragrafo combinati con un massimo di due pulsanti di invito all’azione. Raggruppando questi elementi insieme si ottiene un markup semantico a cui è possibile applicare uno stile senza ulteriori azioni.

Il raggruppamento di elementi utilizza una convenzione di denominazione, in cui il nome del gruppo è separato da ogni proprietà del gruppo da trattino basso. La compressione del campo delle proprietà in un gruppo funziona come descritto in precedenza.

>[!BEGINTABS]

>[!TAB Dati]

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

>[!TAB Markup]

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

>[!TAB Tabella]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## Sezioni e metadati della sezione {#sections-metadata}

Allo stesso modo in cui uno sviluppatore può definire e modellare più [blocchi](#blocks), si possono definire sezioni diverse.

Il modello di contenuto di Edge Delivery Services consente deliberatamente un solo livello di nidificazione, ovvero qualsiasi contenuto o blocco predefinito contenuto in una sezione. Ciò significa che per avere componenti visivi più complessi che possono contenere altri componenti, devono essere modellati come sezioni e combinati utilizzando il blocco automatico lato-client. Esempi tipici di ciò sono le schede e le sezioni comprimibili come i pannelli a soffietto.

Una sezione può essere definita nello stesso modo di un blocco, ma con il tipo di risorsa `core/franklin/components/section/v1/section`. Le sezioni possono avere un nome e un [ID filtro](/help/implementing/universal-editor/filtering.md), utilizzati soltanto dall’[editor universale](/help/implementing/universal-editor/introduction.md), nonché un [ID modello](/help/implementing/universal-editor/field-types.md#model-structure), utilizzato per eseguire il rendering dei metadati della sezione. Il modello è in questo modo il modello del blocco di metadati della sezione, che verrà automaticamente aggiunto a una sezione come blocco di valore-chiave, se non è vuoto.

L’[ID modello](/help/implementing/universal-editor/field-types.md#model-structure) e l’[ID filtro](/help/implementing/universal-editor/filtering.md) della sezione predefinita è `section`. Può essere utilizzato per modificare il comportamento della sezione predefinita. L’esempio seguente aggiunge alcuni stili e un’immagine di sfondo al modello di metadati della sezione.

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

L’esempio che segue definisce una sezione della scheda, che può essere utilizzata per creare un blocco di schede combinando sezioni consecutive con un attributo di dati del titolo della scheda in un blocco di schede durante il blocco automatico.

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## Metadati pagina {#page-metadata}

I documenti possono avere un [blocco di metadati](https://www.aem.live/developer/block-collection/metadata) della pagina, utilizzato per definire quali elementi `<meta>` vengono sottoposti a rendering nel `<head>` di una pagina. Le proprietà di pagina delle pagine in AEM as a Cloud Service corrispondono a quelle disponibili come predefinite per Edge Delivery Services, come `title`, `description`, `keywords`, ecc.

Prima di approfondire la definizione dei metadati, consulta i seguenti documenti, per comprendere il concetto di metadati della pagina.

* [Metadati](https://www.aem.live/developer/block-collection/metadata)
* [Metadati in blocco](/help/edge/docs/bulk-metadata.md)

È possibile inoltre definire metadati di pagina aggiuntivi in due modi.

### Fogli di calcolo metadati {#metadata-spreadsheets}

In AEM as a Cloud Service, è possibile definire i metadati per percorso o per modello di percorso in modo simile a una tabella. È disponibile un’interfaccia utente di authoring per i dati simili a tabelle simile a quella di Excel o Fogli Google.

Per ulteriori dettagli, consulta il documento [Utilizzo dei fogli di calcolo per gestire i dati tabulari](/help/edge/wysiwyg-authoring/tabular-data.md).

### Proprietà pagina {#page-properties}

Molte delle proprietà di pagina predefinite disponibili in AEM sono mappate ai rispettivi metadati di pagina in un documento. Ciò include, ad esempio `title`, `description`, `robots`, `canonical url` o `keywords`. Sono disponibili anche alcune proprietà specifiche per AEM:

* `cq:lastModified` come `modified-time` in formato ISO8601
* Ora dell’ultima pubblicazione del documento come `published-time` in formato ISO8601
* `cq:tags` come `cq-tags` come elenco separato da virgole degli ID dei tag.

È possibile inoltre definire un modello di componente per i metadati della pagina personalizzati, che verrà reso disponibile all’autore nell’editor universale.

A tale scopo, crea un modello di componente con ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

## Passaggi successivi {#next-steps}

Ora che sai come modellare i contenuti, con il progetto di authoring WYSIWYG puoi creare blocchi per i tuoi Edge Delivery Services.

Consulta il documento [Creazione di blocchi abilitati all’utilizzo con l’editor universale](/help/edge/wysiwyg-authoring/create-block.md) per scoprire come creare blocchi abilitati all’utilizzo con l’editor universale nell’authoring WYSIWYG con progetti Edge Delivery Services.

Se hai già familiarità con la creazione di blocchi, consulta il documento [Guida introduttiva per gli sviluppatori per l’authoring WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) per iniziare a utilizzare un nuovo sito Adobe Experience Manager con Edge Delivery Services e l’editor universale per l’authoring dei contenuti.
