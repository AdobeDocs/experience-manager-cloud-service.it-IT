---
title: Note sulla versione 2020.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] note sulla versione as a Cloud Service per 2020.11.0.'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 15%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 è il 2 dicembre 2020.
La seguente versione (2020.12.0) sarà del 17 dicembre 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Launches Hierarchy Management](/help/sites-cloud/authoring/launches/managing-pages.md) e [Future Timewarp](/help/sites-cloud/authoring/launches/preview.md)**: nuova interfaccia utente per aggiungere/rimuovere pagine all&#39;interno di un lancio e la navigazione del sito con Timewarp mostra lo stato futuro da Launches.

* **[Modelli per frammenti di contenuto estesi ed editor](/help/assets/content-fragments/content-fragments-models.md)**: nuove opzioni per la convalida di input su vari tipi di dati, tipo di dati Enumerazione migliorato con nuove visualizzazioni di moduli e il nome del modello per frammenti di contenuto è visualizzato e ricercabile nell&#39;interfaccia utente di Assets.

* **Ordina le pagine Live Copy disponibili per il rollout**: nuova opzione per ordinare le pagine Live Copy disponibili per il rollout utilizzando le proprietà [!UICONTROL Nome], [!UICONTROL Data ultima modifica] e [!UICONTROL Data ultimo rollout]. La [!UICONTROL Data ultimo rollout] per una pagina è una nuova proprietà introdotta.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità in [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* as a Cloud Service **Assegnazione di risorse in blocco**: fornisci ai clienti un servizio di acquisizione scalabile nativo per il cloud che utilizza l&#39;architettura [!DNL Experience Manager], inclusi i microservizi per le risorse. I casi d’uso principali includono l’acquisizione su larga scala con monitoraggio, reporting e pianificazione, consentendo al contempo il trasferimento iniziale delle risorse agli archivi di dati cloud utilizzando gli strumenti comuni di caricamento cloud. Consulta [strumento per l&#39;acquisizione in blocco delle risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

  Questo strumento è destinato agli amministratori di sistema, ai consulenti o ai partner di implementazione. Questa funzione consente l’acquisizione su larga scala ed è idealmente utilizzata durante l’acquisizione iniziale o, occasionalmente, in caso di acquisizione su larga scala. Per processi di acquisizione più piccoli, utilizza l&#39;[[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=it) o il [caricamento tramite l&#39;interfaccia utente di Assets](/help/assets/add-assets.md#upload-assets).

  ![Configurazione importazione in serie](/help/assets/assets/bulk-import-config-low-res.png)

* Ora gli utenti possono ordinare le risorse digitali nelle viste a schede e a colonne.

  ![ordinare le risorse](/help/assets/assets/asset-sort-options.png)

* I seguenti miglioramenti sono stati apportati per l&#39;accessibilità in [!DNL Experience Manager Assets] in questa versione. Per ulteriori informazioni, vedere [funzionalità di accesso facilitato in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il tasto Esc può comprimere l&#39;opzione Mostra tutto senza perdere lo stato attivo.
   * Quando ci si sposta utilizzando il tasto TAB, dopo aver rimosso l’ultimo tag dai tag aggiunti, il campo tag mantiene lo stato attivo.
   * I componenti [!DNL Experience Manager] ora contengono informazioni appropriate per il nome, la mansione e il valore che devono essere utilizzati dagli assistenti vocali.
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, la casella combinata Collegamento, la casella combinata Lingua o la casella di modifica Testo, lo stato attivo sulla tastiera ritorna agli elementi dell&#39;interfaccia utente successivi o precedenti o a un elemento dell&#39;interfaccia utente più rilevante.
   * Quando si passa il puntatore del mouse sulle opzioni, vengono visualizzati suggerimenti quali Seleziona e Scarica. Gli utenti che utilizzano una lente di ingrandimento potrebbero non visualizzare le miniature dei file a causa di questi suggerimenti. Ora è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando la chiave `Escape`.
   * Quando si seleziona una cella della griglia dalla griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo.
   * Gli utenti visivi possono distinguere tra testo normale e un collegamento, poiché vengono visualizzati indizi visivi (sottolineatura e icona con freccia) per i collegamenti a tutte le soluzioni nella home page di [!DNL Experience Manager].

* **Predefiniti per set di batch in Dynamic Media**: ora puoi automatizzare la creazione e l&#39;organizzazione di più risorse in un set di immagini o set 360 gradi al momento del caricamento dei file di risorse in una cartella singolarmente o utilizzando l&#39;acquisizione in blocco.

  Consulta [Informazioni sui predefiniti per set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).

* I seguenti miglioramenti all&#39;accessibilità sono ora disponibili in [!DNL Dynamic Media]:

   * Le utilità per la lettura dello schermo (JAWS, Assistente vocale) narrano il nome, il ruolo e lo stato delle voci di menu nell&#39;opzione di menu Dimensione incorporamento.
   * Gli utenti possono visualizzare la finestra di dialogo Collegamento e-mail utilizzando la chiave `Tab`.
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare, grazie al miglioramento apportato all’assistente vocale.
   * Quando si accede utilizzando il tasto `Tab`, lo stato attivo si sposta sugli elementi dell&#39;interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo.
   * Le pagine Publish, Modifica risorsa, Modifica ritagli avanzati e Editor set di immagini sono state migliorate per rispettare gli standard web. Gli utenti di Assistive Technology (AT) ora possono navigare facilmente in queste pagine e agire su di esse, ad esempio ritagliando immagini.
   * I visualizzatori sono stati migliorati per consentire agli utenti di navigare utilizzando una tastiera.
   * Gli utenti che utilizzano la tastiera e l’assistente vocale possono utilizzare la funzionalità di ritaglio.
   * Gli utenti che utilizzano la tastiera possono gestire meglio gli hotspot.

  Consulta [Accessibilità in [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stato rilasciato il sito di riferimento CIF Venia (2020.11.05), che include la versione più recente dei Componenti core CIF v1.5.0. Per ulteriori dettagli, consulta [Sito di riferimento per CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27).

* È stata rilasciata la versione 1.5.0 dei Componenti core CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0).

### Correzioni di bug {#bug-fixes-commerce}

* La configurazione del client GraphQL non è stata letta correttamente se non è specificata direttamente nella configurazione della CA Sling, ma in una delle configurazioni padre. Questo problema è stato risolto.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2020.11.0 è il 12 novembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Una nuova opzione di menu **Accesso locale** è ora disponibile per gli utenti dalle opzioni di menu dell&#39;ambiente nella scheda **Ambienti** e nelle pagine di riepilogo **Ambienti**.
Per ulteriori dettagli, consulta la [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#login-locally).

* La scheda **Scopri** in Cloud Manager è stata aggiornata aggiungendo nuove immagini nell’interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguito prima dell’esecuzione della build richiedeva di scaricare un plug-in Maven.
* Ora il collegamento per selezionare una lingua dal piè di pagina di Cloud Manager reindirizza alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Ora questo errore viene rilevato automaticamente e viene eseguito un tentativo di riavvio.
* Ora tutte le pipeline di produzione esistenti sono attivate automaticamente con il passaggio Audit dell’esperienza.

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze di flussi di lavoro basate su Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data inizio. Consulta [Istanze flusso di lavoro di ricerca](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html?lang=it).

### Sincronizzazione dei dati utente a livello di Publish {#user-sync}

* I dati utente, inclusi gli attributi di profilo e le appartenenze ai gruppi, possono essere memorizzati sul livello di pubblicazione. Ulteriori informazioni su questa funzione sono disponibili nella [Documentazione su registrazione, accesso e profilo utente](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analyzer {#analyzers}

Il plug-in Maven SDK Build Analyzer per AEM as a Cloud Service rileva i problemi in un progetto Maven, incluse eventuali dipendenze mancanti. Offre agli sviluppatori l’opportunità di individuare i problemi durante lo sviluppo locale, ben prima di distribuirli in ambienti Cloud con Cloud Manager. Per ulteriori informazioni, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it#developing) e [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it#building-for-the-sdk).

### Altri {#others-foundation}

Nuova sintassi [&quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) verifica la presenza di una configurazione di Apache e Dispatcher eseguita durante la compilazione di Cloud Manager, che può essere eseguita anche con gli strumenti Dispatcher dell&#39;SDK di AEM as a Cloud Service.

## Strumento trasferimento contenuti {#content-transfer-tool}

Segui questa sezione per scoprire le novità e gli aggiornamenti di [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Esperienza utente migliorata per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) ignorava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer è il 13 novembre 2020.

### Novità in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) è ora Best Practices Analyzer (BPA). BPA fornisce una valutazione delle best practice relative all’implementazione corrente dell’AEM e aiuta a stimare la fattibilità del passaggio da un’istanza AEM esistente ad AEM as a Cloud Service.

* È stato aggiunto un nuovo rilevatore per rilevare l&#39;utilizzo di `java.io.InputStream`, che può causare problemi se utilizzato in AEM as a Cloud Service.

### Correzioni di bug {#bpa-bug-fixes}

* È stato corretto un bug che causava la correzione dei positivi relativi al componente *textfield foundation*.
