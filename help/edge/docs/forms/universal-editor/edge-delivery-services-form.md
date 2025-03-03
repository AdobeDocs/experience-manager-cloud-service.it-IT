---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: 320ab86bc73e874705d985b927e90eec3cad1cf9
workflow-type: ht
source-wordcount: '1040'
ht-degree: 100%

---


# Moduli di Edge Delivery Services

I moduli di Adobe Edge Delivery Services trasformano il modo in cui i moduli vengono creati, eseguiti ed elaborati. Sfruttando Edge Delivery Services, le organizzazioni possono creare moduli digitali veloci, sicuri e altamente disponibili, migliorando l’esperienza utente e l’efficienza operativa con un ambiente di sviluppo rapido. Con i moduli di Edge Delivery Services puoi aumentare le conversioni, ridurre i costi e accelerare la distribuzione dei contenuti.

## Vantaggi dei moduli di Edge Delivery Services

* **Creazione di moduli più rapida**: crea moduli ad alte prestazioni con un punteggio Lighthouse perfetto e monitora continuamente le prestazioni reali utilizzando il Monitoraggio degli utenti reali (RUM).

* **Processo di authoring semplificato**: gestione semplificata dei contenuti da più origini per una maggiore flessibilità. In modalità predefinita puoi creare moduli con authoring WYSIWYG e basato su documenti, consentendo l’integrazione perfetta di vari formati di contenuto.

* **Facilità d’uso per utenti non tecnici**: Edge Delivery Services consente ai non programmatori di gestire e pubblicare facilmente i moduli senza richiedere una conoscenza approfondita della programmazione.

* **Esperienza utente migliorata**: garantisce tempi di caricamento rapidi e interazioni semplici, offrendo agli utenti tempi di attesa minimi e un’esperienza di compilazione dei moduli intuitiva.

* **Esecuzione senza server**: Edge Delivery Services abilita l’esecuzione senza server della logica del modulo. Ciò include:

   * **Convalida lato client**: la convalida del campo modulo viene eseguita lato client, riducendo i ritardi del ciclo.

   * **Precompilazione e personalizzazione**: la precompilazione dei dati del modulo viene gestita lato client per garantire un’esperienza utente ottimale.

   * **Elaborazione dell’invio**: gli invii dei moduli vengono convalidati e inoltrati in modo sicuro senza server centrale

## Come funzionano i moduli Edge Delivery Services?

Gli utenti possono lavorare sui moduli di Edge Delivery Services utilizzando strumenti di authoring basati su documento come Google Drive, SharePoint o l’editor universale (authoring WYSIWYG), sfruttando lo stile, il comportamento e i componenti di base disponibili nell’archivio GitHub. Terminato l’authoring, i moduli Edge Delivery Services possono inviare dati a qualsiasi piattaforma utilizzando il servizio di invio dei moduli.

![Funzionamento dei moduli di Edge Delivery Services](/help/edge/docs/forms/assets/eds-forms-working.png)

### Componenti chiave dei moduli di Edge Delivery Services

I componenti chiave dei moduli di Edge Delivery Services:

* **Archivio GitHub**: l’archivio GitHub funge da standard per la creazione di moduli di Edge Delivery Services. I moduli sfruttano lo stile e le funzionalità di base dell’archivio e consentono agli utenti di aggiungere personalizzazioni e componenti personalizzati ai moduli di Edge Delivery Services.

* **Authoring dei moduli**: i moduli di Edge Delivery Services supportano due tipi di authoring: l’authoring WYSIWYG e basato su documenti. L’authoring basato su documenti consente agli utenti di creare moduli utilizzando strumenti familiari come Documenti Google e Microsoft Office. L’authoring WYSIWYG consente agli utenti di progettare i moduli visivamente utilizzando l’editor universale, semplificando la creazione e la gestione da parte di utenti non tecnici. L’editor universale offre un’esperienza di creazione dei moduli intuitiva e consente di accedere a numerose funzionalità.

* **Servizio di invio dei moduli**: il servizio di invio dei moduli consente di memorizzare i dati relativi all’invio dei moduli su qualsiasi piattaforma, ad esempio OneDrive, SharePoint o Fogli Google, semplificando l’accesso e la gestione dei dati dei moduli all’interno del sistema preferito.

## Creazione di un modulo

Adobe Experience Manager offre e supporta più editor per la creazione di un modulo. Puoi utilizzare:
* [Editor universale (per l’authoring WYSIWYG)](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel o Fogli Google (noto come authoring basato su documento)](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### Editor universale (per l’authoring WYSIWYG)

L’editor universale è un editor visivo versatile che offre una funzionalità what-you-see-is-what-you-get (WYSIWYG) per garantire un’esperienza di creazione dei moduli intuitiva. Si consiglia di utilizzare l’editor universale durante la creazione di nuovi moduli, in quanto offre un design moderno e intuitivo e una comoda interfaccia tramite trascinamento.

Per creare i moduli tramite l’Editor universale, vengono utilizzati i modelli di Edge Delivery Services disponibili nell’ambiente AEM. Questi moduli ereditano l’aspetto dalle configurazioni nell’archivio GitHub di Edge Delivery Services. È stata stabilita [una connessione tra l’ambiente AEM e l’archivio GitHub di Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md) per consentire la pubblicazione di questi moduli su Edge Delivery Services.

Per informazioni dettagliate su come effettuare l’authoring con l’Editor universale, consulta l’articolo [Authoring dei contenuti con l’Editor universale.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)

### Microsoft Excel o Fogli Google (noto come authoring basato su documento)

Puoi creare i moduli utilizzando l’authoring basato su documenti con file Microsoft Excel o Fogli Google, che consentono di sfruttare i solidi ecosistemi e le API di Fogli Google, Microsoft Excel e Microsoft SharePoint. Questo approccio è particolarmente utile per la creazione di moduli semplici senza servizi di invio avanzati.

Per iniziare a creare un modulo utilizzando Microsoft Excel o Fogli Google, [imposta un progetto AEM utilizzando AEM Forms standard](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) e clona l’’archivio GitHub corrispondente nel computer locale. AEM Forms Edge Delivery fornisce una funzione chiamata Blocco di moduli adattivi, che semplifica il processo di creazione dei moduli per l’acquisizione e l’archiviazione dei dati. Per informazioni su come creare e pubblicare moduli tramite il blocco di moduli adattivi su Edge Delivery Services, consulta [Creare un modulo](/help/edge/docs/forms/create-forms.md).

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### Come scegliere tra i vari tipi di creazione dei moduli?

La tabella seguente illustra le funzioni e i casi d’uso per ogni editor di authoring, per aiutarti a scegliere quello giusto in base ai tuoi requisiti e alle tue esigenze di invio dei moduli.

| **Editor per la creazione moduli** | **Approccio chiave** | **Funzioni** | **Metodo di pubblicazione** | **Casi d’uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Authoring basato su documenti** | Sfrutta strumenti familiari come Documenti Google e Microsoft Office per la creazione di moduli. | I moduli sono progettati utilizzando fogli di calcolo, con dati inviati direttamente a Fogli Google o fogli di Microsoft Excel. </br> </br> Questi moduli sono più veloci da creare e distribuire. Per sviluppare componenti e stili personalizzati per questi moduli non è necessaria alcuna conoscenza preliminare di AEM. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e una SEO migliore. | Questi moduli sono ideali per la creazione rapida di prototipi o per moduli di base in cui non sono necessari servizi di invio avanzati. </br> </br> Questi moduli sono particolarmente adatti per sondaggi, registrazioni o moduli di feedback che richiedono l’archiviazione dei dati nei fogli di calcolo. Questi moduli vengono pubblicati su Edge Delivery Services |
| **Editor universale**  </br> </br> Se stai creando un modulo nuovo, utilizza Editor universale per creare i moduli. | Offre un’interfaccia WYSIWYG per la creazione intuitiva dei moduli. | I moduli sono progettati tramite un’interfaccia di trascinamento intuitiva. </br> </br> Questi moduli prendono in prestito l’aspetto dall’archivio GitHub di Edge Delivery Services configurato per il modulo corrispondente. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e una SEO migliore. | Questi moduli sono ideali per la creazione di moduli per siti e pagine di Edge Delivery Service. Questi scenari di moduli coinvolgono moduli e flussi di lavoro complessi, azioni personalizzate o integrazioni con sistemi esterni |

>[!NOTE]
>
>
> Se nell’editor universale mancano funzioni precedentemente disponibili nell’editor di moduli adattivi, si possono richiedere inviando un’e-mail a mailto:aem-forms-ea@adobe.com utilizzando il proprio indirizzo e-mail ufficiale.

## Consulta anche

{{see-more-forms-eds}}
