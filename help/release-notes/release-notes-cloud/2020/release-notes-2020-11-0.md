---
title: Note sulla versione 2020.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service - Note sulla versione 2020.11.0.'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 4%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 è il 2 dicembre 2020.
La versione seguente (2020.12.0) sarà del 17 dicembre 2020

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Avvia Gestione](/help/sites-cloud/authoring/launches/managing-pages.md)  Gerarchia e Timewarp  [futuro](/help/sites-cloud/authoring/launches/preview.md)**: Nuova interfaccia utente per aggiungere/rimuovere pagine all’interno di un lancio, mentre la navigazione nel sito con Timewarp mostra lo stato futuro da Lanci.

* **[Editor e modelli di frammenti di contenuto estesi](/help/assets/content-fragments/content-fragments-models.md)**: Nell’interfaccia utente Assets sono disponibili nuove opzioni per la convalida dell’input per vari tipi di dati, sono stati migliorati il tipo di dati Enumerazione con nuove visualizzazioni del modulo e il nome del modello Frammento di contenuto.

* **Ordina le pagine Live Copy disponibili per il rollout**: Nuova opzione per ordinare le pagine Live Copy disponibili per il rollout utilizzando le proprietà  [!UICONTROL Nome],  [!UICONTROL Data] ultima modifica e  [!UICONTROL Data ultimo rollout ] . La [!UICONTROL Data ultimo rollout] per una pagina è una nuova proprietà introdotta.

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

### Novità in [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Acquisizione** di risorse in blocco: Fornisci ai clienti un servizio di acquisizione scalabile e nativo per il cloud che sfrutta  [!DNL Experience Manager] come architettura di Cloud Service, inclusi i microservizi per le risorse. I casi d’uso principali includono l’acquisizione su larga scala con monitoraggio, reporting e pianificazione, consentendo al contempo il trasferimento iniziale di risorse agli archivi di dati cloud utilizzando strumenti comuni per il caricamento di cloud. Consulta [strumento per l’inserimento di massa delle risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

   Questo strumento è destinato agli utenti tipo amministratore di sistema, consulente o partner di implementazione. Questa funzione consente l’acquisizione su larga scala ed è ideale durante l’acquisizione iniziale o durante l’ingestione di grandi dimensioni. Per lavori di acquisizione più piccoli, utilizza l’ [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [carica utilizzando l’interfaccia utente di Assets](/help/assets/add-assets.md#upload-assets).

   ![Configurazione dell&#39;importatore di massa](/help/assets/assets/bulk-import-config-low-res.png)

* Gli utenti possono ora ordinare le risorse digitali nelle viste a schede e a colonne.

   ![ordinare risorse](/help/assets/assets/asset-sort-options.png)

* I seguenti miglioramenti sono stati apportati all’accessibilità in [!DNL Experience Manager Assets] in questa versione. Per ulteriori informazioni, consulta [funzioni di accessibilità in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il tasto ESC può comprimere l’opzione Mostra tutto senza perdere lo stato attivo.
   * Quando si naviga utilizzando il tasto di tabulazione della tastiera, dopo aver rimosso l’ultimo tag dai tag aggiunti, il campo tag mantiene lo stato attivo.
   * [!DNL Experience Manager] i componenti ora contengono informazioni appropriate per nome, ruolo e valore che devono essere utilizzati dagli assistenti vocali.
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, la casella combinata Collegamento, la casella combinata Lingua o la casella di modifica Testo, lo stato attivo torna sugli elementi dell’interfaccia utente successivi o precedenti o su un elemento dell’interfaccia utente più pertinente.
   * Quando si passa il puntatore del mouse sulle opzioni, vengono visualizzati suggerimenti come Seleziona e Scarica . Gli utenti che utilizzano una lente di ingrandimento dello schermo potrebbero non vedere le miniature dei file a causa di questi suggerimenti. Ora è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando il tasto `Escape`.
   * Selezionando una cella della griglia dalla griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo.
   * Gli utenti visivi possono distinguere tra testo normale e collegamento, in quanto vengono visualizzati indizi visivi (sottolineatura e icona freccia) per i collegamenti a tutte le soluzioni nella home page di [!DNL Experience Manager].

* **Predefiniti set di batch in Dynamic Media**: Ora puoi automatizzare la creazione e l’organizzazione di più risorse in un set di immagini o set 360 gradi al momento del caricamento dei file di risorse in una cartella singolarmente o tramite l’acquisizione in massa.

   Consulta [Informazioni sui predefiniti per set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).

* I seguenti miglioramenti dell’accessibilità sono ora disponibili in [!DNL Dynamic Media]:

   * Gli assistenti vocali (JAWS, Assistente vocale) indicano il nome, il ruolo e lo stato delle voci di menu nell’opzione di menu Incorpora dimensioni.
   * Gli utenti possono navigare nella finestra di dialogo Collegamento e-mail utilizzando il tasto `Tab` .
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare in considerazione dei miglioramenti apportati all’assistente vocale.
   * Quando si naviga utilizzando il tasto `Tab`, lo stato attivo si sposta sugli elementi dell’interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo.
   * Le pagine Pubblica , Modifica risorsa , Modifica ritaglio avanzato e Editor set di immagini sono state migliorate per conformarsi agli standard web. Gli utenti della tecnologia di assistenza (AT, Assistive Technology) ora possono navigare facilmente in queste pagine e intraprendere azioni come il ritaglio delle immagini.
   * I visualizzatori sono stati migliorati per consentire agli utenti di navigare utilizzando una tastiera.
   * Gli utenti di tastiera e assistenti vocali possono utilizzare la funzionalità di ritaglio.
   * Gli utenti di tastiera possono gestire meglio gli hotspot.

   Consultare [Accessibilità in [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.11.05 che include l’ultima versione dei componenti core CIF v1.5.0. Per ulteriori informazioni, consulta [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) .

* È stata rilasciata la versione 1.5.0 dei componenti core CIF. Per ulteriori informazioni, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) .

### Correzioni di bug {#bug-fixes-commerce}

* La configurazione client GraphQL non è stata letta correttamente quando la configurazione non è specificata direttamente nella configurazione Sling CA, ma in una delle configurazioni principali. Questo problema è stato risolto.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.11.0 è il 12 novembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* È ora disponibile una nuova opzione di menu **Accesso locale** per gli utenti dalle opzioni del menu di ambiente nelle pagine di riepilogo **Ambienti** e **Ambienti** .
Per ulteriori informazioni, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#login-locally) .

* La scheda **Informazioni** in Cloud Manager è stata aggiornata con le nuove immagini nell’interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguito prima dell’esecuzione della build richiede il download di un plug-in Maven.
* Il collegamento dal piè di pagina di Cloud Manager per selezionare una lingua passerà ora alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Questo verrà rilevato automaticamente e verrà tentato un riavvio.
* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base a Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data di inizio. Consulta [Ricerca istanze flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronizzazione dei dati utente a livello di pubblicazione {#user-sync}

* I dati utente, inclusi gli attributi di profilo e le appartenenze al gruppo, possono essere mantenuti sul livello di pubblicazione. Ulteriori informazioni su questa funzione sono disponibili nella [documentazione Registrazione, accesso e profilo utente](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analytics {#analyzers}

Il plug-in Maven AEM as a Cloud Service SDK Build Analyzer rileva i problemi in un progetto Maven, incluse le dipendenze mancanti. Offre agli sviluppatori l’opportunità di scoprire i problemi durante lo sviluppo locale, molto prima di distribuirli in ambienti Cloud con Cloud Manager. Per ulteriori informazioni, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) e [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Altro {#others-foundation}

Nuova sintassi [&quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) controlla la configurazione di apache e dispatcher eseguita durante la build di Cloud Manager, che può essere eseguita anche utilizzando AEM come strumenti Dispatcher dell’SDK di Cloud Service.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novità {#what-is-new-ctt}

* Migliorata l’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio di Best Practices Analyzer è il 13 novembre 2020.

### Novità in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) è ora Best Practices Analyzer (BPA). BPA fornisce una valutazione delle best practice dell’implementazione AEM corrente e aiuta a valutare la disponibilità a passare da un’istanza AEM esistente a AEM come Cloud Service.

* È stato aggiunto un nuovo rilevatore per rilevare l’utilizzo di `java.io.InputStream`, che può causare problemi se utilizzato in AEM come Cloud Service.

### Correzioni di bug {#bpa-bug-fixes}

* È stato corretto un bug che causava la correzione dei positivi relativi al componente *textfield foundation* .
