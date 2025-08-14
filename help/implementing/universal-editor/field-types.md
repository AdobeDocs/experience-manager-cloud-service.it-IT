---
title: Definizioni di modelli, campi e tipi di componenti
description: Scopri i campi e i tipi di componenti che l’Editor universale può modificare nel pannello delle proprietà con alcuni esempi. Scopri come creare una definizione di modello e un collegamento al componente per sfruttare al meglio la tua app.
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 11%

---


# Definizioni di modelli, campi e tipi di componenti {#field-types}

Scopri i campi e i tipi di componenti che l’Editor universale può modificare nel pannello delle proprietà con alcuni esempi. Scopri come creare una definizione di modello e un collegamento al componente per sfruttare al meglio la tua app.

## Panoramica {#overview}

Quando adattate le vostre app per l&#39;uso con l&#39;Editor universale, dovete instrumentare i componenti e definire quali campi e tipi di componenti possono essere manipolati nel pannello delle proprietà dell&#39;editor. A tale scopo, crea un modello e crea un collegamento a tale modello dal componente.

Questo documento fornisce una panoramica della definizione di un modello, dei campi e dei tipi di componenti disponibili, insieme ad esempi di configurazioni.

>[!TIP]
>
>Se non sai come gestire l&#39;app per l&#39;editor universale, consulta il documento [Panoramica dell&#39;editor universale per sviluppatori AEM](/help/implementing/universal-editor/developer-overview.md).

## Struttura definizione modello {#model-structure}

Per configurare un componente tramite il pannello delle proprietà nell’Editor universale, è necessario che esista una definizione di modello e che tale definizione sia collegata al componente.

La definizione del modello è una struttura JSON che inizia con un array di modelli.

```json
[
  {
    "id": "model-id",        // must be unique
    "fields": []             // array of fields which shall be rendered in the properties panel
  }
]
```

Consulta la sezione **[Fields](#fields)** di questo documento per ulteriori informazioni su come definire l&#39;array `fields`.

È possibile collegare un modello a un componente in due modi: utilizzando la [definizione del componente](#component-definition) o [tramite la strumentazione.](#instrumentation)

### Collegamento tramite la definizione del componente {#component-definition}

Questo è il metodo preferito per collegare il modello al componente. In questo modo puoi mantenere il collegamento a livello centrale nella definizione del componente e consentire il trascinamento dei componenti tra i contenitori.

È sufficiente includere la proprietà `model` nell&#39;oggetto componente nell&#39;array `components` nel file `component-definition.json`.

Per informazioni dettagliate, vedere il documento [Definizione del componente.](/help/implementing/universal-editor/component-definition.md)

### Collegamento tramite strumentazione {#instrumentation}

Per utilizzare la definizione del modello con un componente, è possibile utilizzare l&#39;attributo `data-aue-model`.

```html
<div data-aue-resource="urn:datasource:/content/path" data-aue-type="component"  data-aue-model="model-id">Click me</div>
```

>[!NOTE]
>
>Prima di controllare la definizione del componente, Universal Editor controlla se un modello è collegato tramite la strumentazione e lo utilizza. Ciò significa che:
>
>* I progetti che hanno implementato il collegamento al modello tramite la strumentazione continueranno a funzionare così come sono senza bisogno di modifiche.
>* Se si definisce il modello nella [definizione del componente](#component-definition) e nella strumentazione, la strumentazione verrà sempre utilizzata.

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
| `name` | `string` | Proprietà [o percorso](#nesting) in cui i dati devono essere persistenti | Sì |
| `label` | `FieldLabel` | Etichetta del campo | Sì |
| `description` | `FieldDescription` | Descrizione del campo | No |
| `placeholder` | `string` | Segnaposto per il campo | No |
| `value` | `FieldValue` | Valore predefinito | No |
| `valueType` | `ValueType` | Convalida standard, può essere `string`, `string[]`, `number`, `date`, `boolean` | No |
| `required` | `boolean` | Il campo è obbligatorio | No |
| `readOnly` | `boolean` | Campo di sola lettura | No |
| `hidden` | `boolean` | Campo nascosto per impostazione predefinita | No |
| `condition` | `RulesLogic` | Regola per mostrare o nascondere il campo in base a una [condizione](/help/implementing/universal-editor/customizing.md#conditionally-hide) | No |
| `multi` | `boolean` | Il campo è multicampo<br/>Si noti che la nidificazione dei contenitori non è consentita per i campi multipli nel pannello delle proprietà | No |
| `validation` | `ValidationType` | Regola o regole di convalida per il campo | No |
| `raw` | `unknown` | Dati non elaborati che possono essere utilizzati dal componente | No |

### nome Campo e nidificazione {#nesting}

Il campo `name` può puntare direttamente a una proprietà della risorsa corrente oppure, nel caso di componenti in `cq:Pages`, può anche utilizzare un percorso a una proprietà nidificata. Ad esempio:

```json
"name": "teaser/image/fileReference"
```

### Tipi componente {#component-types}

Di seguito sono elencati i tipi di componenti che è possibile utilizzare per il rendering dei campi.

| Descrizione | Tipo componente |
|---|---|
| [Tag AEM](#aem-tag) | `aem-tag` |
| [Contenuto AEM](#aem-content) | `aem-content` |
| [Booleano](#boolean) | `boolean` |
| [Gruppo di caselle di controllo](#checkbox-group) | `checkbox-group` |
| [Contenitore](#container) | `container` |
| [Frammento di contenuto](#content-fragment) | `aem-content-fragment` |
| [Data e ora](#date-time) | `date-time` |
| [Frammento esperienza](#experience-fragment) | `aem-experience-fragment` |
| [Selezione multipla](#multiselect) | `multiselect` |
| [Numero](#number) | `number` |
| [Gruppo pulsanti di scelta](#radio-group) | `radio-group` |
| [Riferimento](#reference) | `reference` |
| [Formato RTF](#rich-text) | `richtext` |
| [Seleziona](#select) | `select` |
| [Scheda](#tab) | `tab` |
| [Testo](#text) | `text` |

#### Tag AEM {#aem-tag}

Un tipo di componente Tag di AEM abilita un selettore di tag di AEM, che può essere utilizzato per allegare i tag al componente.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente tag di AEM](assets/component-types/aem-tag-picker.png)

>[!ENDTABS]

>[!TIP]
>
>Per ulteriori informazioni su come utilizzare i fogli di calcolo per gestire i dati della tassonomia per il progetto Edge Delivery Services, vedere il documento [Gestione dei dati della tassonomia](https://www.aem.live/docs/authoring-taxonomy).

#### Contenuto AEM {#aem-content}

Un tipo di componente contenuto di AEM abilita un selettore di contenuti di AEM, che può essere utilizzato per selezionare qualsiasi risorsa AEM. A differenza del [componente di riferimento](#reference), che può selezionare solo le risorse, il componente di contenuto AEM può fare riferimento a qualsiasi contenuto AEM. Offre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `rootPath` | `string` | Percorso che il selettore contenuto aprirà per consentire all’utente di selezionare il contenuto di AEM, limitando la selezione a tale directory e sottodirectory | No |

>[!BEGINTABS]

>[!TAB Esempio]

```json
{
  "id": "aem-content-picker",
  "fields": [
    {
      "component": "aem-content",
      "name": "reference",
      "value": "",
      "label": "AEM Content Picker",
      "valueType": "string",
      "validation": {
            "rootPath": "/content/refresh"
        }
    }
  ]
}
```

>[!TAB Schermata]

![Schermata del tipo di componente contenuto di AEM](assets/component-types/aem-content-picker.png)

>[!ENDTABS]

#### Booleano {#boolean}

Un tipo di componente booleano memorizza un semplice valore true/false renderizzato come un interruttore. Offre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se il valore immesso non è un valore booleano | No |

>[!BEGINTABS]

>[!TAB Esempio 1]

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

>[!TAB Esempio 2]

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

>[!TAB Schermata]

![Schermata del tipo di componente booleano](assets/component-types/boolean.png)

>[!ENDTABS]

#### Gruppo di caselle di controllo {#checkbox-group}

Simile a un booleano, un tipo di componente gruppo casella di controllo consente la selezione di più elementi true/false, riprodotti come più caselle di controllo.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente gruppo casella di controllo](assets/component-types/checkbox-group.png)

>[!ENDTABS]

#### Contenitore {#container}

Un tipo di componente contenitore consente il raggruppamento di componenti, incluso il supporto per più campi. Offre una configurazione aggiuntiva. La nidificazione dei contenitori non è consentita per i campi multipli nel pannello delle proprietà

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `collapsible` | `boolean` | Il contenitore è comprimibile | No |

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente contenitore](assets/component-types/container.png)

>[!TAB Supporto Multifield]

```json
{
  "component": "container",
  "name": "test",
  "label": "Multi Text",
  "multi": true,
  "fields": [
    {
      "component": "reference",
      "name": "image",
      "value": "",
      "label": "Sample Image",
      "valueType": "string"
    },
    {
      "component": "text",
      "name": "alt",
      "value": "",
      "label": "Alt Text",
      "valueType": "string"
    }
  ]
}
```

>[!ENDTABS]



#### Frammenti di contenuto {#content-fragment}

Il selettore Frammento di contenuto può essere utilizzato per selezionare un [Frammento di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md) e le relative varianti (se necessario). Offre una configurazione aggiuntiva.

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `variationName` | `string` | Nome della variabile per memorizzare la variante selezionata. Se non è definito, non viene visualizzato alcun selettore varianti | No |

Offre inoltre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `rootPath` | `string` | Percorso che il selettore contenuto aprirà per consentire all’utente di selezionare il Frammento di contenuto, limitando la selezione a tale directory e sottodirectory | No |

>[!NOTE]
>
>L&#39;editor universale [convalida i campi dei frammenti di contenuto in base ai relativi modelli](/help/assets/content-fragments/content-fragments-models.md#validation), consentendo di applicare le regole di integrità dei dati, ad esempio i pattern regex e i vincoli di univocità.
>
>In questo modo, il contenuto soddisfa i requisiti aziendali specifici prima della pubblicazione.

>[!BEGINTABS]

>[!TAB Esempio 1]

```json
[
  {
    "id": "aem-content-fragment",
    "fields": [
      {
        "component": "aem-content-fragment",
        "name": "picker",
        "label": "Content Fragment Picker",
        "valueType": "string",
        "variationName": "contentFragmentVariation",
        "validation": {
            "rootPath": "/content/refresh"
        }
      }
    ]
  }
]
```

>[!TAB Schermata]

![Schermata del selettore frammenti di contenuto](assets/component-types/aem-content-fragment.png)

>[!ENDTABS]

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

>[!BEGINTABS]

>[!TAB Esempio 1]

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

>[!TAB Esempio 2]

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

>[!TAB Schermata]

![Schermata del tipo di componente data e ora](assets/component-types/date-time.png)

>[!ENDTABS]

#### Frammento di esperienza {#experience-fragment}

Il selettore Frammento esperienza può essere utilizzato per selezionare un [Frammento esperienza](/help/sites-cloud/authoring/fragments/experience-fragments.md) e le relative varianti (se necessario). Offre una configurazione aggiuntiva.

| Configurazione | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `variationName` | `string` | Nome della variabile per memorizzare la variante selezionata. Se non è definito, non viene visualizzato alcun selettore varianti | No |

Offre inoltre un tipo di convalida aggiuntivo.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `rootPath` | `string` | Percorso che il selettore contenuto aprirà per consentire all’utente di selezionare il frammento di esperienza, limitando la selezione a tale directory e sottodirectory | No |

>[!BEGINTABS]

>[!TAB Esempio 1]

```json
[
  {
    "id": "experience-fragment",
    "fields": [
      {
        "component": "aem-experience-fragment",
        "valueType": "string",
        "name": "experience-fragment",
        "label": "experience-fragment",
        "variationName": "experienceFragmentVariation",
        "validation": {
            "rootPath": "/content/refresh"
        }
      }
    ]
  }
]
```

>[!TAB Schermata]

![Schermata del selettore frammenti esperienza](assets/component-types/aem-experience-fragment.png)

>[!ENDTABS]


#### Selezione multipla {#multiselect}

Un tipo di componente a selezione multipla presenta più elementi da selezionare in un elenco a discesa, inclusa la possibilità di raggruppare gli elementi selezionabili.

>[!BEGINTABS]

>[!TAB Esempio 1]

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

>[!TAB Esempio 2]

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

>[!TAB Schermate]

![Schermata del tipo di componente a selezione multipla](assets/component-types/multiselect.png)
![Schermata del tipo di componente a selezione multipla con raggruppamento](assets/component-types/multiselect-group.png)

>[!ENDTABS]

#### Numero {#number}

Un tipo di componente numero consente di immettere un numero. Offre tipi di convalida aggiuntivi.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `numberMin` | `number` | Numero minimo consentito | No |
| `numberMax` | `number` | Numero massimo consentito | No |
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `numberMin` o `numberMax` non è soddisfatto | No |

>[!BEGINTABS]

>[!TAB Esempio 1]

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

>[!TAB Esempio 2]

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

>[!TAB Schermata]

![Schermata del tipo di componente numero](assets/component-types/number.png)

>[!ENDTABS]

#### Gruppo pulsanti di scelta {#radio-group}

Un tipo di componente gruppo di scelta consente una selezione reciprocamente esclusiva da più opzioni sottoposte a rendering come gruppo simile a un gruppo di caselle di controllo.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente del gruppo radio](assets/component-types/radio.png)

>[!ENDTABS]

#### Riferimento {#reference}

Un tipo di componente di riferimento abilita un selettore risorse di AEM, che può essere utilizzato per selezionare qualsiasi risorsa di AEM a cui fare riferimento. A differenza del [componente contenuto AEM](#aem-content), che può selezionare qualsiasi risorsa AEM, il componente di riferimento può fare riferimento solo alle risorse. Offre un tipo di convalida aggiuntivo.

Un tipo di componente di riferimento consente un riferimento a un altro oggetto dati dall&#39;oggetto corrente.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente di riferimento](assets/component-types/reference.png)

>[!ENDTABS]

#### Testo formattato {#rich-text}

Il testo RTF consente l’inserimento di testo RTF su più righe.

>[!BEGINTABS]

>[!TAB Esempio 1]

```json
{
  "id": "richtext",
  "fields": [
    {
      "component": "richtext",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB Schermata]

![Schermata del tipo di componente area di testo](assets/component-types/richtext.png)

>[!ENDTABS]

#### Seleziona {#select}

Un tipo di componente seleziona consente di selezionare una singola opzione da un elenco di opzioni predefinite in un menu a discesa.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente selezionato](assets/component-types/select.png)

>[!ENDTABS]

#### Tab {#tab}

Un tipo di componente Scheda consente di raggruppare altri campi di input in più schede per migliorare l’organizzazione del layout per gli autori.

Una definizione di `tab` può essere considerata come un separatore nell&#39;array di `fields`. Tutto ciò che arriva dopo un `tab` verrà inserito in quella scheda fino a quando non si incontra un nuovo `tab`, dopo di che i seguenti elementi verranno inseriti nella nuova scheda.

Se desideri che gli elementi vengano visualizzati sopra tutte le schede, è necessario definirli prima di qualsiasi scheda.

>[!BEGINTABS]

>[!TAB Esempio]

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

>[!TAB Schermata]

![Schermata del tipo di componente Scheda](assets/component-types/tab.png)

>[!ENDTABS]

#### Testo {#text}

Il testo consente di inserire una singola riga di testo.  Include tipi di convalida aggiuntivi.

| Tipo di convalida | Tipo di valore | Descrizione | Obbligatorio |
|---|---|---|---|
| `minLength` | `number` | Numero minimo di caratteri consentito | No |
| `maxLength` | `number` | Numero massimo di caratteri consentito | No |
| `regExp` | `string` | Espressione regolare che deve corrispondere al testo di input | No |
| `customErrorMsg` | `string` | Messaggio che verrà visualizzato se `minLength`, `maxLength` e/o `regExp` sono violati | No |

>[!BEGINTABS]

>[!TAB Esempio 1]

```json
{
  "id": "simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string"
    }
  ]
}
```

>[!TAB Esempio 2]

```json
{
  "id": "another simpletext",
  "fields": [
    {
      "component": "text",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string",
      "valueFormat": "regexp",
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

>[!TAB Schermata]

![Schermata del tipo di componente testo](assets/component-types/simpletext.png)

>[!ENDTABS]
