---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a0bf314ff8f994dd77c2c124db1ab604dcae74b6
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Vedi [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2021.10.0) è il 4 novembre 2021.
La versione seguente (2021.11.0) è del 2 dicembre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di ottobre 2021](https://video.tv.adobe.com/v/338253) video per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in [!DNL Sites] {#sites-features}

* I modelli di frammenti di contenuto vengono ora impostati automaticamente in modalità di sola lettura dopo la pubblicazione, per evitare l’interruzione involontaria delle query API live dopo la ripubblicazione di un modello modificato. Agli utenti viene visualizzato un avviso quando si tenta di modificare un modello pubblicato. Una modifica è possibile dopo aver accettato l’avviso.

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] ora supporta la generazione automatica di trascrizioni di testo dalle risorse audio e video supportate, utilizzando un connettore integrato per [!DNL Azure Media Services]. I file supportati vengono automaticamente trascritti e il testo viene memorizzato in formato WebVTT. Le didascalie WebVTT vengono utilizzate per operazioni di ricerca, sottotitoli o traduzione più efficaci. Inoltre, la funzione migliora l’accessibilità, la scoperta e la localizzazione delle risorse.

### Nuova funzione nel [!DNL Assets] canale prerelease {#assets-prerelease-features}

* [!DNL Dynamic Media] Image Smart Crop and Swatch è ora basato sui servizi Sensei più recenti, che genera colture e campioni migliorati. Inoltre, è stato avviato un miglioramento per generare contenuti di ritaglio diversi, per le stesse proporzioni ma con risoluzioni diverse. Inoltre, eventuali modifiche manuali verranno mantenute al momento della rielaborazione, se nel profilo immagine non vi sono modifiche di larghezza e altezza.

* I tag avanzati vengono applicati automaticamente alle risorse utilizzando i microservizi per le risorse, anziché i servizi di contenuti avanzati. Il modello sottostante viene aggiornato per migliorare i risultati dei tag e ridurre i pregiudizi. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità di [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento sia di accesso che di non accesso (anonimo) tramite Adobe Analytics per Adaptive Forms per raccogliere informazioni sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms-oct-2021}

* **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: È possibile memorizzare i dati dei flussi di lavoro AEM in-process (AEM dati variabili di flusso di lavoro) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dati e le variabili del flusso di lavoro non vengono memorizzati AEM archivio e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Funzioni beta di [!DNL Forms] {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che consentono di:

   * Genera i documenti compilando i file modello (PDF e XDP) con i dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Il componente aggiuntivo CIF supporta la versione più recente di Commerce v2.4.3 con nuove API e schemi GraphQL

* Gli autori possono aggiungere collegamenti alle pagine di prodotti e catalogo nei campi di testo mediante l’editor Rich Text. È stata aggiunta un’icona CIF alla barra degli strumenti dell’editor Rich Text che consente di aprire i selettori per cercare e selezionare rapidamente il prodotto o la categoria senza uscire dal contesto.

* Il carrello e il pagamento a comparsa esistenti sono stati sostituiti da pagine dedicate AEM carrello e per il pagamento. I componenti di queste pagine vengono creati utilizzando i componenti di Magento Extensible Peregrine

* I commercianti possono nascondere alcune categorie di catalogo dei prodotti nella navigazione utilizzando il backend Commerce . Il componente core di navigazione CIF rispetta la configurazione back-end di e-commerce &quot;include nel menu&quot; per mostrare/nascondere categorie nella navigazione

* AEM Storefront Venia restituisce un errore HTTP 404 se la pagina di categoria o prodotto non è trovata

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.10.0.

### Data di pubblicazione {#release-date-cm-nov}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.11.0 è il 4 novembre 2021.
La prossima versione è prevista per il 9 dicembre 2021.

### Novità {#what-is-new-cm-nov}

* Gli utenti possono ora sfruttare le nuove pipeline Front End per distribuire esclusivamente il codice front-end in modo accelerato. Vedi [Pipe front-end di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per saperne di più.

   >[!IMPORTANT]
   >È necessario utilizzare AEM versione `2021.10.5933.20211012T154732Z` per sfruttare le nuove pipeline front-end.

* La durata della pipeline di qualità del codice viene notevolmente ridotta, eseguendo l’analisi del codice in modo più efficiente senza la necessità di creare un’immagine intera AEM. Questa modifica verrà implementata progressivamente nelle settimane successive al rilascio.

* L’ID del commit Git verrà ora visualizzato nei dettagli di esecuzione della pipeline, facilitando il tracciamento del codice generato.

* La creazione di programmi è ora disponibile tramite API pubblicamente esposte.

* La creazione di ambiente è ora disponibile tramite API pubblicamente esposte.

* La `x-request-id` l&#39;intestazione di risposta è ora visibile in API Playground on [www.adobe.io](https://www.adobe.io/). Questa intestazione è utile quando si inviano problemi di assistenza clienti per la risoluzione dei problemi.

* In qualità di utente, vedo la scheda Pipeline con tubazioni zero che mi forniscono la guida appropriata.

* È ora disponibile una nuova pagina Attività in cui è possibile visualizzare le attività come la pipeline e le esecuzioni di codice insieme ai relativi dettagli associati. Nel tempo, le attività elencate in questa pagina si espanderanno nell’ambito insieme ai dettagli forniti.

* È ora disponibile una nuova pagina Pipelines con un puntatore di stato al passaggio del mouse per una facile visualizzazione del riepilogo dei dettagli. Le esecuzioni della pipeline possono essere visualizzate insieme ai relativi dettagli associati.

* L’API Edit Pipeline ora supporta la modifica dell’ambiente utilizzato nelle fasi di distribuzione.

* È stata introdotta un&#39;ottimizzazione nel processo di scansione OakPal per i pacchetti di grandi dimensioni.

* Il file CSV del problema qualità conterrà ora la marca temporale per ogni problema di qualità.

### Correzioni di bug {#bug-fixes-nov}

* Alcune configurazioni di build non ortodosse hanno comportato la memorizzazione di file non necessari nella cache degli artefatti Maven della pipeline, causando un I/O di rete estranea all’avvio e all’arresto del contenitore di build.

* L’API di Pipeline PATCH non riesce se la fase di distribuzione non esiste.

* La `ClientlibProxyResourceCheck` la regola di qualità generava falsi problemi positivi in presenza di librerie client con percorsi di base comuni.

* Il messaggio di errore quando è stato raggiunto il numero massimo di archivi non specifica il motivo dell&#39;errore.

* In rari casi, le pipeline non riuscivano a causa di una gestione inappropriata dei tentativi di alcuni codici di risposta.


## Data di pubblicazione {#release-date-cm-oct}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.10.0 è il 14 ottobre 2021.

### Novità {#what-is-new-cm-oct}

* In preparazione di alcune modifiche imminenti, nell’interfaccia utente verrà fatto riferimento alle pipeline di distribuzione esistenti ed etichettarle come **Stack completo** gasdotti.

* La scheda della pipeline è stata aggiornata per visualizzare una singola faccia integrata che mostra sia le pipeline di produzione che quelle non di produzione e l’utente può selezionare Esegui/Pausa/Riprendi direttamente dal menu delle azioni associato a ciascuna pipeline.

* Un utente con il ruolo di Deployment Manager può ora eliminare la pipeline di produzione in modo self-service tramite l’interfaccia utente.

* Le esperienze di aggiunta e modifica delle pipeline sono state aggiornate per poter utilizzare modelli moderni e familiari.

* Gli utenti di Cloud Manager ora possono inviare un feedback direttamente dall’interfaccia utente tramite l’ **Feedback** in alto a destra della pagina di destinazione.

* I grafici SLA annuali possono ora essere scaricati dall’interfaccia utente di Cloud Manager.

* Le esecuzioni della pipeline di qualità del codice e non di produzione ora utilizzeranno un processo di duplicazione poco profondo più efficiente durante il passaggio di creazione, consentendo ai clienti con archivi Git di dimensioni particolarmente grandi di ottenere tempi di creazione più rapidi.

* La procedura guidata Aggiungi Elenco consentiti IP informa l’utente se è stato raggiunto il numero massimo consentito di Elenchi consentiti IP.

* La documentazione API di Cloud Manager ora include un parco giochi interattivo che consente agli utenti connessi di sperimentare l’API dal proprio browser. Vedi [Playground API di Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) per ulteriori dettagli.

* La descrizione comandi nella scheda Programma sarà più descrittiva se un’opzione di selezione in &quot;Passa a&quot; è disabilitata. Ora viene visualizzato &quot;Un ambiente di produzione non esiste&quot;.

### Correzioni di bug {#bug-fixes-cm-oct}

* In rare situazioni, quando uno staff Adobe ripristina l&#39;ambiente del cliente, il ripristino è stato considerato completo prima che l&#39;ambiente fosse completamente operativo.

* Alcune richieste interne effettuate durante la creazione dell’ambiente non sono state ritentate.

* Se si verifica un errore di distribuzione in seguito alla verifica del nome di dominio, il messaggio di errore è stato corretto per richiedere al cliente di contattare il proprio rappresentante Adobe.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Capacità di rilevare e segnalare la dimensione totale dell&#39;indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca il rendering originale.
