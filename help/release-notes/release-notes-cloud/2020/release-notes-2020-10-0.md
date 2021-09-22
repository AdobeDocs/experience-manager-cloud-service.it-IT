---
title: Note sulla versione 2020.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service - Note sulla versione 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: af5eb5aeb34e2f0ead98e0a0acb412b19bcfe517
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 23%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] come Cloud Service 2020.10.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 è il 28 ottobre 2020.
La versione seguente (2020.11.0) sarà il 1° dicembre 2020.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Componenti core 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)**: Adobe Experience Manager as a Cloud Service sfrutta gli aggiornamenti automatici all’ultima versione dei componenti core. La versione 2.12.0 include gli ultimi miglioramenti apportati dalla comunità. I miglioramenti includono [un nuovo gestore di moduli POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la possibilità di includere tag CSS, JavaScript e metadati personalizzati [tramite la configurazione in base al contesto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e un&#39;utilità [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) per semplificare l&#39;integrazione di Adobe Data Layer nei componenti personalizzati. Consulta l’ [elenco delle modifiche](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) in 2.12.0.

* **[Archetipo di progetto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: La fondazione consigliata per avviare un nuovo progetto di Experience Manager è migliorata. Ora include la nuova opzione [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), [distribuisci il sito in AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e i nuovi punti di estensione [per aggiungere il progetto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Cartelle](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)** ContextHub: Possibilità di creare cartelle di pubblico per organizzare, trovare e selezionare facilmente i segmenti di pubblico da utilizzare per le funzionalità di targeting delle offerte ContextHub.

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

* **[!DNL Adobe Sensei]assegnazione tag avanzati video**: Applicando modelli AI per analizzare il contenuto video per i tag specifici per oggetti e azioni, gli utenti DAM possono dedicare meno tempo all’aggiunta di tag e più tempo utilizzando le informazioni avanzate e ricche. A tua volta, fornisci l&#39;esperienza giusta ai clienti. Consulta [Risorse video con tag avanzati](/help/assets/smart-tags-video-assets.md).

* **Miglioramenti** di Brand Portal: Le seguenti nuove funzioni e altro ancora sono disponibili in  [!DNL Brand Portal]. Per informazioni dettagliate, consulta le [[!DNL Brand Portal] note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Esperienza di download migliorata ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) per download semplificati e rapidi. Gli amministratori possono configurare modalità di download aggiuntive per offrire un’esperienza in grado di soddisfare le esigenze specifiche di qualsiasi utente o azienda.
   * L’accesso con un clic a File, [Raccolte](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Collegamenti condivisi è ora possibile da qualsiasi pagina.
   * Gli utenti possono ora [selezionare e scaricare rappresentazioni specifiche](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nuova opzione di download delle rappresentazioni è ora disponibile nel riquadro Rappresentazioni della pagina dei dettagli delle risorse.
   * Un timeout di 15 minuti per le sessioni degli utenti che accedono come ospite garantisce un’esperienza migliore per tutti gli utenti simultanei.

* **[!DNL Adobe Asset Link]versione 2.1**: È disponibile una nuova versione di  [Adobe Asset ](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) Linkextension per  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator], e  [!DNL Adobe InDesign] . Aggiunge compatibilità con le applicazioni [!DNL Adobe Creative Cloud] più recenti con la versione 2021, rilasciata a ottobre 2020.

* **[!DNL Assets]Supporto** file WebP:  [!DNL Assets] come Cloud Service ora supporta il formato immagine WebP. WebP è un formato immagine emergente creato da Google. Le immagini in formato file WebP sono visivamente indistinguibili da file JPG o PNG e i file sono molto più piccoli. Le dimensioni ridotte dei file di risorse migliorano i tempi di caricamento delle pagine e consentono ai creatori di contenuti di offrire un’esperienza web più veloce. Scopri come utilizzare WebP in [crea profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato: 2020.10.2 che include la versione 1.4.0 dei componenti core CIF più recente. Per ulteriori informazioni, consulta [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) .

* È stata rilasciata la versione 1.4.0 dei componenti core CIF. Per ulteriori informazioni, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) .

### Correzioni di bug {#bug-fixes-commerce}

* Le richieste GraphQL presenti nella console dei prodotti e nei selettori sono state eseguite tramite HTTP POST. Questo problema è stato risolto per garantire che il client Apollo GraphQL rispetti l&#39;impostazione nella configurazione OSGi del client GraphQL per supportare le richieste GET, se configurata.

* L’interfaccia utente di configurazione di CIF Cloud mostrava i pulsanti &quot;Salva e chiudi&quot; per le configurazioni in /lib e /apps/. Ma queste interfacce sono di sola lettura, quindi l&#39;interfaccia utente è fissa per visualizzare solo il pulsante &quot;Chiudi&quot;.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in Experience Manager as a Cloud Service 2020.10.0 è il 20 ottobre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il &quot;contenitore di build&quot; di Cloud Manager ora supporta la compilazione di progetti utilizzando Java™ 8 o Java™ 11. Il supporto per Java™ 11 è fornito dal sistema Maven toolchain.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo di ambienti.
Per ulteriori informazioni, consulta [Visualizzazione dell&#39;ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) .

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

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base a Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data di inizio. Consulta [Ricerca istanze flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Strumento Content Transfer (Trasferimento contenuti)  {#content-transfer-tool}

Scopri le novità e gli aggiornamenti di [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Migliorata l’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili.
