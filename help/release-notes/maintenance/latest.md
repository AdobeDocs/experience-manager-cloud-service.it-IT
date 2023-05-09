---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 47%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note tecniche sulla versione per la versione di manutenzione corrente dell’Experience Manager as a Cloud Service.

## Versione 11873 {#release-11873}

Di seguito sono riepilogati i continui miglioramenti della versione di manutenzione 11873, rilasciata pubblicamente il 3 maggio 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 11835.

L’abilitazione delle funzioni per questa versione di manutenzione ti darà accesso al set di funzioni completo. Consulta le [note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md) per ottenere informazioni dettagliate.

### Miglioramenti {#enhancements}

- SITES-1200 - Miglioramenti all&#39;API di ricerca con filtro basato sui tag
- GRANITE-42939 - Aggiungi annotazioni e avvisi obsoleti al codice oauth-server

### Problemi noti {#known-issues-11873}

Nessuno.

### Problemi risolti {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - È stato risolto un problema con PublishPageRenderingErrorsHigh
- GRANITE-4388 - È stato corretto il deterioramento del throughput dopo un numero elevato di scritture di risorse DAM su Mongo
- SITES-11922 - È stato risolto un problema di annullamento della pubblicazione dall&#39;anteprima che non rimuoveva lo stato di sincronizzazione
- ASSETS-21648 - È stato risolto un problema di autorizzazione relativo alla funzionalità Asset Relate

### Tecnologie incorporate {#embedded-tech-11873}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak API 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.21.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
