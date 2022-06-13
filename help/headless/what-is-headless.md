---
title: Cos'è un CMS headless?
description: Scopri di più su Headless CMS. Come funzionano? Quali sono le alternative e le differenze? Perché utilizzare un CMS headless?
source-git-commit: 35064ef7d9a4a3f2368667be02b11840b29d56f0
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# Cos&#39;è un CMS headless? {#what-is-a-headless-cms}

La gestione dei contenuti headless è uno sviluppo chiave per la progettazione web di oggi che consente di separare le applicazioni front-end lato client dal sistema di gestione dei contenuti back-end. Un CMS headless è quindi responsabile dei servizi di gestione dei contenuti (back-end), insieme ai meccanismi che consentono alle applicazioni (front-end) di accedere a tali contenuti.

Ma cosa significa veramente questo termine? Qui offriamo un’introduzione (molto rapida) ai concetti chiave.

## Che cos’è un sistema di gestione dei contenuti (CMS)? {#content-management-system}

Cominciamo dalle nozioni di base: cos’è un sistema di gestione dei contenuti?

Un sistema di gestione dei contenuti (CMS) archivia, gestisce e distribuisce i contenuti utilizzati per fornire esperienze online.

## CMS tradizionale {#traditional-cms}

In genere, un CMS include sia la funzionalità back-end per l’archiviazione e la distribuzione dei contenuti, sia la tecnologia front-end utilizzata per eseguire il rendering del markup per un’esperienza che verrà visualizzata dal browser (il livello di presentazione).

Molto potente, che offre il pieno controllo del contenuto e della formattazione, ma manca parte della flessibilità necessaria nell&#39;ambiente in rapido movimento di oggi; ad esempio, quando si interagisce con applicazioni esterne.

## CMS headless {#headless-cms}

Con un sistema di gestione dei contenuti headless, il back-end e la front-end sono ora disaccoppiati.

La parte headless è il backend del contenuto.

* &quot;*Un sistema di gestione dei contenuti headless, o CMS headless, è un sistema di gestione dei contenuti (CMS) di back-end basato su un archivio di contenuti che rende i contenuti accessibili tramite un’API per la visualizzazione su qualsiasi dispositivo.*

   Vedi [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

Il front-end, sviluppato e gestito in modo indipendente, recupera il contenuto dal backend headless utilizzando un’API di distribuzione dei contenuti, in genere in formato JSON. Ad esempio, potrebbe trattarsi di un’applicazione React o Angular (applicazione a pagina singola (SPA)).

Un backend CMS headless richiede in genere la struttura del contenuto, in base a un modello o a uno schema. Questo facilita le applicazioni client che richiedono il contenuto giusto per il rendering di un’esperienza. Alcuni CMS possono esporre contenuti strutturati e non strutturati in formato JSON.

Una caratteristica chiave di questa topologia è che il contenuto servito da CMS headless in formato JSON è contenuto puro, senza informazioni di progettazione o layout. In un&#39;implementazione CMS headless, tutta la formattazione e il layout vengono mantenuti dall&#39;applicazione front-end disaccoppiata.

Un vantaggio chiave di una topologia CMS headless è la possibilità di riutilizzare i contenuti su più canali, che possono utilizzare implementazioni frontend lato client diverse. Ciò può rendere il processo di sviluppo frontale più efficiente. Ma significa anche che il processo di sviluppo delle esperienze può diventare molto orientato al codice e all&#39;IT, con l&#39;IT che essenzialmente possiede l&#39;esperienza.

## API per la distribuzione dei contenuti {#content-delivery-apis}

Un CMS headless può fornire uno o più modi per esporre i contenuti ad applicazioni lato client. Nella maggior parte dei casi, API REST HTTP, API GraphQL o entrambe.

Anche se un’API REST può spesso sembrare un modo più semplice di richiedere il contenuto (ad esempio, fornendo JSON per tutti i contenuti che corrispondono a un criterio), in genere consegnano troppo contenuto a un’applicazione client. Questo può comportare la necessità da parte del client di analizzare e filtrare il contenuto effettivamente necessario per il rendering.

GraphQL per contrasto è un meccanismo più mirato per consentire alle applicazioni client di eseguire query per individuare esattamente il contenuto necessario per eseguire il rendering di un’esperienza.

## CMS full-stack {#fullstack-cms}

Un CMS Full-Stack solitamente rappresenta la topologia tradizionale per la gestione e la distribuzione dei contenuti, includendo la tecnologia di back-end e front-end per le esperienze di rendering. La distribuzione dei contenuti in CMS con stack completo si verifica solitamente rispetto alle API di distribuzione dei contenuti interne. La funzionalità front-end è tipicamente specifica per il CMS completo. Questa combinazione di tecnologia front-end e content back-end consente di ottenere l&#39;authoring di esperienze WYSIWYG (What-you-see-is-what-you-get) come vantaggio chiave.

## CMS ibrido {#hybrid-cms}

Una moderna evoluzione del CMS a pieno stack può essere un CMS ibrido. L&#39;obiettivo è quello di combinare il meglio di entrambi i mondi:

* sviluppo frontale efficiente su tutti i canali utilizzando strumenti frontend moderni,
* mantenendo al tempo stesso l’authoring di esperienze WYSIWYG per consentire agli utenti non tecnici e per evitare che l’IT diventi un collo di bottiglia per la gestione di contenuti ed esperienze tra organizzazioni diverse.

Ciò si ottiene adottando framework frontend moderni come React, mantenendo però un minimo essenziale di associazione con il back-end dei contenuti.

## CMS disaccoppiato {#decoupled-cms}

Mentre il termine CMS disaccoppiato a volte viene utilizzato indipendentemente, essenzialmente descrive un backend CMS headless sottolineando la sua caratteristica chiave di essere disaccoppiato dall&#39;applicazione front-end lato client.

## CMS headful {#headful-cms}

Questo è un altro termine per un CMS tradizionale.

## Ulteriori informazioni {#further-reading}

Ulteriori informazioni sull&#39;utilizzo di AEM in una topologia CMS headless:

* [Introduzione ad Adobe Experience Manager as a Headless CMS](/help/headless/introduction.md)
