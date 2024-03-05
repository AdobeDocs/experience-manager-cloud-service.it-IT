---
title: Panoramica del servizio di distribuzione AEM Forms Edge
description: Il servizio AEM Forms Edge Delivery è stato progettato per garantire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d63d0f1152d0a23623c197924a44bc6b1e69fb42
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---


# Servizio di consegna AEM Forms Edge

Il servizio AEM Forms Edge Delivery di Adobe semplifica la creazione dei moduli e aumenta i tassi di completamento. Questo servizio potente e componibile consente di creare moduli di livello enterprise con prestazioni eccezionali e un impatto visivo eccezionale. L’AEM dà priorità sia all’esperienza utente che agli obiettivi aziendali, garantendo tempi di caricamento estremamente rapidi e un aumento dei completamenti dei moduli.

Puoi utilizzare il servizio per:

* **Captivate utenti con moduli straordinari**: crea moduli complessi e coinvolgenti con facilità utilizzando una libreria di componenti predefiniti. È possibile integrare facilmente reCAPTCHA, inviare moduli direttamente alle e-mail e consentire caricamenti di file senza soluzione di continuità in soluzioni di archiviazione sicure come Sharepoint, Azure Storage e Amazon S3. Puoi anche creare componenti di moduli personalizzati per realizzare la tua visione unica.

* **Creare esperienze di registrazione digitale con strumenti a tua scelta**: aumenta l’efficienza dell’authoring disaccoppiando le origini di contenuto. È possibile utilizzare sia l’authoring basato su documenti (Microsoft 365 e Google Workspace) che l’authoring AEM (editor AEM). È quindi possibile utilizzare più origini di contenuto nello stesso sito Web e utilizzare gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Google Sheets o Adaptive Forms Editor.

* **Creare moduli con un punteggio perfetto per Lighthouse**: crea moduli che vengono caricati ed eseguiti rapidamente, anche su connessioni Internet lente. I tempi di caricamento più rapidi e l’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento dei moduli e a tassi di conversione migliorati.

  <div>
    <style>
    .image-container {
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container 
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="Funzioni principali di EDS Forms">
    </div>


</div>

<!--

<!--

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
    >[!NOTE]
    >[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Funzioni principali

* **Componenti campo modulo basati su HTML5**: AEM Forms Edge Delivery Service consente di creare moduli interattivi e di facile utilizzo utilizzando componenti modulo basati su HTML5 [tipi di input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">seleziona</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi</a>  elementi. Questi componenti sono adatti a diversi tipi di raccolta dati e possono essere facilmente personalizzati in base a esigenze specifiche.

* **Accessibilità**: i campi nel blocco del modulo sono accessibili. Ogni etichetta è collegata al rispettivo elemento di input e gli ID vengono generati automaticamente per il collegamento. Le descrizioni associate ai campi sono collegate tramite l’attributo aria-descripedby. È supportata la navigazione tramite tastiera con i tasti standard Tab/Shift + Tab.

* **Stile**: ogni campo modulo ha una struttura HTML fissa che può essere facilmente decorata utilizzando file CSS o JavaScript personalizzati. I selettori per i campi di targeting in CSS e JS vengono forniti in base al tipo e al nome. Puoi creare facilmente nuovi selettori grazie alla struttura standardizzata.

* **Regole**: crea facilmente una logica che regola la visibilità, la convalida e il comportamento dei campi in base all’input dell’utente o a condizioni predefinite. Le regole offrono un modo flessibile e intuitivo di aggiungere intelligenza ai moduli, garantendo che si adattino senza problemi in base agli input degli utenti.

* **Convalide**: prima dell’invio, il modulo viene convalidato e i campi non validi vengono contrassegnati in modo appropriato con i messaggi di errore visualizzati all’utente. Sono disponibili vari modelli per la visualizzazione di questi errori.

Su richiesta sono disponibili alcune funzioni avanzate:

* **Caricamenti di file**: è possibile aggiungere funzionalità di file allegati ai moduli. Per raccogliere documenti, immagini o altri file dagli utenti, la funzionalità di caricamento dei file ti consente di lavorare senza problemi. Con le opzioni di gestione personalizzate disponibili, puoi adattare il processo di caricamento dei file alle tue esigenze specifiche.

* **reCAPTCHA**: integrazione perfetta di Google reCAPTCHA nei moduli con il supporto fornito con il prodotto (OOTB). Proteggi i moduli da attività fraudolente, spam e abusi, mantenendo al contempo un’esperienza utente fluida e ininterrotta.

* **Invia notifica e-mail all’invio del modulo**: elimina il problema dei follow-up manuali e assicura una comunicazione tempestiva con l’automazione e-mail integrata per l’invio dei moduli. Questa soluzione integrata consente di informare facilmente le parti interessate, incluso l’invio dei dati del modulo, ogni volta che qualcuno compila un modulo sul sito web. Non sono necessari configurazioni complesse o strumenti aggiuntivi, è pronto per l&#39;uso.


## Blocchi Forms disponibili

Il servizio AEM Forms Edge Delivery offre due tipi di blocchi di moduli per soddisfare esigenze diverse:

* **Blocco Forms di base**: questa è un’opzione versatile, adatta alla creazione di forme semplici con funzionalità essenziali. Consente di integrare vari tipi di input, come campi di testo, menu a discesa e pulsanti di scelta, per raccogliere i dati utente in modo efficace.

* **Blocco Forms adattivo**: questo blocco avanzato sblocca funzionalità aggiuntive rispetto al blocco Forms di base, consentendoti di creare moduli più complessi e interattivi. Ecco una scomposizione delle sue caratteristiche principali:

   * Regole: definire azioni basate sulla logica all&#39;interno dei moduli. Puoi utilizzare le regole per mostrare o nascondere in modo condizionale le sezioni del modulo, precompilare i campi in base all’input dell’utente ed eseguire varie convalide per garantire l’integrità dei dati.

   * Estensibilità lato server: estende le funzionalità dei moduli integrandoli con la logica lato server. Questo consente di eseguire calcoli complessi, interagire con sistemi esterni e automatizzare attività specifiche in base alle azioni degli utenti all’interno del modulo.

   * Cross-Walk: semplificazione dei flussi di lavoro e della gestione dei dati: sfrutta la potenza dell’AEM per:

      * Progettare moduli facili da usare utilizzando gli editor AEM.

      * Generare un &quot;documento di record&quot; per l&#39;archiviazione sicura e a prova di manomissione dei dati inviati.

      * Semplifica la firma elettronica con Adobe Sign per un’esperienza di firma fluida e sicura.

      * Automatizza i processi aziendali tramite i flussi di lavoro AEM, attivando azioni basate sull’invio di moduli.

      * Integrazione semplificata con varie origini dati, per un flusso e uno scambio di dati senza problemi.

  L’utilizzo del blocco Forms adattivo richiede una licenza aggiuntiva.

### Scelta del blocco Forms corretto

La selezione tra i blocchi di Forms di base e adattivi dipende dai requisiti specifici. Se è necessaria una soluzione semplice per la raccolta di informazioni di base sull&#39;utente, il blocco Forms di base è la soluzione ideale. Tuttavia, se i moduli richiedono una logica complessa, la manipolazione dei dati, l’integrazione con sistemi esterni o flussi di lavoro semplificati utilizzando le funzioni AEM e **hai la licenza necessaria**, il blocco Forms adattivo fornisce la potenza e la flessibilità necessarie per raggiungere gli obiettivi.


## Inizia a creare i moduli

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









