---
title: Credenziali JWT in Adobe Developer Console obsolete
description: Ulteriori informazioni sull’impatto della rimozione delle credenziali JWT in Adobe Developer Console su AEM.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b6e26ecaa73aaee37b6b824426dc0cd65d459502
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 62%

---

# Credenziali JWT in Adobe Developer Console obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Per ulteriori informazioni, i clienti di AEM 6.5 dovrebbero fare riferimento a [questo articolo](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console).

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. A partire dal 3 giugno 2024, non sarà possibile creare nuove credenziali dell’account di servizio (JWT) e, a partire dal 27 gennaio 2025, le credenziali JWT esistenti non funzioneranno. È possibile [consultare le informazioni sull’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come AEM as a Cloud Service dovrebbe gestire l’obsolescenza.

L’aspetto principale è che AEM ora supporta le nuove credenziali server-to-server OAuth per AEM as a Cloud Service. È possibile che tu abbia ricevuto un’e-mail con le istruzioni per la migrazione delle credenziali JWT. È ora possibile eseguire questa migrazione.

Le sezioni seguenti elencano gli scenari in cui i clienti devono (o in alcuni casi non devono) sostituire le credenziali dell’account di servizio (JWT) con le credenziali server-to-server OAuth, ora che l’AEM li supporta. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) per migrare le credenziali.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notare che la sigla **AEM** nella denominazione, che la distingue da **Adobe** Developer Console) fornisce un’utilità per generare [token JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzati per le API da server a server. Queste credenziali non sono obsolete e possono continuare a essere utilizzate.

## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: esegui la migrazione della configurazione in quanto AEM ora supporta le credenziali OAuth.

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

I clienti AEM utilizzano l’AEM per configurare le integrazioni con molte altre soluzioni Adobi. Ad esempio, Adobe Target, Adobe Analytics e altri.

Consulta [Configurazione delle integrazioni IMS per AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) per informazioni dettagliate su come:

* creare configurazioni con le credenziali OAuth
* esegui la migrazione delle configurazioni create con credenziali JWT per utilizzare le credenziali OAuth

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: conferma quando è possibile migrare questi elementi da JWT a credenziali OAuth.

**Versioni di AEM pertinenti**: AEM as a Cloud Service

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È opportuno migrare le credenziali nel progetto Adobe Developer al tipo di credenziali da server a server OAuth, primna della scadenza del tipo di credenziali obsolete JWT, che non ci saranno più da gennaio.

## Progetti generati automaticamente {#autogen-projects}

**Azione**: non eseguire la migrazione perché se ne occuperà Adobe.

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

Quando Cloud Manager esegue il provisioning di ambienti AEM as a Cloud Service, genera automaticamente un progetto Adobe Developer Console con credenziali JWT. Questo progetto è contrassegnato come di sola lettura, come illustrato nella schermata seguente. I clienti non possono e non devono tentare di migrare questi progetti alle credenziali da server a server OAuth. Adobe, invece, eseguirà la migrazione di questi progetti da solo, prima che le credenziali non siano più utilizzabili.

![Progetti generati automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
