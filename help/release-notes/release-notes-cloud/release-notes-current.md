---
title: Note sulla versione 2020.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.10.0.'
translation-type: tm+mt
source-git-commit: 4cbee57ff2490802bb473279a37fe6c539a4f44b
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 22%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Data di rilascio {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
La seguente release (2020.11.0) sarà del 26 novembre.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sitess}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **Tipo archivio progetto 24**: La base consigliata per avviare un nuovo progetto AEM è migliorata, ora incluso il nuovo livello dati client  Adobe, l&#39;opzione per distribuire il sito in AMP e nuovi punti di estensione per aggiungere il progetto CSS/JS.

* **Cartelle** ContextHub: Possibilità di creare cartelle di audience per organizzare, trovare e selezionare facilmente i segmenti di pubblico da utilizzare per le funzionalità di targeting delle offerte ContextHub.

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]smart tag** video motorizzato: Sfruttando i modelli AI per l&#39;analisi dei contenuti video per i tag di oggetti e azioni specifici, gli utenti DAM possono dedicare meno tempo all&#39;aggiunta di tag e più tempo sfruttando le informazioni avanzate disponibili per offrire ai clienti l&#39;esperienza giusta. Consultate Risorse [video con tag](/help/assets/smart-tags-video-assets.md)avanzati.

* **Miglioramenti** al Brand Portal: Le seguenti nuove funzioni e altro ancora sono disponibili in [!DNL Brand Portal]. For details, see [[!DNL Brand Portal] release notes](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Esperienza](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) di download migliorata per download semplificati e rapidi. Gli amministratori possono configurare configurazioni di download aggiuntive per offrire un&#39;esperienza che soddisfi le esigenze degli utenti e delle aziende.
   * È ora possibile navigare con un solo clic su File, [Raccolte](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)e Collegamenti condivisi da qualsiasi pagina.
   * Gli utenti ora possono [selezionare e scaricare rappresentazioni](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) specifiche. La nuova opzione di download della rappresentazione è disponibile nel pannello Rappresentazioni nella pagina dei dettagli della risorsa.
   * Un timeout di 15 minuti per le sessioni degli utenti ospiti garantisce un&#39;esperienza migliore a tutti gli utenti simultanei.

* **[!DNL Adobe Asset Link]versione 2.1**: È disponibile una nuova versione dell’estensione [Collegamento](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) risorse Adobe per [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] . Aggiunge compatibilità con le ultime [!DNL Adobe Creative Cloud] applicazioni con la versione 2021, rilasciata a ottobre 2020.

* **[!DNL Assets]Supporto** file WebP: [!DNL Assets] come Cloud Service ora supporta il formato immagine WebP. WebP è un formato immagine emergente creato da Google. Le immagini in formato file WebP sono visivamente indipendenti dai file JPG o PNG e i file sono molto più piccoli. Le dimensioni ridotte dei file delle risorse migliorano i tempi di caricamento delle pagine e aiutano i creatori di contenuti a fornire un&#39;esperienza Web più veloce.

<!--
### Bugs Fixed {#bugs-fixed-assets}

Content to come
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.10.2 che include l&#39;ultima versione CIF Core Components v1.4.0. Per ulteriori informazioni, consultare [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) .

* Componenti CIF di base rilasciati v1.4.0. Per ulteriori informazioni, consulta Componenti [di base](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) CIF.

### Correzioni di bug {#bug-fixes-commerce}

* Le richieste GraphQL nella console prodotto e nei selettori sono state eseguite tramite POST HTTP. Questo è stato corretto per garantire che il client Apollo GraphQL rispetti l&#39;impostazione nella configurazione OSGi client GraphQL per supportare le richieste di GET, se configurata.

* CIF l’interfaccia utente di configurazione cloud mostrava i pulsanti &quot;Save &amp; Close&quot; per le configurazioni in /lib e /apps/. Ma queste sono di sola lettura, quindi l&#39;interfaccia utente è fissa per visualizzare solo il pulsante &quot;Chiudi&quot;.

## Cloud Manager {#cloud-manager}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo degli ambienti.
Per ulteriori informazioni, vedere [Ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) di visualizzazione.

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

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base al titolo del flusso di lavoro, al modello del flusso di lavoro, allo stato, all’iniziatore, al percorso di payload e alla data di inizio. Consultate [Cerca istanze](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)del flusso di lavoro.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Miglioramento dell’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e inserimento. Messaggio aggiunto per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Content Transfer Tool saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo è stato corretto.
