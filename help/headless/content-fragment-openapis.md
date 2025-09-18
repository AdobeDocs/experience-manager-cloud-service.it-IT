---
title: OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto
description: Scopri le API OpenAPI per frammenti di contenuto e modelli per frammenti di contenuto.
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1fb1201fa976e4c0e3c87f22bd9327a55828efef
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# OpenAPI per la gestione di frammenti di contenuto e modelli di frammenti di contenuto {#content-fragments-and-content-fragment-models-management-openapis}

L’implementazione OpenAPI modernizzata dell’API di gestione dei frammenti di contenuto consente agli sviluppatori di eseguire in modo programmatico le operazioni Crea, Leggi, Aggiorna ed Elimina in AEM Author per gestire i modelli di frammenti di contenuto e i frammenti di contenuto memorizzati in AEM. Queste API supportano una serie di casi d’uso.

Per la documentazione completa, consulta [API di gestione dei frammenti di contenuto](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/).

>[!NOTE]
>
>L&#39;utilizzo esistente di [Assets HTTP API](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) per i frammenti di contenuto deve essere migrato alla nuova OpenAPI per la gestione dei frammenti di contenuto.

>[!NOTE]
>
>È necessaria l’autorizzazione per accedere a OpenAPI quando non hai effettuato l’accesso ad AEM, ad esempio quando OpenAPI viene utilizzato da un altro prodotto come parte di un’integrazione.
>
>Consulta [API basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) per informazioni dettagliate su come autorizzare l&#39;accesso a OpenAPI.

>[!CAUTION]
>
>Per impostazione predefinita, OpenAPI di gestione dei frammenti di contenuto è disabilitato al momento della pubblicazione. Invece di questo, per i casi d&#39;uso orientati alla consegna si consiglia di utilizzare [Content Fragment Delivery OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md).

>[!NOTE]
>
>Consulta [API di AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) per una panoramica delle varie API disponibili e un confronto di alcuni dei concetti coinvolti.