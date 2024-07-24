---
title: Introduzione ai nomi di dominio personalizzati
description: L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1c9924b4477d53d86bb72eda8597a02304450195
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 58%

---


# Introduzione ai nomi di dominio personalizzati {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gestione dei nomi di dominio personalizzati"
>abstract="L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Aggiunta di un nome di dominio personalizzato"
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Visualizzazione e aggiornamento del nome di dominio personalizzato"

Adobe Experience Manager as a Cloud Service viene fornito con un nome di dominio predefinito, che termina con `*.adobeaemcloud.com`. Utilizzando l’interfaccia utente di Cloud Manager, puoi aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo. Il nome di dominio predefinito `*.adobeaemcloud.com` rimane, anche dopo aver associato i nomi di dominio personalizzati al sito Web.

## Che cosa sono i nomi di dominio personalizzati? {#what-are-custom-domain-names}

A ciascun sito web è associato un indirizzo numerico univoco in un formato leggibile al computer, ad esempio `184.33.123.64`. Il DNS (Domain Name System) è il sistema che consente di collegare domini personalizzati del marchio ai siti Web traducendo gli indirizzi numerici in indirizzi facili da ricordare come `wknd.com`.

È buona prassi disporre di un nome di dominio per il sito che sia memorabile per i clienti e rifletta il tuo marchio.

Il nome di dominio può essere acquistato da un registrar di nomi di dominio o da un’azienda o organizzazione che gestisce e vende nomi di dominio. I registrar di nomi di dominio gestiscono i nomi di dominio sui server DNS.

>[!IMPORTANT]
>
>Cloud Manager non è un registrar di nomi di dominio e non fornisce servizi DNS.

## Nomi di dominio personalizzati e CDN BYO {#byo-cdn}

AEM as a Cloud Service offre un servizio di rete per la distribuzione di contenuti (CDN) integrato, ma consente anche di usare una rete CDN personalizzata (BYO) con AEM. I domini personalizzati possono essere installati nella rete CDN gestita da AEM o in una rete CDN gestita dall’utente.

* I nomi di dominio personalizzati (e i certificati) installati nel CDN gestito da AEM vengono gestiti tramite Cloud Manager.
* I nomi di dominio personalizzati (e i certificati) installati nel tuo CDN sono gestiti in quel CDN specifico.

**I domini gestiti nella tua rete CDN non devono essere installati tramite Cloud Manager.** Vengono resi disponibili all&#39;AEM tramite X-Forwarded-Host e corrispondono ai vhosts definiti in Dispatcher. Consulta la [documentazione CDN.](/help/implementing/dispatcher/cdn.md)

In un ambiente è possibile installare entrambi i domini nel CDN gestito da AEM e installarli nel proprio CDN.

## Flusso di lavoro {#workflow}

L’aggiunta di un nome di dominio personalizzato richiede l’interazione tra il servizio DNS e Cloud Manager. Per questo motivo sono necessari diversi passaggi per installare, configurare e verificare i nomi di dominio personalizzati. La tabella seguente offre una panoramica dei passaggi necessari, inclusi i collegamenti alle risorse della documentazione per completare tali passaggi.

| Passaggio | Descrizione | Documentazione |
|---|---|---|
| 1 | Aggiungere un certificato SSL a Cloud Manager | [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Aggiungere un dominio personalizzato a Cloud Manager | [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | Aggiunta di un record TXT per verificare il dominio | [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 4 | Verifica stato del dominio | [Controllo dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | Configurazione delle impostazioni DNS tramite aggiunta dei record DNS CNAME o APEX che puntano a AEM as a Cloud Service | [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 6 | Verifica dello stato del record DNS | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>L’impostazione di nomi di dominio personalizzati con AEM as a Cloud Service è in genere un processo semplice. Tuttavia, a volte possono verificarsi problemi di delega del dominio la cui risoluzione può richiedere 1-2 giorni lavorativi. Per questo motivo, si consiglia vivamente di installare i domini con grande anticipo rispetto alla data di Go Live prevista. Per ulteriori informazioni, consulta il documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Limitazioni {#limitations}

L’utilizzo di nomi di dominio personalizzati con AEMaaCS presenta diverse limitazioni.

* I nomi di dominio personalizzati sono supportati in Cloud Manager solo per i servizi di pubblicazione e anteprima per i programmi Sites.
   * I domini personalizzati per i servizi di authoring non sono supportati.
* Ogni ambiente di Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati.
* Non è possibile aggiungere nomi di dominio agli ambienti se a questi è collegata una pipeline attualmente in esecuzione.
* Lo stesso nome di dominio non può essere utilizzato in più ambienti.
* È possibile aggiungere un solo nome di dominio alla volta.
* AEM as a Cloud Service non supporta i domini con caratteri jolly come `*.example.com`.
* Prima di aggiungere un nome di dominio personalizzato, è necessario installare un certificato SSL valido contenente il nome di dominio personalizzato (i certificati con caratteri jolly sono validi).

## Inizia! {#get-started}

* Inizia a configurare un nuovo nome di dominio personalizzato per il progetto [aggiungendo un certificato SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* Gestisci i tuoi nomi di dominio esistenti consultando il documento [Gestione dei nomi di dominio personalizzati.](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
