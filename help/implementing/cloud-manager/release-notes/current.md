---
title: Note sulla versione 2024.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulle note sulla versione 2024.7.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: a823bcd1461b847983d0243cd9abd59efd8d7b6f
workflow-type: ht
source-wordcount: '465'
ht-degree: 100%

---


# Note sulla versione 2024.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.8.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.8.0 in AEM as a Cloud Service è il14 agosto 2024. La prossima versione è prevista per il 14 settembre 2024.

## Novità {#what-is-new}

* [Ulteriori aree geografiche di pubblicazione](/help/operations/additional-publish-regions.md) e un [Accordo sul livello di servizio al 99,99%](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) sono ora disponibili per AEM Forms as a Cloud Service.
   * Questo miglioramento consente di ottenere Accordi sul livello di servizio superiori con tempi di attività più lunghi e latenza più bassa, garantendo esperienze all’avanguardia per gli utenti distribuiti a livello globale.

## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma dei primi utilizzatori di Adobe.

### Supporto per Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, [ora è possibile integrare il sito con Edge Delivery Services direttamente in Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e preparare per il lancio utilizzando un’esperienza guidata e self-service.

Questa funzionalità offre un’esperienza unificata per tutte le proprietà di AEM. Garantisce la coerenza tra i flussi di lavoro critici, tra cui la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

Se ti interessa testare questa nuova funzionalità e condividere il feedback, invia un’e-mail a `aemcs-cmedgedelsvs-program-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID.

### Certificati convalidati dal dominio (DV)

Cloud Manager ora consente di: [generare e gestire certificati SSL convalidati dal dominio (DV) in modalità self-service](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md). Questa funzionalità offre la soluzione più veloce, facile e conveniente per creare un sito web sicuro per il tuo business online.

Se ti interessa testare questa nuova funzionalità e condividere il feedback, invia un’e-mail a `Grp-aemcs-dv-dert-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID.

### Dashboard di Experience Audit {#experience-audit-dashboard}

La [dashboard di Audit dell’esperienza di Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una vista dei trend dei punteggi delle prestazioni della pagina, oltre a insight e consigli per aiutarti a migliorarli. La funzione Audit dell’esperienza è inclusa come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi utilizzarla per controllare qualsiasi pagina web pubblica o che richiede l’autenticazione. Sono disponibili valutazioni di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Vuoi provare la nuova dashboard? Per iniziare, invia un’e-mail a `aem-lighthouse-pilot@adobe.com` utilizzando l’e-mail collegata al tuo Adobe ID.

## Correzione di bug

* È stato risolto un raro problema a causa del quale i passaggi della pipeline rimanevano in esecuzione dopo l’eliminazione della pipeline.
* È stato risolto un problema relativo alla visualizzazione errata dello stato `FAILED` in rari casi delle pipeline di configurazione.
