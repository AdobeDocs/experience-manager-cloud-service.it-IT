---
title: Note sulla versione 2024.9.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Scopri le note sulla versione 2024.9.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 17%

---

# Note sulla versione 2024.9.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.9.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.9.0 in AEM as a Cloud Service è il 5 settembre 2024. La prossima versione è pianificata per il venerdì 3 ottobre 2024.

## Novità {#what-is-new}

* **Dashboard di controllo dell&#39;esperienza:**

  Il dashboard [Enhanced Experience Audit di Adobe Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md), con tecnologia Google Lighthouse, fornisce informazioni approfondite sulla qualità e le prestazioni di AEM Sites valutando i dati fondamentali su web, SEO (Search Engine Optimization) e le metriche di accessibilità. Consente agli utenti di identificare le aree da migliorare offrendo consigli actionable, consentendo ai team di migliorare l’esperienza utente, i tempi di caricamento delle pagine e la conformità del sito. Questa dashboard semplifica il monitoraggio delle metriche critiche del sito e garantisce che le applicazioni AEM soddisfino elevati standard di prestazioni e accessibilità.

* **Adobe di certificati di convalida del dominio generati e gestiti:**

  Con Cloud Manager, ora è possibile [Adobi self-service generati e gestiti da certificati SSL DV (convalida dominio)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). Questa funzionalità offre la soluzione più rapida, semplice e conveniente per creare un sito Web sicuro per l&#39;organizzazione online o l&#39;azienda. <!-- CMGR-52403 -->

* Supporto di **Edge Delivery Services in Cloud Manager:**

  Se disponi di una licenza per Edge Delivery Services come parte di AEM Sites, [ora puoi integrare il tuo sito con i Edge Delivery Services direttamente tramite Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md). Questa funzione consente un’esperienza di lancio guidata e self-service. Inoltre, unifica flussi di lavoro essenziali come la gestione dei nomi di dominio, i certificati SSL e le mappature CDN in tutte le proprietà dell’AEM, garantendo coerenza ed efficienza. <!-- CMGR-49859 -->

* I clienti che utilizzano gli archivi GitHub ora possono creare e utilizzare pipeline di configurazione a livello web. <!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## Correzioni di bug

* La paginazione per la vista tabella dei certificati SSL ora funziona come previsto. <!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* La versione dell&#39;artefatto errata è stata promossa quando si utilizza il pulsante **Promuovi build** da un&#39;esecuzione. <!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
