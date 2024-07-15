---
title: Migrazione al componente aggiuntivo Commerce integration framework AEM (CIF)
description: Come migrare al componente aggiuntivo AEM Commerce integration framework (CIF) da una versione precedente
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 38%

---

# Guida alla migrazione per l’Experience Manager Cloud Service {#cif-migration}

Questa guida aiuta a identificare le aree da aggiornare per la migrazione di Experience Manager Cloud Service.

## Componente aggiuntivo CIF

Ad Experience Manager as a Cloud Service, il componente aggiuntivo CIF è l’unica soluzione di integrazione supportata per le soluzioni commerce di Adobe Commerce e di terze parti. Il componente aggiuntivo CIF viene distribuito automaticamente ai clienti con Experience Manager as a Cloud Service, non è necessaria alcuna distribuzione manuale. Consulta [Guida introduttiva di AEM Commerce as a Cloud Service](getting-started.md).

Per supportare i progetti che distribuiscono l&#39;Adobe CIF, fornire [Componenti core CIF AEM](https://github.com/adobe/aem-core-cif-components).

Il componente aggiuntivo CIF è disponibile anche per AEM 6.5 tramite il [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). È compatibile e fornisce le stesse funzionalità del componente aggiuntivo CIF per Experience Manager as a Cloud Service, senza richiedere alcuna correzione.

Classic CIF con le sue dipendenze non è più disponibile. Il codice che si basa su questa versione dell&#39;CIF con `com.adobe.cq.commerce.api` API Java deve essere adattato al componente aggiuntivo CIF e ai relativi principi.

Il connettore CIF precedentemente disponibile non può più essere installato. Il codice che si basa su questo connettore deve essere adattato al componente aggiuntivo CIF e ai suoi principi.

## Struttura del progetto

Scopri la [struttura del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) e le caratteristiche di AEM as a Cloud Service. Adatta la configurazione del progetto al layout di AEM as a Cloud Service.
Rispetto alle implementazioni dell’AEM 6.5, le differenze principali sono due:

* Il bundle OSGI client GraphQL **non deve** più essere incluso nel progetto AEM, ma viene distribuito tramite il componente aggiuntivo CIF.
* Le configurazioni OSGI per il client GraphQL e Graphql Data Service **non devono** più essere incluse nel progetto AEM.

>[!TIP]
>
>Controlla il progetto [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) su GitHub. Questo progetto fornisce profili Maven per implementazioni AEM as a Cloud Service e on-premise che tengono conto delle diverse condizioni di framework.

## Catalogo prodotti

L’importazione di dati del catalogo prodotti non è più supportata. L’utilizzo dei principi del componente aggiuntivo CIF per le richieste di prodotti e cataloghi avviene on-demand tramite chiamate in tempo reale a una soluzione di e-commerce esterna. Per ulteriori informazioni sull’integrazione di una soluzione commerce, consulta il capitolo Integrazione.

>[!TIP]
>
>Se non sono disponibili API in tempo reale, per l’integrazione deve essere utilizzata una cache di prodotto esterna con API. Esempio [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Esperienze nel catalogo dei prodotti con rendering AEM

Se utilizzi la blueprint del catalogo con CIF classico, devi aggiornare il flusso di lavoro del catalogo dei prodotti. Il componente aggiuntivo CIF ora esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM. Non è più richiesta la replica dei dati di prodotto o delle pagine di prodotto.

## Dati non memorizzabili in cache e interazione con l’acquisto

Le richieste lato client per dati e interazioni non memorizzabili in cache (ad esempio, add-to-cart, ricerca) devono passare direttamente all’endpoint commerce (soluzione commerce o livello di integrazione) tramite CDN/Dispatcher. Rimuovi eventuali chiamate in cui AEM era solo un proxy.
