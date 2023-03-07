---
title: Note sulla versione 2023.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2022.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---

# Note sulla versione 2023.03.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.03.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.40 è il 03 marzo 2023.

### Novità {#what-is-new-bpa}

* BPA è ora in grado di rilevare e segnalare i nodi in conflitto, ovvero i nodi con lo stesso `jcr:uuid`. Tali risultati sono contrassegnati come critici in quanto possono causare errori di acquisizione dei contenuti durante lo spostamento dei contenuti a AEM as a Cloud Service.
* BPA è ora in grado di rilevare e creare rapporti sull’utilizzo dei listener di eventi. Si consiglia di rieseguire il factoring di questo tipo di meccanismo di gestione degli eventi sui processi sling durante il passaggio a AEM as a Cloud Service.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava falsi positivi per `grouprendercondition`. Questo problema è stato risolto.