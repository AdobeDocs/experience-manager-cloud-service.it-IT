---
title: Note sulla versione 2020.3.0
description: Note sulla versione 2020.3.0
translation-type: tm+mt
source-git-commit: bcbb50f467a0e3b3047e2bb872a8fe39a9f02a1a

---


# Release Notes for AEM as a Cloud Service 2020.3.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager come servizio Cloud 2020.3.0.

## Cloud Manager {#cloud-manager}

La data di rilascio per Cloud Manager Release 2020.3.0 è il 05 marzo 2020.

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per Cloud Manager Release 2020.3.0.

### Novità {#what-is-new}

* Il registro per il passaggio di compilazione ora è disponibile mentre il passaggio di compilazione è in esecuzione.
* Alcuni dei messaggi nella pagina dei dettagli dell&#39;esecuzione della pipeline sono stati modificati per maggiore chiarezza.

### Correzioni dei bug {#bug-fixes}

* Non è stato possibile scaricare i file di registro per i passaggi di test funzionali personalizzati e del prodotto tramite l&#39;interfaccia utente.
* Quando non è stato possibile creare l&#39;archivio git per un programma Servizio Cloud, gli utenti nel ruolo Gestione distribuzione a volte non sono stati in grado di recuperare da questo errore.
* Alcune attività degli utenti durante la creazione di un programma sandbox potrebbero causare il fallimento della creazione del programma prima della creazione della pipeline non di produzione.
* L&#39;istanza temporanea SonarQube utilizzata nel passaggio di compilazione non riusciva a avviarsi all&#39;interno del timeout configurato.
* La creazione simultanea di ambienti di sviluppo nello stesso programma Cloud Service potrebbe incontrare una condizione in cui solo uno è stato possibile creare correttamente.
* Le notifiche Experience Cloud per i programmi del servizio Cloud non sono state ricevute in modo coerente.
* In progetti specifici, gli oggetti *ResourceResolver dovrebbero essere sempre chiusi* genererebbe un&#39;eccezione di puntatore Null; tuttavia, ciò non ha influito sull&#39;esecuzione della pipeline.

