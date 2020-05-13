---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.5.0'
description: Note sulla versione 2020.5.0 di Experience Manager
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# Note sulla versione di AEM as a Cloud Service 2020.5.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.5.0.

## Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.5.0.

### Novità {#what-is-new}

* Sono state aggiunte sei ulteriori regole sulla qualità del codice per aiutare i clienti a identificare potenziali problemi durante la pianificazione di una migrazione a Cloud Service.
* È stata aggiunta una nuova metrica Compatibilità *servizio* cloud per riepilogare il numero di problemi relativi alla compatibilità.
* Gli ambienti che non sono stati creati verranno eliminati automaticamente circa 24 ore dopo la creazione, a meno che non siano già stati eliminati.
* Sono state migliorate le prestazioni della pagina Attività e dell&#39;API Elenco esecuzioni pipeline.
* Il registro della qualità del codice ora contiene le tracce complete dello stack per le eccezioni.

### Correzioni di bug {#bug-fixes}

* Una scheda fuorviante è stata visualizzata nella pagina della panoramica durante l&#39;esecuzione della pipeline di produzione.
* La regola di qualità del codice *DontImplementOrExtendProviderTypesPomCheck* potrebbe a volte generare un&#39;eccezione di puntatore Null.
* Alcuni collegamenti della documentazione dalla pagina della panoramica non funzionavano correttamente.
* Il rendering della finestra di dialogo Crea ambiente non è stato eseguito correttamente in Safari.
* Alcune schede nella pagina della panoramica non visualizzavano correttamente i nomi delle entità.
* In alcuni casi, il download dei pacchetti dei clienti non riusciva a causa dell&#39;Immagine build.

