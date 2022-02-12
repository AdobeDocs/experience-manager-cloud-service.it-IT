---
title: Configurazione di Cross-Origin Resource Sharing (CORS) con AEM Headless
description: La condivisione delle risorse tra le origini di Adobe Experience Manager (Cross-Origin Resource Sharing, CORS) consente alle applicazioni web headless di effettuare chiamate a AEM lato client. È necessaria una configurazione CORS per abilitare l’accesso all’endpoint GraphQL.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Configurazione di Cross-Origin Resource Sharing (CORS)

>[!NOTE]
>
>Per una panoramica dettagliata della politica di condivisione delle risorse CORS in AEM vedi [Comprendere la condivisione delle risorse tra le origini (CORS, Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS e aggiungerlo a un progetto AEM [implementato in AEM tramite Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati. È possibile creare e distribuire più configurazioni CORS in ambienti diversi. Gli esempi si trovano nella sezione [Sito di riferimento WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

La configurazione CORS deve specificare un’origine sito web attendibile `alloworigin` o `alloworiginregexp` per i quali deve essere concesso l&#39;accesso.

Il file di configurazione deve essere denominato come: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` dove `appname` riflette il nome dell&#39;applicazione.

Ad esempio, per concedere l’accesso all’endpoint GraphQL `/content/cq:graphql/wknd/endpoint` e endpoint query persistenti per `https://my.domain` puoi utilizzare:

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

Se hai configurato un percorso personalizzato per l’endpoint, puoi anche utilizzarlo in `allowedpaths`.


