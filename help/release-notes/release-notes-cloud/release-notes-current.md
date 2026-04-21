---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: c9ab1fefa8170a1397eb5801f26128e82e7cd4ca
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 29%

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

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2026.3.0) è il venerdì 26 marzo 2026. La prossima versione funzionale (2026.4.0) è pianificata per l’venerdì 30 aprile 2026.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video che mostra una panoramica sulla versione di marzo 2026 per un riepilogo delle funzioni aggiunte alla versione 2026.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)

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

### Estrazione/Inserimento di frammenti di contenuto {#cf-checkout-in}

Per migliorare la parità con l’interfaccia utente touch di AEM, ora è possibile estrarre e archiviare nuovamente i frammenti di contenuto utilizzando anche la nuova interfaccia utente di amministrazione dei frammenti di contenuto. La funzionalità di estrazione rimane invariata, bloccando in modo efficace un frammento di contenuto estratto e impedendo così che possa essere modificato nell’Editor frammento di contenuto da altri utenti. Gli utenti proprietari di un frammento di contenuto e gli amministratori possono estrarlo e inserirlo nuovamente. L’estrazione di un frammento non ha alcun effetto sui frammenti o sulle risorse secondarie a cui si fa riferimento.

### Pannello Processi di avvio frammento di contenuto {#cf-launches-jobs}

Ora è possibile visualizzare i processi asincroni per i lanci di frammenti di contenuto nel pannello delle proprietà dei lanci di frammenti di contenuto, nell’interfaccia di amministrazione, per osservarne lo stato - se un processo è ancora in esecuzione, è stato completato o è stato interrotto, insieme alle informazioni dettagliate pertinenti sul processo.

### Aggiornamento dell’editor Rich Text dell’Editor frammenti di contenuto {#cf-rte-update}

L’editor Rich Text dell’editor di frammenti di contenuto è stato migrato da TinyMCE a TipTap. Questo cambiamento porta con sé una serie di vantaggi.

* Universal Editor e Content Fragment Editor ora utilizzano lo stesso stack di tecnologia RTE.
   * Ciò significa che entrambi gli editor ora producono lo stesso HTML.
   * Le estensioni possono ora essere riutilizzabili.
   * Sono ora disponibili le stesse funzioni e gli stessi metodi utilizzando entrambi gli editor (nei casi di utilizzo headless).
   * L’obiettivo finale è che una configurazione porti a un’esperienza unificata in entrambi gli editor.
* L’editor di contenuti ora ha un nuovo aspetto nello stile Spectrum 2.
* Nell’Editor frammento di contenuto sono disponibili nuove funzionalità, tra cui Trova e sostituisci, pronti per l’uso come consulente per contenuti.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Contenuto verificato in AEM Sites**

Contenuto verificato è ora disponibile in AEM Sites, con l’introduzione dell’individuazione intelligente delle risorse direttamente da AEM Assets. Consente agli utenti di individuare, sfogliare e riutilizzare senza difficoltà le risorse più rilevanti direttamente all’interno del flusso di lavoro, eliminando la necessità di cambiare contesto.

Contenuto verificato fornisce funzioni intelligenti per risorse quali suggerimenti basati su resoconti delle campagne, suggerimenti contestuali, accesso alle rappresentazioni Dynamic Media e metadati dettagliati delle risorse.

Disponibile a breve: supporto di Content Advisor per le applicazioni B2C Adobe Workfront e AJO, inclusa la possibilità di individuare frammenti di contenuto

### Nuove funzioni in Dynamic Media {#dynamic-media-new-features}

#### Aggiornamenti di Dynamic Media Template Editor {#dynamic-media-template-editor-updates}

**Miglioramenti alla gestione dei livelli**

* Riordinamento dei livelli mediante trascinamento: è ora possibile riordinare i livelli direttamente nel pannello Livelli trascinandoli, in modo più rapido e intuitivo per organizzare l&#39;ordine di sovrapposizione dei livelli oltre le azioni Porta avanti o Porta indietro esistenti.
* Copia, Incolla e duplica: supporto completo per copiare, incollare e duplicare i livelli utilizzando le scelte rapide da tastiera (Comando/Ctrl+C, V, D) o il menu di scelta rapida, con supporto per le selezioni a più livelli.
* Pulsante Proprietà livello separato: è stato aggiunto il pulsante Proprietà livello dedicato per facilitare la navigazione alle impostazioni dei livelli, con il supporto del doppio clic sui livelli per un accesso rapido.

**Caratteristiche formattazione testo**

* Controllo dell&#39;interlinea: il nuovo cursore per l&#39;interlinea consente un controllo preciso dell&#39;altezza della linea nei livelli di testo, con il supporto completo dell&#39;operazione end-to-end che include le operazioni Annulla/Ripristina e Salva/Carica modello.
* Formattazione tutto maiuscolo: i livelli di testo ora supportano l&#39;opzione di formattazione Tutto maiuscolo nella barra degli strumenti Stile carattere insieme a Grassetto, Corsivo e Sottolineato.
* Opzioni di allineamento verticale: sono stati aggiunti controlli di allineamento verticale per i livelli di testo, che consentono di posizionare il testo in modo più preciso all&#39;interno delle caselle di testo.

**Controlli dimensione e Dimension**

* Sblocco proporzioni: gli utenti possono ora sbloccare le proporzioni durante la regolazione delle proprietà di dimensione, consentendo regolazioni indipendenti di larghezza e altezza per dimensioni di livello più flessibili.
* Configurazione di righe di adattamento: è stato aggiunto il supporto per le impostazioni `copyfitlines` e `copyfitmaxlines` nelle proprietà di adattamento del testo, fornendo un controllo più preciso sul comportamento dell&#39;adattamento del testo.

**Polacco visivo**

* Sono state aggiornate le icone per i livelli Timer e Forma con le icone perfezionate del sistema di progettazione Spectrum 2 (S2).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzionalità per Accesso anticipato in AEM Forms {#forms-early-access-features}

**Visualizza le etichette per il menu a discesa a selezione multipla in PDF di invio**
I componenti a discesa a selezione multipla in Adaptive Forms ora eseguono il rendering delle etichette di visualizzazione selezionate in [PDF di invio generato](/help/forms/generate-document-of-record-core-components.md), garantendo che il documento rifletta con precisione ciò che viene visualizzato dagli utenti nel modulo.

**Accesso facilitato per i componenti di caselle di controllo, pulsanti di scelta e pannelli**
I componenti core Forms adattivi introducono il markup semantico conforme a WCAG 2.2 per [gruppi di caselle di controllo(v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [gruppi di pulsanti di scelta(v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) e [componente Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Questi componenti sfruttano gli elementi HTML `<fieldset>` e `<legend>` per stabilire relazioni significative tra le etichette dei gruppi e le relative opzioni, consentendo un&#39;interpretazione accurata da parte degli assistenti vocali e di altre tecnologie per l&#39;accessibilità.

**Supporto del controllo delle versioni in Forms Manager**
Forms Manager ora [supporta il controllo delle versioni per Forms adattivo (Componenti core e Componenti di base)](/help/forms/manage-form-versions-forms-manager.md), frammenti di modulo, temi, modelli XDP e risorse binarie. Crea versioni, visualizza la cronologia completa delle versioni e ripristina gli stati precedenti delle risorse del modulo direttamente dalla console Forms &amp; Documents.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### [!DNL Experience Manager] come [!DNL Cloud Service] nuove funzionalità di base {#foundation-new}

#### Gestione semplificata degli indici {#simplified-index-management}

[Gestione semplificata degli indici](https://oak-indexing.github.io/oakTools/simplified.html) offre un modo più semplice per definire indici personalizzati e personalizzare indici predefiniti utilizzando un unico file JSON, senza copiare definizioni complete o gestire manualmente le versioni. Le personalizzazioni vengono unite con l’indice OOTB più recente e, se necessario, viene creata una nuova versione dell’indice.

#### Server Cloud Manager MCP {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

Le IDE moderne utilizzano il protocollo MCP (Model Context Protocol) per abilitare i modelli di linguaggio di grandi dimensioni (Large Language Model, LLM) per richiamare gli strumenti esposti dai server MCP. Invece di integrarsi direttamente con le specifiche API di basso livello, gli sviluppatori possono semplicemente descrivere il loro intento nel linguaggio naturale.

Il server Cloud Manager MCP consente di interagire con le API Cloud Manager direttamente dall’IDE tramite prompt. Gli scenari supportati includono l’esecuzione delle pipeline, la verifica dello stato dell’ambiente e altro ancora.

Ulteriori informazioni sui [server AEM MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

### [!DNL Experience Manager] come [!DNL Cloud Service] Avvisi importanti di Foundation {#foundation-notices}

#### API Java obsolete {#java-api-deprecation}

Le API obsolete con targeting 2/26/2026 non devono più essere utilizzate nel codice. Per evitare blocchi di distribuzione, rimuovi l’utilizzo dell’API prima del **30 marzo 2026**. Date importanti:

* **A partire dal 26 gennaio 2026**: le e-mail di notifica del Centro operativo vengono inviate come promemoria per rimuovere l&#39;utilizzo di queste API.
* **26 febbraio 2026**: le pipeline Cloud Manager che contengono codice che utilizza queste API **sospendono** durante il passaggio **Qualità codice**. Un Responsabile della distribuzione, un Project Manager o un Proprietario business può ignorare il problema per consentire alla pipeline di procedere. *La convalida e il rilascio delle modifiche al codice potrebbero essere rallentati.*
* **30 marzo 2026**: le pipeline Cloud Manager che contengono codice che utilizza queste API **non riusciranno** durante il passaggio **Qualità codice**. Le implementazioni verranno bloccate fino alla rimozione dell’utilizzo API obsoleto. *Ciò potrebbe impedire il rilascio di aggiornamenti sensibili al tempo e potrebbe influire sulle operazioni aziendali.*
* **4 maggio 2026**: gli ambienti che utilizzano ancora API obsolete **non riceveranno aggiornamenti critici della versione di Adobe** e non sono soggetti agli impegni standard di Adobe relativi a prestazioni e disponibilità. Di conseguenza, non riceverai nuove funzioni o correzioni di bug, la stabilità e l’operatività delle applicazioni potrebbero essere influenzate negativamente e l’esposizione al rischio per la sicurezza potrebbe aumentare ulteriormente.

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

#### Strumenti di intelligenza artificiale IDE per lo sviluppo Java e Dispatcher di AEM (programma Beta pubblico) {#ai-dev-beta}

I team Java stack utilizzano sempre più lo sviluppo basato sull’intelligenza artificiale in strumenti come Cursor, Claude Code, Visual Studio e IntelliJ per velocizzare la distribuzione delle funzioni e migliorare la qualità del codice.

Partecipa alla versione beta pubblica (non è necessaria alcuna iscrizione) per provare gli strumenti IDE che possono essere utilizzati dagli agenti di codifica per generare ed eseguire il debug del codice AEM e della configurazione del dispatcher.

Per ulteriori informazioni, consulta la [documentazione sullo sviluppo locale con strumenti di intelligenza artificiale](/help/ai-in-aem/local-development-with-ai-tools.md) beta e invia un&#39;e-mail a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) con domande o feedback.

#### Funzioni di AEM Edge (programma Beta) {#edge-functions}

Le funzioni Edge di AEM consentono di eseguire JavaScript a livello di CDN, avvicinando l’elaborazione dei dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end
* Esposizione di un server MCP per LLM come ChatGPT e Claude per accedere a strumenti personalizzati

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

#### Risoluzione dei problemi relativi alla pipeline di configurazione a livello web con l’agente di sviluppo (programma Beta) {#devagent-webtier}

Le funzionalità di risoluzione dei problemi della pipeline [dell&#39;agente di sviluppo](/help/ai-in-aem/agents/brand-experience/development/development.md) consentono agli sviluppatori di diagnosticare e risolvere in modo efficiente i problemi nelle distribuzioni di AEM as a Cloud Service. Oltre a supportare le pipeline full stack (distribuzione e qualità del codice), l&#39;agente di sviluppo ora supporta la risoluzione dei problemi per la **pipeline di configurazione a livello web** come parte di un programma beta.

Per richiedere l&#39;accesso alla versione beta, invia un&#39;e-mail a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). È richiesto l’accesso preesistente agli agenti in AEM.

#### Strumenti di intelligenza artificiale IDE per la migrazione da AEM 6.5 a AEM Cloud Service (programma Alpha) {#cm-ide-migration}

Accelera la migrazione da AEM 6.5 ad AEM as a Cloud Service (stack Java) utilizzando gli strumenti di intelligenza artificiale IDE per seguire le raccomandazioni del [rapporto di Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Per ulteriori informazioni, invia un&#39;e-mail a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com).

#### Autenticazione Edge per Edge Delivery Services (programma Beta) {#edge-authentication}

L’Autenticazione edge consente di limitare l’accesso alle pagine Edge Delivery Services solo a coloro che si sono autenticati con il provider di identità (IdP). Ciò avviene distribuendo un file YAML di configurazione OpenID Connect (OIDC).

Se ti interessa, invia una e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso ed eventuali domande.

#### Distribuzioni di produzione canary per testare il codice prima di accettare il traffico live (programma Beta) {#canary-beta}

Convalida una build di produzione con traffico di prova esclusivamente interno prima di renderla disponibile agli utenti finali. Invia alla produzione, instrada solo il traffico canary (utilizzando un’intestazione speciale), monitora il comportamento, quindi passa al traffico live o ripristina la versione precedente, senza che ciò abbia un impatto sui clienti.

Distribuisci le versioni del codice in produzione, ma limitalo al traffico di test esclusivamente interno prima di decidere se accettare il traffico in tempo reale o ripristinare la versione precedente.

Invia un’e-mail a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) per richiedere l’accesso e condividere il feedback.

#### Snapshot per RDE (programma Beta) {#rde-snapshot-program}

In versione beta, gli ambienti di sviluppo rapido (RDE) supportano ora una funzione che consente di acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinato in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

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
