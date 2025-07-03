---
title: Integrazione di AEM e Adobe Commerce tramite Commerce integration framework
description: AEM e Adobe Commerce sono integrati direttamente tramite Commerce integration framework (CIF). CIF consente ad AEM di accedere a un’istanza di Adobe Commerce e comunicare con Adobe Commerce tramite GraphQL. Consente inoltre agli autori di AEM di utilizzare i selettori di prodotti e categorie e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Adobe Commerce. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 22%

---

# Integrazione di AEM e Adobe Commerce tramite Commerce integration framework {#aem-framework}

Experience Manager e Adobe Commerce sono integrati direttamente tramite Commerce integration framework (CIF). CIF consente ad AEM di accedere e comunicare direttamente con l&#39;istanza di Commerce utilizzando le [API GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) di Adobe Commerce.

>[!NOTE]
>
> La versione minima supportata dell’API GraphQL è la 2.3.5. Alcune funzioni sono supportate solo nelle versioni più recenti o solo nell’edizione Adobe Commerce.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Questo scenario, in cui CIF comunica con commerce tramite GraphQL.
>* [I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/headless/graphql-api/content-fragments.md).

## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF ](../assets/AEM_Magento_Architecture.png)

In CIF sono supportati modelli di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando il [client GraphQL](https://github.com/adobe/commerce-cif-graphql-client) integrato e generico in combinazione con un [set di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema commerce GraphQL. Inoltre, è possibile utilizzare qualsiasi query GraphQL o mutazione in formato GQL.

Per i componenti lato client, generati con [React](https://reactjs.org/), viene utilizzato il [client Apollo](https://www.apollographql.com/docs/react/).

## Architettura dei componenti core di AEM CIF {#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) seguono modelli di progettazione e best practice molto simili a quelli dei [componenti core WCM di AEM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Adobe Commerce per i componenti core di AEM CIF sono implementate in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM ](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, i componenti core CIF di AEM e i componenti di progetto personalizzati possono facilmente recuperare il client configurato per uno store di Adobe Commerce associato a una pagina AEM tramite la configurazione Sling Context-Aware.

## Ricerca {#search}

CIF fornisce un [componente core di ricerca](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) pronto all&#39;uso che è un&#39;esperienza di ricerca con rendering lato server basata su [API Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/). I clienti Commerce possono utilizzare [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=en). Segui questo [collegamento](/help/commerce-cloud/integrating/live-search-plp.md) per ulteriori informazioni sull&#39;integrazione CIF - Live Search.

