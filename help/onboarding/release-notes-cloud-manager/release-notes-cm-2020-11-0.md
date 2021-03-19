---
title: Note sulla versione per Cloud Manager in AEM as a Cloud Service, versione 2020.11.0
description: Note sulla versione per Cloud Manager in AEM as a Cloud Service, versione 2020.11.0
feature: Informazioni sulla versione
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.11.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.11.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.11.0 è il 12 novembre 2020.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* È ora disponibile una nuova opzione di menu **Accesso locale** per gli utenti dalle opzioni del menu dell&#39;ambiente nelle pagine Scheda ambiente e Riepilogo ambienti.
Per ulteriori informazioni, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#login-locally) .

* La scheda **Informazioni** in Cloud Manager è stata aggiornata con le nuove immagini nell’interfaccia utente.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Il caricamento delle dipendenze eseguito prima dell’esecuzione della build richiede il download di un plug-in Maven.
* Il collegamento dal piè di pagina di Cloud Manager per selezionare una lingua passerà ora alla posizione corretta.
* A volte, durante la scansione del codice, il processo SonarQube non veniva avviato. Questo verrà rilevato automaticamente e verrà tentato un riavvio.
* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .
