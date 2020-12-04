---
title: Note sulla versione 2020.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.10.0.'
translation-type: tm+mt
source-git-commit: fd271f24e5f8ddbe440dccf5c51c91a46c70dead
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 18%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione per [!DNL Experience Manager] come Cloud Service 2020.10.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2020.10.0 è il 28 ottobre 2020.
La seguente release (2020.11.0) sarà il 1° dicembre 2020.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Componenti di base 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**: AEM come Cloud Service offre aggiornamenti automatici all&#39;ultima versione dei componenti core. La release 2.12.0 include gli ultimi miglioramenti apportati dalla comunità, ad esempio [un nuovo gestore di moduli POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la possibilità di includere tag personalizzati CSS, Javascript e metadati [tramite la configurazione in base al contesto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e un&#39;utility [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) per semplificare &#39;integrazione dei livelli di dati dei Adobi nei componenti personalizzati. Vedere l&#39; [elenco di modifiche](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) in 2.12.0.

* **[Tipo archivio progetto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: La base consigliata per avviare un nuovo progetto AEM è migliorata, ora include il nuovo livello [ dati client del ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) Adobe, l&#39;opzione per  [distribuire il sito in AMP ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) e nuovi punti  [di estensione per aggiungere il progetto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Cartelle](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)** ContextHub: Possibilità di creare cartelle di audience per organizzare, trovare e selezionare facilmente i segmenti di pubblico da utilizzare per le funzionalità di targeting delle offerte ContextHub.

## [!DNL Adobe Experience Manager Assets] come Cloud Service  {#assets}

* **[!DNL Adobe Sensei]smart tag** video motorizzato: Sfruttando i modelli AI per l&#39;analisi dei contenuti video per i tag di oggetti e azioni specifici, gli utenti DAM possono dedicare meno tempo all&#39;aggiunta di tag e più tempo sfruttando le informazioni avanzate disponibili per offrire ai clienti l&#39;esperienza giusta. Consultate [Risorse video con tag avanzati](/help/assets/smart-tags-video-assets.md).

* **Miglioramenti** al Brand Portal: Le seguenti nuove funzioni e altro ancora sono disponibili in  [!DNL Brand Portal]. Per informazioni dettagliate, consultate [[!DNL Brand Portal] Note sulla versione](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Esperienza ](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) di download migliorata per download semplificati e rapidi. Gli amministratori possono configurare configurazioni di download aggiuntive per offrire un&#39;esperienza che soddisfi le esigenze degli utenti e delle aziende.
   * È ora possibile navigare con un solo clic su File, [Raccolte](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) e Link condivisi da qualsiasi pagina.
   * Gli utenti possono [selezionare e scaricare rappresentazioni specifiche](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) ora. La nuova opzione di download della rappresentazione è disponibile nel pannello Rappresentazioni nella pagina dei dettagli della risorsa.
   * Un timeout di 15 minuti per le sessioni degli utenti ospiti garantisce un&#39;esperienza migliore a tutti gli utenti simultanei.

* **[!DNL Adobe Asset Link]versione 2.1**: È disponibile una nuova versione di  [ ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Adobe Asset Linkextension per  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]e  [!DNL Adobe InDesign] è disponibile. Aggiunge compatibilità con le applicazioni [!DNL Adobe Creative Cloud] più recenti con la versione 2021, rilasciata a ottobre 2020.

* **[!DNL Assets]Supporto** file WebP:  [!DNL Assets] come Cloud Service ora supporta il formato immagine WebP. WebP è un formato immagine emergente creato da Google. Le immagini in formato file WebP sono visivamente indipendenti dai file JPG o PNG e i file sono molto più piccoli. Le dimensioni ridotte dei file delle risorse migliorano i tempi di caricamento delle pagine e aiutano i creatori di contenuti a fornire un&#39;esperienza Web più veloce. Vedere come utilizzare WebP in [creare il profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.10.2 che include l&#39;ultima versione CIF Core Components v1.4.0. Per ulteriori informazioni, fare riferimento a [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2).

* Componenti CIF di base rilasciati v1.4.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0).

### Correzioni di bug {#bug-fixes-commerce}

* Le richieste GraphQL nella console prodotto e nei selettori sono state eseguite tramite POST HTTP. Questo è stato corretto per garantire che il client Apollo GraphQL rispetti l&#39;impostazione nella configurazione OSGi client GraphQL per supportare le richieste di GET, se configurata.

* CIF l’interfaccia utente di configurazione cloud mostrava i pulsanti &quot;Save &amp; Close&quot; per le configurazioni in /lib e /apps/. Ma queste sono di sola lettura, quindi l&#39;interfaccia utente è fissa per visualizzare solo il pulsante &quot;Chiudi&quot;.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.10.0 è il 20 ottobre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il contenitore di build di Cloud Manager ora supporta la compilazione di progetti tramite Java 8 o Java 11. Il supporto per Java 11 è fornito dal sistema di catene utensili Maven.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo di ambienti.
Per ulteriori informazioni, fare riferimento a [Ambiente di visualizzazione](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* I pulsanti Annulla e Salva nella pagina Modifica pipeline non produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base al titolo del flusso di lavoro, al modello del flusso di lavoro, allo stato, all’iniziatore, al percorso di payload e alla data di inizio. Vedere [Istanze del flusso di lavoro di ricerca](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Miglioramento dell’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e inserimento. Messaggio aggiunto per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Content Transfer Tool saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo è stato corretto.
