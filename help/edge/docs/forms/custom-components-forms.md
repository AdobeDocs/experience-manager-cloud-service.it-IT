---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---

# Creare componenti personalizzati

Edge Delivery Services per AEM Forms ti consente di personalizzare i [componenti nativi del modulo HTML](/help/edge/docs/forms/form-components.md) e di creare moduli interattivi e di facile utilizzo. Consente di modificare i componenti del modulo con il markup predefinito, come spiegato in [Stile dei campi modulo](/help/edge/docs/forms/style-theme-forms.md) utilizzando CSS personalizzato (Cascading Style Sheets) e codice personalizzato per decorare il componente, migliorando in tal modo l’aspetto dei campi modulo all’interno di un Blocco di moduli adattivi.

![Componente personalizzato](/help/edge/assets/custom-component-image.png)

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando uno stile ai componenti per moduli HTML nativi, migliorando l’esperienza utente e aumentando l’impatto visivo dei moduli stessi.

Prendiamo ad esempio un componente `range` che mostra `Estimated trip cost` in un modulo. Il componente `range` viene visualizzato come una linea retta, senza visualizzare valori quali il valore minimo, massimo o selezionato.

![Componente intervallo nativo](/help/edge/assets/native-range-component.png)

Iniziamo a personalizzare il campo `range` per mostrare i valori minimo, massimo e selezionato sulla linea aggiungendo stile tramite CSS e una funzione personalizzata per decorare un componente.

![Componente intervallo personalizzato](/help/edge/assets/custom-range-component.png)

Al termine di questo articolo, imparerai a creare componenti personalizzati aggiungendo stili nel file CSS e nella funzione personalizzata.

## Prerequisiti

Prima di iniziare a creare il componente personalizzato, è necessario:

- Avere una conoscenza di base dei [componenti HTML nativi](/help/edge/docs/forms/form-components.md).
- Scopri come [assegnare uno stile ai campi modulo in base al tipo di campo utilizzando i selettori CSS](/help/edge/docs/forms/style-theme-forms.md)


## Creare un componente personalizzata


![passaggi per creare il componente personalizzato](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Analizziamo ora ogni passaggio nel dettaglio.

<!--Refer to the [enquiry spreadsheet](/help/edge/docs/forms/assets/enquiry.xlsx) to customize the `range` component, by following the steps as explained below.-->

### Aggiungi una funzione personalizzata per decorare il componente

La funzione personalizzata aggiunta in `[../Form Block/components]` è costituita da:

- **Dichiarazione di funzione**: definisce il nome della funzione e i relativi parametri.
- **Implementazione logica**: scrive la logica per aggiungere il comportamento personalizzato relativo al componente.
- **Esportazione funzione**: rende la funzione accessibile in `[Form Block]`.

Per aggiungere una funzione personalizzata:

1. Accedi a `[../Form Block/components]`.
1. Individua un file denominato `range.js`. Se non è presente, crealo.
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

Nel nostro caso, la funzione controlla la proprietà del campo `fieldType` e restituisce il decoratore dell’intervallo personalizzato dal file `range.js` presente in `[../Form Block/components]`.

Per inserire il decoratore nel blocco del modulo:

1. Passa a `[../Form Block/]` e apri `mapping.js`.
1. Aggiungi la seguente riga di codice:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Salva le modifiche.

### Aggiungi stile per il componente nel file CSS

È possibile modificare l’aspetto dei campi modulo in base al tipo e ai nomi dei campi utilizzando i selettori CSS, consentendo uno stile coerente o univoco in base ai requisiti. Per assegnare uno stile al componente, aggiungere il codice nel file `form.css` per modificare l’aspetto del componente del modulo.

Per personalizzare lo stile relativo al componente `range`, includere uno snippet di codice CSS in un modulo che assegna uno stile di un elemento di input `range` e dei relativi componenti associati. Ciò presuppone un layout HTML strutturato con classi come `.form` e `.range-wrapper`.

Per aggiungere uno stile relativo al componente nel file CSS:

1. Passa a `[../Form Block/]` e apri `form.css`.
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

### Distribuire i file e compilare il progetto

Distribuisci i file `range.js`, `mapping.js` e `form.css` aggiornati nel progetto GitHub e verifica la corretta compilazione.

### Visualizzare l’anteprima del modulo utilizzando la barra laterale di AEM

Visualizza l’anteprima del modulo con la nuova funzione implementata che assegna uno stile al componente `range`.

![Modulo componente personalizzato](/help/edge/assets/custom-componet-form.png)

Il nuovo stile per il componente `range` mostra i valori minimi, massimi e selezionati sulla linea aggiungendo gli stili tramite CSS e una funzione personalizzata che include un decoratore per il componente.


