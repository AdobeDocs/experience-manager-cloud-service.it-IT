---
title: Configurare le azioni di invio per AEM Forms con Edge Delivery Services
description: Scopri come configurare le azioni di invio in AEM Forms utilizzando Edge Delivery Services. Scegli tra Servizio di invio Forms e Azione di invio pubblicazione AEM per gestire i dati del modulo in modo sicuro ed efficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# Configurazione Dell’Invio Del Modulo: Dove Arrivano I Dati?

Dopo che un utente ha fatto clic su **invia** nel modulo, è necessario indicare a Edge Delivery Services cosa fare con tali dati. Sono disponibili due opzioni principali:

## Metodo 1: utilizzo del servizio di invio AEM Forms (semplificato)

Questo servizio è ideale per azioni comuni e semplici, come l’invio di dati a un foglio di calcolo o a un’e-mail.

**Che cos&#39;è e come può aiutarti?**

Il [servizio di invio Forms](/help/forms/forms-submission-service.md) è un endpoint ospitato da Adobe. Quando il modulo invia i dati, questo servizio subentra ed esegue un&#39;azione preconfigurata. È progettato per essere facile da configurare. Puoi configurare: Invio a fogli di calcolo o e-mail:

* **Invia al foglio di calcolo:** Aggiungi automaticamente i dati del modulo inviati come nuova riga in un foglio di Google o in un file di Microsoft Excel (archiviato in OneDrive o SharePoint).
* **Invia e-mail:** Invia un messaggio e-mail contenente i dati del modulo a uno o più indirizzi e-mail specificati.

#### Importante: requisiti di configurazione

* **Accesso al foglio di calcolo:** Per inviare dati a un foglio di Google o a un file di Excel in OneDrive/SharePoint, l&#39;account del servizio Adobe (spesso `forms@adobe.com`) richiede in genere **l&#39;autorizzazione di modifica** per il foglio di calcolo specifico.
* **Programma di accesso anticipato:** Alcune funzionalità di questo servizio, in particolare per i fogli di calcolo, potrebbero far parte di un programma di accesso anticipato. Potrebbe essere necessario richiedere l&#39;accesso inviando un&#39;e-mail a `aem-forms-ea@adobe.com` o compilando un modulo Adobe specifico con i dettagli del progetto. Controlla sempre la documentazione più recente di Adobe.

**Diagramma di flusso del servizio di invio Forms**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->

![Invio Forms](/help/forms/assets/eds-fss.png)

Questo diagramma di flusso mostra come il servizio di invio Forms accetta i dati inviati e li invia a un foglio di calcolo o a un messaggio e-mail configurato.

## Metodo 2: invio all’istanza Publish di AEM (avanzato)

Per esigenze più complesse, [i moduli (in particolare quelli creati con Universal Editor) possono inviare dati direttamente all&#39;istanza Publish di AEM as a Cloud Service](/help/forms/configure-submit-actions-core-components.md). Questo consente di sfruttare tutta la potenza del back-end di AEM.

**Quando devi inviare la pubblicazione ad AEM?**

* Per attivare flussi di lavoro AEM personalizzati dopo l’invio.
* Utilizzare AEM Form Data Model (FDM) per l&#39;integrazione con database o altri sistemi aziendali.
* Per connettersi a servizi di terze parti come Marketo, Microsoft Power Automate o Adobe Workfront Fusion.
* Per memorizzare i dati in posizioni specifiche, ad esempio Archiviazione BLOB di Azure o Elenchi/raccolte documenti di SharePoint (non solo semplici fogli di calcolo).
* Se disponi di una logica di convalida lato server o elaborazione dati complessa all’interno di AEM.

**Azioni di invio disponibili (AEM Publish Submissions)**

* [Invia a un endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Inviare e-mail (utilizzando i servizi di posta di AEM)](/help/forms/configure-submit-action-send-email.md)
* [Invia utilizzando il modello dati modulo (FDM)](/help/forms/configure-data-sources.md)
* [Richiama un flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md)
* [Invia a SharePoint (come voci di elenco o documenti)](/help/forms/configure-submit-action-sharepoint.md)
* [Invia a OneDrive (come documenti)](/help/forms/configure-submit-action-onedrive.md)
* [Invia ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Invia a Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Invia ad Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Invia a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> Anche se si esegue il targeting di un foglio Google/Excel da AEM Publish, sono necessari passaggi di configurazione diversi rispetto al servizio di invio diretto di Forms.

**Diagramma di flusso invio pubblicazione AEM**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![Diagramma di flusso invio pubblicazione AEM](/help/forms/assets/eds-aem-publish.png)
Questo diagramma di flusso mostra un modulo che viene inviato ad AEM Publish, che quindi gestisce attività di back-end complesse.

### Confronto tra il servizio di invio Forms e il servizio di pubblicazione AEM

| Funzione | Servizio di invio Forms | Invii di pubblicazione AEM |
| :- | :- | :-- |
| **Ideale per** | Acquisizione semplice dei dati su fogli di calcolo, notifiche e-mail | Flussi di lavoro complessi, integrazioni aziendali, logica personalizzata |
| **Authoring modulo** | Ideale per moduli basati su documenti; OK per moduli UE semplici | Ideale per moduli creati con Universal Editor |
| **Impegno di installazione** | Bassa (configurazione spesso semplice) | Più alto (richiede AEM Publish, Dispatcher, OSGi, CDN setup) |
| **Sistema back-end** | Servizio ospitato da Adobe | Istanza di pubblicazione AEM as a Cloud Service |
| **Flessibilità** | Limitato a foglio/e-mail | Gamma completa e molto flessibile di azioni AEM Forms |
| **Esempio** | Contattare i dati del modulo in un foglio Google | Applicazione di prestito che attiva un flusso di lavoro di approvazione AEM |

## Come incorporare Forms in diversi siti o pagine

Talvolta è necessario visualizzare un modulo creato e gestito in un&#39;unica posizione (ad esempio, un &quot;sito moduli&quot; centrale) su una pagina o un sito Web diverso.

### Perché incorporare un modulo?

* Hai creato un modulo standard &quot;Contattaci&quot; con Universal Editor che deve essere visualizzato su più pagine di destinazione create con Authoring basato su documenti.
* Il contenuto principale del sito web è in Document Authoring (DA) ed è necessario includere un modulo specializzato.
* Si desidera riutilizzare un singolo modulo ben gestito in diversi progetti EDS.

### Funzionamento tecnico dell’incorporamento di moduli

La pagina in cui vuoi visualizzare il modulo (chiamiamolo &quot;Pagina host&quot;) conterrà del codice (in genere un blocco o uno script speciale). Quando un utente visita la pagina host, questo codice invia una richiesta all’URL in cui è ospitato il modulo effettivo (chiamiamolo &quot;Form Source&quot;). Il Source del modulo quindi invia nuovamente il proprio HTML, che la pagina host inserisce e visualizza.

**Architettura modulo incorporato**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->

![Architettura modulo incorporato](/help/forms/assets/eds-embedded-form.png)
Questo diagramma mostra la pagina host che recupera da HTML Form Source e la visualizza. L’invio utilizza l’endpoint configurato del modulo originale.

## Configurazione di CORS per Embedded Forms

[CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) è una funzionalità di sicurezza del browser. Se la pagina host (ad esempio, `site-a.com`) tenta di recuperare un modulo da un dominio diverso (ad esempio, `forms-site-b.com`), il browser lo bloccherà a meno che `forms-site-b.com` non lo consenta esplicitamente tramite le intestazioni CORS.

Senza le intestazioni CORS corrette sul server **Source Form**, il browser impedisce il caricamento del modulo da parte della pagina host e il modulo incorporato non verrà visualizzato.

### Come si configura CORS sul sito che trasmette il modulo?

È necessario configurare il server che ospita il **Source** modulo per inviare intestazioni HTTP specifiche nella risposta. Il metodo esatto dipende dalla configurazione EDS (ad esempio, per i progetti Franklin, questa operazione viene spesso eseguita in un file di configurazione `helix-config.yaml` o simile nell&#39;archivio GitHub che controlla il comportamento CDN o la logica di lavoro Edge).
Intestazioni chiave da aggiungere alle risposte di Source per moduli:

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (esempio: `https://your-site.com`). Per il test, è possibile utilizzare `*`, ma per la produzione, specificare i domini esatti.
* `Access-Control-Allow-Methods: GET, OPTIONS` (potrebbe essere necessario `POST` se l&#39;invio del modulo stesso è anche tra origini diverse, ma in genere gli invii vanno a un endpoint separato, spesso con la stessa origine o configurato in modo specifico).
* `Access-Control-Allow-Headers: Content-Type` (e qualsiasi altra intestazione personalizzata utilizzata dal recupero del modulo).

**Esempio (concettuale per un file di configurazione):**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## Considerazioni aggiuntive: CDN e basi di codice multiple (Helix 4)

* **Regole CDN:** La rete CDN potrebbe offrire modi per inoltrare le richieste. Ad esempio, una richiesta a `host-page.com/embedded-form` potrebbe essere instradata internamente dalla rete CDN per recuperare il contenuto da `form-source.com/actual-form`, facendolo apparire come se fosse della stessa origine nel browser. L&#39;impostazione può essere complessa.
* **Più codebase (Helix 4):** Se la pagina host e il Source del modulo si trovano in archivi GitHub diversi (comuni nelle impostazioni di Helix 4), assicurati che qualsiasi &quot;blocco modulo&quot; JavaScript necessario per il rendering o la gestione del modulo sia disponibile nella base di codice della pagina host o che il modulo HTML recuperato dal Source del modulo sia autonomo con tutti i JavaScript necessari. Nei documenti originali viene indicato che per &quot;helix4 con diverse basi di codice, è necessario aggiungere il blocco Form su entrambe le basi di codice&quot;.

### Impostazioni architetturali comuni e passaggi di configurazione

Di seguito sono riportati alcuni modi comuni per configurare i moduli, combinando i metodi di authoring con le strategie di invio e i punti chiave di configurazione.

#### Modulo basato su documenti con invio di fogli di calcolo/e-mail

Questa è la configurazione più semplice. Il modulo viene creato in Word/Google Docs e i dati vengono inviati a un foglio di calcolo o a un messaggio di posta elettronica tramite il servizio di invio di Forms.

1. Definire il modulo in un documento/foglio Word/Google utilizzando la struttura di tabella o il blocco di modulo specificato.
1. Nel documento (o nella configurazione correlata), specifica l’URL del foglio di calcolo di destinazione o l’indirizzo e-mail per il servizio di invio di Forms.
1. Assicurati che `forms@adobe.com` (o l&#39;account del servizio pertinente) abbia accesso in modifica al tuo foglio di calcolo di destinazione.
1. Pubblica il documento sul tuo sito Edge Delivery.

**Architettura del servizio di invio basata su documenti + Forms**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![Architettura del servizio di invio basata su documenti + Forms](/help/forms/assets/eds-doc-fss.png)

#### Modulo editor universale con invio foglio di calcolo/e-mail

Per creare il modulo si utilizza l&#39;editor universale visivo, ma il semplice servizio di invio Forms per l&#39;acquisizione dei dati viene comunque utilizzato.

1. Crea il modulo utilizzando l’Editor universale in AEM.
1. Configurare l&#39;azione di invio del modulo nell&#39;UE per utilizzare l&#39;opzione &quot;Invia a Forms Submission Service&quot;.
1. Specifica l’URL o l’indirizzo e-mail del foglio di calcolo di destinazione.
1. Se si utilizzano fogli di calcolo, assicurarsi che `forms@adobe.com` disponga dell&#39;accesso di modifica.
1. Pubblica la pagina contenente il modulo da AEM sul tuo sito Edge Delivery.

   **Architettura Universal Editor + Forms Submission Service**

   ![Architettura Universal Editor + Forms Submission Service](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### Modulo editor universale con invio pubblicazione AEM (avanzato)

Questa configurazione utilizza l’Editor universale per la creazione dei moduli e l’istanza di pubblicazione di AEM per una potente elaborazione back-end (flussi di lavoro, FDM, ecc.). Questo richiede una configurazione maggiore.

1. **Crea modulo in UE:** Crea il modulo nell&#39;editor universale. Configura la relativa azione di invio in modo che punti a un’azione AEM Forms (ad esempio, &quot;Richiama un flusso di lavoro AEM&quot;, &quot;Invia utilizzando il modello dati del modulo&quot;).
1. **Configurazione AEM Dispatcher (nel livello di pubblicazione AEM):**
   * **Nessun reindirizzamento:** Assicurarsi che le regole di Dispatcher eseguano *non* richieste di reindirizzamento a `/adobe/forms/af/submit/...` percorsi.
   * **Consenti invii:** Modifica i filtri di Dispatcher (ad esempio, in `filters.any`) per `allow` in modo esplicito le richieste POST a `/adobe/forms/af/submit/...` dal dominio o dagli indirizzi IP del sito Edge Delivery.
1. **Filtro referrer OSGi in AEM (nel livello di pubblicazione AEM):**
   * Nella console OSGi di AEM (`/system/console/configMgr`), individua e configura il &quot;Filtro referrer Apache Sling&quot;.
   * Aggiungi i domini del tuo sito Edge Delivery (ad esempio, `https://your-eds-domain.hlx.page`, `https://your-custom-eds-domain.com`) all&#39;elenco &quot;Consenti host&quot; o &quot;Consenti host RegExp&quot;. Questo comunica ad AEM di accettare gli invii provenienti dal tuo sito EDS.
1. **Regola di reindirizzamento CDN (sulla rete CDN di Edge Delivery):**
   * Il sito Edge Delivery (ad esempio, `your-eds-domain.hlx.page`) deve indirizzare correttamente le richieste di invio all&#39;istanza AEM Publish.
   * Quando il modulo nella pagina EDS viene inviato, potrebbe essere destinato a un percorso relativo come `/adobe/forms/af/submit/...`. È necessaria una regola sulla tua rete CDN di Edge Delivery (o lavoratore perimetrale) che dica: &quot;Se una richiesta arriva a `your-eds-domain.hlx.page/adobe/forms/af/submit/...`, inoltrala (proxy o reindirizzala) a `your-aem-publish-instance.com/adobe/forms/af/submit/...`.&quot;
   * L’implementazione esatta dipende dal provider CDN (ad esempio, Fastly VCL, Akamai Property Manager, Cloud Workers).
1. **(Facoltativo) `constants.js` per lo sviluppo (nel codebase del progetto EDS):**
   * Per lo sviluppo locale o se gli script dei moduli lato client devono conoscere l&#39;URL di pubblicazione completo di AEM, puoi configurarlo in un file di configurazione `constants.js` o simile nell&#39;archivio GitHub del progetto Edge Delivery. Esempio:

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **Pubblicazione:** Pubblica la pagina del modulo da AEM a EDS e assicurati che tutte le configurazioni di AEM siano attive nell&#39;istanza di pubblicazione AEM.

   **Editor universale + Architettura di pubblicazione AEM**

![Editor universale + Architettura di pubblicazione AEM](/help/forms/assets/eds-aem-publish.png)

Questo mostra il flusso: l’utente invia sul sito EDS, CDN invia ad AEM Dispatcher, quindi AEM Publish lo elabora.

#### Incorporazione di un modulo in una pagina di authoring dei documenti (DA)

Il contenuto del sito web principale viene creato in Document Authoring (DA). Il modulo viene creato separatamente utilizzando l’authoring basato su documenti o Universal Editor, quindi incorporato nella pagina DA.

1. **Crea e pubblica il modulo:**
   * Per creare il modulo, utilizzare l&#39;authoring basato su documenti O l&#39;editor universale.
   * Configura il relativo metodo di invio (a Forms Submission Service o AEM Publish, come da configurazione 1, 2 o 3).
   * Pubblica questo modulo in modo che sia attivo sul proprio URL Edge Delivery (ad esempio, `.../forms/my-special-form`).
1. **Configura CORS:** Nel sito/progetto Edge Delivery che ospita questo modulo autonomo, verificare che le intestazioni CORS siano configurate in modo da consentire al dominio del sito di authoring documenti di recuperarlo.
1. **Crea pagina in DA:** Crea o modifica la pagina in Authoring documenti.
1. **Incorpora blocco modulo:** Utilizza il blocco appropriato in DA per incorporare un URL esterno. Posizionare il puntatore del mouse sull&#39;URL del modulo pubblicato autonomo.
1. **Pubblica pagina DA:** Pubblica la pagina DA. Ora recupera e visualizza il modulo.

   **Forms incorporato nell&#39;architettura DA**

   ![Forms incorporato nell&#39;architettura DA](/help/forms/assets/eds-forms-embedd-da.png)

   Mostra una pagina DA che estrae un modulo da un&#39;altra posizione EDS. Il modulo incorporato gestisce i propri invii.

## Risoluzione dei problemi

* **L&#39;invio del modulo non funziona.**
   * **Controlla errori console:** Apri la console per sviluppatori del browser (in genere F12) e cerca gli errori nella scheda Rete o Console al momento dell&#39;invio.
   * **Verificare l&#39;URL di invio:** Il modulo sta tentando di inviare all&#39;endpoint corretto (URL del servizio di invio Forms o percorso di pubblicazione AEM)?
   * **Servizio di invio Forms:** Se si invia a un foglio di calcolo, a `forms@adobe.com` è stato concesso l&#39;accesso di modifica? L’URL del foglio di calcolo è corretto?
   * **Invii pubblicazione AEM:**
      * Il tuo Dispatcher consente ai POST di `/adobe/forms/af/submit/...`?
      * Il filtro Sling Referrer su AEM Publish è configurato per consentire il dominio EDS?
      * Le regole di reindirizzamento CDN per `/adobe/forms/af/submit/...` funzionano correttamente?

* **Il modulo incorporato non è visualizzato.**

   * **CORS!** Questo è il motivo più comune. Controlla la console del browser per individuare eventuali errori CORS. Verificare che il sito *hosting* del modulo contenga le `Access-Control-Allow-Origin` intestazioni corrette.
   * **URL modulo corretto?** Il codice di incorporamento nella pagina host punta all&#39;URL live corretto del modulo?
   * **Blocchi di JavaScript:** se il modulo si basa su un &quot;blocco di modulo&quot; JavaScript specifico per il rendering, il codice di tale blocco è disponibile nella pagina host?

* **Ricevo un messaggio &quot;403 Forbidden&quot; o &quot;401 Unauthorized&quot; quando invii ad AEM Publish.**

   * Questo spesso fa riferimento al filtro Sling Referrer sulla pubblicazione AEM che non consente le richieste dal dominio EDS. Ricontrolla la configurazione.
   * Potrebbe anche trattarsi di un problema di autenticazione/autorizzazione se l’endpoint di invio AEM lo richiede, anche se gli invii dei moduli standard sono in genere anonimi.

## Passaggi successivi

Questa guida offre una panoramica dell’utilizzo dei moduli con AEM Edge Delivery Services. Per istruzioni dettagliate su configurazioni specifiche, consulta la documentazione ufficiale di Adobe Experience Manager:

* [Authoring basato su documenti con Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universale con Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Authoring di documenti (DA) e incorporamento di contenuti](https://www.aem.live/developer/da-tutorial)
* [Servizio di invio AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)