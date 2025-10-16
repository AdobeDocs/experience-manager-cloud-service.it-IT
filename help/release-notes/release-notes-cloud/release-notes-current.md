---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 245ad07ba6abbf18e2011cb71a15948c9b92f80f
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 44%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.9.0) è il venerdì 25 settembre 2025. La prossima versione funzionale (2025.10.0) è pianificata per il venerdì 30 ottobre 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440928?captions=ita&quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Experience Manager Sites Prerelease {#prerelease-sites}

L’Editor modello di contenuto per Frammenti di contenuto di AEM è stato modernizzato per allinearlo ad altre interfacce basate su React Spectrum in AEM. L’implementazione dell’interfaccia utente e il modello di estensibilità sono ora coerenti con l’Editor frammento di contenuto e l’Editor universale. Il nuovo Editor modelli è ora predefinito quando viene aperto dalla nuova interfaccia utente di amministrazione del modello di contenuto. Quando si apre un modello di contenuto nell’interfaccia utente touch, si apre l’editor dell’interfaccia utente touch e si offre di provare il nuovo editor.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Assets {#new-features-assets-view}

**Formattazione testo avanzata con sottostringhe nei modelli Dynamic Media**

È ora possibile applicare la formattazione alle sottostringhe all’interno dei livelli di testo dei modelli Dynamic Media. Una parola o una frase selezionata viene trattata come un livello separato, che consente di regolarne il carattere, la dimensione, il colore e altro ancora. Il livello della sottostringa è parametrizzato in modo da poterlo aggiornare in tempo reale utilizzando l’URL di consegna del modello

### Nuove funzioni di Dynamic Media con funzionalità OpenAPI {#new-features-dynamic-media-with-openapi}

**URL di consegna risorse con marchio e leggibili**

Rendi Dynamic Media con gli URL OpenAPI più leggibili dall’utente sfruttando gli URL personalizzati in Dynamic Media con OpenAPI. Gli URL personalizzati consentono di sostituire lunghi UUID generati dal sistema e difficili da memorizzare negli URL di consegna delle risorse con identificatori brevi controllati dal brand. In questo modo gli URL personalizzati saranno più brevi, più facili da leggere e condividere e più allineati al tuo marchio o alle tue campagne. Gli URL personalizzati si risolvono automaticamente nell’UUID della risorsa originale in fase di esecuzione senza interrompere i flussi di lavoro esistenti.

>[!NOTE]
>
>Questa funzione è disponibile come funzione Disponibilità limitata. Puoi [creare e inviare un caso di assistenza clienti Adobe](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per abilitarlo per la distribuzione.

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

**Richiama il passaggio del flusso di lavoro del modello dati modulo per gli allegati dell&#39;elenco di SharePoint**

Il passaggio del flusso di lavoro Richiama modello dati modulo ora supporta la gestione dei metadati lato flusso di lavoro per gli array di allegati con codifica Base64 nei modelli dati modulo basati su elenco SharePoint. Con questo miglioramento, il passaggio del flusso di lavoro può trasmettere, archiviare e recuperare metadati quali nome file, tipo MIME e proprietà personalizzate per ogni allegato. Questa funzionalità consente una gestione dei dati più completa e agevola l’integrazione diretta a valle. Per informazioni dettagliate, vedere [Supporto avanzato nel passaggio del flusso di lavoro Richiama modello dati modulo per allegati elenco SharePoint](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step).

### Funzioni pre-release in AEM Forms

**Miglioramenti all&#39;editor di regole**

L’Editor regole ora supporta la navigazione avanzata e consente l’utilizzo di espressioni matematiche e funzionali nei parametri di input.

**Navigazione migliorata con supporto payload eventi**

L&#39;azione `Navigate To` nei gestori del servizio Invoke ora supporta `EVENT_PAYLOAD`, consentendo agli autori di moduli di configurare azioni di follow-up in base alle risposte agli eventi. Questo miglioramento offre una maggiore flessibilità nella progettazione dei flussi di lavoro dopo l’invio, garantendo transizioni più fluide ed esperienze utente più personalizzate. Per ulteriori informazioni, vedere [Navigazione avanzata con supporto payload eventi](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Supporto di espressioni matematiche e funzioni nei parametri di input**

I parametri di input ora supportano sia le chiamate di funzione che le espressioni matematiche, consentendo agli autori dei moduli di trasmettere direttamente i valori calcolati in modo dinamico. Questo miglioramento semplifica le configurazioni delle regole, elimina la necessità di campi aggiuntivi e rende i moduli più adattabili a scenari logici complessi e basati su calcoli. Per ulteriori informazioni, vedere [Supporto di espressioni matematiche e funzioni nei parametri di input](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters).

### Nuove funzioni per l’accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

**Anteprima PDF nell&#39;Editor comunicazioni interattive**

Gli utenti possono visualizzare in anteprima i PDF di comunicazione interattiva senza dati, con file di dati JSON locali o con dati provenienti da un modello di dati, consentendo test flessibili basati sui dati. Per ulteriori informazioni, vedere [Anteprima PDF nell&#39;Editor comunicazioni interattive](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md).

**Supporto di caratteri personalizzati nella comunicazione interattiva**

La funzione Font personalizzati consente agli utenti di incorporare font personalizzati o approvati dall’organizzazione nelle comunicazioni interattive, garantendo un rendering PDF coerente e personalizzato su dispositivi e piattaforme. Per ulteriori informazioni, vedere [Supporto di caratteri personalizzati nella comunicazione interattiva](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md).

**Importa ed esporta comunicazioni interattive**

Questa funzione consente la migrazione e il riutilizzo delle comunicazioni interattive in ambienti diversi. Ora puoi esportare una comunicazione interattiva con i frammenti e i modelli di dati associati da un ambiente e importarla in un altro. Per ulteriori informazioni, vedere [Importare ed esportare comunicazioni interattive](/help/forms/interactive-communication/import-and-export-interactive-communications.md).

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
>&#x200B;>Invia un&#39;e-mail a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) per attivarlo nei programmi.

### Nuova versione di AEM Developer Tools per Eclipse {#aem-develeper-tools-for-eclipse}

È stata rilasciata la versione 1.4.0 di AEM Developer Tools per Eclipse. Questa versione aggiunge il supporto per Eclipse IDE 2022-12 o versione successiva ed è stata convalidata con la versione corrente (2025-09). La strumentazione ora funziona con le versioni moderne dell’Archetipo progetto AEM e incorpora miglioramenti rispetto alla Sling IDE Tooling 1.3.0.

Installa da [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) e consulta la [pagina degli strumenti per sviluppatori di AEM](https://eclipse.adobe.com) per ulteriori dettagli.

### Prossime versioni obsolete dell’API Java {#java-api-deprecation}

Diverse API obsolete sono state contrassegnate per la rimozione il 31 agosto e pertanto non è più necessario farvi riferimento. Riceverai notifiche dal Centro operativo se nel codice viene rilevato un utilizzo API obsoleto e dopo il 13 novembre verranno visualizzati avvisi durante le build di Cloud Manager per sottolineare l’importanza di rimuovere l’utilizzo. Per informazioni dettagliate, consulta l’[articolo sulla rimozione](/help/release-notes/deprecated-removed-features.md#aem-apis). Per comodità, tuttavia, le seguenti API sono elencate di seguito:

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

Il runtime *Java 11* è obsoleto e la maggior parte degli ambienti è già stata aggiornata al runtime **Java 21** dalle prestazioni più elevate.

Se non è stato possibile aggiornare l&#39;ambiente a causa di dipendenze non supportate (vedi [Java 21 Runtime Requirements](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), dovresti aver ricevuto un&#39;e-mail da Adobe con i passaggi successivi. Come descritto qui, Adobe ha aggiornato gli ambienti **Dev** e **RDE** in data **18 settembre 2025** per consentirti di convalidare il sito e i processi e risolvere eventuali problemi. Gli aggiornamenti per **Stage** e **Produzione** procederanno il **14 ottobre 2025**.

>[!NOTE]
>
>La versione di runtime è separata dalla versione di build del codice. Mentre consigliamo di creare con Java 21, le build Java 11 sono ancora accettate per il momento. In futuro verrà condiviso un avviso di rimozione separato per le build Java 11.

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dal **30 ottobre**, le sostituzioni di registrazione personalizzate non supportate verranno ignorate. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe ha contattato tutti coloro la cui configurazione corrente potrebbe essere coinvolta.

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

Autenticazione Edge consente di limitare l’accesso alle pagine Edge Delivery Services solo a coloro che si sono autenticati con il provider di identità (IdP). Ciò si ottiene distribuendo un file YAML di configurazione OpenID Connect (OIDC).

Se sei interessato, invia una e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d&#39;uso e le domande che potresti avere.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Distribuzioni di produzione Canarie al codice di test prima di accettare il traffico live (programma Beta) {#canary-beta}

Convalida una build di produzione con traffico di test solo interno prima di esporla agli utenti finali. Spedisci alla produzione, instrada solo il traffico canary (utilizzando un&#39;intestazione speciale), monitora il comportamento, quindi promuovi al traffico live o ripristina lo stato precedente, senza influire sui clienti.

Distribuisci le versioni del codice in produzione, ma limitalo al solo traffico di test interno prima di decidere se accettare il traffico in tempo reale o eseguire il rollback.

Invia un&#39;e-mail a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) per richiedere l&#39;accesso e condividere i commenti.

### Istantanee per RDE (programma Alpha) {#rde-snapshot-program}

In Alpha, gli ambienti di sviluppo rapido (RDE) ora supportano una funzione per acquisire un’istantanea dello stato corrente del codice e del contenuto, che può essere ripristinata in un secondo momento. Questo può essere utile quando si sincronizza un codice che potrebbe essere necessario ripristinare o quando si passa da uno sviluppo di funzioni diverse all’altro. È inoltre possibile ripristinare solo il contenuto mutabile come punto di partenza noto per il test.

Invia un’e-mail a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se ti interessa fornire un feedback su questa funzione.

### Funzionalità di inoltro del registro di AEM a più destinazioni (programma Beta) {#log-forwarding-beta}

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ora in versione Beta, puoi inoltrare i registri di AEM a Amazon S3, Sumo Logic e al tuo account New Relic (non a quello fornito da Adobe). Per queste destinazioni di registrazione, sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

### Monitoraggio avanzato delle prestazioni delle applicazioni (APM) (programma Alpha) {#apm-alpha}

Per motivi di osservabilità, AEM Cloud Service attualmente supporta [New Relic One](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornito da Adobe e [Dynatrace](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gestito dal cliente. Mentre esploriamo il supporto per opzioni APM aggiuntive, inviaci un&#39;e-mail all&#39;indirizzo [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) con il tuo fornitore o tecnologia preferita, oltre a casi d&#39;uso.


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
