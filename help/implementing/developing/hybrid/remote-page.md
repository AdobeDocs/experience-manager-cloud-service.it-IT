---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica del SPA React remoto in AEM.
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# Componente RemotePage {#remote-page-component}

Quando si decide [quale livello di integrazione ](/help/implementing/developing/headful-headless.md) si desidera avere tra la SPA esterna e il AEM, spesso è chiaro che è necessario essere in grado di visualizzare e modificare il SPA all&#39;interno AEM. Il componente RemotePage è un componente pagina personalizzato solo a questo scopo.

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie dall&#39;elemento `asset-manifest.json` generato dall&#39;applicazione e lo utilizza per eseguire il rendering dell&#39;SPA all&#39;interno di AEM.

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto in Proprietà pagina
* Eseguire il rendering del SPA in AEM

## Limitazioni  {#limitations}

* L’implementazione corrente del componente RemotePage supporta solo le applicazioni React remote.
* I CSS interni definiti nel file HTML principale dell&#39;applicazione e i CSS in linea nel nodo DOM principale non saranno disponibili quando si esegue il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA AEM, il componente RemotePage è open source. Per informazioni tecniche complete sul componente RemotePage, vedere l&#39;archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
