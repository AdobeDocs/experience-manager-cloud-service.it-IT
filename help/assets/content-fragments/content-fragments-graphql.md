---
title: Headless Content Delivery using Content Fragments with GraphQL
description: Learn the basic concepts of realizing an AEM Headless CMS using Content Fragments with GraphQL for headless content delivery.
feature: Content Fragments, GraphQL API
topic: Headless
role: User
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
source-git-commit: f296e8cbc12c9426e0fefe6f5342374ba9b21291
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 17%

---

# Headless Content Delivery using Content Fragments with GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

With Content Fragments and the GraphQL API you can use Adobe Experience Manager (AEM) as a Cloud Service as a Headless Content Management System (CMS).

This is achieved using Content Fragments, together with the AEM GraphQL API (a customized implementation, based on standard GraphQL), to headlessly deliver structured content for use in your applications. The ability to customize a single API query allows you to retrieve and deliver the specific content that you want/need to render (as the response to the single API query).

>[!NOTE]
>
>[](/help/headless/introduction.md)

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [](/help/commerce-cloud/integrating/magento.md)
>* [I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/headless/graphql-api/content-fragments.md).


## Headless CMS {#headless-cms}

A Headless Content Management System (CMS) is:

* **

   [](https://en.wikipedia.org/wiki/Headless_content_management_system)

In terms of authoring Content Fragments in AEM this means that:

* You can use Content Fragments to author content that is not primarily intended to be directly published (1:1) on formatted pages.

* The content of your Content Fragments will be structured in a predetermined manner - according to the Content Fragment Models. This simplifies access for your applications, which will further process your content.

## GraphQL - An Overview {#graphql-overview}

GraphQL è:

* **

   Vedi [GraphQL.org](https://graphql.org)

[](#aem-graphql-api)[](/help/assets/content-fragments/content-fragments.md) The content returned can then be used by your applications.

## AEM GraphQL API {#aem-graphql-api}

For Adobe Experience as a Cloud Experience, a customized implementation of the standard GraphQL API has been developed. [](/help/headless/graphql-api/content-fragments.md)

[](https://graphql.org/code/#java)

## Content Fragments for use with the AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

[](#content-fragments)

* They enable you to design, create, curate and publish page-independent content.
* [](#content-fragments-models)
* [](#fragment-references)

![](assets/cfm-nested-01.png "")

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contain structured content.

* [](#content-fragments-models)

### Modelli per frammenti di contenuto {#content-fragments-models}

[](/help/assets/content-fragments/content-fragments-models.md)

* [](https://graphql.org/learn/schema/)****

* Provide the data types and fields required for GraphQL. They ensure that your application only requests what is possible, and receives what is expected.

* **[](#fragment-references)**

### Fragment References {#fragment-references}

**[](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**

* Is of particular interest in conjunction with GraphQL.

* Is a specific data type that can be used when defining a Content Fragment Model.

* References another fragment, dependent on a specific Content Fragment Model.

* Allows you to retrieve structured data.

   * ****

### Anteprima JSON {#json-preview}

[](/help/assets/content-fragments/content-fragments-json-preview.md)

## Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

[](/help/headless/graphql-api/sample-queries.md)

## Tutorial: guida introduttiva ad AEM headless e GraphQL

Cerchi un pratico tutorial? Dai un&#39;occhiata al tutorial [Guida introduttiva di headless AEM e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) che illustra come creare ed esporre contenuti, utilizzati da un’app esterna, mediante le API GraphQL di AEM in uno scenario CMS headless.
