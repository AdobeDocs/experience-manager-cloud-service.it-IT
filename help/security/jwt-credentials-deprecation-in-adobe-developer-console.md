---
title: Deprecazione delle credenziali JWT nella console Adobe Developer
description: Scopri l’impatto della rimozione delle credenziali JWT nella console Adobe Developer sull’AEM
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Deprecazione delle credenziali JWT nella console Adobe Developer {#jwt-credentials-deprecation-in-adobe-developer-console}

Adobe utilizzato dai clienti [Console Adobe Developer](https://developer.adobe.com/console) per generare credenziali che consentano l’accesso a varie API. I clienti possono scegliere tra vari tipi di credenziali, da OAuth Server-to-Server a Single-Page App. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali server-to-server OAuth. Non è possibile creare nuove credenziali dell’account di servizio (JWT) a partire dal 1° maggio 2024 e le credenziali JWT esistenti non funzioneranno a partire dal 1° gennaio 2025. È possibile [leggi informazioni sull’elemento obsoleto](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come i clienti AEM as a Cloud Service e AEM 6.5 devono gestire la rimozione.

L’aspetto principale di questo momento è che le funzionalità AEM non supportano ancora le nuove credenziali server-to-server di OAuth. Il supporto sarà presto disponibile: entro la metà di aprile 2024 tramite una versione AEM per AEM as a Cloud Service e attraverso uno speciale pacchetto di compatibilità da installare per AEM 6.5, se si sta eseguendo il Service Pack 20 più recente o inferiore (Service Pack 21 e versioni successive lo includeranno automaticamente). È possibile che tu abbia ricevuto un’e-mail con le istruzioni per la migrazione delle credenziali JWT, ma tieni presente che puoi e devi rimandare la migrazione delle credenziali fino a quando l’AEM non supporterà il nuovo tipo di credenziali server-to-server OAuth.

Le sezioni seguenti elencano gli scenari in cui i clienti devono (o in alcuni casi non devono) sostituire le credenziali dell’account di servizio (JWT) con le credenziali server-to-server OAuth, una volta che l’AEM li ha supportati a metà aprile. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) per sostituire le credenziali in futuro.

>[!NOTE]
>
>Il [**AEM** Console per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (nota le **AEM** nella denominazione, che la distingue dalla denominazione **Adobe** Developer Console) fornisce un’utility per generare [Token JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzato per le API server-to-server. Queste credenziali non sono obsolete e possono continuare a essere utilizzate.


## Integrazione dell’AEM con altre soluzioni Adobi {#integrating-aem-with-other-adobe-solutions}

**Azione**: attendi di migrare fino a dopo metà aprile 2024, quando l’AEM lo supporterà.

**Versioni pertinenti dell’AEM**: AEM as a Cloud Service e Adobe Managed Services (Service Pack 20 e versioni successive).


I clienti AEM utilizzano l’interfaccia utente di creazione dell’AEM per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio Adobe Target, Adobe Analytics, Adobe Launch, AFCS e molti altri.

![Integrazione dell’AEM con altre soluzioni](/help/security/assets/jwt-deprecation.png)

Ad esempio, ecco [le istruzioni](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) per configurare l’integrazione con Adobe Target. Chiave API in [Completamento della configurazione IMS in AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) deve essere migrata al tipo di credenziali server-to-server OAuth, una volta che AEM supporta tali credenziali a metà aprile. Le istruzioni verranno aggiornate e aggiornate a metà aprile, per aiutarti ad applicare le nuove credenziali server-to-server OAuth.

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: attendi di migrare fino a dopo metà aprile 2024, quando l’AEM lo supporterà.

**Versioni pertinenti dell’AEM**: AEM as a Cloud Service e Adobe Managed Services (Service Pack 20 e versioni successive).

I clienti creano progetti della console Adobe Developer in modo che possano richiamare [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È necessario migrare le credenziali nel progetto Adobe Developer al tipo di credenziali server-to-server OAuth, una volta supportato da AEM e Cloud Manager.

## Progetti generati automaticamente {#autogen-projects}

**Azione**: non eseguire la migrazione perché Adobe eseguirà la migrazione per tuo conto.

**Versioni pertinenti dell’AEM**: Solo AEM as a Cloud Service.

Quando Cloud Manager esegue il provisioning di ambienti AEM as a Cloud Service, genera automaticamente un progetto Adobe Developer Console con credenziali JWT. Questo progetto è contrassegnato come di sola lettura, come illustrato nella schermata seguente. I clienti non possono e non devono tentare di migrare questi progetti alle credenziali da server a server OAuth; al contrario, Adobe eseguirà la migrazione di questi progetti da solo, prima che le credenziali non siano più utilizzabili.

![Progetti generati automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)

