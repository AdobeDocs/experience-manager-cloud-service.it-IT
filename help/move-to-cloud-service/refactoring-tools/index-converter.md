---
title: Convertitore indice
description: Convertitore indice
translation-type: tm+mt
source-git-commit: adfc453729b88a9cc457783806eb7b4d69150b21
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Convertitore indice {#index-converter}

Index Converter è un&#39;utilità sviluppata per migrare la definizione di indice di un cliente in preparazione del passaggio a AEM come Cloud Service.

## Introduzione {#introduction}

Index Converter consente AEM sviluppatori di migrare le definizioni dell&#39;indice Oak personalizzato esistenti da AEM come definizione dell&#39;indice Oak personalizzato compatibile con Cloud Service.

>[!NOTE]
>Il Convertitore indice trasforma solo le definizioni dell&#39;indice Oak personalizzato *lucene* presenti in `/apps` o `/oak:index`. Non trasforma gli indici di tipo *lucene* creati per `nt:base`.

Esistono due modi per creare definizioni personalizzate di indice Oak:

* `under /apps` (tramite qualsiasi pacchetto di contenuto personalizzato)
* direttamente sotto il percorso `/oak:index`

>[!NOTE]
>Fare riferimento a [Assicurarsi che l&#39;indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) venga definito e creato

## Utilizzo di Index Converter {#using-index-converter}

>[!NOTE]
>Sebbene si consiglia di utilizzare lo strumento di conversione indice tramite il plug-in CLI [AIO per la migrazione dell&#39;origine](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration), può anche essere eseguito autonomamente.

Fare riferimento a **[Risorse Git: aem-cs-source-migration-index-converter](https://git.corp.adobe.com/vavarshn/aem-cloud-service-source-migration/blob/master/packages/index-converter/README.md)** per scoprire come installare e usare il plug-in.

