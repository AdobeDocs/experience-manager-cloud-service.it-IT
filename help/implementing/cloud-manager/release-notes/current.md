---
title: Note sulla versione 2023.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.5.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 41%

---


# Note sulla versione 2023.5.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.5.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2023.5.0 di Cloud Manager in AEM as a Cloud Service è l’11 maggio 2023. La prossima versione è prevista per il 8 giugno 2023.

## Novità {#what-is-new}

* Il supporto per i test di prodotto, funzionale e interfaccia utente è stato esteso a [test della pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
* Oltre ad abilitare i test a monte, [Il supporto per i test dell’interfaccia utente è stato esteso ai test Cypress.](/help/implementing/cloud-manager/ui-testing.md)
* [Copia dei contenuti self-service](/help/implementing/developing/tools/content-copy.md) è ora disponibile da un ambiente più alto a uno più basso tramite l’interfaccia utente di Cloud Manager.
* Il passaggio di convalida dell’esecuzione della pipeline è stato migliorato per convalidare lo stato delle code di replica all’inizio del processo di esecuzione. In questo modo i passaggi di distribuzione non vengono influenzati dalle code bloccate che devono essere gestite dagli utenti AEM amministratori direttamente nell’ambiente di authoring.

## Correzioni di bug {#bug-fixes}

* La creazione dell’ambiente non ha più esito negativo quando nel nome dell’ambiente vengono utilizzati caratteri multibyte.
