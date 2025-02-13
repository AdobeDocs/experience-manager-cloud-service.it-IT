---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d71c5d6488935de4a02c8d3828f287542b979d0f
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 5%

---


# Creare un componente personalizzato in WYSIWYG Authoring

Edge Delivery Services Forms offre la personalizzazione, consentendo agli sviluppatori front-end di creare componenti di modulo personalizzati. Questi componenti personalizzati si integrano perfettamente nell’esperienza di authoring di WYSIWYG, consentendo agli autori dei moduli di aggiungerli, configurarli e gestirli facilmente nell’editor di moduli. Con i componenti personalizzati, gli autori possono migliorare le funzionalità garantendo al contempo un processo di authoring fluido e intuitivo.

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando al modulo HTML nativo uno stile che ne ottimizza l’esperienza utente e ne aumenta l’impatto visivo.

## Prerequisiti

Prima di iniziare a creare il componente personalizzato, è necessario:

* Avere una conoscenza di base dei [componenti HTML nativi](/help/edge/docs/forms/form-components.md).
* Scopri come [assegnare uno stile ai campi modulo in base al tipo di campo utilizzando i selettori CSS](/help/edge/docs/forms/style-theme-forms.md)

## Creare un componente personalizzata

L’aggiunta di un componente personalizzato nell’Editor universale comporta la disponibilità di un nuovo componente da utilizzare per gli autori dei moduli durante la progettazione dei moduli. Ciò comporta la registrazione del componente, la definizione delle relative proprietà e la configurazione della posizione in cui può essere utilizzato. I passaggi per creare componenti personalizzati sono i seguenti:

[1. Aggiunta della struttura per il nuovo componente personalizzato](#1-adding-structure-for-new-custom-component)
[2. Definizione delle proprietà del componente personalizzato per l&#39;authoring](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.  Rendere visibile il componente personalizzato nell&#39;elenco dei componenti di WYSIWYG](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4. Registrazione del componente personalizzato](#4-registering-your-custom-component)
[5. Aggiunta del comportamento runtime per il componente personalizzato](#5-adding-the-runtime-behaviour-for-your-custom-component)

Prendiamo ad esempio la creazione di un nuovo componente personalizzato denominato **intervallo**. Il componente Intervallo viene visualizzato come linea retta e mostra valori quali il valore minimo, massimo o selezionato.

![Stile componente intervallo](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

Alla fine di questo articolo imparerai a creare componenti personalizzati da zero.

### 1. Aggiunta della struttura per il nuovo componente personalizzato

Prima di poter utilizzare un componente personalizzato, è necessario registrarlo in modo che l&#39;editor universale lo riconosca come opzione disponibile. Ciò si ottiene tramite una definizione del componente, che include un identificatore univoco, le proprietà predefinite e la struttura del componente.Per rendere disponibile il componente personalizzato per la creazione dei moduli, effettua le seguenti operazioni:

1. **Aggiungi cartella e file**
Aggiungi una nuova cartella e nuovi file per il nuovo componente personalizzato nel progetto AEM.
   1. Apri il progetto AEM e passa a `../blocks/form/components/`.
   1. Aggiungere una nuova cartella per il componente personalizzato in `../blocks/form/components/<component_name>`. In questo esempio verrà creata una cartella denominata `range`.
   1. Passare alla cartella appena creata in `../blocks/form/components/<component_name>`. Ad esempio, passare a `../blocks/form/components/range` e aggiungere i seguenti file:
      * `/blocks/form/components/range/_range.json`: contiene la definizione del componente personalizzato.
      * `../blocks/form/components/range/range.css`: definisce lo stile del componente personalizzato.
      * `../blocks/form/components/range/range.js`: personalizza il componente personalizzato in fase di esecuzione.

        ![Aggiunta del componente personalizzato per l&#39;authoring](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Assicurati che il file json includa un carattere di sottolineatura (_) come prefisso nel nome del file.

1. Passare al file `/blocks/form/components/range/_range.json` e aggiungere la definizione del componente personalizzato.

1. **Aggiungere la definizione del componente**

   Per aggiungere la definizione, i campi da aggiungere nel file `_range.json` sono:

   * **title**: titolo del componente visualizzato nell&#39;editor universale.
   * **id**: identificatore univoco del componente.
   * **fieldType**: Forms supporta vari **fieldType** per acquisire tipi specifici di input utente. Puoi trovare il [tipo di campo supportato nella sezione Byte aggiuntivi](#supported-fieldtypes).
   * **resourceType**: a ogni componente personalizzato è associato un tipo di risorsa basato sul relativo fieldType. Puoi trovare il [resourceType supportato nella sezione Byte aggiuntivi](#supported-resourcetype).
   * **jcr:title**: è simile a un titolo, ma viene memorizzato all&#39;interno della struttura del componente.
   * **fd:viewType**: rappresenta il nome del componente personalizzato. È l’identificatore univoco del componente. È necessario per creare una vista personalizzata per il componente.

Dopo aver aggiunto la definizione del componente, il file `_range.json` è il seguente:

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> Tutti i componenti relativi ai moduli adottano lo stesso approccio di Sites quando si aggiungono blocchi all’Editor universale. Per ulteriori informazioni, consultare l&#39;articolo [Creazione di blocchi instrumentati per l&#39;utilizzo con Universal Editor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block).

### 2. Definizione delle proprietà del componente personalizzato per la creazione

Il componente personalizzato include un modello di componente che specifica quali proprietà possono essere configurate dall’autore del modulo. Queste proprietà vengono visualizzate nella finestra di dialogo **Proprietà** dell&#39;Editor universale, consentendo agli autori di modificare impostazioni quali etichette, regole di convalida, stili e altri attributi. Per definire le proprietà:

1. Passare al file `/blocks/form/components/range/_range.json` e aggiungere il modello del componente personalizzato.

1. **Aggiungi modello componente**

   Per definire il modello del componente personalizzato, è necessario aggiungere i campi pertinenti al file `_range.json`.

   1. **Crea nuovo modello**

      * Nell&#39;array models, aggiungere un nuovo oggetto e impostare `id` del modello di componente in modo che corrisponda alla proprietà `fd:viewType` configurata in precedenza nella definizione del componente.
      * Includi una matrice di campi all’interno di questo oggetto.

   2. **Definisci campi per la finestra di dialogo Proprietà**

      * Ogni oggetto nell&#39;array fields deve essere un componente di tipo contenitore, che consente di visualizzarlo come scheda nella finestra di dialogo **Property**.
      * Alcuni campi possono fare riferimento a proprietà riutilizzabili disponibili in `models/form-common`.

   3. **Utilizza un modello di componente esistente come riferimento**

      * È possibile copiare il contenuto di un modello di componente esistente che corrisponde al `fieldType` scelto e modificarlo in base alle esigenze. Ad esempio, il componente `number-input` è stato esteso per creare un componente **range**, pertanto è possibile utilizzare l&#39;array di modelli da `models/form-components/_number-input.json` come riferimento.

   Il file `_range.json`, dopo l&#39;aggiunta del modello di componente, è il seguente:

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```
   >[!NOTE]
   >
   > Per aggiungere un nuovo campo alla finestra di dialogo **Proprietà** di un componente personalizzato, attieniti allo [schema definito](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   Puoi anche [aggiungere proprietà personalizzate](#adding-custom-properties-for-your-custom-component) a un componente personalizzato per estenderne la funzionalità.

#### Aggiunta di proprietà personalizzate per il componente personalizzato

Le proprietà personalizzate ti consentono di definire comportamenti specifici in base ai valori impostati nella finestra di dialogo Proprietà di un componente. Questo consente di estendere le funzionalità del componente e le opzioni di personalizzazione.

In questo esempio, al componente Range viene aggiunto il valore Step come proprietà personalizzata.

![Proprietà personalizzata valore passaggio](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Per aggiungere la proprietà personalizzata Valore passaggio, aggiungere il modello del componente con le seguenti righe di codice nel file ` _<component>.json`:

```javascript
    {
    "component": "number",
    "name": "stepValue",
    "label": "Step Value",
    "valueType": "number"
    }
    ```
The JSON snippet defines a custom property called **Step Value** for a **Range** component. Below is a breakdown of each field:

* **component**: Specifies the type of input field used in the Property dialog. In this case, `number` indicates that the field accepts numeric values.
* **name**: The identifier for the property, used to reference it in the component’s logic. Here, the `stepValue` represents the step value setting for the range.
* **label**: The display name of the property as seen in the Property dialog. 
* **valueType**: Defines the data type expected for the property. The `number` ensures that only numeric inputs are allowed.

You can now use `stepValue` as a custom property in the JSON properties of `range.js` and implement dynamic behavior based on its value at runtime.

Hence, the final `_range.json` file, after adding the component definition, component model and custom properties, is as follows:

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![definizione componente e modello](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3. Rendere visibile il componente personalizzato nell’elenco dei componenti di WYSIWYG

Un filtro definisce la sezione in cui il componente personalizzato può essere utilizzato nell’Editor universale. In questo modo il componente può essere utilizzato solo nelle sezioni appropriate, mantenendo la struttura e l’usabilità.

Per fare in modo che il componente personalizzato venga visualizzato nell’elenco dei componenti disponibili durante la creazione del modulo in WYSIWYG:

1. Passare al file `/blocks/form/_form.json`.
1. Individuare l&#39;array dei componenti all&#39;interno dell&#39;oggetto che contiene `id="form"`.
1. Aggiungere il valore `fd:viewType` da `definitions[]` alla matrice dei componenti dell&#39;oggetto con `id="form"`.

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![filtro componente](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4. Registrazione del componente personalizzato

Per consentire al blocco di modulo di riconoscere il componente personalizzato e caricarne le proprietà definite nel modello di componente durante la creazione del modulo, aggiungere il valore `fd:viewType` dalla definizione del componente al file `mappings.js`.
Per registrare un componente:
1. Passare al file `/blocks/form/mappings.js`.
1. Individuare l&#39;array `customComponents[]`.
1. Aggiungere il valore `fd:viewType` dall&#39;array `definitions[]` all&#39;array `customComponents[]`.

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![mappatura componente](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

Dopo aver completato i passaggi precedenti, il componente personalizzato viene visualizzato nell’elenco dei componenti del modulo all’interno di Universal Editor. È quindi possibile trascinarlo e rilasciarlo nella sezione del modulo.

![componente intervallo](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

Ora puoi definire il comportamento in fase di esecuzione del componente personalizzato aggiungendo stile e funzionalità.

### 5. Aggiunta del comportamento runtime per il componente personalizzato

Puoi modificare i componenti personalizzati utilizzando markup predefiniti, come spiegato in [Stile dei campi modulo](/help/edge/docs/forms/style-theme-forms.md). A questo scopo, puoi utilizzare CSS (Cascading Style Sheets) personalizzati e codice personalizzato per migliorare l’aspetto del componente. Per aggiungere il comportamento runtime del componente:

1. Per aggiungere lo stile, passare al file `/blocks/form/components/range/range.css` e aggiungere la seguente riga di codice:

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```
   Il codice consente di definire lo stile e l’aspetto visivo del componente personalizzato.

1. Per aggiungere la funzionalità, passare al file `/blocks/form/components/range/range.js` e aggiungere la seguente riga di codice:

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
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
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
   return fieldDiv;
   }
   ```

   Controlla il modo in cui il componente personalizzato interagisce con gli input dell’utente, elabora i dati e si integra con il blocco del modulo nell’Editor universale.

   Dopo aver incorporato uno stile e una funzionalità personalizzati, vengono migliorati l’aspetto e il comportamento del componente Intervallo. Il design aggiornato riflette gli stili applicati, mentre le funzionalità aggiunte garantiscono un’esperienza utente più dinamica e interattiva.
La schermata seguente illustra il componente intervallo aggiornato.

![Stile componente intervallo](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Domanda frequente

* **Se aggiungo uno stile sia in component.css che in forms.css, quale dei due ha la priorità?**
Quando gli stili sono definiti sia in `component.css` che in **forms.css**, `component.css` ha la priorità. Questo perché gli stili a livello di componente sono più specifici e sostituiscono gli stili globali da `forms.css`.

* **Il componente personalizzato non è visibile nell&#39;elenco dei componenti disponibili in Universal Editor. Come posso risolvere questo?**
Se il componente personalizzato non viene visualizzato, seleziona i file seguenti per verificare che il componente sia registrato correttamente:
   * **component-definition.json**: verificare che il componente sia definito correttamente.
   * **component-filters.json**: verifica che il componente sia consentito nelle sezioni appropriate.
   * **component-models.json**: verifica che il modello del componente sia configurato correttamente.

## Best practice

* Si consiglia di [configurare un ambiente di sviluppo AEM locale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) per lo sviluppo locale di stili e componenti personalizzati.


## Byte aggiuntivo

### ResourceType supportato

| Tipo di campo | Tipo risorsa |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| input numerico | core/fd/components/form/number input/v1/number input |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| pannello | core/fd/components/form/panelcontainer/v1/panelcontainer |
| casella di controllo | core/fd/components/form/checkbox/v1/checkbox |
| elenco a discesa | core/fd/components/form/dropdown/v1/dropdown |
| gruppo radio | core/fd/components/form/radiobutton/v1/radiobutton |
| testo normale | core/fd/components/form/text/v1/text |
| file-input | core/fd/components/form/fileinput/v2/fileinput |
| e-mail | core/fd/components/form/emailinput/v1/emailinput |
| immagine | core/fd/components/form/image/v1/image |
| pulsante | core/fd/components/form/button/v1/button |

### Tipi di campo supportati

I tipi di campo supportati per i moduli sono:
* text-input
* input numerico
* date-input
* pannello
* casella di controllo
* elenco a discesa
* gruppo radio
* testo normale
* file-input
* e-mail
* immagine
* pulsante

## Consulta anche

{{see-more-forms-eds}}