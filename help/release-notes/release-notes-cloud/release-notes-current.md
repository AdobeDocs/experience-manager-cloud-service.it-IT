---
title: Note sulla versione [!DNL Adobe Experience Manager] di Cloud Service per la versione 2020.7.0.
description: '[!DNL  Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.7.0.'
translation-type: tm+mt
source-git-commit: 459843adff623395bcf7afb41f427d6ea0fb825c
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 37%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Data di rilascio {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

##  Adobe Experience Manager Sites come Cloud Service {#cloud-services-sites}

### Novità {#what-is-new-sites}

[!DNL Experience Manager] come connettori di Cloud Service per [!DNL Adobe Target] e [!DNL Adobe Analytics] vengono migliorati nei seguenti modi:

* Una nuova implementazione dell’interfaccia utente sostituisce l’implementazione basata sull’interfaccia classica.

* Finestre di dialogo dell&#39;interfaccia utente semplificate, lasciando la creazione del framework per la mappatura delle variabili e altre configurazioni [!DNL Adobe Launch]. Consultate [Integrazione  Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [Integrazione  Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Le configurazioni ora sono memorizzate nell&#39;archivio `/conf` del Experience Manager  anziché `/etc/cloudsettings` nell&#39;archivio.

## Adobe Experience Manager Assets as a Cloud Service {#assets}

### Novità {#what-is-new-assets}

* [!DNL Asset Compute Service] è un servizio scalabile ed estensibile per l’elaborazione delle risorse. Gli amministratori possono configurare  Experience Manager per richiamare il lavoratore personalizzato creato utilizzando il [!DNL Asset Compute Service]. Gli sviluppatori possono utilizzare il servizio per creare lavoratori personalizzati specializzati in casi di utilizzo complessi. Questo servizio Web può generare miniature per diversi tipi di file, rendering di immagini di alta qualità da  formati di file di Adobe, codificare video (in futuro), estrarre metadati, estrarre testo completo come precursore per l’indicizzazione ed eseguire una risorsa tramite tutti i servizi Sensei disponibili. consulta [Utilizzare i microservizi delle risorse e i profili](/help/assets/asset-microservices-configure-and-use.md)di elaborazione.

* La configurazione iniziale di [!DNL Dynamic Media] in [!DNL Experience Manager] come Cloud Service è migliorata per essere più robusta. Ora fornisce agli amministratori l’avanzamento dei processi.

* La pubblicazione delle risorse su [!DNL Dynamic Media] viene semplificata e resa più solida, rendendola parte integrante del ciclo di elaborazione delle risorse complessivo, utilizzando i microservizi delle risorse e migliorando il backend di pubblicazione batch.

* I passaggi del flusso di lavoro non compatibili con la distribuzione di un Cloud Service ora sono contrassegnati da un avviso nell&#39;editor del modello [!UICONTROL di] workflow. Inoltre, durante l&#39;esecuzione dei flussi di lavoro esistenti nell&#39;ambiente di Cloud Service, i passaggi del flusso di lavoro incompatibili vengono ignorati.

* I modelli di flussi di lavoro creati dai clienti che sono distribuiti `/conf/global` nel progetto Git associato all&#39;ambiente in Cloud Manager vengono automaticamente distribuiti `/var` e sono quindi disponibili in  Experience Manager. I modelli di flusso di lavoro dei prodotti in `/libs` cui sono stati modificati dai clienti non vengono distribuiti automaticamente a `/var`.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* AEM Commerce è ora disponibile sul Cloud Service. Per ulteriori informazioni, consulta [Guida introduttiva](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html).

## Componenti core {#core-components}

### Novità {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* Introduzione di un nuovo componente [visualizzatore](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)PDF.

* È ora disponibile il supporto di AMP (Accelerated Mobile Pages) per i componenti core. Consente di creare esperienze cliente più veloci effettuando la transizione di pagina istantaneamente quando si accede al sito da un risultato di ricerca Google Mobile, migliorando il coinvolgimento degli utenti e il SEO.
Per ulteriori informazioni, consulta Supporto [AMP per i componenti](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) core.

* Compatibilità con la versione 1.0.2 del [Livello](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)dati client del Adobe.

* Correzioni di bug e miglioramenti nella qualità del codice.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio di [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Le pipeline di Cloud Manager ora supportano variabili e segreti impostati dal cliente.

   Per ulteriori informazioni, consulta [Variabili delle pipeline](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables).

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

* A causa di una modifica nel modo in cui viene calcolata la copertura del codice, la versione *minima* del plugin Jacoco è ora 0.7.5.201505241946 (rilasciata a maggio 2015). I clienti che fanno esplicito riferimento a una versione precedente ricevono un messaggio di errore nel processo di qualità del codice.


## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Novità {#what-is-new-foundations}

* [I registri possono essere inoltrati agli account](/help/implementing/developing/introduction/logging.md#splunk-logs)Splunk, il che consente alle organizzazioni di sfruttare il loro investimento Splunk.

* [È possibile assegnare un indirizzo](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) IP di uscita statico e dedicato al traffico in uscita programmato nel codice Java, utile per alcune integrazioni.

* Interfaccia  servizio cloud Analytics AEM porta da interfaccia classica a nuova interfaccia AEM. È stata spostata anche la posizione  servizio cloud Analytics in AEM repository da `/etc` a `/conf`, per l&#39;allineamento con altri AEM cloud services.

* Interfaccia AEM servizio cloud Target da interfaccia classica a nuova interfaccia AEM. È stata spostata anche la posizione del servizio cloud Target in AEM repository da `/etc` a `/conf`, per allinearsi con altri AEM cloud services.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.0.2.

### Correzioni di bug {#cra-bug-fixes}

* La versione precedente di Cloud Readiness Analyzer non poteva girare su Adobe Experience Manager (AEM) 6.1. È stato aggiunto il supporto esplicito per gli utenti del gruppo di amministratori.

   Per ulteriori informazioni, consulta [Installazione di Cloud Readiness Analyzer in AEM 6.1](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61).

* Nel rapporto di riepilogo veniva visualizzata una marca temporale di scadenza errata.

* Cloud Readiness Analyzer rilevava componenti personalizzati duplicati.

* In AEM 6.1, l’operazione di ispezione del contenuto veniva terminata prima di essere completata. È stata aggiunta una gestione delle eccezioni che consente all’ispettore di ignorare e continuare fino al completamento di tutta l’ispezione.
