---
title: Credenziali JWT nella console Adobe Developer obsolete
description: Informazioni sull’impatto della rimozione delle credenziali JWT in Adobe Developer Console su AEM
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 484ad9721b1b9da95cf3966f139c0f11ff6ea473
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 71%

---

# Credenziali JWT nella console Adobe Developer obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Per ulteriori informazioni, i clienti di AEM 6.5 dovrebbero fare riferimento a [questo articolo](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=it).

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. Non è possibile creare nuove credenziali dell’account di servizio (JWT) a partire dal 3 giugno 2024 e le credenziali JWT esistenti non funzioneranno il 27 gennaio 2025 o dopo tale data. È possibile [consultare le informazioni sull’’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come AEM as a Cloud Service dovrebbe gestire l’obsolescenza.

In questo momento, l’aspetto principale è che le funzionalità AEM non supportano ancora le nuove credenziali da server a server OAuth. Il supporto arriverà presto, entro la fine di aprile 2024 attraverso un rilascio dell’AEM per gli as a Cloud Service AEM. È possibile che sia stata ricevuta un’e-mail con le istruzioni per la migrazione delle credenziali JWT, ma occorre tenere presente che è possibile e si dovrebbe rimandare la migrazione delle credenziali fino a quando AEM non supporterà il nuovo tipo di credenziali da server a server OAuth.

Le sezioni seguenti elencano gli scenari in cui i clienti devono (o in alcuni casi non devono) sostituire le credenziali dell’account di servizio (JWT) con le credenziali server-to-server OAuth, una volta che l’AEM li ha supportati alla fine di aprile. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) sostituire le credenziali in futuro.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notare che la sigla **AEM** nella denominazione, che la distingue da **Adobe** Developer Console) fornisce un’utilità per generare [token JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzati per le API da server a server. Queste credenziali non sono obsolete e possono continuare a essere utilizzate.


## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: attendi di effettuare la migrazione dopo la fine di aprile 2024, quando l’AEM la supporterà (questo articolo verrà aggiornato in tale data)

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

L’interfaccia utente di authoring di AEM viene utilizzata per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio Adobe Target, Adobe Analytics, Adobe Launch, AFCS e molte altre.

![Integrazione di AEM con altre soluzioni](/help/security/assets/jwt-deprecation.png)

Ad esempio, ecco [le istruzioni](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=it) per configurare l’integrazione con Adobe Target. Chiave API in [Completamento della configurazione IMS in AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) deve essere migrata al tipo di credenziali server-to-server OAuth, una volta che AEM supporta tali credenziali alla fine di aprile. Le istruzioni verranno aggiornate e aggiornate alla fine di aprile per aiutarti ad applicare le nuove credenziali server-to-server OAuth.

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: attendi di migrare a dopo la fine di aprile 2024, quando l’AEM lo supporterà (questo articolo verrà aggiornato in tale data).

**Versioni di AEM pertinenti**: AEM as a Cloud Service

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È opportuno migrare le credenziali nel progetto Adobe Developer al tipo di credenziali da server a server OAuth, quando AEM e Cloud Manager ne forniranno il supporto.

## Progetti generati automaticamente {#autogen-projects}

**Azione**: non eseguire la migrazione perché se ne occuperà Adobe.

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

Quando Cloud Manager esegue il provisioning di ambienti AEM as a Cloud Service, genera automaticamente un progetto Adobe Developer Console con credenziali JWT. Questo progetto è contrassegnato come di sola lettura, come illustrato nella schermata seguente. Non è possibile e non si dovrebbe tentare di migrare questi progetti alle credenziali da server a server OAuth; al contrario, Adobe eseguirà la migrazione di questi progetti autonomamente, prima che le credenziali non siano più utilizzabili.

![Progetti generati automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
