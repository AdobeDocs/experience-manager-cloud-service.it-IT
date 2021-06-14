---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: f447303d3618eb2e9ea38873c88ed04280670218
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] come Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 è il 27 maggio 2021.
La versione seguente (2021.6.0) sarà del 24 giugno 2021.

## Video sulla versione {#release-video}

Per un riepilogo delle funzioni aggiunte, guarda il video [Panoramica sulla versione di maggio 2021](https://video.tv.adobe.com/v/333602) .

## AEM come base di Cloud Service {#foundation}

### Novità di AEM as a Cloud Service Foundation {#what-is-new-foundation}

* [Canale](/help/release-notes/prerelease.md) pre-rilascio: Anteprima delle prossime funzionalità per un mese intero prima che diventino live in produzione!

* [Obsolescenza API](/help/release-notes/deprecated-apis.md): è disponibile un elenco delle API obsolete più recenti per AEM as a Cloud Service .

* [AEM come Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html): Aggiorna i progetti Maven all’ultima versione, che include un controllo Java API obsoleto e altri miglioramenti.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* A breve potrai verificare il contenuto di un nuovo [livello di anteprima](/help/sites-cloud/authoring/fundamentals/previewing-content.md) per simulare l’aspetto e l’aspetto dell’esperienza finale come faresti sul livello di pubblicazione. Questa opzione è abilitata dalla procedura guidata Pubblicazione gestita di AEM Sites che consente di scegliere una destinazione di pubblicazione tra Pubblica o Anteprima. È quindi possibile accedere alle esperienze in anteprima tramite un URL dedicato. Dopo la convalida in Anteprima, il contenuto può essere pubblicato come di consueto da Author a Publish. L’abilitazione del servizio di anteprima in ambienti AEM come Cloud Service verrà gradualmente implementato nelle prossime settimane.

## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

### Nuove funzioni disponibili nel canale pre-rilascio {#what-is-new-assets-prerelease}

* Gli schemi di metadati possono essere applicati direttamente alle proprietà della cartella.

   ![Aggiungi schema metadati dalle proprietà della cartella](/help/assets/assets/metadata-schema-folder-properties.png)

* Lo strumento Asset Bulk Ingestor consente di aggiungere metadati durante un’acquisizione in blocco.

* I miglioramenti dell’esperienza utente visualizzano il numero di risorse presenti in una cartella. Per più di 1000 risorse in una cartella, [!DNL Assets] visualizza più di 1000 risorse.

   ![Nell’interfaccia viene visualizzato il numero di risorse presenti in una cartella](/help/assets/assets/browse-folder-number-of-assets.png)

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Il caricamento di file di grandi dimensioni causa l&#39;arresto anomalo del sistema [!DNL Experience Manager desktop app]. (CQ-4320942)
* Le opzioni della barra degli strumenti sono diverse quando la stessa raccolta è selezionata all’interno di una cartella e quando è selezionata da un risultato di ricerca. (CQ-4321406)

#### Novità in [!DNL Dynamic Media] {#what-is-new-dm}

* Le funzioni DPR (Smart Imaging Device Pixel Ratio) e di ottimizzazione della larghezza di banda della rete consentono di fornire immagini di alta qualità in modo efficiente su dispositivi con display ad alta risoluzione e larghezza di banda limitata della rete. Consulta [domande frequenti sull&#39;imaging intelligente](/help/assets/dynamic-media/imaging-faq.md).

   >[!NOTE]
   >
   >La timeline della versione per i miglioramenti di Smart imaging riportati sopra è:
   >
   >* Nord America 24 maggio 2021 in NA,
      >
      >
   * Europa, Medio Oriente e Africa 25 giugno 2021,
      >
      >
   * Asia-Pacifico, 19 luglio 2021.


* È stato introdotto il supporto per AVIF in formato immagine di nuova generazione in [!DNL Dynamic Media] consegna (modificatore URL fmt).

   >[!NOTE]
   >
   >La timeline della versione per il supporto AVIF è la seguente:
   >
   >* Nord America 10 maggio 2021,
      >
      >
   * Europa, Medio Oriente e Africa 24 maggio 2021,
      >
      >
   * Asia-Pacifico, 24 giugno 2021.


## [!DNL Adobe Experience Manager Forms] come  [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Aiuto contestuale**: È stata aggiunta l’aiuto contestuale per l’editor di moduli adattivi, l’editor di modelli e l’editor di temi, per aiutare gli autori a comprendere meglio le varie funzioni degli editor.
* **Messaggi di errore nel browser** Proprietà: Sono stati aggiunti messaggi di errore per ciascuna proprietà nel browser Proprietà adattive Forms. Questi messaggi consentono di comprendere i valori consentiti per un campo.

### Prossima funzionalità beta di [!DNL Forms] {#what-is-new-forms-prerelease}

Output as a Cloud Service: Il servizio di output consente di combinare i modelli XDP e i dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità batch sincrona e asincrona. Il servizio di output consente di creare applicazioni che consentono di:

* Generare documenti modulo finali compilando i file modello con dati XML.
* Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
* Genera PDF per la stampa da PDF di moduli XFA.

Puoi scrivere su formscsbeta@adobe.com per iscriverti al programma beta.

### Bug corretti in [!DNL Forms] {#forms-bugs-fixed}

* In una fase Assegna attività dei flussi di lavoro AEM Forms, quando sostituisci l&#39;icona predefinita dei pulsanti di azione con un&#39;icona coral, il flusso di lavoro smette di funzionare e registra un&#39;eccezione. Il flusso di lavoro funziona come previsto quando si utilizzano le icone predefinite.
* Nel livello di layout, quando si modifica il numero di colonne, si apre il livello di modifica e si trascina alcuni componenti in un pannello, le caselle blu quadrate iniziano a comparire nell’area contenuto dell’editor di moduli adattivi e l’editor non risponde.
* Il messaggio di errore di un’opzione dell’editor di regole relativa alla fornitura dell’URL di una risorsa adattiva o esterna è troppo lungo e non è di facile utilizzo.

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM as a Cloud Service 2021.6.0 e 2021.5.0.

## Data di rilascio {#release-date-june-cm}

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


### Data di rilascio {#release-date-cm-may}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.

### Novità {#what-is-new-may}

* La regola di qualità PackageOverlaps ora rileva i casi in cui lo stesso pacchetto è stato distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL Git.

* Il registro di distribuzione scaricato da un utente di Cloud Manager sarà più dettagliato e ora includerà dettagli sugli errori e sugli scenari di successo.

* Sono stati risolti gli errori intermittenti durante il push del codice all’Git di Adobe.

* È ora possibile applicare il componente aggiuntivo Commerce ai programmi Sandbox durante il flusso di lavoro Modifica programma .

* L&#39;esperienza del programma Edit è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda Soluzioni nei flussi di lavoro Aggiungi programma e Modifica programma visualizzerà la soluzione, anche se per il programma è disponibile una sola soluzione.

* Il messaggio di errore nel registro dei passaggi della build quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes-cm-may}

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Invece di rimuovere le variabili &quot;eliminate&quot;, le variabili delle pipeline API le contrassegnavano solo con lo stato **ELIMINATO**.

* Alcuni problemi di qualità del tipo di odore del codice hanno avuto un impatto errato sul rating di affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando è stata avviata l’esecuzione di una pipeline tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era garantita come maggiore di una versione creata il giorno precedente.

* Durante la configurazione del programma Sandbox, una volta che il progetto con codice di esempio è stato creato correttamente, Manage Git (Gestisci Git) apparirà come collegamento dalla scheda eroe nella pagina Overview (Panoramica).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.4.6 è il 27 maggio 2021.

### Novità {#what-is-new-ctt-latest}

* È stata aggiunta una nuova istruzione di registrazione al registro degli errori di quickstart, se l’utente non dispone dell’autorizzazione di esecuzione sull’eseguibile Java.

* Quando un utente elimina un set di migrazione dall’interfaccia utente CTT, in cui è stata eseguita un’estrazione, la cartella `tmp` associata a tale set di migrazione verrà eliminata per risparmiare spazio.

### Correzioni di bug {#bug-fixes-ctt-latest}

* Quando si elimina un set di migrazione, occasionalmente nell’interfaccia utente del CTT viene visualizzato un messaggio di errore non utile. Questo problema è stato risolto.

* Durante l’esecuzione di User Mapping, se gli utenti avevano lo stesso indirizzo e-mail sulla destinazione e sull’host ma nomi utente diversi, l’intera acquisizione avrebbe esito negativo. Questo problema è stato risolto. In questo scenario in conflitto, l&#39;utente/gruppo viene ignorato e registrato come conflitto nel file di log.

### Data di rilascio {#release-date-ctt-may}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.4.0 è l’11 maggio 2021.

### Novità {#what-is-new-ctt-may}

* Questa versione dello strumento Content Transfer (Trasferimento contenuti) crea rappresentazioni di testo per le risorse da migrare al Cloud Service. Le rappresentazioni di testo sono necessarie per supportare la ricerca full-text sulle risorse acquisite.
* Il numero massimo di set di migrazione dello strumento Content Transfer (Trasferimento contenuti) che un utente può creare è stato aumentato da 4 a 10.

### Correzioni di bug {#bug-fixes-ctt-may}

* Correzioni di bug multipli relative alla funzione di aggiornamento automatico nell’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti).
* Lo strumento Content Transfer (Trasferimento contenuti) con `wipe=true` causava un indice di contatore errato nel target. Questo problema è stato risolto.

## Componente aggiuntivo Commerce {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per l’impaginazione del contenuto associato nelle proprietà della console del prodotto

### Correzioni di bug {#bug-fixes-commerce}

* Miniature delle risorse non visualizzate nella scheda Risorsa delle proprietà del prodotto

* Breadcrumb ripristina i dati di anteprima nella console del prodotto
