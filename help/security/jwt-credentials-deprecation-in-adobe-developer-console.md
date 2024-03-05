---
title: Credenziali JWT nella console Adobe Developer obsolete
description: Informazioni sull’impatto della rimozione delle credenziali JWT in Adobe Developer Console su AEM
source-git-commit: a354786f1ddfe50b01def85d3c83da09c6a35d2f
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 86%

---


# Credenziali JWT nella console Adobe Developer obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>I clienti di AEM as a Cloud Service devono fare riferimento a [questo articolo](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) per ulteriori informazioni.

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. A partire dal 1° maggio 2024, non sarà possibile creare nuove credenziali dell’account di servizio (JWT) e, a partire dal 1° gennaio 2025, le credenziali JWT esistenti non funzioneranno. È possibile [consultare le informazioni sull’’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come AEM as a Cloud Service dovrebbe gestire la rimozione.

In questo momento, l’aspetto principale è che le funzionalità AEM non supportano ancora le nuove credenziali da server a server OAuth. Il supporto arriverà presto, entro la metà di aprile 2024 attraverso una versione AEM per AEM as a Cloud Service. È possibile che sia stata ricevuta un’e-mail con le istruzioni per la migrazione delle credenziali JWT, ma occorre tenere presente che è possibile e si dovrebbe rimandare la migrazione delle credenziali fino a quando AEM non supporterà il nuovo tipo di credenziali da server a server OAuth.

Le sezioni seguenti elencano gli scenari in cui si deve (o in alcuni casi non si deve) sostituire le credenziali dell’account di servizio (JWT) con le credenziali da server a server OAuth, quando AEM fornirà il supporto a metà aprile. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) sostituire le credenziali in futuro.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notare che la sigla **AEM** nella denominazione, che la distingue da **Adobe** Developer Console) fornisce un’utilità per generare [token JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzati per le API da server a server. Queste credenziali non sono obsolete e possono continuare a essere utilizzate.


## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: posticipare la migrazione a dopo metà aprile 2024, quando AEM fornirà il supporto.

**Versioni pertinenti dell’AEM**: AEM AS A CLOUD SERVICE

L’interfaccia utente di authoring di AEM viene utilizzata per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio Adobe Target, Adobe Analytics, Adobe Launch, AFCS e molte altre.

![Integrazione di AEM con altre soluzioni](/help/security/assets/jwt-deprecation.png)

Ad esempio, ecco [le istruzioni](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=it) per configurare l’integrazione con Adobe Target. La chiave API nella sezione [Completamento della configurazione IMS in AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) deve essere migrata al tipo di credenziali da server a server OAuth, quando AEM ne fornirà il supporto a metà aprile. Per aiutare ad applicare le nuove credenziali da server a server OAuth, tali istruzioni verranno aggiornate e riviste a metà aprile.

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: posticipare la migrazione a dopo metà aprile 2024, quando AEM fornirà il supporto.

**Versioni pertinenti dell’AEM**: AEM AS A CLOUD SERVICE

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È opportuno migrare le credenziali nel progetto Adobe Developer al tipo di credenziali da server a server OAuth, quando AEM e Cloud Manager ne forniranno il supporto.

## Progetti generati automaticamente {#autogen-projects}

**Azione**: non eseguire la migrazione perché se ne occuperà Adobe.

**Versioni pertinenti dell’AEM**: AEM as a Cloud Service.

Quando Cloud Manager esegue il provisioning di ambienti AEM as a Cloud Service, genera automaticamente un progetto Adobe Developer Console con credenziali JWT. Questo progetto è contrassegnato come di sola lettura, come illustrato nella schermata seguente. Non è possibile e non si dovrebbe tentare di migrare questi progetti alle credenziali da server a server OAuth; al contrario, Adobe eseguirà la migrazione di questi progetti autonomamente, prima che le credenziali non siano più utilizzabili.

![Progetti generati automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)

