---
title: Migrazione al componente aggiuntivo CIF (AEM Commerce Integration Framework)
description: Come migrare al componente aggiuntivo CIF di AEM Commerce Integration Framework (CIF) da una versione precedente
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 45%

---

# Guida alla migrazione per l’Experience Manager Cloud Service {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione di Experience Manager Cloud Service.

## Componente aggiuntivo CIF

Per Experience Manager as a Cloud Service il componente aggiuntivo CIF è l’unica soluzione di integrazione supportata per le soluzioni commerce di Adobe e di terze parti. Il componente aggiuntivo CIF viene distribuito automaticamente ai clienti con Experience Manager as a Cloud Service, non è necessaria alcuna distribuzione manuale. Consulta [Guida introduttiva di AEM Commerce as a Cloud Service](getting-started.md).

Per supportare i progetti che utilizzano l’Adobe CIF, fornisci [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components).

Il componente aggiuntivo CIF è disponibile anche per AEM 6.5 tramite il [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). È compatibile e fornisce le stesse funzionalità del componente aggiuntivo CIF per Experience Manager as a Cloud Service, senza richiedere alcuna correzione.

Classic CIF con le sue dipendenze non è più disponibile. Codice basato su questa versione CIF utilizzando `com.adobe.cq.commerce.api` Le API Java devono essere regolate in base al componente aggiuntivo CIF e ai relativi principi.

Impossibile installare più il connettore CIF precedentemente disponibile. Il codice che si basa su questo connettore deve essere regolato in base al componente aggiuntivo CIF e ai suoi principi.

## Struttura del progetto

Scopri le [AEM struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) e le caratteristiche di AEM as a Cloud Service. Adatta la configurazione del progetto al layout di AEM as a Cloud Service.
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
>Se non sono disponibili API in tempo reale, per l’integrazione è necessario utilizzare una cache di prodotto esterna con API. Esempio [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Esperienze del catalogo dei prodotti con rendering AEM

Se utilizzi la blueprint del catalogo con Classic CIF, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering immediato delle esperienze di catalogo di prodotti utilizzando AEM modelli di catalogo. Non è più necessaria alcuna replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili nella cache e interazione con lo shopping

Le richieste lato client per dati e interazioni non memorizzabili nella cache (ad esempio, add-to-cart, search) devono passare direttamente all’endpoint commerce (soluzione commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi tutte le chiamate in cui AEM solo un proxy.
