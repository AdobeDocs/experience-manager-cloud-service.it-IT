---
title: Note sulla versione 2021.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 48%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 è il 28 giugno 2021.
La seguente versione (2021.7.0) sarà del 29 luglio 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al video Panoramica sulla versione di [giugno 2021](https://video.tv.adobe.com/v/334296) per un riepilogo delle funzioni aggiunte.

## XML Documentation per AEM as a Cloud Service {#xml-documentation}

### Novità {#what-is-new-xml-documentation}

* XML Documentation per AEM as a Cloud Service è ora GA.
* Questo consentirà ai clienti AEM Cloud Service esistenti di acquistare XML Documentation Addon per importare, creare, gestire e distribuire contenuti tecnici su più canali, inclusi i siti AEM

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.6.0 e 2021.5.0.

### Data di pubblicazione {#release-date-june-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.6.0 è il 10 giugno 2021.
La prossima versione è prevista per l’venerdì 15 luglio 2021.

### Novità {#what-is-new-junecm}

* Ora il servizio di anteprima viene distribuito su base continua per tutti i programmi. Quando il programma sarà abilitato per il servizio di anteprima, i clienti riceveranno una notifica interna al prodotto. Per ulteriori informazioni, vedi [Accesso al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

* Ora le dipendenze Maven scaricate durante la fase di build vengono memorizzate nella cache tra le esecuzioni della pipeline. La funzione verrà abilitata per i clienti nelle prossime settimane.

* Ora è possibile modificare il nome del programma tramite la finestra di dialogo Modifica programma.

* Il nome del ramo predefinito utilizzato sia durante la creazione del progetto sia nel comando push predefinito tramite Gestione flussi di lavoro Git è stato modificato in `main`.

* L’esperienza di modifica del programma nell’interfaccia utente è stata aggiornata.

* La regola di qualità `ImmutableMutableMixCheck` è stata aggiornata per classificare i nodi `/oak:index` come non modificabili.

* Le regole di qualità `CQBP-84` e `CQBP-84--dependencies` sono state consolidate in un’unica regola. Come parte di tale consolidamento, la scansione delle dipendenze identifica più accuratamente i problemi nelle dipendenze di terze parti distribuite nel runtime di AEM.

* Per evitare confusione, nella pagina Dettagli dell’ambiente sono state consolidate le righe del segmento Pubblica AEM e Pubblica Dispatcher.

  ![Ambienti Dispatcher](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* È stata aggiunta una nuova regola di qualità del codice per convalidare la struttura degli indici `damAssetLucene`. Per ulteriori informazioni, vedi [Indici Oak DAM Asset Lucene personalizzati](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check).

* Ora nella pagina Dettagli dell’ambiente vengono visualizzati più nomi di dominio per i servizi di pubblicazione e anteprima (a seconda dei casi). Vedi [Dettagli dell’ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-junecm}

* Le definizioni dei nodi JCR contenenti una nuova riga dopo il nome dell’elemento radice non venivano analizzate correttamente.

* L’API Elenca archivi non filtrava gli archivi eliminati.

* Veniva visualizzato un messaggio di errore non corretto quando si forniva un valore non valido nel passaggio di pianificazione.

* A volte l’utente visualizzava uno stato verde *attivo* a fianco di un elenco IP consentiti anche quando tale configurazione non era stata distribuita.

* Alcune sequenze di modifica dei programmi impedivano la creazione o la modifica della pipeline di produzione.

* Alcune sequenza di modifica dei programmi causavano la visualizzazione di un messaggio errato nella pagina **Anteprima**, che indicava di rieseguire la configurazione del programma.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#ga-features-assets}

* La funzionalità di automazione dei contenuti consente a [!DNL Experience Manager Assets] di utilizzare le API [!DNL Adobe Creative Cloud] per automatizzare la produzione delle risorse su larga scala. Migliora la velocità dei contenuti riducendo notevolmente il tempo impiegato e le iterazioni necessarie per creare varianti della stessa risorsa. La funzionalità non richiede alcun codice e funziona dall’interno di DAM.
* Rilascio di [!DNL Adobe Asset Link] v3.0 per [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign] e [!DNL Adobe Asset Link] v2.0 per [!DNL Adobe XD]. Esso prevede:

   * Supporto per [!DNL Assets Essentials].
   * Possibilità di connettersi automaticamente a [!DNL Experience Manager] come [!DNL Cloud Service] o [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nuove funzioni disponibili nel canale prerelease [!DNL Assets] {#beta-features-assets}

* Le impostazioni di visualizzazione sono migliorate e consentono agli utenti di scegliere una vista e un parametro di ordinamento predefiniti.
* La funzionalità di download tramite condivisione di collegamenti utilizza download asincroni, più veloci.
* Gli utenti possono cercare e filtrare le cartelle in base ai predicati delle proprietà.
* [!DNL Experience Manager Assets] incorpora il Visualizzatore PDF con tecnologia [!DNL Adobe Document Cloud] per visualizzare in anteprima i documenti supportati. Questa funzione consente agli utenti di visualizzare in anteprima PDF e altri file di più pagine senza alcuna elaborazione complessa. Ciò migliora la parità delle funzionalità con [!DNL Experience Manager] 6.5.

### Bug corretti in [!DNL Assets] {#bugs-fixed-assets}

* Quando si aggiunge un proprietario a una sottocartella, [!DNL Assets] aggiunge anche lo stesso utente come proprietario della cartella principale. (CQ-4323737)
* Quando si aggiungono risorse alle raccolte, se un utente applica un filtro alla ricerca Raccolte, non può visualizzare le raccolte nella vista a elenco. (CQ-4323181)
* Durante la ricerca di file e cartelle, se l&#39;utente applica un filtro e seleziona [!UICONTROL File e cartelle], verranno visualizzati solo i file ma non la cartella. (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#ga-features-sites}

* Pubblica nel livello Anteprima ora viene visualizzato come stato della pagina nell’interfaccia di amministrazione di Sites
* Pubblica nel livello Anteprima ora presenta l’URL di anteprima alla fine dell’azione e mantiene l’URL nelle proprietà della pagina come riferimento successivo

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* È stata aggiunta la possibilità di filtrare colonne personalizzate nella casella in entrata AEM.
* È stata aggiunta la possibilità di utilizzare l’editor di temi e il livello di stile dell’editor di moduli adattivi per assegnare uno stile al componente Captcha.
* Sono state migliorate la velocità e la precisione per il rilevamento automatico delle sezioni logiche nei moduli PDF sorgente e la conversione di tali sezioni nei corrispondenti pannelli dei moduli adattivi.
* È stata aggiunta l’azione Sposta per spostare un file PDF o XDP da una cartella a un’altra.

### Funzione beta di [!DNL Forms]  {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: API di comunicazione consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form (AcroForm).

* **Esternalizzazione dei dati delle variabili**: puoi salvare i dati delle variabili del flusso di lavoro AEM su un sistema di archiviazione esterno gestito dalla tua organizzazione.

Per registrarti al programma beta, puoi inviare un’e-mail all’indirizzo [!DNL formscsbeta@adobe.com].

### Bug corretti in [!DNL Forms] {#forms-bugs-fixed}

* Quando un campo viene convalidato prima dell’invio dei dati al servizio back-end tramite il Modello dati modulo (FDM), le convalide hanno esito positivo ma il relativo servizio non riesce a richiamare la post-convalida.
* Quando invii un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file da 0 byte. Si tratta di un problema noto in Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

Questa sezione illustra le note sulla versione di AEM Screens as a Cloud Service.

### Data di pubblicazione {#release-date-june-screens}

La data di rilascio per AEM Screens as a Cloud Service è il 24 giugno 2021.

### Novità {#what-is-new-screens-june}

>[!NOTE]
>Consulta la [Guida di AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html) per informazioni fondamentali necessarie per installare, configurare ed eseguire correttamente Screens as a Cloud Service e collegarti alla documentazione tecnica sui concetti dettagliati.

* La gestione della registrazione dei dispositivi in blocco rende più veloce ed efficiente il provisioning di enormi quantità di dispositivi di riproduzione.

* Sono state migliorate le opzioni di ricerca e filtro per ciascuna delle viste di inventario Dispositivo, Visualizzazione e Canale.

* Lo snapshot dell’integrità del dispositivo consente di risparmiare tempo, fornendo una panoramica immediata dello stato critico.

* La pagina Dettagli oggetto offre un riepilogo delle informazioni più rilevanti per ciascun oggetto del progetto.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuovi tipi di dati di riferimento per prodotti e categorie CIF per Frammenti di contenuto (incl. supporto dell’interfaccia utente per il selettore di prodotti/categorie)
* Nuovo componente core Frammento di contenuto di Commerce
* Ricerca e-commerce full-text supportata nel back-end di AEM
* I componenti core di Commerce supportano la raccolta di dati Adobe Commerce AI Recs
* Sono stati migliorati gli URL SEO-friendly per le pagine delle categorie
* Supporto per intestazioni HTTP personalizzate per sito/configurazione

## Strumento di trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.5.4 è il 28 giugno 2021.

### Novità {#what-is-new-ctt-latest}

* È stato aggiunto il supporto per un passaggio facoltativo [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) da utilizzare con CTT. Il passaggio di pre-copia può essere utilizzato per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti quando l’istanza AEM di origine è configurata per utilizzare un archivio dati di Amazon S3 o Azure Blob Storage.

* Il guardarrail aggiunto al CTT per impedire agli utenti di interrompere un’acquisizione e potenzialmente danneggiare i dati una volta raggiunto il punto critico durante la fase di acquisizione.

* I registri di estrazione sono stati resi più descrittivi per facilitare la risoluzione dei problemi.

* Sono stati aggiunti messaggi di stato di acquisizione più descrittivi nell’interfaccia utente di.

### Correzioni di bug {#bug-fixes-ctt-latest}

* Durante l&#39;interruzione di un&#39;acquisizione nell&#39;istanza di authoring, l&#39;interfaccia utente ha sovrascritto un&#39;acquisizione precedentemente completata nell&#39;istanza di pubblicazione a `STOPPED` da `FINISHED`. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.16 è il 30 giugno 2021.

### Novità {#what-is-new-bpa-latest}

* Possibilità di rilevare e segnalare i nodi secondari mancanti nelle cartelle in `/content/dam`.

* Possibilità di rilevare e segnalare la versione di Best Practices Analyzer utilizzata.

### Correzioni di bug {#bug-fixes-bpa-latest}

* È stato corretto un errore di registrazione relativo alla struttura dell’archivio non supportata.
