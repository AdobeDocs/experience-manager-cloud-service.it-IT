---
title: Note sulla versione 2020.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] note sulla versione 2020.10.0 di as a Cloud Service.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 24%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 è il 28 ottobre 2020.
La seguente versione (2020.11.0) sarà del 1° dicembre 2020.

## as a Cloud Service [!DNL Adobe Experience Manager Sites] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Componenti core 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)**: Adobe Experience Manager as a Cloud Service beneficia degli aggiornamenti automatici all&#39;ultima versione dei Componenti core. La versione 2.12.0 include gli ultimi miglioramenti apportati dalla community. I miglioramenti includono [un nuovo gestore di moduli POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la possibilità di includere tag [di metadati, JavaScript e CSS personalizzati tramite la configurazione basata sul contesto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e un&#39;utilità [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) per semplificare l&#39;integrazione di Adobe Data Layer nei componenti personalizzati. Visualizza l&#39;[elenco delle modifiche](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) nella versione 2.12.0.

* **[Archetipo progetto 24](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview)**: la base consigliata per l&#39;avvio di un nuovo progetto Experience Manager è stata migliorata. Ora include il nuovo [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=it), l&#39;opzione per [recapitare il sito in AMP](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e i nuovi [punti di estensione per aggiungere il progetto CSS/JS](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading).

* **[Cartelle ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: possibilità di creare cartelle di pubblico per organizzare, trovare e selezionare facilmente i segmenti di pubblico da utilizzare per le funzionalità di targeting delle offerte ContextHub.

## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

* Applicazione di tag avanzati video **[!DNL Adobe AI]basata su**: applicando modelli AI per analizzare contenuti video per tag specifici per oggetti e azioni, gli utenti DAM possono dedicare meno tempo all&#39;aggiunta di tag e più tempo all&#39;utilizzo di informazioni avanzate esposte. A tua volta, puoi offrire ai clienti l’esperienza giusta. Consulta [Risorse per video con tag avanzati](/help/assets/smart-tags-for-videos.md).

* **Miglioramenti di Brand Portal**: le seguenti nuove funzionalità e altro ancora sono disponibili in [!DNL Brand Portal]. Per informazioni dettagliate, consulta [[!DNL Brand Portal] note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Esperienza di download migliorata](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) per download semplificati e rapidi. Gli amministratori possono configurare modalità di download aggiuntive per offrire un’esperienza in grado di soddisfare le esigenze specifiche di qualsiasi utente o azienda.
   * È ora possibile navigare con un solo clic su File, [Raccolte](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Collegamenti condivisi da qualsiasi pagina.
   * Ora gli utenti possono [selezionare e scaricare rappresentazioni specifiche](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nuova opzione di download delle rappresentazioni è ora disponibile nel riquadro Rappresentazioni della pagina dei dettagli delle risorse.
   * Un timeout di 15 minuti per le sessioni degli utenti ospiti garantisce un’esperienza migliore a tutti gli utenti simultanei.

* **[!DNL Adobe Asset Link]versione 2.1**: è disponibile una nuova versione dell&#39;estensione [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) per [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign]. Aggiunge compatibilità con le ultime applicazioni [!DNL Adobe Creative Cloud] con la versione 2021, rilasciata a ottobre 2020.

* **[!DNL Assets]Supporto file WebP**: [!DNL Assets] as a Cloud Service ora supporta il formato immagine WebP. WebP è un formato immagine emergente creato da Google. Le immagini in formato WebP sono visivamente indistinguibili dai file JPG o PNG e i file sono molto più piccoli. La riduzione delle dimensioni dei file delle risorse migliora i tempi di caricamento delle pagine e aiuta i creatori di contenuti a fornire un’esperienza web più veloce. Scopri come utilizzare WebP in [creare un profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## as a Cloud Service [!DNL Adobe Experience Manager Forms] {#forms-oct-2021}

### Novità in [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**: è ora possibile acquisire e tenere traccia del comportamento degli utenti connessi e non connessi (anonimi) tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sugli utenti. Aiuta gli utenti aziendali a prendere decisioni informate sul contenuto, il layout e lo stile dei moduli adattivi in base alle informazioni raccolte.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Esternalizzare i dati del flusso di lavoro AEM per un&#39;elaborazione sicura**: è possibile memorizzare i dati delle variabili del flusso di lavoro AEM in elaborazione che contengono elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un&#39;elaborazione sicura. Durante l’elaborazione del flusso di lavoro, i dati memorizzati nelle variabili del flusso di lavoro non vengono conservati nell’archivio di AEM. Viene recuperato su richiesta dall’archivio gestito dal cliente.

### Funzioni beta di [!DNL Forms]  {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) consentono di combinare un modello e dati XML per generare documenti in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch.

Per registrarti al programma beta, puoi inviare un’e-mail all’indirizzo [!DNL formscsbeta@adobe.com].

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stato rilasciato il sito di riferimento CIF Venia (2020.10.2), che include la versione più recente dei Componenti core di CIF v1.4.0. Per ulteriori dettagli, consulta [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2).

* È stata rilasciata la versione 1.4.0 dei Componenti core di CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0).

### Correzioni di bug {#bug-fixes-commerce}

* Le richieste GraphQL presenti nella console del prodotto e nei selettori sono state effettuate tramite HTTP POST. Questo problema è stato risolto per garantire che il client Apollo GraphQL rispetti l’impostazione nella configurazione OSGi del client GraphQL per supportare le richieste GET, se configurate.

* Nell’interfaccia utente di configurazione di CIF Cloud sono stati visualizzati i pulsanti &quot;Salva e chiudi&quot; per le configurazioni in /lib e /apps/. Tuttavia, queste interfacce sono di sola lettura e pertanto l’interfaccia utente è fissa solo per visualizzare il pulsante &quot;Chiudi&quot;.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in Experience Manager as a Cloud Service 2020.10.0 è il 2 ottobre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* La pagina Ambienti è stata riprogettata.

* Ora gli ambienti che sono stati sospesi presentano uno stato discreto in Cloud Manager.

* Il &quot;contenitore build&quot; di Cloud Manager ora supporta la compilazione di progetti utilizzando Java™ 8 o Java™ 11. Il supporto per Java™ 11 è fornito dal sistema toolchain Maven.

* Il numero di variabili per ambiente è stato aumentato a 200.

* Ora nella scheda Ambiente della pagina Panoramica sono elencati fino a tre ambienti. Gli utenti possono selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con l’elenco completo degli ambienti.
Per ulteriori dettagli, consulta la [Visualizzazione dell’ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il collegamento tra Cloud Manager e Console sviluppatori era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Console sviluppatori non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* I pulsanti Annulla e Salva nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Durante la creazione di un programma, il nome suggerito talvolta restituiva un duplicato di un nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* Talvolta, nella pagina Ambienti venivano visualizzati i segmenti Publish e Dispatcher anche se non ne erano presenti.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze di flussi di lavoro basate su Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data inizio. Consulta [Istanze flusso di lavoro di ricerca](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Strumento di trasferimento contenuti {#content-transfer-tool}

Scopri le novità e gli aggiornamenti di [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Esperienza utente migliorata per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) ignorava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili.
