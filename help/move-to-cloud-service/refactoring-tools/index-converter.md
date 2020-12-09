---
title: Convertitore indice
description: Convertitore indice
translation-type: tm+mt
source-git-commit: 1117f03b2eff37f8b25726c3dc60d5a3fe98a5d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Convertitore indice {#index-converter}

Index Converter è un&#39;utilità sviluppata per migrare le definizioni indice di un cliente in preparazione del passaggio a AEM come Cloud Service.

## Introduzione {#introduction}

Il Convertitore indice consente AEM sviluppatori di migrare le definizioni dell&#39;indice Oak personalizzato esistenti da AEM come definizione dell&#39;indice Oak personalizzato compatibile con Cloud Service.

>[!NOTE]
>Il Convertitore indice trasforma solo le definizioni dell&#39;indice Oak personalizzato *lucene* presenti in `/apps` o `/oak:index`. Non trasforma gli indici di tipo *lucene* creati per `nt:base`.

Esistono due modi per creare definizioni personalizzate di indice Oak:

* `under /apps` (tramite qualsiasi pacchetto di contenuto personalizzato)
* direttamente sotto il percorso `/oak:index`

Se è stato utilizzato [Assicurarsi che l&#39;indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) non sia supportato in AEM come Cloud Service, e quindi devono essere convertiti in definizioni dell&#39;indice Oak e quindi devono essere migrati in definizioni dell&#39;indice Oak personalizzate compatibili con AEM come Cloud Service come indicato di seguito:

* Se la proprietà ignore è impostata su `true`, ignora o salta la definizione di verifica
* Aggiorna `jcr:primaryType` in `oak:QueryIndexDefinition`
* Rimuovere tutte le proprietà da ignorare come indicato nelle configurazioni OSGi
* Rimuovi sottostruttura `/facets/jcr:content` dalla definizione di verifica

## Utilizzo di Index Converter {#using-index-converter}

* Tramite  Adobe I/O CLI: Si consiglia di utilizzare Index Converter tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM come plug-in di refactoring del codice di Cloud Service per la  CLI di Adobe I/O).

Fare riferimento a **[Risorse Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e usare il plug-in.

* Come utilità indipendente : Index Converter può essere eseguito anche come utilità standalone.

Fare riferimento a **[Risorse Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** per scoprire come utilizzare questo strumento.



