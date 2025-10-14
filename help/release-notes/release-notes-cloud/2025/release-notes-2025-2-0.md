---
title: Note sulla versione 2025.2.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2025.2.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: 403ffbede5438131d0b0e770215b990e2d16c018
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 96%

---

# Note sulla versione 2025.2.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2025.2.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.2.0) è il 4 marzo 2025. La prossima versione (2025.3.0) è pianificata per il 27 marzo 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di febbraio 2025 per un riepilogo delle funzioni aggiunte nella versione 2025.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in AEM Sites {#new-features-sites}

**Assegnazione tag automatica per frammento di contenuto**

Durante la creazione di frammenti di contenuto, ora è possibile ereditare automaticamente i tag assegnati al modello di contenuto. Questo consente una potente classificazione automatica dei contenuti memorizzati nei frammenti di contenuto.

**Supporto UUID per frammento di contenuto**

Il supporto UUID per frammenti di contenuto è ora in disponibilità generale. La nuova funzionalità non modifica il comportamento basato sui percorsi delle operazioni all’interno di AEM, come spostamento, ridenominazione, rollout, in cui i percorsi vengono regolati automaticamente, ma può rendere più semplice e stabile il consumo esterno di frammenti di contenuto, soprattutto quando si utilizzano query GraphQL che eseguono direttamente il targeting di singoli frammenti con query ByPath. Tali query possono interrompersi se cambia il percorso di un frammento. Quando si utilizza il nuovo tipo di query ById, la query ora rimane stabile in quanto l’UUID di un frammento non cambia nei casi in cui siano i percorsi a cambiare.

**Dynamic Media con supporto OpenAPI nell’Editor frammento di contenuto e in GraphQL**

Le risorse memorizzate in programmi AEM as a Cloud Service diversi dai frammenti di contenuto e che sono abilitate con la nuova funzionalità Dynamic Media con OpenAPI possono ora essere utilizzate nei frammenti di contenuto. Il selettore delle immagini nel nuovo Editor frammento di contenuto ora consente di selezionare archivi “remoti” come origine per le risorse di immagini a cui fare riferimento nel frammento. E alla consegna di tali frammenti di contenuto tramite AEM GraphQL, la risposta JSON ora include le proprietà richieste per le risorse remote (assetId, repositoryId), in modo che le applicazioni client possano creare i rispettivi Dynamic Media con URL OpenAPI per recuperare l’immagine.

**Rollout dell’Editor frammento di contenuto**

Continueremo ad abilitare il nuovo [Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md) in AEM as a Cloud Service utilizzando [Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) (tramite Spectrum-UI). Dopo essere diventato predefinito per tutti gli ambienti per sviluppatori di Cloud Service a novembre 2024, verrà impostato come predefinito per tutti gli ambienti di staging il 1° aprile 2025 e per tutti gli ambienti di produzione il 1° maggio 2025. In tutti i casi, gli utenti avranno ancora la possibilità di ripristinare l’editor tradizionale frammento di contenuto nell’interfaccia touch in AEM.

**API HTTP di traduzione**

L’API REST HTTP di traduzione AEM, solo per i primi utilizzatori per un certo periodo, adesso è in disponibilità generale. La documentazione è disponibile [&#x200B; qui.](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/translation/) L&#39;API consente di automatizzare i passaggi richiesti nel processo di gestione della traduzione per il contenuto in AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in AEM Assets {#new-features-assets}

**Nuova struttura di pacchetto Dynamic Media**

È ora disponibile una nuova struttura di pacchetto Dynamic Media per allinearsi meglio alle aspettative di mercato e supportare il tracciamento. La nuova struttura di pacchetto comprende:

* Dynamic Media Prime, che include Dynamic Media con OpenAPI e video per migliorare la consegna.

* Dynamic Media Ultimate aggiunge funzioni di consegna e trasformazione per soddisfare i requisiti di utilizzo più severi.

Per usufruire della nuova struttura di pacchetto, è necessario disporre di Assets as a Cloud Service Prime o Ultimate.

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate. Le didascalie vengono generate dall’audio originale, eventuali tracce audio o didascalie aggiuntive sono fornite nella scheda “Didascalie e audio” nella pagina delle proprietà video. Grazie al supporto di più di 60 lingue, le didascalie possono essere riviste e visualizzate in anteprima prima della pubblicazione del video.

**Personalizzare i filtri di ricerca**

I filtri di ricerca personalizzati migliorano la precisione e l’efficienza nella ricerca di informazioni rilevanti. Consentono ricerche più personalizzate, filtrando i dati in base ad attributi specifici come brand, prodotto, categoria o altri identificatori chiave. Questo migliora l’organizzazione, riduce il tempo impiegato per il filtro dei risultati irrilevanti e consente un processo decisionale più rapido. Supporta anche la scalabilità, in quanto diventa più facile accedere e analizzare i set di dati di grandi dimensioni.

![personalizzare filtri di ricerca](/help/assets/assets/custom-search-filters.png)

### Funzionalità per Accesso anticipato a Content Hub {#early-access-content-hub}

Content Hub ora consente di visualizzare e scaricare le rappresentazioni dinamiche e con ritaglio avanzato, oltre alle rappresentazioni statiche esistenti. In qualità di amministratore di Content Hub, è possibile anche configurare la disponibilità di queste rappresentazioni per gli utenti che utilizzano l’interfaccia utente per la configurazione.

![rappresentazioni dinamiche](/help/assets/assets/download-single-asset-renditions-dynamic.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Modelli e-mail per HTML nei moduli adattivi

I moduli adattivi consentono di utilizzare [modelli e-mail HTML](/help/forms/html-email-templates-in-adaptive-forms.md). I modelli e-mail HTML consentono di inviare e-mail avanzate, personalizzate e visivamente accattivanti quando viene inviato un modulo. Queste e-mail possono essere personalizzate con i dati del modulo e migliorate utilizzando vari tag e-mail, come immagini e collegamenti. Con i Moduli adattivi, è possibile caricare un file contenente un modello HTML o utilizzare un editor di testo normale per creare questi modelli.

![Modello e-mail HTML](/help/forms/assets/html-email.png)

#### Supporto di archiviazione cloud migliorato: caricamento diretto di PDF nell’archiviazione BLOB di Azure

Le API per la generazione di documenti di AEM Forms ora consentono di [caricare direttamente i documenti PDF generati](/help/forms/early-access-ea-features.md#doc-generation-api) nell’archiviazione BLOB di Azure. Questo miglioramento semplifica l’archiviazione e il recupero, migliorando l’efficienza e l’integrazione con i flussi di lavoro cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Supporto Java 21 {#java21}

Come indicato nelle note sulla versione di gennaio, ora è possibile generare il codice con Java 21, che include nuove funzioni (ad esempio, corrispondenza dei pattern per le istruzioni switch, classi sigillate) e miglioramenti delle prestazioni; sono ora supportate anche le build di Java 17. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti di runtime di Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> A febbraio, il **runtime** di Java 21 è stato distribuito in ambienti dev/RDE (oltre a quelli già generati con Java 17 o 21, che dispongono già del runtime di Java 21). Java 21 verrà applicato agli ambienti di staging/produzione nel mese di aprile.

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Adobe desidera ricevere commenti sull’utilità di questa tecnologia per i progetti Pubblica cosegna AEM e Edge Delivery Services. Inoltre, il modo in cui pensi di utilizzarla per contribuire alla roadmap.

Alcuni possibili casi d’uso:
* Autenticazione con un IdP per ottenere l’accesso al contenuto
* Rendering di contenuti dinamici (personalizzati, localizzati) in base alla geolocalizzazione, al tipo di dispositivo, agli attributi utente e così via.
* Manipolazione avanzata delle immagini
* Middleware tra la rete CDN e un’origine
* Un livello tra il browser e un’API di terze parti, forse per riformattare la risposta API
* Aggregazione di dati da più origini per facilitare il rendering da parte del browser client

Invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con domande e commenti.

### API basate su OpenAPI - Programma per i primi utilizzatori {#open-apis-earlyadopter}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguono le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione vengono generate creando progetti Adobe Developer Console.

Scopri di più sulle [API AEM basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) che ne illustra la configurazione e l’utilizzo.

In concreto, gli endpoint API elencati di seguito sono disponibili come parte di un programma per i primi utilizzatori. Per partecipare, inviare un’e-mail all’indirizzo [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con la descrizione di come si intende utilizzarli.

* [API per frammenti di contenuto di Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* API per Sites e cartelle di Assets
* [API di comunicazione di Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore i feedback. Si possono inviare via e-mail all’indirizzo [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com).

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0).

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
