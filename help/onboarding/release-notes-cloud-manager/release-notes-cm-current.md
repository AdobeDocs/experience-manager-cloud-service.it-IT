---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.3.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.3.0
translation-type: tm+mt
source-git-commit: 36e5e90785a1bc9a4f4f8d4febd462e00252a0ea
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.3.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.3.0 è l’11 marzo 2021.
La prossima versione è prevista per il 08 aprile 2021.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* I clienti con ambienti con configurazioni di nomi di dominio personalizzati preesistenti per [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) e [Nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) visualizzeranno un messaggio sulle configurazioni esistenti in precedenza e saranno in grado di self-service tramite l&#39;interfaccia utente.

* Gli utenti con le autorizzazioni necessarie possono ora modificare un programma, consentendo loro di effettuare le seguenti operazioni in modalità self-service:
   * Aggiungi la soluzione Sites a un programma esistente con Assets (o viceversa).
   * Rimuovi Sites (o Assets) da un programma esistente sia con Sites che con Assets.
   * Aggiungi il secondo diritto inutilizzato alla soluzione a un programma esistente o a un nuovo programma.

* AEM&#39;etichetta Push Update&quot; verrà ora visualizzata sia per le schermate Pipeline Execution che per Activity.

* Se un ambiente è in ibernazione ma è disponibile anche un aggiornamento AEM, lo stato &quot;Sospeso&quot; avrà la precedenza rispetto a &quot;Aggiorna disponibile&quot;.

* Gli utenti possono ora visualizzare i propri ruoli di Cloud Manager selezionando l’opzione &quot;Visualizza ruoli Cloud Manager&quot; dopo aver visualizzato l’icona Profilo utente (in alto a destra) di Unified Shell.

* L&#39;etichetta &quot;Domanda di approvazione&quot; è stata rinominata &quot;Approvazione produzione&quot; per maggiore chiarezza.

* L’etichetta &quot;Versione&quot; è stata rinominata &quot;Git Tag&quot; nella schermata di esecuzione della pipeline di produzione.

* Le etichette che definiscono il comportamento quando le metriche importanti non soddisfano la soglia definita sono state rinominate per rispecchiare il loro comportamento effettivo - Annulla immediatamente e Approva immediatamente.

* Gli elenchi di elementi obsoleti di classi e metodi sono stati aggiornati in base alla versione `2021.3.4997.20210303T022849Z-210225` dell’SDK del Cloud Service AEM.

* La pipeline di produzione di Cloud Manager ora include funzionalità di test dell’interfaccia utente personalizzata.

### Correzioni di bug {#bug-fixes}

* Il controllo delle versioni del pacchetto è stato ignorato in alcuni casi durante AEM aggiornamento push.

* Alcuni problemi di qualità non sono stati rilevati correttamente quando i pacchetti sono stati incorporati in altri pacchetti.

* In situazioni oscure, il nome predefinito del programma generato all’apertura della finestra di dialogo Aggiungi programma potrebbe essere un duplicato di un nome di programma esistente.

* Talvolta, se l’utente si allontana dalla pagina di esecuzione della pipeline immediatamente dopo l’avvio di una pipeline, viene visualizzato un messaggio di errore che indica che l’azione non è riuscita, anche se l’esecuzione viene effettivamente avviata.

* Il passaggio di compilazione è stato riavviato inutilmente quando le build del cliente hanno generato pacchetti non validi.

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Inserire nell&#39;elenco Consentiti IP anche quando tale configurazione non è stata distribuita.

* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .