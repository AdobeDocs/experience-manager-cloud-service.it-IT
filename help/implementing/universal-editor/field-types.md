---
title: Definizioni di modelli, campi e tipi di componenti
description: Scopri i campi e i tipi di componenti che possono essere modificati dall’Editor universale nella barra delle proprietà, con alcuni esempi. Scopri come creare una definizione di modello e un collegamento al componente per sfruttare al meglio la tua app.
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 550d26cde3d6b7be419bc9df70db8894851361c6
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 11%

---


# Definizioni di modelli, campi e tipi di componenti {#field-types}

Scopri i campi e i tipi di componenti che possono essere modificati dall’Editor universale nella barra delle proprietà, con alcuni esempi. Scopri come creare una definizione di modello e un collegamento al componente per sfruttare al meglio la tua app.

{{universal-editor-status}}

## Panoramica {#overview}

Quando adattate le vostre app per l&#39;uso con l&#39;Editor universale, dovete dotare gli strumenti dei componenti e definire quali campi e tipi di componenti possono essere manipolati nella barra delle proprietà dell&#39;editor. A tale scopo, crea un modello e crea un collegamento a tale modello dal componente.

Questo documento fornisce una panoramica della definizione di un modello, dei campi e dei tipi di componenti disponibili, insieme ad esempi di configurazioni.

>[!TIP]
>
>Se non sai come dotare l’app dell’editor universale, consulta il documento [Panoramica di Universal Editor per sviluppatori AEM.](/help/implementing/universal-editor/developer-overview.md)

## Struttura definizione modello {#model-structure}

Per configurare un componente tramite la barra delle proprietà nell’Editor universale, è necessario che esista una definizione di modello e che tale definizione sia collegata al componente.

La definizione del modello è una struttura JSON che inizia con un array di modelli.

```json
[
  {
    "id": "model-id",        // must be unique
    "fields": []             // array of fields which shall be rendered in the properties rail
  }
]
```

Consulta la **[Campi](#fields)** per ulteriori informazioni su come definire le `fields` array.

Per utilizzare la definizione del modello con un componente, `data-aue-model` può essere utilizzato.

```html
<div data-aue-resource="urn:datasource:/content/path" data-aue-type="component"  data-aue-model="model-id">Click me</div>
```

## Caricamento di una definizione di modello {#loading-model}

Una volta creato un modello, è possibile farvi riferimento come file esterno.

```html
<script type="application/vnd.adobe.aue.model+json" src="<url-of-model-definition>"></script>
```

In alternativa, potete anche definire il modello in linea.

```html
<script type="application/vnd.adobe.aue.model+json">
  { ... model definition ... }
</script>
```

## Campi {#fields}

Un oggetto campo ha la seguente definizione di tipo.

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `component` | `ComponentType` | Rendering del componente | Sì |
| `name` | `string` | Proprietà in cui i dati sono persistenti | Sì |
| `label` | `FieldLabel` | Etichetta del campo | Sì |
| `description` | `FieldDescription` | Descrizione del campo | No |
| `placeholder` | `string` | Segnaposto per il campo | No |
| `value` | `FieldValue` | Valore predefinito | No |
| `valueType` | `ValueType` | Convalida standard, può essere `string`, `string[]`, `number`, `date`, `boolean` | No |
| `required` | `boolean` | Il campo è obbligatorio | No |
| `readOnly` | `boolean` | Campo di sola lettura | No |
| `hidden` | `boolean` | Campo nascosto per impostazione predefinita | No |
| `condition` | `RulesLogic` | Regola per mostrare o nascondere il campo in base a una [condizione](/help/implementing/universal-editor/customizing.md#conditionally-hide) | No |
| `multi` | `boolean` | Campo multiplo | No |
| `validation` | `ValidationType` | Regola o regole di convalida per il campo | No |
| `raw` | `unknown` | Dati non elaborati che possono essere utilizzati dal componente | No |

### Tipi di componenti {#component-types}

Di seguito sono elencati i tipi di componenti che è possibile utilizzare per il rendering dei campi.

#### Tag AEM {#aem-tag}

Un tipo di componente tag AEM abilita un selettore di tag AEM, che può essere utilizzato per allegare i tag al componente.

##### Esempio {#sample-aem-tag}

```json
{
  "id": "aem-tag-picker",
  "fields": [
    {
      "component": "aem-tag",
      "label": "AEM Tag Picker",
      "name": "cq:tags",
      "valueType": "string"
    }
  ]
}
```

##### Schermata {#screenshot-aem-tag}

![Schermata del tipo di componente tag AEM](assets/component-types/aem-tag-picker.png)

#### Contenuto AEM {#aem-content}

Un tipo di componente di contenuto AEM abilita un selettore di contenuti AEM, che può essere utilizzato per impostare riferimenti al contenuto.

##### Esempio {#sample-aem-content}

```json
{
  "id": "aem-content-picker",
  "fields": [
    {
      "component": "aem-content",
      "name": "reference",
      "value": "",
      "label": "AEM Content Picker",
      "valueType": "string"
    }
  ]
}
```

##### Schermata {#screenshot-aem-content}

![Schermata del tipo di componente contenuto AEM](assets/component-types/aem-content-picker.png)

#### Booleano {#boolean}

Un tipo di componente booleano memorizza un semplice valore true/false renderizzato come un interruttore. Offre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se il valore immesso non è un valore booleano | No |

##### Esempio {#sample-boolean}

```json
{
  "id": "boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean"
    }
  ]
}
```

```json
{
  "id": "another-boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean",
      "validation": {
        "customErrorMsg": "Think, McFly. Think!"
      }
    }
  ]
}
```

##### Schermata {#screenshot-boolean}

![Schermata del tipo di componente booleano](assets/component-types/boolean.png)

#### Gruppo di caselle di controllo {#checkbox-group}

Simile a un booleano, un tipo di componente gruppo casella di controllo consente la selezione di più elementi true/false, riprodotti come più caselle di controllo.

##### Esempio {#sample-checkbox-group}

```json
{
  "id": "checkbox-group",
  "fields": [
    {
      "component": "checkbox-group",
      "label": "Checkbox Group",
      "name": "checkbox",
      "valueType": "string[]",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

#### Schermata {#screenshot-checkbox-group}

![Schermata del tipo di componente del gruppo di caselle di controllo](assets/component-types/checkbox-group.png)

#### Contenitore {#container}

Un tipo di componente contenitore consente il raggruppamento di componenti. Offre una configurazione aggiuntiva.

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `collapsible` | `boolean` | Il contenitore è comprimibile | No |

##### Esempio {#sample-container}

```json
 {
  "id": "container",
  "fields": [
    {
      "component": "container",
      "label": "Container",
      "name": "container",
      "valueType": "string",
      "collapsible": true,
      "fields": [
        {
          "component": "text-input",
          "label": "Simple Text 1",
          "name": "text",
          "valueType": "string"
        },
        {
          "component": "text-input",
          "label": "Simple Text 2",
          "name": "text2",
          "valueType": "string"
        }
      ]
    }
  ]
}
```

##### Schermata {#screenshot-container}

![Schermata del tipo di componente del contenitore](assets/component-types/container.png)

#### Data e ora {#date-time}

Un tipo di componente data e ora consente di specificare una data, un’ora o una combinazione di esse. Offre configurazioni aggiuntive.

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `displayFormat` | `string` | Formato con cui visualizzare la stringa della data | Sì |
| `valueFormat` | `string` | Formato in cui memorizzare la stringa della data | Sì |

Offre inoltre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `valueFormat` non è soddisfatto | No |

##### Esempio {#sample-date-time}

```json
{
  "id": "date-time",
  "fields": [
    {
      "component": "date-time",
      "label": "Date & Time",
      "name": "date",
      "valueType": "date"
    }
  ]
}
```

```json
{
  "id": "another-date-time",
  "fields": [
    {
      "component": "date-time",
       "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

##### Schermata {#screenshot-date-time}

![Schermata del tipo di componente data e ora](assets/component-types/date-time.png)

#### Selezione multipla {#multiselect}

Un tipo di componente a selezione multipla presenta più elementi da selezionare in un elenco a discesa, inclusa la possibilità di raggruppare gli elementi selezionabili.

##### Esempi {#sample-multiselect}

```json
{
  "id": "multiselect",
  "fields": [
    {
      "component": "multiselect",
      "name": "multiselect",
      "label": "Multi Select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

```json
{
  "id": "multiselect-grouped",
  "fields": [
    {
      "component": "multiselect",
      "name": "property",
      "label": "Multiselect field",
      "valueType": "string",
      "required": true,
      "maxSize": 2,
      "options": [
        {
          "name": "Theme",
          "children": [
            { "name": "Light", "value": "light" },
            { "name": "Dark",  "value": "dark" }
          ]
        },
        {
          "name": "Type",
          "children": [
            { "name": "Alpha", "value": "alpha" },
            { "name": "Beta", "value": "beta" },
            { "name": "Gamma", "value": "gamma" }
          ]
        }
      ]
    }
  ]
}
```

##### Schermate {#screenshot-multiselect}

![Schermata del tipo di componente a selezione multipla](assets/component-types/multiselect.png)
![Schermata del tipo di componente a selezione multipla con raggruppamento](assets/component-types/multiselect-group.png)

#### Numero {#number}

Un tipo di componente numero consente di immettere un numero. Offre tipi di convalida aggiuntivi.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `numberMin` | `number` | Numero minimo consentito | No |
| `numberMax` | `number` | Numero massimo consentito | No |
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `numberMin` o `numberMax` non è soddisfatto | No |

##### Esempio {#sample-number}

```json
{
  "id": "number",
  "fields": [
    {
      "component": "number",
      "name": "number",
      "label": "Number",
      "valueType": "number",
      "value": 0
    }
  ]
}
```

```json
{
  "id": "another-number",
  "fields": [
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": 0,
        "numberMax": 88,
        "customErrorMsg": "You also need 1.21 gigawatts."
      }
    }
  ]
}
```

##### Schermata {#screenshot-number}

![Schermata del tipo di componente numero](assets/component-types/number.png)

#### Gruppo pulsanti di scelta {#radio-group}

Un tipo di componente gruppo di scelta consente una selezione reciprocamente esclusiva da più opzioni sottoposte a rendering come gruppo simile a un gruppo di caselle di controllo.

##### Esempio {#sample-radio-group}

```json
{
  "id": "radio-group",
  "fields": [
    {
      "component": "radio-group",
      "label": "Radio Group",
      "name": "radio",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

##### Schermata {#screenshot-radio-group}

![Schermata del tipo di componente del gruppo radio](assets/component-types/radio.png)

#### Riferimento {#reference}

Un tipo di componente di riferimento consente un riferimento a un altro oggetto dati dall&#39;oggetto corrente.

##### Esempio {#sample-reference}

```json
{
  "id": "reference",
  "fields": [
    {
      "component": "reference",
      "label": "Reference",
      "name": "reference",
      "valueType": "string"
    }
  ]
}
```

##### Schermata {#screenshot-reference}

![Schermata del tipo di componente di riferimento](assets/component-types/reference.png)

#### Seleziona {#select}

Un tipo di componente seleziona consente di selezionare una singola opzione da un elenco di opzioni predefinite in un menu a discesa.

##### Esempio {#sample-select}

```json
{
  "id": "select",
  "fields": [
    {
      "component": "select",
      "label": "Select",
      "name": "select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

##### Schermata {#screenshot-select}

![Schermata di selezione del tipo di componente](assets/component-types/select.png)

#### Linguetta {#tab}

Un tipo di componente Scheda consente di raggruppare altri campi di input in più schede per migliorare l’organizzazione del layout per gli autori.

A `tab` definizione può essere considerata come un separatore nell’array di `fields`. Tutto ciò che viene dopo un `tab` verrà inserito in quella scheda fino a quando non verrà `tab` viene rilevato, dopo di che i seguenti elementi verranno inseriti nella nuova scheda.

Se desideri che gli elementi vengano visualizzati sopra tutte le schede, è necessario definirli prima di qualsiasi scheda.

##### Esempio {#sample-tab}

```json
{
  "id": "tab",
  "fields": [
    {
      "component": "tab",
      "label": "Tab 1",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "label": "Text 1",
      "name": "text1",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Tab 2",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "label": "Text 2",
      "name": "text2",
      "valueType": "string"
    }
  ]
}
```

##### Schermata {#screenshot-tab}

![Schermata del tipo di componente Scheda](assets/component-types/tab.png)

#### Area testo {#text-area}

Un&#39;area di testo consente l&#39;immissione di testo RTF su più righe. Offre tipi di convalida aggiuntivi.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `maxSize` | `number` | Numero massimo di caratteri consentito | No |
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `maxSize` è stato superato | No |

##### Esempio {#sample-text-area}

```json
{
  "id": "richtext",
  "fields": [
    {
      "component": "text-area",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string"
    }
  ]
}
```

```json
{
  "id": "another-richtext",
  "fields": [
    {
      "component": "text-area",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string",
      "validation": {
        "maxSize": 1000,
        "customErrorMsg": "That's about as funny as a screen door on a battleship."
      }
    }
  ]
}
```

##### Schermata {#screenshot-text-area}

![Schermata del tipo di componente area di testo](assets/component-types/richtext.png)

#### Inserimento testo {#text-input}

Un input di testo consente di inserire una singola riga di testo.  Include tipi di convalida aggiuntivi.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `minLength` | `number` | Numero minimo di caratteri consentito | No |
| `maxLength` | `number` | Numero massimo di caratteri consentito | No |
| `regExp` | `string` | Espressione regolare che deve corrispondere al testo di input | No |
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `minLength`, `maxLength`, e/o `regExp` è/sono violato/i | No |

##### Esempio {#sample-text-input}

```json
{
  "id": "simpletext",
  "fields": [
    {
      "component": "text-input",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string"
    }
  ]
}
```

```json
{
  "id": "another simpletext",
  "fields": [
    {
      "component": "text-input",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string",
      "description": "This is a text input with validation.",
      "required": true,
      "validation": {
        "minLength": 1955,
        "maxLength": 1985,
        "regExp": "^foo:.*",
        "customErrorMsg": "Why don't you make like a tree and get outta here?"
      }
    }
  ]
}
```

##### Schermata {#screenshot-text-input}

![Schermata del tipo di componente di input testo](assets/component-types/simpletext.png)
