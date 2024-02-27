---
title: Personalizzare tema e stile per un modulo del servizio di consegna AEM Forms Edge
description: Personalizzare tema e stile per un modulo del servizio di consegna AEM Forms Edge
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---


# Applicazione di stili ai campi modulo

Forms è fondamentale per l’interazione degli utenti sui siti web, consentendo loro di inserire dati. Questa guida illustra i concetti fondamentali relativi allo stile di vari campi modulo all’interno di [Blocco modulo](/help/edge/docs/forms/create-forms.md), per creare moduli visivi accattivanti e facili da usare.

## Informazioni sui tipi di campi modulo

Prima di iniziare a utilizzare gli stili, esaminiamo i tipi di campi modulo comuni supportati dal blocco modulo:

* Campi di input: includono input di testo, input di e-mail, input di password e altro ancora.
* Gruppi di caselle di controllo: utilizzato per selezionare più opzioni.
* Gruppi di opzioni: utilizzato per selezionare una sola opzione da un gruppo.
* Elenchi a discesa: noti anche come caselle di selezione, utilizzati per selezionare un’opzione da un elenco.
* Pannelli/contenitori: utilizzato per raggruppare gli elementi modulo correlati.

## Principi di base dello stile

Comprendere i concetti fondamentali di CSS è fondamentale prima di formattare campi modulo specifici:

* Selettori: i selettori CSS ti consentono di eseguire il targeting di elementi HTML specifici per lo stile. Puoi utilizzare i selettori di elementi, di classi o di ID.
* Proprietà: le proprietà CSS definiscono l’aspetto visivo degli elementi. Le proprietà comuni per la formattazione dei campi modulo includono colore, colore di sfondo, bordo, riempimento, margine e altro ancora.
* Modello casella: il modello casella CSS descrive la struttura degli elementi HTML come un&#39;area di contenuto circondata da spaziature, bordi e margini.
* Flexbox/Grid: i layout CSS Flexbox e Grid sono strumenti potenti per la creazione di progettazioni dinamiche e flessibili.

## Applicazione di uno stile a un modulo per un blocco di modulo

Il blocco di modulo offre una struttura di HTML standardizzata che semplifica la selezione e lo stile dei componenti del modulo:

* **Aggiorna stili predefiniti**: è possibile modificare gli stili predefiniti di un modulo modificando il `/blocks/form/form.css file`. Questo file offre uno stile completo per un modulo, con supporto per i moduli della procedura guidata in più passaggi. Viene enfatizzato l’utilizzo di variabili CSS personalizzate per una facile personalizzazione, manutenzione e uno stile uniforme tra i moduli. Per istruzioni sull’aggiunta del blocco di modulo al progetto, consulta [creare un modulo](/help/edge/docs/forms/create-forms.md).

* **Personalizzazione**: utilizza il valore predefinito `forms.css` come base e personalizzarla per modificare l’aspetto dei componenti del modulo, rendendolo visivamente accattivante e di facile utilizzo. La struttura del file incoraggia l’organizzazione e mantiene gli stili per i moduli, promuovendo progettazioni coerenti all’interno del sito web.

## Raggruppamento della struttura di forms.css

* **Variabili globali:** Definito in corrispondenza di `:root` livello, queste variabili (`--variable-name`) memorizzare i valori utilizzati nel foglio di stile per garantire coerenza e facilità di aggiornamento. Queste variabili definiscono i colori, le dimensioni dei caratteri, la spaziatura interna e altre proprietà. Puoi dichiarare le tue variabili globali o modificare quelle esistenti per modificare lo stile del modulo.

* **Stili selettore universale:** Il `*` Il selettore corrisponde a ogni elemento del modulo, garantendo che gli stili vengano applicati a tutti i componenti per impostazione predefinita, inclusa l’impostazione di `box-sizing` proprietà a `border-box`.

* **Stile modulo:** Questa sezione descrive come formattare i componenti del modulo utilizzando i selettori per eseguire il targeting di elementi HTML specifici. Definisce gli stili per i campi di input, le aree di testo, le caselle di controllo, i pulsanti di scelta, gli input di file, le etichette dei moduli e le descrizioni.

* **Stile procedura guidata (se applicabile):** Questa sezione è dedicata allo stile del layout della procedura guidata, un modulo con più passaggi in cui ogni passaggio viene visualizzato uno alla volta. Definisce gli stili per il contenitore della procedura guidata, i set di campi, le legende, i pulsanti di navigazione e i layout reattivi.

* **Query multimediali:** che offrono stili per schermi di diverse dimensioni, con conseguente regolazione del layout e dello stile.

* **Stili vari:**: questa sezione descrive gli stili dei messaggi di errore o di successo, le aree di caricamento dei file e altri elementi che potrebbero verificarsi in un modulo.


## Struttura dei componenti

Il blocco modulo offre una struttura HTML coerente per vari elementi del modulo, garantendo una gestione e uno stile più semplici. Puoi manipolare i componenti utilizzando i CSS a scopo di stile.

### Componenti generali (ad eccezione di elenchi a discesa, gruppi di scelta e gruppi di caselle di controllo):

Tutti i campi modulo, ad eccezione di elenchi a discesa, gruppi di scelta e gruppi di caselle di controllo, hanno la seguente struttura HTML:

#### Struttura HTML

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* Classi: l’elemento div dispone di diverse classi per il targeting di elementi e stili specifici. È necessario `form-{Type}-wrapper` o `form-{Name}` classi per sviluppare un selettore CSS per assegnare uno stile a un campo modulo:
   * {Type}: identifica il componente per tipo di campo. Ad esempio, testo (modulo-testo-wrapper), numero (modulo-numero-wrapper), data (modulo-data-wrapper).
   * {Name}: identifica il componente in base al nome. Il nome del campo può contenere solo caratteri alfanumerici; i più trattini consecutivi nel nome vengono sostituiti da un singolo trattino `(-)`, e i trattini iniziale e finale nel nome di un campo vengono rimossi. Ad esempio, nome (form-first-name field-wrapper).
   * {FieldId}: è un identificatore univoco del campo, generato automaticamente.
   * {Required}: valore booleano che indica se il campo è obbligatorio.
* Label: il `label` fornisce un testo descrittivo per il campo e lo associa all&#39;elemento di input utilizzando `for` attributo.
* Input: Il `input` definisce il tipo di dati da immettere. Ad esempio, testo, numero, e-mail.
* Descrizione (Facoltativa): `div` con classe `field-description` fornisce informazioni o istruzioni aggiuntive per l’utente.

**Esempio di struttura HTML**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**Selettore CSS per componenti generali**

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`: indirizza l’esterno `div` in base al tipo di campo. Ad esempio: `.form-text-wrapper` esegue il targeting di tutti i campi di input di testo.
* `.form-{Name}`: seleziona ulteriormente l’elemento in base al nome del campo specifico. Ad esempio: `.form-first-name` esegue il targeting del campo di testo &quot;Nome&quot;.

**Esempio di selettori CSS per componenti generali**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### Componente a discesa

Per i menu a discesa, il `select` viene utilizzato al posto di un elemento `input` elemento:


#### Struttura HTML

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**Esempio di struttura HTML**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### Esempio di selettori CSS per il componente a discesa

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* Eseguire il targeting del wrapper: il primo selettore (`.form-drop-down-wrapper`) esegue il targeting dell’elemento wrapper esterno, assicurando che gli stili vengano applicati all’intero componente del menu a discesa.
* Layout flexbox: Flexbox dispone l’etichetta, il menu a discesa e la descrizione in verticale per un layout pulito.
* Stile etichetta: l’etichetta si distingue per uno spessore del carattere più audace e un leggero margine.
* Stile a discesa: l&#39;elemento select riceve un bordo, una spaziatura interna e angoli arrotondati per un aspetto elegante.
* Colore di sfondo: viene impostato un colore di sfondo coerente per l’armonia visiva.
* Personalizzazione freccia: gli stili facoltativi nascondono la freccia a discesa predefinita e creano una freccia personalizzata utilizzando un carattere Unicode e il posizionamento.

### Gruppi di pulsanti di scelta e caselle di controllo

Analogamente ai componenti a discesa, i gruppi radio e di caselle di controllo hanno una propria struttura HTML e considerazioni CSS:

#### Struttura HTML gruppo pulsanti di scelta

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### Casella di selezione Struttura HTML

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

**Esempio di selettori CSS per gruppi di caselle di controllo e di radio**

* Targeting dell’involucro esterno: questi selettori eseguono il targeting dei contenitori più esterni dei gruppi di caselle di selezione e radio, consentendo di applicare stili generali all’intera struttura del gruppo. Questa opzione è utile per impostare la spaziatura, l&#39;allineamento o altre proprietà relative al layout.


  ```CSS
     /* Targets all radio group wrappers */
  .form-radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */
  }
  
  /* Targets all checkbox group wrappers */
  .form-checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
  ```


* Etichette gruppo di targeting: questo selettore esegue il targeting del `.field-label` all&#39;interno dei wrapper dei gruppi di caselle di controllo e di opzione. Questo consente di applicare uno stile alle etichette specifiche per questi gruppi, rendendoli potenzialmente più evidenti.

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* Targeting di singoli input ed etichette: questi selettori forniscono un controllo più granulare sui singoli pulsanti di scelta, caselle di controllo e le relative etichette associate. È possibile utilizzarli per modificare le dimensioni, la spaziatura o applicare stili visivi più distinti.

  ```CSS
  /* Styling radio buttons */
  .form-radio-group-wrapper input[type="radio"] {
    margin-right: 5px; /* Adds space between the input and its   label */
  } 
  
  /* Styling radio button labels */
  .form-radio-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  
  /* Styling checkboxes */
  .form-checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 5px;  /* Adds space between the input and its  label */ 
  }
  
  /* Styling checkbox labels */
  .form-checkbox-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  ```




* Personalizzazione dell&#39;aspetto dei pulsanti di scelta e delle caselle di controllo: questa tecnica nasconde l&#39;input predefinito e utilizza gli pseudo elementi :before e :after per creare visualizzazioni personalizzate che modificano l&#39;aspetto in base allo stato &quot;selezionato&quot;.

  ```CSS
  /* Hide the default radio button or checkbox */
  .form-radio-group-wrapper input[type="radio"],
  .form-checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0; 
    position: absolute; 
  }
  
  /* Create a custom radio button */
  .form-radio-group-wrapper input[type="radio"] + label::before { 
    content: "";
    display: inline-block;
    width: 16px; 
    height: 16px; 
    border: 2px solid #ccc; 
    border-radius: 50%;
    margin-right: 5px;
  }
  
  .form-radio-group-wrapper input[type="radio"]:checked +  label::before {
    background-color: #007bff; 
  }
  
  /* Create a custom checkbox */
  /* Similar styling as above, with adjustments for a square shape  */
  ```


## Componenti di stile

È inoltre possibile assegnare uno stile ai campi modulo in base al tipo specifico o ai singoli nomi. Ciò consente un controllo più granulare e la personalizzazione dell&#39;aspetto del modulo.

### Stile basato sul tipo di campo

Puoi utilizzare i selettori CSS per eseguire il targeting di tipi di campo specifici e applicare gli stili in modo coerente.

**Esempio di struttura HTML**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* Ogni campo è racchiuso in un `div` elemento con diverse classi:
   * `form-{Type}-wrapper`: identifica il tipo di campo. Ad esempio: `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `form-{Name}`: identifica il campo in base al nome. Ad esempio `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: classe generica per tutti i wrapper di campi.
* Il `data-required` attributo indica se il campo è obbligatorio o facoltativo.
* Ogni campo ha un’etichetta corrispondente, un elemento di input e potenziali elementi aggiuntivi come segnaposto e descrizioni.

**Esempio di selettori CSS**

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### Stile basato sul nome del campo

Per applicare stili univoci, puoi anche eseguire il targeting di singoli campi per nome.

**Esempio di struttura HTML**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**Esempio di selettore CSS**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

Questo CSS esegue il targeting di tutti gli elementi di input che si trovano all’interno di un elemento che ha la classe `form-otp`. La struttura HTML del modulo segue le convenzioni del blocco modulo, il che implica che esiste un contenitore contrassegnato con la classe &quot;form-otp&quot; che contiene il campo con il nome &quot;otp&quot;.


