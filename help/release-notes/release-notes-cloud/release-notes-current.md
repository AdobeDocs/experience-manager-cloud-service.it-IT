---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a2f26e7befe4aa23350cfdca6a2c342500a909db
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 46%

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

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.2.0) è il mercoledì 4 marzo 2025. La prossima versione (2025.3.0) è pianificata per il venerdì 27 marzo 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni di AEM Sites {#new-features-sites}

**Assegnazione automatica tag ai frammenti di contenuto**

Durante la creazione di frammenti di contenuto, ora è possibile ereditare automaticamente i tag assegnati al modello di contenuto. Questo consente una potente classificazione automatica dei contenuti memorizzati nei frammenti di contenuto.

**Supporto UUID frammento di contenuto**

Il supporto UUID dei frammenti di contenuto è ora disponibile in versione GA. La nuova funzionalità non modifica il comportamento basato sui percorsi delle operazioni all’interno di AEM, come spostamento, ridenominazione, rollout, in cui i percorsi vengono regolati automaticamente, ma può rendere più semplice e stabile il consumo esterno di frammenti di contenuto, soprattutto quando si utilizzano query GraphQL che eseguono direttamente il targeting di singoli frammenti con query ByPath. Tali query possono interrompersi se cambia il percorso di un frammento. Quando si utilizza il nuovo tipo di query ById, la query ora rimane stabile in quanto l’UUID di un frammento non cambia nei casi in cui i percorsi lo facciano.

**Dynamic Media con supporto OpenAPI nell&#39;Editor frammenti di contenuto e in GraphQL**

I Assets memorizzati in programmi AEM as a Cloud Service diversi dai frammenti di contenuto e abilitati con la nuova funzionalità Dynamic Media con OpenAPI possono ora essere utilizzati nei frammenti di contenuto. Il selettore delle immagini nel nuovo Editor frammenti di contenuto ora consente di selezionare archivi &quot;remoti&quot; come origine per le risorse di immagini a cui fare riferimento nel frammento. E alla consegna di tali frammenti di contenuto tramite AEM GraphQL, la risposta JSON ora include le proprietà richieste per le risorse remote (assetId, repositoryId), in modo che le applicazioni client possano creare i rispettivi Dynamic Media con URL OpenAPI per recuperare l’immagine.

**Rollout dell&#39;Editor frammenti di contenuto**

Continueremo ad abilitare il nuovo Editor frammenti di contenuto basato sull’interfaccia utente di Spectrum in AEM as a Cloud Service. Dopo essere diventato predefinito per tutti gli ambienti di sviluppo di Cloud Service a novembre 2024, verrà impostato come predefinito per tutti gli ambienti di stage il 1° aprile 2025 e per tutti gli ambienti di produzione il 1° maggio 2025. In tutti i casi, gli utenti avranno ancora la possibilità di ripristinare l’Editor tradizionale dei frammenti di contenuto nell’interfaccia utente touch di AEM.

**API HTTP per la traduzione**

L’API REST HTTP di AEM Translation, che da un po’ è in prima modalità di adozione, ora è in GA. La documentazione è disponibile [qui](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/). L’API consente di automatizzare i passaggi richiesti nel processo di gestione della traduzione dei contenuti in AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in AEM Assets {#new-features-assets}

**Nuova struttura di pacchetto Dynamic Media**

È ora disponibile una nuova struttura di packaging Dynamic Media per allinearsi meglio alle aspettative di mercato e supportare il tracciamento. La nuova struttura di confezionamento comprende:

* Dynamic Media Prime, che include Dynamic Media con OpenAPI e video per migliorare la distribuzione.

* Dynamic Media Ultimate aggiunge funzioni di consegna e trasformazione per soddisfare i requisiti di utilizzo più severi.

Per beneficiare della nuova struttura di packaging, è necessario disporre di Assets as a Cloud Service Prime o Ultimate.

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo sottotitoli accurati. I sottotitoli vengono generati dall&#39;audio originale, eventuali tracce audio aggiuntive o sottotitoli aggiuntivi vengono forniti nella scheda &quot;Sottotitoli e audio&quot; della pagina delle proprietà video. Grazie al supporto di più di 60 lingue, le didascalie possono essere riviste e visualizzate in anteprima prima della pubblicazione del video.

**Personalizzare i filtri di ricerca**

I filtri di ricerca personalizzati migliorano la precisione e l’efficienza nella ricerca di informazioni rilevanti. Consente ricerche più personalizzate, filtrando i dati in base ad attributi specifici come brand, prodotto, categoria o altri identificatori chiave. Ciò migliora l’organizzazione, riduce il tempo impiegato per il vaglio attraverso risultati irrilevanti e consente un processo decisionale più rapido. Supporta anche la scalabilità, in quanto i set di dati di grandi dimensioni diventano più facili da navigare e analizzare.

![personalizza filtri di ricerca](/help/assets/assets/custom-search-filters.png)


### Funzioni di accesso anticipato in Content Hub {#early-access-content-hub}

Content Hub ora consente di visualizzare e scaricare le rappresentazioni dinamiche e di ritaglio avanzato, oltre alle rappresentazioni statiche esistenti. In qualità di amministratore di Content Hub, puoi anche configurare la disponibilità di queste rappresentazioni per gli utenti utilizzando l’interfaccia utente di configurazione.

![rappresentazioni dinamiche](/help/assets/assets/download-single-asset-renditions-dynamic.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Modelli e-mail HTML in Forms adattivo

Forms adattivo consente di utilizzare [modelli e-mail HTML](/help/forms/html-email-templates-in-adaptive-forms.md). I modelli e-mail HTML consentono di inviare e-mail avanzate, personalizzate e visivamente accattivanti quando viene inviato un modulo. Queste e-mail possono essere personalizzate con i dati del modulo e migliorate utilizzando vari tag e-mail, come immagini e collegamenti. Con i Moduli adattivi, è possibile caricare un file contenente un modello HTML o utilizzare un editor di testo normale per creare questi modelli.

![Modello e-mail HTML](/help/forms/assets/html-email.png)

#### Supporto di archiviazione cloud migliorato: caricamento diretto di PDF nell’archiviazione BLOB di Azure

Le API di generazione documenti di AEM Forms ora consentono di [caricare direttamente i documenti PDF generati](/help/forms/early-access-ea-features.md#doc-generation-api) nell&#39;archiviazione BLOB di Azure. Questo miglioramento semplifica l’archiviazione e il recupero, migliorando l’efficienza e l’integrazione con i flussi di lavoro cloud.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto Java 21 {#java21}

Come indicato nelle note sulla versione di gennaio, ora è possibile creare il codice con Java 21, che include nuove funzioni (ad esempio, corrispondenza dei pattern per le istruzioni switch, classi sigillate) e miglioramenti delle prestazioni; sono ora supportate anche le build Java 17. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti di runtime di Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> A febbraio, il runtime **runtime** di Java 21 è stato distribuito in ambienti dev/RDE (oltre a quelli già generati con Java 17 o 21, che hanno già il runtime Java 21). Java 21 verrà applicato agli ambienti di staging/produzione in aprile.

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Adobe ti invita a scoprire se questa tecnologia è utile per i progetti AEM Publish Delivery e Edge Delivery Services. Inoltre, fateci sapere a cosa pensate di utilizzarlo come input nella roadmap del prodotto.

Alcuni possibili casi d’uso:
* Autenticazione con un IdP per controllare l’accesso al contenuto
* Rendering di contenuti dinamici (personalizzati, localizzati) in base alla geolocalizzazione, al tipo di dispositivo, agli attributi utente e così via.
* Manipolazione avanzata delle immagini
* Middleware tra la rete CDN e un’origine
* Un livello tra il browser e un’API di terze parti, ad esempio per riformattare la risposta API
* Aggregazione di dati da più origini per facilitare il rendering da parte del browser client

Invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con domande e commenti.

### API basate su OpenAPI - Programma per i primi utilizzatori {#open-apis-earlyadopter}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguono le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione vengono generate creando progetti Adobe Developer Console.

Scopri di più sulle [API AEM basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) che ne illustra la configurazione e l’utilizzo.

In concreto, gli endpoint API elencati di seguito sono disponibili come parte di un programma per i primi utilizzatori. Per partecipare, inviare un’e-mail all’indirizzo [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con la descrizione di come si intende utilizzarli.

* [API per frammenti di contenuto di Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API di Sites e cartelle di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API di comunicazione di Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore i feedback. Si possono inviare via e-mail all’indirizzo [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com).

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

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
