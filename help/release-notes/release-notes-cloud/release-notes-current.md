---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 372e40eb90d87d9ed366e08a3c0117068542680b
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 34%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.3.0) è il 31 marzo 2022.
La versione seguente (2022.4.0) è del 28 aprile 2022.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di marzo 2022](https://video.tv.adobe.com/v/341465) video per un riepilogo delle funzioni aggiunte nella versione 2022.3.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] offre la flessibilità di [configurare un account alias](/help/assets/dynamic-media/dm-alias-account.md) nell’interfaccia utente, garantendo in tal modo l’aggiornamento degli URL predefiniti di Dynamic Media e del codice di incorporamento del visualizzatore. Questo è particolarmente utile ai fini dell’ottimizzazione SEO (Search Engine Optimization), per riflettere eventuali aggiornamenti apportati al contesto aziendale, ad esempio in caso di rebranding.

* Ora puoi utilizzare l’interfaccia utente di [!DNL Experience Manager Assets] per:

   * Configura le [rilevamento di risorse duplicate](/help/assets/manage-digital-assets.md#detect-duplicate-assets) in un archivio.

   * Configura [aggiunta di filigrane digitali](/help/assets/watermark-assets.md) alle immagini.

* Gli amministratori possono ora configurare il servizio e-mail per i download di grandi dimensioni. Consente agli utenti di [abilitare le notifiche e-mail per i download di grandi dimensioni](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) dall’interfaccia [!DNL Experience Manager Assets]. Al termine del processo di download, l’utente riceve una notifica e-mail contenente il collegamento di download della cartella zip archiviata.

* La funzione [Gestisci pubblicazione](/help/assets/manage-publication.md) viene migliorata con un’interfaccia utente migliorata. Gli utenti possono pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, [Aggiungi contenuto](/help/assets/manage-publication.md#add-content) all’elenco di pubblicazione dall’archivio DAM, [Includi impostazioni cartella](/help/assets/manage-publication.md#include-folder-settings) per pubblicare il contenuto delle cartelle selezionate e applicare i filtri, e [pianifica la pubblicazione](/help/assets/manage-publication.md#publish-assets-later) a una data o un’ora successiva.

### Nuove funzioni disponibili in [!DNL Assets] canale prerelease {#prerelease-features-assets}

* È possibile [ordinare tag](/help/assets/organize-assets.md#use-tags-to-organize-assets) durante la creazione di tag avanzati e quando si applicano filtri di ricerca utilizzando il predicato tags.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [API per la generazione di documenti](/help/forms/aem-forms-cloud-service-communications.md) combinare, ridisporre e convalidare i documenti PDF. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:

   * Assemblare documenti PDF.
   * Smontare i documenti PDF.
   * Conversione e convalida di documenti conformi a PDF/A.

* **Conversione automatica di PDF forms di dimensioni superiori a 15 pagine in moduli adattivi**: È ora possibile utilizzare il servizio automated forms conversion per convertire PDF forms con un massimo di 40 pagine in moduli adattivi. Il servizio ora fornisce l’opzione per convertire sezioni di moduli di dimensioni superiori a 15 pagine in frammenti di modulo adattivi. Consente di migliorare la velocità di rendering dei moduli convertiti e di caricare più facilmente i moduli di grandi dimensioni nell’editor di moduli adattivi.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms}

* **Utilizza XCI personalizzato per generare un documento di record**: È ora possibile utilizzare un file XCI personalizzato per impostare varie proprietà di un documento di record. Sostituisce l’XCI principale con le modifiche personalizzate.

* **Utilizzare il CAPTCHA invisibile in un modulo adattivo**: Puoi usare il CAPTCHA invisibile per mostrare la sfida CAPTCHA solo nel caso di un&#39;attività sospetta. Se non viene trovata alcuna attività sospetta, la sfida CAPTCHA non viene visualizzata.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Beta: Supporto per i componenti core di ricerca CIF di AEM Commerce LiveSearch
* SEO migliorato per scenari multi-store: È ora possibile configurare i formati URL per PDP/PLP a livello di archivio tramite le proprietà CIF Cloud Config
* Il selettore prodotti supporta i prodotti in staging tramite la nuova opzione di filtro nell’interfaccia utente.  In questo modo i professionisti dei contenuti possono preparare la gestione dei contenuti dei prodotti per i prossimi lanci
* Gestione semplificata della configurazione CIF e degli errori utilizzando il nome della configurazione cloud CIF anziché l’URL proxy
* Selezione manuale della categoria per l’elenco dei prodotti e i componenti Carosello. Questo consente agli utenti del contenuto di utilizzare questi componenti sulle pagine di contenuto, al di fuori dell’esperienza del catalogo

## [!DNL Experience Manager] come [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* Per una risoluzione più efficiente ed efficace dei problemi relativi alle funzioni personalizzate negli ambienti Cloud, abbiamo rilasciato un nuovo strumento per sviluppatori: [Browser del repository](/help/implementing/developing/tools/repository-browser.md). È un browser HTML leggero e di sola lettura che può essere avviato da Developer Console. Ottieni visibilità nell’archivio dei contenuti sui livelli di pubblicazione, authoring e anteprima, e in tutti gli ambienti, compresi produzione, stage e sviluppo. Sfoglia la struttura del contenuto, visualizza le proprietà e visualizza in anteprima e scarica i binari.

   ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* Le credenziali utilizzate per autenticare le chiamate API da server a server (ad esempio, per le richieste API GraphQL) ora possono essere aggiornate prima della scadenza in modo self-service dalla Console per sviluppatori. Consulta la sezione [documentazione](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) per ulteriori informazioni.

* Le attività di manutenzione dell’eliminazione della versione e del registro di controllo, che non erano state precedentemente abilitate, verranno abilitate per i nuovi ambienti. Vedi i valori associati in [Attività di manutenzione](/help/operations/maintenance.md) articolo.

* AEM strumenti di Dispatcher SDK as a Cloud Service ora supportano i computer Mac con il chip M1

## Cloud Manager {#cloud-manager}

### Data di rilascio di febbraio {#release-date-cm-feb}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2022.02.0 è il 10 febbraio 2022. La prossima versione è prevista per il 10 marzo 2022.

### Novità {#what-is-new-cm-feb}

* Nuova accelerazione [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) sono stati introdotti per distribuire esclusivamente la configurazione HTTPD/dispatcher.
   * È necessario utilizzare AEM versione `2021.12.6151.20211217T120950Z` o più recenti e [consenso alla modalità flessibile degli strumenti del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per utilizzare questa funzione.
   * Questa funzione verrà implementata in un approccio graduale nelle due settimane successive al rilascio della versione 2022.02.0.
* L’esperienza della pagina di destinazione di Cloud Manager è stata aggiornata per fornire una navigazione migliore, un passaggio semplice tra le visualizzazioni griglia/riquadro e pop-up per un riepilogo rapido del programma.
* Una nuova soglia di errore (`< D`) è stato aggiunto al [metrica di valutazione dell’affidabilità.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * I clienti con gravi problemi di qualità che influiscono sulla stabilità del sistema, principalmente correlati a indici e processi di flusso di lavoro non validi, non saranno in grado di distribuire fino a quando tali problemi non saranno risolti.
* La gravità del `BannedPath` [regola di qualità](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) è stato modificato da blocker a critico.
* La procedura guidata della pipeline informerà l’utente quando potrebbe essere necessario un aggiornamento dell’ambiente AEM prima di configurare un [pipeline di configurazione a livello web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associato.

### Correzioni di bug {#bug-fixes-cm-feb}

* Le password dell’archivio Git precedente ora vengono sempre invalidate quando viene generata una nuova password.
* L’aggiornamento delle variabili di ambiente tramite l’API non interferisce più con l’esecuzione di una pipeline in rare situazioni.

### Data di rilascio di marzo {#release-date-cm-march}

La data di rilascio della versione 2022.3.0 di Cloud Manager in AEM 10 marzo 2022. La prossima versione è prevista per il 7 aprile 2022.

### Novità {#what-is-new-cm-march}

* Per accedere AEM registro dell’ambiente è possibile utilizzare il ruolo Sviluppatore .

### Correzioni di bug {#bug-fixes-cm-march}

* Un sottoinsieme di archivi Git creati manualmente presentava un valore di nome errato che impediva l’efficacia della funzione di riutilizzo degli artefatti di generazione. I nomi di tali archivi sono stati modificati e gli utenti vedranno il nome corretto nell’API/interfaccia utente di Cloud Manager.
* Gli artefatti di generazione da pipeline non di produzione sono stati riutilizzati in modo inappropriato sulle pipeline di stack complete di produzione.
* Quando si aggiunge o si modifica una pipeline di qualità del codice, le opzioni per gestire gli errori di metrica non vengono più visualizzate.
* Alcune configurazioni impreviste di variabili della pipeline potrebbero causare nel passaggio di compilazione.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.9.0 è il 28 febbraio 2022.

### Novità {#what-is-new-ctt}

* Controlla le dimensioni delle protezioni : la funzione di controllo dello strumento di trasferimento dei contenuti consente di ridurre i trasferimenti di contenuto non riusciti.  Con la funzione di controllo dimensioni, gli utenti possono 1) determinare se hanno spazio su disco sufficiente nel `crx-quickstart` sottodirectory prima dell’estrazione e 2) stimare le dimensioni del set di migrazione e verificare se è supportato. Se uno o entrambi questi controlli vengono violati, gli utenti visualizzeranno gli avvisi nell’interfaccia utente del CTT. Con questa soluzione puoi evitare errori di trasferimento dei contenuti e discutere in modo proattivo le opzioni di migrazione con l’Assistenza clienti di Adobe. Fai riferimento a [Determinazione delle dimensioni del set di migrazione e dello spazio su disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) per ulteriori dettagli.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.26 è il 16 marzo 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare le risorse non elaborate. Se vengono rilevate risorse non elaborate, tali risorse devono essere impostate su elaborate o devono essere rimosse dal set di migrazione durante il trasferimento del contenuto per evitare problemi durante l’assimilazione del contenuto.
* Possibilità di rilevare se il contenuto ha più di 1000 URL personalizzati. L’utilizzo di un numero elevato di URL personalizzati non è consigliato in quanto sovraccarica i server Dispatcher e Publish.
* Possibilità di identificare i problemi relativi alle definizioni degli indici Oak e di rilevare le incompatibilità con AEM as a Cloud Service.
* Possibilità di rilevare e creare rapporti sull’utilizzo delle configurazioni di Externalizer. In AEM as a Cloud Service le configurazioni di Externalizer sono impostate da Cloud Manager, pertanto le configurazioni esistenti di Externalizer devono essere reimpostate per mantenere la compatibilità.

### Correzioni di bug {#bug-fixes-bpa}

* In alcuni scenari, l’esecuzione di BPA non è riuscita a causa di un errore di asserzione generato da FormsSelectiveFeaturesAnalysis. Questo problema è stato risolto.
* BPA riportava i risultati relativi al modello WRK come PRINCIPALE invece di CRITICO. Questo problema è stato risolto.
* BPA riportava erroneamente i risultati relativi alle definizioni dell’indice OAK in ui.apps come CRITICO. Questo problema è stato risolto
