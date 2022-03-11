---
title: Utilizzo dell’IDE GraphiQL in AEM
description: Scopri come utilizzare l’IDE GraphiQL in Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---

# Utilizzo dell’IDE GraphiQL {#graphiql-ide}

È disponibile un’implementazione dell’IDE [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) standard per l’uso con GraphQL per AEM. Può essere [installato con AEM](#installing-graphiql-ide).

>[!NOTE]
>
>GraphiQL è associato all’endpoint globale (e non funziona con altri endpoint per configurazioni specifiche di Sites).

Lo strumento GraphiQL ti consente di inserire, verificare ed eseguire query. GraphiQL offre inoltre un facile accesso alla documentazione, semplificando l’apprendimento e la comprensione dei metodi disponibili.

Ad esempio:

* `http://localhost:4502/content/graphiql.html`

Offre funzioni quali evidenziazione della sintassi, completamento automatico, suggerimenti automatici, nonché una cronologia e una documentazione online:

![Interfaccia di GraphiQL](assets/cfm-graphiql-interface.png "Interfaccia di GraphiQL")

## Installazione dell’IDE di GraphiQL per AEM {#installing-graphiql-ide}

L’IDE GraphiQL è uno strumento di sviluppo, necessario solo per ambienti di livello inferiore, come un’istanza di sviluppo o locale. Pertanto, non è incluso nel progetto AEM, ma viene fornito come pacchetto separato che può essere installato all’occorrenza.

1. Vai a **[Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)** > **AEM as a Cloud Service**.
1. Cerca “GraphiQL” (assicurati di includere **i** in **GraphiQL**.
1. Scarica la versione più recente del **pacchetto di contenuti GraphiQL v.x.x.x**
1. Dal menu **Start di AEM**, vai a **Strumenti** > **Distribuzione** > **Pacchetti**.
1. Fai clic su **Carica pacchetto**, quindi seleziona il pacchetto scaricato nel passaggio precedente. Per installare il pacchetto, fai clic su **Installa**.
