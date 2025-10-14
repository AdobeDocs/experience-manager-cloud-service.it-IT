---
title: Configurazione di Cross-Origin Resource Sharing (CORS) con AEM Headless
description: La condivisione CORS (Cross-Origin Resource Sharing) di Adobe Experience Manager consente alle applicazioni web headless di effettuare chiamate lato client a AEM. È necessaria una configurazione CORS per abilitare l’accesso all’endpoint GraphQL.
feature: Headless, GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
solution: Experience Manager
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 89%

---

# Configurazione di Cross-Origin Resource Sharing (CORS)

>[!CAUTION]
>
>Se la memorizzazione nella cache di [&#x200B; in Dispatcher è stata abilitata](/help/headless/deployment/dispatcher-caching.md), il filtro CORS non è necessario e quindi questa sezione può essere ignorata.

>[!NOTE]
>
>Per una panoramica dettagliata della politica di condivisione delle risorse CORS in AEM vedi [Comprendere la condivisione CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=it#understand-cross-origin-resource-sharing-(cors)).

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS e aggiungerlo a un progetto AEM [implementato in AEM tramite Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati. È possibile creare e distribuire più configurazioni CORS in ambienti diversi. Puoi trovare alcuni esempi nel [sito di riferimento WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig).

La configurazione CORS deve specificare un’origine del sito web attendibile `alloworigin` o `alloworiginregexp` per la quale deve essere consentito l’accesso.

Il file di configurazione deve essere denominato nel seguente modo: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` dove `appname` riflette il nome dell’applicazione.

Ad esempio, per consentire l’accesso all’endpoint GraphQL `/content/cq:graphql/wknd/endpoint` e all’endpoint con query persistenti per `https://my.domain` puoi utilizzare:

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se hai configurato un percorso personalizzato per l’endpoint, puoi utilizzarlo in `allowedpaths`.
