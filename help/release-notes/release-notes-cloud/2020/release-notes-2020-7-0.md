---
title: Note sulla versione 2020.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] note sulla versione 2020.7.0 di as a Cloud Service.'
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 74%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.7.0 è il 30 luglio 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Novità {#what-is-new-sites}

I connettori di [!DNL Experience Manager] as a Cloud Service per [!DNL Adobe Target] e [!DNL Adobe Analytics] vengono migliorati nei seguenti modi:

* Una nuova implementazione dell’interfaccia utente sostituisce l’implementazione basata sull’interfaccia classica.

* Le finestre di dialogo dell’interfaccia utente sono state semplificate, lasciando ad [!DNL Adobe Launch] la creazione del framework per la mappatura delle variabili e altre configurazioni. Consulta [Integrazione di Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [Integrazione di Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Le configurazioni ora sono memorizzate in `/conf` anziché `/etc/cloudsettings` nell’archivio di Experience Manager.

## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] è un servizio scalabile ed estensibile per l’elaborazione delle risorse. Gli amministratori possono configurare [!DNL Experience Manager] per richiamare le applicazioni personalizzate create utilizzando [!DNL Asset Compute Service]. Gli sviluppatori possono utilizzare il servizio per creare applicazioni personalizzate specializzate per casi d’uso complessi. Questo servizio Web può generare miniature per diversi tipi di file, eseguire il rendering di immagini di alta qualità da formati di file Adobe, codificare video (in futuro), estrarre metadati, estrarre testo completo come precursore per l&#39;indicizzazione ed eseguire una risorsa tramite tutti i servizi [!DNL AI] disponibili. vedi [utilizzare i microservizi delle risorse e i profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).

* La configurazione iniziale di [!DNL Dynamic Media] in [!DNL Experience Manager] as a Cloud Service è stata migliorata ed è ora più robusta. Fornisce agli amministratori indicazioni sull’avanzamento dei processi.

* La pubblicazione delle risorse su [!DNL Dynamic Media] è stata semplificata ed è più robusta; è ora parte integrante della pipeline di elaborazione delle risorse complessiva tramite i microservizi per le risorse ed è stato migliorato il back-end per la pubblicazione batch.

* I passaggi di un flusso di lavoro non compatibili con un’implementazione Cloud Service ora sono contrassegnati da un avviso nell’editor per [!UICONTROL modelli di flusso di lavoro]. Inoltre, durante l’esecuzione dei flussi di lavoro esistenti nell’ambiente Cloud Service, vengono saltati i passaggi del flusso di lavoro non compatibili.

* I modelli di flusso di lavoro creati dai clienti distribuiti in `/conf/global` nel progetto Git associato all&#39;ambiente in [!DNL Cloud Manager] vengono automaticamente distribuiti in `/var` e sono quindi disponibili in [!DNL Experience Manager]. I modelli di flusso di lavoro dei prodotti in `/libs` che sono stati modificati dai clienti non vengono distribuiti automaticamente in `/var`.

### Bug corretti {#assets-bugs-fixed}

* La procedura guidata Sposta risorsa non si carica come previsto per le risorse incluse nelle raccolte. (CQ-4296756)
* I valori di `dam:size` e `dam:sha1` sono esclusi dal writeback di XMP. (CQ-4237355)
* Quando si annullano in blocco le risorse, [!DNL Brand Portal] genera un errore che suggerisce che l&#39;URI della richiesta è troppo lungo. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

AEM Commerce è ora disponibile su Cloud Service.

Per ulteriori dettagli, consulta la [Guida introduttiva ad AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html).

## Componenti core {#core-components}

### Novità {#what-is-new-core-components}

La versione 2.11.0 dei [Componenti core di AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) è ora disponibile come parte di AEM Sites e include:

* Introduzione di un nuovo [componente Visualizzatore PDF](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html).

* È ora disponibile il supporto di AMP (Accelerated Mobile Pages) per i componenti core. Consente di creare esperienze cliente più veloci, con transizioni di pagina istantanee quando si accede al sito da un risultato di ricerca Google mobile, migliorando il coinvolgimento degli utenti e la SEO (Search Engine Optimization).
Per ulteriori dettagli, vedere [Supporto AMP per i Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html).

* Compatibilità con la versione 1.0.2 del [Livello dati client di Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=it).

* Correzioni di bug e miglioramenti nella qualità del codice.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina Ambienti è stata riprogettata.

* Ora gli ambienti che sono stati sospesi presentano uno stato discreto in Cloud Manager.

* Il numero di variabili per ambiente è stato aumentato a 200.

* Le pipeline di Cloud Manager ora supportano variabili e segreti impostati dal cliente.

  Per ulteriori informazioni, consulta Variabili delle pipeline.

* Ora gli archivi Maven privati vincolati all’autenticazione sono supportati.

* Ora il contenitore della build di Cloud Manager supporta sia Java 8 sia Java 11.
Per ulteriori informazioni, consulta Utilizzo del supporto Java 11.

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento tra Cloud Manager e Console sviluppatori era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Console sviluppatori non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Durante la creazione di un programma, il nome suggerito talvolta restituiva un duplicato di un nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.

### Problemi noti {#known-issues}

* A causa di una modifica nel modo in cui viene calcolata la copertura del codice, la versione *minima* del plugin Jacoco è ora 0.7.5.201505241946 (pubblicata a maggio 2015). I clienti che si riferiscono esplicitamente a una versione precedente ricevono un messaggio di errore nel processo di qualità del codice.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-foundation}

### Novità {#what-is-new-foundations}

* [I registri possono essere inoltrati agli account Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs), il che consente alle organizzazioni di utilizzare il proprio investimento Splunk.

* È possibile assegnare un [indirizzo IP di uscita statico e dedicato](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) al traffico in uscita programmato nel codice Java, utile per alcune integrazioni.

* L’interfaccia classica di AEM Analytics Cloud Service è stata convertita nella nuova interfaccia di AEM. Inoltre, la posizione di Analytics Cloud Service nell’archivio di AEM è stata spostata da `/etc` a `/conf`, in allineamento con altri servizi cloud AEM.

* L’interfaccia classica di AEM Target Cloud Service è stata convertita nella nuova interfaccia di AEM. Inoltre, la posizione di Target Cloud Service nell’archivio di AEM è stata spostata da `/etc` a `/conf`, in allineamento con altri servizi cloud AEM.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.0.2.

### Correzioni di bug {#cra-bug-fixes}

* La versione precedente di Cloud Readiness Analyzer non poteva girare su Adobe Experience Manager (AEM) 6.1. È stato aggiunto il supporto esplicito per gli utenti del gruppo di amministratori.

  Per ulteriori dettagli, consulta [Installazione di CRA in AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61).

* Nel rapporto di riepilogo veniva visualizzata una marca temporale di scadenza errata.

* Cloud Readiness Analyzer rilevava componenti personalizzati duplicati.

* In AEM 6.1, l’operazione di ispezione del contenuto veniva terminata prima di essere completata. È stata aggiunta una gestione delle eccezioni che consente all’ispettore di ignorare e continuare fino al completamento di tutta l’ispezione.
