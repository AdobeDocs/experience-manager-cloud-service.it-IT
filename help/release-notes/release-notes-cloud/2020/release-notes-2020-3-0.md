---
title: Note sulla versione 2020.3.0
description: Note sulla versione 2020.3.0
exl-id: 0393c789-3999-4e51-be83-269d6eabd3f3
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# AEM as a Cloud Service: note sulla versione di 2020.3.0 {#release-notes}

Questa pagina illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.3.0.

## Data di pubblicazione {#release-date}

La data di rilascio per Experience Manager as a Cloud Service 2020.3.0 è il 5 marzo 2020.

## Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.3.0.

### Novità {#what-is-new}

* Il registro della fase di compilazione è ora disponibile durante l’esecuzione della compilazione.
* Alcuni dei messaggi nella pagina dei dettagli di esecuzione della pipeline sono stati modificati per maggiore chiarezza.

### Correzioni di bug  {#bug-fixes}

* Non era possibile scaricare tramite l’interfaccia utente i file di registro per i passaggi di test funzionali personalizzati e del prodotto.
* In caso di mancata creazione dell’archivio git per un programma Cloud Service, a volte gli utenti con ruolo di gestione implementazione non potevano effettuare il ripristino in seguito a questo errore.
* Alcune attività degli utenti durante la creazione di un programma sandbox potevano impedire la creazione del programma prima della creazione della pipeline non di produzione.
* A volte, l’istanza temporanea SonarQube utilizzata nel passaggio di compilazione non veniva avviata entro l’intervallo di timeout configurato.
* Nella creazione simultanea di ambienti di sviluppo nello stesso programma Cloud Service poteva verificarsi una condizione che determinava la riuscita della creazione per un solo ambiente.
* Le notifiche Experience Cloud per i programmi Cloud Service non venivano ricevute in modo coerente.
* In progetti specifici, gli *oggetti ResourceResolver che dovrebbero venire sempre chiusi* generavano un’eccezione Null Pointer che tuttavia non aveva alcun impatto sull’esecuzione della pipeline.
