---
title: Convertitore indice
description: Convertitore indice
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Convertitore indice {#index-converter}

Index Converter è un&#39;utilità sviluppata per migrare le definizioni indice di un cliente in preparazione del passaggio a AEM as a Cloud Service.

## Introduzione {#introduction}

Il convertitore indice consente AEM sviluppatori di migrare le definizioni di indice Oak personalizzato esistenti per AEM definizioni di indice Oak personalizzato compatibile as a Cloud Service.

>[!NOTE]
>Trasformazioni solo di Index Converter *lucene* digitare Definizioni dell&#39;indice Oak personalizzato presenti in `/apps` o `/oak:index`. Non si trasforma *lucene* indici di tipo creati per `nt:base`.

Esistono due modi per creare definizioni di indice Oak personalizzato:

* `under /apps` (tramite qualsiasi pacchetto di contenuti personalizzato)
* direttamente `/oak:index` path

Se [Assicurati l&#39;indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) è stato utilizzato. Si prega di notare che le definizioni di Assicurazione non sono supportate su AEM as a Cloud Service, quindi devono prima essere convertite in definizioni di indice Oak e poi devono essere migrate in Definizioni di indice Oak personalizzato compatibili con AEM as a Cloud Service come indicato di seguito:

* Se la proprietà ignora è impostata su `true`, ignora o salta la definizione di garanzia
* Aggiorna `jcr:primaryType` a `oak:QueryIndexDefinition`
* Rimuovi le proprietà da ignorare come indicato nelle configurazioni OSGi
* Rimuovi sottostruttura `/facets/jcr:content` da Definizione sicura

## Utilizzo di Index Converter {#using-index-converter}

* Tramite Adobe I/O CLI : Si consiglia di utilizzare il convertitore di indice tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM plug-in di refactoring del codice as a Cloud Service per l’interfaccia CLI di Adobe I/O).

   Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utility indipendente : Il Convertitore indice può anche essere eseguito come un&#39;utilità autonoma.

   Fai riferimento a **[Risorsa Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** per scoprire come utilizzare questo strumento.
