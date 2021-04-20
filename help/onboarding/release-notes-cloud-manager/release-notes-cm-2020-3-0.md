---
title: Note sulla versione per Cloud Manager in AEM as a Cloud Service, versione 2020.3.0
description: Note sulla versione per Cloud Manager in AEM as a Cloud Service, versione 2020.3.0
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 73%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.3.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.3.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.3.0 è il 5 marzo 2020.

### Novità {#what-is-new}

* Il registro della fase di compilazione è ora disponibile durante l’esecuzione della compilazione.
* Alcuni dei messaggi nella pagina dei dettagli di esecuzione della pipeline sono stati modificati per maggiore chiarezza.

### Correzioni di bug {#bug-fixes}

* Non era possibile scaricare tramite l’interfaccia utente i file di registro per i passaggi di test funzionali personalizzati e del prodotto.
* In caso di mancata creazione dell’archivio git per un programma Cloud Service, a volte gli utenti con ruolo di gestione implementazione non potevano effettuare il ripristino in seguito a questo errore.
* Alcune attività degli utenti durante la creazione di un programma sandbox potevano impedire la creazione del programma prima della creazione della pipeline non di produzione.
* A volte, l’istanza temporanea SonarQube utilizzata nel passaggio di compilazione non veniva avviata entro l’intervallo di timeout configurato.
* Nella creazione simultanea di ambienti di sviluppo nello stesso programma Cloud Service poteva verificarsi una condizione che determinava la riuscita della creazione per un solo ambiente.
* Le notifiche Experience Cloud per i programmi Cloud Service non venivano ricevute in modo coerente.
* In progetti specifici, gli *oggetti ResourceResolver che dovrebbero venire sempre chiusi* generavano un’eccezione Null Pointer che tuttavia non aveva alcun impatto sull’esecuzione della pipeline.