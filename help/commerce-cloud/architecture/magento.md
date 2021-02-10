---
title: Integrazione tra AEM e Magento con l’utilizzo di Commerce Integration Framework
description: AEM e Magento sono integrati direttamente tramite Commerce Integration Framework (CIF). CIF consente ad AEM di accedere a un’istanza di Magento e di comunicare con Magento tramite GraphQL. Consente inoltre agli autori AEM di utilizzare i selettori di Prodotto e Categoria e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Magento. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: 36e0fd66c9119571cde5c8791862abed8b552d5a
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 88%

---


# Integrazione tra AEM e Magento con l’utilizzo di Commerce Integration Framework {#aem-magento-framework}

AEM e Magento sono integrati direttamente tramite Commerce Integration Framework (CIF). CIF consente ad AEM di accedere a un’istanza di Magento e di comunicare con Magento tramite GraphQL. Consente inoltre agli autori AEM di utilizzare i selettori di Prodotto e Categoria e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Magento. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) come Cloud Service:
>
>* AEM Commerce consuma i dati provenienti da una piattaforma di eCommerce tramite GraphQL.
>* [AEM Frammenti di contenuto collaborano con l&#39;API AEM GraphQL (un&#39;implementazione personalizzata, basata su GraphQL standard) per fornire contenuto strutturato da utilizzare nelle applicazioni](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF ](../assets/AEM_Magento_Architecture.JPG)

CIF si basa sul supporto di GraphQL. Il canale di comunicazione principale tra AEM e Magento è l’API [GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) di Magento. Esistono diversi modi per configurare la comunicazione tra AEM as a Cloud Service e Magento. Per informazioni dettagliate, consulta la pagina [Guida introduttiva](../getting-started.md).

CIF supporta il modello di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando il [client GraphQL ](https://github.com/adobe/commerce-cif-graphql-client) integrato e generico in combinazione con un [set di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema GraphQL di Magento. Inoltre, è possibile utilizzare qualsiasi query GraphQL o mutazione in formato GQL.

Per i componenti lato client, creati con [React](https://reactjs.org/), viene utilizzato il [client Apollo](https://www.apollographql.com/docs/react/).

## Architettura dei componenti core CIF di AEM{#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

I [componenti core CIF di AEM ](https://github.com/adobe/aem-core-cif-components) seguono modelli di progettazione e best practice molto simili a quelli dei [componenti core di AEM WCM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Magento per i componenti core CIF di AEM è implementata in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM ](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, i componenti core CIF di AEM e i componenti di progetto personalizzati possono facilmente recuperare il client configurato per uno store di Magento associato a una pagina AEM tramite la configurazione Sling Context-Aware.
