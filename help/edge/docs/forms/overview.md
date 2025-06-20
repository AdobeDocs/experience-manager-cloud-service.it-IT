---
title: Panoramica di Edge Delivery Services per AEM Forms
description: Edge Delivery Services per AEM Forms
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: ht
source-wordcount: '1033'
ht-degree: 100%

---

# Edge Delivery Services per AEM Forms


Edge Delivery Services per AEM Forms è un set di servizi componibili per un ambiente di sviluppo rapido in cui nuovi moduli possono essere aggiornati, pubblicati e lanciati rapidamente dagli autori. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

Questi servizi consentono di:

* **creare esperienze di iscrizione con strumenti a tua scelta:** aumentare l’efficienza di authoring separando le origini di contenuto. Senza personalizzazioni è possibile utilizzare sia l’authoring basato su documenti (Microsoft SharePoint o Google Drive) che l’authoring WYSIWYG (Editor universale o editor di moduli adattivi). Si possono utilizzare più origini di contenuto nello stesso sito moduli e gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Fogli Google, Editor universale o Editor di moduli adattivi.

* **Offrire esperienze di registrazione digitale eccezionali:** offri esperienze di registrazione digitale che vengono caricate e riprodotte rapidamente, e controlla in modo continuo le prestazioni dei moduli tramite la telemetria operativa. Tempi di caricamento più rapidi e un’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento e conversione dei moduli.

* **Usare set di strumenti intuitivi per gli sviluppatori:** Edge Delivery Services per AEM Forms utilizza il normale linguaggio HTML, CSS moderni e JavaScript Vanilla per creare esperienze eccezionali, evitando la curva di apprendimento ripida di un framework specifico. Uno sviluppatore con competenze di base per lo sviluppo web può personalizzare e creare facilmente componenti ed esperienze di moduli. Non è necessario attendere l’esecuzione di una pipeline, è sufficiente archiviare il codice in GitHub e le modifiche sono live.

## Panoramica di Edge Delivery Services per AEM Forms {#edge-overview}

Edge Delivery Services per AEM Forms offre un elevato grado di flessibilità nel modo in cui vengono creati i moduli sul sito web. È possibile creare contenuti e moduli con [authoring WYSIWYG](/help/forms/creating-adaptive-form-core-components.md) nonché [authoring basato su documenti](/help/edge/docs/forms/create-forms.md). Edge Delivery Services per AEM Forms fornisce un blocco di moduli, noto come [blocco di moduli adattivi](/help/edge/docs/forms/create-forms.md), per aggiungere un modulo al sito Edge Delivery Services.

Ad esempio, i moduli vengono creati direttamente in Microsoft Excel o Fogli Google e questi fogli di calcolo vengono trasformati in moduli per il sito Web. Qualsiasi nuovo modulo o relativo contenuto, ad esempio un nuovo campo modulo, è immediatamente disponibile sul sito web senza che sia necessario ricrearlo.

Il diagramma seguente illustra come modificare il contenuto in Microsoft Excel o Fogli Google (modifica basata su documento) e pubblicarlo in Edge Delivery Services. Mostra anche il metodo di pubblicazione AEM utilizzando l’authoring WYSIWYG (Editor universale o editor di moduli adattivi).

![Pubblicare in Edge Delivery Services e AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services per AEM Forms sfrutta GitHub per consentire di gestire e distribuire il codice direttamente dall’archivio GitHub. Ad esempio, puoi scrivere contenuti in [Fogli Google](/help/edge/docs/forms/create-forms.md) o in [Microsoft Excel](/help/edge/docs/forms/create-forms.md) e i componenti dei moduli possono essere sviluppati utilizzando CSS e JavaScript in un archivio GitHub.

Quando i moduli sono pronti, puoi utilizzare l’estensione del browser [barra laterale di AEM](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare gli aggiornamenti dei contenuti.

![Installare la barra laterale di AEM](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

La scelta tra [authoring basato su documenti](#document-based-authoring-features) e [authoring WYSIWYG](#wysiwyg-authoring-features) dipende dai requisiti specifici:

* Per i moduli semplici che raccolgono solo informazioni di base con alcuni campi (si pensi ai moduli Contattaci, ai moduli di generazione di lead o ai moduli di richiesta di assistenza) e dove è necessaria una connettività dati rapida tramite un foglio di calcolo, l’[authoring basato su documenti](#document-based-authoring-features) è una buona scelta. È possibile creare questi moduli come si farebbe per un documento in Fogli Google o Microsoft Excel.

* Per i moduli complessi, come quelli che richiedono più pannelli, regole complesse e logica di business, manipolazione dei dati, integrazione con sistemi esterni o flussi di lavoro semplificati tramite le funzioni AEM, l’[Authoring WYSIWYG](#wysiwyg-authoring-features) rappresenta un’opzione migliore.


### Caratteristiche principali dell’authoring basato su documenti e dell’authoring WYSIWYG

L’authoring basato su documenti offre una serie di funzioni di base e l’authoring WYSIWYG sblocca funzionalità aggiuntive oltre all’authoring basato su documenti, consentendo di creare moduli più complessi e interattivi. Le caratteristiche chiave dell’authoring basato su documenti e dell’authoring WYSIWYG sono:

#### Funzionalità di authoring basate su documenti

L’authoring basato su documenti consente di creare moduli utilizzando strumenti familiari come Microsoft Excel o Fogli Google. Questi moduli offrono le seguenti funzionalità:

* Componenti accessibili per un’esperienza di facile utilizzo.
* Struttura HTML standardizzata per un rendering coerente.
* Regole e convalide per garantire l’accuratezza dei dati.
* Opzioni di file allegato per la raccolta di informazioni aggiuntive.
* Integrazione del servizio reCaptcha di Google per la protezione da posta indesiderata.
* Possibilità di creare componenti modulo personalizzati per esigenze specifiche.
* Inviare i dati del modulo direttamente a Microsoft Excel o Fogli Google o indirizzi e-mail.
* Monitorare le prestazioni dei moduli tramite la telemetria operativa

#### Funzionalità di authoring WYSIWYG

L’authoring WYSIWYG fornisce l’interfaccia omonima (Editor universale o editor di moduli adattivi) per la creazione di moduli e offre tutte le funzionalità dell’authoring basato su documenti, oltre a un’ampia gamma di funzionalità aggiuntive:

* Editor di regole avanzate per la creazione di logica complessa.
* Estensibilità lato server per funzionalità personalizzate.
* Esperienza di modifica WYSIWYG per creare e visualizzare facilmente i moduli.
* Documento di funzionalità del record per creare archivi inalterabili dei dati inviati.
* Integrazione con Adobe Sign per le firme elettroniche.
* Integrazione con Adobe Workfront Fusion per attivare scenari Adobe Workfront Fusion al momento dell’invio del modulo.
* Integrazione con diverse origini dati per precompilare i moduli e inviare i dati.
* Modello dati del modulo (FDM) per la definizione della struttura dei dati e delle interazioni con varie origini dati.
* Possibilità di scegliere tra più azioni di invio per la gestione degli invii dei moduli, tra cui l’invio di dati a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e molte altre origini dati.

Le funzioni di cui sopra sono disponibili anche tramite editor di moduli adattivi.

In sostanza, l’authoring WYSIWYG (Editor universale o [editor di moduli adattivi](/help/forms/creating-adaptive-form-core-components.md)) si basa sui fondamenti dell’[authoring basato su documenti](/help/edge/docs/forms/create-forms.md), fornendo un toolkit più avanzato per la creazione e la gestione di moduli complessi.

>[!NOTE]
>
>
> La funzionalità di authoring WYSIWYG è disponibile nell’ambito del programma per i primi utilizzatori. Se ti interessa, invia una breve e-mail dal tuo indirizzo di lavoro a aem-forms-ea@adobe.com per richiedere l’accesso a questa funzionalità.

### Edge Delivery Services per AEM Forms

: authoring, pubblicazione e invio di moduli

I seguenti diagrammi illustrano il processo di creazione, pubblicazione e invio di moduli tramite l’authoring basato su documenti e l’authoring WYSIWYG.

![Authoring basato su documenti](/help/edge/assets/document-based-authoring-workflow.png)

![Authoring WYSIWYG](/help/edge/assets/wysiwyg-authoring-workflow.png)

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