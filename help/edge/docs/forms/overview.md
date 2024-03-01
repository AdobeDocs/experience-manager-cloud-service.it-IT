---
title: Panoramica di AEM Forms Edge Delivery Service
description: AEM Forms Edge Delivery Service progettato per garantire prestazioni ottimali, consentendoti di immaginare il futuro di raccolta dati semplificati e di utente coinvolgimento.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1c6e44fd6652d93ba73bc2eb3604cd08eae7a33c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---


# Servizio AEM Forms Edge Delivery

Semplifica la creazione di moduli e dare impulso a tassi di completamento più elevati con il servizio AEM Forms Edge Delivery di Adobe Systems. Questo servizio potente e componibile ti consente di versione moduli di livello aziendale con prestazioni e appeal visivo eccezionali. AEM dà priorità sia al esperienza di utilizzo che agli obiettivi aziendali, garantendo tempi di caricamento fulminei e maggiori completamenti dei moduli.

Puoi utilizzare il servizio per:

* **Affascina gli utenti con forme** straordinarie: crea moduli complessi e coinvolgenti con facilità utilizzando una libreria di predefinito componenti. Integra facilmente reCAPTCHA, invia i moduli direttamente alla posta elettronica e consenti di caricare facilmente i file in soluzioni di archiviazione sicure like Sharepoint, Archiviazione di Azure e Amazon S3. Puoi persino creare componenti personalizzati per i moduli per dare vita alla tua visione unica.

* **Crea le esperienze di registrazione digitale con gli strumenti che preferisci**: aumenta l&#39;efficienza della creazione disaccoppiando contenuto origini. È possibile utilizzare sia l&#39;authoring basato su documenti (Microsoft 365 e Google Area di lavoro) che l&#39;authoring AEM (AEM Editors). Pertanto, puoi lavorare con più origini contenuto sullo stesso sito Web e utilizzare i tuoi strumenti di authoring preferiti, come Microsoft Excel, Fogli Google o Adaptive Forms Editor.

* **Crea moduli con un punteggio** Lighthouse perfetto: crea moduli che vengono caricati e renderizzati rapidamente, lineare su connessioni Internet lente. Tempi di caricamento più rapidi e esperienza di utilizzo ottimizzati contribuiscono a tassi di completamento dei moduli più elevati e tassi di conversione migliorati.

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 70%; /* Set image width to 70% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms Caratteristiche principali">
    </div>


</div>
&lt;!-- &gt;
* **Affascina gli utenti con forme straordinarie**: 
Crea moduli complessi e coinvolgenti con facilità utilizzando una libreria di componenti predefinito. Integra facilmente reCAPTCHA, invia i moduli direttamente alla posta elettronica e consenti di caricare facilmente i file in soluzioni di archiviazione sicure like Sharepoint, Archiviazione di Azure e Amazon S3. Puoi persino creare componenti personalizzati per i moduli per dare vita alla tua visione unica.

    ![Moduli di iscrizione] (/help/edge/risorse/enrollment-form.png)

* **Crea moduli con punteggio** lighthouse perfetto: crea moduli che vengono caricati e renderizzati rapidamente, lineare su connessioni Internet lente. Tempi di caricamento più rapidi e esperienza di utilizzo ottimizzati contribuiscono a tassi di completamento dei moduli più elevati e tassi di conversione migliorati.

  ![Punteggio Lighthouse perfetto per i tuoi moduli](/help/edge/assets/lighthouse-forms.png)

* **Crea le esperienze di registrazione digitale con gli strumenti che preferisci**: aumenta l&#39;efficienza della creazione disaccoppiando contenuto origini. È possibile utilizzare sia l’authoring di AEM che l’authoring basato su documenti. Pertanto, puoi lavorare con più origini contenuto sullo stesso sito Web e utilizzare i tuoi strumenti di authoring preferiti, come Microsoft Excel, Fogli Google o AEM Editor.

  ![Strumenti di creazione dei moduli di consegna Edge](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Inizia creazione di moduli

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Crea un modulo utilizzando i moduli EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Crea un modulo utilizzando Fogli Google o Microsoft Excel
            </b>
        </a>
        <p>Crea moduli che vengono caricati ed eseguiti il rendering vengono ridisposti rapidamente e automaticamente sui dispositivi mobili.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Invia modulo" alt="Uso di frammenti di modulo in un modulo EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Invia modulo a foglio di calcolo
            </b>
        </a>
        <p>Invia i moduli direttamente a Microsoft Excel o Fogli Google.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Applica di stili o temi in un modulo EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Personalizzare un tema
            </b>
        </a>
        <p>Crea un'immagine marchio coerente applicando lo stesso tema ai moduli.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Aggiunta di convalide ai campi del modulo" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Applica convalide dei campi
            </b>
        </a>
        <p>Riduci gli errori e la frustrazione controllando la corretta formattazione degli input del modulo.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Utilizzare regole per aggiungere un comportamento dinamico a un modulo" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Utilizzare regole per aggiungere un comportamento dinamico a un modulo
            </b>
        </a>
        <p>Riutilizzare frammenti preconfigurati in più moduli.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Tradurre un modulo EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Tradurre un modulo
            </b>
        </a>
        <p>Estendi la portata dei tuoi moduli mantenendo sotto controllo i costi.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Aggiunta di sezioni ripetibili a un modulo EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Aggiungi sezioni ripetibili
            </b>
        </a>
        <p>Crea e aggiungi facilmente sezioni ripetibili a un modulo.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Crea di componenti per moduli personalizzati utilizzando JavaScript standard e CSS"  style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Crea di componenti personalizzati
            </b>
        </a>
        <p>Utilizza JavaScript standard e CSS per creare componenti e temi.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Utilizzare reCAPTCHA in un modulo EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Utilizza reCAPTCHA
            </b>
        </a>
        <p>Utilizza l'integrazione OOTB reCAPTCHA per una solida protezione da spam e bot.</p>
    </div>


</div>


</br>









