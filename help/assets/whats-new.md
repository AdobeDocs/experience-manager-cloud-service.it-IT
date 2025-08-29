---
title: Novità di Content Hub
description: Ulteriori informazioni su alcune delle funzionalità di Content Hub recentemente lanciate
role: User
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: 62ac097fca0142265f2e1ef28117619d59045e6c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 49%

---

# Novità di Content Hub {#whats-new-content-hub}

Content Hub è disponibile come parte di Experience Manager Assets as a Cloud Service per rendere i contenuti in linea con il brand accessibili nella propria organizzazione e ai rispettivi partner commerciali. Si concentra sulla distribuzione delle risorse per l’attivazione su larga scala e la creazione di varianti di contenuti fedeli alle linee guida del brand, per una maggiore marketing agility.

Il seguente video illustra le funzionalità principali di Content Hub:

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) e Assets as a Cloud Service includono 250 utenti con limitazioni per Content Hub. [Assets Prime](/help/assets/assets-prime.md) include 50 utenti con limitazioni per Content Hub.

## Data di pubblicazione {#release-date}

La data di rilascio della funzione Content Hub (2025.8.0) è il 28 agosto 2025 (come quella della versione di AEM as a Cloud Service). La prossima versione funzionale (2025.9.0) è pianificata per il venerdì 25 settembre 2025.

## Funzioni della versione di agosto {#august-release-features}

**Ricerca in blocco tramite proprietà filtro**

Content Hub consente ora di individuare più rapidamente le risorse necessarie. Con la nuova funzionalità di ricerca in blocco, puoi immettere più valori per qualsiasi proprietà di filtro, separati da un delimitatore (ad esempio, più ID SKU), e recuperare immediatamente tutte le risorse corrispondenti utilizzando una singola ricerca.

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#bulk-search"}

## Funzioni della versione di luglio {#july-release-features}

**Maggiore flessibilità di branding in Content Hub**

Basandosi sulle funzioni di personalizzazione esistenti, Content Hub consente ora agli amministratori di personalizzare ulteriormente la propria implementazione aggiungendo immagini con loghi personalizzati. È stato inoltre aggiunto il supporto per il formato di file TIFF, sia per le immagini del banner che per quelle del logo, consentendo una maggiore flessibilità di progettazione.

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

**Condivisione più intelligente con collegamenti con titolo**

È ora possibile aggiungere un titolo durante la generazione di un collegamento condiviso, dalla vista dei dettagli della risorsa o dopo aver selezionato una o più risorse. In questo modo i destinatari possono identificare facilmente lo scopo di ogni collegamento, in particolare quando ricevono più risorse condivise.

![collegamento pubblico e privato](/help/assets/assets/shared-link-for-assets.png)

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

**Navigazione filtro migliorata**

Content Hub ora include un’opzione **Mostra tutto** all’interno dei filtri, che consente agli utenti di visualizzare tutti i facet disponibili insieme al numero di risorse, a partire dall’attuale limite di visualizzazione di un massimo di dieci facet. Le funzionalità avanzate di ricerca e ordinamento all’interno di ciascun filtro rendono più facile individuare e gestire le risorse in modo più efficiente.

## Funzioni della versione di giugno {#june-release-features}

### Governance delle raccolte {#collections-governance}

Content Hub ora consente di controllare l’accesso alle raccolte durante la creazione, garantendo che solo gli utenti autorizzati possano visualizzare o gestire le risorse raggruppate. Ciò garantisce maggiore sicurezza, migliore collaborazione, gestione risorse organizzata e governance semplificata.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## Funzioni di maggio {#may-release-features}

Il rilascio di Content Hub di maggio include le seguenti funzionalità:

* [Controllo degli accessi basato su attributi](#attribute-based-access-control)

* [Marchio interfaccia utente](#ui-branding)

* [Condivisione di collegamenti pubblici](#public-link-sharing)

* [Scaricare più risorse come file ZIP](#download-multiple-assets-as-zip)

* [Rappresentazioni Dynamic Media in Content Hub](#dynamic-media-renditions)

### Controllo degli accessi basato su attributi (ABAC) {#attribute-based-access-control}

Content Hub ora consente di applicare restrizioni basate su regole per accedere alle risorse. Le autorizzazioni per le risorse garantiscono la governance e assicurano che solo le risorse pertinenti siano accessibili agli utenti.

Le regole di limitazione delle risorse si basano sui metadati e, se le condizioni definite nella regola corrispondono ai metadati della risorsa, la risorsa viene visualizzata ai gruppi di utenti.

Alcuni dei vantaggi principali del controllo degli accessi basato su attributi includono:

* Eliminazione della dipendenza dalla struttura di cartelle per le autorizzazioni

* Consenso agli amministratori di caricare le risorse e determinare retroattivamente le strutture delle autorizzazioni

* Riduzione del numero di duplicati, migliorando l’integrità della risorsa. I duplicati sono necessari nelle autorizzazioni basate su cartelle quando le stesse risorse sono condivise con gruppi diversi.

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/attribute-based-access-control"}

### Marchio interfaccia utente {#ui-branding}

Content Hub ora consente agli amministratori di personalizzare l’interfaccia utente con elementi specifici del brand, tra cui immagini del banner, titoli dei banner e testo del corpo del messaggio, nonché colori primari e secondari. Questi miglioramenti contribuiscono a garantire la coerenza del brand, semplificare l’onboarding degli utenti e creare fiducia.

![Branding interfaccia utente](/help/assets/assets/content-hub-ui-branding.png)

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

### Condivisione di collegamenti pubblici {#public-link-sharing}

Content Hub ora supporta la generazione di collegamenti condivisibili per consentire agli utenti esterni, senza accesso alle applicazioni, di visualizzare i metadati delle risorse o scaricare le risorse.

![Branding interfaccia utente](/help/assets/assets/public-and-private-link.png)

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

### Scaricare più risorse come file ZIP {#download-multiple-assets-as-zip}

Content Hub ora consente anche di scaricare le risorse selezionate e le relative rappresentazioni in un file ZIP e non come file separati, semplificando la gestione dei file.

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

### Rappresentazioni Dynamic Media in Content Hub {#dynamic-media-renditions}

Accedi a tutte le rappresentazioni predefinite e ai ritagli avanzati di Dynamic Media per il download, direttamente dall’interfaccia utente di Content Hub.

![Rappresentazioni di Dynamic Media](/help/assets/assets/dm-renditions-content-hub.png)

[!BADGE Approfondisci questa funzione]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}
