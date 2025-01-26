---
title: Panoramica di Edge Delivery Services per AEM Forms
description: Edge Delivery Services per AEM Forms
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ae31df22c723c58addd13485259e92abb4d4ad54
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 11%

---

# Editor universale per Edge Delivery Services per Forms (blocco Forms EDS)


L’Editor universale è progettato per aiutare i creatori di contenuti e gli autori di moduli a creare, gestire e modificare facilmente i moduli. Offre un&#39;esperienza di editing semplice, visiva ed efficiente incentrata sui Edge Delivery Services (EDS).

Con Universal Editor, gli utenti possono trascinare e rilasciare elementi del modulo (come campi di testo, caselle di controllo e pulsanti di scelta) per creare moduli in un&#39;interfaccia What You See Is What You Get (WYSIWYG). Questo approccio rende la creazione di moduli intuitiva e accessibile, anche per chi non dispone di competenze tecniche.

![Editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor.png)

Universal Editor consente ai creatori di contenuti e agli autori di moduli di creare, gestire e modificare i moduli in modo semplice ed efficiente. Questo editor è specificamente focalizzato sui Edge Delivery Services (EDS). L&#39;editor universale fornisce un&#39;esperienza di modifica visiva e intuitiva per la creazione di moduli. È possibile trascinare e rilasciare facilmente gli elementi del modulo (come campi di testo, caselle di controllo, pulsanti di scelta e così via) e configurarli in un&#39;interfaccia di stile WYSIWYG (What You See Is What You Get).

Il punto di forza di Universal Editor risiede nel suo solido set di funzioni, che include funzionalità avanzate di creazione dei moduli, modifica dinamica delle regole e integrazione perfetta con varie sorgenti di dati. Gli utenti possono progettare rapidamente moduli dinamici utilizzando componenti predefiniti, modelli personalizzabili e un’ampia libreria di elementi modulo.

Le funzionalità tecniche sono progettate con attenzione per mantenere un rendering lato client leggero, la compatibilità tra browser diversi e la rigorosa aderenza agli standard di accessibilità. Il blocco Universal Editor for EDS Forms rappresenta una soluzione completa per le organizzazioni che desiderano una piattaforma di creazione e gestione di moduli agile e potente.

## Caratteristiche principali di Universal Editor per EDS Forms


<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/universal-editor.png" alt="Interfaccia WYSIWYG"> 
    <h3>Interfaccia WYSIWYG</h3>
    <p>Universal Editor fornisce un'interfaccia WYSIWYG per la progettazione dei moduli. Fornisce libreria di componenti predefinita, supporto per la progettazione reattiva e creazione di moduli basati su modelli. Puoi aggiungere o rimuovere immediatamente i campi modulo e modificare le proprietà dei campi (come etichetta, associazione dati, convalida). È inoltre possibile collegare componenti modulo personalizzati a Universal Editor.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Editor regole">
    <h3>Editor regole</h3>
    <p>L’editor di regole consente di creare interazioni di moduli sofisticate con regole basate su eventi, convalida immediata e gestione degli errori tramite definizioni leggere basate su JavaScript e JSON.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Invia azioni">
    <h3>Invia azioni</h3>
    <p>Le azioni di invio semplificano i flussi di lavoro di invio dei moduli con opzioni di integrazione back-end, preprocessori di dati, logica di invio condizionale e connessioni endpoint sicure.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Servizi di precompilazione">
    <h3>Servizi di precompilazione</h3>
    <p>I servizi di precompilazione migliorano l’esperienza utente compilando in modo intelligente i campi del modulo con dati rilevanti provenienti da varie origini, riducendo l’immissione manuale dei dati.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Associazione dei dati">
    <h3>Associazione dei dati</h3>
    <p>L'associazione dati consente connessioni dirette e dinamiche tra campi modulo e origini dati back-end, supportando la sincronizzazione in tempo reale e la mappatura complessa dei dati.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Internazionalizzazione/localizzazione">
    <h3>Internazionalizzazione/localizzazione</h3>
    <p>Il supporto per l’internazionalizzazione garantisce l’accessibilità globale con il rendering multilingue, la compatibilità delle lingue da destra a sinistra e la formattazione specifica per le impostazioni internazionali.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Analytics e tracciamento">
    <h3>Analytics e tracciamento</h3>
    <p>I meccanismi di analisi e tracciamento incorporati forniscono informazioni approfondite sulle interazioni dei moduli, sui tassi di invio e sul comportamento degli utenti, consentendo un’ottimizzazione continua.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Sperimentazione (Test A/B)">
    <h3>Sperimentazione (Test A/B)</h3>
    <p>La sperimentazione consente alle organizzazioni di eseguire test A/B sulle progettazioni di moduli per identificare i layout o le funzionalità con prestazioni migliori.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Gestione attività">
    <h3>Gestione attività</h3>
    <p>L’integrazione con Adobe Workfront consente ai team di gestire le attività relative alla creazione e alla manutenzione dei moduli, garantendo una collaborazione semplificata.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(33.33% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="https://via.placeholder.com/150" alt="Personalizzazione editor">
    <h3>Personalizzazione editor</h3>
    <p>Gli sviluppatori possono estendere le funzionalità di Universal Editor tramite estensioni dell’interfaccia utente, abilitando soluzioni personalizzate che soddisfano esigenze organizzative specifiche.</p>
  </div>
</div>


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

## Componenti modulo predefiniti

L’Editor universale fornisce i seguenti componenti di modulo pronti all’uso:

<table>
  <thead>
    <tr>
      <th>Bello</th> 
      <th>Componenti del modulo</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Componenti del modulo" style="width: 100%;"></td> 
      <td><b>Pannello a soffietto</b></td>
      <td>Struttura del pannello comprimibile per organizzare il contenuto.</td>
    </tr>
    <tr>
      <td><b>Pulsante</b></td>
      <td>Aggiunge elementi interattivi per azioni quali navigazione o logica personalizzata.</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Impedisce la posta indesiderata richiedendo agli utenti di completare un'attività di verifica umana utilizzando Google reCaptcha o HCaptcha.</td>
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
      <td>Consente agli utenti di selezionare una data utilizzando un'interfaccia calendario.</td>
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
      <td>Visualizza una finestra di dialogo a comparsa, spesso utilizzata per avvisi, informazioni aggiuntive o conferma.</td>
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
      <td>Attiva l'invio di moduli e avvia flussi di lavoro definiti.</td>
    </tr>
    <tr>
      <td><b>Campo Numero di telefono</b></td>
      <td>Acquisisce i numeri di telefono con una formattazione basata sul paese.</td>
    </tr>
    <tr>
      <td><b>Testo</b></td>
      <td>Fornisce una sezione dedicata per visualizzare i termini legali e raccogliere l’accordo utente tramite le caselle di controllo.</td>
    </tr>
    <tr>
      <td><b>Campo testo</b></td>
      <td>DC acquisisce l’input a riga singola, ad esempio nomi o indirizzi e-mail.</td>
    </tr>
    <tr>
      <td><b>Procedura guidata</b></td>
      <td>Guida gli utenti in un processo di modulo in più parti.</td>
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

-->

Oltre ai componenti modulo predefiniti, l’editor universale supporta anche:

* **Incorporazione di Forms in un&#39;altra pagina Web**: Universal Editor supporta l&#39;incorporamento di moduli direttamente nelle pagine dei siti di Edge Deliver Services. Questa operazione può essere eseguita utilizzando il componente di incorporamento fornito con il prodotto.

* **Messaggi di convalida**: i messaggi di convalida forniscono feedback in tempo reale agli utenti quando immettono dati errati o incompleti. Le funzioni includono:
   * Visualizzazione dinamica degli errori: avvisa immediatamente gli utenti in caso di errori, ad esempio indirizzi e-mail non validi o campi obbligatori mancanti.
   * Messaggi personalizzabili: consente agli autori dei moduli di definire testi di errore facili da usare.
   * Convalida basata su regole: supporta la logica di convalida avanzata, ad esempio il controllo delle dipendenze tra i campi o l’implementazione di regole condizionali.

* **Campi nascosti**: i campi nascosti memorizzano i dati in modo invisibile all&#39;interno del modulo, spesso per l&#39;elaborazione back-end o per valori precompilati. I casi di utilizzo includono:
   * Passaggio di informazioni contestuali (ad esempio, ID utente o dati di sessione) al backend senza visualizzarle agli utenti.
   * Acquisizione di metadati come marche temporali o ID di tracciamento.
   * I campi nascosti non sono visibili agli utenti finali, ma possono essere precompilati, aggiornati dinamicamente o utilizzati nei flussi di lavoro.

* **Componenti personalizzati**: i componenti personalizzati consentono agli sviluppatori di estendere le funzionalità dei moduli creando integrazioni specializzate o di terze parti. Le funzioni includono:
   * Flessibilità: gli sviluppatori possono progettare elementi di modulo univoci personalizzati per casi d’uso specifici.
   * Integrazione di terze parti: incorpora widget o strumenti come gateway di pagamento, tracciatori di Analytics o campi di input basati sull’intelligenza artificiale.
   * Compatibilità perfetta: i componenti personalizzati possono essere integrati con l’interfaccia drag-and-drop dell’editor universale e con le funzioni esistenti, come l’associazione o la convalida dei dati.

* **Configurazione per ringraziamento**: personalizza il messaggio di conferma o la pagina visualizzata dopo l&#39;invio del modulo.

## Onboarding

Per abilitare l’editor universale e l’editor di regole per il tuo ambiente o per richiedere funzioni aggiuntive come Forms Portal, Document of Record, l’integrazione di Adobe Sign o il supporto per la lingua da destra a sinistra, invia una e-mail a mailto:aem-forms-ea@adobe.com dal tuo indirizzo ufficiale insieme alla richiesta.



## Inizia a creare i moduli

* [Guida introduttiva a Edge Delivery Services per AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Creare un modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Impostare i fogli di Google o i file di Microsoft Excel per iniziare ad accettare i dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare il modulo e iniziare a raccogliere i dati](/help/edge/docs/forms/publish-forms.md)
* [Personalizzare l’aspetto dei moduli](/help/edge/docs/forms/style-theme-forms.md)
* [Aggiungere sezioni ripetibili a un modulo](/help/edge/docs/forms/repeatable-forms.md)
* [Mostra un messaggio di ringraziamento personalizzato dopo l’invio del modulo](/help/edge/docs/forms/thank-you-page-form.md)
* [Componenti del blocco modulo adattivo e relative proprietà](/help/edge/docs/forms/form-components.md)
* [Monitoraggio dell’utilizzo reale](https://www.aem.live/developer/rum#authentication)

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