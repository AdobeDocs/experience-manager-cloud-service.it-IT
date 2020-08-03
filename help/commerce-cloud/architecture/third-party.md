---
title: Integrazione del commercio AEM e di terze parti tramite Commerce Integration Framework
description: Integrazione del commercio AEM e di terze parti tramite Commerce Integration Framework
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Integrazione del commercio AEM e di terze parti tramite Commerce Integration Framework {#aem-third-party}

Le aziende aziendali possono richiedere soluzioni di commercio di terze parti aggiuntive per alimentare il proprio negozio. Commerce Integration Framework (CIF) può essere utilizzato in tali scenari di integrazione in cui, oltre al Magento, una soluzione di commercio di terze parti deve essere integrata con AEM. CIF fornisce elementi come uno storefront di riferimento acceleratore, componenti AEM CIF di base e strumenti di authoring che funzionano con il Magento out-of-the-box. Per integrare AEM e una soluzione di commercio di terze parti e riutilizzare questi elementi CIF, è necessario un ulteriore sviluppo.

## Architettura {#architecture}

L&#39;architettura generale è la seguente:

![Panoramica AEM sull&#39;architettura di terze parti/non di Magento](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

La differenza principale tra l&#39;architettura di integrazione per AEM - Magento e AEM - commercio di terze parti è l&#39;aggiunta di un livello di integrazione e trasformazione dei dati come mostrato nell&#39;immagine precedente. Il livello di integrazione deve essere ospitato sulla piattaforma Adobe I/O Runtime,  piattaforma senza server  Adobe. Ulteriori informazioni su Adobe I/O Runtime sono disponibili [qui](https://www.adobe.io/apis/experienceplatform/runtime.html).

Lo scopo di questo livello di integrazione è mappare un&#39;API non di Magento o di terze parti rispetto  API Commerce di Adobe (Magenti API GraphQL di ). Questa mappatura consente agli strumenti di authoring CIF [AEM componenti](https://github.com/adobe/aem-core-cif-components) principali e CIF di recuperare i dati dalla soluzione non di Magento. Con questo approccio, il livello di integrazione racchiude la logica di integrazione e crea una separazione di preoccupazione tra AEM e la soluzione di terze parti. Questo consente di utilizzare gli elementi CIF in modo agnostico con diverse soluzioni di terze parti. I vantaggi dell&#39;utilizzo di elementi CIF nel progetto sono stati descritti in [Introduzione](/help/commerce-cloud/overview.md).

## Sviluppare un&#39;integrazione {#develop-integration}

Per aiutarti a iniziare a creare il livello di integrazione richiesto per integrare una soluzione di terze parti con AEM, abbiamo creato un&#39;implementazione [di](https://github.com/adobe/commerce-cif-graphql-integration-reference) riferimento per dimostrarlo. Questo riferimento può essere utilizzato come punto di partenza del progetto.
