---
title: Note sulla versione 2025.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2025.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: b9353092-88a0-477c-85f4-f916a4b8ba8f
source-git-commit: 81e5cfd699fee811fc2b072e3b65e9d463a338b2
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 99%

---

# Note sulla versione 2025.3.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2025.3.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.3.0) è il 27 marzo 2025. La prossima versione funzionale (2025.4.0) è pianificata per il 24 aprile 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video che mostra una panoramica sulla versione di marzo 2025 per un riepilogo delle funzioni aggiunte alla versione 2025.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3463860?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in Dynamic Media {#new-features-dynamic-media}

**Supporto per video in forma estesa distribuiti tramite Dynamic Media con Open API**

Dynamic Media con OpenAPI ora supporta i video in forma estesa. I video in forma estesa supportano fino a 50 GB e 2 ore.

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

La scheda Larghezza di banda nella dashboard di reporting di Dynamic Media Classic non è più supportata da aprile 2025.

Consulta [Larghezza di banda e archiviazione, tipi di rapporti](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Nuove funzioni nella vista Risorse {#new-features-assets-view}


**Supporto per tag principali**

AEM Assets ora supporta la mappatura di una proprietà tag in un modulo metadati sui metadati personalizzati. Inoltre, in qualità di amministratore, puoi limitare la disponibilità dei tag agli utenti limitando l’accesso a un tag principale specifico e ai tag esistenti sotto il tag principale.

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

A partire dalla versione di gennaio, è possibile generare codice con Java 21 e Java 17. È possibile accedere a nuove funzioni quali corrispondenza pattern, classi sigillate e vari miglioramenti delle prestazioni. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti del runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Il **runtime** Java 21 è stato distribuito negli ambienti di sviluppo/RDE a febbraio; verrà applicato agli ambienti di staging/produzione il **28 e 29 aprile**. Tieni presente che **la generazione del codice** con Java 21 (o Java 17) è indipendente dal runtime di Java 21. È necessario eseguire in modo esplicito i passaggi per generare il codice con Java 21 (o Java 17).

### Funzionalità di inoltro del registro di AEM a più destinazioni: programma Beta {#log-forwarding-earlyadopter}

Ora, in versione Beta, è possibile inoltrare i registri di AEM a New Relic (utilizzando HTTPS), Amazon S3 e Sumo Logic. Sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM (disponibilità generale) all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

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

Scopri di più sulle [API AEM basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) che ne illustra la configurazione e l’utilizzo.

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
