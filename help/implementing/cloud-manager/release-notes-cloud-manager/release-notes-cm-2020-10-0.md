---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.10.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2020.10.0
feature: Release Information
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 48%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.10.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.10.0 è il 10 ottobre 2020.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* La pagina Ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* Il contenitore di build di Cloud Manager ora supporta la compilazione di progetti utilizzando Java 8 o Java 11. Il supporto per Java 11 è fornito dal sistema Maven toolchain.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Nella scheda Ambiente della pagina Panoramica sono ora elencati fino a tre ambienti. Gli utenti possono selezionare **Mostra tutto** per passare alla pagina di riepilogo Ambiente e visualizzare una tabella con un elenco completo di ambienti.
Fai riferimento a [Ambiente di visualizzazione](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) per ulteriori dettagli.


### Correzioni di bug {#bug-fixes-cloud-manager}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* I pulsanti Annulla e Salva nella pagina Modifica pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.
