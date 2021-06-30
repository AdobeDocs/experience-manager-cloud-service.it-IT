---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: ffca94ef8d93cf95011d7e3128c49929f69cdc28
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 è il 28 giugno 2021.
La versione seguente (2021.7.0) sarà del 29 luglio 2021.

## Video sulla versione {#release-video}

Per un riepilogo delle funzioni aggiunte, guarda il video [Panoramica sulla versione di giugno 2021](https://video.tv.adobe.com/v/334296) .

## Documentazione XML per AEM as a cloud Service {#xml-documentation}

### Novità {#what-is-new-xml-documentation}

* La documentazione XML per AEM come Cloud Service è ora GA.
* Ciò consentirà ai clienti esistenti di AEM Cloud Service di elaborare la documentazione XML da aggiungere per l’importazione, la creazione, la gestione e la distribuzione di contenuti tecnici su più canali, inclusi AEM siti

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM as a Cloud Service 2021.6.0 e 2021.5.0.

### Data di rilascio {#release-date-june-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.6.0 è il 10 giugno 2021.
La prossima versione è prevista per il 15 luglio 2021.

### Novità {#what-is-new-junecm}

* Preview Service verrà distribuito su base continua a tutti i programmi. I clienti riceveranno una notifica interna al prodotto quando il loro programma è abilitato per Preview Service. Per ulteriori informazioni, consulta [Accesso al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) .

* Le dipendenze Maven scaricate durante il passaggio di creazione ora verranno memorizzate nella cache tra le esecuzioni della pipeline. Questa funzione verrà attivata per i clienti nelle prossime settimane.

* È ora possibile modificare il nome del programma tramite la finestra di dialogo modifica programma.

* Il nome del ramo predefinito utilizzato sia durante la creazione del progetto che nel comando push predefinito tramite gestione flussi di lavoro Git è stato modificato in `main`.

* L’esperienza di modifica del programma nell’interfaccia utente è stata aggiornata.

* La regola di qualità `ImmutableMutableMixCheck` è stata aggiornata per classificare i nodi `/oak:index` come immutabili.

* Le regole di qualità `CQBP-84` e `CQBP-84--dependencies` sono state consolidate in un’unica regola. Come parte di questo consolidamento, la scansione delle dipendenze identifica più accuratamente i problemi nelle dipendenze di terze parti che vengono distribuiti nel runtime di AEM.

* Per evitare confusione, le righe del segmento Pubblica AEM e Pubblica dispatcher nella pagina Dettagli ambiente sono state consolidate.

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* È stata aggiunta una nuova regola di qualità del codice per convalidare la struttura degli indici `damAssetLucene`. Per ulteriori informazioni, consulta [Indici Oak di risorsa Lucene personalizzati DAM](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) .

* Nella pagina dei dettagli dell’ambiente vengono ora visualizzati più nomi di dominio per i servizi di pubblicazione e anteprima (a seconda dei casi). Per ulteriori informazioni, consulta [Dettagli ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) .

### Correzioni di bug {#bug-fixes-junecm}

* Le definizioni dei nodi JCR contenenti una nuova riga dopo che il nome dell&#39;elemento principale non è stato analizzato correttamente.

* L&#39;API degli archivi di elenchi non filtrerebbe gli archivi eliminati.

* Veniva visualizzato un messaggio di errore non corretto quando veniva fornito un valore non valido per il passaggio di pianificazione.

* A volte, l&#39;utente può visualizzare uno stato verde *attivo* accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Alcune sequenze di modifica dei programmi potrebbero impedire la creazione o la modifica della pipeline di produzione.

* Alcune sequenze di modifica del programma potrebbero causare la visualizzazione di un messaggio fuorviante della pagina **Panoramica** per la riesecuzione della configurazione del programma.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#ga-features-assets}

* La funzionalità di automazione dei contenuti consente a [!DNL Experience Manager Assets] di sfruttare le API [!DNL Adobe Creative Cloud] per automatizzare la produzione delle risorse su larga scala. Migliora la velocità dei contenuti riducendo notevolmente il tempo impiegato e le iterazioni necessarie per creare varianti della stessa risorsa. La funzionalità non richiede alcuna programmazione e funziona dall’interno di DAM. Consulta [Generare varianti di risorse utilizzando l’integrazione Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Adobe Asset Link] Viene rilasciata la versione 3.0 per  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator],  [!DNL Adobe InDesign] e  [!DNL Adobe Asset Link] la versione 2.0 per  [!DNL Adobe XD] . Fornisce:

   * Supporto per [!DNL Assets Essentials].
   * Possibilità di connettersi automaticamente a [!DNL Experience Manager] come [!DNL Cloud Service] o [!DNL Assets Essentials].

* Lo strumento [Asset Bulk Ingestor](/help/assets/add-assets.md#asset-bulk-ingestor) consente di aggiungere metadati durante un’acquisizione in blocco.

### Nuove funzioni disponibili nel canale pre-rilascio [!DNL Assets] {#beta-features-assets}

* Le impostazioni di visualizzazione vengono migliorate per consentire agli utenti di scegliere una vista predefinita e un parametro di ordinamento predefinito.

   ![Imposta la visualizzazione predefinita in Impostazioni vista](/help/assets/assets/view-settings-for-defaults.png)

* La funzionalità di download di Linkshare utilizza download asincroni che aumentano la velocità di download.

* Gli utenti possono cercare e filtrare le cartelle in base ai predicati delle proprietà.

   ![Filtrare le cartelle di ricerca utilizzando i predicati di ricerca](/help/assets/assets/search-folders-via-predicates.png)

* [!DNL Experience Manager Assets] incorpora il visualizzatore PDF per visualizzare in anteprima i formati di documento supportati. È alimentato da [!DNL Adobe Document Cloud]. Questa funzione consente agli utenti di visualizzare in anteprima PDF e altri file multipagina senza alcuna elaborazione complessa. Questo migliora la parità delle funzioni con [!DNL Experience Manager] 6.5.

   ![Anteprima di file PDF  [!DNL Experience Manager] con visualizzatore PDF](/help/assets/assets/preview-pdf-file-viewer.png)

### Bug corretti in [!DNL Assets] {#bugs-fixed-assets}

* Quando aggiungi un proprietario a una sottocartella, [!DNL Assets] aggiunge anche lo stesso utente di un proprietario della cartella principale. (CQ-4323737)
* Quando si aggiungono risorse alle raccolte, se un utente applica un filtro alla ricerca Raccolte, non può visualizzare le Raccolte nella vista Elenco. (CQ-4323181)
* Durante la ricerca di file e cartelle, se l&#39;utente applica un filtro e seleziona [!UICONTROL File e cartelle], vengono visualizzati solo i file ma non la cartella. (CQ-4319543)

## [!DNL Experience Manager Sites] come  [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#ga-features-sites}

* Pubblica nel livello anteprima ora mostrato come stato della pagina nell’interfaccia utente di amministrazione di Sites
* Pubblica nel livello di anteprima ora con l’URL di anteprima alla fine dell’azione e la persistenza dell’URL nelle proprietà della pagina per un riferimento successivo

## [!DNL Adobe Experience Manager Forms] come  [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* È stata aggiunta la possibilità di filtrare colonne personalizzate nella casella in entrata AEM.
* È stata aggiunta la possibilità di utilizzare l’editor di temi e il livello di stile dell’editor di moduli adattivi per personalizzare lo stile del componente captcha.
* Velocità e precisione migliorate per rilevare automaticamente le sezioni logiche nei PDF forms sorgente e convertirle in corrispondenti pannelli di moduli adattivi.
* È stata aggiunta l’azione Sposta per spostare un file PDF o XDP da una cartella all’altra.

### Funzione beta di [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: Le API di comunicazione consentono di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che consentono di:
   * Generare documenti modulo finali compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Genera PDF per la stampa da un modulo XFA PDF e Adobe Acrobat Form (AcroForm).

* **Esternalizzatore** dati variabile: È possibile salvare i dati delle variabili AEM flusso di lavoro su un sistema di storage esterno gestito dalla propria organizzazione.

Puoi scrivere su [!DNL formscsbeta@adobe.com] per iscriverti al programma beta.

### Bug corretti in [!DNL Forms] {#forms-bugs-fixed}

* Quando un campo viene convalidato prima dell’invio di dati al servizio back-end tramite Form Data Model (FDM), le convalide hanno esito positivo, ma il servizio Form Data Model non riesce ad avviare la convalida post-convalida.
* Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Questo è un problema noto in Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Adobe Experience Manager Screens] come  [!DNL Cloud Service] {#screens}

Questa sezione illustra le note sulla versione per AEM Screens as a Cloud Service.

### Data di rilascio {#release-date-june-screens}

La data di rilascio per AEM Screens as a Cloud Service è il 24 giugno 2021.

### Novità {#what-is-new-screens-june}

>[!NOTE]
>Per informazioni sulle nozioni fondamentali necessarie per la corretta installazione, configurazione ed esecuzione di Screens come Cloud Service, consulta la [Guida di AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) e collega la documentazione tecnica sui concetti dettagliati.

* Gestione della registrazione di massa dei dispositivi significa che il provisioning di grandi quantità di dispositivi di riproduzione è più veloce ed efficiente.

* Sono state migliorate le opzioni di ricerca e filtro per ciascuna delle visualizzazioni di inventario Dispositivo, Visualizzazione e Canale.

* Lo snapshot dell&#39;integrità del dispositivo consente di risparmiare tempo, fornendo uno stato critico come uno sguardo.

* La pagina dei dettagli dell’oggetto offre un riepilogo delle informazioni più rilevanti per ciascun oggetto del progetto.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuovi tipi di dati di riferimento CIF per prodotti e categorie per Frammenti di contenuto (Incl. supporto per l&#39;interfaccia utente del selettore prodotti/categorie)
* Nuovo componente core Frammento di contenuto Commerce
* Ricerca di e-commerce full-text supportata nel backend AEM
* I componenti core di Commerce supportano la raccolta dati Adobe Commerce Sensei Recs
* URL ottimizzati per l’ottimizzazione SEO (Search Engine Optimization) per le pagine di categorie
* Supporto per intestazioni HTTP personalizzate per sito/configurazione

## Strumento Content Transfer (Trasferimento contenuti)  {#content-transfer-tool}

### Data di rilascio {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.5.4 è il 28 giugno 2021.

### Novità {#what-is-new-ctt-latest}

* È stato aggiunto il supporto per un passaggio [pre-copy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) facoltativo da utilizzare con CTT. Il passaggio di pre-copia può essere utilizzato per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti quando l’istanza di AEM di origine è configurata per l’utilizzo di un archivio dati di archiviazione BLOB di Amazon S3 o Azure.

* Guardrail aggiunto al CTT per evitare che gli utenti interrompano un’acquisizione e potenzialmente danneggiano i dati una volta raggiunto il punto critico durante la fase di acquisizione.

* I registri di estrazione sono più descrittivi per facilitare la risoluzione dei problemi.

* Nell’interfaccia utente sono stati aggiunti messaggi di stato dell’acquisizione più descrittivi.

### Correzioni di bug {#bug-fixes-ctt-latest}

* Durante l’arresto di un’acquisizione sull’istanza Author, l’interfaccia utente ha sovrascritto un’acquisizione precedente sull’istanza Publish in `STOPPED` da `FINISHED`. Questo problema è stato risolto.


