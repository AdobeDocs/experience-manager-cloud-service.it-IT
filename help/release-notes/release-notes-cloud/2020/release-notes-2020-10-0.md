---
title: Note sulla versione 2020.10.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione as a Cloud Service per 2020.10.0."
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 23%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 è il 28 ottobre 2020.
La versione seguente (2020.11.0) sarà il 1° dicembre 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Componenti core 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)**: Adobe Experience Manager as a Cloud Service beneficia di aggiornamenti automatici all’ultima versione dei componenti core. La versione 2.12.0 include gli ultimi miglioramenti apportati dalla comunità. I miglioramenti includono [un nuovo gestore di moduli POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la possibilità di includere CSS, JavaScript e metadati personalizzati [tag tramite la configurazione in base al contesto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) Utilità per semplificare l’integrazione di Adobe Data Layer nei componenti personalizzati. Consulta la sezione [elenco delle modifiche](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) 2.12.0.

* **[Archetipo di progetto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: La fondazione consigliata per avviare un nuovo progetto di Experience Manager è migliorata. Ora include il nuovo [Livello dati client di Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), opzione per [fornire il sito in AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e nuovi [punti di estensione per aggiungere CSS/JS del progetto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Cartelle ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Possibilità di creare cartelle di pubblico per organizzare, trovare e selezionare facilmente i segmenti di pubblico da utilizzare per le funzionalità di targeting delle offerte ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]assegnazione tag avanzati video**: Applicando modelli AI per analizzare il contenuto video per i tag specifici per oggetti e azioni, gli utenti DAM possono dedicare meno tempo all’aggiunta di tag e più tempo utilizzando le informazioni avanzate e ricche. A tua volta, fornisci l&#39;esperienza giusta ai clienti. Vedi [Smart tag per le risorse video](/help/assets/smart-tags-video-assets.md).

* **Miglioramenti a Brand Portal**: Sono disponibili le seguenti nuove funzioni e altro ancora in [!DNL Brand Portal]. Per maggiori dettagli, vedi [[!DNL Brand Portal] note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Esperienza di download migliorata](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) per download semplificati e rapidi. Gli amministratori possono configurare modalità di download aggiuntive per offrire un’esperienza in grado di soddisfare le esigenze specifiche di qualsiasi utente o azienda.
   * L’accesso con un clic a File, [Raccolte](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Collegamenti condivisi è ora possibile da qualsiasi pagina.
   * Gli utenti possono ora [selezionare e scaricare rappresentazioni specifiche](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nuova opzione di download delle rappresentazioni è ora disponibile nel riquadro Rappresentazioni della pagina dei dettagli delle risorse.
   * Un timeout di 15 minuti per le sessioni degli utenti che accedono come ospite garantisce un’esperienza migliore per tutti gli utenti simultanei.

* **[!DNL Adobe Asset Link]versione 2.1**: Una nuova versione di [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) estensione per [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] è disponibile. Aggiunge compatibilità con le [!DNL Adobe Creative Cloud] applicazioni con versione 2021, rilasciate a ottobre 2020.

* **[!DNL Assets]Supporto file WebP**: [!DNL Assets] as a Cloud Service ora supporta il formato immagine WebP. WebP è un formato immagine emergente creato da Google. Le immagini in formato file WebP sono visivamente indistinguibili dai file JPG o PNG e i file sono molto più piccoli. Le dimensioni ridotte dei file di risorse migliorano i tempi di caricamento delle pagine e consentono ai creatori di contenuti di offrire un’esperienza web più veloce. Scopri come utilizzare WebP in [creare un profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Novità in [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento sia di accesso che di non accesso (anonimo) tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sugli utenti finali. Consente agli utenti aziendali di prendere decisioni informate sul contenuto, il layout e lo stile dei moduli adattivi in base alle informazioni raccolte.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: È possibile archiviare in-process AEM dati variabili del flusso di lavoro contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Durante l’elaborazione del flusso di lavoro, i dati memorizzati nelle variabili del flusso di lavoro non vengono conservati AEM archivio. Viene recuperato su richiesta dall’archivio gestito dal cliente.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare un modello e dati XML per generare documenti in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato: 2020.10.2 che include la versione più recente dei componenti core CIF versione v1.4.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) per ulteriori dettagli.

* Componenti core CIF rilasciati v1.4.0. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-commerce}

* Le richieste GraphQL presenti nella console dei prodotti e nei selettori sono state eseguite tramite HTTP POST. Questo problema è stato risolto per garantire che il client Apollo GraphQL rispetti l&#39;impostazione nella configurazione OSGi del client GraphQL per supportare le richieste GET, se configurata.

* L’interfaccia utente di configurazione di CIF Cloud mostrava i pulsanti &quot;Salva e chiudi&quot; per le configurazioni in /lib e /apps/. Ma queste interfacce sono di sola lettura, quindi l&#39;interfaccia utente è fissa per visualizzare solo il pulsante &quot;Chiudi&quot;.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di Cloud Manager in Experience Manager as a Cloud Service 2020.10.0 è il 20 ottobre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il &quot;contenitore di build&quot; di Cloud Manager ora supporta la compilazione di progetti utilizzando Java™ 8 o Java™ 11. Il supporto per Java™ 11 è fornito dal sistema Maven toolchain.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo di ambienti.
Fai riferimento a [Ambiente di visualizzazione](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* I pulsanti Annulla e Salva nella pagina Modifica pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Durante la creazione di un programma, il nome suggerito talvolta restituiva un duplicato del nome di un programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e Dispatcher quando non ne erano presenti.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base a Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data di inizio. Vedi [Cerca istanze del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Ulteriori informazioni sulle novità e sugli aggiornamenti di [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versione v1.1.12.

### Novità {#what-is-new-ctt}

* Migliorata l’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili.
