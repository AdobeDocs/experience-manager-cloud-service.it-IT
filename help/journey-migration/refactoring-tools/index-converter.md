---
title: Convertitore indice
description: Convertitore indice
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# Convertitore indice {#index-converter}

Index Converter è un&#39;utility sviluppata per migrare le definizioni degli indici di un cliente in preparazione al passaggio a AEM as a Cloud Service.

## Introduzione {#introduction}

Il Convertitore indice consente agli sviluppatori AEM di migrare le definizioni degli indici Oak personalizzati esistenti in definizioni degli indici Oak personalizzati compatibili con AEM as a Cloud Service.

>[!NOTE]
>Convertitore indice trasforma solo *lucene* Tipo Definizioni dell’indice Oak personalizzate presenti in `/apps` o `/oak:index`. Non trasforma *lucene* digita gli indici creati per `nt:base`.

Esistono due modi per creare definizioni di indici Oak personalizzati:

* `under /apps` (tramite qualsiasi pacchetto di contenuti personalizzato)
* direttamente sotto `/oak:index` percorso

Se [Assicurati indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) è stato utilizzato, Assicurarsi che le definizioni non siano supportate in AEM as a Cloud Service. Di conseguenza, prima devono essere convertite nelle definizioni dell’indice Oak e quindi migrate alle definizioni dell’indice Oak personalizzate compatibili con AEM as a Cloud Service, come indicato dalle linee guida seguenti:

* Se la proprietà ignore è impostata su `true`, ignora o ignora la definizione di assicurazione
* Aggiornare il `jcr:primaryType` a `oak:QueryIndexDefinition`
* Rimuovi le proprietà da ignorare come indicato nelle configurazioni OSGi
* Rimuovi sottoalbero `/facets/jcr:content` da Assicurare definizione

## Utilizzo del Convertitore indice {#using-index-converter}

* Ad Adobe I/O, CLI : si consiglia di utilizzare il Convertitore indice tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in per il refactoring del codice as a Cloud Service AEM per Adobe I/O CLI).

  Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utilità autonoma: il Convertitore indice può anche essere eseguito come utilità autonoma.

  Fai riferimento a **[Risorsa Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** per scoprire come utilizzare questo strumento.
