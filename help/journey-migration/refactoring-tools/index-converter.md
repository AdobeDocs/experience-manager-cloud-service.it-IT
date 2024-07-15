---
title: Convertitore indice
description: Scopri come migrare le definizioni degli indici in preparazione al passaggio ad AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Convertitore indice {#index-converter}

Index Converter è un’utility sviluppata per migrare le definizioni degli indici di un cliente in preparazione al passaggio ad AEM as a Cloud Service.

## Introduzione {#introduction}

Il Convertitore indice consente agli sviluppatori AEM di migrare le definizioni degli indici Oak personalizzati esistenti in definizioni degli indici Oak personalizzati compatibili con AEM as a Cloud Service.

>[!NOTE]
>Il convertitore indice trasforma solo le definizioni di indice Oak personalizzate di tipo *lucene* presenti in `/apps` o `/oak:index`. Non trasforma gli indici di tipo *lucene* creati per `nt:base`.

Esistono due modi per creare definizioni di indici Oak personalizzate:

* `under /apps` (tramite qualsiasi pacchetto di contenuti personalizzato)
* direttamente nel percorso `/oak:index`

Se [Assicurati che sia stato utilizzato l&#39;indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html), assicurati che le definizioni non siano supportate in AEM as a Cloud Service. Di conseguenza, prima devono essere convertite in Definizioni dell’indice Oak, quindi devono essere migrate in Definizioni dell’indice Oak personalizzate compatibili con AEM as a Cloud Service, come indicato dalle linee guida seguenti:

* Se la proprietà ignore è impostata su `true`, ignorare o ignorare la definizione di assicurazione
* Aggiorna `jcr:primaryType` in `oak:QueryIndexDefinition`
* Rimuovi le proprietà da ignorare come indicato nelle configurazioni OSGi
* Rimuovi sottoalbero `/facets/jcr:content` dalla definizione di garanzia

## Utilizzo del Convertitore indice {#using-index-converter}

* Adobe I/O CLI: Adobe consiglia di utilizzare Index Converter tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in di refactoring del codice AEM as a Cloud Service per Adobe I/O CLI).

  Per informazioni su come installare e utilizzare il plug-in, consulta **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**.

* Come utilità autonoma: il Convertitore indice può anche essere eseguito come utilità autonoma.

  Per informazioni sull&#39;utilizzo di questo strumento, consulta **[Risorsa Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**.
