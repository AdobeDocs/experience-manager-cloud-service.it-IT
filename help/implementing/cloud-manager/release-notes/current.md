---
title: Note sulla versione 2024.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2024.3.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4bae300f653ae6b84cf798f4fe9e8c9326963718
workflow-type: ht
source-wordcount: '648'
ht-degree: 100%

---


# Note sulla versione 2024.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.3.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione della versione 2024.3.0 di Cloud Manager in AEM as a Cloud Service è il 14 marzo 2024. La prossima versione è prevista per l’11 aprile 2024.

## Novità {#what-is-new}

* [Ora puoi creare un’infrastruttura di rete avanzata](/help/security/configuring-advanced-networking.md) nel programma Cloud Manager e configurare gli ambienti in modo autonomo utilizzando l’interfaccia utente di Cloud Manager.
* I [dettagli del passaggio di esecuzione della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) comprenderanno la fase corrente dell’implementazione e gli elementi previsti.

## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma dei primi utilizzatori di Adobe.

### Raccolta lato client tramite il Monitoraggio degli utenti reali (RUM) {#rum}

Puoi sfruttare il [Servizio dati del Monitoraggio degli utenti reali (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) per abilitare la raccolta lato client per AEM as a Cloud Service.

Il servizio dati del monitoraggio utenti reali (RUM) offre una panoramica più precisa delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. Rappresenta un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per chi utilizza una rete CDN gestita o non gestita da Adobe. Per chi utilizza una rete CDN non gestita da Adobe, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a `aemcs-rum-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID. Includi il nome di dominio per gli ambienti di produzione, staging e sviluppo nell’e-mail.  La disponibilità del programma per i primi utilizzatori di questa funzione è limitata.

### Porta il tuo GitHub personale {#byo-github}

Se utilizzi GitHub per gestire gli archivi, [ora puoi convalidare il codice direttamente all’interno degli archivi GitHub tramite Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Questa integrazione elimina la necessità di sincronizzare in modo coerente il codice con l’archivio Adobe e consente di verificare le richieste pull prima di unirle ai rami principali. Questa funzionalità è esclusiva di GitHub pubblico. Il supporto per GitHub self-hosted non è disponibile.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a `Grp-CloudManager_BYOG@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID.

### Ripristino del contenuto self-service {#content-restore}

[Una nuova funzione di ripristino dei contenuti self-service](/help/operations/restore.md) ora fornisce il ripristino del backup per un massimo di sette giorni ed è disponibile per gli utenti iniziali che lo adottano a scopo di valutazione, con le seguenti caratteristiche:

* Ripristino del backup in un momento specifico per le 24 ore precedenti
* Ripristini a tempo fisso per un massimo di sette giorni

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `aemcs-restorefrombackup-adopter@adobe.com` dall’e-mail associata al tuo Adobe ID.

* Il programma di adozione anticipata è limitato solo agli ambienti di sviluppo.
* La disponibilità del programma per i primi utilizzatori di questa funzione è limitata.
* Questa funzione consente di ripristinare i contenuti eliminati accidentalmente e non è destinata al ripristino di emergenza.

### Dashboard di Experience Audit {#experience-audit-dashboard}

La [dashboard di Audit dell’esperienza di Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una vista dei trend dei punteggi delle prestazioni della pagina, oltre a insight e consigli per aiutarti a migliorarli. La funzione Audit dell’esperienza è inclusa come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi eseguirla su qualsiasi pagina web pubblica o che richiede l’autenticazione. Sono disponibili audit di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Ti interessa testare la nuova dashboard? Per iniziare, invia un’e-mail a `aem-lighthouse-pilot@adobe.com` dall’e-mail associata al tuo Adobe ID.

## Correzioni di bug {#bug-fixes}

* È stato corretto un bug che si verificava quando l’utente definiva una variabile `COMMERCE_ENDPOINT` con uno spazio finale, a causa del quale il Dispatcher non veniva caricato.
