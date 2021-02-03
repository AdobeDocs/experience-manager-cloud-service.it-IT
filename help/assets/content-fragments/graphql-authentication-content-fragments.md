---
title: Autenticazione per query AEM GraphQL remote su frammenti di contenuto
description: Informazioni sull'autenticazione necessaria per le query Remote AEM GraphQL.
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autenticazione per query AEM GraphQL remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d&#39;uso principale per L&#39;API [Adobe Experience Manager come Cloud Service (AEM) GraphQL per la distribuzione dei frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md) è accettare query remote da applicazioni o servizi di terze parti.  Queste query remote possono richiedere l&#39;accesso API autenticato.

>[!NOTE]
>
>Per il test e lo sviluppo è inoltre possibile accedere all&#39;API AEM GraphQL direttamente utilizzando l&#39;interfaccia [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Per l&#39;autenticazione, il servizio di terze parti deve utilizzare un [Token di accesso](#access-token), che può quindi essere [utilizzato nella Richiesta GraphQL](#use-access-token-in-graphql-request).

## Recupero di un token di accesso {#retrieving-access-token}

Per informazioni dettagliate, consultate [Generazione di token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

## Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un&#39;istanza AEM, deve disporre di un *Token di accesso*. Il servizio deve quindi aggiungere questo token all&#39;intestazione `Authorization` nella richiesta di POST.

Ad esempio, un&#39;intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisiti di autorizzazione {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso saranno in realtà eseguite *dall&#39;account utente che ha generato il token*.

Ciò significa che devi verificare che l&#39;account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

È possibile controllare questo utilizzando GraphiQL nell&#39;istanza locale.
