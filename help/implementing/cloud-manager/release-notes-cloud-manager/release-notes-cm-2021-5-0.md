---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0
feature: Informazioni sulla versione
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.5.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0.

>[!NOTE]
>Per visualizzare il Cloud Service delle note sulla versione corrente per Adobe Experience Manager, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.

### Novità {#what-is-new}

* La regola di qualità PackageOverlaps ora rileva i casi in cui lo stesso pacchetto è stato distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL Git.

* Il registro di distribuzione scaricato da un utente di Cloud Manager sarà più dettagliato e ora includerà dettagli sugli errori e sugli scenari di successo.

* Sono stati risolti gli errori intermittenti durante il push del codice all’Git di Adobe.

* È ora possibile applicare il componente aggiuntivo Commerce ai programmi Sandbox durante il flusso di lavoro Modifica programma .

* L&#39;esperienza *Modifica programma* è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda **Soluzioni e componenti aggiuntivi** in **Aggiungi programma** e **Modifica programma** mostrerà la soluzione, anche se per il programma è disponibile una sola soluzione.

* Il messaggio di errore nel registro dei passaggi della build quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes}

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Invece di rimuovere le variabili &quot;eliminate&quot;, le variabili delle pipeline API le contrassegnavano solo con lo stato **ELIMINATO**.

* Alcuni problemi di qualità del tipo di odore del codice hanno avuto un impatto errato sul rating di affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando è stata avviata l’esecuzione di una pipeline tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era garantita come maggiore di una versione creata il giorno precedente.

* Durante la configurazione del programma Sandbox, una volta che il progetto con codice di esempio è stato creato correttamente, Manage Git (Gestisci Git) apparirà come collegamento dalla scheda eroe nella pagina Overview (Panoramica).
