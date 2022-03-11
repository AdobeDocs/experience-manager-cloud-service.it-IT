---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.11.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.11.0
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 8%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.11.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.11.0 è il 12 novembre 2020.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* Una nuova opzione di menu **Accesso locale** è ora disponibile per gli utenti dalle opzioni del menu ambiente nelle pagine scheda Ambiente e Riepilogo ambienti .
Fai riferimento a [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#login-locally) per ulteriori dettagli.

* La **Scopri** In Cloud Manager è stata aggiornata la scheda con le nuove immagini nell’interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguito prima dell’esecuzione della build richiede il download di un plug-in Maven.
* Il collegamento dal piè di pagina di Cloud Manager per selezionare una lingua passerà ora alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Questo verrà rilevato automaticamente e verrà tentato un riavvio.
* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .
