---
title: Note sulla versione per Cloud Manager 202.6.0 in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione per Cloud Manager 2022.6.0 in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 1a6ca2647cc185ed0cb60fa75d2f5752e72f5715
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---


# Note sulla versione per Cloud Manager 202.6.0 in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina documenta le note sulla versione di Cloud Manager 2022.6.0 in AEM as a Cloud Service.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.6.0 di Cloud Manager in AEM as a Cloud Service è il 9 giugno 2022. La prossima versione è prevista per il 30 giugno 2022.

## Novità {#what-is-new}

* L’interfaccia utente di Cloud Manager ora consente [ripristino automatico dei contenuti](/help/operations/backup.md) a uno stato valido noto dell&#39;ambiente cloud AEM.
   * Questa funzione verrà implementata in un approccio graduale nelle settimane successive alla versione 2022.06.0.
* Una nuova scheda di benvenuto nella pagina di destinazione di Cloud Manager consente agli utenti di accedere rapidamente alle esercitazioni di onboarding e alle metriche di avanzamento correlate al tenant.
   * Questa funzione verrà implementata in un approccio graduale durante la settimana successiva alla versione 2022.06.0.
* Gli utenti con le autorizzazioni necessarie possono accedere a un nuovo [Dashboard di licenza](/help/implementing/cloud-manager/license-dashboard.md) nella pagina di destinazione di Cloud Manager per visualizzare i dettagli delle adesioni disponibili per il tenant.
   * AEM Sites è la prima soluzione per la quale la disponibilità e il consumo di utilizzo vengono distribuiti tramite il dashboard Cloud Manage.
   * Questa funzione verrà implementata in un approccio graduale nelle settimane successive alla versione 2022.06.0.
* [Nuovo account secondario relic e gestione utenti self-service](/help/implementing/cloud-manager/user-access-new-relic.md) è ora disponibile tramite l’interfaccia utente di Cloud Manager.
   * Questa funzione verrà implementata in un approccio graduale nelle settimane successive alla versione 2022.06.0.
* Un nuovo widget Go Live sulla home page dei programmi di produzione di Cloud Service fornisce ora indicazioni per prepararsi a un&#39;esperienza live di successo.
* [È ora possibile riutilizzare gli artefatti di creazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) quando si utilizza il mirroring git.

## Modifiche API {#api-changes}

* La [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) L’API è stata dichiarata obsoleta e [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) Deve essere invece utilizzato.
   * `List Programs` continua a funzionare, ma il suo utilizzo genererà messaggi di avviso nei registri.
   * Non sarà più supportato dopo tre mesi.

