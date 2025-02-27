---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 754cb41ea59a44820c4bc283b859d660040971ab
workflow-type: ht
source-wordcount: '1750'
ht-degree: 100%

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

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.1.0) è il 30 gennaio 2025. La prossima versione (2025.2.0) è pianificata per il 4 marzo 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**I commenti per l’Editor frammenti di contenuto sono ora disponibili a livello generale**

Collabora facilmente con i colleghi durante la creazione di frammenti di contenuto AEM utilizzando il nuovo servizio per commenti modernizzato nell’Editor frammenti di contenuto AEM.
[Ulteriori informazioni](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment).

**Editor frammenti di contenuto e interfacce utente Amministratore, supporto per la versione aggiornata di AEM as a Cloud Service**

La versione minima supportata di AEM as a Cloud Service per le nuove interfacce utente Amministratore ed Editor frammenti di contenuto è ora 2023.8.13099. Le versioni precedenti al rilascio in disponibilità generale delle nuove interfacce utente non sono più supportate

### Programma per i primi utilizzatori {#sites-early-adopter}

**Frammenti di contenuto migliorati**

È stato migliorato il [riferimento del frammento di contenuto con riferimenti univoci basati su ID](/help/headless/graphql-api/uuid-reference-upgrade.md), per garantire che le query GraphQL per i singoli frammenti di contenuto possano rimanere stabili anche se il frammento è stato spostato in un’altra posizione. Questo è ora possibile con le query “ByID”. Mentre i percorsi possono cambiare, interrompendo potenzialmente le query “ByPath”, gli UUID sono stabili. I nuovi ID possono anche essere restituiti come proprietà in qualsiasi query o altra richiesta API applicabile. Limitazione corrente (2025.1): i riferimenti a pagina non sono ancora supportati con ID univoci. Se nei frammenti di contenuto si fa riferimento alle pagine, questa funzionalità non deve essere utilizzata. La rimozione della limitazione è pianificata per la prossima versione di AEM as a Cloud Service.

**OpenAPI REST di AEM per la distribuzione dei frammenti di contenuto**

[OpenAPI REST di AEM per la distribuzione dei frammenti di contenuto](/help/headless/aem-rest-openapi-content-fragment-delivery.md) è ora disponibile per AEM as a Cloud Service.

### Funzioni obsolete {#sites-deprecated}

#### Editor SPA {#spa-editor}

[L’editor SPA](/help/implementing/developing/hybrid/introduction.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 2025.1.0. Rimarrà supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless in AEM sono ora:

* [Editor universale](/help/edge/wysiwyg-authoring/authoring.md) per la modifica visiva.
* [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo.

#### Funzioni di PWA {#pwa-features}

[Le funzioni progressive delle web app (PWA)](/help/sites-cloud/authoring/sites-console/enable-pwa.md) per AEM Sites sono obsolete per i nuovi progetti a partire dalla versione 2025.1.0. Questa funzione rimane supportata per i progetti esistenti, ma non deve essere utilizzata per i nuovi progetti

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in AEM Assets {#new-features-assets}

**Modelli Dynamic Media**

Personalizza banner di immagini e testo in maniera immediata con un semplice Editor modelli di Dynamic Media WYSIWYG, incorporando l’URL in qualsiasi applicazione di prima parte o di terze parti, per promuovere esperienze altamente coinvolgenti con aggiornamenti dei contenuti dei banner in tempo reale.

![rappresentazioni dinamiche](/help/assets/assets/dm-templates-smart-text-resize.png)

**Rapporti sulle consegne Dynamic Media**

Ottieni informazioni dettagliate sulla consegna delle risorse effettuata con Dynamic Media, inclusi numero di consegna a livello di risorsa, informazioni sul referrer, percorsi della risorsa in AEM Assets e ID univoco della risorsa. Genera report per tutte le risorse nell’archivio AEM Assets o gerarchie di cartelle specifiche. Queste informazioni consentono di misurare il ROI delle risorse fornite, valutare le prestazioni dei canali e prendere decisioni informate per la gestione delle risorse.

![rappresentazioni dinamiche](/help/assets/assets/referrer.png)

**Multi-audio e più didascalie per Dynamic Media**

[Supporto tracce con più didascalie e multi-audio per video Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): è ora possibile aggiungere facilmente più didascalie e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono gestire anche le didascalie e le tracce audio da una singola scheda nell’interfaccia utente.

**Dynamic Adaptative Streaming con supporto HTTP**

Lancio del supporto per il nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato):

* Lo streaming adattivo (DASH/HLS) garantisce agli utenti una migliore esperienza di visualizzazione dei video.

* DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore

**Relazioni risorsa**

La vista risorse ora supporta la visualizzazione e la modifica delle relazioni tra risorse in un pannello semplificato Dettagli risorsa. Aggiungi facilmente relazioni come Origine e Derivata ai contenuti in modo che gli utenti possano trovare più efficacemente contenuti principali rilevanti.

**Rielaborazione risorse**

La vista risorse ora supporta la rielaborazione delle risorse disponibili in una cartella. È possibile scegliere di utilizzare l’opzione **Processo completo** oppure opzioni avanzate, ad esempio rappresentazioni di anteprima predefinite, metadati, flusso di lavoro di post-elaborazione e profilo di elaborazione.

### Funzionalità per Accesso anticipato in AEM Assets {#early-access-features-assets}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. Le didascalie vengono generate dall’audio originale, da eventuali tracce audio o didascalie aggiuntive fornite nella scheda “Didascalie e audio” della pagina delle proprietà video. Grazie al supporto di più di 60 lingue, le didascalie possono essere riviste e visualizzate in anteprima prima della pubblicazione del video.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-features}

#### Gestisci pubblicazione 

È possibile utilizzare il flusso di lavoro [Gestisci pubblicazione](/help/forms/manage-publication.md#publish-forms-using-the-manage-publication-option) per pubblicare o annullare la pubblicazione di moduli in ambienti diversi, in genere dall’istanza di authoring a quelle di pubblicazione e anteprima. Consente agli utenti di pubblicare, annullare o pianificare la pubblicazione dei contenuti in modo semplice.

#### Salvataggio automatico di una bozza per moduli adattivi basati su Componenti core

Gli utenti possono ora beneficiare di una [funzione di salvataggio automatico](/help/forms/save-core-component-based-form-as-draft.md) che consente di salvare automaticamente come bozza un modulo parzialmente completato. L’utente potrà quindi completare in un secondo momento la compilazione del modulo, anche da un altro dispositivo. Questa funzione migliora i tassi di conversione per le organizzazioni riducendo l’abbandono dei moduli, in quanto gli utenti non devono ricominciare a compilarli dall’inizio.

#### Miglioramenti dell’editor di regole

Per moduli adattivi basati su Componenti core, puoi utilizzare l’[output del servizio di chiamata per popolare le opzioni a discesa e impostare un pannello ripetibile o singolo](/help/forms/invoke-service-enhancements-rule-editor.md). Inoltre, tale output può essere utilizzato per convalidare altri campi.

#### Esperienza utente con i pulsanti di navigazione nei layout dei pannelli migliorata

È ora possibile aggiungere pulsanti di navigazione ai layout del pannello, ad esempio Schede orizzontali, Schede verticali, Pannello a soffietto o Procedura guidata. Questi pulsanti [migliorano l’esperienza utente semplificando il passaggio da un pannello a un altro e concentrandosi sul pannello selezionato](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button).


### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Modelli e-mail per HTML nei moduli adattivi

I moduli adattivi consentono di utilizzare [modelli e-mail HTML](/help/forms/html-email-templates-in-adaptive-forms.md). I modelli e-mail HTML consentono di inviare e-mail avanzate, personalizzate e visivamente accattivanti quando viene inviato un modulo. Queste e-mail possono essere personalizzate con i dati del modulo e migliorate utilizzando vari tag e-mail, come immagini e collegamenti. Con i Moduli adattivi, è possibile caricare un file contenente un modello HTML o utilizzare un editor di testo normale per creare questi modelli.

![Modello e-mail HTML](/help/forms/assets/html-email.png)

#### Supporto di archiviazione cloud migliorato: caricamento diretto di PDF nell’archiviazione BLOB di Azure

Le API per la generazione di documenti di AEM Forms ora consentono di [caricare direttamente i documenti PDF generati nell’archiviazione BLOB di Azure](/help/forms/early-access-ea-features.md#doc-generation-api). Questo miglioramento semplifica l’archiviazione e il recupero, migliorando l’efficienza e l’integrazione con i flussi di lavoro cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto Java 21 {#java21}

È ora possibile generare il codice con Java 21, che include nuove funzioni (ad esempio, corrispondenza dei pattern per le istruzioni switch, classi sigillate) e miglioramenti delle prestazioni; sono ora supportate anche le build Java 17. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti di runtime di Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Il **runtime** Java 21 verrà distribuito gradualmente in **tutti** gli ambienti (oltre a quelli già costruiti con Java 17 o 21, che dispongono già del runtime Java 21), a partire da sandbox e dev/RDE, a febbraio, e in seguito in quelli di staging/produzione, ad aprile.

### Programmi sandbox con supporto per le pipeline di configurazione {#sandbox-config-pipelines}

I programmi sandbox ora supportano le pipeline di configurazione, che possono essere configurate in Cloud Manager per distribuire file yaml persistenti in Git.

[Ulteriori informazioni](/help/operations/config-pipeline.md) sulle pipeline di configurazione, che consentono la configurazione della CDN, sull’inoltro dei registri e sulle attività di manutenzione relative all’eliminazione del registro di controllo e alla pulizia delle versioni.

### API basate su OpenAPI - Programma per i primi utilizzatori {#open-apis-earlyadopter}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguono le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione vengono generate creando progetti Adobe Developer Console.

Scopri di più sulle [API AEM basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) che ne illustra la configurazione e l’utilizzo.

In concreto, gli endpoint API elencati di seguito sono disponibili come parte di un programma per i primi utilizzatori. Per partecipare, inviare un’e-mail all’indirizzo [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con la descrizione di come si intende utilizzarli.

* [API per frammenti di contenuto di Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API di Sites e cartelle di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API di comunicazione di Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Adobe vorrebbe ricevere commenti sull’utilità di questa tecnologia per i progetti Pubblica consegna AE e Edge Delivery Services. Inoltre, il modo in cui pensi di utilizzarla per contribuire alla roadmap. Invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con domande e commenti.

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore i feedback. Si possono inviare via e-mail all’indirizzo [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com).

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-0-release/whats-new-2024-10-0).

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
