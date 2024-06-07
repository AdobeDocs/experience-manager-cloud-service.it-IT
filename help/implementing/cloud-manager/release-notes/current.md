---
title: Note sulla versione 2024.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2024.6.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 5644e6f433b18408780e13057ba469e7c4926f78
workflow-type: ht
source-wordcount: '702'
ht-degree: 100%

---


# Note sulla versione 2024.6.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.6.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.6.0 in AEM as a Cloud Service è il 6 giugno 2024. La prossima versione è prevista per l’11 luglio 2024.

## Novità {#what-is-new}

* Ora puoi [utilizzare i tuoi archivi GitHub](/help/implementing/cloud-manager/managing-code/private-repositories.md) come origini per pipeline full-stack e front-end.
   * Inoltre, puoi sfruttare gli archivi GitHub con [sottomoduli Git,](/help/implementing/cloud-manager/managing-code/git-submodules.md) che forniscono un controllo avanzato sulle pipeline generate automaticamente utilizzate per la convalida delle richieste pull e di definire i comportamenti per le metriche cruciali durante la fase di scansione del codice.
   * [Puoi anche scegliere](/help/implementing/cloud-manager/managing-code/github-check-config.md) di mantenere la cronologia dei rapporti su GitHub, assegnare un nome alla pipeline e impostare le variabili della pipeline in base alle tue esigenze.
* [Ripristino self-service dei contenuti](/help/operations/restore.md) consente il ripristino del backup per un massimo di sette giorni e offre le seguenti funzionalità:
   * Ripristino del backup in un momento specifico per le 24 ore precedenti
   * Ripristini a tempo fisso per un massimo di sette giorni
* [Nuove regole OakPal](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) sono state aggiunte all’analisi di qualità del codice di Cloud Manager.
   * Ogni nuova regola aggiunta a partire da giugno 2024 è una modifica senza interruzioni.
   * Ti invitiamo a risolvere questi problemi il prima possibile, poiché queste nuove regole causeranno un errore delle pipeline a partire dalla versione di agosto 2024 di Cloud Manager.

## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma dei primi utilizzatori di Adobe.

### Supporto per Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, [ora è possibile integrare il sito con Edge Delivery Services direttamente in Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e preparare per il lancio utilizzando un’esperienza guidata e self-service.

Ciò consente un’esperienza unificata per tutte le proprietà AEM, garantendo la coerenza con tutti i flussi di lavoro critici, tra cui la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a `aemcs-cmedgedelsvs-program-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID. 

### Certificati convalidati dal dominio (DV)

Cloud Manager ora consente di: [generare e gestire certificati SSL convalidati dal dominio (DV) in modalità self-service.](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Questo offre la soluzione più veloce, facile e conveniente per creare un sito web sicuro per il tuo business online.

Se ti interessa testare questa nuova funzionalità e condividere il feedback, invia un’e-mail a `Grp-aemcs-dv-dert-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID.

### Raccolta lato client tramite il Monitoraggio degli utenti reali (RUM) {#rum}

Puoi sfruttare il [Servizio dati del Monitoraggio degli utenti reali (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) per abilitare la raccolta lato client per AEM as a Cloud Service.

Il servizio dati del monitoraggio utenti reali (RUM) offre una panoramica più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a `aemcs-rum-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID. Includi il nome di dominio per gli ambienti di produzione, staging e sviluppo nell’e-mail.  La disponibilità del programma per i primi utilizzatori di questa funzione è limitata.

### Dashboard di Experience Audit {#experience-audit-dashboard}

La [dashboard di Audit dell’esperienza di Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una vista dei trend dei punteggi delle prestazioni della pagina, oltre a insight e consigli per aiutarti a migliorarli. La funzione Audit dell’esperienza è inclusa come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi eseguirla su qualsiasi pagina web pubblica o che richiede l’autenticazione. Sono disponibili audit di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Ti interessa testare la nuova dashboard? Per iniziare, invia un’e-mail a `aem-lighthouse-pilot@adobe.com` dall’e-mail associata al tuo Adobe ID.
