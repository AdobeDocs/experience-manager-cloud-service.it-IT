---
title: Configurazione dell’endpoint di Dispatcher con AEM Headless
description: Dispatcher è un livello di memorizzazione in cache e sicurezza davanti agli ambienti di pubblicazione Adobe Experience Manager. Diverse configurazioni vengono utilizzate per aprire gli endpoint GraphQL alle applicazioni headless.
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 94%

---


# Dispatcher: configurazione dell’endpoint con AEM Headless

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) è un livello di caching e sicurezza davanti agli ambienti di pubblicazione Adobe Experience Manager. Per impostazione predefinita, sono incluse diverse configurazioni per aprire gli endpoint GraphQL alle applicazioni headless.

>[!NOTE]
>
>Per la documentazione dettagliata su Dispatcher consulta la sezione [Guida a Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it).

In un progetto AEM è incluso un modulo Dispatcher che contiene configurazioni per il Dispatcher. I progetti generati di recente da [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype) includono automaticamente [filtri](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it#defining-a-filter) che abilitano gli endpoint GraphQL.

## Endpoint GraphQL

Come parte dei filtri predefiniti, [Endpoint GraphQL](/help/headless/graphql-api/graphql-endpoint.md) sono aperti con la seguente regola:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

Il carattere jolly `*` apre più endpoint sull’istanza AEM. La query tramite un endpoint GraphQL viene eseguita utilizzando `POST` e la risposta **non** viene memorizzata nella cache.

## Query persistenti GraphQL

La richiesta di query persistenti viene eseguita su un endpoint diverso. Nella configurazione del filtro predefinita, l’URL di [Query persistenti](/help/headless/graphql-api/persisted-queries.md) è aperto con la seguente regola:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

È possibile richiedere query persistenti utilizzando `GET`, memorizzando nella cache la risposta a livello di Dispatcher e CDN. Ulteriori dettagli sulla memorizzazione in cache e sull’annullamento della validità della cache sono disponibili [qui](/help/implementing/dispatcher/caching.md).
