---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 827077d8dd39520a74992907134e0466b7beb648
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 47%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.8.0) è il venerdì 28 agosto 2025. La prossima versione funzionale (2025.9.0) è pianificata per il venerdì 25 settembre 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) è il punto di partenza centralizzato per accedere a tutte le funzionalità di AEM. È personalizzato in base alla persona utente e alle licenze disponibili, consentendo a ogni utente di raggiungere i propri risultati in modo efficiente.

## Assistente AI in AEM {#AI-assistant}

L&#39;[Assistente AI](/help/implementing/cloud-manager/ai-assistant-in-aem.md) per AEM offre un&#39;interfaccia di conversazione progettata per ottenere risposte immediate alle domande relative al prodotto AEM (*disponibile per tutti gli utenti*) e automatizzare la creazione di ticket di supporto (*disponibile per gli amministratori del supporto*). È direttamente incorporato in AEM e accessibile dall’interfaccia utente di AEM Experience Hub, Cloud Manager e Author.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Experience Manager Sites {#enhancements-sites}

* Nell’interfaccia utente di amministrazione dei frammenti di contenuto ora è possibile visualizzare lo stato del flusso di lavoro per i frammenti di contenuto, con informazioni dettagliate sui flussi di lavoro passati e attualmente in esecuzione per un frammento selezionato.
* Le prestazioni per l’apertura di frammenti di contenuto nel nuovo editor di frammenti di contenuto sono state aumentate del 25% negli scenari comuni aprendo i frammenti tramite UUID anziché tramite il percorso.
* Quando si copiano frammenti di contenuto con frammenti di riferimento, le copie dei frammenti di riferimento ora vengono memorizzate nella stessa posizione della copia del frammento principale.
* Ora puoi configurare un’area di lavoro personalizzata nelle impostazioni della cartella per esportare i frammenti di contenuto nell’area di lavoro configurata in Adobe Target.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in Content Hub {#new-features-content-hub}

**Ricerca in blocco tramite le proprietà filtro**

Content Hub consente ora di individuare più rapidamente le risorse necessarie. Con la nuova funzionalità di ricerca in blocco, puoi immettere più valori per qualsiasi proprietà di filtro, separati da un delimitatore (ad esempio, più ID SKU), e recuperare immediatamente tutte le risorse corrispondenti utilizzando una singola ricerca.

### Nuove funzioni di Dynamic Media con funzionalità OpenAPI {#new-features-dynamic-media-with-openapi}

**DM compatibile SEO con URL OpenAPI**

Crea URL personalizzati per la consegna delle risorse in DM con OpenAPI, sostituendo gli UUID lunghi generati dal sistema con identificatori brevi e leggibili. In questo modo i collegamenti SEO sono più facili da usare e meglio allineati con il marchio o le campagne. Gli URL personalizzati si risolvono automaticamente nell’UUID della risorsa originale in fase di esecuzione senza interrompere i flussi di lavoro esistenti.

>[!NOTE]
>
>Questa funzione sarà disponibile come funzionalità a disponibilità limitata il 10 settembre. Puoi [creare e inviare un caso di assistenza clienti Adobe](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per abilitarlo per la distribuzione.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-features}

* [Componente input data e ora](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component): è ora disponibile un componente data e ora che consente agli utenti di selezionare sia la data che l&#39;ora tramite un&#39;interfaccia calendario e orologio oppure immettendo manualmente i valori in un formato supportato.
* [Gestione avanzata degli errori per i caricamenti di file](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab): il componente File allegato ora convalida automaticamente il tipo di file caricato in base all&#39;elenco Consentiti. Se un utente carica un file in un formato non supportato, il modulo mostra un errore durante l’invio. Il componente controlla anche il contenuto del file per convalidarne il tipo, migliorando la sicurezza complessiva del modulo.
* [Risposta di errore specificata per l&#39;azione di invio personalizzata](/help/forms/custom-submit-action-troubleshooting.md): quando un&#39;azione di invio personalizzata rileva un errore non gestito, viene restituito il codice di errore 502. Questo aiuta a identificare che il problema è correlato all’azione di invio personalizzata, semplificando il debug.
* [Esclusione dei campi nascosti dal documento record](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings): è stata aggiunta una nuova proprietà per consentire l&#39;esclusione dei campi nascosti dal documento record. Per impostazione predefinita, questa opzione non è selezionata e si applica a tutti i campi modulo.

### Funzioni pre-release in AEM Forms

* [Genera e sincronizza rappresentazioni AFP](/help/forms/document-generation-afp-api.md): ora puoi utilizzare l&#39;API di comunicazione di AEM Forms per convertire un file XDP in formato AFP. AFP è un formato ad alte prestazioni ampiamente utilizzato nella stampa aziendale su larga scala.
* **Miglioramenti nell&#39;editor di regole**
   * [Metodo di convalida nell&#39;elenco funzioni](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): i metodi di convalida e ripristino supportano ora l&#39;esecuzione a livello di pannello, campo e modulo. In precedenza, erano supportate solo a livello di modulo.
   * [Supporto moderno di JavaScript](/help/forms/rule-editor-core-components-difference-tables.md): è stato aggiunto il supporto per le funzioni personalizzate di ECMAScript 2019 e versioni successive, che consente di scrivere codice più efficiente, modulare e riutilizzabile
   * [Scarica opzione DoR nell&#39;editor di regole](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): una funzione per scaricare il documento di record (DoR) è stata aggiunta come opzione preconfigurata nell&#39;editor di regole.
     ![Documento di record](/help/forms/assets/document-of-record-rn.gif)
   * [Variabili dinamiche nell&#39;Editor regole](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): è ora possibile utilizzare variabili dinamiche (temporanee) nell&#39;Editor regole per una maggiore flessibilità nella definizione di condizioni e azioni. I campi nascosti non sono più necessari per memorizzare valori temporanei.
   * [Supporto di regole basate su eventi personalizzati](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): è ora possibile definire eventi personalizzati e attivare regole in base a tali eventi.
   * [Regole pannello ripetibili in base al contesto](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): nei pannelli ripetibili, le regole vengono ora eseguite in base al contesto, anziché essere applicate solo all&#39;ultima istanza del pannello.
   * [Regole attivate dai parametri](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): l&#39;editor di regole ora supporta l&#39;esecuzione di regole basate su parametri di query, parametri UTM o parametri del browser.
   * [Funzioni personalizzate specifiche del modulo](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): Edge Delivery Services Forms ora supporta gli script di funzioni personalizzate specifiche del modulo, fornendo maggiore flessibilità nella gestione della logica riutilizzabile.
   * [Importazioni statiche per funzioni personalizzate](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): l&#39;editor di regole in Universal Editor ora supporta le importazioni statiche, consentendo agli sviluppatori di organizzare, condividere e riutilizzare le funzioni in più moduli.

### Funzionalità per i primi utilizzatori di AEM Forms

* [Componente Firma scarabocchio](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature): è ora possibile utilizzare il componente Firma scarabocchio per consentire agli utenti di aggiungere le firme a un modulo, ad esempio in un modulo di contratto. Il componente consente agli utenti di disegnare la propria firma direttamente all’interno del modulo utilizzando un mouse, uno stilo o un touchscreen.
* [Integrazione API diretta nell&#39;editor di regole](/help/forms/api-integration-in-rule-editor.md): Forms adattivo ora supporta l&#39;integrazione API diretta nell&#39;editor di regole visive senza richiedere un modello dati modulo. Gli autori possono configurare le API utilizzando un’importazione URL o cURL, mappare i parametri di input/output e le chiamate sicure con l’autenticazione.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Aggiornamento compilazione JavaScript {#javascript-compilation}

La compilazione JavaScript predefinita lato client (clientlibs) ora esegue il targeting di ECMASCRIPT_2018 invece di ECMASCRIPT5. Anche se sostituibile in passato, questo aggiornamento consente miglioramenti delle prestazioni, una sintassi moderna di JavaScript e funzionalità per impostazione predefinita.

### Prossime versioni obsolete dell’API Java {#java-api-deprecation}

Diverse API obsolete eseguono il targeting della rimozione il 31 agosto e pertanto non è più necessario farvi riferimento. All’inizio di settembre, se viene rilevato l’utilizzo di API, verranno inviate notifiche al Centro operativo e dopo il 25 settembre verranno visualizzate notifiche durante le build di Cloud Manager per sottolineare l’importanza di rimuovere l’utilizzo. Per informazioni dettagliate, consulta l&#39;[articolo sugli elementi obsoleti](/help/release-notes/deprecated-removed-features.md#aem-apis). Per comodità, tuttavia, le seguenti API sono elencate di seguito:

<details>
  <summary>Espandi per visualizzare le API Java obsolete</summary>

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
</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Rimozione runtime Java 11 {#java11-runtime-deprecation}

Il *runtime Java 11* è ora obsoleto e la maggior parte degli ambienti è stata già aggiornata al runtime **Java 21** più performante.

Se non è stato possibile aggiornare l’ambiente a causa di dipendenze non supportate (consulta [Requisiti di runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), dovresti aver ricevuto un’e-mail da Adobe con i passaggi successivi specifici. Assicurati che tutti gli aggiornamenti richiesti siano completati entro il **1 ottobre 2025**, in modo che l&#39;ambiente possa essere aggiornato senza interruzioni.

Nota: la versione di runtime è separata dalla versione di build del codice. Sebbene consigliamo di creare con Java 21, le build Java 11 sono ancora supportate per il momento. In futuro verrà condiviso un avviso di rimozione separato per le build Java 11.

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dal **25 settembre**, le sostituzioni di registrazione personalizzate non supportate verranno ignorate. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe ha contattato tutti coloro la cui configurazione corrente potrebbe essere coinvolta.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di verbosità del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Elaborazione Edge (programma Beta) {#edge-computing}

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

Ora in versione beta, puoi distribuire una pipeline di configurazione per funzioni quali i selettori di origine CDN, le trasformazioni di risposta e richiesta, l’inoltro del registro CDN e altro ancora. Rivolgiti a [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con i dettagli del tuo caso d’uso.

### Istantanee per RDE (programma Alpha) {#rde-snapshot-program}

In Alpha, gli ambienti di sviluppo rapido (RDE) ora supportano una funzione per acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinata in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un’e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se ti interessa fornire un feedback su questa funzione.

### Funzionalità di inoltro del registro di AEM a più destinazioni (programma Beta) {#log-forwarding-beta}

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ora in versione Beta, puoi inoltrare i registri di AEM a Amazon S3, Sumo Logic e al tuo account New Relic (non a quello fornito da Adobe). Per queste destinazioni di registrazione, sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

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
