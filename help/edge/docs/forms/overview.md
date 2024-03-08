---
title: Panoramica dei Edge Delivery Services AEM Forms
description: I Edge Delivery Services AEM Forms sono stati progettati per offrire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# Edge Delivery Services AEM Forms

Semplifica la creazione di moduli e aumenta i tassi di completamento con i Edge Delivery Services AEM Forms di Adobe. Questo servizio potente e componibile consente di creare moduli di livello enterprise con prestazioni eccezionali e un impatto visivo straordinario. L’AEM dà priorità sia all’esperienza utente che agli obiettivi aziendali, garantendo tempi di caricamento estremamente rapidi e un aumento delle conversioni dei moduli.

Puoi utilizzare il servizio per:

* **Creare esperienze di registrazione eccezionali**: crea esperienze di registrazione che consentono di caricare ed eseguire il rendering rapidamente, anche su connessioni Internet lente. I tempi di caricamento più rapidi e l’esperienza utente ottimizzata contribuiscono a tassi più elevati di completamento dei moduli e a tassi di conversione migliorati.

* **Creare esperienze di iscrizione con strumenti a tua scelta**: aumenta l’efficienza dell’authoring disaccoppiando le origini di contenuto. È possibile utilizzare entrambi **authoring basato su documenti** (Microsoft SharePoint o Google Drive) e **Authoring AEM** (Redattori AEM). È quindi possibile utilizzare più origini di contenuto nello stesso modulo e utilizzare gli strumenti di authoring preferiti, ad esempio Microsoft Excel, Google Sheets o Adaptive Forms Editor.

* **Usa set di strumenti intuitivo per gli sviluppatori:** AEM Forms utilizza JavaScript plain HTML, modern CSS e vanilla per creare esperienze eccezionali senza il solito sovraccarico. Qualsiasi sviluppatore con conoscenze di base di HTML, CSS e JS dovrebbe essere in grado di creare i propri componenti e non dovrebbe dover imparare alcun linguaggio o framework specifico. Non è necessario usare alcuna pipeline o attendere, archivia il codice in Github e le modifiche sono live. Inoltre, non è necessario eseguire alcuna pipeline o attendere, archivia il codice in Github e le modifiche sono live.


## Creazione di un’esperienza di registrazione digitale

AEM Forms offre entrambi **authoring basato su documenti** (Microsoft SharePoint o Google Drive) e **Authoring AEM** (Redattori AEM). È possibile utilizzare [Blocco Forms adattivo](/help/edge/docs/forms/create-forms.md) per aggiungere un modulo al sito Edge Delivery Services.


>[!BEGINTABS]

>[!TAB Authoring basato su documenti]

L’authoring basato su documenti è un’opzione versatile, adatta alla creazione di moduli semplici con funzionalità essenziali. Consente di integrare vari tipi di input, come campi di testo, menu a discesa e pulsanti di scelta, per raccogliere i dati utente in modo efficace. Offre una versione di base delle regole per aggiungere un comportamento dinamico ai moduli. Le caratteristiche principali dell&#39;authoring basato su documenti sono:

* **[Componenti campo modulo basati su HTML5](/help/edge/docs/forms/form-components.md)**: i Edge Delivery Services AEM Forms ti consentono di creare moduli interattivi e di facile utilizzo utilizzando componenti modulo basati su HTML 5 [tipi di input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">seleziona</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi</a>  elementi. Questi componenti sono adatti a diversi tipi di raccolta dati e possono essere facilmente personalizzati in base a esigenze specifiche.

* **Accessibilità**: i campi nel blocco del modulo sono accessibili. Ogni etichetta è collegata al rispettivo elemento di input e gli ID vengono generati automaticamente per il collegamento. Le descrizioni associate ai campi sono collegate tramite l’attributo aria-descripedby. È supportata la navigazione tramite tastiera con i tasti standard Tab/Shift + Tab.

* **[Stile](/help/edge/docs/forms/style-theme-forms.md)**: ogni campo modulo ha una struttura HTML fissa che può essere facilmente decorata utilizzando file CSS o JavaScript personalizzati. I selettori per i campi di targeting in CSS e JS vengono forniti in base al tipo e al nome. È possibile creare facilmente nuovi selettori grazie alla struttura e allo stile standardizzati del modulo.

* **Regole di base**: crea facilmente una logica che regola la visibilità, la convalida e il comportamento dei campi in base all’input dell’utente o a condizioni predefinite. Le regole offrono un modo flessibile e intuitivo di aggiungere intelligenza ai moduli, garantendo che si adattino senza problemi in base agli input degli utenti.

* **Convalide**: prima dell’invio, il modulo viene convalidato e i campi non validi vengono contrassegnati in modo appropriato con i messaggi di errore visualizzati all’utente. I blocchi adattivi di Forms supportano tutte le funzioni di convalida dei moduli HTML, supportate dai browser moderni, e forniscono un meccanismo di convalida aggiuntivo, ad esempio script di convalida, dimensioni dei file, tipo di file, dimensioni complessive dei file e altro ancora.

* **Caricamenti di file**: è possibile aggiungere funzionalità di file allegati ai moduli. Per raccogliere documenti, immagini o altri file dagli utenti, la funzionalità di caricamento dei file ti consente di lavorare senza problemi. Con le opzioni di gestione personalizzate disponibili, puoi adattare il processo di caricamento dei file alle tue esigenze specifiche.

* **reCAPTCHA**: integrazione perfetta di Google reCAPTCHA nei moduli con il supporto fornito con il prodotto (OOTB). Proteggi i moduli da attività fraudolente, spam e abusi, mantenendo al contempo un’esperienza utente fluida e ininterrotta. Il blocco Forms adattivo supporta reCaptcha V3 e reCaptcha Enterprise.

* **Invia notifica e-mail all’invio del modulo**: elimina il problema dei follow-up manuali e assicura una comunicazione tempestiva con l’automazione e-mail integrata per l’invio dei moduli. Questa soluzione integrata consente di informare facilmente le parti interessate, incluso l’invio dei dati del modulo, ogni volta che qualcuno compila un modulo sul sito web. Non sono necessari configurazioni complesse o strumenti aggiuntivi, è pronto per l&#39;uso.

>[!TAB Authoring AEM]

L’authoring AEM sfrutta funzionalità aggiuntive oltre all’authoring basato sui documenti, consentendo di creare moduli più complessi e interattivi. Oltre alle funzioni di authoring basato su documenti, l’authoring AEM offre le seguenti funzioni aggiuntive:

* Regole avanzate: consente di definire azioni basate sulla logica all&#39;interno dei moduli. Puoi utilizzare le regole per mostrare o nascondere in modo condizionale le sezioni del modulo, precompilare i campi in base all’input dell’utente ed eseguire varie convalide per garantire l’integrità dei dati.

* Estensibilità lato server: estende le funzionalità dei moduli integrandoli con la logica lato server. Questo consente di eseguire calcoli complessi, interagire con sistemi esterni e automatizzare attività specifiche in base alle azioni degli utenti all’interno del modulo.
* Semplificazione dei flussi di lavoro e della gestione dei dati: sfrutta la potenza dell’AEM per:
   * Progettare moduli facili da usare utilizzando gli editor AEM.
   * Generare un &quot;documento di record&quot; per l&#39;archiviazione sicura e a prova di manomissione dei dati inviati.
   * Semplifica la firma elettronica con Adobe Sign per un’esperienza di firma fluida e sicura.
   * Automatizza i processi aziendali tramite i flussi di lavoro AEM, attivando azioni basate sull’invio di moduli.
   * Integrazione semplificata con varie origini dati, per un flusso e uno scambio di dati senza problemi.

>[!ENDTABS]








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
