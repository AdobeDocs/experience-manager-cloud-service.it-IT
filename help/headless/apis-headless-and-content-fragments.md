---
title: API AEM per la distribuzione strutturata dei contenuti e la gestione dei frammenti di contenuto
description: Scopri le API disponibili per la distribuzione strutturata dei contenuti e la gestione dei frammenti di contenuto
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# API AEM per la distribuzione e la gestione strutturata dei contenuti {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service offre più API per la distribuzione di contenuti strutturati da frammenti di contenuto e per la gestione dei frammenti di contenuto. Per ulteriori dettagli sulle API specifiche, consulta le singole pagine.

* [REST OpenAPI per AEM per la distribuzione dei frammenti di contenuto](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
   * Questa API crea risposte JSON per la distribuzione di contenuti strutturati da frammenti di contenuto in AEM.
   * Utilizza come endpoint il percorso di un frammento di contenuto.
   * Questa API è basata su REST.
   * È ottimizzato per la distribuzione dei contenuti, inclusa l’integrazione CDN.
* [API GraphQL dell’AEM per la distribuzione dei frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
   * Questa API è basata su schema. Gli schemi API sono rappresentati da Modelli per frammenti di contenuto, che definiscono la struttura del contenuto.
   * Questa API è basata su GraphQL.
* [Frammenti di contenuto e modelli per frammenti di contenuto OpenAPI](/help/headless/content-fragment-openapis.md)
   * Queste API sono destinate alla gestione di contenuti strutturati.
   * I rispettivi operatori di GET non sono ottimizzati per la distribuzione dei contenuti.
   * Questa API è basata su REST.
* [Supporto per frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
   * L’API originale per l’output JSON per la distribuzione di contenuti strutturati in AEM.
      * Benché solida e comprovata, questa API non fornisce l&#39;output JSON *completamente idratato*. I riferimenti vengono generati solo come percorsi, e richiedono richieste API secondarie per recuperare ulteriore contenuto.
   * L’API HTTP di Assets può essere utilizzata anche per la gestione dei Frammenti di contenuto e dei Modelli per frammenti di contenuto (CRUD).
   * Questa API è basata su REST.
   * In futuro, il supporto per i frammenti di contenuto nell’API HTTP di Assets diventerà obsoleto in quanto verrà sostituito dall’API REST JSON per i Edge Delivery Services. La tempistica non è ancora stata decisa.

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

## REST e GRAPHQL {#rest-vs-graphql}

L’API utilizzata è una decisione per gli sviluppatori: l’AEM supporta entrambi.

Molti confronti sono disponibili online, ma alcuni punti salienti e vantaggi di REST includono:

* Semplicità

   * Gli sviluppatori hanno (spesso) familiarità con HTTP e REST. In base al [rapporto Stato Postman delle API](https://www.postman.com/state-of-api/), un&#39;alta percentuale di sviluppatori utilizza REST.

   * Con la semplicità si arriva alla familiarità. Con REST non ci sono domande organizzative su chi è il proprietario delle query e chi è il proprietario dell’app, mentre queste domande possono sorgere con GraphQL.

   * Con la familiarità (tipicamente) viene fornito un ampio panorama di comunità e strumenti. Non è uno svantaggio intrinseco di GraphQL, ma è probabile che sia più ampio e profondo per REST.

   * L&#39;approccio più semplice può anche semplificare l&#39;implementazione della sicurezza. Con REST, il filtro per determinare il contenuto di cui eseguire il rendering si verifica nell’app client. Con GraphQL questo si verifica in una query basata su schema tra client e server.

* Flessibilità

   * Con REST, lo sviluppatore può `GET` qualsiasi risorsa. Con GraphQL sono limitati alle risorse definite all’interno di uno schema.

* Memorizzazione in cache

   * Le risposte JSON alle richieste REST `GET` sono intrinsecamente memorizzabili nella cache. Le richieste di GraphQL `POST` non possono essere memorizzate nella cache, a meno che non vengano effettuate in questo modo, ad esempio utilizzando query persistenti AEM memorizzate nel server e richieste con `GET` richieste simili a REST.

I vantaggi di GraphQL includono:

* Efficienza nella distribuzione dei contenuti

   * Stato attivo

      * Con GraphQL le applicazioni client possono richiedere il contenuto esatto necessario per il rendering e non più. Questo approccio evita la distribuzione eccessiva dei contenuti, con carichi utili eccessivi dei contenuti e un inutile consumo di larghezza di banda.

   * Endpoint singolo

      * Mentre nel REST ogni richiesta API è un endpoint, in GraphQL esiste un solo endpoint comune e diverse richieste di contenuto vengono espresse come query che utilizzano tale endpoint comune.

* Prototipizzazione rapida

   * Con GraphQL si tratta di un processo in un’unica fase, integrato nella query di GraphQL, che può semplificare la creazione di prototipi. REST è invece un processo in due fasi:

      1. Recupera il contenuto con API.
      2. Nella risposta JSON, determina cosa utilizzare per il rendering nell’app client.