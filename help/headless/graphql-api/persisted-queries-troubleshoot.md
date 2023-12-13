---
title: Risolvere i problemi relativi alle query GraphQL persistenti
description: Scopri come risolvere i problemi relativi alle query GraphQL persistenti in Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Risoluzione dei problemi relativi alle query GraphQL persistenti {#troubleshoot-persisted-graphql-queries}

Il [Centro azioni](/help/operations/actions-center.md) include **Errore di query persistente GraphQL** attenzione. Ciò significa che vieni informato ogni volta che una delle query persistenti di GraphQL genera un errore.

Per aiutarti a risolvere questi problemi, ti spieghiamo le *più comune* cause degli errori e passaggi per risolverli.

## Modifiche al modello per frammenti di contenuto {#changes-to-content-fragment-model}

Una query persistente di GraphQL può non riuscire quando è basata su tipi di GraphQL obsoleti, spesso a causa di una modifica nei modelli dei frammenti di contenuto sottostanti.

Questo può accadere per una serie di motivi. Ad esempio, quando un autore del modello di contenuto:

* rimuove o rinomina un campo
* aggiorna i modelli consentiti definiti per un riferimento frammento
* annulla la pubblicazione di un modello a cui fanno riferimento altri modelli
* altre azioni e motivi

Per risolvere questo problema:

* la query persistente che non riesce deve essere aggiornata per adattarsi alla modifica nel modello Frammento di contenuto
* o la modifica apportata al modello che ha introdotto il problema deve essere ripristinata

## Endpoint GraphQL non configurato {#graphql-endpoint-not-configured}

Quando le query persistenti restituiscono `400` o `500` codice di errore, insieme alle informazioni `No suitable endpoint found`, significa che nell’ambiente AEM non è configurato alcun endpoint GraphQL.

Per risolvere questo problema, segui la procedura per abilitare e pubblicare l’endpoint da [Gestire gli endpoint GraphQL nell’AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Percorso mancante nell’URL della query persistente di GraphQL {#missing-path-query-url}

Se le query persistenti restituiscono `400` o `500` codice di errore con le informazioni `Suffix: '/' does not contain a path`, il servlet GraphQL viene chiamato senza un suffisso di percorso.

Il pattern deve essere `/graphql/execute.json/thePath`.

## Bloccato a causa di elenco consentiti IP {#blocked-due-to-ip-allow-list}

In questo caso, la query restituisce `405` codice di errore.

Questo non è un aspetto specifico di GraphQL. Consulta l’articolo KB [Errore 405 non consentito](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## Bloccato da Dispatcher {#blocked-dispatcher}

Se l’endpoint GraphQL restituisce `404` errore durante la pubblicazione per `POST` questo significa che le query GraphQL sono bloccate a livello di Dispatcher e che l’endpoint deve essere abilitato manualmente.

Questo non dovrebbe accadere per impostazione predefinita, ma il problema potrebbe essere causato da una configurazione del dispatcher personalizzata. Vedi altro sotto [Dispatcher: configurazione dell’endpoint con AEM Headless](/help/headless/deployment/dispatcher.md).
