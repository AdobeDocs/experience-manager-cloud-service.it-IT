---
title: Integrazione di AEM e Adobe Commerce tramite Commerce integration framework
description: AEM e Adobe Commerce sono perfettamente integrati tramite la Commerce integration framework (CIF). L’CIF consente all’AEM di accedere a un’istanza di Adobe Commerce e comunicare con Adobe Commerce tramite GraphQL. Consente inoltre agli autori dell’AEM di utilizzare i selettori di prodotti e categorie e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Adobe Commerce. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 30%

---

# Integrazione di AEM e Adobe Commerce tramite Commerce integration framework {#aem-framework}

L’Experience Manager e Adobe Commerce sono integrati direttamente tramite la Commerce integration framework (CIF). L’CIF consente all’AEM di accedere e comunicare direttamente con l’istanza di Commerce utilizzando Adobe Commerce [API di GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> La versione minima supportata dell’API GraphQL è la 2.3.5. Alcune funzioni sono supportate solo nelle versioni più recenti o solo nell’edizione Adobe Commerce.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Questo scenario, in cui l’CIF comunica con il Commerce tramite GraphQL.
>* [I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/headless/graphql-api/content-fragments.md).

## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF ](../assets/AEM_Magento_Architecture.png)

All’interno dell’CIF è disponibile il supporto di modelli di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando il [client GraphQL](https://github.com/adobe/commerce-cif-graphql-client) in combinazione con un [set di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema commerce GraphQL. Inoltre, è possibile utilizzare qualsiasi query GraphQL o mutazione in formato GQL.

Per i componenti lato client, creati con [React](https://reactjs.org/), il [Client Apollo](https://www.apollographql.com/docs/react/) viene utilizzato.

## Architettura dei componenti core CIF di AEM {#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

[Componenti core CIF dell’AEM](https://github.com/adobe/aem-core-cif-components) seguire modelli di progettazione e best practice molto simili a quelli [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Adobe Commerce per i componenti core CIF dell’AEM sono implementate in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM ](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, i componenti core CIF dell’AEM e i componenti di progetto personalizzati possono facilmente recuperare il client configurato per un archivio Adobe Commerce associato a una pagina AEM tramite la configurazione Sling Context-Aware.
