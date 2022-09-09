---
title: Note sulla versione 2020.11.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione as a Cloud Service per 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 11%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 è il 2 dicembre 2020.
La versione seguente (2020.12.0) sarà del 17 dicembre 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* **[Avvia la gestione della gerarchia](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Timewarp futuro](/help/sites-cloud/authoring/launches/preview.md)**: Nuova interfaccia utente per aggiungere/rimuovere pagine all’interno di un lancio, mentre la navigazione nel sito con Timewarp mostra lo stato futuro da Lanci.

* **[Editor e modelli per frammenti di contenuto estesi](/help/assets/content-fragments/content-fragments-models.md)**: Nell’interfaccia utente Assets sono disponibili nuove opzioni per la convalida dell’input per vari tipi di dati, sono stati migliorati il tipo di dati Enumerazione con nuove visualizzazioni del modulo e il nome del modello Frammento di contenuto.

* **Ordinare le pagine Live Copy disponibili per il rollout**: Nuova opzione per ordinare le pagine Live Copy disponibili per il rollout utilizzando [!UICONTROL Nome], [!UICONTROL Data ultima modifica]e [!UICONTROL Data ultimo rollout] proprietà. La [!UICONTROL Data ultimo rollout] per una pagina è stata introdotta una nuova proprietà .

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità di [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Acquisizione in blocco di risorse**: Fornisci ai clienti un servizio di acquisizione scalabile e nativo per il cloud che sfrutta [!DNL Experience Manager] Architettura as a Cloud Service, inclusi i microservizi per le risorse. I casi d’uso chiave includono l’acquisizione su larga scala con monitoraggio, reporting e pianificazione, consentendo al contempo il trasferimento iniziale di risorse agli archivi di dati cloud utilizzando comuni strumenti di caricamento cloud. Vedi [strumento di acquisizione collettiva risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

   Questo strumento è destinato agli utenti tipo amministratore di sistema, consulente o partner di implementazione. Questa funzione consente l’acquisizione su larga scala ed è ideale durante l’acquisizione iniziale o durante l’ingestione di grandi dimensioni. Per i processi di acquisizione più piccoli, utilizza la variabile [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [caricare utilizzando l’interfaccia utente Assets](/help/assets/add-assets.md#upload-assets).

   ![Configurazione dell&#39;importatore di massa](/help/assets/assets/bulk-import-config-low-res.png)

* Gli utenti possono ora ordinare le risorse digitali nelle viste a schede e a colonne.

   ![ordinare risorse](/help/assets/assets/asset-sort-options.png)

* I seguenti miglioramenti sono stati apportati all’accessibilità in [!DNL Experience Manager Assets] in questa versione. Per ulteriori informazioni, consulta [funzioni di accessibilità in [!DNL Assets]](/help/assets/accessibility.md).

   * Quando si naviga nella timeline utilizzando una tastiera, il tasto ESC può comprimere l’opzione Mostra tutto senza perdere lo stato attivo.
   * Quando si naviga utilizzando il tasto di tabulazione della tastiera, dopo aver rimosso l’ultimo tag dai tag aggiunti, il campo tag mantiene lo stato attivo.
   * [!DNL Experience Manager] i componenti ora contengono informazioni appropriate per nome, ruolo e valore che devono essere utilizzati dagli assistenti vocali.
   * Dopo aver eliminato la casella combinata Tipo/Dimensione, la casella combinata Collegamento, la casella combinata Lingua o la casella di modifica Testo, lo stato attivo torna sugli elementi dell’interfaccia utente successivi o precedenti o su un elemento dell’interfaccia utente più pertinente.
   * Quando si passa il puntatore del mouse sulle opzioni, vengono visualizzati suggerimenti come Seleziona e Scarica . Gli utenti che utilizzano una lente di ingrandimento dello schermo potrebbero non vedere le miniature dei file a causa di questi suggerimenti. Ora, è possibile mantenere lo stato attivo, dopo aver rimosso l&#39;opzione utilizzando `Escape` chiave.
   * Selezionando una cella della griglia dalla griglia presente nella pagina, lo stato attivo si sposta sulla barra delle azioni visualizzata sullo schermo.
   * Gli utenti visivi possono distinguere tra testo normale e collegamento, in quanto vengono visualizzati indizi visivi (sottolineatura e icona freccia) per i collegamenti a tutte le soluzioni in [!DNL Experience Manager] home page.

* **Predefiniti set di batch in Dynamic Media**: Ora puoi automatizzare la creazione e l’organizzazione di più risorse in un set di immagini o set 360 gradi al momento del caricamento dei file di risorse in una cartella singolarmente o tramite l’acquisizione in massa.

   Vedi [Informazioni sui predefiniti per set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).

* I seguenti miglioramenti dell’accessibilità sono ora disponibili in [!DNL Dynamic Media]:

   * Gli assistenti vocali (JAWS, Assistente vocale) indicano il nome, il ruolo e lo stato delle voci di menu nell’opzione di menu Incorpora dimensioni.
   * Gli utenti possono navigare nella finestra di dialogo Collegamento e-mail utilizzando `Tab` chiave.
   * Il flusso di lavoro per la creazione di profili di codifica video è più semplice da usare in considerazione dei miglioramenti apportati all’assistente vocale.
   * Durante la navigazione con `Tab` lo stato attivo si sposta sugli elementi dell’interfaccia utente appropriati nel flusso di lavoro per creare un video interattivo.
   * Le pagine Pubblica , Modifica risorsa , Modifica ritaglio avanzato e Editor set di immagini sono state migliorate per conformarsi agli standard web. Gli utenti della tecnologia di assistenza (AT, Assistive Technology) ora possono navigare facilmente in queste pagine e intraprendere azioni come il ritaglio delle immagini.
   * I visualizzatori sono stati migliorati per consentire agli utenti di navigare utilizzando una tastiera.
   * Gli utenti di tastiera e assistenti vocali possono utilizzare la funzionalità di ritaglio.
   * Gli utenti di tastiera possono gestire meglio gli hotspot.

   Vedi [Accessibilità in [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.11.05 che include l’ultima versione dei componenti core CIF versione v1.5.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) per ulteriori dettagli.

* Componenti core CIF rilasciati v1.5.0. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-commerce}

* La configurazione client GraphQL non è stata letta correttamente quando la configurazione non è specificata direttamente nella configurazione Sling CA, ma in una delle configurazioni principali. Questo problema è stato risolto.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.11.0 è il 12 novembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Una nuova opzione di menu **Accesso locale** è ora disponibile per gli utenti dalle opzioni del menu di ambiente nella **Ambienti** carta e **Ambienti** pagine di riepilogo.
Fai riferimento a [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#login-locally) per ulteriori dettagli.

* La **Scopri** In Cloud Manager è stata aggiornata la scheda con le nuove immagini nell’interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguito prima dell’esecuzione della build richiede il download di un plug-in Maven.
* Il collegamento dal piè di pagina di Cloud Manager per selezionare una lingua passerà ora alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Questo verrà rilevato automaticamente e verrà tentato un riavvio.
* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .

## Fondamenti di Adobe Experience Manager as a Cloud Service {#cloud-service-foundation}

### Flussi di lavoro {#workflows}

* È stato aggiunto il supporto per la ricerca di istanze del flusso di lavoro in base a Titolo flusso di lavoro, Modello flusso di lavoro, Stato, Iniziatore, Percorso payload e Data di inizio. Vedi [Cerca istanze del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronizzazione dei dati utente a livello di pubblicazione {#user-sync}

* I dati utente, inclusi gli attributi di profilo e le appartenenze al gruppo, possono essere mantenuti sul livello di pubblicazione. Ulteriori informazioni su questa funzione in [Documentazione di registrazione, accesso e profilo utente](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analyzer {#analyzers}

Il plug-in Maven SDK Build Analyzer per AEM as a Cloud Service rileva i problemi in un progetto Maven, incluse eventuali dipendenze mancanti. Offre agli sviluppatori l’opportunità di individuare i problemi durante lo sviluppo locale, molto prima che vengano distribuiti in ambienti Cloud con Cloud Manager. Per ulteriori informazioni, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it#developing) e [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Altro {#others-foundation}

Nuovo [Sintassi &quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) controlla la configurazione di apache e dispatcher eseguita durante la build di Cloud Manager, che può essere eseguita anche utilizzando AEM strumenti di Dispatcher dell’SDK as a Cloud Service.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di [Strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versione v1.1.12.

### Novità {#what-is-new-ctt}

* Migliorata l’esperienza utente per i registri. Marca temporale aggiunta ai registri di estrazione e acquisizione. È stato aggiunto un messaggio per indicare se i registri sono vuoti.

### Correzioni di bug {#ctt-bug-fixes}

* Lo strumento Content Transfer (Trasferimento contenuti) saltava i file di contenuto se il set di migrazione conteneva percorsi con nomi di file parzialmente simili. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer è il 13 novembre 2020.

### Novità in [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) è ora Best Practices Analyzer (BPA). BPA fornisce una valutazione delle best practice dell’implementazione AEM corrente e aiuta a valutare la disponibilità a passare da un’istanza AEM esistente a AEM as a Cloud Service.

* È stato aggiunto un nuovo rilevatore per rilevare l&#39;utilizzo di `java.io.InputStream`, che può causare problemi se utilizzato in AEM as a Cloud Service.

### Correzioni di bug {#bpa-bug-fixes}

* Bug che causa i positivi relativi al *textfield foundation* componente fisso.
