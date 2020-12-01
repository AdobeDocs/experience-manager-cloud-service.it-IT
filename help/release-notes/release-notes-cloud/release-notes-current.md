---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: 89f7e60205efc275bbeb97246ccc3add28810cfa
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 3%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2020.11.0 è il 1 dicembre 2020.
La seguente release (2020.12.0) sarà del 17 dicembre 2020

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Avvia Gestione](/help/sites-cloud/authoring/launches/managing-pages.md)  Gerarchia e Timewarp  [futuro](/help/sites-cloud/authoring/launches/preview.md)**: Nuova interfaccia utente per aggiungere/rimuovere pagine all’interno di un lancio, mentre nel sito con Timewarp viene visualizzato lo stato futuro dagli avvii.

* **[Editor e modelli](/help/assets/content-fragments/content-fragments-models.md)** di frammenti di contenuto estesi: Nuove opzioni per la convalida dell&#39;input su vari tipi di dati, il miglioramento del tipo di dati di enumerazione con nuove visualizzazioni di moduli e il nome del modello di frammento di contenuto sono visualizzati e ricercabili nell&#39;interfaccia utente Risorse.

* **Rendi sito installabile**: Nuove proprietà del sito per configurare le funzionalità Progressive Web Application (PWA), che renderanno disponibile un sito installabile e un sito offline facoltativo. Le funzioni richiedono componenti core.

* **[Componenti di base 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**: AEM come Cloud Service offre aggiornamenti automatici all&#39;ultima versione dei componenti core. La release 2.12.0 include gli ultimi miglioramenti apportati dalla comunità, ad esempio [un nuovo gestore di moduli POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la possibilità di includere tag personalizzati CSS, Javascript e metadati [tramite la configurazione in base al contesto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) e un&#39;utility [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) per semplificare &#39;integrazione dei livelli di dati dei Adobi nei componenti personalizzati. Vedere l&#39; [elenco di modifiche](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) in 2.12.0.

## [!DNL Adobe Experience Manager Assets] come Cloud Service  {#assets}

### Novità in [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Caricamento** di massa delle risorse: Offrite ai clienti un servizio di inserimento scalabile e nativo basato su cloud che si basa  [!DNL Experience Manager] su un&#39;architettura di Cloud Service con microservizi per risorse. I casi d’uso chiave includono l’assimilazione su larga scala con monitoraggio, reporting e pianificazione, consentendo al contempo il trasferimento iniziale delle risorse agli store di dati cloud utilizzando i comuni strumenti di caricamento cloud. Vedere [strumento di importazione in blocco](/help/assets/add-assets.md#bulk-ingestion-tool).
Questo strumento è per gli amministratori di sistema, i consulenti o i partner di implementazione. Questa funzione consente l’inserimento su larga scala ed è ideale per l’assimilazione iniziale o per ingestione di grandi dimensioni. Per processi di assimilazione più piccoli, utilizzate l&#39;app [[!DNL Experience Manager] desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [il caricamento mediante l&#39;interfaccia utente di Assets](/help/assets/add-assets.md#upload-assets).

   ![Configurazione dell&#39;importatore di massa](/help/assets/assets/bulk-import-config-low-res.png)

* Gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne.

   ![ordinare risorse](/help/assets/assets/asset-sort-options.png)

* I seguenti miglioramenti sono stati apportati per l&#39;accessibilità in [ risorse di Experience Manager] in questa versione. Per ulteriori informazioni, vedere [funzioni di accessibilità in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il tasto Esc può comprimere l&#39;opzione Mostra tutto senza perdere lo stato attivo.
   * Quando si naviga utilizzando il tasto di tabulazione della tastiera, dopo aver rimosso l&#39;ultimo tag dai tag aggiunti, il campo del tag rimane attivo.
   * [!DNL Experience Manager] i componenti ora contengono informazioni appropriate per nome, ruolo e valore che devono essere utilizzati dagli assistenti vocali.
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, Collegamento, Lingua o Testo, lo stato attivo torna agli elementi dell&#39;interfaccia utente successivi o precedenti o a un elemento dell&#39;interfaccia utente più rilevante.
   * Quando si passa il puntatore sulle opzioni, vengono visualizzati suggerimenti come Seleziona e Scarica. Gli utenti che utilizzano una lente di ingrandimento dello schermo potrebbero non visualizzare le miniature dei file a causa di questi suggerimenti. Ora, è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando il tasto `Escape`.
   * Selezionando una cella della griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo.
   * Gli utenti visivi possono distinguere tra testo normale e collegamento, in quanto vengono visualizzati indizi visivi (sottolineatura e icona a forma di freccia) per i collegamenti a tutte le soluzioni nella pagina principale [!DNL Experience Manager].

* **Predefiniti set di batch per elementi multimediali** dinamici: Ora potete automatizzare la creazione e l’organizzazione di più risorse in un set di immagini o set 360 gradi al momento di caricare i file di risorse in una cartella singolarmente o utilizzando l’assimilazione in blocco.

   Consultate [I predefiniti per set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).

* I seguenti miglioramenti dell&#39;accessibilità sono ora disponibili in [!DNL Dynamic Media]:

   * Gli assistenti vocali (JAWS, Assistente vocale) indicano il nome, il ruolo e lo stato delle voci di menu nell&#39;opzione di menu Incorpora dimensioni.
   * Gli utenti possono navigare nella finestra di dialogo del collegamento E-mail utilizzando la chiave `Tab`.
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare, grazie al miglioramento dell’assistente vocale.
   * Quando si naviga utilizzando il tasto `Tab`, lo stato attivo si sposta sugli elementi dell&#39;interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo.
   * Sono state migliorate le pagine Pubblica, Modifica risorsa, Modifica Smart Crops e Editor set di immagini per soddisfare gli standard Web. Gli utenti della tecnologia di assistenza (AT) ora possono navigare facilmente in queste pagine e intraprendere azioni come il ritaglio delle immagini.
   * I visualizzatori sono stati migliorati per consentire agli utenti di spostarsi utilizzando una tastiera.
   * Gli utenti di tastiera e utilità di lettura dello schermo possono utilizzare la funzionalità di ritaglio.
   * Gli utenti della tastiera possono gestire meglio i punti di attivazione.

   Vedere [Accessibilità in [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.11.05 che include l&#39;ultima versione CIF Core Components v1.5.0. Per ulteriori informazioni, fare riferimento a [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27).

* Componenti CIF di base rilasciati v1.5.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0).

### Correzioni di bug {#bug-fixes-commerce}

* La configurazione client GraphQL non è stata letta correttamente se la configurazione non è specificata direttamente nella configurazione Sling CA, ma in una delle configurazioni padre. Questo è stato corretto.



## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.11.0 è il 12 novembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Una nuova opzione di menu **Accesso locale** è ora disponibile per gli utenti dalle opzioni del menu di ambiente nelle pagine di riepilogo **Ambienti** e **Ambienti** della scheda &lt;a2/>Ambienti&lt;a3/>.
Per ulteriori informazioni, fare riferimento a [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md##login-locally).

* La scheda **Informazioni** in Cloud Manager è stata aggiornata con le nuove immagini nell&#39;interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguite prima dell&#39;esecuzione della creazione richiede il download di un plug-in Maven.
* Il collegamento dal piè di pagina di Cloud Manager per selezionare una lingua ora passerà alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Ora verrà rilevato automaticamente e verrà tentato un riavvio.
* Tutte le condutture di produzione esistenti verranno automaticamente abilitate con il passaggio Experience Audit (Controllo esperienza).

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base al titolo del flusso di lavoro, al modello del flusso di lavoro, allo stato, all’iniziatore, al percorso di payload e alla data di inizio. Vedere [Istanze del flusso di lavoro di ricerca](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronizzazione utente {#user-sync}

* I dati utente, inclusi gli attributi di profilo e le appartenenze ai gruppi, possono essere memorizzati nel livello di pubblicazione. Ulteriori informazioni su questa funzione sono disponibili nella [documentazione relativa a registrazione, login e profilo utente](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analizzatori {#analyzers}

Il AEM come Cloud Service SDK Build Analyzer Maven Plugin rileva i problemi in un progetto maven, comprese le dipendenze mancanti. Offre agli sviluppatori l&#39;opportunità di individuare i problemi durante lo sviluppo locale, ben prima di distribuirli in ambienti Cloud con Cloud Manager. Per ulteriori informazioni, consultare la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) e [qui](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Miglioramento dell’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e inserimento. Messaggio aggiunto per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Content Transfer Tool saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo è stato corretto.

## Best practice Analyzer {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio di Best Practices Analyzer è il 13 novembre 2020.

### Novità in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Il Cloud Readiness Analyzer è ora Best Practices Analyzer (BPA). BPA fornisce una valutazione delle procedure ottimali dell&#39;implementazione AEM corrente e aiuta a valutare la disponibilità a passare da un&#39;istanza AEM esistente a AEM come Cloud Service.

* È stato aggiunto un nuovo rilevatore per rilevare l&#39;uso di `java.io.InputStream`, che può causare problemi se utilizzato in AEM come Cloud Service.

### Correzioni di bug {#bpa-bug-fixes}

* È stato corretto il bug che causava i positivi relativi al componente *textfield foundation*.
