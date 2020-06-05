---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.5.0'
description: Note sulla versione 2020.5.0 di Experience Manager
translation-type: ht
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: ht
source-wordcount: '374'
ht-degree: 100%

---


# Note sulla versione di AEM as a Cloud Service 2020.5.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.5.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.5.0 è il 7 maggio 2020.

## Novità di AEM Sites {#aem-sites}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di AEM Sites in AEM as a Cloud Service, versione 2020.5.0.

* Informazioni dettagliate sul processo sono ora disponibili dopo l’elaborazione degli spostamenti in massa delle pagine e dei rollout come processi asincroni.
* Quando si copia/incolla una struttura di pagina, ora è possibile scegliere se incollare solo la pagina principale o anche le pagine secondarie della struttura.
* I frammenti di esperienza AEM esportati nelle aree di lavoro di Adobe Target ora vengono visualizzati come tipi di offerta univoci e origini offerte in Target.
* MSM: l&#39;utilizzo dell’attivazione di *pubblicazione* ora esegue correttamente gli eventi di eliminazione per i componenti nella Live Copy di origine, ovvero l’eliminazione dei componenti di una Live Copy che erano stati eliminati nell&#39;origine della Live Copy.
* MSM: i componenti Live Copy ora vengono rinominati in *_msm_move* dopo il rollout dello stesso componente dalla Live Copy di origine.


## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.5.0.

### Novità {#what-is-new}

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

