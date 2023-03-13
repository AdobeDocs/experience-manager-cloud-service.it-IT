---
title: Cos’è un CMS headless?
description: Scopri di più sui CMS headless. Come funzionano? Quali sono le alternative e le differenze? Perché utilizzare un CMS headless?
exl-id: 53f24f69-ad49-4b8e-9a91-36cd64c1f2b9
source-git-commit: 3306bde7b94b9f863b57d36542e8822df38c79ba
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 100%

---

# Cos’è un CMS headless? {#what-is-a-headless-cms}

La gestione dei contenuti headless è uno sviluppo chiave per la progettazione web di oggi che consente di separare le applicazioni front-end lato client dal sistema di gestione dei contenuti (CMS, content management system) back-end. Un CMS headless è quindi responsabile dei servizi di gestione dei contenuti (back-end), insieme ai meccanismi che consentono alle applicazioni (front-end) di accedere a tali contenuti.

Ma cosa significa veramente questo termine? Qui offriamo una rapida introduzione ai concetti chiave.

## Che cos’è un sistema di gestione dei contenuti (CMS)? {#content-management-system}

Cominciamo dalle nozioni di base: cos’è un sistema di gestione dei contenuti?

Un sistema di gestione dei contenuti (CMS, content management system) archivia, gestisce e distribuisce i contenuti utilizzati per fornire esperienze online.

## CMS tradizionale {#traditional-cms}

In genere, un CMS include sia le funzionalità back-end di archiviazione e distribuzione dei contenuti, sia la tecnologia front-end utilizzata per il rendering del linguaggio markup al fine di creare l’esperienza che verrà visualizzata dal browser (il livello di presentazione).

Si tratta di uno strumento molto potente, che offre il pieno controllo del contenuto e della formattazione, ma a cui manca parte della flessibilità necessaria negli ambienti di oggi che richiedono elevate velocità, ad esempio nell’interazione con applicazioni esterne.

## CMS headless {#headless-cms}

Con un sistema di gestione dei contenuti headless, il back-end e il front-end sono ora separati, o “disaccoppiati”.

La parte headless è il back-end del contenuto, in quanto un sistema di gestione dei contenuti headless è un sistema di gestione dei contenuti (CSM) solo back-end, progettato e creato esplicitamente come archivio dei contenuti che li rende accessibili tramite un’API per la visualizzazione su qualsiasi dispositivo.

Il front-end, sviluppato e gestito in modo indipendente, recupera il contenuto dal back-end headless tramite un’API di distribuzione dei contenuti, in genere in formato JSON. Ad esempio, potrebbe trattarsi di un’applicazione React o Angular (applicazione a pagina singola).

Un back-end CMS headless richiede in genere la struttura del contenuto, in base a un modello o a uno schema. Questo facilita le applicazioni client che richiedono il contenuto giusto per il rendering di un’esperienza. Alcuni CMS possono esporre contenuti strutturati e non strutturati in formato JSON.

Una caratteristica chiave di questa topologia è che il contenuto fornito dal CMS headless in formato JSON è contenuto puro, senza informazioni di progettazione o layout. In un’implementazione CMS headless, tutta la formattazione e il layout vengono mantenuti dall’applicazione front-end separata.

Un vantaggio chiave di una topologia CMS headless è la possibilità di riutilizzare i contenuti su più canali, che possono utilizzare implementazioni front-end lato client diverse. Ciò può rendere il processo di sviluppo del front-end più efficiente. Ma significa anche che il processo di sviluppo delle esperienze front-end può diventare molto orientato al codice e all’IT, a tal punto che sarà l’IT a gestire l’esperienza.

## API per la distribuzione dei contenuti {#content-delivery-apis}

Un CMS headless può fornire uno o più modi per esporre i contenuti ad applicazioni lato client. Nella maggior parte dei casi utilizza API REST HTTP, API GraphQL o entrambe.

Anche se un’API REST può spesso sembrare un modo più semplice di richiedere il contenuto (ad esempio, fornendo JSON per tutti i contenuti che corrispondono a un criterio), in genere consegna troppo contenuto a un’applicazione client. Questo può comportare la necessità da parte del client di analizzare e filtrare il contenuto effettivamente necessario per il rendering.

GraphQL, al contrario, si basa su un meccanismo più mirato che consente alle applicazioni client di richiedere esattamente il contenuto necessario per riprodurre un’esperienza.

## CMS full-stack {#fullstack-cms}

Un CMS full-stack solitamente rappresenta la topologia tradizionale per la gestione e la distribuzione dei contenuti, includendo la tecnologia di back-end e front-end per la riproduzione delle esperienze. La distribuzione dei contenuti in CMS full-stack si verifica solitamente rispetto alle API di distribuzione dei contenuti interne. La funzionalità front-end è tipicamente specifica per il CMS full-stack. Questa combinazione di tecnologia front-end con back-end di contenuto offre il vantaggio chiave di consentire la creazione di esperienze WYSIWYG (What-you-see-is-what-you-get).

## CMS ibrido {#hybrid-cms}

Una moderna evoluzione del CMS full-stack può essere il CMS ibrido. L’obiettivo è quello di combinare il meglio di entrambi i mondi:

* uno sviluppo front-end efficiente su tutti i canali utilizzando strumenti moderni,
* mantenendo al tempo stesso un approccio WYSIWYG alla creazione delle esperienze, per rendere autonomi gli utenti non tecnici ed evitare colli di bottiglia all’IT per la gestione di contenuti ed esperienze tra organizzazioni diverse.

Ciò si ottiene adottando framework front-end moderni come React, mantenendo però un minimo essenziale di associazione con il back-end dei contenuti.

## CMS disaccoppiato {#decoupled-cms}

Mentre il termine CMS disaccoppiato a volte viene utilizzato indipendentemente, in pratica descrive un back-end CMS headless sottolineandone la caratteristica chiave di essere separato dall’applicazione front-end lato client.

## CMS headful {#headful-cms}

Questo è un altro termine che indica un CMS tradizionale.

## Ulteriori informazioni {#further-reading}

Per ulteriori informazioni sull’utilizzo di AEM in una topologia CMS headless, consulta:

* [Introduzione ad Adobe Experience Manager come CMS headless](/help/headless/introduction.md)
