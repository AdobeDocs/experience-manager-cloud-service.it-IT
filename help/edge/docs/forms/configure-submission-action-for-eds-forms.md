---
title: Configurare le azioni di invio per AEM Forms con Edge Delivery Services
description: Scopri come configurare le azioni di invio in AEM Forms utilizzando Edge Delivery Services. Scegli tra Servizio di invio moduli e Azione di invio di AEM Publish per gestire i dati del modulo in modo sicuro ed efficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 99%

---

# Configurazione dell’invio dei moduli: dove finiscono i dati?

Dopo che un utente ha fatto clic su **Invia** nel modulo, è necessario indicare a Edge Delivery Services cosa fare con tali dati. Sono disponibili due opzioni principali:

## Metodo 1: utilizzo del servizio di invio moduli di AEM (semplificato)

Questo servizio è ideale per operazioni comuni e semplici, come l’invio di dati a un foglio di calcolo o a un’e-mail.

**Che cos’è e in che modo può aiutare?**

Il [servizio di invio moduli](/help/forms/forms-submission-service.md) è un endpoint ospitato da Adobe. Quando il modulo invia i dati, questo servizio subentra ed esegue un’azione preconfigurata. È progettato per essere facile da configurare. Puoi configurare: invio a fogli di calcolo o e-mail:

* **Invia al foglio di calcolo:** aggiungi automaticamente i dati del modulo inviati come nuova riga in un foglio di Google o in un file di Microsoft Excel (archiviato in OneDrive o SharePoint).
* **Invia e-mail:** invia un’e-mail contenente i dati del modulo a uno o più indirizzi e-mail specificati.

#### Importante: requisiti di configurazione

* **Accesso al foglio di calcolo:** per inviare dati a un foglio di Google o a un file di Excel in OneDrive/SharePoint, l’account del servizio Adobe (spesso `forms@adobe.com`) richiede in genere **l’autorizzazione di modifica** su tale foglio di calcolo specificato.
* **Programma di accesso anticipato:** alcune funzioni di questo servizio, in particolare per i fogli di calcolo, potrebbero far parte di un programma di accesso anticipato. Potrebbe essere necessario richiedere l’accesso inviando un’e-mail a `aem-forms-ea@adobe.com` o compilando un modulo Adobe specifico con i dettagli del progetto. Controlla sempre la documentazione più recente di Adobe.

**Diagramma di flusso del servizio di invio moduli**
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

![Invio moduli](/help/forms/assets/eds-fss.png)

Questo diagramma di flusso mostra come il servizio di invio moduli acquisisce i dati inviati e li inoltra a un foglio di calcolo o a un’e-mail configurati.

## Metodo 2: invio all’istanza AEM Publish (avanzato)

Per esigenze più complesse, [i moduli (in particolare quelli creati con l’editor universale) possono inviare dati direttamente all’istanza di pubblicazione di AEM as a Cloud Service](/help/forms/configure-submit-actions-core-components.md). Questo consente di sfruttare tutta la potenza del back-end di AEM.

**Quando è necessario effettuare l’invio ad AEM Publish?**

* Per attivare flussi di lavoro AEM personalizzati dopo l’invio.
* Per utilizzare il Modello dati modulo AEM (FDM) per l’integrazione con database o altri sistemi aziendali.
* Per connettersi a servizi di terze parti come Marketo, Microsoft Power Automate o Adobe Workfront Fusion.
* Per memorizzare i dati in posizioni specifiche, ad esempio Archiviazione BLOB di Azure o Elenchi/librerie documenti di SharePoint (non solo semplici fogli di calcolo).
* Se disponi di una logica di convalida lato server o elaborazione dati complessa all’interno di AEM.

**Azioni di invio disponibili (Invii AEM Publish)**

* [Inviare a endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Inviare e-mail (utilizzando i servizi di posta di AEM)](/help/forms/configure-submit-action-send-email.md)
* [Inviare mediante il modello di dati modulo (FDM)](/help/forms/configure-data-sources.md)
* [Richiamare un flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md)
* [Inviare a SharePoint (come voci di elenco o documenti)](/help/forms/configure-submit-action-sharepoint.md)
* [Inviare a OneDrive (come documenti)](/help/forms/configure-submit-action-onedrive.md)
* [Inviare ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Inviare a iMicrosoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Inviare a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Invia a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> Anche eseguendo il targeting di un foglio Google/Excel da AEM Publish, sono necessari passaggi di configurazione diversi rispetto al servizio di invio diretto di moduli.

**Diagramma di flusso invio AEM Publish**

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

![Diagramma di flusso invio AEM Publish](/help/forms/assets/eds-aem-publish.png)
Questo diagramma di flusso mostra l’invio di un modulo ad AEM Publish, il quale in seguito gestirà attività di back-end complesse.

### Confronto tra servizio di invio moduli e Invii AEM Publish

| Funzione | Servizio di invio dei moduli | Invii AEM Publish |
| :- | :- | :-- |
| **Ideale per** | Acquisizione semplice dei dati su fogli di calcolo, notifiche e-mail | Flussi di lavoro complessi, integrazioni aziendali, logica personalizzata |
| **Authoring modulo** | Ottimo per moduli basati su documenti; adeguato per moduli UE semplici | Ideale per moduli creati con l’editor universale |
| **Impegno richiesto per la configurazione** | Basso (configurazione spesso semplice) | Più alto (necessita di AEM Publish, Dispatcher, OSGi, configurazione CDN) |
| **Sistema back-end** | Servizio ospitato da Adobe | Istanza di pubblicazione AEM as a Cloud Service |
| **Flessibilità** | Limitato a foglio/e-mail | Molto flessibile e gamma completa di azioni AEM Forms |
| **Esempio** | Dati del modulo di contatto in un foglio Google | Richiesta di prestito che attiva un flusso di lavoro di approvazione AEM |

## Come incorporare i moduli in diversi siti o pagine

Talvolta, si desidera visualizzare un modulo creato e gestito in un’unica posizione (ad esempio, un “sito moduli” centrale) su una pagina o un sito Web diverso.

### Perché incorporare un modulo?

* Hai creato un modulo standard “Contattaci” con l’editor universale che deve essere visualizzato su più pagine di destinazione realizzate con l’authoring basato su documenti.
* Il contenuto principale del sito web è in Authoring di documenti (DA) ed è necessario includere un modulo specializzato.
* Desideri riutilizzare un singolo modulo ben gestito in diversi progetti EDS.

### Funzionamento tecnico dell’incorporamento dei moduli

La pagina in cui desideri visualizzare il modulo (che qui verrà denominata, “pagina host”) conterrà del codice (in genere un blocco o uno script speciale). Quando un utente visita la pagina host, questo codice invia una richiesta all’URL in cui è ospitato il modulo effettivo (qui denominato “sorgente modulo”). La sorgente del modulo in seguito restituisce il proprio HTML, che la pagina host inserisce e visualizza.

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
Questo diagramma mostra la pagina host che recupera l’HTML del modulo dalla relativa sorgente e lo visualizza. L’invio utilizza l’endpoint configurato del modulo originale.

## Configurazione di CORS per moduli incorporati

[CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) è una funzione di sicurezza del browser. Se la pagina host (ad esempio, `site-a.com`) tenta di recuperare un modulo da un dominio diverso (ad esempio, `forms-site-b.com`), il browser ne eseguirà il blocco, a meno che `forms-site-b.com` non lo consenta esplicitamente tramite le intestazioni CORS.

Senza le intestazioni CORS corrette sul **server della sorgente del modulo**, il browser impedisce il caricamento del modulo da parte della pagina host e il modulo incorporato non verrà visualizzato.

### Come configurare CORS sul sito che trasmette il modulo?

È necessario configurare il server che ospita la **sorgente modulo** per inviare intestazioni HTTP specifiche nella risposta. Il metodo esatto dipende dalla configurazione EDS (ad esempio, per i progetti Franklin, questa operazione viene spesso eseguita in un file di configurazione `helix-config.yaml` o simile nell’archivio GitHub che controlla il comportamento della CDN o la logica dell’edge worker).
Intestazioni chiave da aggiungere alle risposte della sorgente del modulo:

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (esempio: `https://your-site.com`). Per il test, è possibile utilizzare `*`, per la produzione, invece, è necessario specificare i domini esatti.
* `Access-Control-Allow-Methods: GET, OPTIONS` (potrebbe essere necessario `POST` se anche l’invio del modulo stesso avviene tra origini diverse, ma in genere le operazioni di invio sono dirette a un endpoint separato, spesso con la stessa origine o configurato in modo specifico).
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

* **Regole CDN:** la rete CDN potrebbe offrire alcune modalità per effettuare il proxy delle richieste. Ad esempio, una richiesta a `host-page.com/embedded-form` potrebbe essere instradata internamente dalla rete CDN per recuperare il contenuto da `form-source.com/actual-form`, facendolo apparire al browser come proveniente dalla stessa origine. Questa configurazione potrebbe risultare complessa.
* **Basi di codice multiple (Helix 4):** se la pagina host e la sorgente del modulo si trovano in archivi GitHub diversi (comuni nelle impostazioni di Helix 4), assicurati che qualsiasi “blocco modulo” JavaScript necessario per il rendering o la gestione del modulo sia disponibile nella base di codice della pagina host o che il modulo HTML recuperato dalla sorgente del modulo sia autonomo con tutti i JavaScript necessari. Nei documenti originali viene indicato che per “helix4 con diverse basi di codice, è necessario aggiungere il blocco del modulo su entrambe le basi di codice”.

### Configurazioni architetturali comuni e passaggi di configurazione

Di seguito sono riportati alcuni modi comuni per configurare i moduli, combinando i metodi di authoring con le strategie di invio, insieme ai punti chiave di configurazione.

#### Modulo basato su documenti con invio di fogli di calcolo/e-mail

Questa è la configurazione più semplice. Creando il modulo in Word/Google Docs, i dati vengono inviati a un foglio di calcolo o a un’e-mail tramite il servizio di invio moduli.

1. Definisci il modulo in un documento/foglio Word/Google utilizzando la struttura di tabella o il blocco di modulo specificato.
1. Nel documento (o nella configurazione correlata), specifica l’URL del foglio di calcolo di destinazione o l’indirizzo e-mail per il servizio di invio moduli.
1. Assicurati che `forms@adobe.com` (o l’account del servizio pertinente) abbia accesso per la modifica al foglio di calcolo di destinazione.
1. Pubblica il documento sul tuo sito Edge Delivery.

**Architettura del servizio di invio basata su documenti + moduli**
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

![Architettura del servizio di invio basata su documenti + moduli](/help/forms/assets/eds-doc-fss.png)

#### Modulo editor universale con invio foglio di calcolo/e-mail

Per creare il modulo viene utilizzato l’editor universale visivo; per l’acquisizione dei dati, viene comunque utilizzato il semplice servizio di invio moduli.

1. Crea il modulo utilizzando l’editor universale in AEM.
1. Configura l’azione di invio del modulo nell’editor universale (UE) per utilizzare l’opzione “Invia al servizio di invio moduli”.
1. Specifica l’URL o l’indirizzo e-mail del foglio di calcolo di destinazione.
1. Se utilizzi i fogli di calcolo, assicurati che `forms@adobe.com` disponga dell’accesso per la modifica.
1. Pubblica la pagina contenente il modulo da AEM sul tuo sito Edge Delivery.

   **Architettura del servizio di invio moduli + editor universale**

   ![Architettura del servizio di invio moduli + editor universale](/help/forms/assets/eds-ue-fss.png)

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

#### Modulo editor universale con invio AEM Publish (avanzato)

Questa configurazione utilizza l’editor universale per la creazione dei moduli e l’istanza AEM Publish per una potente elaborazione back-end (flussi di lavoro, FDM, ecc.). Ciò richiede una maggiore configurazione.

1. **Crea modulo in UE:** crea il modulo nell’editor universale. Configura la relativa azione di invio in modo che punti a un’azione AEM Forms (ad esempio, “Avvia un flusso di lavoro AEM”, “Invia utilizzando il modello dati del modulo”).
1. **Configurazione AEM Dispatcher (a livello di AEM Publish):**
   * **Nessun reindirizzamento:** assicurati che le regole di Dispatcher *non* reindirizzino le richieste effettuate ai `/adobe/forms/af/submit/...` percorsi.
   * **Consenti invii:** modifica i filtri di Dispatcher (ad esempio, in `filters.any`) per `allow` in modo esplicito le richieste POST a `/adobe/forms/af/submit/...` dal dominio o dagli indirizzi IP del sito Edge Delivery.
1. **Filtro referrer OSGi in AEM (nel livello AEM Publish):**
   * Nella console OSGi di AEM (`/system/console/configMgr`), individua e configura il “Filtro referrer Apache Sling”.
   * Aggiungi i domini del tuo sito Edge Delivery (ad esempio, `https://your-eds-domain.hlx.page`, `https://your-custom-eds-domain.com`) all’elenco “Consenti host” o “Consenti host RegExp”. Questo comunica ad AEM di accettare gli invii provenienti dal tuo sito EDS.
1. **Regola di reindirizzamento CDN (sulla rete CDN di Edge Delivery):**
   * Il sito Edge Delivery (ad esempio, `your-eds-domain.hlx.page`) deve indirizzare correttamente le richieste di invio all’istanza AEM Publish.
   * Quando il modulo nella pagina EDS viene inviato, potrebbe essere destinato a un percorso relativo come `/adobe/forms/af/submit/...`. È necessaria una regola sul CDN di Edge Delivery (o edge worker) che dica: “Se una richiesta arriva a `your-eds-domain.hlx.page/adobe/forms/af/submit/...`, inoltrala (tramite proxy o reindirizzmento) a `your-aem-publish-instance.com/adobe/forms/af/submit/...`”.
   * L’implementazione esatta dipende dal provider CDN (ad esempio, Fastly VCL, Akamai Property Manager, Cloudflare Workers).
1. **(Facoltativo) `constants.js` per lo sviluppo (nella base di codice del progetto EDS):**
   * Per lo sviluppo locale o se gli script dei moduli lato client devono conoscere l’URL completo di AEM Publish, puoi configurarlo in un file di configurazione `constants.js` o simile nell’archivio GitHub del progetto Edge Delivery. Esempio:

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **Pubblicazione:** pubblica la pagina del modulo da AEM a EDS e assicurati che tutte le configurazioni di AEM siano attive nell’istanza AEM Publish.

   **Editor universale + Architettura AEM Publish**

![Editor universale + Architettura AEM Publish](/help/forms/assets/eds-aem-publish.png)

Questo mostra il flusso: l’utente invia sul sito EDS, CDN invia ad AEM Dispatcher, quindi AEM Publish lo elabora.

#### Incorporamento di un modulo in una pagina di Authoring di documenti (DA)

Il contenuto del sito web principale viene creato in Authoring di documenti (DA). Il modulo viene creato separatamente utilizzando l’authoring basato su documenti o l’editor universale, in seguito incorporandolo nella pagina DA.

1. **Crea e pubblica il modulo:**
   * Per creare il modulo, utilizza l’authoring basato sui documenti O l’editor universale.
   * Configura il relativo metodo di invio (al servizio di invio dei moduli o AEM Publish, come da configurazione 1, 2 o 3).
   * Pubblica questo modulo in modo che sia attivo sul proprio URL di Edge Delivery (ad esempio, `.../forms/my-special-form`).
1. **Configura CORS:** nel sito/progetto Edge Delivery che ospita questo modulo autonomo, verifica che le intestazioni CORS siano configurate in modo da consentire al dominio del sito di authoring dei documenti di recuperarlo.
1. **Crea pagina in DA:** crea o modifica la pagina in Authoring documenti.
1. **Incorpora blocco modulo:** utilizza il blocco appropriato in DA per incorporare un URL esterno. Punta questo blocco all’URL del modulo autonomo pubblicato.
1. **Pubblica pagina DA:** pubblica la pagina DA. Ora recupera e visualizza il modulo.

   **Moduli incorporati nell’architettura DA**

   ![Moduli incorporati nell’architettura DA](/help/forms/assets/eds-forms-embedd-da.png)

   Mostra una pagina DA che estrae un modulo da un’altra posizione EDS. Il modulo incorporato gestisce il proprio invio.

## Risoluzione di problemi

* **L’invio del modulo non funziona.**
   * **Controlla errori console:** apri la console di sviluppo del browser (di solito F12) e cerca gli errori nella scheda Rete o Console al momento dell’invio.
   * **Verifica l’URL di invio:** il modulo sta tentando di inviare all’endpoint corretto (URL del servizio di invio moduli o percorso di AEM Publish)?
   * **Servizio di invio moduli:** se si invia a un foglio di calcolo, è stato concesso l’accesso di modifica a `forms@adobe.com`? L’URL del foglio di calcolo è corretto?
   * **Invii AEM Publish:**
      * Il Dispatcher consente ai POST di `/adobe/forms/af/submit/...`?
      * Il filtro Sling Referrer su AEM Publish è configurato per consentire il dominio EDS?
      * Le regole di reindirizzamento CDN per `/adobe/forms/af/submit/...` funzionano correttamente?

* **Il modulo incorporato non viene visualizzato.**

   * **CORS!** Questo è il motivo più comune. Controlla la console del browser per individuare eventuali errori CORS. Assicurati che il sito *che ospita* il modulo contenga le intestazioni `Access-Control-Allow-Origin` corrette.
   * **URL del modulo corretto?** Il codice da incorporare nella pagina host punta all’URL live corretto del modulo?
   * **Blocchi JavaScript:** se il modulo dipende da uno specifico “blocco modulo” JavaScript per il rendering, il codice di tale blocco è disponibile nella pagina host?

* **Ricevo un messaggio “403 Forbidden” o “401 Unauthorized” quando invio ad AEM Publish.**

   * Questo spesso indica che il filtro Sling Referrer su AEM Publish non consente le richieste dal dominio EDS. Ricontrolla la configurazione.
   * Potrebbe anche trattarsi di un problema di autenticazione/autorizzazione se l’endpoint di invio AEM lo richiede, anche se gli invii dei moduli standard sono in genere anonimi.

## Passaggi successivi

Questa guida ha fornito una panoramica sull’utilizzo dei moduli con AEM Edge Delivery Services. Per istruzioni più dettagliate, passo dopo passo, su configurazioni specifiche, fai riferimento alla documentazione ufficiale di Adobe Experience Manager:

* [Authoring basato su documenti con moduli Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [Editor universale con moduli Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Authoring di documenti (DA) e incorporamento di contenuti](https://www.aem.live/developer/da-tutorial)
* [Servizio di invio dei moduli AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
