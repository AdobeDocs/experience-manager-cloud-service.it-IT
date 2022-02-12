---
title: Autenticazione per query GraphQL AEM remote su frammenti di contenuto
description: Comprendere l’autenticazione necessaria per le query GraphQL AEM remote al fine di proteggere la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---

# Autenticazione per query GraphQL AEM remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d’uso principale per [API GraphQL di Adobe Experience Manager as a Cloud Service (AEM) per la distribuzione di frammenti di contenuto](/help/headless/graphql-api/content-fragments.md) accetta query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione di contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è inoltre possibile accedere all’API GraphQL AEM direttamente utilizzando l’ [Interfaccia GraphiQL](/help/headless/graphql-api/graphiql-ide.md) interfaccia.

Per l&#39;autenticazione, il servizio di terze parti deve [recuperare un token di accesso](#retrieving-access-token), che può essere [utilizzato nella richiesta GraphQL](#use-access-token-in-graphql-request).

## Recupero di un token di accesso {#retrieving-access-token}

Vedi [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) per informazioni complete.

## Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un&#39;istanza AEM, deve disporre di un *Token di accesso*. Il servizio deve quindi aggiungere questo token al `Authorization` intestazione nella richiesta POST.

Ad esempio, un’intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisiti delle autorizzazioni {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso verranno effettivamente effettuate *dall’account utente che ha generato il token*.

Ciò significa che devi verificare che l’account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

Puoi controllare questo usando GraphiQL sull&#39;istanza locale. Maggiori dettagli [le autorizzazioni sono disponibili qui](/help/headless/security/permissions.md).
