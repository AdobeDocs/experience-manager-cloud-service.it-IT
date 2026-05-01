---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0ba0b95eac6b3a3ca0aa6ed0a816edcc63b9d50f
workflow-type: tm+mt
source-wordcount: '2009'
ht-degree: 31%

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

La data di rilascio di [!DNL Adobe Experience Manager] come versione corrente della funzionalità [!DNL Cloud Service] (2026.4.0) è il 30 aprile 2026. La prossima versione (2026.5.0) è prevista per il 28 maggio 2026.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)
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

### Agenti in AEM {#agents-in-aem}

Se desideri esplorare le potenti e nuove funzionalità di AEM Agent per la produzione, la governance, l&#39;ottimizzazione, l&#39;individuazione e lo sviluppo, [scopri come accedervi qui.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (programmi Beta) {#aem-foundation-beta-programs}

Consulta [Programmi beta di AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programmi Beta) {#cloud-manager-beta-programs}

Consulta [Programmi beta di Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Integrazione traduzione IA {#ai-translation-integration}

Gli utenti di AEM ora possono sfruttare i modelli LLM (Large Language Models) per la traduzione dei contenuti, fornendo qualità di traduzione umana alla velocità di traduzione automatica. Analogamente ai tradizionali servizi di traduzione di terze parti, Azure OpenAI può essere configurato come fornitore di traduzione in AEM, con supporto per ulteriori moduli LLM pianificati per le versioni future. Per questa funzionalità i clienti utilizzano le proprie licenze LLM. Inoltre, è possibile caricare in AEM le guide aziendali sullo stile di traduzione, consentendo l’estrazione delle regole di traduzione per garantire la coerenza di brand e stile. Per ulteriori informazioni, vedere [Configurazione dell&#39;integrazione della traduzione AI](/help/sites-cloud/administering/translation/ai-translation-integration.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Contenuto verificato ora disponibile per le applicazioni Adobe Workfront e non Adobe**

Contenuto verificato è ora disponibile per applicazioni Adobe Workfront e non Adobe (di terze parti), estendendo l’individuazione intelligente delle risorse e il riutilizzo dei contenuti oltre Adobe Express e AEM Sites. Questa versione offre l’esperienza completa di Content Advisor, con funzionalità di ricerca basate sull’intelligenza artificiale, consigli in base al contesto, individuazione basata su resoconto della campagna, accesso alle rappresentazioni Dynamic Media, individuazione dei frammenti di contenuto, filtri e metadati delle risorse ai flussi di lavoro di Adobe Workfront e alle applicazioni esterne.

Ora puoi scoprire, valutare e riutilizzare le risorse approvate da AEM Assets direttamente nelle applicazioni preferite, consentendo un utilizzo coerente delle risorse, una maggiore efficienza e una creazione semplificata dei contenuti sia nelle applicazioni Adobe che in quelle non Adobe.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms

* **Sovrascrivi configurazione cloud reCAPTCHA con OSGi** 
Gli ID progetto, le chiavi del sito e i segreti di reCAPTCHA Enterprise che conservi con i file di origine possono essere risolti in valori diversi in ogni ambiente Cloud Service dopo [aver aggiunto l&#39;override della configurazione in base al contesto e averli distribuiti tramite Cloud Manager](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi).

* **Autenticazione basata su certificato** 
I Forms adattivi che vengono inviati a un elenco di Microsoft SharePoint ora supportano [l&#39;autenticazione basata su certificato](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication) insieme all&#39;autenticazione URL OAuth. Per l’accesso basato su certificati, registra un alias del certificato e i dettagli del tenant in AEM e Microsoft Azure.

* **Miglioramenti dell’editor di regole**

   * L&#39;editor di regole di Forms adattivo ora supporta la grammatica semplificata per le regole [Dispatch Event e On Trigger Event per i trigger predefiniti e per gli eventi personalizzati](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events), pertanto gli autori non sono limitati alla grammatica solo per i trigger personalizzati.
   * Quando le regole di Adaptive Forms basate sui Componenti core ora includono il componente [File Attachment insieme ad altre condizioni utilizzando AND o OR logic](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component), la regola esegue le proprie azioni solo quando lo stato dell&#39;allegato e gli altri controlli valutano tutti come previsto.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### [!DNL Experience Manager] come [!DNL Cloud Service] nuove funzionalità di base {#foundation-new}

#### Strumenti di intelligenza artificiale IDE per lo sviluppo Java e Dispatcher di AEM {#ai-dev}

I team Java stack utilizzano sempre più lo sviluppo basato sull’intelligenza artificiale in strumenti come Cursor, Claude Code, Visual Studio e IntelliJ per velocizzare la distribuzione delle funzioni e migliorare la qualità del codice.

Gli strumenti IDE possono essere utilizzati dagli agenti di codifica per generare ed eseguire il debug del codice AEM e della configurazione del dispatcher. Ad esempio, la procedura dettagliata video riportata di seguito illustra la creazione di un componente AEM utilizzando le abilità dell’agente.

Ulteriori informazioni su [Sviluppo locale con strumenti di intelligenza artificiale](/help/ai-in-aem/local-development-with-ai-tools.md) e invia un&#39;e-mail a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) con domande o commenti.


>[!VIDEO](https://video.tv.adobe.com/v/3484978/?learn=on&enablevpops)

#### Server MCP per governance dell’esperienza {#gov-mcp-server}

Il server MCP di Experience Governance è ora generalmente disponibile (GA). Si integra con gli strumenti per sviluppatori AI e i chatbot che supportano il protocollo MCP (Model Context Protocol), consentendoti di salvaguardare l’integrità del brand e la conformità utilizzando prompt del linguaggio naturale nel chatbot o nell’IDE. Puoi valutare i contenuti (testo, immagini, pagine) in base alle regole di governance del brand e recuperare le configurazioni del brand e i controlli di governance disponibili.

Ulteriori informazioni sui [server AEM MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) e sull&#39;[agente di governance](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview).

#### Claude Connector {#aem-claude-connector}

Gli utenti Claude possono sfogliare il [marketplace dei connettori](https://claude.ai/settings/connectors) di Anthropic per installare con un solo clic il [connettore Adobe Experience Manager](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector). Questo server MCP espone un set crescente di strumenti per interagire con AEM, inclusa la modifica dei contenuti tramite prompt.

#### AEM OIDC sulla pubblicazione di nuove funzioni {#aem-oidc-on-publish-new-features}

* Correzione: i parametri di query della richiesta originale vengono persi dopo l’autenticazione
* Reindirizzamento personalizzato dopo l&#39;autenticazione nella [documentazione](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication) dell&#39;autenticazione OIDC

#### Supporto del servizio di posta per l’API di Microsoft Graph {#mail-service-graph-api}

Il servizio di posta di AEM ora supporta Microsoft® Outlook (tramite Microsoft 365) utilizzando l’API di Microsoft Graph. Questo è particolarmente utile per le organizzazioni che non consentono SMTP, che è già supportato dal servizio di posta. L’autenticazione avviene tramite OAuth 2.0. [Scopri come configurare](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api).

#### I registri CDN possono essere inoltrati alla logica di riepilogo {#sumo-cdn-logforwarding}

La funzionalità [Inoltro log](/help/implementing/developing/introduction/log-forwarding.md#sumologic) ora supporta l&#39;invio di registri CDN alla logica di riepilogo. In precedenza, l’inoltro dei registri a Sumo Logic era limitato ai registri di AEM.

### [!DNL Experience Manager] come [!DNL Cloud Service] Avvisi importanti di Foundation {#foundation-notices}

#### Errori complessi di autenticazione IMS {#ims-auth-rich-errors}

Per facilitare la risoluzione dei problemi relativi alle integrazioni IMS, `imsauth` ha aggiunto il supporto per *errori rich*.

Invece di restituire solo un codice di stato HTTP, questi errori forniscono ulteriore contesto per aiutare a diagnosticare e risolvere i problemi che possono bloccare l’autenticazione e l’accesso.

#### API Java obsolete {#java-api-deprecation}

È fondamentale rimuovere l’utilizzo di API obsolete.

A partire dal **14 aprile**, le pipeline Cloud Manager che contengono codice con destinazione API 2/26/2026 rimozione **non riescono durante il passaggio Qualità codice**. Le implementazioni verranno bloccate fino alla rimozione dell’utilizzo API obsoleto. *Ciò potrebbe impedire il rilascio di aggiornamenti sensibili al tempo e potrebbe influire sulle operazioni aziendali.*

A partire dall&#39;**11 giugno 2026**, gli ambienti che utilizzano ancora queste API obsolete **non riceveranno aggiornamenti critici della versione di Adobe** e non saranno soggetti agli impegni standard di Adobe in materia di prestazioni e disponibilità. Di conseguenza, non riceverai nuove funzioni o correzioni di bug, la stabilità e l’operatività delle applicazioni potrebbero essere influenzate negativamente e l’esposizione al rischio per la sicurezza potrebbe aumentare ulteriormente.

Per informazioni dettagliate, consulta l’[articolo sulla rimozione](/help/release-notes/deprecated-removed-features.md#aem-apis). Per comodità, tuttavia, le seguenti API sono elencate di seguito:

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
* `org.apache.jackrabbit.oak.plugins.memory`

+++

### Caratteristiche di [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Funzioni di AEM Edge (programma Beta) {#edge-functions}

[Funzioni AEM Edge](/help/implementing/developing/introduction/edge-functions.md) consente di eseguire JavaScript a livello di CDN, avvicinando l&#39;elaborazione dei dati all&#39;utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end
* Esposizione di un server MCP per gli assistenti AI come ChatGPT e Claude per accedere a strumenti personalizzati

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

#### Risoluzione dei problemi relativi alla pipeline di configurazione a livello web (programma Beta) {#devagent-webtier}

Le funzionalità di risoluzione dei problemi della pipeline [dell&#39;agente di sviluppo](/help/ai-in-aem/agents/brand-experience/development/development.md) consentono agli sviluppatori di diagnosticare e risolvere in modo efficiente i problemi nelle distribuzioni di AEM as a Cloud Service. Oltre a supportare le pipeline full stack (distribuzione e qualità del codice), l&#39;agente di sviluppo ora supporta la risoluzione dei problemi per la **pipeline di configurazione a livello web** come parte di un programma beta.

Per richiedere l&#39;accesso alla versione beta, invia un&#39;e-mail a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). È richiesto l’accesso preesistente agli agenti in AEM.

#### Risoluzione dei problemi di IA per la replica (programma Alpha) {#replication-ai-troubleshooting-alpha}

Utilizzando l’Assistente IA in AEM Author e altre interfacce, puoi risolvere i problemi relativi alla replica, ad esempio le code bloccate. Per partecipare al programma Alpha, invia un&#39;e-mail a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) con la descrizione del tuo interesse.

#### Strumenti di intelligenza artificiale IDE per la migrazione da AEM 6.5 a AEM Cloud Service (programma Beta) {#cm-ide-migration}

Accelera la migrazione da AEM 6.5 ad AEM as a Cloud Service (stack Java) utilizzando gli strumenti di intelligenza artificiale IDE per seguire le raccomandazioni del [rapporto di Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Invia un&#39;e-mail a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) per ulteriori informazioni e per richiedere l&#39;accesso alla funzionalità.

#### Autenticazione Edge per Edge Delivery Services (programma Beta) {#edge-authentication}

L’Autenticazione edge consente di limitare l’accesso alle pagine Edge Delivery Services solo a coloro che si sono autenticati con il provider di identità (IdP). Ciò avviene distribuendo un file YAML di configurazione OpenID Connect (OIDC).

Se ti interessa, invia una e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso ed eventuali domande.

#### Distribuzioni di produzione canary per testare il codice prima di accettare il traffico live (programma Beta) {#canary-beta}

Convalida una build di produzione con traffico di prova esclusivamente interno prima di renderla disponibile agli utenti finali. Invia alla produzione, instrada solo il traffico canary (utilizzando un’intestazione speciale), monitora il comportamento, quindi passa al traffico live o ripristina la versione precedente, senza che ciò abbia un impatto sui clienti.

Invia un’e-mail a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) per richiedere l’accesso e condividere il feedback.

#### Snapshot per RDE (programma Beta) {#rde-snapshot-program}

In versione beta, gli ambienti di sviluppo rapido (RDE) ora supportano una funzionalità [per creare uno snapshot](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots) dello stato corrente del codice e del contenuto, che può essere ripristinato in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un&#39;e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se sei interessato a utilizzare e fornire feedback su questa funzione.

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
