---
title: Proprietà campo di blocco Forms adattivo per la masterizzazione
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e proprietà dei campi a blocchi adattivi di Forms. Questa guida elenca tutte le proprietà supportate dal blocco Forms EDS.
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---


# Proprietà campo di blocco Forms adattivo

In questo documento viene riepilogato il modo in cui lo schema JSON viene mappato su HTML sottoposto a rendering in `blocks/form/form.js`, concentrandosi su come vengono identificati e renderizzati i campi, sui pattern comuni e sulle differenze specifiche dei campi.

## Identificazione Dei Campi (`fieldType`)

Ogni campo nello schema JSON ha una proprietà `fieldType` che determina come viene eseguito il rendering. `fieldType` può essere:

- **Tipo speciale**\
  Esempi: `drop-down`, `radio-group`, `checkbox-group`, `panel`, `plain-text`, `image`, `heading`, ecc.
- **Tipo di input HTML valido**\
  Esempi: `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file`, ecc.
- **Tipo con suffisso `-input`**\
  Esempi: `text-input`, `number-input`, ecc. normalizzato al tipo di base, ad esempio `text`, `number`.

Se `fieldType` corrisponde a un tipo speciale, viene utilizzato un **renderer personalizzato**. In caso contrario, verrà trattato come **tipo di input predefinito**.

Vedere le sezioni seguenti per la struttura e le proprietà [complete di HTML](#common-html-structure) per ogni tipo di campo.

## Proprietà comuni utilizzate dai campi

Di seguito sono riportate le proprietà utilizzate dalla maggior parte dei campi:

- `id`: specifica l&#39;ID dell&#39;elemento e supporta l&#39;accessibilità.
- `name`: definisce l&#39;attributo `name` per gli elementi di input, selezione o set di campi.
- `label.value`, `label.richText`, `label.visible`: specifica l&#39;etichetta/testo della legenda, il contenuto di HTML e la visibilità.
- `value`: rappresenta il valore corrente del campo.
- `required`: aggiunge l&#39;attributo `required` o i dati di convalida.
- `readOnly`, `enabled`: controlla se il campo è modificabile o disabilitato.
- `description`: visualizza il testo della Guida sotto il campo.
- `tooltip`: imposta l&#39;attributo `title` per gli input.
- `constraintMessages`: fornisce messaggi di errore personalizzati come attributi di dati.

## Struttura comune di HTML

Il rendering della maggior parte dei campi viene eseguito all&#39;interno di un wrapper che include un&#39;etichetta e un testo di aiuto facoltativo. Lo snippet seguente illustra la struttura:

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

Per i gruppi (radio/casella di controllo) e i pannelli, viene utilizzato `<fieldset>` con `<legend>` invece di `<div>/<label>`. Testo della guida <div> è presente solo se è impostata la descrizione.

## Visualizzazione messaggio di errore

I messaggi di errore vengono visualizzati nello stesso elemento `.field-description` utilizzato per il testo della Guida, che viene aggiornato dinamicamente.

**Quando un campo non è valido**:

- Al wrapper (ad esempio, `.field-wrapper`) viene assegnata la classe `.field-invalid`.
- Il contenuto di `.field-description` viene sostituito con il messaggio di errore corrispondente.

**Quando il campo diventa valido**:

- La classe `.field-invalid` è stata rimossa.
- `.field-description` viene ripristinato al testo della Guida originale (se disponibile) o rimosso se non ne esiste alcuno.

I messaggi di errore personalizzati possono essere definiti utilizzando la proprietà `constraintMessages` nel JSON.\
Questi vengono aggiunti come `data-<constraint>ErrorMessage` attributi nel wrapper (ad esempio, `data-requiredErrorMessage`).

## Tipi di input predefiniti (HTML Input o `*-input`)

Se `fieldType` non è un tipo speciale, verrà considerato come un tipo di input HTML standard o come `<type>-input`, ad esempio `text`, `number`, `email`, `date`, `text-input`, `number-input`.

- Il suffisso `-input` è rimosso e il tipo di base viene utilizzato come attributo `type` dell&#39;input.
- Questi tipi vengono gestiti per impostazione predefinita in `renderField()`.
I tipi di input predefiniti comuni sono `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file` e così via.  Accettano anche `text-input`, `number-input`, ecc., che sono normalizzati al tipo di base.

## Vincoli per i tipi di input predefiniti

I vincoli vengono aggiunti come attributi sull’elemento di input in base alle proprietà JSON.

| Proprietà JSON | Attributo HTML | Si applica a |
|--------------|---------------|------------|
| maxLength | maxlength | testo, e-mail, password, tel |
| minLength | minlength | testo, e-mail, password, tel |
| pattern | pattern | testo, e-mail, password, tel |
| massimo | max | numero, intervallo, data |
| minimo | min. | numero, intervallo, data |
| passaggio | passaggio | numero, intervallo, data |
| accetta | accetta | file |
| multiplo | multiplo | file |
| maxOccur | data-max | pannello |
| minOccur | data-min | pannello |

>[!NOTE]
>
> `multiple` è una proprietà booleana. Se true, viene aggiunto l&#39;attributo `multiple`.

Questi attributi vengono impostati automaticamente dal renderer del modulo in base alla definizione JSON del campo.

## Esempio: struttura HTML con vincoli

L’esempio seguente illustra come viene eseguito il rendering di un campo numerico con vincoli di convalida e attributi di gestione degli errori.

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

Ogni parte della struttura di HTML svolge un ruolo nell&#39;associazione dati, nella convalida e nella visualizzazione di messaggi di aiuto o di errore.

## Proprietà specifiche dei campi e relative strutture HTML

### Elenchi a discesa

**Proprietà aggiuntive:**

- `enum` / `enumNames`: definire i valori delle opzioni e le relative etichette di visualizzazione per il menu a discesa.
- `type`: abilita la selezione multipla se impostata su `array`.
- `placeholder`: aggiunge un&#39;opzione segnaposto disabilitata per guidare gli utenti prima della selezione.

Esempio:

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Testo normale

**Proprietà aggiuntive**:

- `richText`: se true, esegue il rendering di HTML nel paragrafo.

Esempio:

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### Casella di controllo

**Proprietà aggiuntive**:

- `enum`: definisce i valori per lo stato selezionato e deselezionato della casella di controllo.
- `properties.variant / properties.alignment`: specifica lo stile di visualizzazione e l&#39;allineamento per le caselle di controllo di tipo switch.

Esempio:

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Pulsante

**Proprietà aggiuntive**:

- `buttonType`: specifica il comportamento del pulsante impostandone il tipo (pulsante, invio o ripristino).

Esempio:

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### Ingresso multiriga

**Proprietà aggiuntive**:

- `minLength`: specifica il numero minimo di caratteri consentito in un input di testo o di area di testo.
- `maxLength`: specifica il numero massimo di caratteri consentito in un input di testo o di area di testo.
- `pattern`: definisce un&#39;espressione regolare che il valore di input deve corrispondere per essere considerata valida.
- `placeholder`: visualizza il testo segnaposto all&#39;interno dell&#39;area di input o di testo fino all&#39;immissione di un valore.

Esempio:

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Pannello

**Proprietà aggiuntive**:

- `repeatable`: specifica se il pannello può essere ripetuto dinamicamente.
- `minOccur`: imposta il numero minimo di istanze del pannello richieste.   maxOccur: imposta il numero massimo di istanze di pannello consentite.
- `properties.variant`: definisce lo stile visivo o la variante del pannello.
- `properties.colspan`: specifica il numero di colonne contenute nel pannello in un layout griglia.
- `index`: indica la posizione del pannello all&#39;interno del relativo contenitore principale.
- `fieldset`: raggruppa campi correlati in un elemento `<fieldset>` con una legenda o un&#39;etichetta.

Esempio:

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Pulsante di scelta

**Proprietà aggiuntive**:

- `enum`: definisce il set di valori consentiti per il campo di opzione, utilizzato come attributo di valore per ogni opzione del pulsante di opzione.

Esempio:

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Gruppo pulsanti di scelta

**Proprietà aggiuntive**:

- `enum`: definisce l&#39;elenco di valori di opzione per il gruppo di opzioni, utilizzato come valore di ogni pulsante di opzione.
- `enumNames`: fornisce etichette di visualizzazione per i pulsanti di scelta, che corrispondono all&#39;ordine di enumerazione.

Esempio:

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **Gruppo di caselle di controllo**

**Proprietà aggiuntive**:

- `enum`: definisce l&#39;elenco di valori di opzione per il gruppo di caselle di controllo, utilizzato come valore di ogni casella di controllo.
- `enumNames`: fornisce etichette di visualizzazione per le caselle di controllo, che corrispondono all&#39;ordine di enumerazione.
- `minItems`: imposta il numero minimo di caselle di controllo che devono essere selezionate per la validità.
- `maxItems`: imposta il numero massimo di caselle di controllo che è possibile selezionare prima di attivare un errore.

Esempio:

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Immagine

**Proprietà aggiuntive**:

- `value / properties['fd:repoPath']`: definisce il percorso di origine dell&#39;immagine o il percorso dell&#39;archivio per il rendering dell&#39;immagine.
- `altText`: fornisce testo alternativo per l&#39;immagine (attributo alt) per migliorare l&#39;accessibilità.

Esempio:

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### Intestazione

**Proprietà aggiuntive**:

- `value`: specifica il contenuto del testo da visualizzare nell&#39;elemento intestazione (ad esempio, `<h2>`).

Esempio:

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

Per ulteriori dettagli, vedere l&#39;implementazione in `blocks/form/form.js` e `blocks/form/util.js`.


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->

