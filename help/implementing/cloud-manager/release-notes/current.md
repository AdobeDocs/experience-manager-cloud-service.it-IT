---
title: Note sulla versione 2024.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Scopri le note sulla versione 2024.8.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: bf8bab5a195dde6cf15a2fd52e51d58c0215fdf3
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 30%

---


# Note sulla versione 2024.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.8.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di rilascio {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.8.0 in AEM as a Cloud Service è l’martedì 12 agosto 2024. La prossima versione è pianificata per il 14 settembre 2024.

## Novità {#what-is-new}

* [Altre aree geografiche di pubblicazione](/help/operations/additional-publish-regions.md) e un [99,99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) (contratto del livello di servizio) sono ora disponibili per AEM Forms as a Cloud Service.
   * Questo miglioramento consente di ottenere SLA più elevati con tempi di attività più lunghi e latenza più bassa, garantendo esperienze all’avanguardia per gli utenti distribuiti a livello globale.

## Programma di adozione anticipata {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma dei primi utilizzatori di Adobe.

### Supporto dei Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Se disponi di Edge Delivery Services con licenza come parte di AEM Sites, [ora puoi integrare il tuo sito con Edge Delivery Services direttamente in Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e andare in diretta utilizzando un&#39;esperienza guidata e self-service.

Questa funzionalità offre un’esperienza unificata per tutte le proprietà dell’AEM. Garantisce la coerenza tra i flussi di lavoro critici, come la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a `aemcs-cmedgedelsvs-program-adopter@adobe.com` dall&#39;indirizzo e-mail associato al tuo Adobe ID.

### Certificati DV (Domain Validated)

Con Cloud Manager, ora puoi [generare e gestire in autonomia i certificati SSL convalidati dal dominio](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md). Questa funzionalità offre la soluzione più rapida, semplice e conveniente per creare un sito Web sicuro per le attività online.

Se desideri testare questa nuova funzionalità e fornire il tuo feedback, invia un&#39;e-mail a `Grp-aemcs-dv-dert-adopter@adobe.com` utilizzando l&#39;indirizzo e-mail collegato al tuo Adobe ID.

### Dashboard di Experience Audit {#experience-audit-dashboard}

La [dashboard di Audit dell’esperienza di Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una vista dei trend dei punteggi delle prestazioni della pagina, oltre a insight e consigli per aiutarti a migliorarli. La funzione Audit dell’esperienza è inclusa come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi utilizzarlo per controllare qualsiasi pagina web, pubblica o che richieda l’autenticazione. Fornisce valutazioni per prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Vuoi provare il nuovo cruscotto? Per iniziare, invia un&#39;e-mail a `aem-lighthouse-pilot@adobe.com` utilizzando l&#39;e-mail collegata al tuo Adobe ID.

## Correzione bug

* È stato risolto un raro problema a causa del quale i passaggi della pipeline venivano trovati in esecuzione dopo l’eliminazione della pipeline.
* È stato risolto un problema relativo alla visualizzazione errata dello stato `FAILED` delle pipeline di configurazione, in rari casi.
