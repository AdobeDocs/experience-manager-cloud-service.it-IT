---
title: Panoramica dei Edge Delivery Services AEM Forms
description: I Edge Delivery Services AEM Forms sono stati progettati per offrire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 2b64cc8d2afb7d6064d1f60ba023448171862236
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 15%

---

# Edge Delivery Services AEM Forms

Semplifica la creazione di moduli e aumenta i tassi di completamento con i Edge Delivery Services AEM Forms di Adobe. Questo servizio potente e componibile consente di creare moduli di livello enterprise con prestazioni eccezionali e un impatto visivo straordinario. L’AEM dà priorità sia all’esperienza utente che agli obiettivi aziendali, garantendo tempi di caricamento estremamente rapidi e un aumento delle conversioni dei moduli.

Puoi utilizzare il servizio per:

* **Creare esperienze di registrazione eccezionali**: crea esperienze di registrazione che consentono di caricare ed eseguire il rendering rapidamente, anche su connessioni Internet lente. I tempi di caricamento più rapidi e l’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento dei moduli e a tassi di conversione migliorati.

* **Creare esperienze di iscrizione con strumenti a tua scelta**: aumenta l’efficienza dell’authoring disaccoppiando le origini di contenuto. È possibile utilizzare entrambi **authoring basato su documenti** (Microsoft SharePoint o Google Drive) e **Authoring AEM** (Editor Forms adattivo). È quindi possibile utilizzare più origini di contenuto nello stesso modulo e utilizzare gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Google Sheets o Adaptive Forms Editor.

* **Usa set di strumenti intuitivo per gli sviluppatori:** AEM Forms utilizza JavaScript plain HTML, modern CSS e vanilla per creare esperienze eccezionali senza il solito sovraccarico. Qualsiasi sviluppatore con conoscenze di base di HTML, CSS e JS dovrebbe essere in grado di creare i propri componenti e non dovrebbe dover imparare alcun linguaggio o framework specifico. Non è necessario usare alcuna pipeline o attendere, archivia il codice in Github e le modifiche sono live. Inoltre, non è necessario eseguire alcuna pipeline o attendere, archivia il codice in Github e le modifiche sono live.


## Panoramica dei Edge Delivery Services AEM Forms {#edge-overview}

Il diagramma seguente illustra come modificare il contenuto in Microsoft Excel o in fogli Google (modifica basata su documento) e pubblicarlo in Edge Delivery Services. Mostra anche il metodo di pubblicazione dell’AEM utilizzando l’editor di Forms adattivo.

![Architettura di Edge Delivery](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità nel modo in cui vengono creati i contenuti sul sito Web. Come accennato in precedenza, puoi utilizzare entrambi [Gestione dei contenuti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=it) con [Authoring AEM](/help/implementing/universal-editor/introduction.md) nonché [authoring basato su documenti](https://www.aem.live/docs/authoring)

È ad esempio possibile utilizzare il contenuto direttamente da Microsoft Excel o Google Sheets. Ciò significa che il contenuto proveniente da tali origini può diventare un modulo sul sito Web. Il nuovo contenuto viene aggiunto immediatamente senza che sia necessario ricrearlo.

Edge Delivery Services sfrutta GitHub per consentire alla clientela di gestire e distribuire il codice direttamente dall’archivio GitHub. Ad esempio, puoi scrivere moduli in Google Sheets o Microsoft Excel e i componenti dei moduli possono essere sviluppati utilizzando CSS e JavaScript in GitHub. Quando è tutto pronto, puoi utilizzare l’estensione del browser Sidekick per visualizzare in anteprima e pubblicare gli aggiornamenti dei contenuti.

AEM Forms Edge Delivery Services fornisce un blocco di moduli, noto come [Blocco Forms adattivo](/help/edge/docs/forms/create-forms.md) per aggiungere un modulo al sito Edge Delivery Services.

### Caratteristiche principali dei Edge Delivery Services AEM Forms

L’authoring basato sui documenti e un set di funzioni di base e l’authoring AEM consentono di usufruire di funzionalità aggiuntive oltre all’authoring basato sui documenti, per creare moduli più complessi e interattivi. La tabella seguente evidenzia le funzioni chiave per entrambi:

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

|                                           | Authoring basato su documenti | Authoring AEM (editor Forms adattivo) |
| ----------------------------------------- | ------------------------ | ------------------------------------ |
| **Funzionalità modulo** |                          |                                      |
| Componenti accessibili | ✓ | ✓ |
| Struttura HTML standardizzata | ✓ | ✓ |
| Regole e convalide | ✓ | ✓ |
| Allegati (caricamento file) | ✓ | ✓ |
| Google reCAPTCHA | ✓ | ✓ |
| Componenti personalizzati | ✓ | ✓ |
| Invia a e-mail | ✓ | ✓ |
| **Funzioni avanzate** |                          |                                      |
| Regole avanzate con editor di regole visive |                          | ✓ |
| Estensibilità lato server |                          | ✓ |
| Più azioni di invio |                          | ✓ |
| **Progettazione e gestione moduli** |                          |                                      |
| Editor Forms adattivo per la modifica WYSIWYG |                          | ✓ |
| **Integrazioni** |                          |                                      |
| Documento record |                          | ✓ |
| Integrazione con Adobe Sign |                          | ✓ |
| Integrazione con Adobe Analytics |                          | ✓ |
| Integrazione con Marketo |                          | ✓ |
| Integrazione con più origini dati |                          | ✓ |
| Più azioni di invio |                          | ✓ |


## Inizia a creare i moduli

* [Guida introduttiva: tutorial per sviluppatori](/help/edge/docs/forms/tutorial.md)
* [Creare un modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Inviare i moduli direttamente ai fogli di Microsoft Excel o Google](/help/edge/docs/forms/submit-forms.md)
* [Migliora l’aspetto dei moduli: guida allo stile](/help/edge/docs/forms/style-theme-forms.md)


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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->