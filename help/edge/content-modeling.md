---
title: Modellazione dei contenuti per la creazione di AEM con progetti Edge Delivery Services
description: Scopri come funziona la modellazione dei contenuti per l’authoring AEM con progetti di Edge Delivery Services e come modellare i tuoi contenuti.
source-git-commit: 8f3c7524ae8ee642a9aee5989e03e6584a664eba
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 1%

---


# Modellazione dei contenuti per la creazione di AEM con progetti Edge Delivery Services {#content-modeling}

Scopri come funziona la modellazione dei contenuti per l’authoring AEM con progetti di Edge Delivery Services e come modellare i tuoi contenuti.

{{aem-authoring-edge-early-access}}

## Prerequisiti {#prerequisites}

I progetti che utilizzano l’authoring AEM con i Edge Delivery Services ereditano la maggior parte dei meccanismi di qualsiasi altro progetto di Edge Delivery Services, indipendentemente dall’origine dei contenuti o [metodo di authoring.](/help/edge/authoring.md)

Prima di iniziare a modellare il contenuto per il progetto, assicurati di aver letto la seguente documentazione.

* [Guida introduttiva: tutorial per sviluppatori](/help/edge/developer/tutorial.md)
* [Markup, sezioni, blocchi e blocco automatico](/help/edge/developer/markup-sections-blocks.md)
* [Bloccare una raccolta](/help/edge/developer/block-collection.md)

È essenziale comprendere tali concetti per trovare un modello di contenuto convincente che funzioni in modo indipendente dall’origine dei contenuti. Questo documento fornisce dettagli sui meccanismi implementati specificamente per la creazione di AEM.

## Contenuto predefinito {#default-content}

**Contenuto predefinito** è contenuto che un autore può inserire in modo intuitivo in una pagina senza aggiungere alcuna semantica aggiuntiva. Sono inclusi testo, intestazioni, collegamenti e immagini. La funzione e lo scopo di tale contenuto sono auto-esplicativi.

In AEM, questo contenuto viene implementato come componenti con modelli predefiniti molto semplici, che includono tutto ciò che può essere serializzato in Markdown e HTML.

* **Testo**: testo formattato (inclusi gli elementi dell’elenco e testo formattato o in corsivo)
* **Titolo**: testo, tipo (h1-h6)
* **Immagine**: origine, descrizione
* **Pulsante**: Testo, titolo, URL, tipo (predefinito, primario, secondario)

Il modello di questi componenti fa parte della [Boilerplate per la creazione di AEM con Edge Delivery Services.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## Blocchi {#blocks}

I blocchi vengono utilizzati per creare contenuti più ricchi con stili e funzionalità specifici. A differenza del contenuto predefinito, i blocchi richiedono semantica aggiuntiva. I blocchi possono essere collegati a [componenti nell’editor di pagine AEM.](/help/implementing/developing/components/overview.md)

I blocchi sono essenzialmente parti di contenuto decorate da JavaScript e formattate con un foglio di stile.

### Blocca definizione modello {#model-definition}

Quando si utilizza l’authoring AEM con i Edge Delivery Services, il contenuto dei blocchi deve essere modellato esplicitamente per fornire all’autore l’interfaccia per la creazione dei contenuti. In sostanza, devi creare un modello in modo che l’interfaccia utente di authoring sappia quali opzioni presentare all’autore in base al blocco.

Il [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) file definisce il modello dei blocchi. I campi definiti nel modello del componente vengono mantenuti come proprietà nell’AEM e visualizzati come celle nella tabella che costituisce un blocco.

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

Nota che non tutti i blocchi devono avere un modello. Alcuni blocchi sono semplicemente [container](#container) per un elenco di figli, in cui ogni figlio ha un proprio modello.

È inoltre necessario definire quali blocchi esistono e possono essere aggiunti a una pagina utilizzando l’Editor universale. Il [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) file elenca i componenti man mano che vengono resi disponibili da Universal Editor.

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

È possibile utilizzare un modello per molti blocchi. Ad esempio, alcuni blocchi possono condividere un modello che definisce un testo e un’immagine.

Per ogni blocco, lo sviluppatore:

* È necessario utilizzare il `core/franklin/components/block/v1/block` tipo di risorsa, implementazione generica della logica di blocco nell’AEM.
* È necessario definire il nome del blocco, che verrà renderizzato nell’intestazione della tabella del blocco.
* Può definire un [ID modello.](/help/implementing/universal-editor/field-types.md#model-structure)
* Può definire un [ID filtro.](/help/implementing/universal-editor/customizing.md#filtering-components)

Tutte queste informazioni vengono memorizzate nell&#39;AEM quando un blocco viene aggiunto a una pagina.

>[!WARNING]
>
>Anche se possibile, non è necessario implementare componenti AEM personalizzati. I componenti dei Edge Delivery Services forniti dall&#39;AEM sono sufficienti e offrono alcuni parapetti per facilitare lo sviluppo.
>
>Per questo motivo, l’Adobe sconsiglia l’utilizzo di tipi di risorse AEM personalizzati.

### Struttura di blocco {#block-structure}

Le proprietà dei blocchi sono [definite nei modelli di componenti](#model-definition) e persisteva in quanto tale nell’AEM. Le proprietà vengono sottoposte a rendering come celle nella struttura di tipo tabella del blocco.

#### Blocchi semplici {#simple}

Nella forma più semplice, un blocco esegue il rendering di ogni proprietà in una singola riga/colonna nell’ordine in cui sono definite nel modello.

Nell&#39;esempio seguente, l&#39;immagine viene definita per prima nel modello e per seconda nel testo. Viene quindi eseguito il rendering con l&#39;immagine per prima e il testo per seconda.

##### Dati {#data-simple}

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

##### Markup {#markup-simple}

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

È possibile notare che alcuni tipi di valori consentono di dedurre la semantica nel markup e che le proprietà vengono combinate in celle singole. Questo comportamento è descritto nella sezione [Inferenza testo.](#type-inference)

#### Blocco chiave-valore {#key-value}

In molti casi, si consiglia di decorare il markup semantico renderizzato, aggiungere nomi di classi CSS, aggiungere nuovi nodi o spostarli nel DOM e applicare stili.

In altri casi, tuttavia, il blocco viene letto come una configurazione di tipo coppia chiave-valore.

Un esempio è il [metadati di sezione.](/help/edge/developer/markup-sections-blocks.md#sections) In questo caso d’uso, il blocco può essere configurato per il rendering come tabella di coppia chiave-valore. Consulta la sezione [Metadati sezioni e sezioni](#sections-metadata) per ulteriori informazioni.

##### Dati {#data-key-value}

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

##### Markup {#markup-key-value}

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

#### Blocchi contenitore {#container}

Entrambe le strutture precedenti hanno una singola dimensione: l’elenco delle proprietà. I blocchi contenitore consentono di aggiungere elementi figlio (di solito dello stesso tipo o modello) e sono quindi bidimensionali. Questi blocchi supportano ancora le proprie proprietà sottoposte a rendering come righe con una singola colonna. Tuttavia, consentono anche di aggiungere elementi secondari, per i quali ogni elemento viene riprodotto come riga e ogni proprietà come colonna all’interno di tale riga.

Nell’esempio seguente, un blocco accetta un elenco di icone collegate come elementi secondari, dove ogni icona collegata ha un’immagine e un collegamento. Osserva [ID filtro](/help/implementing/universal-editor/customizing.md#filtering-components) impostato nei dati del blocco per fare riferimento alla configurazione del filtro.

##### Dati {#data-container}

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

##### Markup {#markup-container}

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

### Creazione di modelli di contenuto semantico per blocchi {#creating-content-models}

Con il [spiegazioni sulle meccaniche della struttura del blocco,](#block-structure) è possibile creare un modello di contenuto che mappa i contenuti persistenti in AEM uno a uno al livello di consegna.

All’inizio di ogni progetto, è necessario considerare attentamente un modello di contenuto per ogni blocco. Deve essere agnostico rispetto all’origine del contenuto e all’esperienza di authoring per consentire agli autori di passare a un’altra origine o di combinarle riutilizzando al contempo le implementazioni e gli stili dei blocchi. Maggiori dettagli e indicazioni generali sono disponibili in [David&#39;s Model (versione 2).](https://www.aem.live/docs/davidsmodel) In particolare, [raccolta blocchi](/help/edge/developer/block-collection.md) contiene un ampio set di modelli di contenuto per casi d’uso specifici con pattern di interfaccia utente comuni.

Per l’authoring AEM con Edge Delivery Services, questo solleva la questione di come distribuire un modello di contenuto semantico convincente quando le informazioni vengono create con moduli composti da più campi invece di modificare il markup semantico in un contesto come il testo RTF.

Per risolvere questo problema, esistono tre metodi che facilitano la creazione di un modello di contenuto convincente:

* [Inferenza tipo](#type-inference)
* [Comprimi campo](#field-collapse)
* [Raggruppamento elementi](#element-grouping)

>[!NOTE]
>
>Le implementazioni di blocco possono decostruire il contenuto e sostituire il blocco con un DOM renderizzato lato client. Anche se questo è possibile e intuitivo per uno sviluppatore, non è la best practice per i Edge Delivery Services.

#### Inferenza tipo {#type-inference}

Per alcuni valori possiamo dedurre il significato semantico dai valori stessi. Tali valori includono:

* **Immagini** - Se un riferimento a una risorsa in AEM è una risorsa di tipo MIME che inizia con `image/`, il riferimento viene renderizzato come `<picture><img src="${reference}"></picture>`.
* **Collegamenti** - Se esiste un riferimento nell’AEM e non è un’immagine, o se il valore inizia con `https?://`  o `#`, il riferimento viene renderizzato come `<a href="${reference}">${reference}</a>` .
* **Rich Text** - Se un valore tagliato inizia con un paragrafo (`p`, `ul`, `ol`, `h1`-`h6`, ecc.), il valore viene rappresentato come testo RTF.
* **Nomi classi** - Il `classes` viene trattata come opzione di blocco ed è rappresentata nell’intestazione della tabella per [blocchi semplici,](#simple) o come elenco di valori per gli elementi in una [blocco contenitore.](#container)
* **Elenchi valori** - Se un valore è una proprietà con più valori e il primo valore non è nessuno dei precedenti, tutti i valori vengono concatenati come elenco separato da virgole.

Tutto il resto verrà visualizzato come testo normale.

#### Comprimi campo {#field-collapse}

Compressione campo è il meccanismo che consente di combinare più valori di campo in un singolo elemento semantico basato su una convenzione di denominazione che utilizza i suffissi `Title`, `Type`, `Alt`, e `Text` (distinzione maiuscole/minuscole). Qualsiasi proprietà che termina con uno qualsiasi di questi suffissi non sarà considerata un valore, ma piuttosto un attributo di un’altra proprietà.

##### Immagini {#image-collapse}

###### Dati {#data-image}

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

###### Markup {#markup-image}

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

##### Collegamenti e pulsanti {#links-buttons-collapse}

###### Dati {#data-links-buttons}

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

###### Markup {#markup-links-buttons}

No `linkType`, o `linkType=default`

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

##### Titoli {#headings-collapse}

###### Dati {#data-headings}

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

###### Markup {#markup-headings}

```html
<h2>Getting started</h2>
```

#### Raggruppamento elementi {#element-grouping}

Mentre [compressione campo](#field-collapse) riguarda la combinazione di più proprietà in un singolo elemento semantico; il raggruppamento di elementi riguarda la concatenazione di più elementi semantici in una singola cella. Ciò è particolarmente utile per i casi d’uso in cui l’autore deve essere limitato nel tipo e nel numero di elementi che può creare.

Ad esempio, l’autore deve creare solo un sottotitolo, un titolo e una singola descrizione di paragrafo combinati con un massimo di due pulsanti di invito all’azione. Raggruppando questi elementi si ottiene un markup semantico a cui è possibile applicare uno stile senza ulteriori azioni.

##### Dati {#data-grouping}

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

##### Markup {#markup-grouping}

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

## Metadati sezioni e sezioni {#sections-metadata}

Allo stesso modo in cui uno sviluppatore può definire e modellare più [blocchi,](#blocks) possono definire sezioni diverse.

Il modello di contenuto dei Edge Delivery Services consente deliberatamente un solo livello di nidificazione, ovvero qualsiasi contenuto o blocco predefinito contenuto in una sezione. Ciò significa che per avere componenti visivi più complessi che possono contenere altri componenti, devono essere modellati come sezioni e combinati utilizzando il lato client con blocco automatico. Esempi tipici di ciò sono le linguette e le sezioni comprimibili come le fisarmoniche.

Una sezione può essere definita nello stesso modo di un blocco, ma con il tipo di risorsa `core/franklin/components/section/v1/section`. Le sezioni possono avere un nome e un [ID filtro,](/help/implementing/universal-editor/customizing.md#filtering-components) utilizzati da [Editor universale](/help/implementing/universal-editor/introduction.md) solo, nonché un [ID modello,](/help/implementing/universal-editor/field-types.md#model-structure) utilizzato per eseguire il rendering dei metadati della sezione. Il modello è in questo modo il modello del blocco di metadati della sezione, che verrà automaticamente aggiunto a una sezione come blocco chiave-valore, se non è vuoto.

Il [ID modello](/help/implementing/universal-editor/field-types.md#model-structure) e [ID filtro](/help/implementing/universal-editor/customizing.md#filtering-components) della sezione predefinita è `section`. Può essere utilizzato per modificare il comportamento della sezione di default. L’esempio seguente aggiunge alcuni stili e un’immagine di sfondo al modello di metadati della sezione.

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

L’esempio che segue definisce una sezione tab, che può essere utilizzata per creare un blocco tabs combinando sezioni consecutive con un attributo di dati del titolo della scheda in un blocco tabs durante il blocco automatico.

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

I documenti possono avere una pagina [blocco di metadati,](/help/edge/authoring.md#metadata--seo) utilizzato per definire quale `<meta>` gli elementi vengono sottoposti a rendering nel `<head>` di una pagina. Le proprietà di pagina delle pagine in AEM as a Cloud Service corrispondono a quelle disponibili come predefinite per i Edge Delivery Services, come `title`, `description`, `keywords`, ecc.

Prima di approfondire la definizione dei metadati, consulta i seguenti documenti per comprendere il concetto di metadati della pagina.

* [Metadati](https://www.aem.live/developer/block-collection/metadata)
* [Metadati in blocco](/help/edge/docs/bulk-metadata.md)

È inoltre possibile definire metadati di pagina aggiuntivi in due modi.

### Fogli di calcolo metadati {#metadata-spreadsheets}

È possibile definire i metadati per percorso o per modello di percorso in modo simile a una tabella in AEM as a Cloud Service. È disponibile un’interfaccia utente di authoring per i dati simili a tabelle simile a quella di Excel o Google Sheets.

Per creare tale tabella, crea una pagina e utilizza il modello Metadati nella console Sites.

>[!NOTE]
>
>Quando modifichi il foglio di calcolo dei metadati, assicurati di passare a **Anteprima** in quanto l’authoring si verifica sulla pagina stessa, non all’interno dell’editor.

Nelle proprietà di pagina del foglio di calcolo, definisci i campi di metadati necessari e l’URL. Quindi aggiungi i metadati per percorso di pagina o pattern di percorso della pagina, in cui il campo URL si riferisce ai percorsi pubblici e mappati e non al percorso del contenuto nell’AEM.

Assicurati che il foglio di calcolo sia aggiunto anche alla mappatura del percorso prima di pubblicarlo.

```text
mappings:
  - /content/site/:/
  - /content/site/metadata:/metadata.json
```

### Proprietà pagina {#page-properties}

È inoltre possibile definire un modello di componente per i metadati della pagina, che verrà reso disponibile all’autore come scheda della finestra di dialogo delle proprietà della pagina di AEM Sites.

Per farlo, crea un modello di componente con l’ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

Alcuni nomi di campo hanno un significato speciale e verranno ignorati durante la visualizzazione dell’interfaccia utente della finestra di dialogo per la creazione:

* **`cq:tags`** - Per impostazione predefinita, `cq:tags` non vengono aggiunti ai metadati. Aggiungendoli al `page-metadata` il modello aggiungerà gli ID tag come elenco separato da virgole come `tags` tag meta nella parte superiore.
* **`cq:lastModified`** - `cq:lastModified` aggiungerà i dati come `last-modified` alla testa.
