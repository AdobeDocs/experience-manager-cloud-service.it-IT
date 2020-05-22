---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.5.0'
description: Note sulla versione 2020.5.0 di Experience Manager
translation-type: tm+mt
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 18%

---


# Note sulla versione di AEM as a Cloud Service 2020.5.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.5.0.

## Data di rilascio {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.5.0 is May 07, 2020.

## What&#39;s New in AEM Sites {#aem-sites}

Segui questa sezione per scoprire le novità e gli aggiornamenti di AEM Sites in AEM come servizio cloud Release 2020.5.0.

* Informazioni dettagliate sul processo ora disponibili dopo l’elaborazione degli spostamenti in massa delle pagine e dei rollout come processi asincroni.
* Quando si copia/incolla una struttura di pagina, ora è possibile scegliere se incollare solo la pagina principale o anche le sottopagine della struttura.
* I frammenti esperienza AEM esportati nelle aree di lavoro di Adobe Target ora vengono visualizzati come tipi di offerta univoci e origini offerte in Target.
* MSM: l&#39;utilizzo dell&#39;attivatore di *pubblicazione* ora consente di eliminare con successo gli eventi per i componenti in Live Copy, ovvero l&#39;eliminazione di componenti in una Live Copy che erano stati eliminati nell&#39;origine Live Copy.
* MSM - i componenti Live Copy ora vengono rinominati in *_msm_move* dopo il rollout dello stesso componente dall’origine Live Copy.


## Novità di Cloud Manager {#cloud-manager}

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

