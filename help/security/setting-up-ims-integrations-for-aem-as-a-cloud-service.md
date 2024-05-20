---
title: Configurazione delle integrazioni IMS per AEM as a Cloud Service
description: Scopri come impostare le integrazioni IMS per AEM as a Cloud Service
source-git-commit: e6749b9a5e97634a4706db5656b1e11dba4442c9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---


# Configurazione delle integrazioni IMS per AEM as a Cloud Service {#setting-up-ims-integrations-for-aemaacs}

Adobe Experience Manager (AEM) as a Cloud Service può essere integrato con molte altre soluzioni Adobe. Ad esempio, Adobe Target, Adobe Analytics e altri.

Le integrazioni utilizzano un’integrazione IMS, configurata con OAuth S2S.

* Dopo aver creato:

   * [Credenziali nella Console per sviluppatori](#credentials-in-the-developer-console)

* Quindi puoi:

   * Crea un (nuovo) [Configurazione OAuth](#creating-oauth-configuration)

   * [Migrare una configurazione JWT esistente a una configurazione OAuth](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>In precedenza, le configurazioni venivano effettuate con [Credenziali JWT ora obsolete nella console Adobe Developer](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>Tali configurazioni non possono più essere create o aggiornate, ma è possibile eseguirne la migrazione alle configurazioni OAuth.

## Credenziali nella Console per sviluppatori {#credentials-in-the-developer-console}

Come primo passaggio, devi configurare le credenziali OAuth nella console Adobe Developer.

Per informazioni dettagliate su come eseguire questa operazione, consulta la documentazione di Developer Console, a seconda dei requisiti:

* Panoramica:

   * [Autenticazione da server a server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Creazione di nuove credenziali OAuth:

   * [Guida all&#39;implementazione delle credenziali server-to-server di OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* Migrazione di una credenziale JWT esistente a una credenziale OAuth:

   * [Migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali server-to-server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

Ad esempio:

![Credenziali OAuth nella Console per sviluppatori](assets/ims-configuration-developer-console.png)

## Creazione di una configurazione OAuth {#creating-oauth-configuration}

Per creare una nuova integrazione Adobe IMS utilizzando OAuth:

1. In AEM, vai a **Strumenti**, **Sicurezza**, **Integrazione Adobe IMS**.

1. Seleziona **Crea**.

1. Completa la configurazione in base ai dettagli provenienti da [Console per sviluppatori](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Ad esempio:

   ![Crea configurazione OAuth](assets/ims-create-oauth-configuration.png)

1. **Salva** le tue modifiche.

## Migrazione di una configurazione JWT esistente a una configurazione OAuth {#migrating-existing-JWT-configuration-to-oauth}

Per migrare un’integrazione Adobe IMS esistente basata sulle credenziali JWT:

>[!NOTE]
>
>Questo esempio mostra una configurazione IMS di Launch.

1. In AEM, vai a **Strumenti**, **Sicurezza**, **Integrazione Adobe IMS**.

1. Seleziona la configurazione JWT di cui eseguire la migrazione. Le configurazioni JWT sono contrassegnate dall’avviso **Credenziali JWT (obsoleto)**.

1. Seleziona **Proprietà**:

   ![Seleziona configurazione JWT](assets/ims-migrate-jwt-select-configuration.png)

1. La configurazione verrà aperta in sola lettura:

   ![Proprietà di configurazione - Sola lettura](assets/ims-migrate-jwt-properties-read-only.png)

1. Seleziona **OAuth** dal **Tipo di autenticazione** elenco a discesa:

   ![Seleziona tipo di autenticazione](assets/ims-migrate-jwt-authentication-type.png)

1. Le proprietà disponibili verranno aggiornate. Utilizza i dettagli dalla Console per sviluppatori per completarli:

   ![Dettagli OAuth completi](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Utilizzare **Salva e chiudi** per mantenere gli aggiornamenti.
Quando ritorni alla console **Credenziali JWT (obsoleto)** l&#39;avviso non sarà più disponibile.