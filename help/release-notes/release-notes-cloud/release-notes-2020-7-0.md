---
title: Note sulla versione 2020.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.7.0.'
translation-type: tm+mt
source-git-commit: 67d8ef256b410695435446ba0e560edce9115bab
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 86%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.7.0 è il 30 luglio 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Novità {#what-is-new-sites}

I connettori di [!DNL Experience Manager] as a Cloud Service per [!DNL Adobe Target] e [!DNL Adobe Analytics] vengono migliorati nei seguenti modi:

* Una nuova implementazione dell’interfaccia utente sostituisce l’implementazione basata sull’interfaccia classica.

* Le finestre di dialogo dell’interfaccia utente sono state semplificate, lasciando ad [!DNL Adobe Launch] la creazione del framework per la mappatura delle variabili e altre configurazioni. Consulta [Integrazione di Adobe Analytics](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [Integrazione di Adobe Target](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Le configurazioni ora sono memorizzate in `/conf` anziché `/etc/cloudsettings` nell’archivio di Experience Manager.

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] è un servizio scalabile ed estensibile per l’elaborazione delle risorse. Administrators can configure [!DNL Experience Manager] to invoke custom applications created using the [!DNL Asset Compute Service]. Gli sviluppatori possono utilizzare il servizio per creare applicazioni personalizzate specializzate in casi di utilizzo complessi. This web service can generate thumbnails for different file types, high-quality image renderings from Adobe file formats, encode videos (future), extract metadata, extract full text as precursor for indexing, and run an asset through all available [!DNL Sensei] services. see [use asset microservices and processing profiles](/help/assets/asset-microservices-configure-and-use.md).

* La configurazione iniziale di [!DNL Dynamic Media] in [!DNL Experience Manager] as a Cloud Service è stata migliorata ed è ora più robusta. Fornisce agli amministratori indicazioni sull’avanzamento dei processi.

* La pubblicazione delle risorse su [!DNL Dynamic Media] è stata semplificata ed è più robusta; è ora parte integrante della pipeline di elaborazione delle risorse complessiva tramite i microservizi per le risorse ed è stato migliorato il back-end per la pubblicazione batch.

* I passaggi di un flusso di lavoro non compatibili con un’implementazione Cloud Service ora sono contrassegnati da un avviso nell’editor per [!UICONTROL modelli di flusso di lavoro]. Inoltre, durante l’esecuzione dei flussi di lavoro esistenti nell’ambiente Cloud Service, vengono ignorati i passaggi del flusso di lavoro non compatibili.

* I modelli di flussi di lavoro creati dai clienti che vengono distribuiti in `/conf/global`[!DNL Cloud Manager] nel progetto Git associato all’ambiente in vengono automaticamente distribuiti in `/var` e sono quindi disponibili in [!DNL Experience Manager]. I modelli di flusso di lavoro dei prodotti in `/libs` che sono stati modificati dai clienti non vengono distribuiti automaticamente in `/var`.

### Bug corretti {#assets-bugs-fixed}

* La procedura guidata Sposta risorsa non viene caricata come previsto per le risorse incluse nelle raccolte. (CQ-4296756)
* I valori di `dam:size` e `dam:sha1` sono esclusi XMP writeback. (CQ-4237355)
* Quando si annulla la pubblicazione di risorse in massa, [!DNL Brand Portal] viene generato un errore che indica che l’URI della richiesta è troppo lungo. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

AEM Commerce è ora disponibile su Cloud Service.

Per ulteriori informazioni, consulta la [Guida introduttiva ad AEM Commerce as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/commerce/getting-started.html).

## Componenti core {#core-components}

### Novità {#what-is-new-core-components}

La versione 2.11.0 dei [Componenti core di AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) è ora disponibile come parte di AEM Sites e include:

* Introduzione di un nuovo [componente Visualizzatore PDF](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html).

* È ora disponibile il supporto di AMP (Accelerated Mobile Pages) per i componenti core. Consente di creare esperienze cliente più veloci, con transizioni di pagina istantanee quando si accede al sito da un risultato di ricerca Google mobile, migliorando il coinvolgimento degli utenti e la SEO (Search Engine Optimization).
Per ulteriori informazioni, consulta [Supporto AMP per i componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/amp.html).

* Compatibilità con la versione 1.0.2 del [Livello dati client di Adobe](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/data-layer/overview.html).

* Correzioni di bug e miglioramenti nella qualità del codice.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio di [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Le pipeline di Cloud Manager ora supportano variabili e segreti impostati dal cliente.

   Per ulteriori informazioni, consulta [Variabili delle pipeline](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables).

* Sono ora supportati i repository privati con binding di autenticazione.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.
Per ulteriori informazioni, consultate [Utilizzo del supporto](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) Java 11.

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.

### Problemi noti {#known-issues}

* A causa di una modifica nel modo in cui viene calcolata la copertura del codice, la versione *minima* del plugin Jacoco è ora 0.7.5.201505241946 (rilasciata a maggio 2015). I clienti che si riferiscono esplicitamente a una versione precedente ricevono un messaggio di errore nel processo di qualità del codice.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-foundation}

### Novità {#what-is-new-foundations}

* [I registri possono essere inoltrati agli account Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs), il che consente alle organizzazioni di sfruttare il loro investimento su Splunk.

* È possibile assegnare un [indirizzo IP di uscita statico e dedicato](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) al traffico in uscita programmato nel codice Java, utile per alcune integrazioni.

* L’interfaccia classica di AEM Analytics Cloud Service è stata convertita nella nuova interfaccia di AEM. Inoltre, la posizione di Analytics Cloud Service nell’archivio di AEM è stata spostata da `/etc` a `/conf`, in allineamento con altri servizi cloud AEM.

* L’interfaccia classica di AEM Target Cloud Service è stata convertita nella nuova interfaccia di AEM. Inoltre, la posizione di Target Cloud Service nell’archivio di AEM è stata spostata da `/etc` a `/conf`, in allineamento con altri servizi cloud AEM.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.0.2.

### Correzioni di bug {#cra-bug-fixes}

* La versione precedente di Cloud Readiness Analyzer non poteva girare su Adobe Experience Manager (AEM) 6.1. È stato aggiunto il supporto esplicito per gli utenti del gruppo di amministratori.

   Per ulteriori informazioni, consulta [Installazione di Cloud Readiness Analyzer in AEM 6.1](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61).

* Nel rapporto di riepilogo veniva visualizzata una marca temporale di scadenza errata.

* Cloud Readiness Analyzer rilevava componenti personalizzati duplicati.

* In AEM 6.1, l’operazione di ispezione del contenuto veniva terminata prima di essere completata. È stata aggiunta una gestione delle eccezioni che consente all’ispettore di ignorare e continuare fino al completamento di tutta l’ispezione.
