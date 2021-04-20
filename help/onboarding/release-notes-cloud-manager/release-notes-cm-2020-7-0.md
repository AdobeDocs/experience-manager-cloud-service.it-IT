---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.7.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.7.0
feature: Release Information
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 73%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.7.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.7.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.7.0 è il 9 luglio 2020.

## Novità {#whats-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Le pipeline di Cloud Manager ora supportano variabili e segreti impostati dal cliente.

   Per ulteriori informazioni, consulta [Variabili delle pipeline](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables).

* Gli archivi Maven privati con associazione a autenticazione sono ora supportati.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.
Per ulteriori informazioni, consulta [Utilizzo del supporto Java 11](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) .

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.

### Problemi noti {#known-issues}

* A causa di una modifica nel modo in cui viene calcolata la copertura del codice, la versione *minima* del plugin Jacoco è ora 0.7.5.201505241946 (rilasciata a maggio 2015). I clienti che si riferiscono esplicitamente a una versione precedente ricevono un messaggio di errore nel processo di qualità del codice.