---
title: Autenticazione per query GraphQL AEM remote su frammenti di contenuto
description: Comprendere l’autenticazione necessaria per le query GraphQL AEM remote al fine di proteggere la distribuzione di contenuti headless.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Autenticazione per query GraphQL AEM remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d&#39;uso principale per l&#39; [Adobe Experience Manager as a Cloud Service (AEM) API GraphQL per la distribuzione di frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md) è quello di accettare query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione di contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è inoltre possibile accedere all&#39;API GraphQL AEM direttamente utilizzando l&#39;interfaccia [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) .

Per l&#39;autenticazione, il servizio di terze parti deve utilizzare un [token di accesso](#access-token), che può quindi essere [utilizzato nella richiesta GraphQL](#use-access-token-in-graphql-request).

## Recupero di un token di accesso {#retrieving-access-token}

Per informazioni dettagliate, consulta [Generazione di token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) .

## Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un&#39;istanza AEM, deve disporre di un *token di accesso*. Il servizio deve quindi aggiungere questo token all’intestazione `Authorization` nella richiesta di POST.

Ad esempio, un’intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisiti delle autorizzazioni {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso saranno in realtà effettuate *dall&#39;account utente che ha generato il token*.

Ciò significa che devi verificare che l’account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

Puoi controllare questo usando GraphiQL sull&#39;istanza locale.
