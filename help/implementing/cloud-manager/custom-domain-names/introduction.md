---
title: Introduzione ai nomi di dominio personalizzati
description: L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f1e9b76742c8d97f44ff974fb8686fdcb3d804e6
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 37%

---


# Introduzione ai nomi di dominio personalizzati {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gestione dei nomi di dominio personalizzati"
>abstract="L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/custom-domain-names/add-custom-domain-name" text="Aggiunta di un nome di dominio personalizzato"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/cicd-pipelines/custom-domain-names/managing-custom-domain-names" text="Visualizzazione e aggiornamento del nome di dominio personalizzato"

Adobe Experience Manager as a Cloud Service viene fornito con un nome di dominio predefinito, che termina con `*.adobeaemcloud.com`. Utilizzando l’interfaccia utente di Cloud Manager, puoi aggiungere un dominio personalizzato per identificare il sito con un nome univoco e personalizzato in modo autonomo. Il nome di dominio predefinito `*.adobeaemcloud.com` rimane, anche dopo aver associato i nomi di dominio personalizzati al sito Web.

## Cosa sono i nomi di dominio personalizzati? {#what-are-custom-domain-names}

A ciascun sito web è associato un indirizzo numerico univoco in un formato leggibile al computer, ad esempio `184.33.123.64`. Il DNS (Domain Name System) è il sistema che consente di collegare domini personalizzati del marchio ai siti Web traducendo gli indirizzi numerici in indirizzi facili da ricordare come `wknd.com`.

È buona prassi disporre di un nome di dominio per il sito che sia memorabile per i clienti e rifletta il tuo marchio.

Il nome di dominio può essere acquistato da un registrar di nomi di dominio o da un’azienda o organizzazione che gestisce e vende nomi di dominio. I registrar di nomi di dominio gestiscono i nomi di dominio sui server DNS.

>[!IMPORTANT]
>
>Cloud Manager non è un registrar di nomi di dominio e non fornisce servizi DNS.

## Personalizzare i nomi di dominio e creare una propria rete CDN {#byo-cdn}

AEM as a Cloud Service offre un servizio CDN (Content Delivery Network) integrato, ma consente anche di utilizzare la rete CDN BYO (Bring Your Own) con AEM. I domini personalizzati possono essere installati nella rete CDN gestita da AEM o in una rete CDN gestita dall’utente.

* Cloud Manager gestisce i nomi di dominio personalizzati e i certificati installati nella rete CDN gestita da AEM.
* I nomi di dominio personalizzati e i certificati installati in una rete CDN BYO vengono gestiti direttamente all’interno di tale rete CDN.

**I domini gestiti nella tua rete CDN non richiedono l&#39;installazione tramite Cloud Manager**. Vengono resi disponibili ad AEM tramite X-Forwarded-Host e corrispondono ai vhost definiti in Dispatcher. Consulta la [documentazione CDN](/help/implementing/dispatcher/cdn.md).

In un ambiente è possibile installare entrambi i domini nella rete CDN gestita da AEM e in una rete CDN BYO.

## Flusso di lavoro {#workflow}

L’aggiunta di un nome di dominio personalizzato richiede l’interazione tra il servizio DNS e Cloud Manager. A causa di questo flusso di lavoro, sono necessari diversi passaggi per installare, configurare e verificare i nomi di dominio personalizzati. La tabella seguente illustra i passaggi necessari, con collegamenti alle risorse della documentazione per completare tali passaggi.

>[!WARNING]
>
>Eseguire il passaggio 4 (configurare DNS) *solo dopo* il passaggio 3 (aggiungere la mappatura del dominio) è stato completato. In base a questo ordine, il dominio viene registrato con la rete CDN di Adobe e viene impostato il routing corretto, proteggendo il sito dalle acquisizioni del dominio.

| Passaggio | Descrizione |
| --- | --- |
| 1 | [Aggiungi certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | [Aggiungi un dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | [Aggiungi mapping di dominio](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | [Configura DNS](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#config-dns) |
| 5 | [Verifica stato DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>L’impostazione di nomi di dominio personalizzati con AEM as a Cloud Service è in genere un processo semplice. Tuttavia, a volte possono verificarsi problemi di delega del dominio la cui risoluzione può richiedere 1-2 giorni lavorativi. Per questo motivo, si consiglia di installare i domini molto prima della loro data di Go Live. Per ulteriori informazioni, vedere il documento [Verifica stato nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Note sull’utilizzo {#usage-notes}

* I nomi di dominio personalizzati sono supportati in Cloud Manager solo per i servizi di pubblicazione e anteprima per i programmi Sites.
   * I domini personalizzati per i servizi di authoring non sono supportati.
* Ogni ambiente di Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati.
* Non è possibile aggiungere nomi di dominio agli ambienti se a questi è collegata una pipeline attualmente in esecuzione.
* Lo stesso nome di dominio non può essere utilizzato in più ambienti.
* È possibile aggiungere un solo nome di dominio alla volta.
* AEM as a Cloud Service non supporta i domini con caratteri jolly come `*.example.com`.
* Prima di aggiungere un nome di dominio personalizzato, è necessario installare un certificato SSL valido contenente il nome di dominio personalizzato (i certificati con caratteri jolly sono validi).
* Sono necessari ulteriori passaggi di configurazione per utilizzare un nome di dominio personalizzato con [la funzionalità pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md#custom-domains).

## Introduzione {#get-started}

* Inizia a configurare un nuovo nome di dominio personalizzato per il progetto [aggiungendo un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Gestisci i tuoi nomi di dominio esistenti consultando il documento [Gestisci nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
