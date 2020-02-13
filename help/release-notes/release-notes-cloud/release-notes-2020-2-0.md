---
title: Note sulla versione 2020.2.0
description: Note sulla versione 2020.2.0
translation-type: tm+mt
source-git-commit: e9514d2ba625a7df8a8126f5b0ab74b975eeda51

---


# Note sulla versione per AEM come servizio cloud 2020.2.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager come servizio Cloud 2020.2.0.

## Cloud Manager {#cloud-manager}

La data di rilascio per Cloud Manager Release 2020.2.0 è il 13 febbraio 2020.

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per Cloud Manager Release 2020.2.0.

### Novità {#what-is-new}

* La versione dell’archetipo di Adobe Experience Manager è stata aggiornata alla versione 22.
* Gli ambienti Stage e Produzione nei programmi Sandbox/Demo ora possono essere aggiornati tramite l&#39;interfaccia utente di Cloud Manager.
* Gli URL utilizzati nelle notifiche Experience Cloud sono stati ottimizzati per evitare un reindirizzamento aggiuntivo.
* I passi di esecuzione della tubazione che si sono interrotti ora lo dichiarano esplicitamente.
* Il passaggio di analisi del codice ora include un registro scaricabile.
* Il foglio di calcolo contenente i problemi rilevati durante la scansione del codice ora include una colonna con un collegamento alla documentazione per la regola specifica.

### Correzioni dei bug {#bug-fixes}

* I criteri di protezione del browser talvolta impedirebbero il corretto funzionamento di alcuni pulsanti nella schermata di esecuzione della pipeline.
* I collegamenti Panoramica, Ambienti e Attività talvolta erano disponibili nella pagina di destinazione di Cloud Manager.
* Alcuni errori durante la distribuzione potrebbero impedire erroneamente la creazione di nuove condutture.