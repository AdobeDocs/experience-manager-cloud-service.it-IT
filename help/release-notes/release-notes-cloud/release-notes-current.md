---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0411792d22efa70f98777971eb4f16700820abe5
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 50%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.12.0) è il venerdì 11 dicembre 2025. La prossima versione funzionale (2026.1.0) è pianificata per il venerdì 29 gennaio 2026.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Programmi AEM Beta {#aem-beta-programs}

I programmi beta di Adobe Experience Manager (AEM) consentono ai clienti di accedere alle funzioni e al codice prerelease, fornire feedback e guidare il futuro di AEM.

>[!IMPORTANT]
>
>I rilasci di Beta possono contenere difetti e vengono forniti &quot;COSÌ COME SONO&quot; senza alcuna garanzia. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare o altrimenti supportare (tramite i servizi di supporto Adobe o in altro modo) le versioni beta. Adobe consiglia ai clienti di prestare attenzione e di non affidarsi al corretto funzionamento o alle prestazioni delle versioni beta o a qualsiasi documentazione o materiale di accompagnamento. Le funzioni e le API in versione beta sono soggette a modifiche senza preavviso. Di conseguenza, qualsiasi utilizzo delle versioni beta è interamente a rischio del cliente.

**Vantaggi della partecipazione**
L’accesso anticipato alle funzioni sviluppate da Adobe consente a clienti e partner di fornire feedback e plasmare lo sviluppo dei prodotti. Consente inoltre di prepararsi ad adottare nuove funzionalità prima della disponibilità generale.

**Programmi beta correnti**
Nelle sezioni seguenti sono elencati i programmi beta attivi.

### Agenti in AEM (programma Beta) {#agents-in-aem-beta-program}

Accesso anticipato a nuove potenti funzionalità di AEM Agent in ambienti di produzione, governance, ottimizzazione, discovery e sviluppo. Il tuo feedback influisce direttamente sulla roadmap e sulle funzioni finali di Adobe. Per ulteriori informazioni, consulta [Panoramica degli agenti in AEM](/help/ai-in-aem/agents/overview.md).

Questo programma dura in genere 4-6 settimane, ma può essere personalizzato per essere flessibile in base alla tua capacità di partecipazione attiva.

Per partecipare al programma, inviare un&#39;e-mail a [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) e includere i dettagli seguenti nella misura del possibile:

* Nomi e Adobe ID dei membri del gruppo che utilizzeranno attivamente gli agenti.
* Elencare agenti specifici che il tuo team desidera utilizzare. Oppure dire semplicemente &quot;Tutti gli agenti&quot;.

### AEM Foundation (programmi Beta) {#aem-foundation-beta-programs}

Consulta [Programmi beta di AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programmi Beta) {#cloud-manager-beta-programs}

Consulta [Programmi beta di Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**È disponibile una nuova versione del plug-in Figma per l&#39;integrazione con AEM Assets**

* Supporto per file video (MP4, MOV, WebM), file animati (GIF) e file vettoriali (SVG) durante l’importazione di risorse dall’archivio AEM al documento Figma.

* Supporto per la verifica di eventuali aggiornamenti alle risorse utilizzate nel documento Figma rispetto alle risorse esistenti nell’archivio AEM e per ottenere la versione più recente delle risorse, in caso di aggiornamenti.

* Supporto per le configurazioni di esportazione durante l&#39;esportazione di formati di file PNG (scale) e JPG (image scale and quality).

  ![Plug-in Figma](/help/assets/assets/figma-v2-plugin.png)

**Rilevamento malware per risorse caricate**

AEM Assets ora include la scansione automatica dei malware per i file caricati, garantendo che le risorse sospette siano messe in quarantena prima di entrare in DAM per proteggere l’archivio dalle minacce. Gli amministratori possono configurare le impostazioni di scansione e i criteri di conservazione della quarantena per controlli di sicurezza semplificati.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

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

### [!DNL Experience Manager] come [!DNL Cloud Service] nuove funzionalità di base {#foundation-new}

#### Prossime versioni obsolete dell’API Java {#java-api-deprecation}

Diverse API obsolete sono state contrassegnate per la rimozione il 31 agosto e pertanto non è più necessario farvi riferimento.  Riceverai notifiche dal Centro operativo se nel codice viene rilevato un utilizzo API obsoleto e, dopo il 29 gennaio, durante le build di Cloud Manager verranno visualizzati avvisi per sottolineare l’importanza di rimuovere l’utilizzo. Per informazioni dettagliate, consulta l’[articolo sulla rimozione](/help/release-notes/deprecated-removed-features.md#aem-apis). Per comodità, tuttavia, le seguenti API sono elencate di seguito:

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

#### Rimozione runtime Java 11 {#java11-runtime-deprecation}

Adobe ha aggiornato gli ambienti **Stage** e **Produzione** al runtime **Java 21** a prestazioni superiori il 14 ottobre 2025. A partire dal **9 febbraio**, né il SDK di AEM Cloud Service né gli ambienti cloud funzioneranno con Java 11 runtime.

>[!NOTE]
>
> Per sfruttare le ultime ottimizzazioni delle prestazioni e i miglioramenti del linguaggio, si consiglia di creare con Java 17 o Java 21 (preferito). La creazione di con Java 8 e Java 11 rimane supportata per il momento, ma verrà rimossa in una delle prossime versioni. Prima della deprecazione verrà inviata una comunicazione separata. Consulta la sezione *requisiti tempo di compilazione* di [questo articolo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dal **29 gennaio**, le sostituzioni di registrazione personalizzate non supportate verranno ignorate. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe ha contattato tutti coloro la cui configurazione corrente potrebbe essere coinvolta.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di verbosità del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Caratteristiche di [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Sospendi aggiornamenti di manutenzione automatica {#pause-updates}

I giorni di lancio, gli eventi live, i picchi di vendita: non possono fermarsi. [Le nuove funzionalità self-service](/help/implementing/deploying/quiet-hours-update-free-periods.md) consentono di interrompere gli aggiornamenti di manutenzione automatica quando sono importanti, in modo che i team rimangano concentrati.

* Quiet Hours (Ore tranquille): blocca la manutenzione automatica durante gli orari impostati ogni giorno. Ideale per le ore lavorative, le corse notturne o i cutover mattutini.
* Periodo senza aggiornamento: blocca la manutenzione automatica per una settimana intera. Utilizzala per lanci, promozioni o blocchi annuali.

>[!NOTE]
>
>Disponibile come funzionalità a disponibilità limitata il 25 settembre.
>Invia un&#39;e-mail a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) per attivarlo nei programmi.
>

#### Edge Computing (programma Beta)

Edge Computing consente di eseguire JavaScript a livello CDN, avvicinando l’elaborazione dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end
* Esposizione di un server MCP per LLM come ChatGPT e Claude per accedere a strumenti personalizzati

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

#### Autenticazione Edge per Edge Delivery Services (programma Beta) {#edge-authentication}

L’Autenticazione edge consente di limitare l’accesso alle pagine Edge Delivery Services solo a coloro che si sono autenticati con il provider di identità (IdP). Ciò avviene distribuendo un file YAML di configurazione OpenID Connect (OIDC).

Se ti interessa, invia una e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso ed eventuali domande.

#### Distribuzioni di produzione canary per testare il codice prima di accettare il traffico live (programma Beta) {#canary-beta}

Convalida una build di produzione con traffico di prova esclusivamente interno prima di renderla disponibile agli utenti finali. Invia alla produzione, instrada solo il traffico canary (utilizzando un’intestazione speciale), monitora il comportamento, quindi passa al traffico live o ripristina la versione precedente, senza che ciò abbia un impatto sui clienti.

Distribuisci le versioni del codice in produzione, ma limitalo al traffico di test esclusivamente interno prima di decidere se accettare il traffico in tempo reale o ripristinare la versione precedente.

Invia un’e-mail a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) per richiedere l’accesso e condividere il feedback.


#### Risposte basate sull’intelligenza artificiale - Risposte più intelligenti e in base al contesto per AEM Sites (programma Beta) {#ai-answers-beta}

AI Answers introduce un nuovo modo per i visitatori di interagire con il contenuto. Basato sulla tecnologia Retrieval-Augmented Generation (RAG), utilizza i dati gestiti da AEM per fornire risposte precise e coerenti direttamente all’interno delle esperienze digitali.

Stiamo preparando il lancio del programma Beta AI Answers e invitiamo i clienti a registrare il loro interesse. Poiché la versione beta avrà una capacità molto limitata, le iscrizioni anticipate riceveranno la priorità. La partecipazione alla versione beta consente di esplorare le risposte AI nell’ambiente AEM Cloud Service, convalidare le prestazioni e l’accuratezza e contribuire a definire l’esperienza futura prima che diventi generalmente disponibile.

Per richiedere la partecipazione o ricevere aggiornamenti, contattare [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com).

#### Snapshot per RDE (programma Beta) {#rde-snapshot-program}

In versione beta, gli ambienti di sviluppo rapido (RDE) supportano ora una funzione che consente di acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinato in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un&#39;e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se sei interessato a utilizzare e a fornire feedback su questa funzione.

#### Accelerare lo sviluppo di AEM con l’intelligenza artificiale (programma Alpha) {#ai-dev-alpha}

I team Java stack di AEM utilizzano sempre più lo sviluppo basato sull’intelligenza artificiale in strumenti come Cursor, Claude Code, Visual Studio e IntelliJ per velocizzare la distribuzione delle funzioni e migliorare la qualità del codice. Stiamo raccogliendo esperienze reali per aiutare a modellare le future funzionalità di intelligenza artificiale supportate da Adobe.

Condividi ciò che funziona per il tuo team e ciò che desideri che Adobe fornisca inviando un&#39;e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

#### Monitoraggio avanzato delle prestazioni delle applicazioni (APM) (programma Alpha) {#apm-alpha}

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
