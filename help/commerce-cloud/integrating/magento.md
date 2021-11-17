---
title: Integrazione di AEM e Adobe Commerce (Magento) tramite Commerce Integration Framework
description: AEM e Adobe Commerce (Magento) sono perfettamente integrati utilizzando Commerce Integration Framework (CIF). CIF consente ad AEM di accedere a un’istanza di Magento e di comunicare con Magento tramite GraphQL. Consente inoltre agli autori AEM di utilizzare i selettori di Prodotto e Categoria e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Magento. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 52cfd60cde3165fde6b0167783c16b0fc1efc950
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 31%

---

# Integrazione di AEM e Adobe Commerce (Magento) tramite Commerce Integration Framework {#aem-magento-framework}

Experience Manager e Adobe Commerce (Magento) sono perfettamente integrati tramite Commerce Integration Framework (CIF). CIF consente a AEM di accedere e comunicare direttamente con l’istanza virale utilizzando Adobe Commerce [API GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> La versione minima supportata dell’API GraphQL è la 2.3.5. Alcune funzioni sono supportate solo nelle versioni più recenti o solo nell’edizione Adobe Commerce.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Questo scenario, in cui CIF comunica con l’e-commerce tramite GraphQL.
>* [AEM Frammenti di contenuto collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF ](../assets/AEM_Magento_Architecture.png)

CIF supporta il modello di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando l’interfaccia predefinita generica [Client GraphQL](https://github.com/adobe/commerce-cif-graphql-client) in combinazione con un [insieme di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema GraphQL di e-commerce Inoltre, è possibile utilizzare qualsiasi query GraphQL o mutazione in formato GQL.

Per i componenti lato client, creati utilizzando [Reagire](https://reactjs.org/), [Client Apollo](https://www.apollographql.com/docs/react/) viene utilizzato.

## Architettura dei componenti core CIF di AEM {#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

[Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) seguire modelli di progettazione e best practice molto simili come [AEM componenti core WCM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Adobe Commerce per i componenti core CIF di AEM è implementata in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM ](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, AEM componenti core CIF e componenti di progetto personalizzati possono facilmente recuperare il client configurato per un archivio Adobe Commerce associato a una pagina AEM tramite la configurazione Sling Context-Aware.
