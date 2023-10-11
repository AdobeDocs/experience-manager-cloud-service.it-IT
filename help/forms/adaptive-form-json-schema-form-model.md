---
title: Come si progetta lo schema JSON per un modulo adattivo?
description: Scopri come creare uno schema JSON per un modulo adattivo e un modulo adattivo basato sullo schema per produrre i dati del reclamo per lo schema.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 8eeb9c5e-6866-4bfe-b922-1f028728ef0d
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 5%

---

# Progettazione di uno schema JSON per un modulo adattivo {#creating-adaptive-forms-using-json-schema}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-json-schema-form-model.html) |
| AEM as a Cloud Service | Questo articolo |


## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema JSON come modello di modulo è necessario conoscere a fondo lo schema JSON. Si consiglia di leggere attentamente il seguente contenuto prima di questo articolo.

* [Creazione di un modulo adattivo](creating-adaptive-form.md)
* [Schema JSON](https://json-schema.org/)

## Utilizzo di uno schema JSON come modello di modulo  {#using-a-json-schema-as-form-model}

I moduli Adobe Experience Manager supportano la creazione di un modulo adattivo utilizzando uno schema JSON esistente come modello di modulo. Questo schema JSON rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell’organizzazione. Lo schema JSON utilizzato deve essere conforme a [specifiche v4](https://json-schema.org/draft-04/schema).

Le funzioni chiave dell’utilizzo di uno schema JSON sono:

* La struttura del JSON viene visualizzata come struttura nella scheda Content Finder nella modalità di authoring di un modulo adattivo. Puoi trascinare e aggiungere un elemento dalla gerarchia JSON al modulo adattivo.
* Puoi precompilare il modulo utilizzando un JSON conforme allo schema associato.
* All’invio, i dati immessi dall’utente vengono inviati come JSON, in linea con lo schema associato.

Uno schema JSON è costituito da tipi di elementi semplici e complessi. Gli elementi dispongono di attributi che aggiungono regole all’elemento. Quando questi elementi e attributi vengono trascinati in un modulo adattivo, vengono mappati automaticamente al corrispondente componente Modulo adattivo.

La mappatura degli elementi JSON con i componenti del modulo adattivo è la seguente:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento JSON, proprietà o attributi</strong></th>
   <th><strong>Componente modulo adattivo</strong></th>
  </tr>
  <tr>
   <td><p>Proprietà stringa con vincolo enum ed enumNames.</p> <p>Sintassi,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente a discesa:</p>
    <ul>
     <li>I valori elencati in enumNames vengono visualizzati nella casella di riepilogo.</li>
     <li>I valori elencati nell'enum vengono utilizzati per il calcolo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Proprietà stringa con vincolo di formato. Ad esempio e-mail e data.</p> <p>Sintassi,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>Il componente E-mail viene mappato quando il tipo è stringa e il formato è e-mail.</li>
     <li>Il componente Textbox con convalida viene mappato quando il tipo è string (stringa) e il formato è hostname (nome host).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo di testo<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>proprietà number<br /> </td>
   <td>Campo numerico con sottotipo impostato su float<br /> </td>
  </tr>
  <tr>
   <td>proprietà integer<br /> </td>
   <td>Campo numerico con sottotipo impostato su integer<br /> </td>
  </tr>
  <tr>
   <td>proprietà booleana<br /> </td>
   <td>Interruttore<br /> </td>
  </tr>
  <tr>
   <td>proprietà oggetto<br /> </td>
   <td>Pannello<br /> </td>
  </tr>
  <tr>
   <td>proprietà array</td>
   <td>Pannello ripetibile con min e max uguali rispettivamente a minItems e maxItems. Sono supportati solo array omogenei. Pertanto, il vincolo items deve essere un oggetto e non un array.<br /> </td>
  </tr>
 </tbody>
</table>

### Proprietà comuni dello schema {#common-schema-properties}

Il modulo adattivo utilizza le informazioni disponibili nello schema JSON per mappare ogni campo generato. In particolare:

* Il `title` funge da etichetta per i componenti Modulo adattivo.
* Il `description` viene impostata come descrizione lunga per un componente Modulo adattivo.
* Il `default` funge da valore iniziale di un campo Modulo adattivo.
* Il `maxLength` la proprietà è impostata come `maxlength` attributo del componente campo di testo.
* Il `minimum`, `maximum`, `exclusiveMinimum`, e `exclusiveMaximum` Le proprietà vengono utilizzate per il componente Casella numerica.
* Per supportare l&#39;intervallo per `DatePicker component` proprietà aggiuntive dello schema JSON `minDate` e `maxDate` vengono fornite.
* Il `minItems` e `maxItems` Le proprietà vengono utilizzate per limitare il numero di elementi/campi che possono essere aggiunti o rimossi da un componente del pannello.
* Il `readOnly` imposta la proprietà `readonly` di un componente Modulo adattivo.
* Il `required` La proprietà contrassegna il campo Modulo adattivo come obbligatorio, mentre nel pannello (dove tipo è oggetto), i dati JSON finali inviati contengono campi con valore vuoto corrispondente a tale oggetto.
* Il `pattern` viene impostata come pattern di convalida (espressione regolare) in Adaptive Form.
* L’estensione del file di schema JSON deve essere mantenuta .schema.json. Ad esempio: &lt;filename>.schema.json.

## Schema JSON di esempio {#sample-json-schema}

Di seguito è riportato un esempio di schema JSON.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Definizioni di schema riutilizzabili {#reusable-schema-definitions}

Le chiavi di definizione vengono utilizzate per identificare gli schemi riutilizzabili. Per creare frammenti vengono utilizzate le definizioni di schema riutilizzabili. <!-- It is similar to identifying complex types in XSD.--> Di seguito è riportato un esempio di schema JSON con definizioni:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

L&#39;esempio precedente definisce un record cliente, in cui ogni cliente ha sia un indirizzo di spedizione che un indirizzo di fatturazione. La struttura di entrambi gli indirizzi è la stessa: gli indirizzi hanno un indirizzo stradale, una città e uno stato, quindi è consigliabile non duplicare gli indirizzi. Inoltre, agevola l’aggiunta e l’eliminazione dei campi per eventuali modifiche future.

## Preconfigurazione dei campi nella definizione dello schema JSON {#pre-configuring-fields-in-json-schema-definition}

È possibile utilizzare **aem:afProperties** per preconfigurare il campo Schema JSON da mappare a un componente modulo adattivo personalizzato. Di seguito è riportato un esempio:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

<!--- ## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Stepper</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Radio Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telephone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Switch</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Check Box</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Drop-down</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Image Choice</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Date Input Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Date Picker</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>File Attachment</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

```json

"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}

```
-->

## Limitare valori accettabili per un componente Modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

Per limitare i valori accettabili per un componente Modulo adattivo, puoi aggiungere le seguenti restrizioni agli elementi dello schema JSON:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per valori numerici e date. Per impostazione predefinita, il valore massimo è incluso.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico<br /> </li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite inferiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore minimo.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà maximum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà maximum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minimum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo devono essere maggiori o uguali al valore numerico o alla data specificati per la proprietà minimum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero minimo di caratteri consentito in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Stringa</td>
   <td>Specifica il numero massimo di caratteri consentiti in un componente. La lunghezza massima deve essere uguale o maggiore di zero.</td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al modello specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente Modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti Forms adattivi mappati su uno schema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Stringa</td>
   <td>Specifica il numero massimo di elementi in un array. Il numero massimo di elementi deve essere uguale o maggiore di zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Stringa</td>
   <td>Specifica il numero minimo di elementi in un array. Gli elementi minimi devono essere uguali o maggiori di zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>


## Abilita dati conformi allo schema {#enablig-schema-compliant-data}

Per abilitare tutti i Forms adattivi basati su schema JSON a generare dati conformi allo schema al momento dell’invio del modulo, effettua le seguenti operazioni:

1. Vai alla console web di Experience Manager all’indirizzo `https://server:host/system/console/configMgr`.
1. Individua **[!UICONTROL Configurazione del canale web per la comunicazione di moduli adattivi e interattivi]**.
1. Tocca per aprire la configurazione in modalità di modifica.
1. Seleziona la **[!UICONTROL Genera dati conformi allo schema]** casella di controllo.
1. Salva le impostazioni.

![configurazione di un modulo adattivo e di un canale web di comunicazione interattiva](/help/forms/assets/af-ic-web-channel-configuration.png)


## Costrutti non supportati  {#non-supported-constructs}

Forms adattivo non supporta i seguenti costrutti dello schema JSON:

* Tipo nullo
* tipi di unione, come eventuali, e
* Uno di, uno di, tutti e NON
* Sono supportati solo array omogenei. Pertanto, il vincolo items deve essere un oggetto e non un array.

## Domande frequenti {#frequently-asked-questions}

**Perché non è possibile trascinare singoli elementi di una sottomaschera (struttura generata da qualsiasi tipo complesso) per sottomaschere ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In una sottomaschera ripetibile, è necessario utilizzare la sottomaschera completa. Se desideri solo campi selettivi, utilizza l’intera struttura ed elimina quelli indesiderati.

**In Content Finder ho una struttura lunga e complessa. Come posso trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorri nella struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Quale deve essere l’estensione del file di schema JSON?**

L’estensione del file dello schema JSON deve essere .schema.json. Ad esempio: &lt;filename>.schema.json.
