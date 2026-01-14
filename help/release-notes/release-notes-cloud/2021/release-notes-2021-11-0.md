---
title: Note sulla versione 2021.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 94%

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

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.11.0) è il 16 dicembre 2021.
La seguente versione (2022.1.0) è del venerdì 3 febbraio 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video [Panoramica sulla versione di dicembre 2021](https://video.tv.adobe.com/v/339278) per un riepilogo delle funzioni aggiunte alla versione 2021.11.0 (novembre 2021).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Il ritaglio e il campione avanzato dell’immagine di Dynamic Media è ora basato sui servizi AI di Adobe più recenti, che generano ritagli e campioni migliorati. Inoltre, è stato avviato un miglioramento per generare contenuti di ritaglio diversi, per le stesse proporzioni ma con risoluzioni diverse. Inoltre, eventuali modifiche manuali vengono mantenute durante la rielaborazione, se nel profilo immagine non vi sono modifiche di larghezza e altezza.

### Nuove funzioni nel canale pre-release di [!DNL Assets] {#assets-prerelease-features}

* [!DNL Dynamic Media] - È ora possibile utilizzare l’interfaccia Dynamic Media di AEM per configurare le impostazioni generali e le impostazioni di pubblicazione anziché passare attraverso l’applicazione desktop Dynamic Media Classic.

* [!DNL Dynamic Media] ora supporta l’acquisizione, l’anteprima, la riproduzione e la pubblicazione per i video MXF. L&#39;annotazione e il video acquistabile per i video MXF non sono ancora supportati.

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile [aggiornare, eliminare, rinominare e spostare le operazioni](/help/assets/use-assets-across-connected-assets-instances.md) sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: è possibile memorizzare i dati dei flussi di lavoro AEM in elaborazione (dati variabili di flusso di lavoro AEM) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dei dati e le variabili del flusso di lavoro non vengono memorizzati nell’archivio AEM e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=it) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   * Generare i documenti compilando i file modello (PDF e XDP) con i dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

* **Font personalizzati per documenti Record e PDF creati con API di comunicazione**: è ora possibile utilizzare font approvati dal marchio nei documenti PDF generati utilizzando le API di comunicazione per allinearli ai requisiti organizzativi.

* **Portale Forms**: è possibile utilizzare [Portale dei moduli](/help/forms/configure-forms-portal.md) per elencare i moduli adattivi pubblicati in una pagina AEM Sites. Aiuta un visitatore del sito a scoprire tutti i moduli disponibili. Inoltre, il visitatore può utilizzare il portale dei moduli per salvare e accedere alla bozza di un modulo adattivo e consultare la versione PDF di un modulo adattivo inviato.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti myAccount estesi basati sui componenti PEGRA estensibili di Commerce

![Componenti myAccount estesi](/help/assets/CIF/extended-myAccount-components.png)

* Gli autori possono creare consigli di prodotti Commerce ad hoc utilizzando altri tipi di consigli

* Supporto per le carte regalo nel progetto di vetrina digitale di AEM

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.11.0.

### Data di pubblicazione {#release-date-cm-nov}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.11.0 è il 4 novembre 2021.
La prossima versione è prevista per il 9 dicembre 2021.

### Novità {#what-is-new-cm-nov}

* Gli utenti possono ora sfruttare le nuove pipeline Front End per distribuire esclusivamente il codice front-end in modo accelerato. Consulta [Pipeline front-end di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per ulteriori informazioni.

  >[!IMPORTANT]
  >Per utilizzare le nuove pipeline front-end è necessario utilizzare AEM versione `2021.10.5933.20211012T154732Z` o successiva.

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

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.22 è il 1 dicembre 2021.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare la versione di ACS comunemente utilizzata.
* Possibilità di rilevare e segnalare il numero di utenti e sottogruppi in un gruppo.
* Possibilità di rilevare e segnalare i valori delle proprietà dei nodi in MongoDB che superano i 16 MB.

### Correzioni di bug {#bug-fixes-bpa}

* Il rilevamento dei componenti di Foundation è stato perfezionato per ridurre i falsi negativi.
* Per i clienti AEM Forms, la messaggistica BPA riguardante `EMAIL_PDF_SUBMIT_ACTION` non disponibile su AEM as a Cloud Service è stata corretta.
