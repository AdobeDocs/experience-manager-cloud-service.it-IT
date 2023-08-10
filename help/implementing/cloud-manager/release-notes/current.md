---
title: Note sulla versione 2023.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.8.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: d1640c14c796d7b7b6a7b236b38077e360559966
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 27%

---


# Note sulla versione 2023.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.8.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2023.8.0 in AEM as a Cloud Service è l’10 agosto 2023. La versione successiva è pianificata per il 7 settembre 2023.

## Novità {#what-is-new}

* Durante la configurazione di un set di contenuti su [copiare il contenuto,](/help/implementing/developing/tools/content-copy.md) [configurazioni in base al contesto](/help/implementing/developing/introduction/configurations.md) sono ora consentiti nei set di contenuti dell’interfaccia utente.
* Sono stati apportati miglioramenti per migliorare la comprensibilità e la visualizzazione dei messaggi di errore nell’interfaccia utente di Cloud Manager.

## Programma di adozione anticipata per il ripristino dei contenuti self-service {#early-adoption}

[Una nuova funzione di ripristino self-service dei contenuti](/help/operations/restore.md) ora fornisce il ripristino del backup per un massimo di sette giorni ed è disponibile per gli utenti che lo adottano per la valutazione, con:

* Ripristino del backup point-in-time per le 24 ore precedenti
* Ripristini a tempo fisso per un massimo di sette giorni

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `aemcs-restorefrombackup-adopter@adobe.com` dall’e-mail associata al tuo Adobe ID. Nota:

* Il programma di adozione anticipata è limitato solo agli ambienti di sviluppo.
* La disponibilità del programma di adozione anticipata è limitata.
* Questa funzione consente di ripristinare i contenuti eliminati accidentalmente e non è destinata al disaster recovery.

## Correzioni di bug {#bug-fixes}

* Il **Ambienti** Il menu ora si chiude dopo aver attivato **[Copia contenuto](/help/implementing/developing/tools/content-copy.md)** modale.
* [Una riesecuzione della pipeline](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) non è più consentito se l’esecuzione precedente non ha un `commitId` impostato sullo stato della fase di build.
* Ora quando un utente fa clic su una pipeline in viene visualizzato un messaggio più comprensibile per i rari errori **Attività** o **Pipeline** schermi.
* Il `contentSetName` il valore non è più mancante nei registri ed è ora fornito negli input quando si avvia un [copia contenuto](/help/implementing/developing/tools/content-copy.md) operazione.
* In alcune rare circostanze non è più possibile avviare due esecuzioni dalla stessa pipeline portando a uno stato &quot;bloccato&quot;.
* Alla scadenza di un certificato, i nomi di dominio e gli elenchi IP consentiti associati al certificato non verranno più rimossi dalla rete CDN.
   * In questi casi, il sito continuerà ad essere raggiungibile.
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)L’interfaccia utente di Cloud Manager fornisce avvisi anticipati più visibili relativi al Certificato SSL che sta per scadere.
* È stato risolto un problema che causava la perdita dell’accesso AEM a un endpoint di pubblicazione nelle situazioni in cui Sites veniva aggiunto come soluzione a un programma per sole risorse.
