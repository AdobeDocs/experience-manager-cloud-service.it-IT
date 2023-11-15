---
title: Note sulla versione 2023.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.11.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 3a9eaa162d62cd3e674f14ba39ed7c96ad271f79
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 13%

---


# Note sulla versione 2023.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.11.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager versione 2023.11.0 in AEM as a Cloud Service è il 14 novembre 2023. La prossima versione è prevista per il 7 dicembre 2023.

## Novità {#what-is-new}

* La protezione WAF-DDOS (Web Application Firewall-DDOS Protection) è ora disponibile per l&#39;acquisto come parte dei diritti as a Cloud Service AEM e [può essere configurato in modo autonomo.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* Specializzato [configurare le pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) Sono ora disponibili per configurare le impostazioni dell’ambiente, le attività di manutenzione, le regole CDN e altro in pochi minuti.
* [Durante la copia del contenuto](/help/implementing/developing/tools/content-copy.md) da un ambiente superiore a uno di sviluppo, ora viene visualizzato un messaggio che consiglia di prestare attenzione quando si copiano set di contenuti di grandi dimensioni, poiché gli ambienti di sviluppo hanno capacità limitata.
* [Pagina dei dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) mostrerà ora tutti i passaggi di un’esecuzione della pipeline con quelli non ancora avviati disattivati.
* Su entrambi **[Attività](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** e **[Pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** Quando si fa clic su una pipeline con stato in esecuzione, è ora disponibile un riepilogo dell’esecuzione della pipeline.
* Una nuova **Durata** è stata aggiunta alla sezione [pagina dei dettagli della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) che include la durata media del passaggio della pipeline in base alla tendenza storica per quel programma.
* Il giorno [pagina di esecuzione della pipeline,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) i passaggi completati ora visualizzano la durata.
* Esecuzioni che [riutilizzare gli artefatti di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) mostrerà ora il collegamento all’esecuzione che ha inizialmente creato tali artefatti.
* Opzione da selezionare **Errori di metriche importanti** può ora essere configurato per [pipeline di qualità del codice](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) anche.


## Programma di adozione anticipata {#early-adoption}

Partecipa al nostro programma di adozione anticipata e hai la possibilità di testare alcune delle prossime funzionalità.

### GitHub personalizzato {#byo-github}

Se utilizzi GitHub per gestire gli archivi, [ora puoi convalidare il codice direttamente all’interno degli archivi GitHub tramite Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Questa integrazione elimina la necessità di sincronizzare in modo coerente il codice con l’archivio Adobe e consente di verificare le richieste pull prima di unirle ai rami principali.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un’e-mail a `Grp-CloudManager_BYOG@adobe.com` dal tuo indirizzo e-mail associato al tuo Adobe ID.

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

## Problemi noti {#known-issues}

Esiste un bug noto che impedisce [configurare le pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) dall&#39;invio alla produzione.

Se il **Sospendi prima della distribuzione in produzione** per una pipeline di configurazione è necessaria l’opzione, di seguito è riportata la soluzione alternativa consigliata fino alla risoluzione del bug.

1. Eseguire la pipeline.
1. Verifica il codice nell’ambiente di staging.
1. Quando la distribuzione e l’approvazione diventano disponibili, fai clic su **Rifiuta**.
1. Modifica la pipeline per disabilitare **Sospendi prima della distribuzione in produzione** opzione.
1. Esegui nuovamente la pipeline. Verrà eseguito nuovamente sullo staging e quindi sulla produzione.
