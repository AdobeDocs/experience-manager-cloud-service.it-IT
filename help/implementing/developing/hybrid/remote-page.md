---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica di React SPA in AEM.
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Componente RemotePage {#remote-page-component}

Quando si decide [quale livello di integrazione](/help/implementing/developing/headful-headless.md) si desidera avere tra l’applicazione a pagina singola esterna e AEM, spesso è chiaro che è necessario essere in grado di visualizzare e modificare l’applicazione a pagina singola in AEM. Il componente RemotePage è un componente pagina personalizzato solo a questo scopo.

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie dall’ `asset-manifest.json` generato dall’applicazione e lo utilizza per il rendering dell’applicazione a pagina singola in AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un’applicazione a pagina singola nel corpo di un componente Pagina AEM.
* I componenti Frontend virtuali consentono di contrassegnare le sezioni come modificabili in AEM SPA Editor.
* Insieme, un’applicazione a pagina singola ospitata su un dominio diverso può essere resa modificabile in AEM.

Per ulteriori informazioni sulle applicazioni a pagina singola modificabili esterne in AEM, consulta l’ articolo [Modifica di un’applicazione a pagina singola esterna in AEM](editing-external-spa.md) .

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Eseguire il rendering dell’applicazione a pagina singola in AEM

## Limitazioni  {#limitations}

* L&#39;implementazione corrente del componente RemotePage supporta solo le applicazioni React remote.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili quando si esegue il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto AEM SPA, il componente RemotePage è open source. Per informazioni tecniche complete sul componente RemotePage, [vedere l&#39;archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
