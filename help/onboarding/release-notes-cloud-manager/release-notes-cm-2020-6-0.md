---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.6.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.6.0
feature: Informazioni sulla versione
exl-id: 879a5025-f94f-4549-bf6e-e1cc6b6a7b58
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 83%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.6.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.6.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.6.0 è il 4 giugno 2020.

## Novità {#whats-new-cloud-manager}

* Un utente con il ruolo *Proprietario business* in Cloud Manager è ora in grado di eliminare un programma sandbox dalla pagina di destinazione (tramite il pulsante di azione rapida nella scheda Programma) o dall’interno del programma.

   Per ulteriori informazioni, consulta [Eliminazione di un programma sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html).

* Un utente del programma sandbox con il ruolo di *Proprietario business* o *Manager implementazione* in Cloud Manager è ora in grado di eliminare l’ambiente di produzione e stage impostato tramite l’interfaccia di Cloud Manager. L’opzione di eliminazione è ora disponibile sia nella scheda Ambiente nella pagina **Panoramica dei programmi**, sia nella pagina **Ambienti**. Selezionando l’opzione Elimina in Produzione o Stage, viene eliminato anche l’altro nel set.

   Per ulteriori informazioni, consulta [Eliminazione di un programma sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html).

* Delle descrizioni sulla pagina di destinazione forniscono all’utente istruzioni di base sulla navigazione.

* Delle descrizioni nella pagina **Panoramica del programma** forniscono all’utente istruzioni di base sulla navigazione in Cloud Manager, utili per iniziare a usarlo.

* Cloud Manager ora presenta una pagina **SCOPRI**, accessibile tramite la navigazione superiore. Questa pagina include risorse per aiutare gli utenti a conoscere i flussi di lavoro più utilizzati in base ai loro ruoli assegnati in Cloud Manager.

* I programmi sandbox ora sono identificati da un contrassegno **Sandbox** visualizzato sulla scheda del programma nella pagina di destinazione e accanto al nome del programma nella pagina **Panoramica del programma**.

* Un utente con il ruolo SysAdmin ora ha accesso con un solo clic alla posizione in Admin Console da cui è possibile gestire i ruoli o le autorizzazioni degli utenti per Cloud Manager. Nella pagina di destinazione è ora disponibile un pulsante **Gestisci accesso** accanto al pulsante **Aggiungi programma**.

   Per ulteriori informazioni, consulta [Attività SysAdmin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks).

* Un utente con il ruolo SysAdmin ora dispone dell’accesso con un solo clic all’istanza di authoring direttamente da Cloud Manager.

   Per ulteriori informazioni, consulta [Gestione dell’accesso all’istanza di authoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem).

* Il registro Build ora include l’elenco degli artefatti individuati, inclusi i pacchetti di contenuti saltati.

* Il passaggio Build ora verifica se tutti i pacchetti di contenuto generati includono tutte le proprietà obbligatorie: nome, gruppo e versione.

* Il passaggio Build ora verifica se la build ha prodotto almeno un pacchetto di contenuto.

### Correzioni di bug {#bug-fixes-cm}

* In alcune situazioni, le icone nella finestra di dialogo **Crea programma** non erano allineate.

* L’identificatore di versione di AEM non veniva visualizzato in modo coerente nella pagina **Panoramica dei programmi**.

* Durante la configurazione della pipeline di produzione, l’opzione **Scheduled Deployment** (Implementazione pianificata) non era visibile per alcuni clienti.

### Problemi noti {#known-issues-cm}

* Gli ambienti di un programma sandbox vengono ibernati se non viene rilevata alcuna attività per un certo periodo di tempo. Questo stato non sarà osservato in Cloud Manager. Tuttavia, lo stato può essere osservato tramite la Console per sviluppatori. Questo problema sarà risolto in una versione successiva.

* Il collegamento alla Console per sviluppatori direttamente da Cloud Manager non mostra l’opzione per ibernare/riattivare l’ambiente di un programma sandbox. Per risolvere questo problema, una volta nella Console per sviluppatori, aggiungi il pattern `#release-cm-p1234-e5678` alla fine dell’URL, dove *1234* è l’ID del programma e *5678* è l’ID dell’ambiente. Questo problema sarà risolto in una versione successiva.
