---
title: Note sulla versione 2023.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.10.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b760b3a65d89b0b4f924379fc460015a58e2ed3e
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 19%

---


# Note sulla versione 2023.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.10.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2023.10.0 in AEM as a Cloud Service è il 5 ottobre 2023. La prossima versione è pianificata per il 2 novembre 2023.

## Novità {#what-is-new}

* Miglioramenti a [indicizzazione](/help/operations/indexing.md) hanno una durata della pipeline ridotta durante la distribuzione di nuovi indici.
   * I miglioramenti variano a seconda del profilo del contenuto.
* Automatico [aggiornamenti per gli ambienti di sviluppo](/help/implementing/cloud-manager/manage-environments.md#updating-environments) sono attivate per impostazione predefinita per i nuovi programmi, risparmiando tempo per eseguire gli aggiornamenti manualmente.
   * Questo aggiornamento verrà introdotto in modo graduale.
* Con la versione di ottobre 2023 di Cloud Manager, le versioni Java sono in fase di aggiornamento tramite un rollout graduale.
   * Le versioni secondarie di Java 8 e 11 e Maven sono state aggiornate e verranno implementate in modo graduale nei prossimi 2 mesi. La nuova versione include più correzioni di sicurezza e bug. Le nuove versioni sono:
   * *Maven: 3.8.8*
   * *Java 8 versione: /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11 versione: /usr/lib/jvm/jdk-11.0.20*
   * [Consulta l’avviso OpenJDK](https://openjdk.org/groups/vulnerability/advisories/) per informazioni dettagliate sulla sicurezza e sui bug risolti in questi aggiornamenti JDK.

## Programma di adozione anticipata {#early-adoption}

Partecipa al nostro programma di adozione anticipata e hai la possibilità di testare alcune delle prossime funzionalità.

### Autorizzazioni personalizzate {#custom-permissions}

[Autorizzazioni personalizzate di Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) consente di creare nuovi profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.

se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un messaggio e-mail `Grp-CloudManager-custom-permissions@adobe.com` dal tuo indirizzo e-mail associato al tuo Adobe ID.

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
