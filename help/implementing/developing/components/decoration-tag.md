---
title: Tag di decorazione
description: Quando viene eseguito il rendering di un componente in una pagina web, è possibile generare un elemento HTML che racchiude all’interno il componente renderizzato. AEM offre agli sviluppatori una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti.
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 8%

---

# Tag di decorazione {#decoration-tag}

Quando viene eseguito il rendering di un componente in una pagina web, è possibile generare un elemento HTML che racchiude all’interno il componente renderizzato. Questo serve principalmente a due scopi:

* Un componente può essere modificato solo quando è racchiuso in un elemento HTML.
* L’elemento wrapping viene utilizzato per applicare classi HTML che forniscono:
   * Informazioni layout
   * Informazioni sullo stile

Per gli sviluppatori, AEM offre una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti. Se e come viene eseguito il rendering del tag di decorazione è definito dalla combinazione di due fattori, in cui questa pagina si immergerà:

* Il componente stesso può configurare il proprio tag di decorazione con un set di proprietà.
* Gli script che includono i componenti possono definire gli aspetti del tag di decorazione con parametri di inclusione.

## Consigli {#recommendations}

Di seguito sono riportati alcuni consigli generali su quando includere l’elemento wrapper per evitare problemi imprevisti:

* La presenza dell’elemento wrapper non deve differire tra i diversi metodi WCMM (modalità di modifica o anteprima), le istanze (di authoring o pubblicazione) o l’ambiente (di staging o produzione), in modo che i CSS e i JavaScript della pagina funzionino in modo identico in tutti i casi.
* L’elemento wrapper deve essere aggiunto a tutti i componenti modificabili, in modo che l’editor pagina possa inizializzarli e aggiornarli correttamente.
* Per i componenti non modificabili, l&#39;elemento wrapper può essere evitato se non svolge alcuna funzione particolare, in modo che il markup risultante non risulti eccessivamente esteso.

## Controlli dei componenti {#component-controls}

Per controllare il comportamento del tag di decorazione, è possibile applicare ai componenti le proprietà e i nodi seguenti:

* **`cq:noDecoration {boolean}`:** Questa proprietà può essere aggiunta a un componente e un valore true impedisce ad AEM di generare elementi wrapper sul componente.
* **`cq:htmlTag`nodo :** Questo nodo può essere aggiunto in un componente e può avere le seguenti proprietà:
   * **`cq:tagName {String}`:** Questo può essere utilizzato per specificare un tag HTML personalizzato da utilizzare per il wrapping dei componenti invece dell&#39;elemento DIV predefinito.
   * **`class {String}`:** Può essere utilizzato per specificare i nomi di classe css da aggiungere al wrapper.
   * Altri nomi di proprietà vengono aggiunti come attributi HTML con lo stesso valore String fornito.

## Controlli script {#script-controls}

In generale, il comportamento del wrapper in HTL può essere riassunto come segue:

* Per impostazione predefinita, non viene eseguito il rendering di alcun DIV wrapper (solo durante l&#39;esecuzione di `data-sly-resource="foo"`).
* Tutte le modalità wcm (disabilitate, anteprima, modifica sia per l’authoring che per la pubblicazione) eseguono il rendering in modo identico.

Il comportamento dell&#39;involucro può anche essere completamente controllato.

* Lo script HTL ha il controllo completo sul comportamento risultante del tag wrapper.
* Anche le proprietà dei componenti (come `cq:noDecoration` e `cq:tagName`) possono definire il tag wrapper.

È possibile controllare completamente il comportamento dei tag wrapper dagli script HTL e dalla relativa logica associata.

Per ulteriori informazioni sullo sviluppo in HTL, consulta la [documentazione di HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it).

### Albero decisionale {#decision-tree}

Questo albero decisionale riepiloga la logica che determina il comportamento dei tag wrapper.

![Albero delle decisioni](assets/decoration-tag-decision-tree.png)

### Casi d’uso {#use-cases}

I tre casi d’uso seguenti forniscono esempi di gestione dei tag wrapper e illustrano quanto sia semplice controllare il comportamento desiderato dei tag wrapper.

Tutti gli esempi seguenti presuppongono la seguente struttura di contenuto e i seguenti componenti:

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

#### Caso d&#39;uso 1: inclusione di un componente per il riutilizzo del codice {#use-case-include-a-component-for-code-reuse}

Il caso d’uso più tipico è quando un componente include un altro componente per motivi di riutilizzo del codice. In tal caso, non si desidera che il componente incluso sia modificabile con la propria barra degli strumenti e finestra di dialogo, pertanto non è necessario alcun wrapper e il componente `cq:htmlTag` viene ignorato. Questo può essere considerato il comportamento predefinito.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`Hello World!`**

Un esempio può essere un componente che include un componente immagine principale per visualizzare un’immagine, in genere utilizzando una risorsa sintetica che consiste nell’includere un componente secondario virtuale passando a data-sly-resource un oggetto Map che rappresenta tutte le proprietà del componente.

#### Caso d&#39;uso 2: inclusione di un componente modificabile {#use-case-include-an-editable-component}

Un altro caso d’uso comune si verifica quando i componenti contenitore includono componenti figlio modificabili, come un Contenitore di layout. In questo caso, per il funzionamento dell&#39;editor è necessario un wrapper per ogni elemento figlio incluso, a meno che non sia esplicitamente disabilitato con la proprietà `cq:noDecoration`.

Poiché il componente incluso è in questo caso un componente indipendente, è necessario un elemento wrapper per il funzionamento dell’editor e per definirne il layout e lo stile da applicare. Per attivare questo comportamento, è disponibile l&#39;opzione `decoration=true`.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso d’uso 3: comportamento personalizzato {#use-case-custom-behavior}

Ci può essere un numero qualsiasi di casi complessi, che possono essere facilmente raggiunti dalla possibilità che HTL fornisca esplicitamente:

* **`decorationTagName='ELEMENT_NAME'`** Per definire il nome elemento del wrapper.
* **`cssClassName='CLASS_NAME'`** Per definire i nomi delle classi CSS da impostarvi.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Output risultante `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**
