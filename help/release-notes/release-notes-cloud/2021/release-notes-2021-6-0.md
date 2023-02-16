---
title: Note sulla versione 2021.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 34%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 è il 28 giugno 2021.
La versione seguente (2021.7.0) sarà del 29 luglio 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di giugno 2021](https://video.tv.adobe.com/v/334296) video per un riepilogo delle funzioni aggiunte.

## XML Documentation for AEM as a cloud Service {#xml-documentation}

### Novità {#what-is-new-xml-documentation}

* XML Documentation per AEM as a Cloud Service è ora GA.
* In questo modo, i clienti AEM Cloud Service esistenti potranno acquistare addon XML Documentation per l’importazione, la creazione, la gestione e la distribuzione di contenuti tecnici su più canali, compresi i siti di AEM

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM 2021.6.0 e 2021.5.0.

### Data di pubblicazione {#release-date-june-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.6.0 è il 10 giugno 2021.
La prossima versione è prevista per il 15 luglio 2021.

### Novità {#what-is-new-junecm}

* Ora il servizio di anteprima viene distribuito su base continua per tutti i programmi. Quando il programma sarà abilitato per il servizio di anteprima, i clienti riceveranno una notifica interna al prodotto. Per ulteriori informazioni, consulta [Accedere al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

* Ora le dipendenze Maven scaricate durante la fase di build vengono memorizzate nella cache tra le esecuzioni della pipeline. La funzione verrà attivata per i clienti nelle prossime settimane.

* Ora è possibile modificare il nome del programma tramite la finestra di dialogo Modifica programma.

* Il nome del ramo predefinito utilizzato sia durante la creazione del progetto sia nel comando push predefinito tramite Gestione flussi di lavoro Git è stato modificato in `main`.

* L’esperienza di modifica del programma nell’interfaccia utente è stata aggiornata.

* La regola di qualità `ImmutableMutableMixCheck` è stata aggiornata per classificare i nodi `/oak:index` come non modificabili.

* Le regole di qualità `CQBP-84` e `CQBP-84--dependencies` sono state consolidate in un’unica regola. Come parte di tale consolidamento, la scansione delle dipendenze identifica più accuratamente i problemi nelle dipendenze di terze parti che vengono distribuiti nel runtime di AEM.

* Per evitare confusione, nella pagina Dettagli dell’ambiente sono state consolidate le righe del segmento Pubblica AEM e Pubblica Dispatcher.

   ![](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* È stata aggiunta una nuova regola di qualità del codice per convalidare la struttura degli indici `damAssetLucene`. Per ulteriori informazioni, consulta [Indici Oak DAM Asset Lucene personalizzati](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check).

* Ora nella pagina Dettagli dell’ambiente vengono visualizzati più nomi di dominio per i servizi Publish e Anteprima (a seconda dei casi). Per ulteriori informazioni, consulta [Dettagli dell’ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).

### Correzioni di bug {#bug-fixes-junecm}

* Le definizioni dei nodi JCR contenenti una nuova riga dopo il nome dell’elemento radice non venivano analizzate correttamente.

* L’API Elenca archivi non filtrava gli archivi eliminati.

* Veniva visualizzato un messaggio di errore non corretto quando si forniva un valore non valido nel passaggio di pianificazione.

* A volte l’utente visualizzava uno stato verde *attivo* a fianco di un elenco IP consentiti anche quando tale configurazione non era stata distribuita.

* Alcune sequenze di modifica dei programmi impedivano la creazione o la modifica della pipeline di produzione.

* Alcune sequenza di modifica dei programmi causavano la visualizzazione di un messaggio errato nella pagina **Anteprima**, che indicava di rieseguire la configurazione del programma.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#ga-features-assets}

* Funzionalità di automazione dei contenuti [!DNL Experience Manager Assets] sfruttare [!DNL Adobe Creative Cloud] API per automatizzare la produzione di risorse su larga scala. Migliora la velocità dei contenuti riducendo notevolmente il tempo impiegato e le iterazioni necessarie per creare varianti della stessa risorsa. La funzionalità non richiede alcun codice e funziona dall’interno di DAM.
* [!DNL Adobe Asset Link] v3.0 per [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] e [!DNL Adobe Asset Link] v2.0 per [!DNL Adobe XD] viene rilasciato. Fornisce:

   * Supporto per [!DNL Assets Essentials].
   * Possibilità di connettersi automaticamente a [!DNL Experience Manager] come [!DNL Cloud Service] o [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nuove funzioni disponibili in [!DNL Assets] canale prerelease {#beta-features-assets}

* Le impostazioni di visualizzazione vengono migliorate per consentire agli utenti di scegliere una vista predefinita e un parametro di ordinamento predefinito.
* La funzionalità di download di Linkshare utilizza download asincroni che aumentano la velocità di download.
* Gli utenti possono cercare e filtrare le cartelle in base ai predicati delle proprietà.
* [!DNL Experience Manager Assets] incorpora il visualizzatore PDF basato su [!DNL Adobe Document Cloud] per visualizzare in anteprima i documenti supportati. Questa funzione consente agli utenti di visualizzare in anteprima i file PDF e altri file multipagina senza alcuna elaborazione complessa. Ciò migliora la parità delle funzioni con [!DNL Experience Manager] 6.5.

### Bug fissati in [!DNL Assets] {#bugs-fixed-assets}

* Quando si aggiunge un proprietario a una sottocartella, [!DNL Assets] aggiunge anche lo stesso utente di un proprietario della cartella principale. (CQ-4323737)
* Quando si aggiungono risorse alle raccolte, se un utente applica un filtro alla ricerca Raccolte, non può visualizzare le Raccolte nella vista Elenco. (CQ-4323181)
* Durante la ricerca di file e cartelle, se l&#39;utente applica un filtro e seleziona [!UICONTROL File e cartelle], vengono visualizzati solo i file ma non la cartella . (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#ga-features-sites}

* Pubblica nel livello anteprima ora mostrato come stato della pagina nell’interfaccia utente di amministrazione di Sites
* Pubblica nel livello di anteprima ora con l’URL di anteprima alla fine dell’azione e la persistenza dell’URL nelle proprietà della pagina per un riferimento successivo

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* È stata aggiunta la possibilità di filtrare colonne personalizzate nella casella in entrata AEM.
* È stata aggiunta la possibilità di utilizzare l’editor di temi e il livello di stile dell’editor di moduli adattivi per personalizzare lo stile del componente captcha.
* Velocità e precisione migliorate per rilevare automaticamente le sezioni logiche nei PDF forms sorgente e convertirle in corrispondenti pannelli di moduli adattivi.
* È stata aggiunta l’azione Sposta per spostare un file PDF o XDP da una cartella all’altra.

### Funzione beta di [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: Le API di comunicazione consentono di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare documenti modulo finali compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form (AcroForm).

* **Esternalizzatore dati variabile**: È possibile salvare i dati delle variabili AEM flusso di lavoro su un sistema di storage esterno gestito dalla propria organizzazione.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Bug fissati in [!DNL Forms] {#forms-bugs-fixed}

* Quando un campo viene convalidato prima dell’invio di dati al servizio back-end tramite Form Data Model (FDM), le convalide hanno esito positivo, ma il servizio Form Data Model non riesce ad avviare la convalida post-convalida.
* Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Questo è un problema noto in Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

Questa sezione illustra le note sulla versione per AEM Screens as a Cloud Service.

### Data di pubblicazione {#release-date-june-screens}

La data di rilascio per AEM Screens as a Cloud Service è il 24 giugno 2021.

### Novità {#what-is-new-screens-june}

>[!NOTE]
>Vedi [AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) Guida alle conoscenze di base necessarie per la corretta installazione, configurazione ed esecuzione di Screens as a Cloud Service e collegamento alla documentazione tecnica dei concetti dettagliati.

* Gestione della registrazione di massa dei dispositivi significa che il provisioning di grandi quantità di dispositivi di riproduzione è più veloce ed efficiente.

* Sono state migliorate le opzioni di ricerca e filtro per ciascuna delle visualizzazioni di inventario Dispositivo, Visualizzazione e Canale.

* Lo snapshot dell&#39;integrità del dispositivo consente di risparmiare tempo, fornendo uno stato critico come uno sguardo.

* La pagina dei dettagli dell’oggetto offre un riepilogo delle informazioni più rilevanti per ciascun oggetto del progetto.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuovi tipi di dati di riferimento CIF per prodotti e categorie per Frammenti di contenuto (Incl. supporto per l&#39;interfaccia utente del selettore prodotti/categorie)
* Nuovo componente core Frammento di contenuto Commerce
* Ricerca di e-commerce full-text supportata nel backend AEM
* I componenti core di Commerce supportano la raccolta dati di Adobe Commerce Sensei Recs
* URL ottimizzati per l’ottimizzazione SEO (Search Engine Optimization) per le pagine di categorie
* Supporto per intestazioni HTTP personalizzate per sito/configurazione

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.5.4 è il 28 giugno 2021.

### Novità {#what-is-new-ctt-latest}

* Supporto per un [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) è stato aggiunto il passaggio da utilizzare con CTT. Il passaggio di pre-copia può essere utilizzato per accelerare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti quando l’istanza di AEM di origine è configurata per l’utilizzo di un archivio dati di archiviazione BLOB di Amazon S3 o Azure.

* Guardrail aggiunto al CTT per evitare che gli utenti interrompano un’acquisizione e potenzialmente danneggiano i dati una volta raggiunto il punto critico durante la fase di acquisizione.

* I registri di estrazione sono più descrittivi per facilitare la risoluzione dei problemi.

* Nell’interfaccia utente sono stati aggiunti messaggi di stato dell’acquisizione più descrittivi.

### Correzioni di bug {#bug-fixes-ctt-latest}

* Durante l’arresto di un’acquisizione sull’istanza Author, l’interfaccia utente ha sovrascritto un’acquisizione precedente sull’istanza Publish in `STOPPED` da `FINISHED`. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.16 è il 30 giugno 2021.

### Novità {#what-is-new-bpa-latest}

* Possibilità di rilevare e segnalare i nodi figlio mancanti nelle cartelle in `/content/dam`.

* Possibilità di rilevare e segnalare la versione di Best Practices Analyzer utilizzata.

### Correzioni di bug {#bug-fixes-bpa-latest}

* Errore di registrazione relativo alla correzione di URS (Unsupported Repository Structure).
