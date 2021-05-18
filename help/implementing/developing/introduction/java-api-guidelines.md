---
title: Linee guida per le API Java
description: AEM è basato su uno stack software open-source ricco che espone molte API Java per l’uso.
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: cbcc20e75e4a0cb6d0e060039f4945ff4a85ff5c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Linee guida per le API Java {#java-api-guidelines}

Adobe Experience Manager (AEM) è basato su uno stack software open-source ricco che espone molte API Java da utilizzare durante lo sviluppo.

AEM è basato sui seguenti quattro set principali di API Java in ordine decrescente di preferenza.

1. **[Adobe Experience Manager (AEM)](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html)** : astrazioni di prodotto come pagine, risorse, flussi di lavoro, ecc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)** : astrazioni REST e basate su risorse come risorse, mappe dei valori e richieste HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  - Estrazioni di dati e contenuti come nodo, proprietà e sessioni.
1. **[OSGi (Apache Felix)](https://felix.apache.org)**  - astrazioni dei contenitori di applicazioni OSGi come servizi e componenti (OSGi).

Se un’API è fornita da AEM, preferiscila rispetto a Sling, JCR e OSGi. Se AEM non fornisce un’API, preferisci Sling rispetto a JCR e OSGi.

Per informazioni dettagliate su queste linee guida, consulta il documento [Comprendere le best practice per le API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
