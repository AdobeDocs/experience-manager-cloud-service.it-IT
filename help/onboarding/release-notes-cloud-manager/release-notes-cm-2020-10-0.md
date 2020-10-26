---
title: Note sulla versione 2020.10.0
description: Note sulla versione 2020.10.0
translation-type: tm+mt
source-git-commit: 9ed52fb3a9971bcaede71613774f653273a86530
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 60%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

In questa pagina sono delineate le Note sulla versione di Marketing Cloud Manager in AEM come Cloud Service 2020.10.0.

## Data di rilascio {#release-date}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.10.0 è il 01 ottobre 2020.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo degli ambienti.
Per ulteriori informazioni, consulta [Visualizzazione degli ambienti](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) .


### Correzioni di bug {#bug-fixes-cloud-manager}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* I pulsanti Annulla e Salva nella pagina Modifica pipeline non produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.