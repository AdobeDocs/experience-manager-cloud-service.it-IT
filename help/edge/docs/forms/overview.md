---
title: Panoramica di Edge Delivery Services per AEM Forms
description: Edge Delivery Services per AEM Forms è stato progettato per offrire prestazioni di picco, consentendoti di immaginare il futuro di una raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 8%

---


# Guida introduttiva di Forms su AEM Edge Delivery Services

<span class="preview">Si tratta di una funzione pre-release accessibile tramite il [canale pre-release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features). </span>

Questa guida ti aiuta a comprendere e implementare i moduli utilizzando Adobe Experience Manager (AEM) Edge Delivery Services (EDS). Questa pagina illustra le opzioni per la creazione di un semplice modulo per i contatti o di uno strumento complesso per la raccolta dati.

## Informazioni su Forms in Edge Delivery Services

Edge Delivery Services è la soluzione moderna di Adobe per la distribuzione di contenuti web, inclusi moduli, con prestazioni e agilità eccezionali. Utilizzando Edge Delivery Services per i moduli, è possibile:

* **Distribuisci esperienze più veloci:** Forms viene caricato in modo incredibilmente rapido perché viene servito da una rete globale di server perimetrali (CDN) vicina ai tuoi utenti. Ciò migliora la soddisfazione degli utenti e può aumentare i tassi di completamento dei moduli.
* **Aggiornare Forms più facilmente:** L&#39;approccio Edge Delivery Services spesso consente cicli di sviluppo più rapidi e aggiornamenti dei contenuti, in modo da poter adattare rapidamente i moduli.
* **Genera Forms moderno e reattivo:** Crea moduli che hanno un aspetto ottimale e funzionano senza problemi su qualsiasi dispositivo.
* **Vantaggi della scalabilità e dell&#39;affidabilità:** I moduli saranno solidi e scalabili come l&#39;infrastruttura Edge sottostante.

Questa guida:

* Spiega i diversi modi in cui puoi creare (creare) moduli per i siti Edge Delivery.
* Mostra come configurare ciò che accade dopo l’invio di un modulo da parte di un utente (azioni di invio).
* Consente di scegliere i metodi migliori in base alle esigenze specifiche e alle abilità del team.
* Fornisci diagrammi architettonici e best practice.

## Termini chiave da conoscere

* **Edge Delivery Services (EDS):** architettura Adobe basata sulle prestazioni per la distribuzione di contenuti AEM tramite CDN. Anche conosciuto come Progetto Franklin.
* **AEM Forms:** soluzione Adobe per la creazione, la gestione e l&#39;elaborazione di moduli.
* **Editor universale (UE):** Un editor visivo WYSIWYG per contenuti AEM, inclusi i moduli.
* **Authoring basato su documenti:** Creazione di moduli tramite Microsoft Word o Google Docs/Sheets.
* **Document Authoring (DA):** servizio ospitato da Adobe per l&#39;authoring di contenuti (incluse pagine che possono ospitare moduli) per Edge Delivery Services.
* **Servizio di invio Forms (FSS):** servizio Adobe che semplifica l&#39;invio dei dati del modulo a fogli di calcolo o posta elettronica.
* **Istanza di pubblicazione AEM:** l&#39;ambiente AEM live che può elaborare gli invii di moduli complessi.
* **CORS (Cross-Origin Resource Sharing):** funzionalità di sicurezza del browser che richiede la configurazione per l&#39;incorporamento di moduli di domini diversi.
* **CDN (Content Delivery Network):** una rete di server che fornisce rapidamente contenuti Web agli utenti in base alla loro posizione geografica.


**Diagramma concettuale dell&#39;interazione di Edge Delivery Services Form**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Intercazione modulo](/help/forms/assets/eds-form-interaction.png)
Questo diagramma mostra un utente che interagisce con un modulo distribuito rapidamente tramite una rete CDN. I dati inviati vengono quindi gestiti da un sistema back-end.

## Come funziona Forms su Edge?

Con EDS, il contenuto del sito Web (inclusa la struttura dei moduli) può provenire da varie origini come AEM as a Cloud Service, SharePoint, Google Drive o il servizio di authoring dei documenti (DA). Questo contenuto viene quindi pubblicato in una rete CDN globale. Quando un utente visita il sito, il contenuto viene distribuito direttamente dal server Edge CDN più vicino, garantendo la massima velocità.

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**Architettura Edge Delivery Services semplificata con Forms**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Architettura](/help/forms/assets/eds-simplified-architecture.png)
Questo diagramma mostra il percorso: i moduli vengono definiti in un sistema di authoring, pubblicati in Edge, forniti agli utenti e i dati inviati vengono elaborati da un back-end.

## Scelta del metodo di creazione del modulo

Sono disponibili tre modi principali per creare moduli per i siti Edge Delivery Services. La scelta dipenderà dalle competenze del team, dalla complessità del modulo e dalle esigenze del progetto.

### Quale approccio di authoring è adatto alle tue esigenze?

Utilizza questa struttura decisionale per aiutarti a scegliere:

**Struttura delle decisioni per l&#39;authoring dei moduli**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![Selezione della piattaforma corretta](/help/forms/assets/eds-authoring-selection.png)

Questa struttura decisionale consente di selezionare un metodo di authoring in base alle esigenze del team e del modulo.

### Creazione di Forms con documenti (Word/Google Docs)

Questo metodo è ideale per [creare moduli in modo rapido se il team ha familiarità con Microsoft Word o Google Docs/Sheets](/help/edge/docs/forms/create-forms.md).

**Funzionamento: da documento a modulo Web**

È possibile definire i campi, le etichette e i tipi del modulo direttamente in un documento di Word o in un foglio di Google utilizzando un formato di tabella speciale o un &quot;blocco modulo&quot;. Quando si pubblica il documento, Edge Delivery Services lo converte automaticamente in un modulo HTML pronto per il Web con cui gli utenti possono interagire sul sito.

**Funzionalità e caratteristiche**

* Creazione in strumenti familiari: Word, Google Docs, Google Sheets.
* Definisci i campi: input di testo, e-mail, elenchi a discesa, caselle di controllo, pulsanti di scelta, aree di testo.
* Aggiungi etichette, segnaposto e messaggi di aiuto.
* Imposta regole di convalida di base: campi obbligatori, formato e-mail.
* Integra reCAPTCHA per la protezione da posta indesiderata.
* Consenti caricamenti di file.
* Pubblicazione immediata: le modifiche apportate al documento si riflettono rapidamente sul sito live.
* Estendi con codice personalizzato: gli utenti avanzati possono aggiungere componenti di moduli personalizzati e stili tramite GitHub.

**Considerazioni**

* Il tuo team utilizza regolarmente Word o Google Docs/Sheets per i contenuti.
* È necessario creare rapidamente moduli semplici o moderatamente complessi.
* Desideri inviare i dati del modulo direttamente a un foglio di calcolo o a un indirizzo e-mail con una configurazione minima.

**Funzionamento Degli Invii (Principalmente Forms Submission Service)**

Forms ha creato in questo modo in genere [invia i dati al servizio di invio AEM Forms](/help/forms/forms-submission-service.md). Questa configurazione, spesso presente nel documento di origine stesso, consente di inviare dati a un foglio di Google, a un file Excel in OneDrive/SharePoint o come messaggio di posta elettronica.

**Concetto di authoring basato su documenti**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![Basato su documento](/help/forms/assets/eds-doc-based.png)
In questo diagramma viene illustrato come un modulo definito in un documento diventa un modulo web live.

### Forms visivamente con Universal Editor

L&#39;[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) offre un&#39;interfaccia moderna per la creazione di moduli direttamente nel browser Web.

**Funzionamento: generazione di moduli mediante trascinamento**

Un’interfaccia visiva consente di trascinare i componenti del modulo (come campi di input, pulsanti, elenchi a discesa) sulla pagina. Puoi quindi configurare le proprietà di ciascun componente (etichette, convalida, ecc.) tramite un pannello delle proprietà. Nell&#39;Editor universale viene visualizzata un&#39;anteprima in tempo reale del modulo.

**Funzionalità e caratteristiche**

* Creazione di moduli visivi con una libreria di componenti predefiniti.
* Configura la convalida in tempo reale e la logica di business (ad esempio, mostra/nascondi campi in base alle selezioni).
* Guarda le anteprime live per diversi dispositivi (desktop, mobili).
* Integrazione con funzioni di AEM come Frammenti di contenuto, Flussi di lavoro di AEM e autorizzazioni per gli utenti.
* Utilizza &quot;Experience Builder&quot; per ottenere assistenza IA per la creazione o la modifica di moduli tramite prompt.

**Considerazioni**

* È necessario creare moduli complessi con logica condizionale, pannelli con più passaggi o personalizzazione.
* Il tuo team (ad esempio, esperti di marketing, utenti aziendali) preferisce gli strumenti visivi.
* È necessaria una forte integrazione con AEM as a Cloud Service per la governance, i flussi di lavoro o l’utilizzo di risorse AEM nei moduli.

**Funzionamento degli invii (servizio di invio Forms o pubblicazione AEM)**

Forms creato con Universal Editor può:

* Utilizza il semplice [Servizio di invio Forms](/help/forms/forms-submission-service.md) (per inviare dati a fogli di calcolo o e-mail).
* Invia dati all’istanza Publish di AEM per un’elaborazione più avanzata, ad esempio per avviare un flusso di lavoro di AEM, utilizzare il modello dati del modulo o eseguire l’integrazione con altri sistemi aziendali.

**Concetto dell&#39;editor universale**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![Editor universale](/help/forms/assets/eds-ue-based.png)

In questo diagramma vengono illustrate le parti principali dell&#39;Editor universale utilizzate per la creazione di moduli.

### Utilizzo di Forms con l’authoring dei documenti (DA)

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) è un servizio ospitato da Adobe per la creazione e la gestione dei contenuti principali del sito Web (pagine, articoli) che verranno consegnati tramite Edge Delivery Services. È un&#39;alternativa all&#39;utilizzo di SharePoint o Google Drive per il contenuto Edge Delivery Services di origine.

**Informazioni su Document Authoring (DA) per Edge Delivery Services Content**

L’authoring dei documenti offre un ambiente di authoring di livello Enterprise che utilizza Adobe Design System (Spectrum) e il modello di documento di AEM (Blocchi, Sezioni). È progettato per la gestione strutturata dei contenuti per EDS.

**Gestione di Forms da parte di DA (incorporamento, non authoring diretto)**

DA non è uno strumento per la creazione di moduli da zero **.** Si utilizza invece DA per creare le pagine Web, quindi si *incorporano* moduli (creati mediante l&#39;authoring basato su documenti o l&#39;editor universale) nelle pagine create da DA.

**Passaggi per incorporare Forms nelle pagine DA**

1. **Crea modulo:** Crea il modulo utilizzando:
   * Authoring basato su documenti (Word/Google Docs)
   * Editor universale

1. **Pubblica modulo:** Assicurati che il modulo sia pubblicato e accessibile tramite il proprio URL Edge Delivery (ad esempio, `https://your-eds-project.hlx.page/forms/contact-us`).
1. **Creare la pagina in DA:** Creare o modificare la pagina in Document Authoring in cui si desidera visualizzare il modulo.
1. **Incorpora il modulo:** Utilizza un &quot;blocco&quot; o un componente specifico nella pagina DA per fare riferimento al modulo e incorporarlo dal relativo URL. La pagina DA recupera e visualizza il modulo creato esternamente.

**Authoring di documenti con modulo incorporato**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![Authoring dei documenti](/help/forms/assets/eds-da-based.png)

In questo diagramma viene illustrato come creare innanzitutto un modulo utilizzando UE o Docs, quindi incorporarlo in una pagina creata in Document Authoring.


### Confronto delle opzioni di authoring

| Criteri | Authoring basato su documenti | Editor universale (WYSIWYG) | Forms nell’authoring dei documenti (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Strumento di authoring primario** | Word/Google Docs/Fogli | Browser (AEM Universal Editor) | N/D (i Forms sono *embedded*) |
| **Livello abilità team** | Conoscenza degli editor di documenti | Comodità degli strumenti Web visivi | Utilizza DA per il contenuto della pagina |
| **Complessità tipica del modulo** | Da semplice a moderato | Da moderato a complesso, di livello Enterprise | Dipende dal modulo incorporato |
| **Opzione di invio 1 (semplice)** | Servizio di invio Forms (a foglio/e-mail) | Servizio di invio Forms (a foglio/e-mail) | Segue la configurazione del modulo incorporato |
| **Opzione di invio 2 (avanzata)** | N/D | Pubblicazione AEM (flusso di lavoro, FDM, ecc.) | Segue la configurazione del modulo incorporato |
| **Integrazione back-end di AEM** | Minimo | Alta (con invio pubblicazione AEM) | Indirettamente, tramite modulo Editor universale incorporato |
| **Ottimo per...** | Creazione rapida di moduli semplici da parte di team di contenuti, acquisizione rapida dei dati. | Esperti di marketing, utenti aziendali che necessitano di controllo visivo, moduli complessi o un’integrazione approfondita con AEM. | Siti in cui il contenuto principale viene gestito in DA, che richiedono moduli da altre origini. |

**Albero decisionale avanzato**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![Albero delle decisioni](/help/forms/assets/eds-enhanced-decision.png)

## Confronto delle funzioni dei metodi di authoring

La tabella seguente fornisce un confronto dettagliato delle funzioni chiave tra i diversi metodi di authoring dei moduli di AEM, utili per scegliere l’approccio più adatto alle tue esigenze.

| **Funzionalità** | **Editor universale (WYSIWYG)** | **Authoring basato su documenti** | **Authoring di documenti (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Composizione unificata con Sites** | ✅ |                              | ✅ (con moduli incorporati) |
| **Incorporazione del supporto dei moduli** | ✅ | ✅ | ✅ (incorporamento da Universal Editor o Docs) |
| **Regole (comportamento dinamico)** | Editor di regole avanzate con funzioni personalizzate | Limitato: Mostra/nascondi, valore di calcolo, funzioni personalizzate | Dipende dal modulo incorporato |
| **Supporto allegato** | ✅ | ℹ️ (Accesso anticipato) | Dipende dal modulo incorporato |
| **Supporto CAPTCHA** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Dipende dal modulo incorporato |
| **Funzioni di invio** | REST, e-mail, FDM, flusso di lavoro, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Solo foglio di calcolo | Segue la configurazione del modulo incorporato |
| **Schema dati** | FDM, personalizzato | Personalizzato | Basato su modulo incorporato |
| **Precompilazione** | 💡 (tramite procedura guidata) | ✅ | Dipende dal modulo incorporato |
| **Frammenti** | ✅ | ✅ | Dipende dal modulo incorporato |
| **Editor di regole visivo** | ✅ |                              |                              |
| **Localizzazione** | 💡 (tramite Sites) | ℹ️ (manuale Excel/Sheets) | Dipende dal modulo incorporato |
| **Schema dati (struttura dati)** | 💡 (tramite estensione dell’interfaccia utente) |                              |                              |
| **Supporto modello** | Solo contenuto iniziale |                              |                              |
| **Portale** |                               |                              |                              |
| **Tema** | ℹ️ (a livello di progetto) | ℹ️ (a livello di progetto) | ℹ️ (in base al sito di hosting) |
| **Componente personalizzato** | ✅ | ✅ | ✅ (se supportato dal componente incorporato) |
| **Funzioni OOTB e personalizzate** | ✅ | ✅ | ✅ (in formato incorporato) |
| **Riferimento frammento** |                               |                              |                              |
| **Integrazione di Sign** |                               |                              |                              |
| **Sperimentazione** | ✅ | ✅ | Dipende dal contesto di incorporamento |
| **Gestione attività tramite Workfront** | ✅ |                              |                              |
| **Estensione della personalizzazione** | 💡 |                              |                              |
| **Personalizzazione dell’editor** | ✅ (tramite estensione dell’interfaccia utente) |                              |                              |
| **Azione di invio** | ✅ | Solo foglio di calcolo | Basato su modulo incorporato |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

Per sviluppare ciò che hai imparato, ecco come procedere:

[Scegli la strategia di invio](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) per decidere se il progetto richiede la semplicità del servizio di invio di Forms (ideale per l&#39;output di fogli di calcolo/e-mail) o la flessibilità e l&#39;integrazione back-end offerte dalle azioni di invio di pubblicazione di AEM.

Consulta l&#39;articolo [Best practice per la creazione di Forms](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md) per scoprire come progettare moduli efficaci, accessibili e di facile utilizzo.

## Passaggi successivi

Questa guida offre una panoramica dell’utilizzo dei moduli con AEM Edge Delivery Services. Per istruzioni dettagliate su configurazioni specifiche, consulta la documentazione ufficiale di Adobe Experience Manager:

* [Authoring basato su documenti con Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universale con Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Authoring di documenti (DA) e incorporamento di contenuti](https://www.aem.live/developer/da-tutorial)
* [Servizio di invio AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
