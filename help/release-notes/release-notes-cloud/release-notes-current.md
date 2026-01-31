---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: c5c63e4ecfa099f953c1cf01861c0342ba4bae18
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 37%

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

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2026.1.0) è il venerdì 29 gennaio 2026. La prossima versione funzionale (2026.2.0) è pianificata per il venerdì 26 febbraio 2026.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440928?captions=ita&quality=12)

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

I clienti selezionati per la partecipazione riceveranno una notifica diretta da Adobe. La partecipazione è soggetta a considerazioni di idoneità, tra cui la concessione di licenze ai clienti e la capacità limitata del programma. Anche se non tutte le richieste possono essere soddisfatte inizialmente, ulteriori clienti potrebbero essere presi in considerazione nelle prossime ondate beta.

### AEM Foundation (programmi Beta) {#aem-foundation-beta-programs}

Consulta [Programmi beta di AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programmi Beta) {#cloud-manager-beta-programs}

Consulta [Programmi beta di Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Server MCP dei contenuti {#content-MCP}

AEM Cloud Service ora include **Content MCP Server**, che fornisce un modo standardizzato per consentire alle esperienze basate sull&#39;intelligenza artificiale di lavorare con i contenuti AEM tramite strumenti compatibili con MCP.

Sviluppatori e utenti esperti che lavorano su app di chat e piattaforme di agenti possono collegare AEM a compilazioni e automazioni personalizzate, in modo che il lavoro sui contenuti diventi parte dei flussi di lavoro aziendali end-to-end.

AEM fornisce due server:

1. **Server MCP dei contenuti di sola lettura** - per recuperare i contenuti in modo sicuro
1. **Server MCP del contenuto di lettura/scrittura** - per apportare modifiche al contenuto

Questi server MCP includono strumenti per l&#39;utilizzo di **Pagine**, **Frammenti di contenuto** e **Assets** e possono essere utilizzati dai seguenti client MCP: **ChatGPT**, **Claude**, **Cursore** e **Microsoft Copilot Studio**.

Ulteriori informazioni in [Utilizzo di MCP con AEM Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Per domande o commenti, invia un&#39;e-mail a [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Ricerca IA**

Ricerca IA introduce un’esperienza di ricerca intelligente e basata sul contesto che va oltre la tradizionale corrispondenza delle parole chiave, comprendendo il significato e le finalità alla base delle query degli utenti. Basato sull’intelligenza artificiale e sull’apprendimento automatico, fornisce risultati più precisi anche quando le query sono formulate in modo diverso, contengono errori ortografici, utilizzano sinonimi o vengono inviate in lingue diverse, consentendo agli utenti di trovare contenuti rilevanti più rapidamente e con meno sforzo.

Per ulteriori informazioni, vedere Ricerche IA in [Assets view](/help/assets/search-assets-view.md#ai-search) e [Admin view](/help/assets/search-assets.md#ai-search).

**Versione app desktop 3.0.1**

[App desktop 3.0.1 (20 dicembre 2025)](https://experienceleague.adobe.com/it/docs/experience-manager-desktop-app/using/release-notes) migliora l&#39;affidabilità, le prestazioni e la stabilità tra i flussi di lavoro chiave. Questa versione assicura una denominazione coerente delle cartelle, risolvendo i problemi di sincronizzazione con AEM Author, consente un utilizzo ininterrotto dell’app durante i trasferimenti attivi, migliora la reattività dell’interfaccia utente tramite l’elaborazione asincrona, ottimizza i trasferimenti di file di grandi dimensioni con l’impaginazione e risolve i problemi di stabilità, tra cui i riavvii e gli arresti anomali del server di authoring durante caricamenti e download di cartelle di grandi dimensioni.

**Versione di Adobe Asset Link CEP 2026.01.0**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) introduce una nuova opzione Ricollega collegamenti mancanti in InDesign che ricollega automaticamente altre risorse mancanti dalla stessa cartella di AEM. La funzione associa le risorse in base al nome file, riducendo notevolmente lo sforzo manuale durante il ripristino dei collegamenti interrotti.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

* [Miglioramenti al segnaposto nota a piè di pagina in Forms adattivo (componenti di base)](/help/forms/footnotes-richtextsupport.md):
   * Il rendering delle note a piè di pagina è stato ulteriormente perfezionato per supportare la formattazione su più righe attraverso interruzioni di riga, consentendo una presentazione più chiara ed espressiva del contenuto delle note a piè di pagina.
   * Le note a piè di pagina ora rimangono sempre visibili all’interno del segnaposto della nota a piè di pagina, indipendentemente dalla visibilità dei pannelli associati, garantendo un accesso coerente alle informazioni critiche.


### Nuove funzioni per l’accesso anticipato in AEM Forms {#forms-new-early-access-features}

* [Recuperare valori da un array JSON](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array): le funzionalità di integrazione dei dati espanse ora consentono di richiamare le API tramite funzioni personalizzate per estrarre in modo efficiente i valori dagli array JSON e associarli direttamente ai campi del modulo adattivo. Questo miglioramento semplifica il consumo di dati, riduce al minimo la mappatura manuale e supporta esperienze di moduli più dinamiche e basate su dati.

* **Richiama l&#39;interfaccia utente Associate in un&#39;istanza Publish**: il supporto esteso è ora disponibile per richiamare l&#39;interfaccia utente Associate direttamente nelle istanze Publish. Questa funzionalità definisce la configurazione, la struttura del payload e il flusso di richiamo richiesti, semplificando l’integrazione e accelerando l’implementazione negli ambienti.

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

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] come [!DNL Cloud Service] Avvisi importanti di Foundation {#foundation-notices}

#### API Java obsolete {#java-api-deprecation}

Le API obsolete con targeting 2/26/2026 non devono più essere utilizzate nel codice. Per evitare blocchi di distribuzione, rimuovi l’utilizzo dell’API prima del 26 marzo 2026. Date importanti:

* **A partire dal 26 gennaio 2026**: le e-mail di notifica del Centro operativo vengono inviate **ogni settimana per ogni ambiente** come promemoria per rimuovere l&#39;utilizzo di queste API.
* **26 febbraio 2026**: le pipeline Cloud Manager che contengono codice che utilizza queste API **sospendono** durante il passaggio **Qualità codice**. Un Responsabile della distribuzione, un Project Manager o un Proprietario business può ignorare il problema per consentire alla pipeline di procedere.
* **26 marzo 2026**: le pipeline Cloud Manager che contengono codice che utilizza queste API **non riusciranno** durante il passaggio **Qualità codice**, **bloccando le distribuzioni** del nuovo codice fino alla rimozione dell&#39;utilizzo.
* **30 aprile 2026**: gli ambienti che utilizzano ancora queste API potrebbero **non ricevere più aggiornamenti critici sulla versione di Adobe**.

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

Adobe ha aggiornato gli ambienti **Stage** e **Produzione** al runtime **Java 21** a prestazioni superiori il 14 ottobre 2025. A partire dal **9 febbraio** (rollout graduale fino all&#39;11 febbraio), né AEM Cloud Service SDK né alcun ambiente cloud funzioneranno con Java 11 runtime.

>[!NOTE]
>
> Per sfruttare le ultime ottimizzazioni delle prestazioni e i miglioramenti del linguaggio, si consiglia di creare con Java 17 o Java 21 (preferito). La creazione di con Java 8 e Java 11 rimane supportata per il momento, ma verrà rimossa in una delle prossime versioni. Prima della deprecazione verrà inviata una comunicazione separata. Consulta la sezione *requisiti tempo di compilazione* di [questo articolo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

I registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti dei clienti. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Eventuali sostituzioni di registrazione personalizzate non supportate *vengono ora ignorate*. La maggior parte dei clienti non è stata interessata e Adobe ha contattato i clienti la cui configurazione corrente potrebbe essere interessata.

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

#### Funzioni di AEM Edge (programma Beta) {#edge-functions}

Le funzioni di AEM Edge (a cui si fa riferimento nelle note precedenti sulla versione come *Edge Computing*) consentono di eseguire JavaScript a livello di CDN, avvicinando l&#39;elaborazione dei dati all&#39;utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

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

Invia un&#39;e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se sei interessato a utilizzare e fornire feedback su questa funzione.

#### Strumenti di intelligenza artificiale per IDE per lo sviluppo Java e Dispatcher di AEM (programma Beta) {#ai-dev-beta}

I team Java stack utilizzano sempre più lo sviluppo basato sull’intelligenza artificiale in strumenti come Cursor, Claude Code, Visual Studio e IntelliJ per velocizzare la distribuzione delle funzioni e migliorare la qualità del codice. Partecipa alla versione beta per:

* Condividi esperienze reali per contribuire a definire le future funzionalità di intelligenza artificiale supportate da Adobe
* Prova gli strumenti IDE che possono essere utilizzati dagli agenti di intelligenza artificiale per generare ed eseguire il debug del codice AEM e della configurazione del dispatcher

Per ulteriori informazioni, invia un&#39;e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

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
