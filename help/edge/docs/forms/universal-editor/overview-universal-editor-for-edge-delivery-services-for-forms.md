---
title: Editor universale di moduli per Edge Delivery Services
description: Utilizza l’editor universale di moduli per Edge Delivery Services per creare moduli adattivi.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 99%

---


# Editor universale di moduli per Edge Delivery Services

<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail con il nome dell’organizzazione e il nome dell’archivio GitHub dall’indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

L’editor universale rivoluziona la creazione di moduli per Edge Delivery Services di Adobe, grazie a un’interfaccia WYSIWYG (What You See Is What You Get) semplice, visiva e intuitiva. Progettato per chi crea contenuti e moduli, elimina la complessità dei processi tradizionali di creazione dei moduli, rendendola accessibile anche agli utenti non tecnici.

Con l’editor universale è possibile progettare rapidamente moduli interattivi e reattivi utilizzando componenti predefiniti quali campi di testo, caselle di controllo e pulsanti di scelta. Il suo solido set di funzioni supporta regole dinamiche, integrazione perfetta dei dati e personalizzazione avanzata, affinché ogni modulo possa essere personalizzato in base alle tue esigenze.

Che si tratti di gestire un rendering snello lato client, garantire la compatibilità tra browser diversi o rispettare rigorosi standard di accessibilità, l’editor universale offre una soluzione semplificata per la creazione e la gestione dei moduli.

![Editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Funzioni chiave dell’editor universale di moduli per Edge Delivery Services



| ![Interfaccia WYSIWYG](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![Editor di regole](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![Azioni di invio](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Interfaccia WYSIWYG**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**Editor di regole**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**Azioni di invio**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| L’editor universale fornisce un’interfaccia WYSIWYG per la progettazione di moduli con una libreria di componenti predefinita e funzionalità per la progettazione responsive, la creazione basata su modelli e la modifica dei campi in tempo reale. | L’editor di regole consente di creare interazioni dinamiche nei moduli utilizzando regole basate su eventi, convalida immediata e gestione degli errori tramite codici JavaScript e JSON snelli. | Le azioni di invio supportano l’integrazione back-end, la logica di invio condizionale, gli endpoint sicuri e i preprocessori, per flussi di lavoro di invio più semplici e diretti. |

| ![Pubblicazione/Annullamento della pubblicazione](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![Componenti personalizzati](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Pubblicazione/Annullamento della pubblicazione**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**Modalità reattiva**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**Componenti personalizzati**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| Controlla facilmente la visibilità dei moduli, pubblicandoli o annullandone la pubblicazione direttamente dall’editor con pochi clic. | Progetta moduli che si adattino perfettamente ai diversi dispositivi (desktop, tablet e dispositivi mobili). Utilizza la modalità reattiva per visualizzare in anteprima e testare i moduli per schermi di diverse dimensioni. | I componenti personalizzati consentono agli sviluppatori di estendere le funzionalità dei moduli creando elementi univoci personalizzati per casi d’uso specifici a livello organizzativo. |

| ![Definizione dello stile](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![Servizi di precompilazione](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![Test A/B](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Definizione dello stile**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **Servizi di precompilazione** (disponibile a breve) | [**Test A/B**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| La definizione dello stile con CSS consente agli sviluppatori di personalizzare l’aspetto degli elementi del modulo e di creare un design visivamente accattivante e allineato all’estetica del sito web. | I servizi di precompilazione compilano automaticamente i campi del modulo con i dati utente pertinenti provenienti da varie origini, riducendo l’input manuale e migliorando l’esperienza utente. | Il test A/B consente alle organizzazioni di sperimentare diverse progettazioni, layout e funzionalità nei moduli per individuare le varianti che offrono prestazioni migliori. |

| ![Analisi e tracciamento](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![Frammenti di modulo](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![Associazione dei dati](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Analisi e tracciamento**](https://www.aem.live/developer/martech-integration) | **Frammenti di modulo** (presto disponibili) | [**Associazione dei dati**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| Con le funzionalità di analisi e tracciamento integrate puoi ottenere informazioni sul comportamento degli utenti, sulle interazioni con i moduli e sui tassi di invio, per l’ottimizzazione dei moduli basata sui dati. | I frammenti di modulo facilitano il riutilizzo consentendo la creazione di sezioni di uso comune una sola volta e il relativo riutilizzo in più moduli, garantendo coerenza e riducendo le attività di manutenzione. | L’associazione dei dati consente connessioni dirette tra i campi modulo e le origini dati back-end, e supporta gli aggiornamenti in tempo reale e la mappatura avanzata dei dati. |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Incorporazione dei moduli](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Configurazione del ringraziamento](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**CAPTCHA**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **Incorporazione dei moduli** (presto disponibile) | [**Configurazione del ringraziamento**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| Utilizza reCAPTCHA per proteggere i moduli dai bot automatizzati, garantendo una raccolta dati sicura e affidabile. | I moduli possono essere incorporati direttamente nelle pagine dei siti Edge Delivery Services utilizzando il componente Incorpora integrato nell’editor universale. | Personalizza facilmente il messaggio di ringraziamento o la pagina mostrata agli utenti dopo l’invio corretto del modulo. |


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## Componenti dei moduli predefiniti

L’editor universale fornisce i seguenti componenti dei moduli predefiniti:

<table>
  <thead>
    <tr>
      <th></th> 
      <th>Componenti dei moduli</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Componenti dei moduli" style="width: 100%;"></td> 
      <td><b>Pannello a soffietto</b></td>
      <td>Struttura del pannello comprimibile per organizzare il contenuto.</td>
    </tr>
    <tr>
      <td><b>Pulsante</b></td>
      <td>Aggiunge elementi interattivi per azioni quali navigazione o logica personalizzata.</td>
    </tr>
    <tr>
      <td><b>CAPTCHA</b></td>
      <td>Impedisce la posta indesiderata richiedendo agli utenti di completare un’attività di verifica umana utilizzando Google reCAPTCHA o hCAPTCHA.</td>
    </tr>
    <tr>
      <td><b>Casella di controllo</b></td>
      <td>Consente agli utenti di configurare una casella di controllo.</td>
    </tr>
    <tr>
      <td><b>Gruppo di caselle di controllo</b></td>
      <td>Consente agli utenti di selezionare più opzioni da un gruppo.</td>
    </tr>
    <tr>
      <td><b>Selettore data</b></td>
      <td>Consente agli utenti di selezionare una data utilizzando un’interfaccia calendario.</td>
    </tr>
    <tr>
      <td><b>Elenchi a discesa</b></td>
      <td>Offre opzioni a selezione singola o multipla da un elenco predefinito.</td>
    </tr>
    <tr>
      <td><b>E-mail</b></td>
      <td>Acquisisce gli indirizzi e-mail con la convalida del formato di base.</td>
    </tr>
    <tr>
      <td><b>Allegato file</b></td>
      <td>Consente il caricamento di documenti, immagini o altri tipi di file.</td>
    </tr>
    <tr>
      <td><b>Frammenti di modulo</b></td>
      <td>Componenti del modulo riutilizzabili per sezioni come campi indirizzo o dettagli di contatto.</td>
    </tr>
    <tr>
      <td><b>Immagine</b></td>
      <td>Supporta il caricamento e la visualizzazione di immagini nei moduli.</td>
    </tr>
    <tr>
      <td><b>Finestra modale</b></td>
      <td>Mostra una finestra di dialogo a comparsa, spesso utilizzata per avvisi, informazioni aggiuntive o conferma.</td>
    </tr>
    <tr>
      <td><b>Campo numerico</b></td>
      <td>Acquisisce l’input numerico, consentendo la convalida di numeri o intervalli.</td>
    </tr>
    <tr>
      <td><b>Pannello</b></td>
      <td>Organizza le sezioni dei moduli con pannelli espandibili/comprimibili.</td>
    </tr>
    <tr>
      <td><b>Pulsanti di scelta</b></td>
      <td>Abilita la selezione a scelta singola da un gruppo di opzioni.</td>
    </tr>
    <tr>
      <td><b>Valutazione</b></td>
      <td>Consente agli utenti di fornire una valutazione basata su stelle.</td>
    </tr>
    <tr>
      <td><b>Pulsante Ripristina</b></td>
      <td>Ripristina lo stato predefinito dei campi modulo.</td>
    </tr>
    <tr>
      <td><b>Pulsante Invia</b></td>
      <td>Attiva l’invio di moduli e avvia flussi di lavoro definiti.</td>
    </tr>
    <tr>
      <td><b>Campo numero di telefono</b></td>
      <td>Acquisisce i numeri di telefono con una formattazione basata sul paese.</td>
    </tr>
    <tr>
      <td><b>Testo</b></td>
      <td>Fornisce una sezione dedicata per visualizzare i termini legali e raccogliere l’accordo utente tramite le caselle di controllo.</td>
    </tr>
    <tr>
      <td><b>Campo testo</b></td>
      <td>Acquisisce l’input a riga singola, ad esempio nomi o indirizzi e-mail.</td>
    </tr>
    <tr>
      <td><b>Procedura guidata</b></td>
      <td>Guida gli utenti attraverso un processo di modulo in più parti.</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## Onboarding

<span class="preview"> Questa è una funzionalità pre-release disponibile tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>

## Domande frequenti (FAQ)

**D. Chi può utilizzare l’editor universale?**
L’editor universale è progettato per un pubblico ampio, tra cui:

* Creatori di contenuti che desiderano creare moduli visivamente accattivanti.
* Sviluppatori che richiedono funzionalità avanzate di personalizzazione e integrazione.
* Organizzazioni alla ricerca di soluzioni di moduli scalabili, sicure e conformi.

**D: è possibile integrare i moduli creati con l’editor universale nei sistemi esistenti?**
Assolutamente. L’editor universale supporta l’associazione diretta dei dati con i sistemi back-end, consentendo aggiornamenti in tempo reale e mappatura avanzata dei dati. Si integra anche con strumenti come Adobe Workfront per la gestione delle attività e supporta endpoint sicuri per i flussi di lavoro di invio dei dati.

**D: è possibile personalizzare i componenti del modulo?**
Sì, l’editor universale consente agli sviluppatori di creare componenti personalizzati in base a esigenze organizzative specifiche. Inoltre, puoi estendere le funzionalità dell’editor tramite estensioni dell’interfaccia utente e flussi di lavoro personalizzati.

**D: in che modo l’editor universale gestisce l’accessibilità?**
L’editor universale è progettato in modo da rispettare rigorosamente gli standard di accessibilità, incluse le linee guida per l’accessibilità dei contenuti WCAG (Web Content Accessibility Guidelines). In questo modo i moduli sono utilizzabili da persone affette da disabilità e forniscono un’esperienza inclusiva.

**D: che tipo di analisi è possibile ottenere dai moduli?**
L’editor universale include strumenti di analisi e tracciamento incorporati per monitorare le interazioni degli utenti, i tassi di invio dei moduli e le metriche di conversione. Queste informazioni consentono di ottimizzare i moduli per ottenere prestazioni migliori.


## Iniziare a creare i moduli

{{universal-editor-see-also}}

