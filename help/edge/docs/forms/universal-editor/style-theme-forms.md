---
title: Personalizzare tema e stile per un modulo Edge Delivery Services di AEM Forms
description: Personalizza efficacemente il tema e lo stile per AEM Forms fornito tramite Edge Delivery Services, garantendo un’esperienza utente coerente e con il brand.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 97%

---

# Personalizzare l’aspetto dei moduli

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio dall&#39;indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Ad esempio, se l&#39;URL del repository è https://github.com/adobe/abc, il nome dell&#39;organizzazione è adobe e il nome del repository è abc.</span>


I moduli sono fondamentali per l’interazione degli utenti sui siti web, poiché consentono loro di inserire dati. È possibile utilizzare i fogli di stile CSS (Cascading Style Sheets) per applicare uno stile ai campi di un modulo, migliorandone la presentazione visiva e l’esperienza utente.

Il blocco moduli adattivi produce una struttura coerente per tutti i campi modulo. La struttura coerente semplifica lo sviluppo di selettori CSS per selezionare e assegnare uno stile ai campi modulo in base al tipo di campo e ai nomi dei campi.

Questo documento illustra la struttura HTML di vari componenti del modulo e spiega come creare selettori CSS per vari campi modulo per assegnare stili ai campi modulo di un blocco moduli adattivi.

Entro la fine dell’articolo:

* Riuscirai a comprendere la struttura del file CSS predefinito incluso in un blocco moduli adattivi.
* Puoi creare e comprendere la struttura HTML dei componenti modulo forniti dal Blocco moduli adattivi, inclusi i componenti generali e specifici come elenchi a discesa, gruppi di pulsanti di scelta e gruppi di caselle di controllo.
* Scopri come assegnare uno stile ai campi modulo in base al tipo di campo e ai nomi di campo utilizzando i selettori CSS, consentendo uno stile coerente o univoco in base ai requisiti.

## Informazioni sui tipi di campi modulo

Prima di approfondire lo stile, esaminiamo i [tipi di campo](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) di un modulo comune supportato dal blocco moduli adattivi:

* Campi di input: includono input di testo, input di e-mail, input di password e altro ancora.
* Gruppi di caselle di controllo: utilizzati per selezionare più opzioni.
* Gruppi di scelta: utilizzati per selezionare una sola opzione all’interno di un gruppo.
* Elenchi a discesa: noti anche come caselle di selezione, utilizzati per selezionare un’opzione da un elenco.
* Pannelli/contenitori: utilizzati per raggruppare gli elementi modulo correlati.

## Principi di base dello stile

La comprensione dei [concetti CSS fondamentali](https://www.w3schools.com/css/css_intro.asp) è indispensabile prima di applicare uno stile a campi modulo specifici:

* [Selettori](https://www.w3schools.com/css/css_selectors.as): i selettori CSS ti consentono di eseguire il targeting di elementi HTML specifici per l’applicazione di uno stile. Puoi utilizzare i selettori di elementi, di classi o di ID.
* [Proprietà](https://www.w3schools.com/css/css_syntax.asp): le proprietà CSS definiscono l’aspetto visivo degli elementi. Le proprietà comuni per lo stile dei campi modulo includono colore, colore di sfondo, bordo, riempimento, margine e altro ancora.
* [Modello casella](https://www.w3schools.com/css/css_boxmodel.asp): il modello casella CSS descrive la struttura degli elementi HTML come un’area di contenuto circondata da riempimenti, bordi e margini.
* Flexbox/Griglia: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) e [Layout griglia](https://www.w3schools.com/css/css_grid.asp) sono strumenti potenti per la creazione di progettazioni dinamiche e flessibili.


## Applicazione di uno stile a un modulo per un blocco di moduli adattivi

Il blocco di moduli adattivi offre una struttura HTML standardizzata che semplifica la selezione e lo stile dei componenti dei moduli:

* **Aggiorna stili predefiniti**: è possibile modificare gli stili predefiniti di un modulo modificando il `/blocks/form/form.css file`. Questo file offre uno stile completo per un modulo, con supporto per i moduli della procedura guidata in più passaggi. Evidenzia l’utilizzo di variabili CSS personalizzate per una facile personalizzazione, manutenzione e uno stile uniforme tra i moduli.

* **Stile CSS per i moduli**: per garantire la corretta applicazione degli stili, racchiudi il CSS specifico per il modulo nel selettore `main .form form`. In questo modo, gli stili verranno indirizzati solo agli elementi del modulo all’interno dell’area del contenuto principale, evitando conflitti con altre parti del sito web.
Esempio:

  ```css
    main .form form input {
        /* Add styles specific to input fields inside the form */
    }
  
    main .form form button {
        /* Add styles specific to buttons inside the form */
    }
  
    main .form form label {
        /* Add styles specific to labels inside the form */
    }
  
## Struttura dei componenti

Il Blocco moduli adattivi offre una struttura HTML coerente per vari elementi del modulo, garantendo così uno stile e una gestione più semplici. Puoi manipolare i componenti utilizzando i CSS a scopo di stile.

### Componenti generali (ad eccezione di elenchi a discesa, gruppi di pulsanti di scelta e gruppi di caselle di controllo):

Tutti i campi modulo, ad eccezione di elenchi a discesa, gruppi di pulsanti di scelta e gruppi di caselle di controllo, hanno la seguente struttura HTML:

+++ Struttura HTML dei componenti generali

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

* Classi: l’elemento div dispone di diverse classi per il targeting di elementi e stili specifici. È necessario che le classi `{Type}-wrapper` o `field-{Name}` sviluppino un selettore CSS per assegnare uno stile a un campo modulo:
* {Type}: identifica il componente per tipo di campo. Ad esempio, testo (ritorno a capo automatico), numero (ritorno a capo automatico), data (ritorno a capo automatico).
* {Name}: identifica il componente in base al nome. Il nome del campo può contenere solo caratteri alfanumerici; i trattini consecutivi multipli nel nome vengono sostituiti da un singolo trattino `(-)` e i trattini iniziali e finali nel nome di un campo vengono rimossi. Ad esempio, nome (field-first-name field-wrapper).
* {FieldId}: è un identificatore univoco per il campo, generato automaticamente.
* {Obbligatorio}: valore booleano che indica se il campo è obbligatorio.
* Etichetta: l’elemento `label` fornisce un testo descrittivo per il campo e lo associa all’elemento di input utilizzando l’attributo `for`.
* Input: l’elemento `input` definisce il tipo di dati da immettere. Ad esempio, testo, numero, e-mail.
* Descrizione (Facoltativa): il `div` con classe `field-description` fornisce informazioni o istruzioni aggiuntive per l’utente.

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

+++

+++ Selettore CSS per componenti generali

```CSS
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper  {
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  }
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper input {
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  }
  
  /* Target any element with the class field-{Name}  */
  main .form form .field-{Name} {
    /* Add your styles here */
    /* This could be used for styles specific to all elements with   field-{Name} class, not just inputs */
  }
  
```
* `.{Type}-wrapper`: esegue il targeting dell’elemento esterno `div` in base al tipo di campo. Ad esempio: `.text-wrapper` esegue il targeting di tutti i campi di testo.
* `.field-{Name}`: seleziona ulteriormente l’elemento in base al nome del campo specifico. Ad esempio: `.field-first-name` esegue il targeting del campo di testo “Nome”. Questo selettore può essere utilizzato per eseguire il targeting di elementi con la classe field-{Name}, ma è importante prestare attenzione. In questo caso specifico, non sarebbe utile per la formattazione dei campi di input perché avrebbe come target non solo l’input stesso, ma anche gli elementi etichetta e descrizione. Si consiglia di utilizzare selettori più specifici, come quelli disponibili per il targeting dei campi di input di testo (input .text-wrapper).

**Esempio di selettori CSS per componenti generali**

```CSS
/*Target all text input fields */
main .form form .text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  color: red;
}

/*Target all fields with name first-name*/
main .form form .field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### Componente a discesa

Per i menu a discesa, l’elemento `select` viene utilizzato al posto di un elemento `input`:

+++ Struttura HTML del componente a discesa

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
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

+++

+++ Selettori CSS per componente a discesa

Di seguito sono elencati alcuni esempi di selettori CSS per i componenti a discesa.

```CSS
/* Target the outer wrapper */
main .form form .drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
main .form form .drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}
```
* Eseguire il targeting del wrapper: il primo selettore (`.drop-down-wrapper`) esegue il targeting dell’elemento wrapper esterno, assicurando che gli stili vengano applicati all’intero componente del menu a discesa.
* Layout flexbox: flexbox dispone l’etichetta, il menu a discesa e la descrizione in verticale per un layout pulito.
* Stile etichetta: l’etichetta si distingue per uno spessore del carattere più audace e un leggero margine.
* Stile a discesa: L&#39;elemento `select` riceve un bordo, una spaziatura interna e angoli arrotondati per ottenere un aspetto ordinato.
* Colore di sfondo: viene impostato un colore di sfondo coerente per l’armonia visiva.
* Personalizzazione freccia: gli stili facoltativi nascondono la freccia a discesa predefinita e creano una freccia personalizzata utilizzando un carattere Unicode e il posizionamento.

+++

---

### Gruppi pulsanti di scelta

Analogamente ai componenti a discesa, i gruppi pulsanti di scelta dispongono di una propria struttura HTML e CSS:

+++ Struttura HTML del gruppo pulsanti di scelta

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

**Esempio di struttura HTML**

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

+++

+++ Selettori CSS per gruppi di pulsanti di scelta

* Targeting del set di campi

```CSS
  main .form form .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```
Questo selettore esegue il targeting di qualsiasi set di campi con la classe radio-group-wrapper. Questo sarebbe utile per applicare stili generali all’intero gruppo pulsanti di scelta.

* Targeting delle etichette del pulsante di scelta

```CSS
main .form form .radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

* Esegui il targeting di tutte le etichette del pulsante di scelta in un set di campi specifico in base al suo nome

```CSS
main .form form .field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++

### Gruppi di caselle di controllo

+++ Struttura HTML del gruppo di caselle di controllo

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

**Esempio di struttura HTML**

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

+++

+++ Selettori CSS per gruppi di caselle di controllo

* Targeting del wrapper esterno: questi selettori eseguono il targeting dei contenitori dei gruppi di pulsanti scelta e delle caselle di controllo, consentendo di applicare stili generali all’intera struttura del gruppo. Questo è utile per impostare la spaziatura, l’allineamento o altre proprietà relative al layout.

```CSS
  
  /* Targets radio group wrappers */
  main .form form .radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */  
  }

  /* Targets checkbox group wrappers */
  main .form form .checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
```

* Etichette del gruppo di targeting: questo selettore esegue il targeting dell’elemento `.field-label` all’interno dei wrapper dei gruppi pulsanti di scelta e delle caselle di controllo. Questo consente di applicare uno stile alle etichette specifiche per tali gruppi, rendendoli potenzialmente più evidenti.

```CSS
main .form form .radio-group-wrapper legend,
main .form form .checkbox-group-wrapper legend {
  font-weight: bold; /* Makes the group label bold */
}
```

* Targeting di singoli input ed etichette: questi selettori forniscono un controllo più dettagliato su singoli pulsanti di scelta, caselle di controllo e le relative etichette associate. Puoi utilizzarli per modificare le dimensioni, la spaziatura o applicare stili visivi più distinti.

```CSS
/* Styling radio buttons */
main .form form .radio-group-wrapper input[type="radio"] {
  margin-right: 5px; /* Adds space between the input and its label */
}

/* Styling radio button labels */
main .form form .radio-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}

/* Styling checkboxes */
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 5px; /* Adds space between the input and its label */
}

/* Styling checkbox labels */
main .form form .checkbox-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}
```

* Personalizzazione dell’aspetto dei pulsanti di scelta e delle caselle di controllo: questa tecnica nasconde l’input predefinito e utilizza pseudo-elementi `:before` e `:after` per creare elementi visivi personalizzati che cambiano aspetto in base allo stato “selezionato”.

```CSS
/* Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0;
  position: absolute;
}

/* Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before {
  /* ... styles for custom radio button ... */
}

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before {
  /* ... styles for checked radio button ... */
}

/* Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before {
  /* ... styles for custom checkbox ... */
}

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
  /* ... styles for checked checkbox ... */
}
```

+++

### Componenti pannello/contenitore

+++ Struttura HTML dei componenti pannello/contenitore

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

* L’elemento fieldset funge da contenitore del pannello con la classe panel-wrapper e classi aggiuntive per lo stile in base al nome del pannello (field-login).
* L’elemento legend (<legend>) funge da titolo del pannello con il testo “Informazioni di accesso” e la classe field-label. L’attributo data-visible=&quot;false&quot; può essere utilizzato con JavaScript per controllare la visibilità del titolo.
* All’interno del fieldset, più.elementi wrapper {Type} (.text-wrapper e .password-wrapper in questo caso) rappresentano singoli campi modulo all’interno del pannello.
* Ogni wrapper contiene un’etichetta, un campo di input e una descrizione, simili agli esempi precedenti.

+++

+++ Esempio di selettori CSS per i componenti pannello/contenitore

1. Targeting del pannello:

```CSS
  /* Target the entire panel container */
  main .form form .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

* il selettore `.panel-wrapper` assegna a tutti gli elementi uno stile basato sulla classe panel-wrapper, creando un aspetto coerente per tutti i pannelli.

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

* il selettore `.panel-wrapper legend` applica uno stile all’elemento legend all’interno del pannello, rendendo il titolo evidente.


1. Esecuzione del targeting di singoli campi all’interno del pannello:

```CSS
/* Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

* il selettore `.panel-wrapper .{Type}-wrapper` esegue il targeting di tutti i wrapper con la classe `.{Type}-wrapper` all’interno del pannello, che consente di applicare uno stile alla spaziatura tra i campi modulo.

1. Targeting di campi specifici (facoltativo):

```CSS
  /* Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

* questi selettori facoltativi consentono di eseguire il targeting di wrapper di campi specifici all’interno del pannello per uno stile univoco, ad esempio per evidenziare il campo del nome utente.

+++

### Pannello ripetibile

+++ Struttura HTML di un pannello ripetibile

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

* ID e nomi univoci: ogni elemento all’interno del pannello ha un ID univoco (ad esempio, nome-1, e-mail-1) e un attributo del nome basato sull’indice del pannello (ad esempio, nome=&quot;contacts[0].name&quot;). Questo consente una corretta raccolta dei dati quando vengono inviati più pannelli.

+++

+++ Selettori CSS per un pannello ripetibile

* Targeting di tutti i pannelli ripetibili:

```CSS
  /* Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

il selettore applica uno stile a tutti i pannelli che possono essere ripetuti, assicurando un aspetto coerente.


* Targeting di singoli campi all’interno di un pannello:

```CSS
/* Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```
questo selettore applica uno stile a tutti i wrapper del campo all’interno di un pannello ripetibile, mantenendo una spaziatura coerente tra i campi.

* Targeting di campi specifici (all’interno di un pannello):

```CSS
/* Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

+++

### Allegato file

+++ Struttura HTML per l’allegato file

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

* L’attributo della classe utilizza il nome fornito per l’allegato file (claim_form).
* Gli attributi ID e nome dell’elemento di input corrispondono al nome dell’allegato (claim_form).
* La sezione dell’elenco dei file è inizialmente vuota. Viene compilato dinamicamente con JavaScript quando i file vengono caricati.

+++

+++ Selettori CSS per il componente File allegato

* Esecuzione del targeting dell&#39;intero componente allegato file:

```CSS
/* Target the entire file attachment component */
main .form form .file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Questo selettore imposta lo stile dell’intero componente allegato file, inclusi la legenda, l’area di trascinamento, il campo di input e l’elenco.

* Targeting di elementi specifici:

```CSS
/* Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Questi selettori consentono di applicare uno stile a varie parti del componente di file allegato. È possibile modificare gli stili in base alle preferenze di progettazione.

+++


## Componenti di stile

È possibile assegnare uno stile ai campi modulo in base al tipo specifico (`{Type}-wrapper`) o nomi individuali (`field-{Name}`). Ciò consente un controllo più granulare e la personalizzazione dell’aspetto del modulo.

### Stile basato sul tipo di campo

Puoi utilizzare i selettori CSS per eseguire il targeting di tipi di campo specifici e applicare gli stili in modo coerente.

+++ Struttura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

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

* Ogni campo è racchiuso in un elemento `div` con diverse classi:
   * `{Type}-wrapper`: identifica il tipo di campo. Ad esempio, `form-text-wrapper`, `form-number-wrapper` e `form-email-wrapper`.
   * `field-{Name}`: identifica il campo in base al nome. Ad esempio, `form-name`, `form-age` e `form-email`.
   * `field-wrapper`: classe generica per tutti i wrapper di campi.
* L’attributo `data-required` indica se il campo è obbligatorio o facoltativo.
* Ogni campo ha un’etichetta corrispondente, un elemento di input e potenziali elementi aggiuntivi come segnaposto e descrizioni.


+++


+++ Esempio di selettori CSS

```CSS
/* Target all text input fields */
main .form form .text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
main .form form .number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

+++

### Stile basato sul nome del campo

Per applicare stili univoci, puoi anche eseguire il targeting di singoli campi per nome.

+++ Struttura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**Esempio di struttura HTML**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

+++

+++ Esempio di selettore CSS

```CSS
main .form form .field-otp input {
   letter-spacing: 2px
}
```

Questo CSS esegue il targeting di tutti gli elementi di input che si trovano all’interno di un elemento che ha la classe `field-otp`. La struttura HTML del modulo segue le convenzioni del Blocco moduli adattivi. Ciò implica che esiste un contenitore contrassegnato con la classe “field-otp” che contiene il campo con il nome “otp”.

+++




## Consulta anche

{{universal-editor-see-also}}
