---
title: Note sulla versione 2023.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione 2023.11.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be38ca5bf79d401fc12c1422c270a2ee84bbbad2
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 25%

---


# Note sulla versione 2023.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.11.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager versione 2023.11.0 in AEM as a Cloud Service è il 14 novembre 2023. La prossima versione è pianificata per il 7 dicembre 2023.

## Novità {#what-is-new}

* La protezione WAF-DDOS (Web Application Firewall-DDOS) è ora disponibile per l&#39;acquisto come parte della licenza as a Cloud Service per l&#39;AEM e [può essere configurato in modo autonomo.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* Specializzato [configurare le pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) Sono ora disponibili per configurare e distribuire in pochi minuti le regole del filtro del traffico, incluse le regole WAF.
* [Durante la copia del contenuto](/help/implementing/developing/tools/content-copy.md) da un ambiente superiore a uno di sviluppo, ora viene visualizzato un messaggio che consiglia di prestare attenzione quando si copiano set di contenuti di grandi dimensioni, poiché gli ambienti di sviluppo hanno capacità limitata.
* [Pagina dei dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) ora mostra tutti i passaggi di un’esecuzione della pipeline con quelli non ancora avviati in grigio.
* Su entrambi **[Attività](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** e **[Pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** Quando si seleziona una pipeline con stato in esecuzione, è ora disponibile un riepilogo dell’esecuzione della pipeline.
* È stata aggiunta una nuova sezione **Durata** alla [pagina Dettagli della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details), che include la durata media del passaggio della pipeline in base alla tendenza storica per quel programma.
* Il giorno [pagina di esecuzione della pipeline,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) i passaggi completati ora visualizzano la durata.
* Esecuzioni che [riutilizzare gli artefatti di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) ora mostra il collegamento all’esecuzione che ha generato inizialmente tali artefatti.
* Opzione da selezionare **Errori di metriche importanti** può ora essere configurato per [pipeline di qualità del codice](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) anche.


## Programma per i primi utilizzatori {#early-adoption}

Per testare alcune delle prossime funzionalità, partecipa al programma di adozione anticipata di Adobe.

### Porta il tuo GitHub personale {#byo-github}

Se utilizzi GitHub per gestire gli archivi, [ora puoi convalidare il codice direttamente all’interno degli archivi GitHub tramite Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Questa integrazione elimina la necessità di sincronizzare in modo coerente il codice con l’archivio Adobe e consente di verificare le richieste pull prima di unirle ai rami principali.

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un’e-mail a `Grp-CloudManager_BYOG@adobe.com` dal tuo indirizzo e-mail associato al tuo Adobe ID.

### Autorizzazioni personalizzate {#custom-permissions}

[Autorizzazioni personalizzate di Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) consente di creare profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un’e-mail a `Grp-CloudManager-custom-permissions@adobe.com` dal tuo indirizzo e-mail associato al tuo Adobe ID.

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

## Problemi noti {#known-issues}

Esiste un bug noto che impedisce [configurare le pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) dall&#39;invio alla produzione.

Se il **Sospendi prima della distribuzione in produzione** per una pipeline di configurazione è necessaria l’opzione, di seguito è riportata la soluzione alternativa consigliata fino alla risoluzione del bug.

1. Eseguire la pipeline.
1. Verifica il codice nell’ambiente di staging.
1. Quando la distribuzione e l’approvazione diventano disponibili, fai clic su **Rifiuta**.
1. Modifica la pipeline in modo da poter disabilitare **Sospendi prima della distribuzione in produzione** opzione.
1. Esegui nuovamente la pipeline in modo che possa essere eseguita nuovamente nell’ambiente di staging e quindi in produzione.
