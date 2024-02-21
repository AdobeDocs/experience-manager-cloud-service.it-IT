---
title: Note sulla versione 2024.2.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2024.2.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4a41de9da557be562bb2ff5773c7954f76a9acc7
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 97%

---


# Note sulla versione 2024.2.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.2.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.2.0 in AEM as a Cloud Service è il 15 febbraio 2024. La prossima versione è prevista per il 16 marzo 2024.

## Novità {#what-is-new}

* Cloud Manager ora supporta la gestione in autonomia di [variabili della pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) tramite l’interfaccia utente di Cloud Manager.
* [Il servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-sevice) verrà ora abilitato per gli ambienti creati prima dell’implementazione della funzione del servizio di anteprima.
* Le [autorizzazioni personalizzate di Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) consentono di creare profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.
   * Questa funzione è stata implementata in modo graduale con la [versione di dicembre 2023](/help/implementing/cloud-manager/release-notes/2023/2023-12-0.md) e sarà completata il 20 febbraio 2024.
* Per tutti i nuovi ambienti, i nomi del [profilo di prodotto ambiente](/help/onboarding/aem-cs-team-product-profiles.md) avranno un formato più intuitivo basato su una combinazione di descrizione del profilo, tipo di ambiente, numero e numero di programma.
* [L’ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) è stato aggiornato alle versioni Maven 3.9.4 e JDK jdk-11.0.22 e jdk1.8.0_401.

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

* Il JDK dei contenitori di build è stato aggiornato a una versione che risolve [JDK-8313765.](https://bugs.openjdk.org/browse/JDK-8313765)
