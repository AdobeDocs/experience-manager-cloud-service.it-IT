---
title: Personalizzare tema e stile per un AEM Forms Edge Delivery Services Form
description: Personalizzare tema e stile per un AEM Forms Edge Delivery Services Form
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: c214711c-979b-4833-9541-8e35b2aa8e09
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 0%

---

# Applicazione di stili ai campi modulo

Forms è fondamentale per l’interazione degli utenti sui siti web, consentendo loro di inserire dati. Questa guida illustra i concetti fondamentali relativi allo stile di vari campi modulo all’interno di [Blocco Forms adattivo](/help/edge/docs/forms/create-forms.md), per creare moduli visivi accattivanti e facili da usare.

## Informazioni sui tipi di campi modulo

Prima di immergerci nello stile, esaminiamo i tipi di campi modulo comuni supportati dal blocco Forms adattivo:

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

## Applicazione di uno stile a un modulo per un blocco Forms adattivo

L’Adaptive Forms Block offre una struttura di HTML standardizzata che semplifica la selezione e lo stile dei componenti dei moduli:

* **Aggiorna stili predefiniti**: è possibile modificare gli stili predefiniti di un modulo modificando il `/blocks/form/form.css file`. Questo file offre uno stile completo per un modulo, con supporto per i moduli della procedura guidata in più passaggi. Viene enfatizzato l’utilizzo di variabili CSS personalizzate per una facile personalizzazione, manutenzione e uno stile uniforme tra i moduli. Per istruzioni sull’aggiunta del blocco Forms adattivo al progetto, consulta [creare un modulo](/help/edge/docs/forms/create-forms.md).

* **Personalizzazione**: utilizza il valore predefinito `forms.css` come base e personalizzarla per modificare l’aspetto dei componenti del modulo, rendendolo visivamente accattivante e di facile utilizzo. La struttura del file incoraggia l’organizzazione e mantiene gli stili per i moduli, promuovendo progettazioni coerenti all’interno del sito web.

## Raggruppamento della struttura di forms.css

* **Variabili globali:** Definito in corrispondenza di `:root` livello, queste variabili (`--variable-name`) memorizzare i valori utilizzati nel foglio di stile per garantire coerenza e facilità di aggiornamento. Queste variabili definiscono i colori, le dimensioni dei caratteri, la spaziatura interna e altre proprietà. Puoi dichiarare le tue variabili globali o modificare quelle esistenti per modificare lo stile del modulo.

* **Stili selettore universale:** Il `*` Il selettore corrisponde a ogni elemento del modulo, garantendo che gli stili vengano applicati a tutti i componenti per impostazione predefinita, inclusa l’impostazione di `box-sizing` proprietà a `border-box`.

* **Stile modulo:** Questa sezione descrive come formattare i componenti del modulo utilizzando i selettori per eseguire il targeting di elementi HTML specifici. Definisce gli stili per i campi di input, le aree di testo, le caselle di controllo, i pulsanti di scelta, gli input di file, le etichette dei moduli e le descrizioni.

* **Stile procedura guidata (se applicabile):** Questa sezione è dedicata allo stile del layout della procedura guidata, un modulo con più passaggi in cui ogni passaggio viene visualizzato uno alla volta. Definisce gli stili per il contenitore della procedura guidata, i set di campi, le legende, i pulsanti di navigazione e i layout reattivi.

* **Query multimediali:** che offrono stili per schermi di diverse dimensioni, con conseguente regolazione del layout e dello stile.

* **Stili vari:**: questa sezione descrive gli stili dei messaggi di errore o di successo, le aree di caricamento dei file e altri elementi che potrebbero verificarsi in un modulo.


## Struttura dei componenti

Il blocco Forms adattivo offre una struttura HTML coerente per vari elementi del modulo, garantendo così uno stile e una gestione più semplici. Puoi manipolare i componenti utilizzando i CSS a scopo di stile.

### Componenti generali (ad eccezione di elenchi a discesa, gruppi di scelta e gruppi di caselle di controllo):

Tutti i campi modulo, ad eccezione di elenchi a discesa, gruppi di scelta e gruppi di caselle di controllo, hanno la seguente struttura HTML:

#### Struttura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

* Classi: l’elemento div dispone di diverse classi per il targeting di elementi e stili specifici. È necessario `{Type}-wrapper` o `field-{Name}` classi per sviluppare un selettore CSS per assegnare uno stile a un campo modulo:
   * {Type}: identifica il componente per tipo di campo. Ad esempio, testo (ritorno a capo automatico), numero (ritorno a capo automatico), data (ritorno a capo automatico).
   * {Name}: identifica il componente in base al nome. Il nome del campo può contenere solo caratteri alfanumerici; i più trattini consecutivi nel nome vengono sostituiti da un singolo trattino `(-)`, e i trattini iniziale e finale nel nome di un campo vengono rimossi. Ad esempio, nome (field-first-name field-wrapper).
   * {FieldId}: è un identificatore univoco del campo, generato automaticamente.
   * {Required}: valore booleano che indica se il campo è obbligatorio.
* Label: il `label` fornisce un testo descrittivo per il campo e lo associa all&#39;elemento di input utilizzando `for` attributo.
* Input: Il `input` definisce il tipo di dati da immettere. Ad esempio, testo, numero, e-mail.
* Descrizione (Facoltativa): `div` con classe `field-description` fornisce informazioni o istruzioni aggiuntive per l’utente.

**Esempio di struttura HTML**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**Selettore CSS per componenti generali**

```CSS
/* Target all input fields within any .{Type}-wrapper  */
.{Type}-wrapper  {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all input fields within any .{Type}-wrapper  */
.{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target any element with the class field-{Name}  */
.field-{Name} {
  /* Add your styles here */
  /* This could be used for styles specific to all elements with field-{Name} class, not just inputs */
}
```

* `.{Type}-wrapper`: indirizza l’esterno `div` in base al tipo di campo. Ad esempio: `.text-wrapper` esegue il targeting di tutti i campi di testo.
* `.field-{Name}`: seleziona ulteriormente l’elemento in base al nome del campo specifico. Ad esempio: `.field-first-name` esegue il targeting del campo di testo &quot;Nome&quot;. Questo selettore può essere utilizzato per il targeting di elementi con il campo-{Name} classe, è importante essere cauti. In questo caso specifico, non sarebbe molto utile per la formattazione dei campi di input, perché avrebbe come target non solo l’input stesso, ma anche gli elementi etichetta e descrizione. In genere, si consiglia di utilizzare selettori più specifici, come quelli disponibili per il targeting dei campi di input di testo (input .text-wrapper).



**Esempio di selettori CSS per componenti generali**

```CSS
/*Target all text input fields */

text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### Componente a discesa

Per i menu a discesa, il `select` viene utilizzato al posto di un elemento `input` elemento:


#### Struttura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Esempio di struttura HTML**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

#### Esempio di selettori CSS per il componente a discesa

```CSS
/* Target the outer wrapper */
.drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.drop-down-wrapper select {
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
.drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.drop-down-wrapper select::after {
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

* Eseguire il targeting del wrapper: il primo selettore (`.drop-down-wrapper`) esegue il targeting dell’elemento wrapper esterno, assicurando che gli stili vengano applicati all’intero componente del menu a discesa.
* Layout flexbox: Flexbox dispone l’etichetta, il menu a discesa e la descrizione in verticale per un layout pulito.
* Stile etichetta: l’etichetta si distingue per uno spessore del carattere più audace e un leggero margine.
* Stile a discesa: l&#39;elemento select riceve un bordo, una spaziatura interna e angoli arrotondati per un aspetto elegante.
* Colore di sfondo: viene impostato un colore di sfondo coerente per l’armonia visiva.
* Personalizzazione freccia: gli stili facoltativi nascondono la freccia a discesa predefinita e creano una freccia personalizzata utilizzando un carattere Unicode e il posizionamento.

### Gruppi pulsanti di scelta

Analogamente ai componenti a discesa, i gruppi radio dispongono di una propria struttura HTML e CSS:

#### Struttura HTML gruppo pulsanti di scelta

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### Esempio di struttura HTML

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

#### Esempio di selettori CSS per il componente a discesa

* Targeting del set di campi

```CSS
  .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

Questo selettore esegue il targeting di qualsiasi set di campi con la classe radio-group-wrapper. Questo sarebbe utile per applicare stili generali all&#39;intero gruppo radio.

* Etichette dei pulsanti di scelta Targeting

```CSS
.radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

* Eseguire il targeting di tutte le etichette dei pulsanti di scelta in un set di campi specifico in base al nome

```CSS
.field-color .radio-wrapper label {
  /* Your styles here */
}
```

### Gruppi di caselle di controllo

#### Casella di selezione Struttura HTML

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### Esempio di struttura HTML

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

**Esempio di selettori CSS per gruppi di caselle di controllo e di radio**

* Targeting dell’involucro esterno: questi selettori eseguono il targeting dei contenitori più esterni dei gruppi di caselle di selezione e radio, consentendo di applicare stili generali all’intera struttura del gruppo. Questa opzione è utile per impostare la spaziatura, l&#39;allineamento o altre proprietà relative al layout.


  ```CSS
     /* Targets radio group wrappers */
       .radio-group-wrapper {
       margin-bottom: 20px; /* Adds space between radio groups */  
     }
  
     /* Targets checkbox group wrappers */
     .checkbox-group-wrapper {
     margin-bottom: 20px; /* Adds space between checkbox groups */
     }
  ```


* Etichette gruppo di targeting: questo selettore esegue il targeting del `.field-label` all&#39;interno dei wrapper dei gruppi di caselle di controllo e di opzione. Questo consente di applicare uno stile alle etichette specifiche per questi gruppi, rendendoli potenzialmente più evidenti.

  ```CSS
   .radio-group-wrapper legend,
   .checkbox-group-wrapper legend {
     font-weight: bold; /* Makes the group label bold */
   }
  ```



* Targeting di singoli input ed etichette: questi selettori forniscono un controllo più granulare sui singoli pulsanti di scelta, caselle di controllo e le relative etichette associate. È possibile utilizzarli per modificare le dimensioni, la spaziatura o applicare stili visivi più distinti.

  ```CSS
  /* Styling radio buttons */
   .radio-group-wrapper input[type="radio"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling radio button labels */
   .radio-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  
  /* Styling checkboxes */
   .checkbox-group-wrapper input[type="checkbox"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling checkbox labels */
   .checkbox-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  ```




* Personalizzazione dell&#39;aspetto dei pulsanti di scelta e delle caselle di controllo: questa tecnica nasconde l&#39;input predefinito e utilizza gli pseudo elementi :before e :after per creare visualizzazioni personalizzate che modificano l&#39;aspetto in base allo stato &quot;selezionato&quot;.

  ```CSS
  /* Hide the default radio button or checkbox */
     .radio-group-wrapper input[type="radio"],
     .checkbox-group-wrapper input[type="checkbox"] {
       opacity: 0;
       position: absolute;
     }
  
     /* Create a custom radio button */
     .radio-group-wrapper input[type="radio"] + label::before {
       /* ... styles for custom radio button ... */
     }
  
     .radio-group-wrapper input[type="radio"]:checked + label::before {
       /* ... styles for checked radio button ... */
     }
  
     /* Create a custom checkbox */
     /* Similar styling as above, with adjustments for a square shape  */
     .checkbox-group-wrapper input[type="checkbox"] + label::before {
       /* ... styles for custom checkbox ... */
     }
  
     .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
       /* ... styles for checked checkbox ... */
     }
  ```

### Componenti pannello/contenitore

#### Struttura HTML

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**Esempio di struttura HTML**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

* L’elemento set di campi funge da contenitore pannello con la classe panel-wrapper e classi aggiuntive per lo stile in base al nome del pannello (field-login).
* Elemento legenda (<legend>) funge da titolo del pannello con il testo &quot;Informazioni di accesso&quot; e l’etichetta del campo della classe. L’attributo data-visible=&quot;false&quot; può essere utilizzato con JavaScript per controllare la visibilità del titolo.
* All&#39;interno del set di campi, più .{Type}Gli elementi -wrapper (.text-wrapper e .password-wrapper in questo caso) rappresentano i singoli campi del modulo all’interno del pannello.
* Ogni wrapper contiene un&#39;etichetta, un campo di input e una descrizione, simili agli esempi precedenti.

#### Selettori ed esempi CSS

1. Targeting del pannello:

```CSS
  /* Target the entire panel container */
  .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

* Il `.panel-wrapper` il selettore assegna a tutti gli elementi uno stile basato sul wrapper del pannello classe, creando un aspetto coerente per tutti i pannelli.

1. Targeting del titolo del pannello:

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

* Il `.panel-wrapper legend` selettore applica uno stile all’elemento legenda all’interno del pannello, rendendo il titolo visibile.


1. Esecuzione del targeting di singoli campi nel pannello:

```CSS
/* Target all form field wrappers within a panel */
.panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

* Il `.panel-wrapper .{Type}-wrapper` il selettore esegue il targeting di tutti i wrapper con `.{Type}-wrapper` nel pannello, che consente di applicare uno stile alla spaziatura tra i campi del modulo.

1. Campi Specifici Di Targeting (Facoltativo):

```CSS
  /* Target the username field wrapper */
  .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

* Questi selettori facoltativi consentono di eseguire il targeting di wrapper di campi specifici all’interno del pannello per uno stile univoco, ad esempio per evidenziare il campo del nome utente.

### Pannello ripetibile

#### Struttura HTML

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**Esempio di struttura HTML**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

Ogni pannello ha la stessa struttura dell’esempio di pannello singolo, con attributi aggiuntivi:

* data-Repeable=&quot;true&quot;: questo attributo indica che il pannello può essere ripetuto dinamicamente utilizzando JavaScript o un framework.

* ID e nomi univoci: ogni elemento all’interno del pannello ha un ID univoco (ad esempio, nome-1, e-mail-1) e un attributo di nome in base all’indice del pannello (ad esempio, nome=&quot;contatti[0].name&quot;) Questo consente una corretta raccolta dei dati quando vengono inviati più pannelli.



#### Selettori ed esempi CSS

* Targeting di tutti i pannelli ripetibili:

```CSS
  /* Target all panels with the repeatable attribute */
  .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

Il selettore assegna uno stile a tutti i pannelli che possono essere ripetuti, assicurando un aspetto coerente.


* Targeting di singoli campi all’interno di un pannello:

```CSS
/* Target all form field wrappers within a repeatable panel */
.panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```
Questo selettore applica uno stile a tutti i wrapper di campo all’interno di un pannello ripetibile, mantenendo una spaziatura coerente tra i campi.

* Campi specifici di targeting (all’interno di un pannello):

```CSS
/* Target the name field wrapper within the first panel */
.panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

### Allegato file


```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**Esempio di struttura HTML**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

* L’attributo class utilizza il nome fornito per il file allegato (claim_form).
* Gli attributi ID e nome dell&#39;elemento di input corrispondono al nome dell&#39;allegato (claim_form).
* La sezione dell’elenco dei file è inizialmente vuota. Verrà compilato dinamicamente con JavaScript al caricamento dei file.


**Selettori ed esempi CSS:**

* Esecuzione del targeting dell&#39;intero componente File allegato:

```CSS
/* Target the entire file attachment component */
.file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Questo selettore imposta lo stile dell&#39;intero componente allegato, inclusi la legenda, l&#39;area di trascinamento, il campo di input e l&#39;elenco.

* Targeting di elementi specifici:

```CSS
/* Target the drag and drop area */
.file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
.file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
.file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
.file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}

/* Target the file size within the description */
.file-wrapper .files-list .file-description .file-description-size {
  /* Add your styles here (e.g., font-size) */
  font-size: 0.8em;
}

/* Target the remove button within the description */
.file-wrapper .files-list .file-description .file-description-remove {
  /* Add your styles here (e.g., background color, hover effect) */
  background-color: transparent;
  border: none;
  cursor: pointer;
}
```

Questi selettori consentono di applicare uno stile a varie parti del componente di file allegato. È possibile modificare gli stili in base alle preferenze di progettazione.


## Componenti di stile

È inoltre possibile assegnare uno stile ai campi modulo in base al tipo specifico o ai singoli nomi. Ciò consente un controllo più granulare e la personalizzazione dell&#39;aspetto del modulo.

### Stile basato sul tipo di campo

Puoi utilizzare i selettori CSS per eseguire il targeting di tipi di campo specifici e applicare gli stili in modo coerente.

**Esempio di struttura HTML**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* Ogni campo è racchiuso in un `div` elemento con diverse classi:
   * `{Type}-wrapper`: identifica il tipo di campo. Ad esempio: `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `field-{Name}`: identifica il campo in base al nome. Ad esempio `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: classe generica per tutti i wrapper di campi.
* Il `data-required` attributo indica se il campo è obbligatorio o facoltativo.
* Ogni campo ha un’etichetta corrispondente, un elemento di input e potenziali elementi aggiuntivi come segnaposto e descrizioni.

**Esempio di selettori CSS**

```CSS
/* Target all text input fields */
.text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### Stile basato sul nome del campo

Per applicare stili univoci, puoi anche eseguire il targeting di singoli campi per nome.

**Esempio di struttura HTML**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**Esempio di selettore CSS**

```CSS
.field-otp input {
   letter-spacing: 2px
}
```

Questo CSS esegue il targeting di tutti gli elementi di input che si trovano all’interno di un elemento che ha la classe `field-otp`. La struttura HTML del modulo segue le convenzioni del blocco Forms adattivo. Ciò implica che esiste un contenitore contrassegnato con la classe &quot;field-otp&quot; che contiene il campo con il nome &quot;otp&quot;.

