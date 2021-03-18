---
title: Guida di riferimento dei componenti
description: Guida di riferimento per sviluppatori per i dettagli dei componenti e della relativa struttura
translation-type: tm+mt
source-git-commit: f9a6dbec25b8154fda8069ff213aaaaa1d443ca1
workflow-type: tm+mt
source-wordcount: '3675'
ht-degree: 1%

---


# Guida di riferimento dei componenti {#components-reference-guide}

I componenti sono al centro della creazione di un’esperienza in AEM. I [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) consentono di iniziare a utilizzare un set di strumenti di componenti affidabili e pronti. Il [tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) spiega allo sviluppatore come utilizzare questi strumenti e come creare componenti personalizzati per creare un nuovo sito AEM.

>[!TIP]
>
>Prima di fare riferimento a questo documento, assicurati di aver completato il [tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e quindi di avere familiarità con i [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e il [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Poiché l’esercitazione WKND copre la maggior parte dei casi d’uso, questo documento è inteso solo come complemento a tali risorse. Fornisce specifiche tecniche approfondite sulla struttura e la configurazione dei componenti in AEM e non è inteso come guida introduttiva.

## Panoramica {#overview}

Questa sezione descrive i concetti e i problemi chiave come introduzione ai dettagli necessari allo sviluppo dei tuoi componenti.

### Pianificazione {#planning}

Prima di iniziare effettivamente a configurare o codificare il componente, è necessario chiedere:

* Cosa devi fare esattamente con il nuovo componente?
* È necessario creare un componente da zero o è possibile ereditare le nozioni di base da un componente esistente?
* Il componente richiederà una logica per selezionare/manipolare il contenuto?
   * La logica deve essere mantenuta separata dal livello dell’interfaccia utente. HTL è progettato per garantire che ciò accada.
* Il componente avrà bisogno della formattazione CSS?
   * La formattazione CSS deve essere mantenuta separata dalle definizioni dei componenti. Definisci le convenzioni per denominare gli elementi HTML in modo da poterli modificare tramite file CSS esterni.
* Quali sono le implicazioni per la sicurezza del nuovo componente?

### Riutilizzo dei componenti esistenti {#reusing-components}

Prima di investire tempo nella creazione di un componente completamente nuovo, è consigliabile personalizzare o estendere i componenti esistenti. [Il ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) componente core offre una suite di componenti flessibili, affidabili e testati per la produzione.

#### Estensione dei componenti core {#extending-core-components}

I componenti core offrono inoltre [chiari pattern di personalizzazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html) che è possibile utilizzare per adattarli alle esigenze del proprio progetto.

#### Sovrapposizione dei componenti {#overlying-components}

I componenti possono anche essere ridefiniti con una [sovrapposizione](/help/implementing/developing/introduction/overlays.md) in base alla logica del percorso di ricerca. Tuttavia in questo caso, [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) non verrà attivato e `/apps` deve definire l&#39;intera sovrapposizione.

#### Estensione delle finestre di dialogo dei componenti {#extending-component-dialogs}

È inoltre possibile ignorare una finestra di dialogo di un componente utilizzando Sling Resource Merger e definendo la proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l’intera finestra di dialogo.

### Logica dei contenuti e marcatura di rendering {#content-logic-and-rendering-markup}

Viene eseguito il rendering del componente con [HTML.](https://www.w3schools.com/htmL/html_intro.asp) Il componente deve definire l’HTML necessario per prendere il contenuto richiesto e quindi eseguirne il rendering come necessario, sia negli ambienti di authoring che di pubblicazione.

Si consiglia di mantenere il codice responsabile del markup e del rendering separato dal codice che controlla la logica utilizzata per selezionare il contenuto del componente.

Questa filosofia è supportata da [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it), un linguaggio di template appositamente limitato per garantire un linguaggio di programmazione reale viene utilizzato per definire la logica di business sottostante. Questo meccanismo evidenzia il codice richiesto per una determinata visualizzazione e, se necessario, consente una logica specifica per diverse visualizzazioni dello stesso componente.

Questa logica (facoltativa) può essere implementata in modi diversi e viene richiamata da HTL con comandi specifici:

* Utilizzando Java - [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) abilita un file HTL per accedere ai metodi helper in una classe Java personalizzata. Questo consente di utilizzare il codice Java per implementare la logica necessaria per selezionare e configurare il contenuto del componente.
* Utilizzando JavaScript - [L&#39;API Use-API JavaScript HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) abilita un file HTL per accedere al codice helper scritto in JavaScript. Questo consente di utilizzare il codice JavaScript per implementare la logica necessaria per selezionare e configurare il contenuto del componente.
* Utilizzo di librerie lato client : i siti web moderni si basano in larga misura sull’elaborazione lato client basata su codice JavaScript e CSS complessi. Per ulteriori informazioni, consulta il documento [Utilizzo delle librerie lato client su AEM come Cloud Service](/help/implementing/developing/introduction/clientlibs.md) .

## Struttura del componente {#structure}

La struttura di un componente AEM è potente e flessibile. Le parti principali sono:

* [Tipo risorsa](#resource-type)
* [Definizione del componente](#component-definition)
* [Proprietà e nodi secondari di un componente](#properties-and-child-nodes-of-a-component)
* [Finestre di dialogo](#dialogs)
* [Finestre di dialogo di progettazione](#design-dialogs)

### Tipo risorsa {#resource-type}

Un elemento chiave della struttura è il tipo di risorsa.

* La struttura dei contenuti dichiara le intenzioni.
* Il tipo di risorsa li implementa.

Questa è un&#39;astrazione che aiuta a garantire che anche quando l&#39;aspetto e l&#39;aspetto cambiano nel tempo, l&#39;intenzione rimanga nel tempo.

### Definizione del componente {#component-definition}

La definizione di un componente può essere suddivisa come segue:

* I componenti AEM sono basati su [Sling.](https://sling.apache.org/documentation.html)
* I componenti AEM si trovano in `/libs/core/wcm/components`.
* I componenti specifici per progetto/sito si trovano in `/apps/<myApp>/components`.
* AEM componenti standard sono definiti come `cq:Component` e presentano gli elementi chiave:
   * proprietà jcr - Elenco di proprietà jcr. Si tratta di variabili e alcune possono essere facoltative anche se la struttura di base di un nodo di componente, le relative proprietà e i sottonodi sono definiti dalla definizione `cq:Component`.
   * Risorse : definiscono gli elementi statici utilizzati dal componente.
   * Script : vengono utilizzati per implementare il comportamento dell’istanza risultante del componente.

#### Proprietà vitali {#vital-properties}

* **Nodo principale**:
   * `<mycomponent> (cq:Component)` - Nodo gerarchico del componente.
* **Proprietà** vitali:
   * `jcr:title` - Titolo del componente; ad esempio, utilizzato come etichetta quando il componente è elencato nella console  [Componenti ](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) browser e  [componenti](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description` - Descrizione del componente; utilizzato come suggerimento per il passaggio del mouse nella console Componenti, browser e componenti
   * Per ulteriori informazioni, consulta la sezione [Icona componente](#component-icon) .
* **Nodi** figlio fondamentali:
   * `cq:editConfig (cq:EditConfig)` - Definisce le proprietà di modifica del componente e consente al componente di essere visualizzato nel browser Componenti
      * Se il componente dispone di una finestra di dialogo, viene visualizzato automaticamente nel browser Componenti o nella barra laterale, anche se cq:editConfig non esiste.
   * `cq:childEditConfig (cq:EditConfig)` - Controlla gli aspetti dell’interfaccia utente dell’autore per i componenti secondari che non ne definiscono i propri  `cq:editConfig`.
   * `cq:dialog (nt:unstructured)` - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o modificare il contenuto.
   * `cq:design_dialog (nt:unstructured)` - Modifica di progettazione per questo componente

#### Icona componente {#component-icon}

L’icona o l’abbreviazione del componente viene definita tramite le proprietà JCR del componente quando il componente viene creato dallo sviluppatore. Queste proprietà vengono valutate nell&#39;ordine seguente e viene utilizzata la prima proprietà valida trovata.

1. `cq:icon` - Proprietà String che punta a un&#39;icona standard nella libreria  [Coral UI ](https://opensource.adobe.com/coral-spectrum/examples/#icon) da visualizzare nel browser componenti
   * Utilizza il valore dell’attributo HTML dell’icona Coral.
1. `abbreviation` - Proprietà String per personalizzare l&#39;abbreviazione del nome del componente nel browser componenti
   * L&#39;abbreviazione deve essere limitata a due caratteri.
   * Specificando una stringa vuota si otterrà l&#39;abbreviazione dei primi due caratteri della proprietà `jcr:title` .
      * Ad esempio &quot;Im&quot; per &quot;Image&quot;
      * Il titolo localizzato verrà utilizzato per creare l’abbreviazione.
   * L’abbreviazione viene tradotta solo se il componente ha una proprietà `abbreviation_commentI18n` , che viene quindi utilizzata come suggerimento di traduzione.
1. `cq:icon.png` o  `cq:icon.svg` - Icona per questo componente, visualizzata nel browser Componenti
   * 20 x 20 pixel è la dimensione delle icone dei componenti standard.
      * Verranno ridimensionate le icone più grandi (lato client).
   * Il colore consigliato è rgb(112, 112, 112) > #707070
   * Lo sfondo delle icone dei componenti standard è trasparente.
   * Sono supportati solo i file `.png` e `.svg` .
   * Se si importa dal file system tramite il plug-in Eclipse, i nomi dei file devono essere preceduti, ad esempio, da un escape come `_cq_icon.png` o `_cq_icon.svg`.
   * `.png` ha un precedente su  `.svg` se entrambi sono presenti.

Se sul componente non è presente nessuna delle proprietà di cui sopra (`cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`):

* Il sistema cercherà le stesse proprietà sui super componenti che seguono la proprietà `sling:resourceSuperType` .
* Se a livello di super componente non viene trovato nulla o un&#39;abbreviazione vuota, il sistema costruirà l&#39;abbreviazione dalle prime lettere della proprietà `jcr:title` del componente corrente.

Per annullare l’ereditarietà di icone da super componenti, l’impostazione di una proprietà `abbreviation` vuota sul componente ripristina il comportamento predefinito.

La [console Componenti](/help/sites-cloud/authoring/features/components-console.md#component-details) mostra come è definita l’icona di un particolare componente.

#### Esempio di icona SVG {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### Proprietà e nodi secondari di un componente {#properties-and-child-nodes-of-a-component}

Molti dei nodi/proprietà necessari per definire un componente sono comuni a entrambe le interfacce, con differenze che rimangono indipendenti in modo che il componente possa funzionare in entrambi gli ambienti.

Un componente è un nodo di tipo `cq:Component` e ha le seguenti proprietà e nodi figlio:

| Nome | Tipo | Descrizione |
|---|---|---|
| `.` | `cq:Component` | Rappresenta il componente corrente. Un componente è di tipo nodo `cq:Component`. |
| `componentGroup` | `String` | Rappresenta il gruppo in cui il componente può essere selezionato nel [Browser componenti.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) Un valore che inizia con  `.` viene utilizzato per i componenti che non sono disponibili per la selezione dall’interfaccia utente, ad esempio i componenti di base da cui ereditano altri componenti. |
| `cq:isContainer` | `Boolean` | Indica se il componente è un componente contenitore e può quindi contenere altri componenti, ad esempio un sistema paragrafo. |
| `cq:dialog` | `nt:unstructured` | Questa è la definizione della finestra di dialogo di modifica per il componente. |
| `cq:design_dialog` | `nt:unstructured` | Questa è la definizione della finestra di dialogo di progettazione per il componente. |
| `cq:editConfig` | `cq:EditConfig` | Definisce la [modifica la configurazione del componente.](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | Questo restituisce attributi di tag aggiuntivi aggiunti al tag HTML circostante. Abilita l’aggiunta di attributi ai div generati automaticamente. |
| `cq:noDecoration` | `Boolean` | Se true, non viene eseguito il rendering del componente con classi div e css generate automaticamente. |
| `cq:template` | `nt:unstructured` | Se trovato, questo nodo verrà utilizzato come modello di contenuto quando il componente viene aggiunto dal browser Componenti. |
| `jcr:created` | `Date` | Data di creazione del componente. |
| `jcr:description` | `String` | Descrizione del componente. |
| `jcr:title` | `String` | Titolo del componente. |
| `sling:resourceSuperType` | `String` | Quando è impostato, il componente eredita da questo componente. |
| `component.html` | `nt:file` | Questo è il file di script HTL del componente. |
| `cq:icon` | `String` | Questo valore fa riferimento all&#39; [icona del componente](#component-icon) e viene visualizzato nel browser Componenti. |

Se osserviamo il componente **Testo**, è possibile vedere una serie di elementi:

![Struttura del componente testo](assets/components-text.png)

Le proprietà di particolare interesse comprendono:

* `jcr:title` - Titolo del componente utilizzato per identificare il componente all’interno del Browser componenti.
* `jcr:description` - Descrizione del componente.
* `sling:resourceSuperType` - Indica il percorso di ereditarietà quando si estende un componente (ignorando una definizione).

I nodi figlio di particolare interesse includono:

* `cq:editConfig` - Consente di controllare gli aspetti visivi del componente durante la modifica.
* `cq:dialog` - Definisce la finestra di dialogo per la modifica del contenuto di questo componente.
* `cq:design_dialog` - Specifica le opzioni di modifica della progettazione per questo componente.

### Finestre di dialogo {#dialogs}

Le finestre di dialogo sono un elemento chiave del componente, in quanto forniscono un’interfaccia che consente agli autori di configurare il componente in una pagina di contenuto e fornire l’input per quel componente. Per informazioni dettagliate sull’interazione degli autori di contenuti con i componenti, consulta la [documentazione sull’authoring](/help/sites-cloud/authoring/fundamentals/editing-content.md) .

A seconda della complessità del componente, potrebbe essere necessaria una o più schede nella finestra di dialogo.

Finestre di dialogo per i componenti AEM:

* Sono `cq:dialog` nodi di tipo `nt:unstructured`.
* Si trovano sotto i relativi nodi `cq:Component` e accanto alle relative definizioni di componenti.
* Definisci la finestra di dialogo per la modifica del contenuto di questo componente.
* Sono definite utilizzando i componenti dell’interfaccia utente Granite.
* Sono sottoposte a rendering lato server (come componenti Sling) in base alla loro struttura del contenuto e alla proprietà `sling:resourceType` .
* Contiene una struttura di nodo che descrive i campi all’interno della finestra di dialogo
   * Questi nodi sono `nt:unstructured` con la proprietà `sling:resourceType` richiesta.

![Definizione finestra di dialogo del componente titolo](assets/components-title-dialog.png)

All’interno della finestra di dialogo, vengono definiti i singoli campi:

![Campi della finestra di dialogo definizione del componente Titolo](assets/components-title-dialog-items.png)

### Finestre di dialogo di progettazione {#design-dialogs}

Le finestre di dialogo di progettazione sono simili alle finestre di dialogo utilizzate per modificare e configurare i contenuti, ma forniscono agli autori di modelli l’interfaccia per la configurazione e l’impostazione di specifici dettagli di progettazione in un modello di pagina. I modelli di pagina vengono quindi utilizzati dagli autori dei contenuti per creare pagine di contenuto. Per informazioni dettagliate sulla creazione dei modelli, consulta la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md) .

[Le finestre di dialogo Progettazione vengono utilizzate per modificare un modello](/help/sites-cloud/authoring/features/templates.md) di pagina, anche se non sono necessarie per tutti i componenti. Ad esempio, i **Titolo** e **Componenti immagine** dispongono entrambe di finestre di dialogo di progettazione, mentre il **Componente di condivisione social media** no.

### Interfaccia Coral e interfaccia Granite {#coral-and-granite}

L’interfaccia Coral e l’interfaccia Granite definiscono l’aspetto AEM.

* [L’](https://opensource.adobe.com/coral-spectrum/documentation/) interfaccia utente Coral fornisce un’interfaccia utente coerente per tutte le soluzioni cloud.
* [L’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) interfaccia utente Granite fornisce il markup dell’interfaccia Coral nei componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente.

L’interfaccia utente Granite offre una vasta gamma di widget di base necessari per creare la finestra di dialogo sull’ambiente di authoring. Se necessario, puoi estendere questa selezione e creare un widget personalizzato.

Per ulteriori dettagli, consulta le risorse seguenti:

* [Struttura dell’interfaccia AEM](/help/implementing/developing/introduction/ui-structure.md)

### Personalizzazione dei campi della finestra di dialogo {#customizing-dialog-fields}

>[!TIP]
>
>Consulta la [sessione Gems AEM](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) sulla personalizzazione dei campi di dialogo.

Per creare un nuovo widget da utilizzare in una finestra di dialogo dei componenti è necessario creare un nuovo componente campo dell’interfaccia Granite.

Se si considera la finestra di dialogo come un contenitore semplice per un elemento modulo, è anche possibile visualizzare il contenuto principale del contenuto della finestra di dialogo come campi modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa; equivale a creare un nuovo componente. Per facilitare l’esecuzione di tale attività, l’interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

L&#39;interfaccia utente Granite fornisce in modo più specifico una serie di componenti campo adatti all&#39;uso nelle finestre di dialogo o, più in generale, nei moduli [.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

Dopo aver creato il tipo di risorsa, puoi creare un’istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` che fa riferimento al tipo di risorsa appena introdotto.

#### Accesso ai campi della finestra di dialogo {#access-to-dialog-fields}

È inoltre possibile utilizzare le condizioni di rendering (`rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo; ad esempio:

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## Uso dei componenti {#using-components}

Una volta creato un componente, è necessario attivarlo per utilizzarlo. Il suo utilizzo mostra come la struttura del componente si relaziona alla struttura del contenuto risultante nell’archivio.

### Aggiunta del componente al modello {#adding-your-component-to-the-template}

Una volta definito un componente, questo deve essere reso disponibile per l’uso. Per rendere un componente disponibile per l’utilizzo in un modello, è necessario attivarlo nel criterio del contenitore layout del modello.

Per informazioni dettagliate sulla creazione dei modelli, consulta la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md) .

### Componenti e contenuti creati {#components-and-the-content-they-create}

Se creiamo e configuriamo un&#39;istanza del componente **Titolo** sulla pagina: `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![Finestra di dialogo per la modifica del titolo](assets/components-title-dialog.png)

A questo punto è possibile vedere la struttura del contenuto creato all’interno dell’archivio:

![Struttura del nodo del componente titolo](assets/components-title-content-nodes.png)

In particolare, se osservi il testo effettivo di un **Componente titolo**:

* Il contenuto contiene una proprietà `jcr:title` contenente il testo effettivo del titolo immesso dall&#39;autore.
* Contiene anche un riferimento `sling:resourceType` alla definizione del componente.

Le proprietà definite dipendono dalle singole definizioni. Anche se possono essere più complessi di quanto sopra, seguono comunque gli stessi principi di base.

## Gerarchia e ereditarietà dei componenti {#component-hierarchy-and-inheritance}

I componenti all&#39;interno di AEM sono soggetti alla **Gerarchia dei tipi di risorse**. Viene utilizzato per estendere i componenti utilizzando la proprietà `sling:resourceSuperType`. Questo consente al componente di ereditare da un altro componente.

Per ulteriori informazioni, consulta la sezione [Riutilizzo dei componenti](#reusing-components) .

## Modifica comportamento {#edit-behavior}

Questa sezione spiega come configurare il comportamento di modifica di un componente. Ciò include attributi come le azioni disponibili per il componente, le caratteristiche dell’editor in.place e i listener relativi agli eventi sul componente.

Il comportamento di modifica di un componente viene configurato aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi secondari. Sono disponibili le seguenti proprietà e nodi figlio:

* `cq:editConfig` proprietà nodo
* [`cq:editConfig` nodi](#configuring-with-cq-editconfig-child-nodes) secondari:
   * `cq:dropTargets` (tipo di nodo  `nt:unstructured`): definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa di Content Finder (è consentita una singola destinazione di rilascio)
   * `cq:inplaceEditing` (tipo di nodo  `cq:InplaceEditingConfig`): definisce una configurazione di modifica diretta per il componente
   * `cq:listeners` (tipo di nodo  `cq:EditListenersConfig`): definisce cosa accade prima o dopo un’azione sul componente

Ci sono molte configurazioni esistenti in AEM. È possibile cercare facilmente proprietà specifiche o nodi secondari utilizzando lo strumento Query in **CRXDE Lite**.

### Segnaposto Componente {#component-placeholders}

I componenti devono sempre eseguire il rendering di contenuti HTML visibili all’autore, anche quando il componente non dispone di contenuti. In caso contrario, potrebbe scomparire visivamente dall’interfaccia dell’editor, rendendola tecnicamente presente ma invisibile sulla pagina e nell’editor. In tal caso, gli autori non potranno selezionare e interagire con il componente vuoto.

Per questo motivo, i componenti devono eseguire il rendering di un segnaposto purché non eseguano il rendering di alcun output visibile quando la pagina viene sottoposta a rendering nell’editor di pagine (quando la modalità WCM è `edit` o `preview`).
Il markup HTML tipico per un segnaposto è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

Lo script HTL tipico che esegue il rendering del segnaposto HTML di cui sopra è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

Nell’esempio precedente, `isEmpty` è una variabile che è true solo quando il componente non ha contenuto ed è invisibile all’autore.

Per evitare ripetizioni, l&#39;Adobe consiglia agli implementatori di componenti di utilizzare un modello HTL per questi segnaposto, [come quello fornito dai componenti core.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

L’utilizzo del modello nel collegamento precedente viene quindi fatto con la seguente riga di HTL:

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

Nell’esempio precedente, `model.text` è la variabile che è true solo quando il contenuto ha contenuto ed è visibile.

Un esempio di utilizzo di questo modello può essere visualizzato nei componenti core [come nel componente titolo.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### Configurazione con cq:EditConfig Child Nodes {#configuring-with-cq-editconfig-child-nodes}

#### Eliminazione di risorse in una finestra di dialogo - cq:dropTargets {#cq-droptargets}

Il nodo `cq:dropTargets` (tipo di nodo `nt:unstructured`) definisce il target di rilascio che può accettare un rilascio da una risorsa trascinata da Content Finder. È un nodo di tipo `cq:DropTargetConfig`.

Il nodo figlio di tipo `cq:DropTargetConfig` definisce una destinazione di rilascio nel componente.

### Modifica diretta - cq:inplaceEditing {#cq-inplaceediting}

Un editor locale consente all’utente di modificare il contenuto direttamente nel flusso di contenuto, senza la necessità di aprire una finestra di dialogo. Ad esempio, i componenti standard **Testo** e **Titolo** dispongono entrambi di un editor in-lace.

Un editor locale non è necessario/significativo per ogni tipo di componente.

Il nodo `cq:inplaceEditing` (tipo di nodo `cq:InplaceEditingConfig`) definisce una configurazione di modifica diretta per il componente. Può avere le seguenti proprietà:

| Nome proprietà | Tipo di proprietà | Valore proprietà |
|---|---|---|
| `active` | `Boolean` | `true` per abilitare la modifica diretta del componente. |
| `configPath` | `String` | Percorso della configurazione dell&#39;editor, che può essere specificato da un nodo di configurazione |
| `editorType` | `String` | I tipi disponibili sono: `plaintext` per i contenuti non HTML, `title` converte i titoli grafici in un testo normale prima dell’inizio della modifica e `text` utilizza l’editor Rich Text |

La seguente configurazione abilita la modifica in-lace del componente e definisce `plaintext` come tipo di editor:

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### Gestione degli eventi dei campi - cq:listener {#cq-listeners}

Il metodo di gestione degli eventi nei campi di dialogo viene eseguito con i listener in una [libreria client personalizzata.](/help/implementing/developing/introduction/clientlibs.md)

Per inserire una logica nel campo, devi:

* Fai segnare il tuo campo con una determinata classe CSS (il gancio).
* Definisci nella libreria client un listener JS collegato al nome della classe CSS (in questo modo la logica personalizzata viene delimitata solo nel campo e non influisce su altri campi dello stesso tipo).

Per ottenere questo risultato è necessario conoscere la libreria di widget sottostante con cui si desidera interagire. [Consulta la ](https://opensource.adobe.com/coral-spectrum/documentation/) documentazione Coral UI per identificare l’evento a cui desideri reagire.

Il nodo `cq:listeners` (tipo di nodo `cq:EditListenersConfig`) definisce cosa accade prima o dopo un’azione sul componente. Nella tabella seguente sono definite le proprietà possibili.

| Nome proprietà | Valore proprietà |
|---|---|
| `beforedelete` | Il gestore viene attivato prima della rimozione del componente. |
| `beforeedit` | Il gestore viene attivato prima della modifica del componente. |
| `beforecopy` | Il gestore viene attivato prima della copia del componente. |
| `beforeremove` | Il gestore viene attivato prima dello spostamento del componente. |
| `beforeinsert` | Il gestore viene attivato prima dell’inserimento del componente. |
| `beforechildinsert` | Il gestore viene attivato prima che il componente venga inserito all’interno di un altro componente (solo contenitori). |
| `afterdelete` | Il gestore viene attivato dopo la rimozione del componente. |
| `afteredit` | Il gestore viene attivato dopo la modifica del componente. |
| `aftercopy` | Il gestore viene attivato dopo la copia del componente. |
| `afterinsert` | Il gestore viene attivato dopo l’inserimento del componente. |
| `aftermove` | Il gestore viene attivato dopo lo spostamento del componente. |
| `afterchildinsert` | Il gestore viene attivato dopo che il componente è stato inserito all’interno di un altro componente (solo contenitori). |

>[!NOTE]
>
>Nel caso dei componenti nidificati, esistono alcune restrizioni alle azioni definite come proprietà sul nodo `cq:listeners` . Per i componenti nidificati, i valori delle seguenti proprietà **devono essere**:`REFRESH_PAGE`
>
>* `aftermove`
>* `aftercopy`


Il gestore eventi può essere implementato con un&#39;implementazione personalizzata. Ad esempio (dove `project.customerAction` è un metodo statico):

`afteredit = "project.customerAction"`

L&#39;esempio seguente equivale alla configurazione `REFRESH_INSERTED`:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

Con la seguente configurazione, la pagina viene aggiornata dopo che il componente è stato eliminato, modificato, inserito o spostato:

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### Convalida campo {#field-validation}

La convalida dei campi nell’interfaccia utente Granite e i widget dell’interfaccia utente Granite viene eseguita utilizzando l’API `foundation-validation` . Per ulteriori informazioni, consulta la [`foundation-valdiation` documentazione Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html) .

### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se si dispone di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare l’evento `dialog-ready` .

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, il che significa che ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per agganciare nel codice personalizzato JavaScript che esegue personalizzazioni sui campi all’interno di una finestra di dialogo o attività simili.

## Comportamento anteprima {#preview-behavior}

Il cookie [WCM Mode](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/WCMMode.html) viene impostato quando si passa alla modalità Anteprima anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibile alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico, quindi basarsi sul valore del cookie.

## Documentazione dei componenti {#documenting-components}

In qualità di sviluppatore, desideri accedere facilmente alla documentazione del componente per comprendere rapidamente i seguenti elementi:

* Descrizione
* Uso previsto
* Struttura e proprietà del contenuto
* API e punti di estensione esposti
* Ecc.

Per questo motivo, è abbastanza semplice rendere disponibile qualsiasi markdown della documentazione esistente all’interno del componente stesso.

È sufficiente inserire un file `README.md` nella struttura del componente.

![README.md nella struttura del componente](assets/components-documentation.png)

Questa Markdown verrà quindi visualizzata nella [Console dei componenti.](/help/sites-cloud/authoring/features/components-console.md)

![README.md visibile nella console Componenti](assets/components-documentation-console.png)

Il markdown supportato è lo stesso dei frammenti di contenuto [frammenti.](/help/assets/content-fragments/content-fragments.md)