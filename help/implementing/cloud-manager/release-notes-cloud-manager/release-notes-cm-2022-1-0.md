---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.01.0
description: Queste sono le note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2022.01.0.
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 62%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2022.01.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2022.01.0.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2022.01.0 è il 20 gennaio 2022. La prossima versione è prevista per il 10 febbraio 2022.

## Novità {#what-is-new}

* Cloud Manager [evita di ricostruire la base di codice quando rileva che viene utilizzato lo stesso commit git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) in più esecuzioni di pipeline full-stack.
* L’accesso al registro dell’ambiente AEM ora richiede il profilo di prodotto **Gestione distribuzione**. Gli utenti senza questo profilo visualizzeranno un pulsante disabilitato nell’interfaccia utente.
* L’interfaccia utente non consente la configurazione della pipeline front-end per un programma in cui Sites non è abilitato come soluzione.
* Al momento della generazione di una password git, verrà visualizzata la data di scadenza.

## Correzioni di bug {#bug-fixes}

* Sono state corrette le eccezioni Null al puntatore rilevate da alcune distribuzioni di pipeline front-end.
* È ora possibile aggiungere, aggiornare ed eliminare variabili di ambiente quando un ambiente esegue una versione obsoleta di AEM.
* Il passaggio dell’immagine della build non verrà più contrassegnato come ERRORE per le pipeline che hanno utilizzato il passaggio pianificato in alcuni rari casi.
* Per i programmi con un solo archivio, nella schermata di esecuzione della pipeline viene ora visualizzato il nome dell’archivio.
