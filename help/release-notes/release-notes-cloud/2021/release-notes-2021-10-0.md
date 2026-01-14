---
title: Note sulla versione 2021.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: ab584923-5f06-4b54-941b-e00bc1158b81
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 70%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.10.0) è il venerdì 4 novembre 2021.
La seguente versione (2021.11.0) è del venerdì 2 dicembre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al video [Panoramica sulla versione di ottobre 2021](https://video.tv.adobe.com/v/338253) per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzionalità in [!DNL Sites] {#sites-features}

* I modelli per frammenti di contenuto ora vengono impostati automaticamente in stato di sola lettura una volta pubblicati, per evitare di interrompere accidentalmente le query API live dopo la ripubblicazione di un modello modificato. Gli utenti ricevono un avviso quando tentano di modificare un modello pubblicato. La modifica è possibile dopo aver accettato l’avviso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [!DNL Experience Manager] ora supporta la generazione automatica di trascrizioni di testo dalle risorse audio e video supportate, utilizzando un connettore incorporato per [!DNL Azure Media Services]. I [tipi di file supportati](/help/assets/file-format-support.md#audio-video-transcription-formats) vengono trascritti automaticamente e il testo viene archiviato in formato WebVTT. I sottotitoli WebVTT vengono utilizzati per ricerche, sottotitoli o traduzioni più efficaci. Inoltre, la funzione migliora l’accessibilità, la reperibilità e la localizzazione delle risorse.

### Nuova funzionalità nel canale prerelease [!DNL Assets] {#assets-prerelease-features}

* Ritaglio e campione avanzato immagine [!DNL Dynamic Media] ora si basa sui servizi di intelligenza artificiale più recenti, che generano ritagli e campioni migliorati. Inoltre, è stato avviato un miglioramento per generare contenuti di ritaglio diversi, per le stesse proporzioni ma con risoluzioni diverse. Inoltre, eventuali modifiche manuali vengono mantenute durante la rielaborazione, se nel profilo immagine non vi sono modifiche di larghezza e altezza.

* I tag avanzati vengono applicati automaticamente alle risorse utilizzando i microservizi per le risorse, anziché Smart Content Services. Il modello sottostante viene aggiornato per migliorare i risultati dei tag e ridurre i pregiudizi. <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**: è ora possibile acquisire e tenere traccia del comportamento sia degli utenti connessi che di quelli non connessi (anonimi) tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sugli utenti. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza utente.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: è possibile memorizzare i dati dei flussi di lavoro AEM in elaborazione (dati variabili di flusso di lavoro AEM) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dei dati e le variabili del flusso di lavoro non vengono memorizzati nell’archivio AEM e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Funzioni beta di [!DNL Forms]  {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=it) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   * Generare i documenti compilando i file modello (PDF e XDP) con i dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

Per registrarti al programma beta, puoi inviare un’e-mail all’indirizzo [!DNL formscsbeta@adobe.com].

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Il componente aggiuntivo CIF supporta la versione più recente di Commerce v2.4.3 con nuovi API e schemi di GraphQL

* Gli autori possono aggiungere collegamenti alle pagine di prodotti e cataloghi nei campi di testo utilizzando l’editor Rich Text. Alla barra degli strumenti dell’editor Rich Text è stata aggiunta un’icona CIF che apre i selettori per cercare e selezionare rapidamente il prodotto o la categoria senza uscire dal contesto.

* Il carrello e il pagamento pop-up esistenti sono stati sostituiti con il carrello e le pagine di pagamento AEM dedicate. I componenti di queste pagine vengono generati utilizzando i componenti PEGRA estensibili di Adobe Commerce

* Gli esercenti possono nascondere determinate categorie del catalogo dei prodotti nella navigazione utilizzando il backend di Commerce. Il componente core Navigazione CIF rispetta la configurazione back-end per l’e-commerce &quot;includi nel menu&quot; per mostrare/nascondere le categorie nella navigazione

* AEM Storefront Venia restituisce l’errore HTTP 404 se la pagina della categoria o del prodotto non viene trovata

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione 2021.10.0 di Cloud Manager AEM as a Cloud Service.

### Data di pubblicazione {#release-date-cm-nov}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.11.0 è il 4 novembre 2021.
La prossima versione è prevista per il 9 dicembre 2021.

### Novità {#what-is-new-cm-nov}

* Gli utenti possono ora sfruttare le nuove pipeline Front End per distribuire esclusivamente il codice front-end in modo accelerato. Consulta [Pipeline front-end di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per ulteriori informazioni.

  >[!IMPORTANT]
  >Per utilizzare le nuove pipeline front-end è necessaria la versione `2021.10.5933.20211012T154732Z` di AEM.

* La durata della pipeline di qualità del codice viene notevolmente ridotta, eseguendo l’analisi del codice in modo più efficiente senza la necessità di creare un’immagine intera AEM. Questa modifica verrà implementata progressivamente nelle settimane successive al rilascio.

* L’ID del commit Git verrà ora visualizzato nei dettagli di esecuzione della pipeline, facilitando il tracciamento del codice generato.

* La creazione di programmi è ora disponibile tramite API pubblicamente esposte.

* La creazione di ambiente è ora disponibile tramite API pubblicamente esposte.

* L’`x-request-id` intestazione di risposta è ora visibile in API Playground su [www.adobe.io](https://www.adobe.io/). Questa intestazione è utile quando si inviano problemi di assistenza clienti per la risoluzione dei problemi.

* In qualità di utente, vedo la scheda Pipeline senza pipeline che mi forniscano la guida appropriata.

* È ora disponibile una nuova pagina Attività in cui è possibile visualizzare le attività come la pipeline e le esecuzioni di codice insieme ai relativi dettagli associati. Nel tempo, le attività elencate in questa pagina si espanderanno nell’ambito insieme ai dettagli forniti.

* È ora disponibile una nuova pagina di pipeline con un puntatore di stato al passaggio del mouse per una facile visualizzazione del riepilogo dei dettagli. Le esecuzioni della pipeline possono essere visualizzate insieme ai relativi dettagli associati.

* L’API di modifica delle pipeline ora supporta la modifica dell’ambiente utilizzato nelle fasi di distribuzione.

* È stata introdotta un’ottimizzazione nel processo di scansione OakPal per i pacchetti di grandi dimensioni.

* Il file CSV del problema qualità conterrà ora la timestamp per ogni problema di qualità.

### Correzioni di bug {#bug-fixes-nov}

* Alcune configurazioni della versione non ortodosse hanno comportato la memorizzazione di file non necessari nella cache degli artefatti Maven della pipeline, causando un I/O di rete estranea all’avvio e all’interruzione del contenitore della versione.

* L’API di Pipeline PATCH non riesce se la fase di distribuzione non esiste.

* La `ClientlibProxyResourceCheck` la regola di qualità generava falsi problemi positivi in presenza di librerie client con percorsi di base comuni.

* Il messaggio di errore quando è stato raggiunto il numero massimo di archivi non specifica il motivo dell’errore.

* In rari casi, le pipeline non riuscivano a causa di una gestione inappropriata dei tentativi di alcuni codici di risposta.


## Data di pubblicazione {#release-date-cm-oct}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.10.0 è il 14 ottobre 2021.

### Novità {#what-is-new-cm-oct}

* Per prepararci ad alcune modifiche imminenti, ora le pipeline di distribuzione esistenti verranno indicate ed etichettate nell’interfaccia utente come pipeline **full stack**.

* Ora la scheda Pipeline è stata aggiornata per visualizzare una singola pagina integrata che mostra entrambe le pipeline di produzione e non di produzione. L’utente può selezionare Esegui/Pausa/Riprendi direttamente dal menu Azioni associato a ogni pipeline.

* Ora l’utente con il ruolo Responsabile dell’implementazione può eliminare la pipeline di produzione tramite l’interfaccia utente in modo autonomo.

* Le esperienze di aggiunta e modifica delle pipeline sono state aggiornate per poter utilizzare finestre modali moderne e intuitive.

* Ora gli utenti di Cloud Manager possono inviare feedback direttamente dall’interfaccia utente, tramite il pulsante **Feedback** posizionato nella parte in alto a destra della pagina di destinazione.

* Ora è possibile scaricare i grafici SLA annuali dall’interfaccia utente di Cloud Manager.

* Ora le esecuzioni delle pipeline di qualità del codice e non di produzione utilizzano un processo di clonazione superficiale durante la fase di build, garantendo tempi di generazione più brevi ai clienti con archivi Git di dimensioni particolarmente grandi.

* Ora la procedura guidata Aggiungi elenco IP consentiti informa l’utente se è stato raggiunto il numero massimo di elenchi IP consentiti.

* Ora la documentazione API di Cloud Manager include un ambiente playground interattivo che consente agli utenti connessi di sperimentare l’API dal browser in uso. Per ulteriori informazioni, consulta [Ambiente playground dell’API di Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/).

* Il suggerimento della scheda Programma presenta una descrizione più dettagliata se è disattivata l’opzione di selezione sotto “Accedi a”. Ora viene visualizzato “Non esiste un ambiente di produzione”.

### Correzioni di bug {#bug-fixes-cm-oct}

* In rare situazioni, quando il personale Adobe ripristinava l’ambiente del cliente, il ripristino veniva considerato completo prima che l’ambiente fosse completamente operativo.

* Per alcune richieste interne effettuate durante la creazione dell’ambiente non veniva effettuato un secondo tentativo.

* In caso di errori della distribuzione rilevati successivamente alla verifica del nome di dominio, il messaggio di errore è stato corretto per suggerire all’utente di contattare il rappresentante Adobe.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Possibilità di rilevare e segnalare le dimensioni totali dell’indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca la rappresentazione originale.
