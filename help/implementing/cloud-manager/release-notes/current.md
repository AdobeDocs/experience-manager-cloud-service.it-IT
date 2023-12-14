---
title: Note sulla versione 2023.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.12.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 3e7d3113b25e9b4058130bf3352a612f36ef5c63
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 17%

---


# Note sulla versione 2023.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.12.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2023.12.0 in AEM as a Cloud Service è il 14 dicembre 2023. La prossima versione è prevista per il 18 gennaio 2024.

## Novità {#what-is-new}

* [Autorizzazioni personalizzate di Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) consente di creare profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.
   * Questa funzione verrà implementata in modo graduale, con il completamento previsto con la versione di Cloud Manager di febbraio 2024.
   * Invia un&#39;e-mail a `Grp-CloudManager-custom-permissions@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID, se desideri che venga attivato prima.
* I contenitori delle build ora supportano Node.js versione 18 per [pipeline front-end.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* Per i nuovi programmi di Cloud Manager, [l’account secondario New Relic associato](/help/implementing/cloud-manager/user-access-new-relic.md) non è attivato per impostazione predefinita.
   * Per i programmi esistenti in cui non si accede all’account secondario di New Relic da più di 90 giorni, questo verrà disattivato.
   * Se desideri utilizzare l’account secondario New Relic, devi fornire il consenso tramite Cloud Manager.
* Rollout delle versioni secondarie per Java 8 e 11 e aggiornamenti a maven [annunciato e iniziato con la versione di ottobre di Cloud Manager](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) sono state completate.
   * È stato aggiunto il supporto per il nodo 18 per le pipeline front-end e full-stack.
   * La versione secondaria di Java 8 è stata aggiornata a `jdk1.8.0_371`.
   * La versione secondaria di Java 11 è stata aggiornata a `jdk-11.0.20`.
   * È stato aggiunto il supporto per Java 17.
   * Maven è stato aggiornato alla versione 3.8.8
   * L’immagine base del contenitore della build è stata aggiornata a Ubuntu 22.04.

## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma di adozione anticipata di Adobe.

### Raccolta lato client tramite Real User Monitoring (RUM) {#rum}

Puoi sfruttare [Servizio dati di Real User Monitoring (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) per abilitare la raccolta lato client per AEM as a Cloud Service.

Real User Monitoring (RUM) Data Service offre un riflesso più preciso delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. È un’ottima opportunità per ottenere informazioni avanzate sulle prestazioni della pagina. Questa funzione è utile per i clienti che utilizzano una rete CDN gestita da Adobe o una rete CDN gestita da non Adobe. Per i clienti che utilizzano una rete CDN gestita non basata su Adobi, ora è possibile abilitare il reporting automatico del traffico, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `aemcs-rum-adopter@adobe.com` dall’indirizzo e-mail associato al tuo Adobe ID. Includi il nome di dominio per gli ambienti di produzione, staging e sviluppo nell’e-mail.  La disponibilità del programma di adozione anticipata di questa funzione è limitata.

### Porta il tuo GitHub personale {#byo-github}

Se utilizzi GitHub per gestire gli archivi, [ora puoi convalidare il codice direttamente all’interno degli archivi GitHub tramite Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Questa integrazione elimina la necessità di sincronizzare in modo coerente il codice con l’archivio Adobe e consente di verificare le richieste pull prima di unirle ai rami principali.

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un’e-mail a `Grp-CloudManager_BYOG@adobe.com` dal tuo indirizzo e-mail associato al tuo Adobe ID.

### Ripristino del contenuto self-service {#content-restore}

[Una nuova funzione di ripristino self-service dei contenuti](/help/operations/restore.md) ora fornisce il ripristino del backup per un massimo di sette giorni ed è disponibile per gli utenti che lo adottano per la valutazione, con:

* Ripristino del backup point-in-time per le 24 ore precedenti
* Ripristini a tempo fisso per un massimo di sette giorni

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un’e-mail a `aemcs-restorefrombackup-adopter@adobe.com` dall’e-mail associata al tuo Adobe ID.

* Il programma di adozione anticipata è limitato solo agli ambienti di sviluppo.
* La disponibilità del programma di adozione anticipata di questa funzione è limitata.
* Questa funzione consente di ripristinare i contenuti eliminati accidentalmente e non è destinata al disaster recovery.

### Dashboard di audit dell’esperienza {#experience-audit-dashboard}

[Dashboard di Cloud Manager Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una visualizzazione con tendenze dei punteggi di prestazioni della pagina, oltre a informazioni approfondite e consigli per aiutarti a migliorarli. L’audit dell’esperienza è incluso come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard utilizza Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi eseguirla su qualsiasi pagina web, pubblica o che richiede l’autenticazione. Sono disponibili controlli di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Ti interessa testare il nuovo cruscotto? Per iniziare, invia un’e-mail a `aem-lighthouse-pilot@adobe.com` dall’e-mail associata al tuo Adobe ID.
