---
title: Integrazione di AEM e Adobe Commerce (Magento) tramite Commerce Integration Framework
description: AEM e Adobe Commerce (Magento) sono perfettamente integrati tramite Commerce Integration Framework (CIF). CIF consente ad AEM di accedere a un’istanza di Magento e di comunicare con Magento tramite GraphQL. Consente inoltre agli autori AEM di utilizzare i selettori di Prodotto e Categoria e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Magento. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
exl-id: 1cdfda88-a728-432f-b24a-f81347572bcf
translation-type: tm+mt
source-git-commit: a4e53fdcb33eab8afabcb13d651155cd247bda1f
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 37%

---

# Integrazione di AEM e Adobe Commerce (Magento) tramite Commerce Integration Framework {#aem-magento-framework}

L’integrazione di Experience Manager e Adobe Commerce (Magento) avviene senza soluzione di continuità tramite Commerce Integration Framework (CIF). CIF consente a AEM di accedere e comunicare direttamente con l’istanza comune utilizzando le API Commerce di Adobe [GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) come Cloud Service:
>
>* Questo scenario, in cui CIF comunica con l’e-commerce tramite GraphQL.
>* [AEM Frammenti di contenuto collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF ](../assets/AEM_Magento_Architecture.png)

CIF supporta il modello di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando il client [GraphQL](https://github.com/adobe/commerce-cif-graphql-client) integrato e un [set di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema GraphQL di e-commerce Inoltre, è possibile utilizzare qualsiasi query o mutazione GraphQL in formato GQL.

Per i componenti lato client, creati con [React](https://reactjs.org/), viene utilizzato il [client Apollo](https://www.apollographql.com/docs/react/).

## Architettura dei componenti core CIF di AEM{#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

[AEM ](https://github.com/adobe/aem-core-cif-components) componenti core CIF seguono modelli di progettazione e best practice molto simili a quelli dei  [AEM componenti core WCM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Adobe Commerce per i componenti core CIF di AEM è implementata in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM ](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, AEM componenti core CIF e componenti di progetto personalizzati possono facilmente recuperare il client configurato per un archivio Adobe Commerce associato a una pagina AEM tramite la configurazione Sling Context-Aware.
