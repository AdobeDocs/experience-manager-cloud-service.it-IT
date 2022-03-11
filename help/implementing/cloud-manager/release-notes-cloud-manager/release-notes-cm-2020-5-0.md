---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.5.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.5.0
feature: Release Information
exl-id: 9f534858-d18f-4224-8b94-9583a05aed95
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.5.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.5.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.5.0 è il 7 maggio 2020.

## Novità {#whats-new-cloud-manager}

* Sono state aggiunte altre sei regole per la qualità del codice, per aiutare i clienti a identificare potenziali problemi durante la pianificazione di una migrazione a Cloud Service.
* È stata aggiunta la nuova metrica *Compatibilità Cloud Service* che consente di ottenere un riepilogo del numero di problemi correlati alla compatibilità.
* Gli ambienti che non è stato possibile creare verranno eliminati automaticamente circa 24 ore dopo la mancata creazione, a meno che non siano già stati eliminati.
* Sono state migliorate le prestazioni della pagina Attività e dell’API dell’elenco di esecuzioni della pipeline.
* Il registro della qualità del codice contiene ora le tracce dello stack complete per le eccezioni.

### Correzioni di bug  {#bug-fixes}

* Durante l’esecuzione della pipeline di produzione nella pagina della panoramica veniva visualizzata una scheda fuorviante.
* La regola per la qualità del codice *DontImplementOrExtendProviderTypesPomCheck* restituiva talvolta un’eccezione Null Pointer.
* Alcuni collegamenti della documentazione nella pagina della panoramica non funzionavano correttamente.
* La finestra di dialogo di creazione dell’ambiente non veniva visualizzata correttamente in Safari.
* Alcune schede nella pagina della panoramica non visualizzavano correttamente i nomi delle entità.
* In alcuni casi, durante la generazione dell’immagine non veniva eseguito il download dei pacchetti dei clienti.
