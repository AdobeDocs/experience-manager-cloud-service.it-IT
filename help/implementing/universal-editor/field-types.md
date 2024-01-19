---
title: Tipi di campi
description: Scopri i diversi tipi di campi che l’Editor universale può modificare nella barra dei componenti, con esempi di come puoi creare strumenti per la tua app.
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 7%

---


# Tipi di campi {#field-types}

Scopri i diversi tipi di campi che l’Editor universale può modificare nella barra dei componenti, con esempi di come puoi creare strumenti per la tua app.

{{universal-editor-status}}

## Panoramica {#overview}

Quando adattate le vostre app per l’utilizzo con Universal Editor, dovete dotare gli strumenti dei componenti e definire quali tipi di dati possono essere manipolati nella barra dei componenti dell’editor.

Questo documento fornisce una panoramica dei tipi di campo disponibili, insieme ad esempi di configurazioni.

>[!TIP]
>
>Se non sai come dotare l’app dell’editor universale, consulta il documento [Panoramica di Universal Editor per sviluppatori AEM.](/help/implementing/universal-editor/developer-overview.md)

## Booleano {#boolean}

Un campo booleano memorizza un semplice valore true/false renderizzato come una casella di controllo.

### Esempio {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## Gruppo di caselle di controllo {#checkbox-group}

Analogamente a un valore booleano, un gruppo di caselle di controllo consente la selezione di più elementi true/false.

### Esempio {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## Data e ora {#date-time}

Un campo data/ora consente di specificare una data, un’ora o una combinazione di queste.

### Esempio {#sample-date-time}

```json
{
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

## Numero {#number}

Un campo numerico consente di immettere un numero.

### Esempio {#sample-number}

```json
{
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
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## Gruppo pulsanti di scelta {#radio-group}

Un gruppo di scelta consente una selezione reciprocamente esclusiva da più opzioni sottoposte a rendering come gruppo simile a un gruppo di caselle di controllo.

### Esempio {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## Riferimento {#reference}

Un riferimento consente di specificare un altro oggetto dati come riferimento dall&#39;oggetto corrente.

## Seleziona {#select}

Una selezione consente di selezionare una o più opzioni predefinite in un menu a discesa.

### Esempio {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## Area testo {#text-area}

Un&#39;area di testo consente l&#39;immissione di testo su più righe.

### Esempio {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## Inserimento testo {#text-input}

Un input di testo consente di inserire una singola riga di testo.

### Esempio {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## Linguetta {#tab}

Una scheda consente di raggruppare altri campi di input in più schede per migliorare l’organizzazione del layout per gli autori.

A `tab` definizione può essere considerata come un separatore nell’array di `fields`. Tutto ciò che viene dopo un `tab` verrà inserito in quella scheda fino a quando non verrà `tab` viene rilevato, dopo di che i seguenti elementi verranno inseriti nella nuova scheda.

Se desideri che gli elementi vengano visualizzati sopra tutte le schede, è necessario definirli prima di qualsiasi scheda.

### Esempio {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```
