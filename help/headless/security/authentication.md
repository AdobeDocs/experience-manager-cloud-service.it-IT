---
title: Autenticazione per query GraphQL AEM remote su frammenti di contenuto
description: Comprendi l’autenticazione necessaria per le query remote su GraphQL AEM per proteggere la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 88%

---

# Autenticazione per query GraphQL AEM remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d’uso principale per [API GraphQL di Adobe Experience Manager as a Cloud Service (AEM) per la distribuzione di frammenti di contenuto](/help/headless/graphql-api/content-fragments.md) accetta query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione sicura dei contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è inoltre possibile accedere all’API GraphQL AEM direttamente utilizzando l’ [Interfaccia GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

Per l’autenticazione, il servizio di terze parti deve [recuperare un token di accesso](#retrieving-access-token), che può essere [utilizzato nella richiesta GraphQL](#use-access-token-in-graphql-request).

## Recupero di un token di accesso {#retrieving-access-token}

Per informazioni complete, consulta [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

## Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un’istanza AEM, deve disporre di un *Token di accesso*. Il servizio deve quindi aggiungere questo token all’`Authorization` intestazione nella richiesta POST.

Ad esempio, un’intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisiti delle autorizzazioni {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso verranno effettivamente effettuate *dall’account utente che ha generato il token*.

Ciò significa che devi verificare che l’account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

Puoi controllare questo usando GraphiQL sull’istanza locale. Maggiori dettagli sulle [autorizzazioni sono disponibili qui](/help/headless/security/permissions.md).
