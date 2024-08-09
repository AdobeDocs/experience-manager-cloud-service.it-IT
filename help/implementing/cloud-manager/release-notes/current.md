---
title: Note sulla versione 2024.7.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2024.7.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 8d9f5296a2e79ee5560d1ede967b3eb2155cd151
workflow-type: ht
source-wordcount: '633'
ht-degree: 100%

---


# Note sulla versione 2024.7.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.7.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2024.7.0 di Cloud Manager in AEM as a Cloud Service è il 18 luglio 2024. La prossima versione è prevista per l’12 agosto 2024.

## Novità {#what-is-new}

* Il trigger **Cambiamenti su Git** della [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline) e della [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline) per avviare la pipeline in un commit è ora disponibile per gli [archivi privati.](/help/implementing/cloud-manager/managing-code/private-repositories.md)
   * Questa funzione verrà implementata in modo graduale con il completamento entro la metà di agosto.
* Quando si aggiunge un [certificato DV gestito da Adobe,](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) è ora possibile aggiungere un singolo certificato che copre più domini anziché crearne uno per ciascun dominio.
* È ora possibile aggiungere a un programma soluzioni che non dispongono di [ulteriori aree geografiche di pubblicazione](/help/operations/additional-publish-regions.md), purché il programma disponga di almeno una soluzione Sites o Forms applicabile.
* È ora possibile aggiungere a un programma soluzioni che non dispongono del [99,99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla), purché il programma disponga di almeno una soluzione Sites o Forms applicabile.
* La [dashboard dell’audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-dashboard.md) è stato migliorata in diversi modi.
   * Gli audit ora vengono eseguiti su endpoint `.com` tramite CDN, sostituendo il precedente approccio `.net`.
      * Questa modifica simula in modo più accurato le esperienze degli utenti reali e consente di prendere decisioni più informate sulla gestione e l’ottimizzazione del sito web.
   * Sono stati apportati diversi miglioramenti all’interfaccia utente dell’audit dell’esperienza, tra cui:
      * È stata aggiunta una vista delle tendenze su prestazioni, best practice, SEO e accessibilità.
      * Il collegamento del rapporto non elaborato Lighthouse è ora visibile in modo più intuitivo direttamente nel pannello dei dettagli delle istantanee di scansione.
      * La sezione consigli di Lighthouse è stata migliorata.
   * La metrica PWA è stata rimossa in conformità alla versione 12.0.0 di Lighthouse, che l’ha eliminata.
* L’[Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) è stato aggiornato alla [versione 49.](https://github.com/adobe/aem-project-archetype/tree/aem-project-archetype-49)

## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma dei primi utilizzatori di Adobe.

### Supporto per Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, [ora è possibile integrare il sito con Edge Delivery Services direttamente in Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e preparare per il lancio utilizzando un’esperienza guidata e self-service.

Ciò consente un’esperienza unificata per tutte le proprietà AEM, garantendo la coerenza con tutti i flussi di lavoro critici, tra cui la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a `aemcs-cmedgedelsvs-program-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID. 

### Certificati convalidati dal dominio (DV)

Cloud Manager ora consente di: [generare e gestire certificati SSL convalidati dal dominio (DV) in modalità self-service.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Questo offre la soluzione più veloce, facile e conveniente per creare un sito web sicuro per il tuo business online.

Se ti interessa testare questa nuova funzionalità e condividere il feedback, invia un’e-mail a `Grp-aemcs-dv-dert-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID.

### Dashboard di Experience Audit {#experience-audit-dashboard}

La [dashboard di Audit dell’esperienza di Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una vista dei trend dei punteggi delle prestazioni della pagina, oltre a insight e consigli per aiutarti a migliorarli. La funzione Audit dell’esperienza è inclusa come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi eseguirla su qualsiasi pagina web pubblica o che richiede l’autenticazione. Sono disponibili audit di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Ti interessa testare la nuova dashboard? Per iniziare, invia un’e-mail a `aem-lighthouse-pilot@adobe.com` dall’e-mail associata al tuo Adobe ID.
