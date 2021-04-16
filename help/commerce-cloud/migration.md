---
title: Migrazione al componente aggiuntivo CIF (AEM Commerce Integration Framework)
description: Come migrare al componente aggiuntivo CIF di AEM Commerce Integration Framework (CIF) da una versione precedente
translation-type: tm+mt
source-git-commit: cda25048e171f6aacd5349706ad4192965e703db
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 20%

---

# Guida alla migrazione per l’Experience Manager Cloud Service {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione degli Experienci Manager Cloud Service.

## Componente aggiuntivo CIF

Ad Experience Manager, come Cloud Service, il componente aggiuntivo CIF è l’unica soluzione di integrazione Commerce supportata per le soluzioni Commerce di Adobe e Commerce di terze parti. Il componente aggiuntivo CIF viene distribuito automaticamente per i clienti su Experience Manager come Cloud Service, non è necessaria alcuna distribuzione manuale. Consulta [Guida introduttiva a Commerce as a Cloud Service](getting-started.md) .

Per supportare i progetti che utilizzano l’Adobe CIF, fornisci [AEM componenti core CIF](https://github.com/adobe/aem-core-cif-components).

Il componente aggiuntivo CIF è disponibile per AEM 6.5 e tramite il [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). È compatibile e fornisce le stesse caratteristiche del componente aggiuntivo CIF, ad Experience Manager come Cloud Service - non sono necessarie regolazioni.

Classic CIF con le sue dipendenze non è più disponibile. Il codice che si basa su questa versione CIF che utilizza `com.adobe.cq.commerce.api` API Java deve essere regolato in base al componente aggiuntivo CIF e ai relativi principi.

Impossibile installare più il connettore CIF precedentemente disponibile. Il codice che si basa su questo connettore deve essere regolato in base al componente aggiuntivo CIF e ai suoi principi.

## Struttura del progetto

Scopri la [AEM Struttura del progetto](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) e le caratteristiche di AEM come Cloud Service. Adatta la configurazione del progetto al layout di AEM as a Cloud Service.
Rispetto alle implementazioni di AEM 6.5, le differenze principali sono due:

* Il bundle OSGI client GraphQL **non deve** più essere incluso nel progetto AEM, ma viene distribuito tramite il componente aggiuntivo CIF.
* Le configurazioni OSGI per il client GraphQL e Graphql Data Service **non devono** più essere incluse nel progetto AEM.

>[!TIP]
>
>Controlla il progetto [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) su GitHub. Questo progetto fornisce profili Maven per implementazioni AEM as a Cloud Service e on-premise che tengono conto delle diverse condizioni di framework.

## Catalogo dei prodotti

L&#39;importazione dei dati del catalogo dei prodotti non è più supportata. L’utilizzo dei componenti aggiuntivi CIF per le richieste di prodotti e catalogo è on-demand tramite chiamate in tempo reale a una soluzione commerce esterna. Vai a capitolo Integrazione per ulteriori informazioni sull&#39;integrazione di una soluzione commerce.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione è necessario utilizzare una cache di prodotto esterna con API. Esempio [Magento open-source](https://magento.com/products/magento-open-source).

## Esperienze del catalogo dei prodotti con rendering AEM

Se utilizzi la blueprint del catalogo con Classic CIF, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering immediato delle esperienze di catalogo di prodotti utilizzando AEM modelli di catalogo. Non è più necessaria alcuna replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili nella cache e interazione con lo shopping

Le richieste lato client per dati e interazioni non memorizzabili nella cache (ad esempio, add-to-cart, search) devono passare direttamente all’endpoint e-commerce (soluzione e-commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi tutte le chiamate in cui AEM solo un proxy.
