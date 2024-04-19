---
title: Introduzione ai nomi di dominio personalizzati
description: L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: d9cd10772252d80487f578ee73f40ec334600029
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 83%

---


# Introduzione ai nomi di dominio personalizzati {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gestione dei nomi di dominio personalizzati"
>abstract="L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Aggiunta di un nome di dominio personalizzato"
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Visualizzazione e aggiornamento del nome di dominio personalizzato"

L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo. Adobe Experience Manager as a Cloud Service viene fornito con un nome di dominio predefinito, che termina con `*.adobeaemcloud.com`. Questo nome di dominio predefinito viene conservato anche dopo aver associato i nomi di dominio personalizzati al sito web.

## Che cosa sono i nomi di dominio personalizzati? {#what-are-custom-domain-names}

A ciascun sito web è associato un indirizzo numerico univoco in un formato leggibile al computer, ad esempio `184.33.123.64`. Il DNS (Domain Name System) è il sistema che consente di collegare domini personalizzati del marchio ai siti web traducendo gli indirizzi numerici in indirizzi facili da ricordare come `wknd.com`.

È buona prassi scegliere per il sito un nome di dominio che sia facile da ricordare per la clientela e che rispecchi il marchio.

Il nome di dominio può essere acquistato da un registrar di nomi di dominio o da un’azienda o organizzazione che gestisce e vende nomi di dominio. I registrar di nomi di dominio gestiscono i nomi di dominio sui server DNS.

>[!IMPORTANT]
>
>Cloud Manager non è un registrar di nomi di dominio e non fornisce servizi DNS.

## Nomi di dominio personalizzati e CDN BYO {#byo-cdn}

AEM as a Cloud Service offre un servizio integrato di rete per la distribuzione di contenuti (CDN), ma consente anche di usare una rete CDN personalizzata (BYO) con AEM. I domini personalizzati possono essere installati nella rete CDN gestita da AEM o in una rete CDN gestita dall’utente.

* I nomi di dominio personalizzati (e i certificati) installati nel CDN gestito da AEM vengono gestiti tramite Cloud Manager.
* I nomi di dominio personalizzati (e i certificati) installati nel tuo CDN sono gestiti in quel CDN specifico.

I domini gestiti nel tuo CDN non devono essere installati tramite Cloud Manager. Vengono resi disponibili per AEM tramite X-Forwarded-Host e corrispondono agli host definiti nel Dispatcher. Consulta la [documentazione CDN](/help/implementing/dispatcher/cdn.md).

In un ambiente è possibile installare entrambi i domini nel CDN gestito da AEM e installarli nel proprio CDN.

## Flusso di lavoro {#workflow}

L’aggiunta di un nome di dominio personalizzato richiede l’interazione tra il servizio DNS e Cloud Manager. Per questo motivo sono necessari diversi passaggi per installare, configurare e verificare i nomi di dominio personalizzati. La tabella seguente fornisce una panoramica dei passaggi necessari, tra cui le operazioni da eseguire quando si verificano errori comuni.

| Passaggio | Descrizione | Responsabilità | Ulteriori informazioni |
|--- |--- |--- |---|
| 1 | Aggiungere un certificato SSL a Cloud Manager | Cliente | [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Aggiunta di un record TXT per verificare il dominio | Cliente | [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Revisione dello stato di verifica del dominio | Cliente | [Controllo dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | Se la verifica del dominio non va a buon fine e riporta lo stato `Domain Verification Failure` | Cliente | [Controllo dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Se la verifica del dominio non va a buon fine e riporta lo stato `Verified, Deployment Failed`, contatta Adobe | Assistenza clienti Adobe | [Controllo dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Configurazione delle impostazioni DNS tramite aggiunta dei record DNS CNAME o APEX che puntano a AEM as a Cloud Service | Cliente | [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Verifica dello stato del record DNS | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | Se lo stato del record DNS non va a buon fine e mostra l’errore `DNS status not detected` | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Se lo stato del record DNS non va a buon fine e mostra l’errore `DNS resolves incorrectly` | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>L’impostazione di nomi di dominio personalizzati con AEM as a Cloud Service è in genere un processo semplice. Tuttavia, a volte possono verificarsi problemi di delega del dominio la cui risoluzione può richiedere 1-2 giorni lavorativi. Per questo motivo, si consiglia vivamente di installare i domini con grande anticipo rispetto alla data di Go Live prevista. Per ulteriori informazioni, consulta il documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Limitazioni {#limitations}

L’utilizzo di nomi di dominio personalizzati con AEMaaCS presenta diverse limitazioni.

* I nomi di dominio personalizzati sono supportati in Cloud Manager per entrambi i servizi di publicazione e anteprima dei programmi Sites. I domini personalizzati per i servizi di authoring non sono supportati.
* Ogni ambiente di Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati.
* Non è possibile aggiungere nomi di dominio agli ambienti se a essi è collegata una pipeline attualmente in esecuzione.
* Impossibile utilizzare lo stesso nome di dominio in più ambienti.
* È possibile aggiungere un solo nome di dominio alla volta.
* AEM as a Cloud Service non supporta i domini con caratteri jolly come `*.example.com`.
* Prima di aggiungere un nome di dominio personalizzato, è necessario installare un certificato SSL valido contenente il nome di dominio personalizzato del programma (i certificati wildcard sono validi). Per ulteriori informazioni, consulta [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
