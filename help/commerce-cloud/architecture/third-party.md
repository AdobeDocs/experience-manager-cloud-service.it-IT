---
title: Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework
description: Le imprese possono richiedere soluzioni Commerce di terze parti aggiuntive per potenziare la propria vetrina. Commerce Integration Framework (CIF) può essere utilizzato in tali scenari di integrazione per collegare una soluzione di e-commerce di terze parti ad Adobe Experience Manager tramite I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 92%

---


# Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework {#aem-third-party}

Le imprese possono richiedere soluzioni Commerce di terze parti aggiuntive per potenziare la propria vetrina. Commerce Integration Framework (CIF) può essere utilizzato in scenari di integrazione in cui, oltre a Magento, è necessario integrare con AEM anche una soluzione Commerce di terze parti. CIF fornisce elementi come una vetrina di riferimento di accelerazione, componenti core CIF di AEM e strumenti di authoring pronti all’uso per Magento. Per integrare AEM e una soluzione Commerce di terze parti e riutilizzare questi elementi CIF, è necessario un ulteriore sviluppo.

## Architettura {#architecture}

L’architettura generale è la seguente:

![Panoramica dell’architettura AEM per terze parti/non Magento](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

La differenza principale tra l’architettura di integrazione per AEM con Magento e AEM e una soluzione commerce di terze parti consiste nell’aggiunta di un livello di integrazione e trasformazione dei dati, come illustrato nell’immagine precedente. Il livello di integrazione deve essere ospitato sulla piattaforma Adobe I/O Runtime, che è una piattaforma di Adobe senza server. Ulteriori informazioni su Adobe I/O Runtime sono disponibili [qui](https://www.adobe.io/apis/experienceplatform/runtime.html).

Questo livello di integrazione ha lo scopo di mappare un’API non Magento o di terze parti rispetto sulle API Commerce di Adobe (API di Magento GraphQL). Questa mappatura consente ai [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) e agli strumenti di authoring CIF di recuperare i dati dalla soluzione non Magento. Con questo approccio, il livello di integrazione racchiude la logica di integrazione e crea una separazione tra AEM e la soluzione di terze parti. Ciò consente di utilizzare gli elementi CIF in modo agnostico con diverse soluzioni di terze parti. I vantaggi dell’utilizzo di elementi CIF nel progetto sono descritti nell’[Introduzione](/help/commerce-cloud/overview.md).

## Sviluppare un’integrazione {#develop-integration}

Per aiutarti a iniziare a creare il livello di integrazione richiesto per integrare con AEM una soluzione non Magento/di terze parti, abbiamo creato un’[implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference). Questo riferimento può essere utilizzato come punto di partenza del progetto.
