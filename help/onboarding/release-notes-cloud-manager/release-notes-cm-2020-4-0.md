---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.4.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.4.0
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 77%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.4.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.4.0 è il 9 aprile 2020.

## Novità {#whats-new-cloud-manager}

* Gli URL dell’editore sono ora disponibili nella pagina Ambiente dell’interfaccia utente di Cloud Manager.
* Sono state apportate modifiche al sistema di navigazione per consentire agli utenti di modificare, cambiare o aggiungere un programma dalla pagina di panoramica di Cloud Manager.
* Sono state apportate modifiche per consentire all’utente di modificare il programma dalla scheda del programma nella pagina di destinazione di Cloud Manager.
* È stato introdotto il nuovo stato di pipeline “**In esecuzione**”, visualizzato per l’ambiente a cui la pipeline è associata.
* Sono stati introdotti miglioramenti nella pagina di esecuzione della pipeline, che ne facilitano la comprensione. Questi includono la visualizzazione del nome della pipeline (solo per pipeline non di produzione) e del tipo, oltre all’indicazione dello stato della pipeline (In corso, Annullato, Non riuscito).
* Sono state aggiunte descrizioni per migliorare l’esperienza utente e spiegare perché il pulsante Aggiungi programma/ambiente è disattivato.
* Gli ambienti con errore possono ora essere eliminati tramite l’interfaccia utente e l’API.
* Il processo utilizzato per generare password git è stato reso più flessibile per affrontare eventuali problemi nel livello di servizio sottostante.

### Correzioni di bug {#bug-fixes-cloud-manager}

* I collegamenti all’ambiente Stage nella pagina dei dettagli di esecuzione della pipeline non passavano alla posizione corretta in modo regolare.
* Singoli passaggi del processo di creazione dell’ambiente venivano interrotti per timeout prima del necessario, causando errori del processo.
* La configurazione Maven utilizzata nel contenitore di build è stata aggiornata per evitare deadlock durante il download dei metadati dell’artefatto.
* In alcuni casi, il passaggio di generazione dell’immagine non eseguiva il download dei pacchetti dei clienti.
* Alcune condizioni poco frequenti impedivano l’eliminazione degli ambienti.
* Le notifiche di Experience Cloud non venivano ricevute in modo costante.

