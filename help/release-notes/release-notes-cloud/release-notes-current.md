---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 401eaaaa0bb8dad054c7105533cbd4486964c484
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 49%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.7.0) è il venerdì 7 agosto 2025. La prossima versione funzionale (2025.8.0) è pianificata per il venerdì 28 agosto 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440928?quality=12&captions=ita)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Experience Manager Sites {#enhancements-sites}

* È ora possibile copiare frammenti di contenuto con frammenti di riferimento (elementi secondari) in un’unica operazione. Ciò consente di riutilizzare le strutture dei frammenti di contenuto esistenti per creare nuovi contenuti.
* Nell’interfaccia utente di amministrazione dei frammenti di contenuto ora è possibile visualizzare lo stato del flusso di lavoro per i frammenti di contenuto, con informazioni dettagliate sui flussi di lavoro passati e attualmente in esecuzione per un frammento selezionato.
* Ora la ridenominazione o lo spostamento di una pagina Live Copy di origine attiva la ripubblicazione di una pagina Live Copy rinominata o spostata di conseguenza.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Aggiungere forme ai modelli Dynamic Media**

È ora possibile [aggiungere livelli forma ai modelli Dynamic Media](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas) in Experience Manager Assets. Analogamente ai livelli immagine e testo, i livelli forma supportano i parametri per gli aggiornamenti in tempo reale tramite l’URL del modello. Nei modelli è inoltre possibile includere collegamenti call-to-action (CTA) alle forme.

![Aggiungi forme ai modelli Dynamic Media](/help/assets/assets/enable-uniform-radius-shape.png)

**Miglioramenti ai metadati generati da IA**

AEM Assets ora consente di [configurare la visualizzazione dei titoli delle risorse nella vista a schede o nella vista a elenco](/help/assets/smart-tags.md#configure-ai-generated-titles) nella pagina Sfoglia risorse. Puoi scegliere di visualizzare il titolo della risorsa definito dall’utente, il titolo generato tramite IA o utilizzare il titolo generato tramite IA solo se non è presente alcun titolo per la risorsa.

![Configura titoli generati da IA](/help/assets/assets/configure-title-ai-generated.png)

Ora puoi anche scegliere di disabilitare i metadati generati dall’intelligenza artificiale a livello di cartella.

### Nuove funzioni in Content Hub {#new-features-content-hub}

**Maggiore flessibilità di branding in Content Hub**

Basandosi sulle funzioni di personalizzazione esistenti, Content Hub consente ora agli amministratori di personalizzare ulteriormente la propria implementazione aggiungendo immagini con logo personalizzati. È stato aggiunto il supporto per il formato di file TIFF sia per le immagini del banner che per quelle del logo, consentendo una maggiore flessibilità di progettazione.

**Condivisione più intelligente con collegamenti con titolo**

È ora possibile aggiungere un titolo durante la generazione di un collegamento condiviso, dalla vista dei dettagli della risorsa o dopo aver selezionato una o più risorse. In questo modo i destinatari possono identificare facilmente lo scopo di ogni collegamento, in particolare quando ricevono più risorse condivise.

![collegamento pubblico e privato](/help/assets/assets/shared-link-for-assets.png)

**Navigazione filtro migliorata**

Content Hub ora include un&#39;opzione **Mostra tutto** all&#39;interno dei filtri, che consente agli utenti di visualizzare tutti i facet disponibili insieme al numero di risorse, a partire dall&#39;attuale limite di visualizzazione di un massimo di dieci facet. Le funzionalità avanzate di ricerca e ordinamento all’interno di ciascun filtro semplificano l’individuazione e la gestione delle risorse in modo più efficiente.

### App desktop AEM versione 3.0.0 {#desktop-app-release-3.0.0}

Caricamento automatizzato di nuovi file e cartelle, operazioni avanzate sui file, individuazione più intelligente delle risorse e integrazione perfetta con AEM, per una gestione dei contenuti più rapida, chiara e intuitiva.

Per l&#39;elenco completo delle funzionalità, vedere [Note sulla versione dell&#39;app desktop](https://experienceleague.adobe.com/it/docs/experience-manager-desktop-app/using/release-notes).

### Nuove funzioni di Dynamic Media con funzionalità OpenAPI {#new-features-dynamic-media-with-openapi}

**Anteprima risorse prima della pubblicazione**

[!DNL Dynamic Media with OpenAPI capabilities] ora consente di visualizzare in anteprima le risorse direttamente nelle pagine di authoring di [!DNL AEM Sites] prima di renderle pubbliche. Condividi le pagine di anteprima con le parti interessate per raccogliere feedback sulla qualità visiva e sull’adattamento contestuale. Durante il ciclo di revisione, puoi creare e gestire più versioni di risorse prima di finalizzarle per la pubblicazione.

**Imaging avanzato per richieste di immagini OpenAPI**

Tutte le richieste di immagini OpenAPI ora sfruttano completamente la tecnologia Smart Imaging con logica di fallback e promozione automatica. Questo miglioramento ottimizza le immagini in base alle condizioni del dispositivo e della rete, offrendo caricamenti di pagina più rapidi e un utilizzo ridotto della larghezza di banda, mantenendo al contempo la qualità visiva.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-features}

**Editor universale per Forms adattivo e frammenti di moduli**

L&#39;[Editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ora supporta la creazione sia di Forms adattivo che di frammenti di moduli riutilizzabili. Gli autori possono creare moduli visivamente, configurare azioni di invio e aggiungere la convalida reCAPTCHA, il tutto in un ambiente di authoring WYSIWYG semplificato. Questa funzionalità accelera la creazione di moduli, ne incrementa la coerenza e ne migliora la protezione contro spam e abusi automatizzati.

![Editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


**Servizio di invio Forms per Edge Delivery Services Forms**

Vedere [Servizio di invio Forms](/help/forms/forms-submission-service.md). consente di memorizzare facilmente i dati provenienti dall’invio di moduli adattivi direttamente nelle piattaforme di fogli di calcolo più diffuse, come Google Sheets, Microsoft OneDrive o SharePoint. Questa integrazione semplifica la gestione dei dati consentendo l’invio diretto dei dati del modulo al foglio di calcolo scelto, eliminando il trasferimento manuale dei dati e riducendo gli errori.

I vantaggi principali includono:

* **Integrazione diretta:** Configura i moduli per inviare i dati direttamente a un foglio di calcolo specificato.
* **Mappatura dati personalizzati:** Mappatura dei campi modulo alle colonne del foglio di calcolo corrispondenti per l&#39;archiviazione organizzata.
* **Controllo degli accessi:** Sfrutta le autorizzazioni esistenti per i fogli di calcolo per gestire gli utenti che possono accedere ai dati inviati o modificarli.

**Genera e sincronizza copie trasformate AFP da Forms adattivo**

L&#39;API di sincronizzazione output [AFP](/help/forms/document-generation-afp-api.md) consente agli amministratori e agli utenti di generare output AFP (Advanced Function Presentation) da Adaptive Forms e di sincronizzare l&#39;output con i sistemi esterni o i percorsi di archiviazione. AFP è un formato di documento ad alte prestazioni ottimizzato per la stampa, spesso utilizzato in ambienti aziendali di larga scala.

<!-- ### New pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

 -->

### Nuove funzioni di accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma di accesso anticipato di AEM Forms offre un’opportunità unica per ottenere accesso esclusivo alle innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).


<!-- **Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**Editor regole per l&#39;editor comunicazioni interattive**

Creare azioni dinamiche e basate sui dati direttamente all&#39;interno dei documenti mediante un&#39;interfaccia intuitiva e intuitiva. Definisci facilmente la logica condizionale, automatizza i flussi di lavoro e personalizza i contenuti senza scrivere codice.

**CLI di AEM Forms Scaffolder per i componenti personalizzati**

>[!VIDEO]&#x200B;(https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component generator-aem-forms cli-aem-forms custom component-aem-forms)

Accelera lo sviluppo di AEM Forms Edge Delivery Services con questo strumento CLI. Genera all&#39;istante il codice e il cablaggio necessari per avviare lo sviluppo di componenti personalizzati, senza problemi.

**Strumento di integrazione API per dati modulo dinamico**

Lo strumento di integrazione API consente agli autori dei moduli di creare moduli dinamici e intelligenti che recuperano e compilano automaticamente i dati dalle API REST esterne in base alle interazioni degli utenti. Questa funzionalità di integrazione senza codice trasforma i moduli statici in interfacce di raccolta dati dinamiche.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Visualizzazione nodo per la gestione delle autorizzazioni {#node-view}

AEM introduce la funzione di gestione delle autorizzazioni nella vista Nodo. La funzionalità principale rimane la stessa dell’interfaccia classica, ma è più semplice ed efficiente. Per ulteriori informazioni, consulta l&#39;[articolo dedicato](/help/security/touch-ui-principal-view.md).

### Processo di rimozione aggiornato {#updated-deprecation-process}

Adobe esamina regolarmente funzioni, librerie, API e configurazioni per garantire che soddisfino gli standard in termini di prestazioni, sicurezza e valore. Quando le funzionalità non soddisfano più questi standard, vengono contrassegnate come obsolete e l’utilizzo ne deve essere interrotto entro una data di rimozione specificata. In attesa di tale data, Adobe lo ricorderà alla clientela tramite notifiche e-mail e azioni da eseguire in Cloud Manager, prima di procedere con le nuove build o di distribuirne di nuove. La mancata adozione delle misure necessarie può comportare l’impossibilità di eseguire l’aggiornamento a nuove versioni di AEM, generando potenziali impatti su sicurezza, prestazioni, affidabilità e disponibilità.

Per ulteriori informazioni, consulta l’articolo [Rimozione](/help/release-notes/deprecated-removed-features.md).

#### API Java obsolete e configurazione OSGi prossime alle date di rimozione {#deprecated-near-removals}

Espandi l’elenco seguente per visualizzare le API e le configurazioni OSGi obsolete che non devono più essere utilizzate. Per informazioni complete, comprese le timeline di rimozione, consulta l’articolo sulla rimozione.

<details>
  <summary>Espandi per visualizzare le rimozioni</summary>

API Java:

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

Proprietà OSGi:

* `org.apache.sling.commons.log.LogManager` (tutte le proprietà)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Rimozione runtime Java 11 {#java11-runtime-deprecation}

Il runtime **Java 11*- è ora obsoleto e la maggior parte degli ambienti è già stata aggiornata al runtime &#x200B;** Java 21** più performante.

Se non è stato possibile aggiornare l’ambiente a causa di dipendenze non supportate (consulta [Requisiti di runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), dovresti aver ricevuto un’e-mail da Adobe con i passaggi successivi specifici. Assicurati che tutti gli aggiornamenti richiesti siano completati entro il **28 agosto 2025**, in modo che l’ambiente possa essere aggiornato senza interruzioni.

Nota: la versione di runtime è separata dalla versione di build del codice. Sebbene consigliamo di creare con Java 21, le build Java 11 sono ancora supportate per il momento. In futuro verrà condiviso un avviso di rimozione separato per le build Java 11.

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dalla **fine di agosto**, qualsiasi sostituzione di registrazione personalizzata non supportate verrà ignorata. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe ha contattato tutti coloro la cui configurazione corrente potrebbe essere coinvolta.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di verbosità del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Eliminazione predefinita delle versioni precedenti e dei registri di controllo {#mt-defaults}

Attualmente, le attività di manutenzione *eliminazione- associate alle versioni dei contenuti e ai registri di audit sono disattivate per impostazione predefinita e, di conseguenza, i dati non vengono rimossi a meno che non siano configurati in modo esplicito.

Tuttavia, per ottimizzare le prestazioni dell’archivio, l’eliminazione sarà abilitata per impostazione predefinita in una data futura annunciata, seguendo queste linee guida:

#### Versioni di contenuto {#mt-content}

* **Nuovi ambienti*- (creati dopo una data futura (da comunicare in un secondo momento)
   * Le versioni precedenti a **30 giorni*- verranno eliminate periodicamente.
   * Vengono mantenute le cinque versioni più recenti degli ultimi 30 giorni, insieme alla versione più recente e a quella corrente, indipendentemente dalla loro età.

* **Ambienti esistenti*- (creati prima di questa data):
   * Le versioni precedenti a **7 anni*- verranno eliminate periodicamente.
   * Vengono mantenute tutte le versioni degli ultimi 7 anni.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare questi valori predefiniti tramite la configurazione YAML, distribuita mediante la pipeline di configurazione.

#### Registro di controllo {#mt-auditlogs}

* **Nuovi ambienti*- (creati dopo una data futura, che verrà comunicata separatamente):
   * I registri di replica, DAM e controllo pagina precedenti a **7 giorni*- verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.

* **Ambienti esistenti*- (creati prima di questa data):
   * I registri di replica, DAM e controllo delle pagine più vecchi di **7 anni*- verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare questi valori predefiniti tramite la configurazione YAML, distribuita mediante la pipeline di configurazione.

Per ulteriori dettagli, consulta l’articolo [Attività di manutenzione](/help/operations/maintenance.md#defaults).

### Edge Computing (programma Alpha) {#edge-computing}

Edge Computing consente di eseguire JavaScript a livello CDN, avvicinando l’elaborazione dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Autenticazione degli utenti con un provider di identità prima di concedere l’accesso al contenuto
* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end
* Esposizione di un server MCP per LLM come ChatGPT e Claude per accedere a strumenti personalizzati

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

### Configurazione rete CDN per Edge Delivery Services (programma Beta) {#cdn-eds-beta}

La rete CDN gestita da Adobe offre opzioni di configurazione flessibili, come descritto nell’articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#configurations).

Ora in versione beta, distribuisci una pipeline di configurazione per le funzioni che includono i selettori di origine CDN, le trasformazioni di risposta e richiesta, l’inoltro del registro CDN e altro ancora. Rivolgiti a [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con i dettagli del tuo caso d’uso.

### Snapshot per RDE (programma Alpha) {#rde-snapshot-beta}

In Alpha, gli ambienti di sviluppo rapido (RDE) ora supportano una funzione per acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinata in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un&#39;e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se sei interessato a fornire un feedback su questa funzione.

### Funzionalità di inoltro del registro di AEM a più destinazioni (programma Beta) {#log-forwarding-beta}

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ora in versione beta, puoi inoltrare i registri di AEM a Amazon S3, Sumo Logic, Dynatrace e al tuo account New Relic (non a quello fornito da Adobe). Per queste destinazioni di registrazione, sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

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
