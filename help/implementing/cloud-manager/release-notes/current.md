---
title: Note sulla versione 2024.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2024.1.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 06f534e6541bd04e005f3acf1edbb3e372c1cd0d
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 20%

---


# Note sulla versione 2024.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.1.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.1.0 in AEM as a Cloud Service è il 18 gennaio 2024. La prossima versione è prevista per il 16 febbraio 2024.

## Novità {#what-is-new}

* Cloud Manager ora convalida le date di scadenza non solo per il [certificato,](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) ma anche per i certificati intermedi.
* CDN [registri](/help/implementing/cloud-manager/manage-logs.md) vengono ora restituiti in formato compresso.

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

## Correzioni di bug {#bug-fixes}

* È stato corretto un errore a causa del quale le pipeline di configurazione non riuscivano nella fase di build con un messaggio di errore non chiaro se il percorso dei file di configurazione non era impostato correttamente. Il messaggio di errore è ora chiaro e indica che l’utente deve verificare che il percorso dei file di configurazione sia corretto.
* Quando un passaggio della build termina con lo stato `FAILED` a causa di un `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR`, ora è descritto correttamente come un errore dovuto a conflitti di unione con il ramo di destinazione.
