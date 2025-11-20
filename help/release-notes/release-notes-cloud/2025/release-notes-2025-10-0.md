---
title: Note sulla versione 2025.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2025.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: c5918c887be60c5198b762d860fe72afd31df352
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 59%

---

# Note sulla versione 2025.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2025.10.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.10.0) è il venerdì 30 ottobre 2025. La prossima versione funzionale (2025.11.0) è pianificata per il venerdì 20 novembre 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Experience Manager Sites {#new-sites}

* [Lanci per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md): gli autori dei contenuti possono ora creare e pianificare varianti future di contenuti strutturati utilizzando Lanci per frammenti di contenuto. La nuova console Frammenti di contenuto consente di creare, modificare, gestire e pianificare i lanci di frammenti di contenuto come rami per contenuti futuri che possono essere sincronizzati con il ramo di origine. Una nuova Visualizzazione differenze offre una panoramica chiara di tutte le modifiche apportate al contenuto prima di confermare un lancio per la pubblicazione futura.

* L&#39;editor del modello di contenuto [per i frammenti di contenuto di AEM](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) è stato modernizzato per l&#39;allineamento con altre interfacce basate su React Spectrum in AEM. L’implementazione dell’interfaccia utente e il modello di estensibilità sono ora coerenti con l’editor di frammenti di contenuto e l’editor universale. Il nuovo editor di modelli è ora predefinito quando viene aperto dalla nuova interfaccia di amministrazione del modello di contenuto. Quando si apre un modello di contenuto nell’interfaccia Touch, si apre l’editor dell’interfaccia Touch e viene presentata l&#39;opzione di provare il nuovo editor.

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in Experience Manager Forms {#new-features-forms}

**Editor universale per moduli adattivi e frammenti di moduli**

Universal Editor ora offre un’esperienza di authoring unificata per la creazione di Forms adattivi e frammenti di moduli riutilizzabili. Gli autori possono progettare i moduli visivamente all’interno di un ambiente WYSIWYG intuitivo, sfruttando potenti estensioni e funzionalità di invio complete. L’editor integra la convalida reCAPTCHA per una maggiore sicurezza, fornisce servizi di precompilazione per ridurre l’input manuale e supporta la progettazione reattiva su tutti i dispositivi.

**Estensioni disponibili:**

* **Editor regole**: l&#39;editor di regole visive consente agli autori di moduli di aggiungere un comportamento dinamico ai campi modulo senza codificare, supportare regole basate su eventi, convalida immediata e gestione degli errori.
* **Proprietà modulo**: procedura guidata che consente agli utenti di configurare le azioni di invio, il servizio di precompilazione, il messaggio di ringraziamento e altri comportamenti relativi ai moduli direttamente all&#39;interno dell&#39;editor.
* **Source dati modulo e riferimento associazione**: l&#39;estensione dell&#39;origine dati consente agli autori dei moduli di aggiungere componenti associati a un modello dati direttamente in un modulo adattivo e selezionare un riferimento associazione da una struttura ad albero per tutti i componenti.

**Azioni di invio supportate:**

Universal Editor supporta una gamma completa di flussi di lavoro per l’invio, tra cui Azione di invio personalizzata, Invia a Microsoft SharePoint, Invia a Microsoft OneDrive, Invia ad Azure Blob Storage, Invia a endpoint REST, Richiama un flusso di lavoro AEM, Richiama un flusso Power Automate, Invia a Marketo Engage, Invia a Adobe Experience Platform (AEP), Invia a foglio di calcolo, Invia utilizzando il modello dati del modulo (FDM), Invia a Workfront Fusion e Invia e-mail.

Per informazioni dettagliate, vedere la [documentazione di Universal Editor for Edge Delivery Services for Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md). Per informazioni sulla configurazione delle azioni di invio, vedere [Azione di invio modulo adattivo](/help/edge/docs/forms/universal-editor/submit-action.md).

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### Nuove funzioni per l’accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Miglioramenti alla comunicazione interattiva

##### Blocco modello

Blocca il contenuto e gli elementi di layout all’interno dei modelli per mantenere l’integrità del brand ed evitare modifiche non autorizzate. Ciò garantisce la coerenza del design in tutte le comunicazioni.

##### Supporto per overflow dei contenuti

Introduzione all’opzione &quot;Consenti interruzioni di pagina nel contenuto&quot; per i layout a flusso. Questo miglioramento consente di semplificare la modifica di più pagine e migliorare la gestione del testo per i documenti complessi.

##### Modifica file XDP

L’editor di comunicazioni interattive ora supporta la modifica XDP, inclusa l’integrazione dei frammenti. È ora possibile modificare i file XDP in un browser anziché in Forms Designer che viene eseguito solo su Microsoft Windows.

##### Numerazione dinamica delle pagine

Visualizza automaticamente &quot;Pagina # di ##&quot; nelle pagine master per una paginazione chiara e coerente nei documenti a più pagine.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Nuove funzioni in Release Management {#new-features-release-management}

**Sospendi aggiornamenti di manutenzione automatica**

I giorni di lancio, gli eventi live, i picchi di vendita: non possono fermarsi. [Le nuove funzionalità self-service](/help/implementing/deploying/quiet-hours-update-free-periods.md) consentono di interrompere gli aggiornamenti di manutenzione automatica quando sono importanti, in modo che i team rimangano concentrati.

* Quiet Hours (Ore tranquille): blocca la manutenzione automatica durante gli orari impostati ogni giorno. Ideale per le ore lavorative, le corse notturne o i cutover mattutini.
* Periodo senza aggiornamento: blocca la manutenzione automatica per una settimana intera. Utilizzala per lanci, promozioni o blocchi annuali.

>[!NOTE]
>
>Disponibile come funzionalità a disponibilità limitata il 25 settembre.
>Invia un&#39;e-mail a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) per attivarlo nei programmi.

### Inoltro dei registri di AEM a più destinazioni {#log-forwarding}

È ora possibile inoltrare i registri di AEM a Amazon S3, Sumo Logic, Dynatrace e al tuo account New Relic (non all’account fornito da Adobe). I registri di AEM (incluso Apache/Dispatcher) sono supportati per queste destinazioni di registrazione, ma non per i registri CDN.

Vedi il set completo di [destinazioni di inoltro log supportate](/help/implementing/developing/introduction/log-forwarding.md).

### Pipeline di configurazione per Edge Delivery Services {#config-pipeline-eds}

Le pipeline di configurazione sono ora supportate per i siti generati con Edge Delivery Services, espandendo questa funzionalità oltre la semplice distribuzione di AEM Author e AEM Publish. Puoi utilizzare le pipeline di configurazione per gestire impostazioni quali la configurazione CDN, incluse le regole del filtro del traffico e i selettori di origine. Consulta le [configurazioni supportate](/help/operations/config-pipeline.md#configurations).

Le pipeline di configurazione Edge Delivery ora supportano i secret tramite le variabili pipeline di Cloud Manager.

Consulta [Aggiungere pipeline Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

### Prossime versioni obsolete dell’API Java {#java-api-deprecation}

Diverse API obsolete sono state contrassegnate per la rimozione il 31 agosto e pertanto non è più necessario farvi riferimento.  Riceverai notifiche dal Centro operativo se nel codice viene rilevato un utilizzo di API obsolete e dopo il 13 novembre verranno visualizzati avvisi durante le build di Cloud Manager per sottolineare l’importanza di cessare tale utilizzo. Per informazioni dettagliate, consulta l’[articolo sulla rimozione](/help/release-notes/deprecated-removed-features.md#aem-apis). Per comodità, tuttavia, le seguenti API sono elencate di seguito:

+++ Espandi per visualizzare le rimozioni

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Rimozione runtime Java 11 {#java11-runtime-deprecation}

Adobe ha aggiornato gli ambienti **Stage** e **Produzione** al runtime **Java 21** a prestazioni superiori il 14 ottobre 2025. A partire dalla fine di gennaio, né il SDK di AEM Cloud Service né alcun ambiente cloud funzioneranno con il runtime Java 11.

>[!NOTE]
>
> Per sfruttare le ultime ottimizzazioni delle prestazioni e i miglioramenti del linguaggio, si consiglia di creare con Java 17 o Java 21 (preferito). La creazione di con Java 8 e Java 11 rimane supportata per il momento, ma verrà rimossa in una delle prossime versioni. Prima della deprecazione verrà inviata una comunicazione separata. Consulta la sezione *requisiti tempo di compilazione* di [questo articolo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dal **20 novembre**, le sostituzioni di registrazione personalizzate non supportate verranno ignorate. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe ha contattato tutti coloro la cui configurazione corrente potrebbe essere coinvolta.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di verbosità del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Edge Computing (programma Beta) {#edge-computing}

Edge Computing consente di eseguire JavaScript a livello CDN, avvicinando l’elaborazione dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end
* Esposizione di un server MCP per LLM come ChatGPT e Claude per accedere a strumenti personalizzati

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

### Autenticazione Edge per Edge Delivery Services (programma Beta) {#edge-authentication}

L’Autenticazione edge consente di limitare l’accesso alle pagine Edge Delivery Services solo a coloro che si sono autenticati con il provider di identità (IdP). Ciò avviene distribuendo un file YAML di configurazione OpenID Connect (OIDC).

Se ti interessa, invia una e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso ed eventuali domande.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Distribuzioni di produzione canary per testare il codice prima di accettare il traffico live (programma Beta) {#canary-beta}

Convalida una build di produzione con traffico di prova esclusivamente interno prima di renderla disponibile agli utenti finali. Invia alla produzione, instrada solo il traffico canary (utilizzando un’intestazione speciale), monitora il comportamento, quindi passa al traffico live o ripristina la versione precedente, senza che ciò abbia un impatto sui clienti.

Distribuisci le versioni del codice in produzione, ma limitalo al traffico di test esclusivamente interno prima di decidere se accettare il traffico in tempo reale o ripristinare la versione precedente.

Invia un’e-mail a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) per richiedere l’accesso e condividere il feedback.


### Risposte basate sull’intelligenza artificiale - Risposte più intelligenti e in base al contesto per AEM Sites (programma Beta) {#ai-answers-beta}

AI Answers introduce un nuovo modo per i visitatori di interagire con il contenuto. Basato sulla tecnologia Retrieval-Augmented Generation (RAG), utilizza i dati gestiti da AEM per fornire risposte precise e coerenti direttamente all’interno delle esperienze digitali.

Stiamo preparando il lancio del programma Beta AI Answers e invitiamo i clienti a registrare il loro interesse. Poiché la versione beta avrà una capacità molto limitata, le iscrizioni anticipate riceveranno la priorità. La partecipazione alla versione beta consente di esplorare le risposte AI nell’ambiente AEM Cloud Service, convalidare le prestazioni e l’accuratezza e contribuire a definire l’esperienza futura prima che diventi generalmente disponibile.

Per richiedere la partecipazione o ricevere aggiornamenti, contattare [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com).


### Istantanee per RDE (programma Alpha) {#rde-snapshot-program}

In Alpha, gli ambienti di sviluppo rapido (RDE) ora supportano una funzione per acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinata in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un’e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se ti interessa fornire un feedback su questa funzione.

### Monitoraggio avanzato delle prestazioni delle applicazioni (APM) (programma Alpha) {#apm-alpha}

Per motivi di osservabilità, AEM Cloud Service attualmente supporta [New Relic One](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornito da Adobe e [Dynatrace](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gestito dal cliente. Mentre esploriamo il supporto di ulteriori opzioni APM, inviaci un’e-mail all’indirizzo [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) indicando il fornitore o la tecnologia che preferisci, oltre ai casi d’uso.

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universale {#universal-editor}

L’elenco completo dei rilasci dell’editor universale è disponibile [qui](/help/release-notes/universal-editor/current.md).

## Generare varianti {#generate-variations}

L’elenco completo dei rilasci di generare varianti è disponibile [qui](/help/generative-ai/release-notes-generate-variations.md).

## Note sulla versione di Experience Cloud {#experience-cloud}

Informazioni sulle versioni di altre applicazioni Experience Cloud sono disponibili [qui](https://experienceleague.adobe.com/it/docs/release-notes/experience-cloud/current).
