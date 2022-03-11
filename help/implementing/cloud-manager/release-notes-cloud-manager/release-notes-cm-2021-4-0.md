---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.4.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.4.0
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.4.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2021.4.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.4.0 è l’8 aprile 2021.
La prossima versione è prevista per il 6 maggio 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente è aggiornata ai flussi di lavoro Aggiungi e Modifica programma per renderlo più intuitivo.

* Un utente con le autorizzazioni necessarie può ora inviare l’endpoint di e-commerce tramite l’interfaccia utente di .

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione `2021.03.5104.20210328T185548Z` o superiore.

* La **Gestisci Git** sulla scheda Pipelines viene visualizzato il pulsante anche quando non è stata configurata alcuna pipeline.

* La versione dell’archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 27.

* I progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager non possono più essere modificati o eliminati accidentalmente.

* Quando un utente aggiunge un nuovo ambiente, viene informato che una volta creato l’ambiente non può essere spostato in un’area diversa.

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* È stato chiarito il messaggio di errore durante l’avvio di una pipeline quando un ambiente è stato eliminato.

* I bundle OSGi forniti dai progetti Eclipse ora sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Quando modifichi la pagina di audit esperienza di una pipeline, crea un percorso di input che inizia con una barra `( / )` non comporterà più il blocco del passaggio nello stato in sospeso.

* Quando viene creata una nuova pipeline di produzione, se l’utente non aggiunge alcuna sostituzione di controllo del contenuto, la pagina home predefinita non è stata sottoposta a controllo.

* Problemi relativi al `CloudServiceIncompatibleWorkflowProcess` aveva la gravità errata nel file CSV del problema scaricabile.

* La `Runmode` check stava producendo falsi positivi sui nodi non cartelle.
