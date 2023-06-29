---
title: Guida di riferimento dei componenti
description: Guida di riferimento per sviluppatori per i dettagli dei componenti e della loro struttura
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '3650'
ht-degree: 2%

---

# Guida di riferimento dei componenti {#components-reference-guide}

I componenti sono al centro della creazione di un’esperienza nell’AEM. Il [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) semplificate l&#39;utilizzo di un set di strumenti con componenti robusti e pronti. Il [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) spiega allo sviluppatore come utilizzare questi strumenti e come creare componenti personalizzati per creare un sito AEM.

>[!TIP]
>
>Prima di fare riferimento a questo documento, assicurati di aver completato [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e hanno quindi familiarità con [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Archetipo progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)

Poiché l’esercitazione WKND copre la maggior parte dei casi d’uso, questo documento è inteso solo come supplemento a tali risorse. Fornisce informazioni tecniche approfondite sulla struttura e la configurazione dei componenti in AEM e non intende essere una guida introduttiva.

## Panoramica {#overview}

Questa sezione descrive concetti e problemi chiave come introduzione ai dettagli necessari per lo sviluppo di componenti personalizzati.

### Pianificazione {#planning}

Prima di iniziare a configurare o codificare il componente, è necessario chiedere:

* Cosa devi fare esattamente con il nuovo componente?
* È necessario creare il componente da zero o è possibile ereditare le nozioni di base da un componente esistente?
* Il componente richiederà logica per selezionare/manipolare il contenuto?
   * La logica deve essere tenuta separata dal livello dell&#39;interfaccia utente. HTL è progettato per garantire che questo accada.
* Il componente avrà bisogno della formattazione CSS?
   * La formattazione CSS deve essere mantenuta separata dalle definizioni dei componenti. Definisci le convenzioni per la denominazione degli elementi HTML in modo da poterli modificare tramite file CSS esterni.
* Quali implicazioni per la sicurezza può presentare il nuovo componente?

### Riutilizzo dei componenti esistenti {#reusing-components}

Prima di dedicare tempo alla creazione di un componente completamente nuovo, è consigliabile personalizzare o estendere i componenti esistenti. [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) offre una suite di componenti flessibili, robusti e testati pronti per la produzione.

#### Estensione dei Componenti core {#extending-core-components}

I Componenti core offrono anche [cancella modelli di personalizzazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=it) che puoi utilizzare per adattarle alle esigenze del tuo progetto.

#### Sovrapposizione di componenti {#overlying-components}

I componenti possono essere ridefiniti anche con [sovrapposizione](/help/implementing/developing/introduction/overlays.md) in base alla logica del percorso di ricerca. Tuttavia, in tal caso, [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) non verrà attivato e `/apps` deve definire l’intera sovrapposizione.

#### Estensione delle finestre di dialogo dei componenti {#extending-component-dialogs}

È inoltre possibile modificare la finestra di dialogo di un componente utilizzando Sling Resource Merger e definendo la proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l’intera finestra di dialogo.

### Logica dei contenuti e markup di rendering  {#content-logic-and-rendering-markup}

Viene eseguito il rendering del componente con [HTML](https://www.w3schools.com/htmL/html_intro.asp). Il componente deve definire le HTML necessarie per acquisire il contenuto richiesto e quindi eseguirne il rendering come richiesto, sia nell’ambiente di authoring che in quello di pubblicazione.

Si consiglia di mantenere il codice responsabile del markup e del rendering separato dal codice che controlla la logica utilizzata per selezionare il contenuto del componente.

Questa filosofia è supportata da [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it): linguaggio per modelli appositamente limitato per garantire che venga utilizzato un linguaggio di programmazione reale per definire la logica di business sottostante. Questo meccanismo evidenzia il codice chiamato per una determinata vista e, se necessario, consente una logica specifica per diverse viste dello stesso componente.

Questa logica (facoltativa) può essere implementata in diversi modi e viene richiamata da HTL con comandi specifici:

* Utilizzo di Java - [Java Use-API per HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html) abilita un file HTL per accedere a metodi helper in una classe Java personalizzata. Questo consente di utilizzare il codice Java per implementare la logica per selezionare e configurare il contenuto del componente.
* Utilizzo di JavaScript - [JavaScript Use-API per HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) abilita un file HTL per accedere a codice helper scritto in JavaScript. Questo consente di utilizzare il codice JavaScript per implementare la logica per selezionare e configurare il contenuto del componente.
* Utilizzo delle librerie lato client: i siti web moderni si basano in larga misura sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. Consulta il documento [Utilizzo di librerie lato client su AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md) per ulteriori informazioni.

## Struttura dei componenti {#structure}

La struttura di una componente AEM è potente e flessibile. Le parti principali sono:

* [Tipo risorsa](#resource-type)
* [Definizione componente](#component-definition)
* [Proprietà e nodi figlio di un componente](#properties-and-child-nodes-of-a-component)
* [Finestre di dialogo](#dialogs)
* [Finestre di dialogo per progettazione](#design-dialogs)

### Tipo risorsa {#resource-type}

Un elemento chiave della struttura è il tipo di risorsa.

* La struttura del contenuto dichiara le intenzioni.
* Il tipo di risorsa li implementa.

Si tratta di un’astrazione che aiuta a garantire che, anche quando l’aspetto cambia nel tempo, l’intenzione rimanga nel tempo.

### Definizione componente {#component-definition}

La definizione di un componente può essere suddivisa come segue:

* I componenti AEM si basano su [Sling.](https://sling.apache.org/documentation.html)
* I componenti dell’AEM si trovano sotto `/libs/core/wcm/components`.
* I componenti specifici del progetto/sito si trovano in `/apps/<myApp>/components`.
* I componenti standard dell’AEM sono definiti come `cq:Component` e avere gli elementi chiave:
   * Proprietà jcr: elenco di proprietà jcr. Queste sono variabili e alcune possono essere facoltative, anche se la struttura di base di un nodo componente, le sue proprietà e i sottonodi sono definiti da `cq:Component` definizione.
   * Risorse: definiscono gli elementi statici utilizzati dal componente.
   * Script: vengono utilizzati per implementare il comportamento dell’istanza risultante del componente.

#### Proprietà vitali {#vital-properties}

* **Nodo principale**:
   * `<mycomponent> (cq:Component)` - Nodo gerarchico del componente.
* **Proprietà vitali**:
   * `jcr:title` - Titolo del componente; ad esempio, utilizzato come etichetta quando il componente è elencato in [Browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) e [Console Componenti](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description` - Descrizione del componente; utilizzata come suggerimento del mouse nella console Browser componenti e Componenti
   * Consulta la sezione [Icona componente](#component-icon) per i dettagli
* **Nodi figlio vitali**:
   * `cq:editConfig (cq:EditConfig)` - Definisce le proprietà di modifica del componente e ne attiva la visualizzazione nel browser Componenti
      * Se il componente ha una finestra di dialogo, questa viene visualizzata automaticamente nel browser Componenti o nel Sidekick, anche se cq:editConfig non esiste.
   * `cq:childEditConfig (cq:EditConfig)` - Controlla gli aspetti dell’interfaccia utente di authoring per i componenti secondari che non definiscono i propri `cq:editConfig`.
   * `cq:dialog (nt:unstructured)` - Finestra di dialogo per questo componente. Definisce l’interfaccia che consente all’utente di configurare il componente e/o modificare il contenuto.
   * `cq:design_dialog (nt:unstructured)` - Modifica del design di questo componente

#### Icona componente {#component-icon}

L’icona o l’abbreviazione del componente viene definita tramite le proprietà JCR del componente quando questo viene creato dallo sviluppatore. Queste proprietà vengono valutate nell&#39;ordine seguente e viene utilizzata la prima proprietà valida trovata.

1. `cq:icon` : proprietà stringa che punta a un&#39;icona standard nella [Libreria interfaccia utente Coral](https://opensource.adobe.com/coral-spectrum/examples/#icon) da visualizzare nel browser componenti
   * Utilizza il valore dell’attributo HTML dell’icona Coral.
1. `abbreviation` - Proprietà stringa per personalizzare l&#39;abbreviazione del nome del componente nel browser componenti
   * L’abbreviazione deve essere limitata a due caratteri.
   * Specificando una stringa vuota, verrà creata l’abbreviazione a partire dai primi due caratteri della `jcr:title` proprietà.
      * Ad esempio, &quot;Im&quot; per &quot;Immagine&quot;
      * Il titolo localizzato viene utilizzato per creare l’abbreviazione.
   * L’abbreviazione viene tradotta solo se il componente ha un `abbreviation_commentI18n` , che viene quindi utilizzata come suggerimento di traduzione.
1. `cq:icon.png` o `cq:icon.svg` : icona per questo componente, che viene visualizzata nel browser Componenti
   * 20 x 20 pixel sono le dimensioni delle icone dei componenti standard.
      * Le icone più grandi vengono ridimensionate (lato client).
   * Il colore consigliato è rgb(112, 112, 112) > #707070
   * Lo sfondo delle icone dei componenti standard è trasparente.
   * Solo `.png` e `.svg` sono supportati.
   * Se si importa dal file system tramite il plug-in Eclipse, i nomi dei file devono essere preceduti come `_cq_icon.png` o `_cq_icon.svg` ad esempio.
   * `.png` ha precedenza su `.svg` se sono presenti entrambi.

Se nessuna delle proprietà precedenti (`cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`) si trovano nel componente:

* Il sistema cercherà le stesse proprietà sui super componenti seguendo la `sling:resourceSuperType` proprietà.
* Se a livello di super componente non viene trovato nulla o un’abbreviazione vuota, il sistema crea l’abbreviazione dalle prime lettere del `jcr:title` del componente corrente.

Per annullare l’ereditarietà delle icone dai super componenti, imposta un valore vuoto `abbreviation` sul componente verrà ripristinato il comportamento predefinito.

Il [Console Componenti](/help/sites-cloud/authoring/features/components-console.md#component-details) mostra come viene definita l’icona di un particolare componente.

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

### Proprietà e nodi figlio di un componente {#properties-and-child-nodes-of-a-component}

Molti nodi/proprietà necessari per definire un componente sono comuni a entrambe le interfacce, con differenze che rimangono indipendenti in modo che il componente possa funzionare in entrambi gli ambienti.

Un componente è un nodo di tipo `cq:Component` e ha le seguenti proprietà e nodi secondari:

| Nome | Tipo | Descrizione |
|---|---|---|
| `.` | `cq:Component` | Rappresenta il componente corrente. Un componente è di tipo nodo `cq:Component`. |
| `componentGroup` | `String` | Rappresenta il gruppo in cui il componente può essere selezionato nella [Browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Un valore che inizia con `.` viene utilizzato per i componenti che non sono disponibili per la selezione dall’interfaccia utente, ad esempio i componenti di base da cui ereditano altri componenti. |
| `cq:isContainer` | `Boolean` | Indica se il componente è un componente contenitore e può quindi contenere altri componenti, ad esempio un sistema paragrafo. |
| `cq:dialog` | `nt:unstructured` | Questa è la definizione della finestra di dialogo per modifica del componente. |
| `cq:design_dialog` | `nt:unstructured` | Questa è la definizione della finestra di dialogo per progettazione del componente. |
| `cq:editConfig` | `cq:EditConfig` | Questo definisce il [modifica la configurazione del componente.](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | In questo modo vengono restituiti attributi di tag aggiuntivi che vengono aggiunti al tag HTML circostante. Abilita l’aggiunta di attributi ai div generati automaticamente. |
| `cq:noDecoration` | `Boolean` | Se true, il componente non viene renderizzato con le classi div e css generate automaticamente. |
| `cq:template` | `nt:unstructured` | Se individuato, questo nodo viene utilizzato come modello di contenuto quando il componente viene aggiunto dal browser Componenti. |
| `jcr:created` | `Date` | Data di creazione del componente. |
| `jcr:description` | `String` | Descrizione del componente. |
| `jcr:title` | `String` | Titolo del componente. |
| `sling:resourceSuperType` | `String` | Con questa impostazione, il componente eredita da questo componente. |
| `component.html` | `nt:file` | Questo è il file di script HTL del componente. |
| `cq:icon` | `String` | Questo valore punta al [icona del componente](#component-icon) e viene visualizzato nel browser Componenti. |

Se consideriamo il **Testo** componente, possiamo vedere una serie di questi elementi:

![Struttura dei componenti di testo](assets/components-text.png)

Le proprietà di particolare interesse comprendono:

* `jcr:title` : titolo del componente utilizzato per identificare il componente nel browser Componenti.
* `jcr:description` - Questa è la descrizione del componente.
* `sling:resourceSuperType` - Indica il percorso di ereditarietà quando si estende un componente (sovrascrivendo una definizione).

I nodi figlio di particolare interesse includono:

* `cq:editConfig` - Questa opzione controlla gli aspetti visivi del componente durante la modifica.
* `cq:dialog` : definisce la finestra di dialogo per la modifica del contenuto di questo componente.
* `cq:design_dialog` - Specifica le opzioni di modifica della progettazione per questo componente.

### Finestre di dialogo {#dialogs}

Le finestre di dialogo sono un elemento chiave del componente in quanto forniscono un’interfaccia che consente agli autori di configurare il componente in una pagina di contenuto e fornire input per tale componente. Consulta la [documentazione di authoring](/help/sites-cloud/authoring/fundamentals/editing-content.md) per informazioni dettagliate su come gli autori di contenuti interagiscono con i componenti.

A seconda della complessità del componente, la finestra di dialogo potrebbe richiedere una o più schede.

Finestre di dialogo per le componenti AEM:

* Sono `cq:dialog` nodi di tipo `nt:unstructured`.
* Si trovano sotto il loro `cq:Component` e accanto alle relative definizioni dei componenti.
* Definisci la finestra di dialogo per la modifica del contenuto di questo componente.
* Sono definiti utilizzando i componenti dell’interfaccia utente Granite.
* Viene eseguito il rendering lato server (come componenti Sling), in base alla struttura del contenuto e al `sling:resourceType` proprietà.
* Contengono una struttura di nodi che descrive i campi all’interno della finestra di dialogo
   * Questi nodi sono `nt:unstructured` con il necessario `sling:resourceType` proprietà.

![Definizione finestra di dialogo del componente Titolo](assets/components-title-dialog.png)

Nella finestra di dialogo sono definiti i singoli campi:

![Campi della definizione della finestra di dialogo del componente Titolo](assets/components-title-dialog-items.png)

### Finestre di dialogo per progettazione {#design-dialogs}

Le finestre di dialogo per progettazione sono simili alle finestre di dialogo utilizzate per modificare e configurare il contenuto, ma forniscono agli autori di modelli l’interfaccia per la pro-configurazione e i dettagli di progettazione per tale componente su un modello di pagina. I modelli di pagina vengono quindi utilizzati dagli autori dei contenuti per creare pagine di contenuto. Consulta la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md) per informazioni dettagliate sulla creazione dei modelli.

[Le finestre di dialogo per progettazione vengono utilizzate quando si modifica un modello di pagina](/help/sites-cloud/authoring/features/templates.md), anche se non sono necessari per tutti i componenti. Ad esempio, il **Titolo** e **Componenti immagine** entrambi dispongono di finestre di dialogo di progettazione, mentre **Componente condivisione social media** non lo fa.

### Coral UI e Granite UI {#coral-and-granite}

L’interfaccia utente Coral e Granite definiscono l’aspetto dell’AEM.

* [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) fornisce un’interfaccia utente coerente per tutte le soluzioni cloud.
* [Interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) fornisce il markup dell’interfaccia utente Coral racchiuso tra i componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente.

L’interfaccia utente Granite offre una vasta gamma di widget di base necessari per creare la finestra di dialogo nell’ambiente di authoring. Se necessario, puoi estendere questa selezione e creare un widget personalizzato.

Per ulteriori informazioni, consulta le seguenti risorse:

* [Struttura dell’interfaccia AEM](/help/implementing/developing/introduction/ui-structure.md)

### Personalizzazione dei campi della finestra di dialogo {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

Per creare un nuovo widget da utilizzare nella finestra di dialogo di un componente è necessario creare un nuovo componente campo dell’interfaccia utente Granite.

Se consideri la finestra di dialogo come un semplice contenitore per un elemento del modulo, puoi anche visualizzare il contenuto principale della finestra di dialogo come campi del modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa, il che equivale alla creazione di un nuovo componente. Per facilitare questa attività, l’interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Più precisamente, l’interfaccia utente Granite offre una serie di componenti di campo adatti all’utilizzo nelle finestre di dialogo o, più in generale, in [moduli.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

Dopo aver creato il tipo di risorsa, puoi creare un’istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` facendo riferimento al tipo di risorsa appena introdotto.

#### Accesso ai campi della finestra di dialogo {#access-to-dialog-fields}

È inoltre possibile utilizzare le condizioni di rendering (`rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo; ad esempio:

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## Utilizzo dei componenti {#using-components}

Dopo aver creato un componente, devi abilitarlo per utilizzarlo. Il suo utilizzo mostra come la struttura del componente è correlata alla struttura del contenuto risultante nell’archivio.

### Aggiunta del componente al modello {#adding-your-component-to-the-template}

Una volta definito, il componente deve essere reso disponibile per l’uso. Per rendere un componente disponibile per l’utilizzo in un modello, devi abilitarlo nel criterio del Contenitore di layout del modello.

Consulta la [documentazione del modello](/help/sites-cloud/authoring/features/templates.md) per informazioni dettagliate sulla creazione dei modelli.

### Componenti e contenuti creati {#components-and-the-content-they-create}

Se creiamo e configuriamo un’istanza di **Titolo** componente nella pagina: `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![Finestra di dialogo per modifica del titolo](assets/components-title-dialog.png)

Quindi possiamo vedere la struttura del contenuto creato all’interno dell’archivio:

![Struttura del nodo del componente Titolo](assets/components-title-content-nodes.png)

In particolare, se si considera il testo effettivo di un **Componente Titolo**:

* Il contenuto contiene un `jcr:title` proprietà contenente il testo effettivo del titolo immesso dall’autore.
* Contiene anche un `sling:resourceType` riferimento alla definizione del componente.

Le proprietà definite dipendono dalle singole definizioni. Anche se possono essere più complesse di quanto sopra, seguono comunque gli stessi principi di base.

## Gerarchia dei componenti ed ereditarietà {#component-hierarchy-and-inheritance}

I componenti dell’AEM sono soggetti agli **Gerarchia dei tipi di risorsa**. Viene utilizzato per estendere i componenti utilizzando la proprietà `sling:resourceSuperType`. Questo consente al componente di ereditare da un altro componente.

Consulta la sezione [Riutilizzo dei componenti](#reusing-components) per ulteriori informazioni.

## Modifica comportamento {#edit-behavior}

Questa sezione spiega come configurare il comportamento di modifica di un componente. Ciò include attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor in.place e i listener relativi agli eventi sul componente.

Il comportamento di modifica di un componente viene configurato aggiungendo un `cq:editConfig` nodo di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà e nodi secondari specifici. Sono disponibili le seguenti proprietà e nodi figlio:

* `cq:editConfig` proprietà nodo
* [`cq:editConfig` nodi secondari](#configuring-with-cq-editconfig-child-nodes):
   * `cq:dropTargets` (tipo di nodo `nt:unstructured`): definisce un elenco di destinazioni di rilascio che possono accettare un rilascio da una risorsa di content finder (è consentita una singola destinazione di rilascio)
   * `cq:inplaceEditing` (tipo di nodo `cq:InplaceEditingConfig`): definisce una configurazione per la modifica diretta del componente
   * `cq:listeners` (tipo di nodo `cq:EditListenersConfig`): definisce cosa accade prima o dopo che si verifica un’azione sul componente

Ci sono molte configurazioni esistenti nell&#39;AEM. Puoi cercare facilmente proprietà specifiche o nodi secondari utilizzando lo strumento Query in **CRXDE Lite**.

### Segnaposto Componente {#component-placeholders}

I componenti devono sempre eseguire il rendering di alcuni HTML visibili all’autore, anche quando il componente non ha contenuto. In caso contrario, potrebbe scomparire visivamente dall’interfaccia dell’editor, rendendolo tecnicamente presente ma invisibile nella pagina e nell’editor. In questo caso, gli autori non potranno selezionare e interagire con il componente vuoto.

Per questo motivo, i componenti devono eseguire il rendering di un segnaposto, a condizione che non eseguano il rendering di alcun output visibile quando si esegue il rendering della pagina nell’editor di pagine (quando la modalità WCM è `edit` o `preview`).
Il markup HTML tipico per un segnaposto è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

HTML Il tipico script HTL che esegue il rendering del segnaposto sopra riportato è il seguente:

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

Nell’esempio precedente, `isEmpty` è una variabile che è true solo quando il componente non ha contenuto ed è invisibile all’autore.

Per evitare ripetizioni, l’Adobe consiglia agli implementatori di componenti di utilizzare un modello HTL per questi segnaposto, [come quello fornito dai Componenti core.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

L’utilizzo del modello nel collegamento precedente viene quindi eseguito con la seguente riga di HTL:

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

Nell’esempio precedente, `model.text` è la variabile che è true solo quando il contenuto ha contenuto ed è visibile.

Un esempio di utilizzo di questo modello è disponibile nei Componenti core, [come nel componente Titolo.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### Configurazione con i nodi secondari cq:EditConfig {#configuring-with-cq-editconfig-child-nodes}

#### Eliminazione di risorse in una finestra di dialogo - cq:dropTargets {#cq-droptargets}

Il `cq:dropTargets` nodo (tipo di nodo) `nt:unstructured`) definisce la destinazione di rilascio in grado di accettare un rilascio da una risorsa trascinata da content finder. È un nodo di tipo `cq:DropTargetConfig`.

Nodo figlio di tipo `cq:DropTargetConfig` definisce una destinazione di rilascio nel componente.

### Modifica diretta - cq:inplaceEditing {#cq-inplaceediting}

Un editor locale consente all’utente di modificare il contenuto direttamente nel flusso di contenuto, senza dover aprire una finestra di dialogo. Ad esempio, lo standard **Testo** e **Titolo** entrambi i componenti dispongono di un editor locale.

Non è necessario/significativo un editor locale per ogni tipo di componente.

Il `cq:inplaceEditing` nodo (tipo di nodo) `cq:InplaceEditingConfig`) definisce una configurazione di modifica diretta per il componente. Può avere le seguenti proprietà:

| Nome proprietà | Tipo di proprietà | Valore proprietà |
|---|---|---|
| `active` | `Boolean` | `true` per abilitare la modifica diretta del componente. |
| `configPath` | `String` | Percorso della configurazione dell’editor, che può essere specificata da un nodo di configurazione |
| `editorType` | `String` | I tipi disponibili sono: `plaintext` per contenuti non HTML, `title` converte i titoli grafici in testo normale prima di iniziare la modifica e `text` utilizza l’Editor Rich Text |

La seguente configurazione abilita la modifica diretta del componente e definisce `plaintext` come tipo di editor:

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### Gestione degli eventi dei campi - cq:listeners {#cq-listeners}

Il metodo di gestione degli eventi sui campi della finestra di dialogo viene eseguito con i listener in un [libreria client](/help/implementing/developing/introduction/clientlibs.md).

Per inserire la logica nel campo, è necessario:

* Fai marcare il campo con una determinata classe CSS (l’hook).
* Definisci nella libreria client un listener JS collegato al nome di classe CSS (in modo che la logica personalizzata abbia ambito solo sul tuo campo e non influisca su altri campi dello stesso tipo).

A questo scopo, è necessario conoscere la libreria di widget sottostante con cui desideri interagire. [Consulta la documentazione sull’interfaccia utente Coral](https://opensource.adobe.com/coral-spectrum/documentation/) per identificare a quale evento desideri reagire.

Il `cq:listeners` nodo (tipo di nodo) `cq:EditListenersConfig`) definisce cosa accade prima o dopo un’azione sul componente. La tabella seguente definisce le proprietà possibili.

| Nome proprietà | Valore proprietà |
|---|---|
| `beforedelete` | Il gestore viene attivato prima della rimozione del componente. |
| `beforeedit` | L’handler viene attivato prima che il componente venga modificato. |
| `beforecopy` | L’handler viene attivato prima che il componente venga copiato. |
| `beforeremove` | L’handler viene attivato prima che il componente venga spostato. |
| `beforeinsert` | Il gestore viene attivato prima dell’inserimento del componente. |
| `beforechildinsert` | L’handler viene attivato prima che il componente venga inserito all’interno di un altro componente (solo contenitori). |
| `afterdelete` | Il gestore viene attivato dopo la rimozione del componente. |
| `afteredit` | Il gestore viene attivato dopo la modifica del componente. |
| `aftercopy` | Il gestore viene attivato dopo la copia del componente. |
| `afterinsert` | Il gestore viene attivato dopo l’inserimento del componente. |
| `aftermove` | Il gestore viene attivato dopo lo spostamento del componente. |
| `afterchildinsert` | L’handler viene attivato dopo che il componente è stato inserito all’interno di un altro componente (solo contenitori). |

>[!NOTE]
>
>Nel caso di componenti nidificati, esistono alcune restrizioni alle azioni definite come proprietà sul `cq:listeners` nodo. Per i componenti nidificati, i valori delle seguenti proprietà **deve** essere `REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`

Il gestore eventi può essere implementato con un’implementazione personalizzata. Ad esempio, (dove `project.customerAction` è un metodo statico):

`afteredit = "project.customerAction"`

L’esempio seguente è equivalente al `REFRESH_INSERTED` configurazione:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

Con la seguente configurazione la pagina viene aggiornata dopo che il componente è stato eliminato, modificato, inserito o spostato:

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### Convalida campo {#field-validation}

La convalida dei campi nell’interfaccia utente Granite e nei widget dell’interfaccia utente Granite viene eseguita utilizzando `foundation-validation` API. Consulta la [`foundation-valdiation` Documentazione di Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html) per i dettagli.

### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se disponi di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare `dialog-ready` evento.

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, ovvero ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per hook nel codice personalizzato JavaScript che esegue personalizzazioni sui campi all’interno di una finestra di dialogo o attività simili.

## Anteprima comportamento {#preview-behavior}

Il [Modalità WCM](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) Il cookie viene impostato quando si passa alla modalità Anteprima anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibili alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico e quindi basarsi sul valore del cookie.

## Documentazione dei componenti {#documenting-components}

In qualità di sviluppatore, desideri poter accedere facilmente alla documentazione dei componenti per comprendere rapidamente i relativi:

* Descrizione
* Uso previsto
* Struttura e proprietà del contenuto
* API e punti di estensione esposti
* Ecc.

Per questo motivo, è molto semplice creare qualsiasi markdown della documentazione esistente disponibile all’interno del componente stesso.

È sufficiente inserire un `README.md` nella struttura dei componenti.

![README.md nella struttura dei componenti](assets/components-documentation.png)

Questo markdown verrà quindi visualizzato nel [Console Componenti](/help/sites-cloud/authoring/features/components-console.md).

![README.md visibile nella console Componenti](assets/components-documentation-console.png)

Il markdown supportato è lo stesso di [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md).
