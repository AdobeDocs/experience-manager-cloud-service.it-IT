---
title: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2020.5.0
description: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2020.5.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.5.0 {#release-notes}

In questa pagina sono delineate le Note sulla versione di Marketing Cloud Manager in AEM come Cloud Service 2020.5.0.

## Data di rilascio {#release-date}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.5.0 è il 7 maggio 2020.

## Novità {#whats-new-cloud-manager}

* Sono state aggiunte altre sei regole per la qualità del codice, per aiutare i clienti a identificare potenziali problemi durante la pianificazione di una migrazione a Cloud Service.
* È stata aggiunta la nuova metrica *Compatibilità Cloud Service* che consente di ottenere un riepilogo del numero di problemi correlati alla compatibilità.
* Gli ambienti che non è stato possibile creare verranno eliminati automaticamente circa 24 ore dopo la mancata creazione, a meno che non siano già stati eliminati.
* Sono state migliorate le prestazioni della pagina Attività e dell’API dell’elenco di esecuzioni della pipeline.
* Il registro della qualità del codice contiene ora le tracce dello stack complete per le eccezioni.

### Correzioni di bug {#bug-fixes}

* Durante l’esecuzione della pipeline di produzione nella pagina della panoramica veniva visualizzata una scheda fuorviante.
* La regola per la qualità del codice *DontImplementOrExtendProviderTypesPomCheck* restituiva talvolta un’eccezione Null Pointer.
* Alcuni collegamenti della documentazione nella pagina della panoramica non funzionavano correttamente.
* La finestra di dialogo di creazione dell’ambiente non veniva visualizzata correttamente in Safari.
* Alcune schede nella pagina della panoramica non visualizzavano correttamente i nomi delle entità.
* In alcuni casi, durante la generazione dell’immagine non veniva eseguito il download dei pacchetti dei clienti.
