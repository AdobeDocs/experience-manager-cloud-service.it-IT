---
title: Come aggiornare i contenuti tramite API di AEM
description: In questa sezione del Percorso per sviluppatori AEM Headless, scopri come utilizzare le API disponibili per accedere e aggiornare il contenuto dei frammenti di contenuto.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d8e4fdc4f79e40a43a6845ab083dc231444b9c99
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 33%

---

# Come aggiornare i contenuti tramite API di AEM {#update-your-content}

In questa sezione del [Percorso di sviluppatori AEM Headless](overview.md), scopri come utilizzare le API disponibili per accedere e aggiornare il contenuto dei frammenti di contenuto.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso headless di AEM, [Come accedere ai contenuti utilizzando API di distribuzione di AEM](access-your-content.md) hai imparato ad accedere ai contenuti headless in AEM utilizzando l’API GraphQL AEM e ora dovresti aver appreso quanto segue:

* Conoscenza generale di GraphQL.
* Come funziona l’API GraphQL di AEM.
* Alcune query pratiche di esempio.

Questo articolo si basa su questi elementi fondamentali per comprendere come aggiornare i contenuti headless esistenti in AEM tramite le API disponibili.

## Obiettivo {#objective}

* **Pubblico**: avanzato
* **Obiettivo**: scopri le API disponibili per accedere e aggiornare il contenuto dei frammenti di contenuto.

## API di AEM da utilizzare con frammenti di contenuto {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service offre più API sia per la distribuzione strutturata dei contenuti dai frammenti di contenuto che per la gestione dei frammenti di contenuto. Per ulteriori dettagli sulle API specifiche, consulta le singole pagine.

* OpenAPI REST AEM per la consegna dei frammenti di contenuto
   * Questa API crea risposte JSON per la distribuzione di contenuti strutturati da frammenti di contenuto in AEM.
   * Utilizza come endpoint il percorso di un frammento di contenuto.
   * Questa API è basata su REST.
   * È ottimizzato per la distribuzione dei contenuti, inclusa l’integrazione CDN.
* API GraphQL di AEM per la distribuzione dei frammenti di contenuto
   * Questa API è basata su schema. Gli schemi API sono rappresentati da Modelli per frammenti di contenuto, che definiscono la struttura del contenuto.
   * Questa API è basata su GraphQL.
* Frammenti di contenuto e modelli per frammenti di contenuto OpenAPI
   * Queste API sono destinate alla gestione di contenuti strutturati.
   * I rispettivi operatori GET non sono ottimizzati per la distribuzione dei contenuti.
   * Questa API è basata su REST.
* Supporto per frammenti di contenuto nell’API HTTP di AEM Assets
   * API originale per l’output JSON per la distribuzione di contenuti strutturati in AEM.
      * Benché solida e comprovata, questa API non fornisce l&#39;output JSON *completamente idratato*. I riferimenti vengono generati solo come percorsi, e richiedono richieste API secondarie per recuperare ulteriore contenuto.
   * L’API HTTP di Assets può essere utilizzata anche per la gestione dei Frammenti di contenuto e dei Modelli per frammenti di contenuto (CRUD).
   * Questa API è basata su REST.
   * In futuro, il supporto per i frammenti di contenuto nell’API HTTP di Assets diventerà obsoleto in quanto verrà sostituito dall’API REST JSON di Edge Delivery Services. La tempistica non è ancora stata decisa.

## Passaggio successivo {#whats-next}

Ora che hai completato questa parte del percorso per sviluppatori di AEM headless, dovresti aver appreso quanto segue:

* Comprendere le API di AEM disponibili.
* Scopri come i frammenti di contenuto sono supportati in queste API.

Continua il tuo percorso AEM headless rivedendo il documento successivo [Come mettere tutto insieme - La tua app e il tuo contenuto in AEM headless](put-it-all-together.md) dove acquisire familiarità con le nozioni di base e gli strumenti dell’architettura AEM necessari per mettere insieme l’applicazione.

## Risorse aggiuntive {#additional-resources}

* [API di Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [API AEM per la consegna e la gestione di contenuti strutturati](/help/headless/apis-headless-and-content-fragments.md)
* [OpenAPI REST AEM per la consegna dei frammenti di contenuto](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
* [API GraphQL di AEM per la distribuzione dei frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)
* [Frammenti di contenuto e modelli per frammenti di contenuto OpenAPI](/help/headless/content-fragment-openapis.md)
* [Supporto per frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
* [Utilizzo di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md)
* [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
* [Spiegazione di CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=it)
* [Video: sviluppo per CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=it)
* [Introduzione ad AEM come CMS headless](/help/headless/introduction.md)
* [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
