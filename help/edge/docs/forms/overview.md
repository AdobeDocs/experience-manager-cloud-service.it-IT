---
title: Panoramica di Edge Delivery Services per AEM Forms
description: Crea e distribuisci moduli con prestazioni elevate su Adobe Experience Manager Edge Delivery Services, con particolare attenzione all’approccio di authoring dell’editor universale.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 100%

---


# Edge Delivery Services per AEM Forms


Edge Delivery Services per AEM Forms è un set di servizi componibili per un ambiente di sviluppo rapido in cui nuovi moduli possono essere aggiornati, pubblicati e lanciati rapidamente dagli autori. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

Questi servizi consentono di:

- **creare esperienze di iscrizione con strumenti a tua scelta:** aumentare l’efficienza di authoring separando le origini di contenuto. Senza personalizzazioni è possibile utilizzare sia l’authoring basato su documenti (Microsoft SharePoint o Google Drive) che l’authoring WYSIWYG (Editor universale o editor di moduli adattivi). Si possono utilizzare più origini di contenuto nello stesso sito moduli e gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Fogli Google, Editor universale o Editor di moduli adattivi.

- **Offrire esperienze di registrazione digitale eccezionali:** offri esperienze di registrazione digitale che vengono caricate e riprodotte rapidamente, e controlla in modo continuo le prestazioni dei moduli tramite la telemetria operativa. Tempi di caricamento più rapidi e un’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento e conversione dei moduli.

- **Usare set di strumenti intuitivi per gli sviluppatori:** Edge Delivery Services per AEM Forms utilizza il normale linguaggio HTML, CSS moderni e JavaScript Vanilla per creare esperienze eccezionali, evitando la curva di apprendimento ripida di un framework specifico. Uno sviluppatore con competenze di base per lo sviluppo web può personalizzare e creare facilmente componenti ed esperienze di moduli. Non è necessario attendere l’esecuzione di una pipeline, è sufficiente archiviare il codice in GitHub e le modifiche sono live.

## Scelta di un metodo di authoring


Adobe Experience Manager (AEM) Edge Delivery Services (EDS) consente di offrire esperienze web estremamente veloci e altamente scalabili dall’edge. Questa guida spiega **come creare e pubblicare moduli per tali esperienze**, con una chiara gerarchia di consigli:

- **Editor universale (UE): la migliore scelta per la maggior parte dei team**
- **Authoring basato su documenti (documenti/fogli): ideale per moduli semplici e veloci**
- **Authoring di documenti (DA): da utilizzare per incorporare i moduli nelle pagine create da DA**

Alla fine, sarai in grado di scegliere il metodo di authoring adatto, comprendere le opzioni di invio e seguire i passaggi successivi verso i moduli pronti per la produzione.


| Team &amp; requisiti | Metodo consigliato | Perché |
|--------------------|--------------------|-----|
| Gli addetti al marketing e i designer hanno bisogno di controllo visivo, logica condizionale o integrazioni AEM | **Editor universale** | Trascinamento, regole avanzate, invii a FSS o AEM Publish |
| Autori di contenuti che già lavorano in Word/Google Docs/Sheets; acquisizione semplice dei dati su foglio di calcolo/e-mail | **Authoring basato su documenti** | Strumenti noti, percorso più veloce per moduli di base |
| Pagine del sito web generate in **Document Authoring (DA)** | **Incorpora** un modulo UE o basato su documenti nella pagina DA | DA non genera i moduli autonomamente |


## Metodi di authoring in dettaglio

### Editor universale

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">pre-release channel</a>. </span>
-->

[Editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) è uno strumento di authoring visivo e di trascinamento per gli addetti al marketing e i designer che combina velocità e potenza di livello enterprise:

- Editing WYSIWYG in tempo reale e anteprime dei dispositivi.
- Integrazione diretta con AEM Assets, flussi di lavoro e modello dati modulo (FDM).
- Passaggio semplice per sviluppatori di componenti personalizzati in Vanilla JS/CSS.
- Editor di regole avanzate per la creazione di logica complessa.
- Estensibilità lato server per funzionalità personalizzate.
- Esperienza di modifica WYSIWYG per creare e visualizzare facilmente i moduli.
- Documento di funzionalità del record per creare archivi inalterabili dei dati inviati.
- Integrazione con Adobe Sign per le firme elettroniche.
- Integrazione con Adobe Workfront Fusion per attivare scenari Adobe Workfront Fusion al momento dell’invio del modulo.
- Integrazione con diverse origini dati per precompilare i moduli e inviare i dati.
- Modello dati modulo (FDM) per la definizione della struttura dei dati e delle interazioni con varie origini dati.
- Possibilità di scegliere tra più azioni di invio per la gestione degli invii dei moduli, tra cui l’invio di dati a Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e molte altre origini dati.
- Invia utilizzando le azioni di invio del servizio di invio moduli (FSS) o AEM Publish

**Consiglio**: avvia ogni nuovo progetto di modulo con l’editor universale a meno che il team non sia interamente incentrato sul documento e il modulo non sia molto semplice.


### Authoring basato su documenti (utilizzando Microsoft Docs o Google Sheets)

[Authoring basato su documenti](/help/edge/docs/forms/tutorial.md) è ideale per la creazione di moduli semplici e a bassa complessità utilizzando strumenti noti come Microsoft Word, Google Docs o Google Sheets. Questo metodo è ideale per i team di contenuti che richiedono un modo rapido e diretto per creare moduli.

- Componenti accessibili per un’esperienza di facile utilizzo.
- Struttura HTML standardizzata per un rendering coerente.
- Regole e convalide per garantire l’accuratezza dei dati.
- Opzioni di file allegato per la raccolta di informazioni aggiuntive.
- Integrazione del servizio reCaptcha di Google per la protezione da posta indesiderata.
- Possibilità di creare componenti modulo personalizzati per esigenze specifiche.
- Inviare i dati del modulo direttamente a Microsoft Excel o Fogli Google o indirizzi e-mail.
- Monitorare le prestazioni dei moduli tramite la telemetria operativa


### Incorporamento di moduli in Document Authoring (DA)

Document Authoring (DA) è progettato per la creazione di contenuti di pagina strutturati e non supporta la creazione di moduli nativi. Per aggiungere un modulo a una pagina creata da DA, è possibile creare il modulo utilizzando l’**editor universale** (consigliato) o l&#39;authoring basato su documenti e incorporarlo nella pagina di authoring dei documenti.

## Pubblicazione di moduli di Edge Delivery Services {#edge-overview}

Il diagramma seguente illustra come modificare il contenuto in Microsoft Excel o Fogli Google (modifica basata su documento) e pubblicarlo in Edge Delivery Services. Mostra anche il metodo di pubblicazione di AEM utilizzando l’authoring WYSIWYG (editor universale).

![Pubblicare in Edge Delivery Services e AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |
-->

## Passaggi successivi

- [Funzioni e funzionalità dell’editor universale per i moduli di Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Creare il primo modulo utilizzando l’editor universale](/help/edge/docs/forms/universal-editor/create-forms.md)
- [Crea il primo modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/tutorial.md).
- [Moduli incorporati in Document Authoring (DA)](https://www.aem.live/developer/da-tutorial)


Ora puoi creare il tuo primo modulo a prestazioni elevate con AEM Edge Delivery Services.

<!--
## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
