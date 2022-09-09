---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.12.0
description: Queste sono le note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.12.0.
feature: Release Information
exl-id: ee920bc5-cad7-4fac-bf73-bc1178699f90
source-git-commit: 1b7183421b9acd30697f1dc228dd9e2728d24ba6
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.12.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.12.0 è il 16 dicembre 2021. La prossima versione è prevista per il 20 gennaio 2022.

## Novità {#what-is-new}

* L’hash di commit, già visibile nell’interfaccia utente, ora viene fornito anche nell’API.
* La pagina Attività ora include un pop-over per l’esecuzione delle pipeline che fornisce un riepilogo dei dettagli della pipeline a colpo d’occhio.
* Sono stati aggiunti aggiornamenti per includere ulteriori dettagli presentati nella pagina Attività .
* La scheda Informazioni in Cloud Manager ora include l’accesso rapido alle guide API e alle risorse associate.
* Un utente con il ruolo di gestione distribuzione può ora avviare la procedura guidata per la creazione di progetti/rami per un archivio senza rami dal menu azione nella pagina repository.
* Deployment Manager, che si trova nel flusso di lavoro di aggiunta o modifica della pipeline, ora viene informato su come creare un ramo o un progetto se l’archivio selezionato non dispone di rami.
* È stata aggiunta una nuova funzione self-service di Cloud Manager per consentire [aggiunta di variabili e segreti in formato libero a livello di ambiente.](/help/implementing/cloud-manager/environment-variables.md)
* Con il nuovo [Componente aggiuntivo Demos di riferimento](/help/journey-sites/demos-add-on/overview.md) (disponibile il 17 dicembre 2021), è possibile installare le ultime basi di codice demo per i prodotti AEM ed essere pronti per essere implementati tramite il nuovo [strumento rapido per la creazione di siti](/help/journey-sites/quick-site/overview.md) in Sites.
* Le pipeline front-end ora supportano le variabili della pipeline.
* È ora possibile abilitare gli schermi nella finestra di dialogo Modifica programma per tutte le sandbox.
* Le indicazioni fornite dalla scheda di invito all’azione nella pagina della panoramica sono state aggiornate per riflettere con precisione la sua associazione con la pipeline di stack completa di produzione.
* Sono stati aggiunti miglioramenti alla pagina Attività per ottenere ulteriori dettagli applicabili alle pipeline, tra cui codice sorgente, ID commit e così via.
* Sono stati apportati aggiornamenti minori all’interfaccia utente durante la copia delle voci TXT (&quot;valore TXT&quot; invece di &quot;record TXT&quot;) per rimuovere potenziali confusione.
* [Documentazione relativa agli errori del certificato](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) è stato aggiornato per fornire ulteriori esempi insieme ai passaggi necessari per risolvere i problemi.
* È ora disponibile un’opzione nell’esecuzione della pipeline front-end per rifiutare o approvare prima della distribuzione in produzione.
* La versione dell’Archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 32.


## Correzioni di bug {#bug-fixes}

* Gli artefatti funzionali e di test dell’interfaccia utente non sono stati inclusi nel registro dei passaggi della build.
* I registri per i passaggi di test di prodotto, funzionale e interfaccia utente non erano accessibili tramite l’API pubblica.
* In rari casi, il collegamento dalla pagina dei dettagli dell’ambiente al servizio di pubblicazione o anteprima non funzionerebbe.
* Le pipeline di produzione dello stack complete rimangono denominate &quot;pipeline di produzione&quot; anche quando l’utente immette un nome diverso nel campo name.
