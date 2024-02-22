---
title: Panoramica del servizio di distribuzione AEM Forms Edge
description: Il servizio AEM Forms Edge Delivery è stato progettato per garantire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Servizio di consegna AEM Forms Edge {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service è un servizio componibile offerto da Adobe che consente di creare e distribuire moduli web di forte impatto e dalle prestazioni elevate. Puoi utilizzare il servizio per:

* **Artigianato forme visivamente stupefacenti**: unisci le progettazioni blande e taglienti dei cookie e affascina gli utenti con moduli dinamici e moderni che riflettono la tua identità del brand. Sfrutta componenti predefiniti o crea componenti personalizzati per dare vita alla tua visione in modo rapido e semplice.

* **Crea moduli con punteggio faro perfetto**: crea moduli che vengono caricati ed eseguiti rapidamente, anche su connessioni Internet lente. I tempi di caricamento più rapidi e l’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento dei moduli e a tassi di conversione migliorati.

* **Semplificare l’authoring e gli invii**: per creare i moduli utilizza strumenti familiari come Microsoft Excel o Google Sheets anziché gli ambienti di authoring tradizionali. Inviare moduli direttamente a Microsoft Excel o Google Sheets e utilizzarne l&#39;ecosistema per elaborare facilmente i dati inviati.


Questo servizio componibile è scollegato dall’origine dei contenuti e offre la flessibilità necessaria per creare i contenuti, consentendo agli utenti di utilizzare gli strumenti di authoring preferiti.

![Strumenti di creazione di moduli Edge Delivery](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

Per progettare e creare i moduli, i creatori di contenuti possono utilizzare strumenti a loro disposizione, come Microsoft Excel o Google Sheets (authoring basato su documenti), editor JSON o AEM Forms Adaptive Forms editor per la modifica WYSIWYG (progetti AEM Forms).

>[!NOTE]
>
>
> La funzione di modifica WYSIWYG e Cross Walk sono disponibili nel primo programma di adozione. Puoi scrivere a aem-forms-early-adopter-program@adobe.com dal tuo ID e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità.

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
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Aggiungere convalide ai campi modulo" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Applicare le convalide dei campi</b>
        </a>
        <p>Riduci gli errori e le frustrazioni controllando gli input del modulo per la formattazione corretta.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Utilizzare frammenti di modulo in un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creare frammenti di modulo</b>
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
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Applicare stili o temi a un modulo finale" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizzare un tema</b>
        </a>
        <p>Crea un’immagine di marchio coerente applicando lo stesso tema nei moduli.</p>
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
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Invia modulo" alt="Utilizzare frammenti di modulo in un modulo EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Invia modulo a foglio di calcolo</b>
        </a>
        <p>Inviare i moduli direttamente ai fogli di Microsoft Excel o Google.</p>
    </div>
</div>


</br>









