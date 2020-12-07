---
title: Linee guida API Java
description: AEM è basato su uno stack software open-source ricco che espone molte API Java per l'uso.
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Linee guida API Java {#java-api-guidelines}

Adobe Experience Manager (AEM) è basato su uno stack software open-source avanzato che espone molte API Java da utilizzare durante lo sviluppo.

AEM è basato sui seguenti quattro set di API Java principali in ordine decrescente di preferenza.

1. **Adobe Experience Manager (AEM)**  - astrazioni di prodotto come pagine, risorse, flussi di lavoro ecc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST e astrazioni basate su risorse come risorse, mappe dei valori e richieste HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  - Estrazioni di dati e contenuti quali nodi, proprietà e sessioni.
1. **[OSGi (Apache Felix)](https://felix.apache.org)** - OSGi astrazioni di contenitori di applicazioni quali servizi e componenti (OSGi).

Se un&#39;API è fornita da AEM, preferitela rispetto a Sling, JCR e OSGi. Se AEM non fornisce un’API, preferisci Sling su JCR e OSGi.

Per informazioni dettagliate su queste linee guida, consultate il documento [Comprendere le best practice per le API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
