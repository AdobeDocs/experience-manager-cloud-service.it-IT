---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e76ee82b44e48e88d5c750ebb22db11067cb11b5
workflow-type: tm+mt
source-wordcount: '1053'
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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2021.11.0) è il 16 dicembre 2021.
La seguente versione (2022.1.0) è del 27 gennaio 2022.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di dicembre 2021](https://video.tv.adobe.com/v/339278) video per un riepilogo delle funzioni aggiunte nella versione 2021.11.0 (novembre 2021).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Il ritaglio e il campione avanzato dell’immagine di Dynamic Media è ora basato sui servizi Sensei più recenti, che generano raccolti e campioni migliorati. Inoltre, è stato avviato un miglioramento per generare contenuti di ritaglio diversi, per le stesse proporzioni ma con risoluzioni diverse. Inoltre, eventuali modifiche manuali verranno mantenute al momento della rielaborazione, se nel profilo immagine non vi sono modifiche di larghezza e altezza.

### Nuove funzioni in [!DNL Assets] canale prerelease {#assets-prerelease-features}

* [!DNL Dynamic Media] - È ora possibile utilizzare AEM&#39;interfaccia di Dynamic Media per configurare Impostazioni generali e Impostazioni di pubblicazione anziché passare attraverso l&#39;applicazione desktop Dynamic Media Classic.

* [!DNL Dynamic Media] ora supporta l’acquisizione, l’anteprima, la riproduzione e la pubblicazione per i video MXF. L&#39;annotazione e il video acquistabili per i video MXF non sono ancora supportati.

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile eseguire le [operazioni di aggiornamento, eliminazione, ridenominazione e spostamento](../../assets/use-assets-across-connected-assets-instances.md) nelle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità di [!DNL Forms] {#what-is-new-forms}

* **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: È possibile memorizzare i dati dei flussi di lavoro AEM in-process (AEM dati variabili di flusso di lavoro) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dati e le variabili del flusso di lavoro non vengono memorizzati AEM archivio e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che consentono di:

   * Genera i documenti compilando i file modello (PDF e XDP) con i dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

* **Font personalizzati per documenti Record e PDF creati con API di comunicazione**: È ora possibile utilizzare font approvati dal marchio nei documenti PDF generati utilizzando le API di comunicazione per allinearli ai requisiti organizzativi.

* **Portale Forms**: È possibile utilizzare [Portale Forms](/help/forms/configure-forms-portal.md) per elencare i moduli adattivi pubblicati in una pagina AEM Sites. Aiuta un visitatore del sito a scoprire tutti i moduli disponibili. Inoltre, il visitatore può utilizzare il portale dei moduli per salvare e accedere alla bozza di un modulo adattivo e consultare la versione PDF di un modulo adattivo inviato.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti myAccount estesi basati sui componenti PEGRA estensibili di Commerce

![Componenti myAccount estesi](/help/assets/CIF/extended-myAccount-components.png)

* Gli autori possono creare un Recommendations di prodotti Commerce ad hoc utilizzando altri tipi di consigli

* Supporto per le carte regalo in AEM Storefront

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.11.0.

### Data di pubblicazione {#release-date-cm-nov}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.11.0 è il 4 novembre 2021.
La prossima versione è prevista per il 9 dicembre 2021.

### Novità {#what-is-new-cm-nov}

* Gli utenti possono ora sfruttare le nuove pipeline Front End per distribuire esclusivamente il codice front-end in modo accelerato. Vedi [Pipe front-end di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per saperne di più.

   >[!IMPORTANT]
   >È necessario utilizzare AEM versione `2021.10.5933.20211012T154732Z` o superiore per sfruttare nuove pipeline front-end.

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

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.22 è il 10 dicembre 2021.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare la versione di ACS commons utilizzata.
* Possibilità di rilevare e segnalare il numero di utenti e sottogruppi in un gruppo.
* Possibilità di rilevare e segnalare i valori delle proprietà dei nodi in MongoDB che superano i 16 MB.

### Correzioni di bug {#bug-fixes-bpa}

* Il rilevamento dei componenti di Foundation è stato perfezionato per ridurre i falsi negativi.
* Per i clienti AEM Forms, messaggistica BPA riguardante `EMAIL_PDF_SUBMIT_ACTION` non disponibile su AEM as a Cloud Service è stato corretto.
