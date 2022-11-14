---
title: Note sulla versione 2021.4.0 di Cloud Manager in AEM as a Cloud Service
description: Note sulla versione 2021.4.0 di Cloud Manager in AEM as a Cloud Service
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# Note sulla versione 2021.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2021.4.0 di Cloud Manager in AEM as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.4.0 è il 8 aprile 2021.
La prossima versione è pianificata per il 6 maggio 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente dei flussi di lavoro Aggiungi e Modifica programma è stata aggiornata per renderli più intuitivi.

* Ora gli utenti con le autorizzazioni necessarie possono inviare l’endpoint di Commerce tramite l’interfaccia utente.

* Ora le variabili di ambiente possono avere l’ambito di un servizio specifico tra Author o Publish. Richiede AEM versione `2021.03.5104.20210328T185548Z` o superiore.

* Il pulsante **Gestisci Git** viene visualizzato nella scheda Pipeline anche quando non è stata configurata alcuna pipeline.

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 27.

* Ora non è più possibile modificare o eliminare accidentalmente i progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager.

* Quando l’utente aggiunge un nuovo ambiente viene informato che, dopo la sua creazione, l’ambiente non può essere spostato in un’area geografica diversa.

* Ora le variabili di ambiente possono avere l’ambito di un servizio specifico tra Author o Publish. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* Il messaggio di errore durante l’avvio di una pipeline quando un ambiente veniva eliminato è stato corretto per maggiore chiarezza.

* Ora i bundle OSGi forniti dai progetti Eclipse sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Ora quando si modifica la pagina Audit dell’esperienza di una pipeline inserendo un percorso di input che inizia con una barra `( / )`, il passaggio non si blocca più nello stato In sospeso.

* Quando si creava una nuova pipeline di produzione, se l’utente non aggiungeva alcuna sostituzione dei contenuti dall’audit, la pagina Home predefinita non veniva sottoposta a audit.

* Alcuni problemi relativi a `CloudServiceIncompatibleWorkflowProcess` riportavano la gravità errata nel file CSV scaricabile relativo ai problemi.

* Il controllo `Runmode` generava falsi positivi per i nodi non inclusi nella cartella.
