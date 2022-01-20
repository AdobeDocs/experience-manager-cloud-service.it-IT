---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.11.0
description: Queste sono le note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.11.0
feature: Release Information
source-git-commit: e402578fc95fd97f808fde01a860d4c583af4c9b
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.11.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.11.0 è il 4 novembre 2021.
La prossima versione è prevista per il 16 dicembre 2021.

## Novità {#what-is-new}

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

## Correzioni di bug {#bug-fixes}

* Alcune configurazioni di build non ortodosse hanno comportato la memorizzazione di file non necessari nella cache degli artefatti Maven della pipeline, causando un I/O di rete estranea all’avvio e all’arresto del contenitore di build.

* L’API di Pipeline PATCH non riesce se la fase di distribuzione non esiste.

* La `ClientlibProxyResourceCheck` la regola di qualità generava falsi problemi positivi in presenza di librerie client con percorsi di base comuni.

* Il messaggio di errore quando è stato raggiunto il numero massimo di archivi non specifica il motivo dell&#39;errore.

* In rari casi, le pipeline non riuscivano a causa di una gestione inappropriata dei tentativi di alcuni codici di risposta.
