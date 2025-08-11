---
title: Personalizzare tema e stile per un modulo Edge Delivery Services di AEM Forms
description: Personalizza efficacemente il tema e lo stile per AEM Forms fornito tramite Edge Delivery Services, garantendo un’esperienza utente coerente e con il brand.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 55%

---

# Personalizzare l’aspetto dei moduli

Lo stile dei moduli in Edge Delivery Services per AEM Forms richiede una conoscenza approfondita delle proprietà personalizzate CSS, dell’architettura basata su blocchi e delle strategie di targeting specifiche dei componenti. A differenza degli approcci tradizionali allo stile dei moduli, l’Adaptive Forms Block implementa un sistema di token di progettazione sistematico che consente di applicare temi coerenti, mantenendo al contempo i vantaggi di prestazioni e accessibilità di Edge Delivery Services.

L’architettura Adaptive Forms Block genera strutture HTML standardizzate su tutti i componenti del modulo, creando modelli prevedibili per il targeting e la personalizzazione CSS. Questa coerenza consente agli sviluppatori di implementare sistemi di stile completi che si adattano a implementazioni di moduli complessi, preservando al contempo le ottimizzazioni delle prestazioni basate su blocchi che rendono Edge Delivery Services eccezionalmente veloce.

Questa guida completa descrive le basi tecniche dello stile dei moduli all’interno dell’ecosistema Edge Delivery Services, inclusi i sistemi di proprietà personalizzati CSS, i modelli di struttura dei componenti HTML e le tecniche di stile avanzate. La documentazione fornisce sia conoscenze teoriche che indicazioni pratiche sull’implementazione per creare esperienze di modulo sofisticate e di marca.

## Cosa imparerai

**Proprietà personalizzate CSS**: comprende il sistema completo di variabili che controlla l&#39;aspetto del modulo, incluse le combinazioni di colori, le scale tipografiche, i sistemi di spaziatura e i parametri di layout. Scopri come escludere ed estendere queste proprietà per implementare i temi completi del brand.

**Informazioni sull&#39;architettura dei componenti**: acquisisci una conoscenza approfondita dei modelli di struttura HTML utilizzati da ciascun tipo di componente modulo, consentendo un targeting e una personalizzazione CSS precisi senza interrompere le funzionalità sottostanti o le funzioni di accessibilità.

**Tecniche di stile avanzate**: implementa modelli di stile sofisticati, tra cui stili basati sullo stato, integrazione di progettazione reattiva e strategie di personalizzazione ottimizzate per le prestazioni, che mantengono le caratteristiche di caricamento rapido di Edge Delivery Services.

**Strategie di implementazione professionali**: scopri gli approcci standard del settore allo stile dei moduli, inclusa l&#39;integrazione del sistema di progettazione, l&#39;architettura CSS manutenibile e le tecniche di risoluzione dei problemi per scenari di stile complessi.

## Informazioni sui tipi di campi modulo

Prima di approfondire lo stile, esaminiamo i [tipi di campo](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) di un modulo comune supportato dal blocco moduli adattivi:

- Campi di input: includono input di testo, input di e-mail, input di password e altro ancora.
- Gruppi di caselle di controllo: utilizzati per selezionare più opzioni.
- Gruppi di scelta: utilizzati per selezionare una sola opzione all’interno di un gruppo.
- Elenchi a discesa: noti anche come caselle di selezione, utilizzati per selezionare un’opzione da un elenco.
- Pannelli/contenitori: utilizzati per raggruppare gli elementi modulo correlati.

## Principi di base dello stile

La comprensione dei [concetti CSS fondamentali](https://www.w3schools.com/css/css_intro.asp) è indispensabile prima di applicare uno stile a campi modulo specifici:

- [Selettori](https://www.w3schools.com/css/css_selectors.as): i selettori CSS ti consentono di eseguire il targeting di elementi HTML specifici per l’applicazione di uno stile. Puoi utilizzare i selettori di elementi, di classi o di ID.
- [Proprietà](https://www.w3schools.com/css/css_syntax.asp): le proprietà CSS definiscono l’aspetto visivo degli elementi. Le proprietà comuni per lo stile dei campi modulo includono colore, colore di sfondo, bordo, riempimento, margine e altro ancora.
- [Modello casella](https://www.w3schools.com/css/css_boxmodel.asp): il modello casella CSS descrive la struttura degli elementi HTML come un’area di contenuto circondata da riempimenti, bordi e margini.
- Flexbox/Griglia: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) e [Layout griglia](https://www.w3schools.com/css/css_grid.asp) sono strumenti potenti per la creazione di progettazioni dinamiche e flessibili.




## Stile modulo completo con proprietà personalizzate CSS

Il blocco Forms adattivo utilizza una sofisticata architettura CSS basata su proprietà personalizzate (variabili CSS) che consente di applicare temi sistematici e uno stile coerente a tutti i componenti del modulo. Comprendere questa struttura è essenziale per una personalizzazione e un branding efficaci dei moduli.

### Informazioni sull’architettura di forms.css

Gli stili di modulo predefiniti si trovano nell&#39;archivio dei progetti in `/blocks/form/form.css` e seguono un approccio strutturato che dà priorità a manutenibilità, coerenza e flessibilità di personalizzazione. L’architettura è costituita da diversi componenti chiave:

**Proprietà personalizzate CSS Foundation**: il sistema di stile è basato sulle proprietà personalizzate CSS definite al livello `:root`, fornendo un sistema di temi centralizzato che esegue la cascata in tutti i componenti del modulo. Queste variabili stabiliscono i token di progettazione per i colori, la composizione tipografica, la spaziatura e le proprietà di layout.

**Struttura CSS basata su blocchi**: Edge Delivery Services utilizza un&#39;architettura basata su blocchi in cui la classe `.form` funge da spazio dei nomi primario per tutti gli stili correlati ai moduli, garantendo il corretto isolamento dell&#39;ambito ed evitando conflitti CSS con altri componenti di pagina.

**Stile specifico del componente**: i singoli componenti del modulo sono formattati con modelli di wrapper coerenti (`.{Type}-wrapper`) che forniscono un targeting prevedibile per tipi di campo diversi mantenendo al contempo l&#39;integrità complessiva del sistema di progettazione.

### Riferimento e personalizzazione delle proprietà personalizzate CSS

Il sistema di stile dei moduli include oltre 50 proprietà personalizzate CSS che controllano ogni aspetto dell’aspetto e del comportamento dei moduli. Comprendere queste proprietà consente una personalizzazione completa mantenendo al contempo la coerenza della progettazione.

+++ Variabili di colore e temi

Il sistema di colori stabilisce una base visiva completa per i moduli attraverso proprietà personalizzate attentamente organizzate:

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**Esempio pratico di personalizzazione**: per implementare un tema scuro per i moduli, sostituire le variabili dei colori di base:

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

Questa singola modifica si propaga attraverso tutti i componenti del modulo poiché il sistema utilizza riferimenti variabili anziché valori hardcoded.

+++

+++ Tipografia e spaziatura variabili

Le variabili di composizione tipografica e spaziatura forniscono un controllo completo sulla presentazione del testo e sulla spaziatura del layout:

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**Esempio pratico di personalizzazione**: per creare un layout di modulo più compatto con caratteri tipografici più piccoli:

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ Variabili di layout e struttura

Le variabili di layout controllano le dimensioni del modulo, il comportamento della griglia e la disposizione dei componenti:

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**Esempio pratico di personalizzazione**: per creare un modulo in stile scheda con profondità visiva migliorata:

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### Modelli di stile CSS e best practice

Il blocco Forms adattivo segue pattern CSS specifici che garantiscono uno stile manutenibile, performante e coerente per tutti i componenti.

+++ Modelli di stile principali

**Contenitore modulo a livello di blocco**: esegui il targeting del contenitore del modulo principale per il layout generale e lo stile di sfondo:

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**Modelli wrapper componenti**: utilizzare classi wrapper coerenti per tipi di campi specifici di destinazione:

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ Modelli di personalizzazione avanzati

**Targeting specifico per campo**: esegui il targeting di singoli campi per nome per requisiti di stile univoci:

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**Stile basato sullo stato**: implementare gli stati di convalida e interazione:

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## Struttura dei componenti

Il Blocco moduli adattivi offre una struttura HTML coerente per vari elementi del modulo, garantendo così uno stile e una gestione più semplici. Puoi manipolare i componenti utilizzando i CSS a scopo di stile.

+++ Componenti generali (ad eccezione di elenchi a discesa, gruppi di pulsanti di scelta e gruppi di caselle di controllo):

Tutti i campi modulo, ad eccezione di elenchi a discesa, gruppi di pulsanti di scelta e gruppi di caselle di controllo, hanno la seguente struttura HTML:

#### Struttura HTML dei componenti generali

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- Classi: l’elemento div dispone di diverse classi per il targeting di elementi e stili specifici. È necessario che le classi `{Type}-wrapper` o `field-{Name}` sviluppino un selettore CSS per assegnare uno stile a un campo modulo:
- {Type}: identifica il componente per tipo di campo. Ad esempio, testo (ritorno a capo automatico), numero (ritorno a capo automatico), data (ritorno a capo automatico).
- {Name}: identifica il componente per nome. Il nome del campo può contenere solo caratteri alfanumerici; i trattini consecutivi multipli nel nome vengono sostituiti da un singolo trattino `(-)` e i trattini iniziali e finali nel nome di un campo vengono rimossi. Ad esempio, nome (field-first-name field-wrapper).
- {FieldId}: è un identificatore univoco per il campo, generato automaticamente.
- {Required}: valore booleano che indica se il campo è obbligatorio.
- Etichetta: l’elemento `label` fornisce un testo descrittivo per il campo e lo associa all’elemento di input utilizzando l’attributo `for`.
- Input: l’elemento `input` definisce il tipo di dati da immettere. Ad esempio, testo, numero, e-mail.
- Descrizione (Facoltativa): il `div` con classe `field-description` fornisce informazioni o istruzioni aggiuntive per l’utente.

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

#### Selettore CSS per componenti generali

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`: esegue il targeting dell&#39;elemento wrapper del campo in base al tipo di campo. Ad esempio, `.form .text-wrapper` esegue il targeting di tutti i contenitori di campi di testo.
- `.form .{Type}-wrapper input`: esegue il targeting degli elementi di input effettivi nel wrapper. Questo è il pattern consigliato per la formattazione degli input dei moduli.
- `.form .field-{Name}`: esegue il targeting degli elementi in base al nome di campo specifico. Ad esempio, `.form .field-first-name` esegue il targeting del contenitore di campi &quot;First Name&quot;. Utilizza `.form .field-{Name} input` per eseguire il targeting specifico dell&#39;elemento di input.
- **Evita**: `main .form form .{Type}-wrapper` - Questo crea una specificità CSS non necessaria ed è più difficile da mantenere.

**Esempio di selettori CSS per componenti generali**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ Componente a discesa

Per i menu a discesa, l’elemento `select` viene utilizzato al posto di un elemento `input`:

#### Struttura HTML del componente a discesa

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

#### Selettori CSS per componente a discesa

Di seguito sono elencati alcuni esempi di selettori CSS per i componenti a discesa.

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- Eseguire il targeting del wrapper: il primo selettore (`.drop-down-wrapper`) esegue il targeting dell’elemento wrapper esterno, assicurando che gli stili vengano applicati all’intero componente del menu a discesa.
- Layout flexbox: flexbox dispone l’etichetta, il menu a discesa e la descrizione in verticale per un layout pulito.
- Stile etichetta: l’etichetta si distingue per uno spessore del carattere più audace e un leggero margine.
- Stile a discesa: L&#39;elemento `select` riceve un bordo, una spaziatura interna e angoli arrotondati per ottenere un aspetto ordinato.
- Colore di sfondo: viene impostato un colore di sfondo coerente per l’armonia visiva.
- Personalizzazione freccia: gli stili facoltativi nascondono la freccia a discesa predefinita e creano una freccia personalizzata utilizzando un carattere Unicode e il posizionamento.

+++

+++ Gruppi pulsanti di scelta

Analogamente ai componenti a discesa, i gruppi pulsanti di scelta dispongono di una propria struttura HTML e CSS:

#### Struttura HTML del gruppo pulsanti di scelta

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

#### Selettori CSS per gruppi di pulsanti di scelta

- Targeting del set di campi

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

Questo selettore esegue il targeting di qualsiasi set di campi con la classe radio-group-wrapper. Questo sarebbe utile per applicare stili generali all’intero gruppo pulsanti di scelta.

- Targeting delle etichette del pulsante di scelta

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- Esegui il targeting di tutte le etichette del pulsante di scelta in un set di campi specifico in base al suo nome

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ Gruppi di caselle di controllo

#### Struttura HTML del gruppo di caselle di controllo

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
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

#### Selettori CSS per gruppi di caselle di controllo

- Targeting del wrapper esterno: questi selettori eseguono il targeting dei contenitori dei gruppi di pulsanti scelta e delle caselle di controllo, consentendo di applicare stili generali all’intera struttura del gruppo. Questo è utile per impostare la spaziatura, l’allineamento o altre proprietà relative al layout.

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- Etichette del gruppo di targeting: questo selettore esegue il targeting dell’elemento `.field-label` all’interno dei wrapper dei gruppi pulsanti di scelta e delle caselle di controllo. Questo consente di applicare uno stile alle etichette specifiche per tali gruppi, rendendoli potenzialmente più evidenti.

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- Targeting di singoli input ed etichette: questi selettori forniscono un controllo più dettagliato su singoli pulsanti di scelta, caselle di controllo e le relative etichette associate. Puoi utilizzarli per modificare le dimensioni, la spaziatura o applicare stili visivi più distinti.

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- Personalizzazione dell’aspetto dei pulsanti di scelta e delle caselle di controllo: questa tecnica nasconde l’input predefinito e utilizza pseudo-elementi `:before` e `:after` per creare elementi visivi personalizzati che cambiano aspetto in base allo stato “selezionato”.

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ Componenti pannello/contenitore

#### Struttura HTML dei componenti pannello/contenitore

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

- L’elemento fieldset funge da contenitore del pannello con la classe panel-wrapper e classi aggiuntive per lo stile in base al nome del pannello (field-login).
- L&#39;elemento legenda (`<legend>`) funge da titolo del pannello con il testo &quot;Informazioni di accesso&quot; e l&#39;etichetta del campo della classe. L’attributo data-visible=&quot;false&quot; può essere utilizzato con JavaScript per controllare la visibilità del titolo.
- All’interno del fieldset, più.{Type}-elementi wrapper (.text-wrapper e .password-wrapper in questo caso) rappresentano singoli campi modulo all’interno del pannello.
- Ogni wrapper contiene un’etichetta, un campo di input e una descrizione, simili agli esempi precedenti.


#### Esempio di selettori CSS per i componenti pannello/contenitore

1. Targeting del pannello:

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- il selettore `.panel-wrapper` assegna a tutti gli elementi uno stile basato sulla classe panel-wrapper, creando un aspetto coerente per tutti i pannelli.

1. Targeting del titolo del pannello:

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- il selettore `.panel-wrapper legend` applica uno stile all’elemento legend all’interno del pannello, rendendo il titolo evidente.


1. Esecuzione del targeting di singoli campi all’interno del pannello:

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- il selettore `.panel-wrapper .{Type}-wrapper` esegue il targeting di tutti i wrapper con la classe `.{Type}-wrapper` all’interno del pannello, che consente di applicare uno stile alla spaziatura tra i campi modulo.

1. Targeting di campi specifici (facoltativo):

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- questi selettori facoltativi consentono di eseguire il targeting di wrapper di campi specifici all’interno del pannello per uno stile univoco, ad esempio per evidenziare il campo del nome utente.


+++

+++ Pannello ripetibile

#### Struttura HTML di un pannello ripetibile

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

- data-Repeable=&quot;true&quot;: questo attributo indica che il pannello può essere ripetuto dinamicamente utilizzando JavaScript o un framework.

- ID e nomi univoci: ogni elemento all’interno del pannello ha un ID univoco (ad esempio, nome-1, e-mail-1) e un attributo del nome basato sull’indice del pannello (ad esempio, nome=&quot;contacts[0].name&quot;). Questo consente una corretta raccolta dei dati quando vengono inviati più pannelli.


#### Selettori CSS per un pannello ripetibile

- Targeting di tutti i pannelli ripetibili:

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

il selettore applica uno stile a tutti i pannelli che possono essere ripetuti, assicurando un aspetto coerente.


- Targeting di singoli campi all’interno di un pannello:

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

questo selettore applica uno stile a tutti i wrapper del campo all’interno di un pannello ripetibile, mantenendo una spaziatura coerente tra i campi.

- Targeting di campi specifici (all’interno di un pannello):

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ Allegato file

#### Struttura HTML per l’allegato file

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

- L’attributo della classe utilizza il nome fornito per l’allegato file (claim_form).
- Gli attributi ID e nome dell’elemento di input corrispondono al nome dell’allegato (claim_form).
- La sezione dell’elenco dei file è inizialmente vuota. Viene compilato dinamicamente con JavaScript quando i file vengono caricati.


#### Selettori CSS per il componente File allegato

- Esecuzione del targeting dell&#39;intero componente allegato file:

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Questo selettore imposta lo stile dell’intero componente allegato file, inclusi la legenda, l’area di trascinamento, il campo di input e l’elenco.

- Targeting di elementi specifici:

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Questi selettori consentono di applicare uno stile a varie parti del componente di file allegato. È possibile modificare gli stili in base alle preferenze di progettazione.

+++



## Componenti di stile

È possibile assegnare uno stile ai campi modulo in base al tipo specifico (`{Type}-wrapper`) o nomi individuali (`field-{Name}`). Ciò consente un controllo più granulare e la personalizzazione dell’aspetto del modulo.

+++ Stile basato sul tipo di campo

Puoi utilizzare i selettori CSS per eseguire il targeting di tipi di campo specifici e applicare gli stili in modo coerente.

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

- Ogni campo è racchiuso in un elemento `div` con diverse classi:
   - `{Type}-wrapper`: identifica il tipo di campo. Ad esempio, `form-text-wrapper`, `form-number-wrapper` e `form-email-wrapper`.
   - `field-{Name}`: identifica il campo in base al nome. Ad esempio, `form-name`, `form-age` e `form-email`.
   - `field-wrapper`: classe generica per tutti i wrapper di campi.
- L’attributo `data-required` indica se il campo è obbligatorio o facoltativo.
- Ogni campo ha un’etichetta corrispondente, un elemento di input e potenziali elementi aggiuntivi come segnaposto e descrizioni.




#### Esempio di selettori CSS

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

+++ Stile basato sul nome del campo

Per applicare stili univoci, puoi anche eseguire il targeting di singoli campi per nome.

#### Struttura HTML

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


#### Esempio di selettore CSS

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

Questo CSS esegue il targeting di tutti gli elementi di input che si trovano all’interno di un elemento che ha la classe `field-otp`. La struttura del modulo di Edge Delivery Services segue le convenzioni di blocco di Forms adattivo, in cui i contenitori sono contrassegnati con classi specifiche dei campi come &quot;field-otp&quot; per i campi con il nome &quot;otp&quot;.


## Struttura e implementazione dei file CSS

### **Implementazione di riferimento**

Il riferimento completo allo stile del modulo è disponibile nell’archivio AEM Forms Boilerplate:

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

Questo file funge da implementazione canonica del sistema di proprietà personalizzate CSS e fornisce le basi per tutti gli stili dei moduli. Include definizioni complete per tutte le variabili CSS, i pattern di stile dei componenti e le implementazioni di progettazione reattiva.

+++

+++ Integrazione dei progetti

Nel progetto Edge Delivery Services, implementa lo stile del modulo tramite questo approccio strutturato:

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ Strategia di implementazione

**Sovrascritture proprietà personalizzate CSS**: sovrascrivi le variabili modulo negli stili globali per implementare i temi specifici del brand:

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**Personalizzazioni specifiche per i componenti**:
Aggiungi uno stile specifico per il componente mantenendo il sistema di variabili CSS:

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**Integrazione di progettazione reattiva**: utilizza le proprietà personalizzate CSS all&#39;interno delle query multimediali per un comportamento reattivo coerente:

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### Completa l’implementazione dello stile

In questa sezione viene illustrato come creare un modulo moderno con marchio utilizzando le proprietà personalizzate CSS. L’implementazione è suddivisa in sottosezioni chiare per facilitarne la comprensione e la navigazione.



+++ &#x200B;1. Variabili del tema del marchio

Definisci la palette di colori, la spaziatura e la tipografia del tuo marchio utilizzando le proprietà personalizzate CSS.

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ &#x200B;2. Stile contenitore modulo

Applica uno sfondo moderno, un raggio del bordo e un&#39;ombreggiatura al contenitore del modulo per un layout visivamente accattivante.


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ &#x200B;3. Stile campo di input

I campi di input per testo, e-mail e numeri di stile conferiscono un aspetto moderno e pulito.


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ &#x200B;4. Personalizzazione aggiuntiva

Puoi estendere ulteriormente lo stile del modulo eseguendo il targeting di campi, stati o componenti specifici, in base alle esigenze. Per i motivi avanzati, fare riferimento alle sezioni precedenti.

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

Questo approccio completo dimostra come le proprietà personalizzate CSS consentano temi sofisticati mantenendo le funzioni di integrità strutturale e accessibilità del sistema di blocchi Forms adattivi.

+++

## Risoluzione dei problemi CSS

+++ Problemi di specificità CSS

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ Problemi di sostituzione della variabile CSS

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ Stile stato modulo

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ Errori selettori comuni

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **Best practice specifiche per i componenti**


+++ Stile pulsanti

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ Progettazione modulo reattivo

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## Riepilogo delle best practice

1. **Usa proprietà personalizzate CSS**: sfrutta le variabili per temi coerenti
2. **Segui architettura basata su blocchi**: utilizza `.form` come selettore di blocchi principale
3. **Evita di specificare eccessivamente**: non utilizzare `main .form form` se non necessario
4. **Wrapper di destinazione**: utilizza `.{Type}-wrapper` modelli per il targeting dei componenti
5. **Mantieni coerenza**: utilizza gli stessi modelli di selettore in tutto il progetto
6. **Test tra dispositivi**: garantire il corretto funzionamento dei moduli su dispositivi mobili, tablet e desktop
7. **Convalida accessibilità**: assicurati che gli stili non interferiscano con le utilità per la lettura dello schermo o la navigazione da tastiera


