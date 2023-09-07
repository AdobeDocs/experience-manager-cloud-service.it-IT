---
title: Note sulla versione 2023.9.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.9.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
source-git-commit: dd52aef2f88cf64e8d9a32b1c8cafe4fcfbcb812
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 24%

---


# Note sulla versione 2023.9.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.9.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2023.9.0 di Cloud Manager in AEM as a Cloud Service è l’7 settembre 2023. La prossima versione è prevista per il 5 ottobre 2023.

## Novità {#what-is-new}

Questa versione si concentra sulle correzioni di bug.

## Programma di adozione anticipata {#early-adoption}

Partecipa al nostro programma di adozione anticipata e hai la possibilità di testare alcune delle prossime funzionalità.

### Ripristino del contenuto self-service {#content-restore}

[Una nuova funzione di ripristino self-service dei contenuti](/help/operations/restore.md) ora fornisce il ripristino del backup per un massimo di sette giorni ed è disponibile per gli utenti che lo adottano per la valutazione, con:

* Ripristino del backup point-in-time per le 24 ore precedenti
* Ripristini a tempo fisso per un massimo di sette giorni

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `aemcs-restorefrombackup-adopter@adobe.com` dall’e-mail associata al tuo Adobe ID. Nota:

* Il programma di adozione anticipata è limitato solo agli ambienti di sviluppo.
* La disponibilità del programma di adozione anticipata di questa funzione è limitata.
* Questa funzione consente di ripristinare i contenuti eliminati accidentalmente e non è destinata al disaster recovery.

### Dashboard di audit dell’esperienza {#experience-audit-dashboard}

[Dashboard di Cloud Manager Experience Audit](/help/implementing/cloud-manager/experience-audit-dashboard.md) include una visualizzazione con tendenze dei punteggi di prestazioni della pagina, oltre a informazioni approfondite e consigli per aiutarti a migliorarli. L’audit dell’esperienza è incluso come passaggio nella pipeline di produzione di Cloud Manager.

La dashboard sfrutta Google Lighthouse, uno strumento open-source automatizzato per migliorare la qualità delle app web. Puoi eseguirla su qualsiasi pagina web, pubblica o che richiede l’autenticazione. Sono disponibili controlli di prestazioni, accessibilità, applicazioni web progressive, SEO e altro ancora.

Ti interessa testare il nuovo cruscotto? Invia un&#39;e-mail a `aem-lighthouse-pilot@adobe.com` dall’e-mail associata al tuo Adobe ID per iniziare.

## Correzioni di bug {#bug-fixes}

* Quando un programma viene eliminato, viene eliminata anche qualsiasi pipeline in esecuzione associata, garantendo che la pipeline non venga erroneamente designata come stato di errore.
* Talvolta, quando tutti i passaggi di un’esecuzione della pipeline sono &quot;completati&quot;, lo stato della pipeline viene visualizzato come &quot;in esecuzione&quot;, facendola sembrare in uno stato bloccato. Ora viene visualizzato come &#39;Completo&#39;.
* Per i rami dell’archivio generati utilizzando l’archetipo del generatore di codice, la pipeline CI/CD non riesce.
