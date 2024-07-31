---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# Creare componenti personalizzati

AEM Forms Edge Delivery Services ti consente di personalizzare i [componenti nativi del modulo HTML](/help/edge/docs/forms/form-components.md) e di creare moduli interattivi e di facile utilizzo. Consente di modificare i componenti del modulo con il markup predefinito, come spiegato in [Stile dei campi modulo](/help/edge/docs/forms/style-theme-forms.md) utilizzando CSS personalizzato (Cascading Style Sheets) e codice personalizzato per decorare il componente, migliorando in tal modo l&#39;aspetto dei campi modulo all&#39;interno di un blocco Forms adattivo.

![Componente personalizzato](/help/edge/assets/custom-component-image.png)

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando al modulo HTML uno stile che ne ottimizza l’esperienza utente e ne aumenta l’impatto visivo.

Prendiamo ad esempio un componente `range` che visualizza `Estimated trip cost` in un modulo. Il componente `range` viene visualizzato come una linea retta, senza visualizzare valori quali il valore minimo, massimo o selezionato.

![Componente intervallo nativo](/help/edge/assets/native-range-component.png)

Iniziamo a personalizzare il campo `range` per mostrare i valori minimo, massimo e selezionato sulla linea aggiungendo stile tramite CSS e aggiungendo una funzione personalizzata per decorare un componente.

![Componente intervallo personalizzato](/help/edge/assets/custom-range-component.png)

Alla fine di questo articolo, imparerai a creare componenti personalizzati aggiungendo stili nel file CSS e nella funzione personalizzata.

## Prerequisiti

Prima di iniziare a creare il componente personalizzato, è necessario:

* Avere una conoscenza di base di [componenti HTML nativi](/help/edge/docs/forms/form-components.md).
* Scopri come [assegnare uno stile ai campi modulo in base al tipo di campo utilizzando i selettori CSS](/help/edge/docs/forms/style-theme-forms.md)


## Creare un componente personalizzato


![passaggi per creare il componente personalizzato](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Comprendiamo ora ogni passaggio nel dettaglio.

Per personalizzare il componente `range`, fare riferimento al foglio di calcolo [interrogazione](/help/edge/docs/forms/assets/enquiry.xlsx), seguendo i passaggi descritti di seguito.

### Aggiungi una funzione personalizzata per decorare il componente

La funzione personalizzata aggiunta in `[../Form Block/components]` è costituita da:

* **Dichiarazione di funzione**: definire il nome della funzione e i relativi parametri.
* **Implementazione logica**: scrivere la logica per aggiungere il comportamento personalizzato per il componente.
* **Esportazione funzione**: rendere la funzione accessibile in `[Form Block]`.

Creare un file JavaScript denominato `range.js` per assegnare uno stile al componente intervallo. Per aggiungere una funzione personalizzata:

1. Vai alla cartella del progetto AEM su Google Drive o SharePoint.
1. Passa a `[../Form Block/components]`.
1. Aggiungere un nuovo file denominato `range.js`.
1. Aggiungi la seguente riga di codice:

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
       updateBubble(e.target, div);
   });
   updateBubble(input, div);
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. Salva le modifiche.

### Inserisci il decoratore nel blocco modulo

`[Form Block]` utilizza HTML semantico per eseguire il rendering dei campi modulo, inclusi campi di input, etichette e testo della Guida, con attributi standard per l&#39;accessibilità. Per fare in modo che `[Form Block]` utilizzi un decoratore personalizzato per un componente specificato, definirlo nel file `mappings.js`. Il file `mappings.js` importa una funzione che restituisce il modulo responsabile della decorazione di un particolare componente. La funzione accetta le proprietà del campo e restituisce una funzione decorativa per il campo modulo.

Nel nostro caso, la funzione controlla la proprietà `fieldType` del campo e restituisce il decoratore dell&#39;intervallo personalizzato dal file `range.js` presente in `[../Form Block/components]`.

Per inserire il decoratore nel blocco di modulo:

1. Vai a `[../Form Block/]` e apri `mapping.js`.
1. Aggiungi la seguente riga di codice:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Salva le modifiche.

### Aggiungi stile per il componente nel file CSS

È possibile modificare l’aspetto dei campi modulo in base al tipo di campo e ai nomi di campo utilizzando selettori CSS, consentendo uno stile coerente o univoco in base ai requisiti. Per assegnare uno stile al componente, aggiungere il codice nel file `form.css` per modificare l&#39;aspetto del componente del modulo.

Per personalizzare lo stile del componente `range`, includere in un modulo uno snippet di codice CSS con lo stile di un elemento di input `range` e dei relativi componenti associati. Ciò presuppone un layout HTML strutturato con classi come `.form` e `.range-wrapper`.

Per aggiungere uno stile per un componente nel file CSS:
1. Vai a `[../Form Block/]` e apri `form.css`.
1. Aggiungi la seguente riga di codice:

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```
1. Salva le modifiche.

### Distribuire i file e generare il progetto

Distribuisci i file aggiornati di `range.js`, `mapping.css` e `form.css` nel progetto GitHub e verifica che la build sia corretta.

### Visualizzare l’anteprima del modulo utilizzando la barra laterale AEM

Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima il modulo con la nuova funzione implementata che assegna lo stile al componente `range`.

![Modulo componente personalizzato](/help/edge/assets/custom-componet-form.png)

Il nuovo stile per il componente `range` mostra i valori minimo, massimo e selezionato sulla linea aggiungendo stili tramite CSS e una funzione personalizzata che include un decoratore per il componente.


## Consulta anche

{{see-more-forms-eds}}



