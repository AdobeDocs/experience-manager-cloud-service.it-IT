---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 95%

---

# Creare un componente personalizzato nell’ambiente di authoring WYSIWYG

<span class="preview"> Questa è una funzionalità pre-release disponibile tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>


I moduli di Edge Delivery Services offrono funzionalità di personalizzazione e permettono agli sviluppatori front-end di creare componenti per moduli su misura. Questi componenti personalizzati si integrano direttamente nell’esperienza di authoring WYSIWYG, consentendo agli autori di moduli di aggiungerli, configurarli e gestirli facilmente nell’editor di moduli. I componenti personalizzati permettono agli autori di ottimizzare le funzionalità dei moduli. Inoltre, assicurano un processo di authoring fluido e intuitivo.

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando uno stile ai componenti per moduli HTML nativi, migliorando l’esperienza utente e aumentando l’impatto visivo dei moduli stessi.

## Prerequisiti

Prima di iniziare a creare il componente personalizzato, è necessario:

* Avere una conoscenza di base dei [componenti HTML nativi](/help/edge/docs/forms/form-components.md).
* Scopri come [assegnare uno stile ai campi modulo in base al tipo di campo utilizzando i selettori CSS](/help/edge/docs/forms/style-theme-forms.md)

## Creare un componente personalizzata

Quando si aggiunge nell’editor universale un componente personalizzato, questo diventa disponibile per gli autori che potranno utilizzarlo per progettare i moduli. Per aggiungere un componente personalizzato, occorre registrarlo, definirne le proprietà e configurare la posizione in cui può essere utilizzato. Per creare componenti personalizzati, segui i passaggi seguenti:

[1. Aggiungere la struttura per il nuovo componente personalizzato](#1-adding-structure-for-new-custom-component)
[2. Definire le proprietà per l’authoring del componente personalizzato](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.  Rendere visibile il componente personalizzato nell’elenco dei componenti WYSIWYG](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4. Registrare il componente personalizzato](#4-registering-your-custom-component)
[5. Aggiungere il comportamento runtime del componente personalizzato](#5-adding-the-runtime-behaviour-for-your-custom-component)

Prendiamo ad esempio la creazione di un nuovo componente personalizzato denominato **Intervallo**. Il componente Intervallo viene visualizzato come una linea retta e mostra valori quali minimo, massimo o il valore selezionato.

![Rappresentazione visiva di un componente intervallo che mostra un dispositivo di scorrimento con valori minimi e massimi e un indicatore di valori selezionato](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

Alla fine di questo articolo avrai appreso a creare componenti personalizzati da zero.

### &#x200B;1. Aggiungere la struttura per il nuovo componente personalizzato

Prima di poter utilizzare un componente personalizzato, è necessario registrarlo in modo che l’editor universale lo riconosca come opzione disponibile. A tale scopo è necessaria una definizione del componente, che include un identificatore univoco, le proprietà predefinite e la struttura. Per rendere il componente personalizzato disponibile per l’authoring dei moduli, segui i passaggi riportati di seguito:

1. **Aggiungere una nuova cartella e nuovi file**
Aggiungi al progetto AEM una nuova cartella e nuovi file per il componente personalizzato.
   1. Apri il progetto AEM e passa a `../blocks/form/components/`.
   1. Aggiungi una nuova cartella per il componente personalizzato in `../blocks/form/components/<component_name>`. In questo esempio verrà creata una cartella denominata `range`.
   1. Passa alla cartella appena creata in `../blocks/form/components/<component_name>`. Ad esempio, passa a `../blocks/form/components/range` e aggiungi i seguenti file:
      * `/blocks/form/components/range/_range.json`: contiene la definizione del componente personalizzato.
      * `../blocks/form/components/range/range.css`: definisce lo stile del componente personalizzato.
      * `../blocks/form/components/range/range.js`: personalizza il componente personalizzato in fase di esecuzione.

        ![Aggiungere il componente personalizzato per l’authoring](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Assicurati che il file JSON includa un trattino basso (_) come prefisso nel nome del file.

1. Passa al file `/blocks/form/components/range/_range.json` e aggiungi la definizione del componente personalizzato.

1. **Aggiungere la definizione del componente**

   Per aggiungere la definizione, è necessario aggiungere i seguenti campi al file `_range.json`:

   * **title**: titolo del componente visualizzato nell’editor universale.
   * **id**: identificatore univoco del componente.
   * **fieldType**: i moduli supportano vari **fieldType** per acquisire tipi specifici di input dell’utente. Puoi trovare i [fieldType supportati nella sezione Byte aggiuntivi](#supported-fieldtypes).
   * **resourceType**: a ogni componente personalizzato è associato un tipo di risorsa basato sul relativo fieldType. Puoi trovare i [resourceType supportati nella sezione Byte aggiuntivi](#supported-resourcetype).
   * **jcr:title**: è simile a un titolo, ma viene memorizzato all’interno della struttura del componente.
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
> Tutti i componenti relativi ai moduli adottano lo stesso approccio di Sites nell’aggiunta di blocchi all’editor universale. Per ulteriori informazioni, puoi consultare l’articolo [Creazione di blocchi abilitati all’utilizzo con l’editor universale](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block).

### &#x200B;2. Definizione delle proprietà per l’authoring del componente personalizzato

Il componente personalizzato include un modello di componente che specifica quali proprietà possono essere configurate dall’autore del modulo. Queste proprietà vengono visualizzate nella finestra di dialogo **Proprietà** dell’editor universale, consentendo agli autori di modificare impostazioni quali etichette, regole di convalida, stili e altri attributi. Per definire le proprietà:

1. Passa al file `/blocks/form/components/range/_range.json` e aggiungi il modello del componente personalizzato.

1. **Aggiungere il modello componente**

   Per definire il modello per il componente personalizzato, devi aggiungere i campi pertinenti al file `_range.json`.

   1. **Creare un nuovo modello**

      * Nell’array dei modelli, aggiungi un nuovo oggetto e imposta l’`id` del modello di componente in modo che corrisponda alla proprietà `fd:viewType` configurata in precedenza nella definizione del componente.
      * Includi un’array di campi all’interno di questo oggetto.

   2. **Definire i campi per la finestra di dialogo Proprietà**

      * Ogni oggetto nell’array di campi deve essere un componente di tipo contenitore, per poter comparire come scheda nella finestra di dialogo **Proprietà**.
      * Alcuni campi possono fare riferimento a proprietà riutilizzabili disponibili in `models/form-common`.

   3. **Utilizzare un modello di componente esistente come riferimento**

      * Puoi copiare il contenuto di un modello di componente esistente che corrisponde al `fieldType` scelto e modificarlo in base alle esigenze. Ad esempio, il componente `number-input` è stato esteso per creare un componente **intervallo**, pertanto è possibile utilizzare l’array di modelli da `models/form-components/_number-input.json` come riferimento.

   Il file `_range.json`, dopo l’aggiunta del modello di componente, è il seguente:

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
   > Per aggiungere un nuovo campo alla finestra di dialogo **Proprietà** di un componente personalizzato, rispetta lo [schema definito](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   Puoi anche [aggiungere proprietà personalizzate](#adding-custom-properties-for-your-custom-component) a un componente personalizzato per estenderne la funzionalità.

#### Aggiungere proprietà personalizzate per il componente personalizzato

Le proprietà personalizzate ti consentono di definire comportamenti specifici in base ai valori impostati nella finestra di dialogo Proprietà di un componente. Questo consente di estendere le funzionalità del componente e le opzioni di personalizzazione.

In questo esempio, al componente Intervallo viene aggiunto il Valore passaggio come proprietà personalizzata.

![Proprietà personalizzata Valore passaggio](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Per aggiungere la proprietà personalizzata Valore passaggio, aggiungi il modello del componente con le seguenti righe di codice nel file ` _<component>.json`:

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

Lo snippet JSON definisce una proprietà personalizzata denominata **Valore passaggio** per un componente **Intervallo**. Di seguito è riportata la suddivisione di ciascun campo:

* **component**: specifica il tipo di campo di input utilizzato nella finestra di dialogo Proprietà. In questo caso, `number` indica che il campo accetta valori numerici.
* **name**: l’identificatore della proprietà, utilizzato per farvi riferimento nella logica del componente. In questo caso `stepValue` rappresenta l’impostazione del valore incremento per l’intervallo.
* **label**: nome visualizzato con cui la proprietà viene identificata nella finestra di dialogo Proprietà.
* **valueType**: definisce il tipo di dati previsto per la proprietà. `number` garantisce che siano consentiti solo gli input numerici.

Ora puoi utilizzare `stepValue` come proprietà personalizzata nelle proprietà JSON di `range.js` e implementarne il comportamento dinamico in base al relativo valore in fase di esecuzione.

Di conseguenza, il file `_range.json` finale, dopo l’aggiunta della definizione del componente, del modello del componente e delle proprietà personalizzate, è il seguente:

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


### &#x200B;3. Rendere visibile il componente personalizzato nell’elenco dei componenti WYSIWYG.

Un filtro definisce la sezione in cui il componente personalizzato può essere utilizzato nell’editor universale. In questo modo il componente può essere utilizzato solo nelle sezioni appropriate, mantenendo la struttura e l’usabilità.

Per fare in modo che il componente personalizzato venga visualizzato nell’elenco dei componenti disponibili durante l’authoring del modulo WYSIWYG:

1. Passa al file `/blocks/form/_form.json`.
1. Individua l’array di componenti all’interno dell’oggetto che contiene `id="form"`.
1. Aggiungi il valore `fd:viewType` da `definitions[]` all’array di componenti dell’oggetto con `id="form"`.

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

### &#x200B;4. Registrazione del componente personalizzato

Per consentire al blocco modulo di riconoscere il componente personalizzato e caricarne le proprietà definite nel modello di componente durante l’authoring, aggiungi il valore `fd:viewType` dalla definizione del componente al file `mappings.js`.
Per registrare un componente:
1. Passa al file `/blocks/form/mappings.js`.
1. Individua l’array `customComponents[]`.
1. Aggiungi il valore `fd:viewType` dall’array `definitions[]` all’array `customComponents[]`.

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

Dopo aver completato i passaggi precedenti, il componente personalizzato viene visualizzato nell’elenco dei componenti del modulo all’interno dell’editor universale. Puoi quindi trascinarlo nella sezione del modulo.

![Schermata della tavolozza dei componenti di Universal Editor che mostra il componente intervallo personalizzato disponibile per il trascinamento nei moduli](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

La schermata seguente mostra le proprietà del componente `range` aggiunto al modello di componente, che specifica le proprietà che l’autore del modulo può configurare.:

![Schermata del pannello delle proprietà di Universal Editor che mostra le impostazioni configurabili per il componente intervallo, incluse le proprietà di base, le regole di convalida e le opzioni di stile](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

Ora puoi definire il comportamento runtime del componente personalizzato aggiungendo stile e funzionalità.

### &#x200B;5. Aggiungere il comportamento runtime per il componente personalizzato

Puoi modificare i componenti personalizzati utilizzando markup predefiniti, come spiegato in [ Stile dei campi modulo](/help/edge/docs/forms/style-theme-forms.md). A questo scopo, puoi utilizzare CSS (Cascading Style Sheets) personalizzati e codice personalizzato per migliorare l’aspetto del componente. Per aggiungere i il comportamento runtime del componente:

1. Per aggiungere lo stile, passa al file `/blocks/form/components/range/range.css` e aggiungi la seguente riga di codice:

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

1. Per aggiungere la funzionalità, passa al file `/blocks/form/components/range/range.js` e aggiungi la seguente riga di codice:

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

   Controlla il modo in cui il componente personalizzato interagisce con gli input dell’utente, elabora i dati e si integra con il blocco modulo nell’editor universale.

   L’integrazione di stile e funzionalità personalizzati migliora l’aspetto e il comportamento del componente Intervallo. Il design aggiornato riflette gli stili applicati, mentre la funzionalità aggiunta garantisce un’esperienza utente più dinamica e interattiva.
La schermata seguente illustra il componente intervallo aggiornato.

![Componente intervallo finale in azione che mostra un dispositivo di scorrimento formattato con visualizzazione a bolla di valori e funzionalità interattive nell&#39;Universal Editor](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Domande frequenti

* **Se aggiungo lo stile sia in component.css che in forms.css, quale dei due ha la priorità?**
Quando gli stili sono definiti sia in `component.css` che in **forms.css**, `component.css` ha la priorità. Questo perché gli stili a livello di componente sono più specifici e sovrascrivono gli stili globali di `forms.css`.

* **Il componente personalizzato non è visibile nell’elenco dei componenti disponibili nell’editor universale. Come posso risolvere il problema?**
Se il componente personalizzato non viene visualizzato, controlla i file seguenti per verificare che il componente sia registrato correttamente:
   * **component-definition.json**: verifica che il componente sia definito correttamente.
   * **component-filters.json**: verifica che il componente sia consentito nelle sezioni appropriate.
   * **component-models.json**: verifica che il modello del componente sia configurato correttamente.

## Best practice

* È consigliato di [configurare un ambiente di sviluppo AEM locale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) per sviluppare stili e componenti personalizzati a livello locale.


## Byte aggiuntivi

### ResourceType supportato

| Tipo campo | Tipo risorsa |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| number-input | core/fd/components/form/numberinput/v1/numberinput |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| pannello | core/fd/components/form/panelcontainer/v1/panelcontainer |
| checkbox | core/fd/components/form/checkbox/v1/checkbox |
| drop-down | core/fd/components/form/dropdown/v1/dropdown |
| radio-group | core/fd/components/form/radiobutton/v1/radiobutton |
| plain-text | core/fd/components/form/text/v1/text |
| file-input | core/fd/components/form/fileinput/v2/fileinput |
| email | core/fd/components/form/emailinput/v1/emailinput |
| immagine | core/fd/components/form/image/v1/image |
| button | core/fd/components/form/button/v1/button |

### fieldType supportati

I fieldType supportati per i moduli sono:
* text-input
* number-input
* date-input
* pannello
* checkbox
* drop-down
* radio-group
* plain-text
* file-input
* email
* immagine
* button

## Consulta anche

{{universal-editor-see-also}}
