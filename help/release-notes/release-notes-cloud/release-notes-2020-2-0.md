---
title: Note sulla versione 2020.2.0
description: Note sulla versione 2020.2.0
translation-type: ht
source-git-commit: e9514d2ba625a7df8a8126f5b0ab74b975eeda51

---


# Note sulla versione di AEM as a Cloud Service 2020.2.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.2.0.

## Cloud Manager {#cloud-manager}

La data di rilascio della versione 2020.2.0 di Cloud Manager è il 13 febbraio 2020.

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti della versione 2020.2.0 di Cloud Manager.

### Novità {#what-is-new}

* La versione dell’archetipo di Adobe Experience Manager è stata aggiornata alla versione 22.
* Gli ambienti di stage e produzione nei programmi Sandbox/Demo ora possono essere aggiornati tramite l’interfaccia utente di Cloud Manager.
* Gli URL utilizzati nelle notifiche di Experience Cloud sono stati ottimizzati per evitare un reindirizzamento aggiuntivo.
* I passaggi di esecuzione della pipeline interrotti a causa di timeout ora vengono segnalati in modo esplicito.
* Il passaggio di analisi del codice ora include un registro scaricabile.
* Il foglio di calcolo che contiene i problemi rilevati durante la scansione del codice ora include una colonna con un collegamento alla documentazione per la regola specifica.

### Correzioni di bug {#bug-fixes}

* Talvolta, i criteri di sicurezza del browser impedivano il corretto funzionamento di alcuni pulsanti nella schermata di esecuzione della pipeline.
* I collegamenti Panoramica, Ambienti e Attività talvolta erano disponibili nella pagina di destinazione di Cloud Manager.
* Alcuni errori durante l’implementazione potevano impedire erroneamente la creazione di nuove pipeline.