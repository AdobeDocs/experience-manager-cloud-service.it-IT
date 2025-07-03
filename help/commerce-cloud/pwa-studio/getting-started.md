---
title: Guida introduttiva all’estensione AEM per PWA Studio
description: Scopri come distribuire un progetto AEM headless Content e Commerce con PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Guida introduttiva all’estensione AEM per PWA Studio {#getting-started-pwa}

PWA Studio si integra perfettamente con Adobe Commerce tramite GraphQL, fornendo opzioni illimitate per la creazione di vetrine innovative e coinvolgenti e altre esperienze digitali.

I frammenti di contenuto sono parti di contenuto con una struttura predefinita che consente di utilizzarli in modo headless utilizzando GraphQL come API in formati diversi (ad esempio, JSON, Markdown) e renderizzati in modo indipendente. I frammenti di contenuto includono tutti i tipi di dati e i campi necessari affinché GraphQL possa garantire che l’applicazione richieda solo ciò che è disponibile e riceva ciò che è previsto. La flessibilità che forniscono in termini di struttura li rende perfetti per l&#39;utilizzo in più posizioni e su più canali.

L’Editor modello per frammenti di contenuto in Adobe Experience Manager semplifica la progettazione della struttura necessaria. Il problema principale per l’integrazione di Frammenti di contenuto di Adobe Experience Manager (o di qualsiasi altro dato) con l’applicazione PWA Studio è il recupero di dati da più endpoint di GraphQL. Questo perché, come funzione predefinita, PWA Studio funziona con un singolo endpoint Adobe Commerce GraphQL.

## Architettura {#architecture}

![Architettura headless PWA](/help/commerce-cloud/assets/PWA-Studio_Architecture.png)

## Configura PWA Studio {#setup-pwa}

Segui la [documentazione di PWA Studio](https://developer.adobe.com/commerce/pwa-studio/tutorials/) di Adobe Commerce per configurare la tua app PWA Studio.

Per connettere PWA Studio all&#39;endpoint GraphQL di AEM, puoi utilizzare l&#39;estensione [AEM per PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Estrarre l’archivio

1. Nell&#39;applicazione PWA Studio, aggiungi l&#39;estensione come dipendenza di sviluppo.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Aggiungi il wrapper Apollo Link all’applicazione PWA Studio. In pwa-root/src/index.js, apporta le seguenti modifiche:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Ulteriori dettagli sulla personalizzazione del client Apollo sono disponibili in [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Per estendere il componente Navigazione con una voce Blog, aggiungi i seguenti adattamenti a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Ulteriori dettagli sulla personalizzazione del componente Navigazione sono disponibili in [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e nella documentazione del [Extensibility Framework](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) di PWA Studio.

1. Il client Apollo prevede l&#39;endpoint AEM GraphQL in `<https://pwa-studio/endpoint.js>`. Per mappare l’endpoint a questa posizione, personalizza la configurazione UPWARD dell’applicazione PWA Studio:
a. Aggiungi la variabile AEM_CFM_GRAPHQL a pwa-root/.env e adattala in modo che punti all’endpoint GraphQL AEM Content Fragments.

   Esempio: `AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

   b. Aggiungi un resolver proxy alla configurazione UPWARD. Un esempio di configurazione UPWARD potrebbe essere simile al seguente:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## Configurare AEM {#setup-aem}

Segui la documentazione sui Frammenti di contenuto di AEM per impostare un endpoint GraphQL per il progetto AEM. Inoltre, nel tuo progetto AEM, aggiungi le seguenti configurazioni per consentire all’applicazione PWA Studio di accedere all’endpoint GraphQL:

* Criteri di condivisione risorse multiorigine di Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

  Imposta la proprietà allowedorigin sul nome host completo dell’applicazione PWA.

  Esempio: `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Filtro referrer Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  Imposta la proprietà allow.hosts sul nome host dell&#39;applicazione PWA.

  Esempio: `pwa-studio-test-vflyn.local.pwadev`

Di seguito sono riportati alcuni esempi completi di entrambe le configurazioni: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Per mostrare l’endpoint GraphQL, sono disponibili alcuni esempi preparati di modelli e dati per frammenti di contenuto tramite un pacchetto di contenuti. Questi funzionano bene insieme ai componenti React forniti con l’estensione PWA Studio.

## Guida all’uso {#how-to-use}

Questa estensione è considerata un’implementazione di esempio di come collegare un’applicazione PWA Studio ad AEM per recuperare ed eseguire il rendering del contenuto tramite GraphQL.

A seconda del caso d’uso, desideri creare modelli di Frammento di contenuto personalizzati, che si traducono in uno schema GraphQL personalizzato utilizzabile dai tuoi componenti React.

Le impostazioni di produzione possono variare in diversi aspetti.

* Puoi avere un singolo endpoint GraphQL federato che combina i dati di AEM e Adobe Commerce GraphQL invece di personalizzare il client Apollo.
* L’applicazione PWA Studio può utilizzare direttamente l’URL dell’endpoint AEM GraphQL, senza un proxy con UPWARD. Il proxy può anche essere spostato in un livello diverso (ad esempio, CDN).
* L’approccio più adatto alle tue esigenze dipende inoltre in larga misura da come distribuisci l’applicazione PWA Studio all’utente.

Questa estensione viene fornita con due esempi.

### Blog {#blog}

Visualizza i post di blog in base ad alcuni modelli di frammenti di contenuto. Contiene inoltre esempi di come configurare il client Apollo per l’utilizzo con l’endpoint AEM GraphQL e di come estendere il componente Navigazione in PWA Studio. Per ulteriori dettagli, vedi [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension).

### Arricchimento PDP {#pdp-enrichment}

Consente agli addetti al marketing di arricchire facilmente i PDP con contenuto aggiuntivo gestito come Frammenti di contenuto.  Per ulteriori dettagli, vedi [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension).
