---
title: Note sulla versione 2021.5.0 di Cloud Manager in AEM as a Cloud Service
description: Note sulla versione 2021.5.0 di Cloud Manager in AEM as a Cloud Service
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 100%

---

# Note sulla versione 2021.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2021.5.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>Per visualizzare le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.

### Novità {#what-is-new}

* Ora la regola di qualità PackageOverlaps rileva i casi in cui lo stesso pacchetto viene distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL di Git.

* Ora il registro di distribuzione scaricato dall’utente di Cloud Manager è più dettagliato e include dettagli sugli scenari di errore e di completamento corretto.

* Sono stati risolti gli errori intermittenti che si verificavano durante il push del codice nell’archivio Git di Adobe.

* Ora è possibile applicare il componente aggiuntivo Commerce ai programmi sandbox durante il flusso di lavoro Modifica programma.

* L’esperienza *Modifica programma* è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli dell’ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda **Soluzioni e componenti aggiuntivi** nei flussi di lavoro **Aggiungi programma** e **Modifica programma** mostrano la soluzione anche se per il programma ne è disponibile solo una.

* Il messaggio di errore nel registro della fase di build relativo a quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes}

* In alcuni casi, l’utente visualizzava uno stato verde “attivo” a fianco di un elenco IP consentiti anche quando tale configurazione non era stata distribuita.

* Anziché rimuovere le variabili “eliminate”, l’API delle variabili della pipeline si limitava a contrassegnarle con lo stato **ELIMINATE**.

* Alcuni problemi di qualità di tipo code smell influivano erroneamente sulla valutazione dell’affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando l’esecuzione di una pipeline veniva avviata tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era sempre superiore alla versione creata il giorno precedente.

* Ora durante la configurazione del programma sandbox, al termine della creazione corretta del progetto con il codice di esempio, viene visualizzato il collegamento Gestisci Git nella scheda hero della pagina Panoramica.
