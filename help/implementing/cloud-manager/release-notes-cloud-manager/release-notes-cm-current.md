---
title: Note sulla versione 2022.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2022.12.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 516c0027f917ea1e54286b268e7a0fb4c4e2b3d7
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 48%

---


# Note sulla versione 2022.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.12.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.12.0 di Cloud Manager in AEM as a Cloud Service è il 29 novembre 2022. La prossima versione è pianificata per il 19 gennaio 2023.

## Novità {#what-is-new}

* Notifiche per [Aggiornamenti alla manutenzione AEM](/help/overview/what-is-new-and-different.md#aem-updates) verranno visualizzate nell’interfaccia utente di Cloud Manager. Questa modifica verrà implementata in modo graduale nelle settimane successive al rilascio della versione 2022.12.0.
* Quando un’acquisizione tramite il [Strumento Content Transfer (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) è in corso, lo stato dell’ambiente sia nella console per sviluppatori che in Cloud Manager viene visualizzato come `Ingestion in Progress`.
* Sono stati apportati miglioramenti alla disponibilità e all’affidabilità di [pipeline di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

## Correzioni di bug {#bug-fixes}

* È stata apportata una modifica per evitare [gasdotti front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) dall’esecuzione mentre è in corso un’esecuzione della pipeline nello stesso ambiente.
* È stata apportata una modifica per evitare un `PATCH /program//environment//variables` richiesta per ambienti con `FAILED` stato.
