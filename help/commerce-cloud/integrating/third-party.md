---
title: Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework
description: Le imprese possono richiedere soluzioni Commerce di terze parti aggiuntive per potenziare la propria vetrina. The Commerce Integration Framework (CIF) can be used in such integration scenarios to connect a 3rd party commerce solution to Adobe Experience Manager using I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: a53ef07cd9da636c8d938c711de6defb9eb8e05f
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 11%

---

# Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework {#aem-third-party}

The integration of non-Adobe Commerce solution is a common scenario for CIF. Le soluzioni di terze parti con diverse API e schemi vengono connesse tramite un livello di integrazione.

## Architettura {#architecture}

L’architettura generale è la seguente:

![Panoramica dell’architettura AEM per terze parti/non Magento](../assets//AEM_nonMagento_Architecture.png)

The purpose of this integration layer is to map 3rd-party APIs and schemas against the supported Adobe Commerce GraphQL APIs and schemas outside of the Experience Manager. Grazie a questa incapsulazione, la logica di integrazione e i sistemi possono essere aggiornati senza modificare il codice all’interno dell’Experience Manager.

## Requisiti della soluzione per un&#39;integrazione

Poiché l’Experience Manager recupera i dati on-demand, sono necessarie API in tempo reale per il catalogo dei prodotti.

>[!TIP]
>
>If no real-time APIs are available, an external product cache with APIs should be used for the integration. Esempio [Magento open-source](https://magento.com/products/magento-open-source).

Non è necessario implementare l&#39;intero schema GraphQL, ma solo gli oggetti dello schema per abilitare i casi d&#39;uso desiderati.

## Casi d’uso di back-end

CIF estende l’Experience Manager con strumenti di accesso al catalogo dei prodotti in tempo reale e di gestione dell’esperienza di prodotto. Questa integrazione diretta consente agli autori di accedere ai dati di e-commerce utilizzando le interfacce utente incorporate ogni volta che necessario, senza lasciare il contesto del contenuto.

The integration of product catalog APIs are required to unlock these use-cases.

## Frontend use-cases

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) retrieve and exchage data via the CIF supported Adobe Commerce APIs. Per riutilizzare i componenti, è necessario implementare le rispettive API.

Il consiglio per i componenti lato client critici in termini di prestazioni è di comunicare direttamente con la soluzione di terze parti per evitare la latenza.

## Sviluppo di un’integrazione {#develop-integration}

We recommend to use [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) for the integration layer. È incluso nel componente aggiuntivo CIF per terze parti. Funzionando con un approccio microservice, è ideale per integrare facilmente soluzioni multiple.

La [implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) è un ottimo punto di partenza per creare l’integrazione nella soluzione commerce. Anche se supporta GraphQL, può essere integrato con qualsiasi altro tipo di API, come REST.

Questo livello di integrazione non è necessario se è disponibile un livello di terze parti (ad esempio Mulesoft) o se l’integrazione viene basata sulla soluzione di terze parti.

## Connettori predefiniti {#connectors}

Connectors provide a good starting for projects. Sono dotati di una connessione specifica per la soluzione commerce e di una mappatura API predefinita. Questi connettori sono costruiti da terze parti e non sono mantenuti da Adobe. Per informazioni, contattare il partner.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), costruito da Diconium
* [Strumenti commerciali](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), costruito da Diconium

>[!TIP]
>
>Anche se i connettori aiutano i progetti ad accelerare l’integrazione Commerce, non sono plug-in-play. Enterprise commerce solutions are usually heavily customized and require a custom integration. Good knowledge of the commerce platform, Adobe Commerce GraphQL schemas, and Adobe I/O Runtime is required.
