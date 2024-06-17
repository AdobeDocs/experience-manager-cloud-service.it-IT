---
title: Risolvere i problemi relativi alle query GraphQL persistenti
description: Scopri come risolvere i problemi relativi alle query GraphQL persistenti in Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
source-git-commit: 736fbc28c800c1c181721df7e0d7feed143642d9
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Risoluzione dei problemi relativi alle query GraphQL persistenti {#troubleshoot-persisted-graphql-queries}

Il [Centro azioni](/help/operations/actions-center.md) include **Errore di query persistente GraphQL** attenzione. Ciò significa che vieni informato ogni volta che una delle query persistenti di GraphQL genera un errore.

Per aiutarti a risolvere questi problemi, questa pagina descrive *più comune* cause degli errori e passaggi per risolverli.

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

Quando le query persistenti restituiscono `404` codice di errore, insieme alle informazioni `No suitable endpoint found`, significa che nell’ambiente AEM non è configurato alcun endpoint GraphQL.

Per risolvere questo problema, segui la procedura per abilitare e pubblicare l’endpoint da [Gestire gli endpoint GraphQL nell’AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Percorso mancante nell’URL della query persistente di GraphQL {#missing-path-query-url}

Se le query persistenti restituiscono `400` codice di errore con le informazioni `Suffix: '/' does not contain a path`, il servlet GraphQL viene chiamato senza un suffisso di percorso.

Il pattern deve essere `/graphql/execute.json/thePath`.

## Bloccato a causa di elenco consentiti IP {#blocked-due-to-ip-allow-list}

In questo caso, la query restituisce `405` codice di errore.

Un errore di questo tipo non è specifico di GraphQL. Consulta l’articolo KB [Errore 405 non consentito](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Bloccato da Dispatcher {#blocked-dispatcher}

Se l’endpoint GraphQL restituisce `404` errore durante la pubblicazione per `POST` questo significa che le query GraphQL sono bloccate a livello di Dispatcher e che l’endpoint deve essere abilitato manualmente.

Questo non dovrebbe accadere per impostazione predefinita, ma il problema potrebbe essere causato da una configurazione del dispatcher personalizzata. Vedi altro sotto [Dispatcher: configurazione dell’endpoint con AEM Headless](/help/headless/deployment/dispatcher.md).
