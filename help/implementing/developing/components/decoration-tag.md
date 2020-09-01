---
title: Tag Decoration
description: Quando viene eseguito il rendering di un componente in una pagina Web, è possibile generare un elemento HTML che racchiude il componente renderizzato all’interno di se stesso. Per gli sviluppatori, AEM offre una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti inclusi.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---


# Tag Decoration {#decoration-tag}

Quando viene eseguito il rendering di un componente in una pagina Web, è possibile generare un elemento HTML che racchiude il componente renderizzato all’interno di se stesso. Ciò ha principalmente due finalità:

* Un componente può essere modificato solo se è racchiuso con un elemento HTML.
* L&#39;elemento wrapping viene utilizzato per applicare classi HTML che forniscono:
   * Informazioni sul layout
   * Informazioni sullo stile

Per gli sviluppatori, AEM offre una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti inclusi. Se e come viene rappresentato il tag di decorazione è definito dalla combinazione di due fattori, che questa pagina illustrerà:

* Il componente stesso può configurare il tag decorazione con un set di proprietà.
* Gli script che includono componenti possono definire gli aspetti del tag decorazione con parametri di inclusione.

## Consigli {#recommendations}

Di seguito sono riportate alcune raccomandazioni generali su quando includere l&#39;elemento wrapper che dovrebbe aiutare a evitare di correre in problemi imprevisti:

* La presenza dell’elemento wrapper non deve essere diversa tra WCMModes (modalità di modifica o anteprima), istanze (autore o pubblicazione) o ambiente (fase di pubblicazione o produzione), in modo che i CSS e JavaScript della pagina funzionino in modo identico in tutti i casi.
* L’elemento wrapper deve essere aggiunto a tutti i componenti modificabili, in modo che l’editor pagina possa inizializzarli e aggiornarli correttamente.
* Per i componenti non modificabili, l&#39;elemento wrapper può essere evitato se non svolge alcuna funzione particolare, in modo che il markup risultante non sia necessariamente gonfiato.

## Controlli per componenti {#component-controls}

Le proprietà e i nodi seguenti possono essere applicati ai componenti per controllare il comportamento del relativo tag di decorazione:

* **`cq:noDecoration {boolean}`:** Questa proprietà può essere aggiunta a un componente e un valore vero forza AEM non generare alcun elemento wrapper sul componente.
* **`cq:htmlTag`node:** Questo nodo può essere aggiunto sotto un componente e può avere le seguenti proprietà:
   * **`cq:tagName {String}`:** Questo può essere utilizzato per specificare un tag HTML personalizzato da utilizzare per racchiudere i componenti al posto dell&#39;elemento DIV predefinito.
   * **`class {String}`:** Può essere utilizzato per specificare i nomi delle classi css da aggiungere al wrapper.
   * Altri nomi di proprietà saranno aggiunti come attributi HTML con lo stesso valore String fornito.

## Controlli script {#script-controls}

In generale, il comportamento del wrapper in HTL può essere riassunto come segue:

* Per impostazione predefinita non viene eseguito il rendering di alcun DIV per wrapper (solo durante l’operazione `data-sly-resource="foo"`).
* Tutte le modalità wcm (disabilitate, visualizzate in anteprima, modificate sia l’autore che la pubblicazione) vengono sottoposte a rendering nello stesso modo.

Il comportamento del wrapper può anche essere controllato completamente.

* Lo script HTL ha il controllo completo sul comportamento risultante del tag wrapper.
* Le proprietà del componente (come `cq:noDecoration` e `cq:tagName`) possono anche definire il tag wrapper.

È possibile controllare completamente il comportamento dei tag wrapper dagli script HTL e la relativa logica.

Per ulteriori informazioni sullo sviluppo in HTL consultate la documentazione [](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html)HTL.

### Albero decisionale {#decision-tree}

Questa struttura decisionale riepiloga la logica che determina il comportamento dei tag wrapper.

![Albero decisionale](assets/decoration-tag-decision-tree.png)

### Use Cases {#use-cases}

I tre esempi di utilizzo riportati di seguito illustrano come vengono gestiti i tag wrapper e come è semplice controllare il comportamento desiderato dei tag wrapper.

Tutti gli esempi che seguono si basano sulla seguente struttura di contenuto e componenti:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Caso d’uso 1: Includi un componente per il riutilizzo del codice {#use-case-include-a-component-for-code-reuse}

Il caso d’uso più tipico è quello in cui un componente include un altro componente per motivi di riutilizzo del codice. In tal caso, il componente incluso non è desiderato per essere modificabile con una propria barra degli strumenti e una propria finestra di dialogo, pertanto non è necessario alcun wrapper e il componente `cq:htmlTag` verrà ignorato. Questo può essere considerato il comportamento predefinito.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`Hello World!`**

Un esempio potrebbe essere un componente che include un componente immagine di base per visualizzare un’immagine, in genere utilizzando una risorsa sintetica, che consiste nell’includere un componente figlio virtuale trasmettendo a una risorsa semplice di dati un oggetto Mappa che rappresenta tutte le proprietà del componente.

#### Caso d’uso 2: Includi un componente modificabile {#use-case-include-an-editable-component}

Un altro esempio di utilizzo comune è rappresentato dai componenti contenitore che includono componenti secondari modificabili, come un Contenitore di layout. In questo caso, ogni bambino incluso ha bisogno di un wrapper per il funzionamento dell&#39;editor (a meno che non sia esplicitamente disabilitato con la `cq:noDecoration` proprietà).

Poiché in questo caso il componente incluso è un componente indipendente, per il funzionamento dell’editor è necessario un elemento wrapper e per definire il layout e lo stile da applicare. Per attivare questo comportamento, è disponibile l&#39; `decoration=true` opzione.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso d’uso 3: Comportamento personalizzato {#use-case-custom-behavior}

Può esserci un certo numero di casi complessi, che possono essere facilmente raggiunti dalla possibilità di HTL di fornire esplicitamente:

* **`decorationTagName='ELEMENT_NAME'`** Per definire il nome dell&#39;elemento del wrapper.
* **`cssClassName='CLASS_NAME'`** Per definire i nomi delle classi CSS da impostare.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Output risultante `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**
