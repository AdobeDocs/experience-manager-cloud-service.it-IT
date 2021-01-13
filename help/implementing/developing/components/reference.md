---
title: Guida di riferimento ai componenti
description: Guida di riferimento per sviluppatori ai dettagli dei componenti e della loro struttura
translation-type: tm+mt
source-git-commit: d843182585a269b5ebb24cc31679b77fb6b6d697
workflow-type: tm+mt
source-wordcount: '3720'
ht-degree: 0%

---


# Guida di riferimento dei componenti {#components-reference-guide}

I componenti sono al centro della creazione di un&#39;esperienza in AEM. I [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e il [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) semplificano l&#39;utilizzo di un set di utensili di componenti robusti e pronti. L&#39; [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) spiega allo sviluppatore come utilizzare questi strumenti e come creare componenti personalizzati per creare un nuovo sito AEM.

>[!TIP]
>
>Prima di fare riferimento a questo documento, accertarsi di aver completato l&#39; [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e di avere familiarità con i [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e con il [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Poiché l’esercitazione WKND copre la maggior parte dei casi di utilizzo, questo documento è destinato solo a essere un complemento a tali risorse. Fornisce informazioni tecniche dettagliate sulla struttura e la configurazione dei componenti in AEM e non è una guida introduttiva.

## Panoramica {#overview}

Questa sezione illustra i concetti e i problemi chiave come introduzione ai dettagli necessari per lo sviluppo di componenti personalizzati.

### Pianificazione {#planning}

Prima di iniziare a configurare o codificare il componente, è necessario chiedere:

* Quali operazioni sono necessarie esattamente per il nuovo componente?
* È necessario creare un componente da zero o ereditare le nozioni di base da un componente esistente?
* Il componente richiede logica per selezionare o manipolare il contenuto?
   * La logica deve essere separata dal livello dell&#39;interfaccia utente. HTL è progettato per contribuire a garantire che ciò avvenga.
* Il componente avrà bisogno di formattazione CSS?
   * La formattazione CSS deve essere separata dalle definizioni dei componenti. Definite le convenzioni per denominare gli elementi HTML in modo da poterli modificare tramite file CSS esterni.
* Quali sono le implicazioni per la sicurezza del nuovo componente?

### Riutilizzo dei componenti esistenti {#reusing-components}

Prima di investire tempo nella creazione di un componente completamente nuovo, è consigliabile personalizzare o estendere i componenti esistenti. [I componenti core ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) offrono una suite di componenti flessibili, robusti e testati per la produzione.

#### Estensione dei componenti core {#extending-core-components}

I componenti core offrono inoltre [chiari pattern di personalizzazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html) che è possibile utilizzare per adattarli alle esigenze del proprio progetto.

#### Sovrapposizione di componenti {#overlying-components}

I componenti possono essere ridefiniti anche con una [sovrapposizione](/help/implementing/developing/introduction/overlays.md) in base alla logica del percorso di ricerca. In questo caso, tuttavia, la [fusione risorse Sling](/help/implementing/developing/introduction/sling-resource-merger.md) non verrà attivata e `/apps` deve definire l&#39;intera sovrapposizione.

#### Estensione delle finestre di dialogo dei componenti {#extending-component-dialogs}

È inoltre possibile ignorare una finestra di dialogo di componente utilizzando la fusione Sling Resource e definendo la proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l’intera finestra di dialogo.

### Logica dei contenuti e markup di rendering {#content-logic-and-rendering-markup}

Il componente verrà rappresentato con [HTML.](https://www.w3schools.com/htmL/html_intro.asp) Il componente deve definire l’HTML necessario per acquisire il contenuto richiesto e eseguirne il rendering come necessario, sia nell’ambiente di creazione che nell’ambiente di pubblicazione.

È consigliabile mantenere il codice responsabile per la marcatura e il rendering separato dal codice che controlla la logica utilizzata per selezionare il contenuto del componente.

Questa filosofia è supportata da [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html), un linguaggio di modello appositamente limitato per garantire che un linguaggio di programmazione reale venga utilizzato per definire la logica di business sottostante. Questo meccanismo evidenzia il codice richiesto per una vista specifica e, se necessario, consente logiche specifiche per diverse viste dello stesso componente.

Questa logica (facoltativa) può essere implementata in modi diversi e viene richiamata da HTL con comandi specifici:

* Utilizzando Java - [L&#39;HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) consente a un file HTL di accedere ai metodi helper in una classe Java personalizzata. Questo consente di utilizzare il codice Java per implementare la logica di selezione e configurazione del contenuto del componente.
* Utilizzando JavaScript - [L&#39;HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) consente a un file HTL di accedere al codice helper scritto in JavaScript. Questo consente di utilizzare il codice JavaScript per implementare la logica necessaria per selezionare e configurare il contenuto del componente.
* Utilizzo di librerie lato client - I siti Web moderni dipendono in larga misura dall&#39;elaborazione lato client basata su codice JavaScript e CSS complessi. Per ulteriori informazioni, vedere il documento [Utilizzo delle librerie lato client in AEM come Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Struttura componente {#structure}

La struttura di un componente AEM è potente e flessibile. Le parti principali sono:

* [Tipo risorsa](#resource-type)
* [Definizione componente](#component-definition)
* [Proprietà e nodi secondari di un componente](#properties-and-child-nodes-of-a-component)
* [Finestre di dialogo](#dialogs)
* [Finestre di dialogo Progettazione](#design-dialogs)

### Tipo risorsa {#resource-type}

Un elemento chiave della struttura è il tipo di risorsa.

* La struttura del contenuto dichiara le intenzioni.
* Il tipo di risorsa li implementa.

Questa è un&#39;astrazione che aiuta a garantire che anche quando l&#39;aspetto e il sentire cambiano nel tempo, l&#39;intenzione rimanga il tempo.

### Definizione del componente {#component-definition}

La definizione di un componente può essere ripartita come segue:

* AEM componenti si basano su [Sling.](https://sling.apache.org/documentation.html)
* AEM componenti si trovano in `/libs/core/wcm/components`.
* I componenti specifici per progetto/sito si trovano in `/apps/<myApp>/components`.
* AEM componenti standard sono definiti come `cq:Component` e presentano gli elementi chiave:
   * jcr Properties - Un elenco di proprietà jcr. Queste sono variabili e alcune possono essere facoltative attraverso la struttura di base di un nodo di componente, le relative proprietà e i sottonodi sono definiti dalla definizione `cq:Component`.
   * Risorse - Definiscono gli elementi statici utilizzati dal componente.
   * Script - Utilizzati per implementare il comportamento dell&#39;istanza risultante del componente.

#### Proprietà vitali {#vital-properties}

* **Nodo principale**:
   * `<mycomponent> (cq:Component)` - Nodo gerarchico del componente.
* **Proprietà** vitali:
   * `jcr:title` - Titolo componente; ad esempio, utilizzato come etichetta quando il componente è elencato nella console  [Componenti ](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) Browser e  [Componenti](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description` - Descrizione del componente; utilizzato come suggerimento al passaggio del mouse nella console Componenti, Browser e Componenti
   * Per ulteriori informazioni, vedere la sezione [Icona componente](#component-icon)
* **Nodi** secondari fondamentali:
   * `cq:editConfig (cq:EditConfig)` - Definisce le proprietà di modifica del componente e abilita la visualizzazione del componente nel browser Componenti
      * Se il componente dispone di una finestra di dialogo, questa viene visualizzata automaticamente nel browser Componenti o nella barra laterale, anche se cq:editConfig non esiste.
   * `cq:childEditConfig (cq:EditConfig)` - Controlla gli aspetti dell’interfaccia utente dell’autore per i componenti secondari che non ne definiscono uno personalizzato  `cq:editConfig`.
   * `cq:dialog (nt:unstructured)` - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o di modificarne il contenuto.
   * `cq:design_dialog (nt:unstructured)` - Modifica di progettazione per questo componente

#### Icona componente {#component-icon}

L’icona o l’abbreviazione del componente viene definita tramite le proprietà JCR del componente quando il componente viene creato dallo sviluppatore. Tali proprietà vengono valutate nell&#39;ordine seguente e viene utilizzata la prima proprietà valida trovata.

1. `cq:icon` - Proprietà String che punta a un&#39;icona standard nella libreria  [Coral UI ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) da visualizzare nel browser dei componenti
   * Utilizzate il valore dell&#39;attributo HTML dell&#39;icona Corallo.
1. `abbreviation` - Proprietà String per personalizzare l&#39;abbreviazione del nome del componente nel browser Componenti
   * L&#39;abbreviazione deve essere limitata a due caratteri.
   * Se si specifica una stringa vuota, l&#39;abbreviazione verrà generata dai primi due caratteri della proprietà `jcr:title`.
      * Ad esempio &quot;Im&quot; per &quot;Image&quot;
      * Il titolo localizzato verrà utilizzato per creare l’abbreviazione.
   * L&#39;abbreviazione viene tradotta solo se il componente dispone di una proprietà `abbreviation_commentI18n`, che viene quindi utilizzata come hint di traduzione.
1. `cq:icon.png` o  `cq:icon.svg` - Icona per questo componente, visualizzata nel browser Componenti
   * 20 x 20 pixel è la dimensione delle icone dei componenti standard.
      * Le icone più grandi verranno ridotte (lato client).
   * Il colore consigliato è rgb(112, 112, 112) > #707070
   * Lo sfondo delle icone dei componenti standard è trasparente.
   * Sono supportati solo i file `.png` e `.svg`.
   * Se si importa dal file system tramite il plug-in Eclipse, i nomi dei file devono essere preceduti, ad esempio, da un carattere di escape come `_cq_icon.png` o `_cq_icon.svg`.
   * `.png` ha un precedente su  `.svg` se entrambi sono presenti.

Se sul componente non viene trovata nessuna delle proprietà di cui sopra (`cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`):

* Il sistema cercherà le stesse proprietà sui super componenti che seguono la proprietà `sling:resourceSuperType`.
* Se a livello di super componente non viene trovata alcuna abbreviazione o un&#39;abbreviazione vuota, il sistema genererà l&#39;abbreviazione dalle prime lettere della proprietà `jcr:title` del componente corrente.

Per annullare l&#39;ereditarietà delle icone dai super componenti, l&#39;impostazione di una proprietà vuota `abbreviation` sul componente ripristina il comportamento predefinito.

La [console dei componenti](/help/sites-cloud/authoring/features/components-console.md#component-details) mostra come viene definita l&#39;icona di un particolare componente.

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

Molti dei nodi/proprietà necessari per definire un componente sono comuni a entrambe le interfacce e le differenze rimangono indipendenti, in modo che il componente possa funzionare in entrambi gli ambienti.

Un componente è un nodo di tipo `cq:Component` con le seguenti proprietà e nodi secondari:

| Nome | Tipo | Descrizione |
|---|---|---|
| `.` | `cq:Component` | Rappresenta il componente corrente. Un componente è di tipo nodo `cq:Component`. |
| `componentGroup` | `String` | Rappresenta il gruppo in base al quale il componente può essere selezionato nel [Browser componenti.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) Un valore che inizia con  `.` è utilizzato per i componenti che non sono disponibili per la selezione dall’interfaccia utente, ad esempio i componenti di base da cui ereditano altri componenti. |
| `cq:isContainer` | `Boolean` | Indica se il componente è un componente contenitore e può quindi contenere altri componenti, ad esempio un sistema paragrafo. |
| `cq:dialog` | `nt:unstructured` | Definizione della finestra di dialogo di modifica per il componente. |
| `cq:design_dialog` | `nt:unstructured` | Questa è la definizione della finestra di dialogo della progettazione per il componente. |
| `cq:editConfig` | `cq:EditConfig` | Definisce la [configurazione di modifica del componente.](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | Questo restituisce attributi di tag aggiuntivi aggiunti al tag HTML circostante. Consente l&#39;aggiunta di attributi ai div generati automaticamente. |
| `cq:noDecoration` | `Boolean` | Se true, il rendering del componente non viene eseguito con classi div e css generate automaticamente. |
| `cq:template` | `nt:unstructured` | Se trovato, questo nodo verrà utilizzato come modello di contenuto quando il componente viene aggiunto dal Browser componenti. |
| `jcr:created` | `Date` | Data di creazione del componente. |
| `jcr:description` | `String` | Descrizione del componente. |
| `jcr:title` | `String` | Titolo del componente. |
| `sling:resourceSuperType` | `String` | Quando è impostato, il componente eredita da questo componente. |
| `component.html` | `nt:file` | Questo è il file di script HTL del componente. |
| `cq:icon` | `String` | Questo valore punta all&#39;icona [del componente](#component-icon) e viene visualizzato nel browser Componenti. |

Se osserviamo il componente **Text**, è possibile vedere una serie di elementi:

![Struttura componente testo](assets/components-text.png)

Le proprietà di particolare interesse comprendono:

* `jcr:title` - Titolo del componente usato per identificare il componente nel Browser componenti.
* `jcr:description` - Descrizione del componente.
* `sling:resourceSuperType` - Indica il percorso di ereditarietà quando si estende un componente (sostituendo una definizione).

I nodi secondari di particolare interesse includono:

* `cq:editConfig` - Consente di controllare gli aspetti visivi del componente durante la modifica.
* `cq:dialog` - Definisce la finestra di dialogo per la modifica del contenuto di questo componente.
* `cq:design_dialog` - Specifica le opzioni di modifica della progettazione per il componente.

### Finestre di dialogo {#dialogs}

Le finestre di dialogo sono un elemento chiave del componente in quanto forniscono agli autori un’interfaccia per configurare il componente in una pagina di contenuto e fornire l’input per tale componente. Per informazioni dettagliate sulle interazioni tra autori di contenuti e componenti, consultate la [documentazione sull&#39;authoring](/help/sites-cloud/authoring/fundamentals/editing-content.md).

A seconda della complessità del componente, la finestra di dialogo può richiedere una o più schede.

Finestre di dialogo per AEM componenti:

* Sono nodi `cq:dialog` di tipo `nt:unstructured`.
* Si trovano sotto i nodi `cq:Component` e accanto alle relative definizioni di componenti.
* Definire la finestra di dialogo per la modifica del contenuto di questo componente.
* Sono definiti utilizzando i componenti dell’interfaccia Granite.
* Viene eseguito il rendering lato server (come componenti Sling), in base alla struttura del contenuto e alla proprietà `sling:resourceType`.
* Contiene una struttura di nodi che descrive i campi all’interno della finestra di dialogo
   * Questi nodi sono `nt:unstructured` con la proprietà `sling:resourceType` richiesta.

![Definizione finestra di dialogo del componente titolo](assets/components-title-dialog.png)

All’interno della finestra di dialogo, sono definiti i singoli campi:

![Campi della finestra di dialogo definizione del componente Titolo](assets/components-title-dialog-items.png)

### Finestre di dialogo di progettazione {#design-dialogs}

Le finestre di dialogo Progettazione sono simili alle finestre di dialogo utilizzate per modificare e configurare il contenuto, ma forniscono agli autori dei modelli l’interfaccia per la proconfigurazione e fornire dettagli di progettazione per quel componente in un modello di pagina. I modelli di pagina vengono quindi utilizzati dagli autori dei contenuti per creare pagine di contenuto. Per informazioni dettagliate sulla creazione dei modelli, consultate la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md).

[Le finestre di dialogo Progettazione vengono utilizzate per modificare un modello](/help/sites-cloud/authoring/features/templates.md) di pagina, anche se non sono necessarie per tutti i componenti. Ad esempio, i **Titolo** e **Componenti immagine** sono entrambi dotati di finestre di dialogo di progettazione, mentre il **Componente di condivisione social media** non lo è.

### Interfaccia utente Coral e interfaccia Granite {#coral-and-granite}

L’interfaccia utente Coral e l’interfaccia utente Granite definiscono l’aspetto e il comportamento dei AEM.

* [L’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) interfaccia utente Coral fornisce un’interfaccia utente coerente in tutte le soluzioni cloud.
* [L’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) interfaccia utente Granite fornisce la marcatura Coral dell’interfaccia utente inclusa nei componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente.

L’interfaccia utente Granite offre una vasta gamma di widget di base per creare la finestra di dialogo nell’ambiente di authoring. Se necessario potete estendere questa selezione e creare un widget personalizzato.

Per ulteriori dettagli, consulta le risorse seguenti:

* [Guida all’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)
* [Documentazione di Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
* [Struttura dell’interfaccia AEM](/help/implementing/developing/introduction/ui-structure.md)

### Personalizzazione dei campi di dialogo {#customizing-dialog-fields}

>[!TIP]
>
>Vedere la [sessione AEM Gems](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) sulla personalizzazione dei campi di dialogo.

Per creare un nuovo widget da usare in una finestra di dialogo dei componenti, è necessario creare un nuovo componente Campo interfaccia Granite.

Se si considera la finestra di dialogo come un semplice contenitore per un elemento modulo, è anche possibile visualizzare il contenuto principale del contenuto della finestra di dialogo come campi modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa; equivale a creare un nuovo componente. Per facilitare l&#39;esecuzione di tale attività, l&#39;interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Più specificamente, l&#39;interfaccia utente Granite offre una serie di componenti campo adatti per l&#39;uso nelle finestre di dialogo, o più in generale parlando in [moduli.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

Dopo aver creato il tipo di risorsa, è possibile creare un&#39;istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` che fa riferimento al tipo di risorsa appena introdotto.

#### Accesso ai campi di dialogo {#access-to-dialog-fields}

Potete anche utilizzare le condizioni di rendering (`rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo; ad esempio:

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## Uso dei componenti {#using-components}

Dopo aver creato un componente, è necessario attivarlo per poterlo usare. Il suo utilizzo mostra come la struttura del componente si collega alla struttura del contenuto risultante nell’archivio.

### Aggiunta del componente al modello {#adding-your-component-to-the-template}

Una volta definito, il componente deve essere reso disponibile per l’uso. Per rendere un componente disponibile per l’uso in un modello, è necessario attivarlo nel criterio del Contenitore di layout del modello.

Per informazioni dettagliate sulla creazione dei modelli, consultate la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md).

### Componenti e contenuti creati {#components-and-the-content-they-create}

Se si crea e si configura un&#39;istanza del componente **Titolo** sulla pagina: `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![Finestra di dialogo di modifica del titolo](assets/components-title-dialog.png)

Potete quindi visualizzare la struttura del contenuto creato all’interno della directory archivio:

![Struttura nodo componente titolo](assets/components-title-content-nodes.png)

In particolare, se si guarda il testo effettivo di un **Componente titolo**:

* Il contenuto contiene una proprietà `jcr:title` che contiene il testo effettivo del titolo immesso dall&#39;autore.
* Contiene inoltre un riferimento `sling:resourceType` alla definizione del componente.

Le proprietà definite dipendono dalle singole definizioni. Anche se possono essere più complessi di quanto non lo siano in precedenza, seguono comunque gli stessi principi di base.

## Gerarchia e ereditarietà dei componenti {#component-hierarchy-and-inheritance}

I componenti all&#39;interno di AEM sono soggetti alla **Gerarchia dei tipi di risorse**. Viene utilizzato per estendere i componenti utilizzando la proprietà `sling:resourceSuperType`. Questo consente al componente di ereditare da un altro componente.

Per ulteriori informazioni, vedere la sezione [Riutilizzo di componenti](#reusing-components).

## Modifica comportamento {#edit-behavior}

In questa sezione viene illustrato come configurare il comportamento di modifica di un componente. Questo include attributi come le azioni disponibili per il componente, le caratteristiche dell’editor in.place e i listener relativi agli eventi sul componente.

Il comportamento di modifica di un componente è configurato aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi secondari. Sono disponibili le seguenti proprietà e nodi secondari:

* `cq:editConfig` proprietà node
* [`cq:editConfig` nodi](#configuring-with-cq-editconfig-child-nodes) secondari:
   * `cq:dropTargets` (tipo di nodo  `nt:unstructured`): Definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa di Content Finder (è consentita una singola destinazione di rilascio)
   * `cq:inplaceEditing` (tipo di nodo  `cq:InplaceEditingConfig`): definisce una configurazione di modifica diretta per il componente
   * `cq:listeners` (tipo di nodo  `cq:EditListenersConfig`): definisce cosa accade prima o dopo un’azione sul componente

Esistono molte configurazioni in AEM. È possibile cercare facilmente proprietà specifiche o nodi secondari utilizzando lo strumento Query in **CRXDE Lite**.

### Segnaposto componente {#component-placeholders}

I componenti devono sempre eseguire il rendering di codice HTML visibile all’autore, anche quando il componente non ha contenuto. In caso contrario, potrebbe scomparire visivamente dall&#39;interfaccia dell&#39;editor, rendendola tecnicamente presente ma invisibile sulla pagina e nell&#39;editor. In tal caso, gli autori non potranno selezionare e interagire con il componente vuoto.

Per questo motivo, i componenti devono eseguire il rendering di un segnaposto purché non rendano alcun output visibile quando la pagina viene sottoposta a rendering nell&#39;editor pagina (quando la modalità WCM è `edit` o `preview`).
La marcatura HTML tipica di un segnaposto è la seguente:

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

Lo script HTL tipico che esegue il rendering del codice HTML segnaposto riportato sopra è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

Nell&#39;esempio precedente, `isEmpty` è una variabile che è vera solo quando il componente non ha contenuto ed è invisibile all&#39;autore.

Per evitare ripetizioni,  Adobe consiglia agli implementatori di componenti di utilizzare un modello HTL per questi segnaposto, [come quello fornito dai componenti core.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

L’utilizzo del modello nel collegamento precedente viene quindi effettuato con la seguente riga di HTL:

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

Nell&#39;esempio precedente, `model.text` è la variabile che è true solo quando il contenuto ha contenuto ed è visibile.

Un esempio di utilizzo di questo modello può essere visualizzato nei componenti core, [come nel componente titolo.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### Configurazione con cq:EditConfig Child Nodes {#configuring-with-cq-editconfig-child-nodes}

#### Trascinamento delle risorse in una finestra di dialogo - cq:dropTargets {#cq-droptargets}

Il nodo `cq:dropTargets` (tipo di nodo `nt:unstructured`) definisce la destinazione di rilascio che può accettare un rilascio da una risorsa trascinata da Content Finder. È un nodo di tipo `cq:DropTargetConfig`.

Il nodo figlio di tipo `cq:DropTargetConfig` definisce una destinazione di rilascio nel componente.

### Modifica diretta - cq:inplaceEditing {#cq-inplaceediting}

Un editor locale consente all&#39;utente di modificare i contenuti direttamente nel flusso di contenuti, senza dover aprire una finestra di dialogo. Ad esempio, i componenti standard **Text** e **Title** dispongono entrambi di un editor in-lace.

Un editor locale non è necessario/significativo per ogni tipo di componente.

Il nodo `cq:inplaceEditing` (tipo di nodo `cq:InplaceEditingConfig`) definisce una configurazione di modifica diretta per il componente. Può avere le seguenti proprietà:

| Nome proprietà | Tipo proprietà | Valore proprietà |
|---|---|---|
| `active` | `Boolean` | `true` per abilitare la modifica diretta del componente. |
| `configPath` | `String` | Percorso della configurazione dell&#39;editor, che può essere specificato da un nodo di configurazione |
| `editorType` | `String` | I tipi disponibili sono: `plaintext` per i contenuti non HTML, `title` converte i titoli grafici in un testo normale prima dell&#39;inizio della modifica e `text` utilizza l&#39;editor Rich Text |

La seguente configurazione abilita la modifica in locale del componente e definisce `plaintext` come tipo di editor:

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### Gestione degli eventi dei campi - cq:listener {#cq-listeners}

Il metodo di gestione degli eventi nei campi di dialogo viene eseguito con i listener in una [libreria client personalizzata.](/help/implementing/developing/introduction/clientlibs.md)

Per inserire la logica nel campo, è necessario:

* Il campo deve essere contrassegnato con una determinata classe CSS (il gancio).
* Definite nella libreria client un listener JS collegato al nome della classe CSS (in questo modo la logica personalizzata viene limitata al campo e non influisce sugli altri campi dello stesso tipo).

Per ottenere questo risultato è necessario conoscere la libreria di widget sottostante con cui si desidera interagire. [Consultate la ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) documentazione dell’interfaccia utente Coral per identificare l’evento a cui intendete reagire.

Il nodo `cq:listeners` (tipo di nodo `cq:EditListenersConfig`) definisce cosa accade prima o dopo un&#39;azione sul componente. Nella tabella seguente sono definite le proprietà possibili.

| Nome proprietà | Valore proprietà |
|---|---|
| `beforedelete` | Il gestore viene attivato prima della rimozione del componente. |
| `beforeedit` | Il gestore viene attivato prima della modifica del componente. |
| `beforecopy` | Il gestore viene attivato prima della copia del componente. |
| `beforeremove` | Il gestore viene attivato prima dello spostamento del componente. |
| `beforeinsert` | Il gestore viene attivato prima dell&#39;inserimento del componente. |
| `beforechildinsert` | Il gestore viene attivato prima che il componente venga inserito in un altro componente (solo contenitori). |
| `afterdelete` | Il gestore viene attivato dopo la rimozione del componente. |
| `afteredit` | Il gestore viene attivato dopo la modifica del componente. |
| `aftercopy` | Il gestore viene attivato dopo la copia del componente. |
| `afterinsert` | Il gestore viene attivato dopo l&#39;inserimento del componente. |
| `aftermove` | Il gestore viene attivato dopo lo spostamento del componente. |
| `afterchildinsert` | Il gestore viene attivato dopo che il componente è stato inserito in un altro componente (solo contenitori). |

>[!NOTE]
>
>Nel caso di componenti nidificati, esistono alcune limitazioni alle azioni definite come proprietà sul nodo `cq:listeners`. Per i componenti nidificati, i valori delle seguenti proprietà **devono essere**:`REFRESH_PAGE`
>
>* `aftermove`
>* `aftercopy`


Il gestore eventi può essere implementato con un&#39;implementazione personalizzata. Ad esempio (dove `project.customerAction` è un metodo statico):

`afteredit = "project.customerAction"`

L&#39;esempio seguente è equivalente alla configurazione `REFRESH_INSERTED`:

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

### Convalida del campo {#field-validation}

La convalida dei campi nell&#39;interfaccia utente Granite e nei widget dell&#39;interfaccia utente Granite viene eseguita utilizzando l&#39;API `foundation-validation`. Per informazioni, consultare la [`foundation-valdiation` documentazione Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html).

### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se si dispone di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare l&#39;evento `dialog-ready`.

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, il che significa che ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per collegare in JavaScript codice personalizzato che esegue personalizzazioni sui campi all&#39;interno di una finestra di dialogo o attività simili.

## Comportamento anteprima {#preview-behavior}

Il cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) viene impostato quando si passa alla modalità Anteprima anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibile alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico, quindi basarsi sul valore del cookie.

## Documentazione dei componenti {#documenting-components}

Gli sviluppatori desiderano un accesso semplice alla documentazione del componente per comprendere rapidamente i componenti:

* Descrizione
* Uso previsto
* Struttura del contenuto e proprietà
* API e punti di estensione esposti
* Ecc.

Per questo motivo, è abbastanza semplice rendere disponibile qualsiasi marcatura della documentazione esistente all’interno del componente stesso.

È sufficiente inserire un file `README.md` nella struttura del componente.

![README.md nella struttura del componente](assets/components-documentation.png)

Questa sezione verrà visualizzata nella [console dei componenti.](/help/sites-cloud/authoring/features/components-console.md)

![README.md visibile nella console Componenti](assets/components-documentation-console.png)

La riduzione supportata è la stessa per i frammenti di contenuto [.](/help/assets/content-fragments/content-fragments.md)