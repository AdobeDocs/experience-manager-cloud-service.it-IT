---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.3.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.3.0
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2021.3.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.3.0 è l’11 marzo 2021.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* Clienti con ambienti con configurazioni di nomi di dominio personalizzati preesistenti per [ELENCHI CONSENTITI IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) e [Nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) visualizzerà un messaggio sulle configurazioni esistenti in precedenza e sarà in grado di self-service tramite l’interfaccia utente di .

* Gli utenti con le autorizzazioni necessarie possono ora modificare un programma, consentendo loro di effettuare le seguenti operazioni in modalità self-service:
   * Aggiungi la soluzione Sites a un programma esistente con Assets o viceversa.
   * Rimuovi Sites o Assets da un programma esistente sia con Sites che con Assets.
   * Aggiungi il secondo diritto inutilizzato alla soluzione a un programma esistente o a un nuovo programma.

* **Aggiornamento della manutenzione AEM** verrà ora visualizzata l’etichetta per le schermate di esecuzione della pipeline e di attività.

* Se un ambiente è in ibernazione ma è disponibile anche un aggiornamento AEM, il **Sospeso** lo stato ha la precedenza **Aggiornamento disponibile**.

* Gli utenti possono ora visualizzare i propri ruoli di Cloud Manager selezionando l’opzione &quot;Visualizza ruoli Cloud Manager&quot; dopo aver visualizzato l’icona Profilo utente (in alto a destra) di Unified Shell.

* Etichetta **Domanda di approvazione** è stato riassegnato a **Approvazione produzione** per una maggiore chiarezza.

* La **Versione** l’etichetta è stata rinominata in **Tag Git** nella schermata di esecuzione della pipeline di produzione .

* Le etichette che definiscono il comportamento quando metriche importanti non soddisfano la soglia definita sono state rinominate per rispecchiare il loro comportamento effettivo: **Annulla immediatamente** e **Approva immediatamente**.

* Gli elenchi di elementi obsoleti di classi e metodi sono stati aggiornati in base alla versione `2021.3.4997.20210303T022849Z-210225` dell’SDK AEM Cloud Service.

* La pipeline di produzione di Cloud Manager ora include [Test personalizzati dell&#39;interfaccia utente](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) funzionalità.

### Correzioni di bug  {#bug-fixes}

* Il controllo delle versioni del pacchetto è stato ignorato in alcuni casi durante AEM aggiornamento push.

* Alcuni problemi di qualità non sono stati rilevati correttamente quando i pacchetti sono stati incorporati in altri pacchetti.

* In situazioni oscure, il nome predefinito del programma generato all’apertura della finestra di dialogo Aggiungi programma potrebbe essere un duplicato di un nome di programma esistente.

* Talvolta, se l’utente si allontana dalla pagina di esecuzione della pipeline immediatamente dopo l’avvio di una pipeline, viene visualizzato un messaggio di errore che indica che l’azione non è riuscita, anche se l’esecuzione viene effettivamente avviata.

* Il passaggio di compilazione è stato riavviato inutilmente quando le build del cliente hanno generato pacchetti non validi.

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Inserire nell&#39;elenco Consentiti IP anche quando tale configurazione non è stata distribuita.

* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .
