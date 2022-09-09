---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica del SPA React remoto in AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: eaa59b6ecfa50c4a6b4e316e5e305e48cb3d5676
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# Componente RemotePage {#remote-page-component}

Quando si decide [quale livello di integrazione](/help/implementing/developing/headful-headless.md) desideri avere tra il tuo SPA esterno e il AEM, spesso è chiaro che devi essere in grado di visualizzare e modificare il SPA in AEM. Il componente RemotePage è un componente pagina personalizzato solo a questo scopo.

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie dall&#39;applicazione generata `asset-manifest.json` e lo utilizza per il rendering del SPA all&#39;interno di AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un SPA nel corpo di un componente Pagina AEM.
* I componenti Frontend virtuali consentono di contrassegnare le sezioni come modificabili in AEM editor di SPA.
* Insieme, un SPA ospitato su un dominio diverso può essere reso modificabile in AEM.

Vedi l&#39;articolo [Modifica di un SPA esterno in AEM](editing-external-spa.md) per ulteriori dettagli sulle SPA modificabili esterne in AEM.

## Requisiti  {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Esegui il rendering del SPA in AEM
* L&#39;applicazione web deve utilizzare un manifesto di risorse del bundler come uno dei seguenti ed esporre un `asset-manifest.json` file nella directory principale del dominio in cui è presente l&#39;elenco in un `entrypoints property` tutti i file CSS e JS da caricare:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![esempio di proprietà entrypoints](assets/asset-manifest-entrypoints.png)
* L&#39;applicazione deve essere in grado di inizializzare in un `<div id="root"></div>` sotto il `body` elemento. Se è previsto un markup diverso per l’istanza dell’app, questo deve essere regolato di conseguenza negli script HTL del componente proxy che ha un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitazioni  {#limitations}

* L&#39;implementazione corrente del componente RemotePage supporta solo le applicazioni React remote.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili quando si esegue il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA AEM, il componente RemotePage è open source. Per tutti i dettagli tecnici del componente RemotePage, [consulta l’archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
