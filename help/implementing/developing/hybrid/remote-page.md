---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica dell’SPA di React remoto all’interno dell’AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# Componente RemotePage {#remote-page-component}

Quando si decide [quale livello di integrazione](/help/implementing/developing/headful-headless.md) si desidera avere tra l&#39;SPA esterno e l&#39;AEM, spesso è chiaro che è necessario essere in grado di visualizzare e modificare l&#39;SPA all&#39;interno dell&#39;AEM. Il componente RemotePage è un componente pagina personalizzato appositamente per questo scopo.

{{ue-over-spa}}

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie da `asset-manifest.json` generato dall&#39;applicazione e le utilizza per il rendering dell&#39;SPA in AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un SPA nel corpo di un componente Pagina AEM.
* I componenti front-end virtuali consentono di contrassegnare le sezioni come modificabili nell’editor SPA dell’AEM.
* Insieme, un SPA ospitato su un dominio diverso può essere reso modificabile in AEM.

Per ulteriori dettagli sull&#39;SPA esterno modificabile nell&#39;AEM, vedere l&#39;articolo [Modifica di un SPA esterno nell&#39;AEM](editing-external-spa.md).

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Rendere l’SPA nell’AEM
* L&#39;applicazione Web deve utilizzare un manifesto della risorsa del bundler come uno dei seguenti ed esporre un file `asset-manifest.json` nella directory principale del dominio che elenca in un `entrypoints property` tutti i file CSS e JS da caricare:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![esempio di proprietà entrypoints](assets/asset-manifest-entrypoints.png)
* L&#39;applicazione deve essere in grado di inizializzare in un `<div id="root"></div>` sotto l&#39;elemento `body`. Se è previsto un markup diverso per la creazione dell&#39;istanza dell&#39;app, è necessario regolarlo di conseguenza negli script HTL del componente proxy con `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitazioni {#limitations}

* Il componente RemotePage prevede che l&#39;implementazione fornisca un manifesto delle risorse come quello [ trovato qui.](https://github.com/shellscape/webpack-manifest-plugin) Il componente RemotePage, tuttavia, è stato testato per funzionare solo con il framework React (e Next.js tramite il componente remote-page-next) e pertanto non supporta il caricamento remoto di applicazioni da altri framework, ad esempio Angular.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili durante il rendering remoto nell’AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA dell’AEM, il componente RemotePage è open source. Per informazioni tecniche complete sul componente RemotePage, [consulta l&#39;archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
