---
title: Panoramica del servizio di distribuzione AEM Forms Edge
description: Il servizio AEM Forms Edge Delivery è stato progettato per garantire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 4%

---


# Servizio di consegna AEM Forms Edge {#aem-forms-edge-delivery-service-overview}


<div style="font-family: Arial, sans-serif; margin: 0; padding: 0;">
        <main class="content">
            <section class="content-section">
                <p style="line-height: 1.5;">AEM Forms Edge Delivery Service è un servizio componibile offerto da Adobe che consente di creare e distribuire moduli web di forte impatto e dalle prestazioni elevate. Puoi utilizzare il servizio per:</p>
            </section>
            <section class="content-section"></br>
                <h2 style="font-size: 20px; margin-bottom: 10px;">Captivate utenti con moduli straordinari</h2>
                <img src="/help/edge/assets/enrollment-form.png" alt="Modulo di iscrizione" style="float: left; margin: 0 20px 20px 0; width: 30%;">
                <p style="line-height: 1.5;">Crea moduli complessi e coinvolgenti con facilità utilizzando una libreria di componenti predefiniti. È possibile integrare facilmente reCAPTCHA, inviare moduli direttamente alle e-mail e consentire caricamenti di file senza soluzione di continuità in soluzioni di archiviazione sicure come Sharepoint, Azure Storage e Amazon S3. Puoi anche creare componenti di moduli personalizzati per realizzare la tua visione unica.</p>
            </section>
            <section class="content-section"></br>
                <h2 style="font-size: 20px; margin-bottom: 10px;">Crea moduli con punteggio faro perfetto</h2>
                <img src="/help/edge/assets/lighthouse-forms.png" alt="punteggio faro perfetto per i moduli" style="float: right; margin: 20px 0 0 20px; width: 30%;">
                <p style="line-height: 1.5;"> Crea moduli che vengono caricati e riprodotti rapidamente, anche su connessioni Internet lente. I tempi di caricamento più rapidi e l’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento dei moduli e a tassi di conversione migliorati.</p>
            </section>
            <section class="content-section"></br>
                <h2 style="font-size: 20px; margin-bottom: 10px;">Creare esperienze di registrazione digitale con strumenti a tua scelta</h2>
                <img src="/help/edge/assets/edge-delivery-forms-authoring-tools.png" alt="Modulo di iscrizione" style="float: left; margin: 0 20px 20px 0; width: 30%;">
                <p style="line-height: 1.5;">Aumentare l’efficienza di authoring separando le origini di contenuto. È possibile utilizzare sia l’authoring di AEM che l’authoring basato su documenti. Di conseguenza, puoi lavorare con più origini di contenuto sullo stesso sito web e utilizzare gli strumenti di authoring preferiti, come Microsoft Excel, Google Sheets o AEM Editors.</p>
            </section>
        </main>
    </div>


<!-- >
* **Captivate users with stunning forms**: 
Build complex and engaging forms with ease using a library of pre-built components. Easily integrate reCAPTCHA, submit forms directly to email, and allow seamless file uploads to secure storage solutions like Sharepoint, Azure Storage, and Amazon S3. Even create your own custom forms components to bring your unique vision to life. 

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Inizia con le nozioni di base

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Creare un modulo utilizzando i moduli eds" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creare un modulo utilizzando Google Sheets o Microsoft Excel</b>
        </a>
        <p>Crea moduli che vengono caricati e riversati rapidamente e automaticamente sui dispositivi mobili.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Invia modulo" alt="Utilizzare frammenti di modulo in un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Invia modulo a foglio di calcolo</b>
        </a>
        <p>Inviare i moduli direttamente ai fogli di Microsoft Excel o Google.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Applicare stili o temi a un modulo finale" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizzare un tema</b>
        </a>
        <p>Crea un’immagine di marchio coerente applicando lo stesso tema nei moduli.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Aggiungere convalide ai campi modulo" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Applicare le convalide dei campi</b>
        </a>
        <p>Riduci gli errori e le frustrazioni controllando gli input del modulo per la formattazione corretta.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Utilizzare le regole per aggiungere un comportamento dinamico a un modulo" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Utilizzare le regole per aggiungere un comportamento dinamico a un modulo</b>
        </a>
        <p>Riutilizzare frammenti preconfigurati in più moduli.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Tradurre un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Tradurre un modulo</b>
        </a>
        <p>Amplia la portata dei moduli mantenendo i costi sotto controllo.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Aggiungere sezioni ripetibili a un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aggiungere sezioni ripetibili</b>
        </a>
        <p>Creare e aggiungere facilmente sezioni ripetibili a un modulo.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Creare componenti per moduli personalizzati utilizzando JavaScript e CSS standard"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creare componenti personalizzati</b>
        </a>
        <p>Utilizza JavaScript e CSS standard per creare componenti e temi.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Utilizzare reCAPTCHA in un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usa reCAPTCHA</b>
        </a>
        <p>Utilizza l’integrazione OOTB reCAPTCHA per una solida protezione da spam e bot.</p>
    </div>


</div>


</br>









