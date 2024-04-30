---
title: Credenziali JWT nella console Adobe Developer obsolete
description: Scopri l’impatto della rimozione delle credenziali JWT nella console Adobe Developer sull’AEM.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 802e29017d3f1e59ee1676b4172292cb3453648a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 56%

---

# Credenziali JWT nella console Adobe Developer obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Per ulteriori informazioni, i clienti di AEM 6.5 dovrebbero fare riferimento a [questo articolo](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console).

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. A partire dal 3 giugno 2024, non sarà possibile creare nuove credenziali dell’account di servizio (JWT) e, a partire dal 27 gennaio 2025, le credenziali JWT esistenti non funzioneranno. È possibile [consultare le informazioni sull’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come AEM as a Cloud Service dovrebbe gestire l’obsolescenza.

Attualmente, l’aspetto principale è che le funzioni AEM non supportano ancora le nuove credenziali server-to-server di OAuth. Il supporto per AEM as a Cloud Service sarà presto disponibile entro metà maggio 2024 tramite una versione dell’AEM. È possibile che sia stata ricevuta un’e-mail con le istruzioni per la migrazione delle credenziali JWT, ma occorre tenere presente che è possibile e si dovrebbe rimandare la migrazione delle credenziali fino a quando AEM non supporterà il nuovo tipo di credenziali da server a server OAuth.

Le sezioni seguenti elencano gli scenari in cui i clienti devono (o a volte non devono) sostituire le credenziali del proprio account di servizio (JWT) con credenziali server-to-server OAuth, una volta che l’AEM li ha supportati a metà maggio. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) sostituire le credenziali in futuro.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (notare che la sigla **AEM** nella denominazione, che la distingue da **Adobe** Developer Console) fornisce un’utilità per generare [token JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzati per le API da server a server. Queste credenziali non sono obsolete e possono continuare a essere utilizzate.


## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: attendi di effettuare la migrazione dopo metà maggio 2024, quando l’AEM la supporterà (questo articolo verrà aggiornato in tale data)

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

L’interfaccia utente di authoring di AEM viene utilizzata per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio Adobe Target, Adobe Analytics, Adobe Launch, AFCS e molte altre.

![Integrazione di AEM con altre soluzioni](/help/security/assets/jwt-deprecation.png)

Ad esempio, ecco [le istruzioni](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims) per configurare l’integrazione con Adobe Target. Chiave API in [Completamento della configurazione IMS in AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims#completing-the-ims-configuration-in-aem) deve essere migrata al tipo di credenziali server-to-server OAuth, una volta che l’AEM supporta tali credenziali a metà maggio. Tali istruzioni saranno aggiornate a metà maggio per aiutarti ad applicare le nuove credenziali server-to-server OAuth.

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: esegui la migrazione alle credenziali OAuth server-to-server.

**Versioni di AEM pertinenti**: AEM as a Cloud Service

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È necessario migrare le credenziali nel progetto Adobe Developer al tipo di credenziali server-to-server OAuth prima che le credenziali JWT obsolete scadano nel gennaio 2025.

## Progetti generati automaticamente {#autogen-projects}

**Azione**: non eseguire la migrazione perché Adobe sta per eseguire la migrazione per tuo conto.

**Versioni di AEM pertinenti**: AEM as a Cloud Service.

Quando Cloud Manager esegue il provisioning dell’ambiente as a Cloud Service dall’AEM, genera automaticamente un progetto Adobe Developer Console con credenziali JWT. Questo progetto è contrassegnato come di sola lettura, come illustrato nella schermata seguente. I clienti non possono e non devono tentare di migrare questi progetti alle credenziali da server a server OAuth; al contrario, Adobe eseguirà la migrazione di questi progetti da solo, prima che le credenziali non siano più utilizzabili.

![Progetti generati automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
