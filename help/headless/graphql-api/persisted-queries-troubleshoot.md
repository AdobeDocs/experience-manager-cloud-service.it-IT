---
title: Risolvere i problemi relativi alle query GraphQL persistenti
description: Scopri come risolvere i problemi relativi alle query GraphQL persistenti in Adobe Experience Manager as a Cloud Service.
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Risoluzione dei problemi relativi alle query GraphQL persistenti {#troubleshoot-persisted-graphql-queries}

Il [Centro azioni](/help/operations/actions-center.md) include l&#39;avviso **Errore di query persistente di GraphQL**. Ciò significa che vieni informato ogni volta che una delle query persistenti di GraphQL genera un errore.

Per aiutarti a risolvere questi problemi, in questa pagina sono illustrate le *cause più comuni* degli errori e i passaggi per risolverli.

## Modifiche al modello per frammenti di contenuto {#changes-to-content-fragment-model}

Una query persistente di GraphQL può non riuscire quando è basata su tipi di GraphQL obsoleti, spesso a causa di una modifica nei modelli dei frammenti di contenuto sottostanti.

Tali errori possono verificarsi per una serie di motivi. Alcuni esempi includono (l’elenco non è esaustivo), quando l’autore di un modello per frammenti di contenuto:

* rimuove o rinomina un campo
* aggiorna il **Tipo di modello** che definisce i modelli consentiti per il riferimento al frammento
* non pubblica un modello a cui fanno riferimento altri modelli

Per risolvere tali errori, è necessario:

* aggiorna la query persistente che non soddisfa le modifiche apportate al modello per frammenti di contenuto
* ripristina la modifica nel modello che ha introdotto il problema

## Endpoint GraphQL non configurato {#graphql-endpoint-not-configured}

Quando le query persistenti restituiscono il codice di errore `404`, insieme alle informazioni `No suitable endpoint found`, significa che nell&#39;ambiente AEM non è configurato alcun endpoint GraphQL.

Per risolvere il problema, seguire la procedura per abilitare e pubblicare l&#39;endpoint da [Gestione endpoint GraphQL nell&#39;AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Percorso mancante nell’URL della query persistente di GraphQL {#missing-path-query-url}

Se le query persistenti restituiscono il codice di errore `400` con le informazioni `Suffix: '/' does not contain a path`, il servlet GraphQL verrà chiamato senza un suffisso di percorso.

Il modello deve essere `/graphql/execute.json/thePath`.

## Bloccato a causa di elenco consentiti IP {#blocked-due-to-ip-allow-list}

In questo caso, la query restituisce il codice di errore `405`.

Un errore di questo tipo non è specifico di GraphQL. Vedere l&#39;articolo della Knowledge Base [405 Errore non consentito](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Bloccato da Dispatcher {#blocked-dispatcher}

Se l&#39;endpoint GraphQL restituisce l&#39;errore `404` in fase di pubblicazione per le richieste `POST`, significa che le query GraphQL sono bloccate a livello di Dispatcher e che l&#39;endpoint deve essere abilitato manualmente.

Questo non dovrebbe accadere per impostazione predefinita, ma il problema potrebbe essere causato da una configurazione del dispatcher personalizzata. Vedi altro in [Dispatcher - Configurazione endpoint con AEM Headless](/help/headless/deployment/dispatcher.md).
