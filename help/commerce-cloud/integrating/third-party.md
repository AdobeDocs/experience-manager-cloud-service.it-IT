---
title: Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework
description: Le imprese possono richiedere soluzioni Commerce di terze parti aggiuntive per potenziare la propria vetrina. Commerce Integration Framework (CIF) può essere utilizzato in tali scenari di integrazione per collegare una soluzione Commerce di terze parti a Adobe Experience Manager utilizzando I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 42dd8922-540d-4a93-9e45-b5e83dc11e16
translation-type: tm+mt
source-git-commit: c0a79d9ffefba06b64d48aed79e9a00baa4987df
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 14%

---

# Integrazione di AEM e Commerce di terze parti tramite Commerce Integration Framework {#aem-third-party}

L’integrazione della soluzione Commerce non Adobe è uno scenario comune per CIF. Le soluzioni di terze parti con diverse API e schemi vengono connesse tramite un livello di integrazione.

## Architettura {#architecture}

L’architettura generale è la seguente:

![Panoramica dell’architettura AEM per terze parti/non Magento](../assets//AEM_nonMagento_Architecture.png)

Lo scopo di questo livello di integrazione è mappare API e schemi di terze parti rispetto alle API e agli schemi Adobe Commerce GraphQL supportati al di fuori dell’Experience Manager. Grazie a questa incapsulazione, la logica di integrazione e i sistemi possono essere aggiornati senza modificare il codice all’interno dell’Experience Manager.

## Requisiti della soluzione per un&#39;integrazione

Poiché l’Experience Manager recupera i dati on-demand, sono necessarie API in tempo reale per il catalogo dei prodotti.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione è necessario utilizzare una cache di prodotto esterna con API. Esempio [Magento open-source](https://magento.com/products/magento-open-source).

Non è necessario implementare l&#39;intero schema GraphQL, ma solo gli oggetti dello schema per abilitare i casi d&#39;uso desiderati.

## Casi d’uso di back-end

CIF estende l’Experience Manager con strumenti di accesso al catalogo dei prodotti in tempo reale e di gestione dell’esperienza di prodotto. Questa integrazione diretta consente agli autori di accedere ai dati di e-commerce utilizzando le interfacce utente incorporate ogni volta che necessario, senza lasciare il contesto del contenuto.

Per sbloccare questi casi d’uso è necessaria l’integrazione delle API del catalogo di prodotti.

## Casi d’uso anteriori

[AEM ](https://github.com/adobe/aem-core-cif-components) componenti core CIF recuperano e scambiano dati tramite le API Commerce di Adobe supportate da CIF. Per riutilizzare i componenti, è necessario implementare le rispettive API.

Il consiglio per i componenti lato client critici in termini di prestazioni è di comunicare direttamente con la soluzione di terze parti per evitare la latenza.

## Sviluppo di un&#39;integrazione {#develop-integration}

È consigliabile utilizzare [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) per il livello di integrazione. È incluso nel componente aggiuntivo CIF per terze parti. Funzionando con un approccio microservice, è ideale per integrare facilmente soluzioni multiple.

L’ [implementazione di riferimento](https://github.com/adobe/commerce-cif-graphql-integration-reference) è un ottimo punto di partenza per creare l’integrazione nella soluzione commerce. Anche se supporta GraphQL, può essere integrato con qualsiasi altro tipo di API, come REST.

Questo livello di integrazione non è necessario se è disponibile un livello di terze parti (ad esempio Mulesoft) o se l’integrazione viene basata sulla soluzione di terze parti.
