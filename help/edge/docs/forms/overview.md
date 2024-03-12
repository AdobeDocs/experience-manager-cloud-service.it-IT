---
title: Panoramica dei Edge Delivery Services AEM Forms
description: I Edge Delivery Services AEM Forms sono stati progettati per offrire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# Edge Delivery Services AEM Forms

AEM Forms Edge Delivery Services è un insieme componibile di servizi che consente un ambiente di sviluppo rapido in cui gli autori possono aggiornare, pubblicare e avviare rapidamente nuovi moduli. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

Questi servizi consentono di:

* **Crea esperienze di iscrizione con strumenti a tua scelta:** Aumentare l’efficienza di authoring disaccoppiando le origini di contenuto. È possibile utilizzare sia l’authoring basato su documenti (Microsoft SharePoint o Google Drive) che l’authoring AEM (Adaptive Forms Editor). È possibile utilizzare più origini di contenuto nello stesso sito moduli e utilizzare gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Google Sheets o Adaptive Forms Editor.

* **Offri esperienze di registrazione digitale eccezionali:** Fornisci esperienze di registrazione digitale da caricare ed eseguire rapidamente il rendering. Tempi di caricamento più rapidi e un’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento e conversione dei moduli.

* **Usa set di strumenti intuitivo per gli sviluppatori:** I Edge Delivery Services AEM Forms utilizzano plain HTML, modern CSS e JavaScript vanilla per creare esperienze eccezionali, evitando la curva di apprendimento ripida di un framework specifico. Uno sviluppatore con competenze di base per lo sviluppo web può personalizzare e creare facilmente componenti ed esperienze di moduli. Non è necessario attendere l’esecuzione di una pipeline, è sufficiente archiviare il codice in GitHub e le modifiche sono live.

## Panoramica dei Edge Delivery Services AEM Forms {#edge-overview}

I servizi di distribuzione Edge di AEM Forms offrono un elevato grado di flessibilità nelle modalità di authoring dei moduli sul sito web. È possibile creare contenuti e moduli con [Authoring AEM](/help/forms/creating-adaptive-form-core-components.md) nonché [Authoring basato su documenti](/help/edge/docs/forms/create-forms.md). I Edge Delivery Services AEM Forms forniscono un blocco di moduli, noto come [Blocco Forms adattivo](/help/edge/docs/forms/create-forms.md) per aggiungere un modulo al sito Edge Delivery Services.

Ad esempio, i moduli vengono creati direttamente in Microsoft Excel o nei fogli di Google e questi fogli di calcolo vengono trasformati in moduli per il sito Web. Qualsiasi nuovo modulo o contenuto del modulo, ad esempio un nuovo campo modulo, è immediatamente disponibile sul sito web senza che sia necessario un processo di ricostruzione.

Il diagramma seguente illustra come modificare i moduli in Microsoft Excel o Google Sheets (authoring basato su documenti) e pubblicarli in Edge Delivery Services. Mostra anche il metodo di pubblicazione dell’AEM utilizzando l’editor di Forms adattivo (AEM Authoring).

![Architettura di Edge Delivery](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

I Edge Delivery Services AEM Forms utilizzano GitHub per consentire ai clienti di gestire e distribuire il codice direttamente dall’archivio GitHub. Ad esempio, è possibile scrivere moduli in [Fogli Google](/help/edge/docs/forms/create-forms.md) o [Microsoft Excel](/help/edge/docs/forms/create-forms.md) e i componenti dei moduli possono essere sviluppati utilizzando CSS e JavaScript in un archivio GitHub.

Quando i moduli sono pronti, è possibile utilizzare [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), un’estensione del browser chrome, per visualizzare in anteprima e pubblicare gli aggiornamenti dei contenuti.

![Installa AEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

La scelta tra [Authoring basato su documenti](#document-based-authoring-features) e [Authoring AEM](#aem-authoring-features) dipende dai requisiti specifici:

* Per i moduli semplici che raccolgono solo informazioni di base con alcuni campi (si pensi ai moduli Contattaci, ai moduli di generazione di lead o ai moduli di richiesta di assistenza) e dove è necessaria una connettività dati rapida utilizzando un foglio di calcolo, il [Authoring basato su documenti](#document-based-authoring-features) è un buon abbinamento. È possibile creare questi moduli come si farebbe per un documento in Google Sheets o Microsoft Excel.

* Per i moduli complessi, come i moduli che richiedono più pannelli, regole complesse e logica di business, manipolazione dei dati, integrazione con sistemi esterni o flussi di lavoro semplificati utilizzando le funzioni AEM, [Authoring AEM](#aem-authoring-features) è un&#39;opzione migliore.


### Caratteristiche principali dell’authoring basato su documenti e dell’authoring AEM

L’authoring basato su documenti offre una serie di funzioni di base e l’authoring AEM sblocca funzionalità aggiuntive oltre all’authoring basato su documenti, consentendoti di creare moduli più complessi e interattivi. Le caratteristiche chiave dell’authoring basato su documenti e dell’authoring AEM sono:

#### Funzioni di authoring basate su documenti

L’authoring basato su documenti consente di creare moduli utilizzando strumenti familiari come Microsoft Excel o Google Sheets. Questi moduli offrono le seguenti funzionalità:

* Componenti accessibili per un’esperienza di facile utilizzo.
* Struttura HTML standardizzata per un rendering coerente.
* Regole e convalide per garantire l’accuratezza dei dati.
* Opzioni di file allegato per la raccolta di informazioni aggiuntive.
* Integrazione di Google reCAPTCHA per la protezione da posta indesiderata.
* Possibilità di creare componenti modulo personalizzati per esigenze specifiche.
* Inviare i dati del modulo direttamente a Microsoft Excel o Google Sheets o indirizzi e-mail.

#### Funzioni di authoring AEM

L’authoring AEM fornisce un’interfaccia WYSIWYG (Adaptive Forms Editor) per la creazione di moduli e offre tutte le funzionalità dell’authoring basato su documenti, oltre a un’ampia gamma di funzioni aggiuntive:

* Editor di regole avanzate per la creazione di logica complessa.
* Estensibilità lato server per funzionalità personalizzate.
* Esperienza di modifica WYSIWYG per creare e visualizzare facilmente i moduli.
* Documento di funzionalità di registrazione per creare archivi a prova di manomissione dei dati inviati.
* Integrazione con Adobe Sign per le firme elettroniche.
* Integrazione con Adobe Workfront Fusion per attivare scenari Adobe Workfront Fusion al momento dell’invio del modulo.
* Integrazione con diverse origini dati per precompilare i moduli e inviare i dati.
* Modello dati modulo per definire la struttura dei dati e le interazioni con varie origini dati.
* Possibilità di scegliere tra più azioni di invio per la gestione degli invii di moduli, tra cui l&#39;invio di dati a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e molte altre origini dati.

In sostanza, [Authoring AEM](/help/forms/creating-adaptive-form-core-components.md) si basa sulle basi di [Authoring basato su documenti](/help/edge/docs/forms/create-forms.md), fornendo un toolkit più avanzato per la creazione e la gestione di moduli complessi.

>[!NOTE]
>
>
> La funzionalità di authoring dell’AEM è disponibile nell’ambito del programma per l’adozione anticipata. Se sei interessato, invia una breve e-mail dal tuo indirizzo di lavoro a aem-forms-ea@adobe.com per richiedere l’accesso alla funzionalità.

### Edge Delivery Services AEM Forms: authoring. Pubblicazione e presentazione di Forms

I seguenti diagrammi illustrano il processo di creazione, pubblicazione e invio di moduli tramite l’authoring basato su documenti e l’authoring AEM.

![Authoring basato su documenti ](/help/edge/assets/document-based-authoring-workflow.png)

![Authoring AEM](/help/edge/assets/aem-authoring-workflow.png)




## Inizia a creare i moduli

* [Introduzione ai Edge Delivery Services AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Creare un modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Imposta i fogli di Google o i file di Microsoft Excel per iniziare ad accettare i dati&#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare il modulo e iniziare a raccogliere i dati](/help/edge/docs/forms/publish-forms.md)
* [Personalizzare l&#39;aspetto dei moduli&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Aggiungere sezioni ripetibili a un modulo&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Mostra un messaggio di ringraziamento personalizzato dopo l’invio del modulo&#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Componenti del blocco di modulo adattivo e relative proprietà](/help/edge/docs/forms/form-components.md)















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