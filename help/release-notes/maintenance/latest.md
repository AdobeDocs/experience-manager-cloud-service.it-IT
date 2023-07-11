---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e1183791f543d17f98cb6c9ca0c513c8936ef477
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 47%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 12585 {#release-12585}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 12585, rilasciata pubblicamente l’11 luglio 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12549.

2023.7.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-12585}

- Miglioramenti generali alla stabilità RDE (SKYOPS-61133, SKYOPS-55281, SKYOPS-61216 e SKYOPS-61401)
- DXML-12327: Guide AEM: supporto per le variabili di linguaggio nella pubblicazione nativa di PDF
- DXML-11518: guide AEM: supporto migliorato per i metadati nella pubblicazione nativa in PDF
- DXML-10093: guide AEM: supporto per la connessione a origini dati esterne e l&#39;inserimento di dati in argomenti dita
- DXML-10699: Guide AEM: supporto per il formato XLIFF nella traduzione
- DXML-10141: guide AEM: opzione per utilizzare la pubblicazione basata su microservizi per i tipi di predefiniti PDF (Native e DITA-OT), HTML e Custom

### Problemi risolti {#fixed-issues-12585}

- Guide AEM: vari miglioramenti e correzioni di stabilità per Native PDF
- SKYOPS-53130: migliorare il supporto dello strumento CA in RDE
- SKYOPS-57146: Correggere il deadlock di Sling all’avvio dell’AEM

### Problemi noti {#known-issues-12585}

Nessuno.

### Tecnologie incorporate {#embedded-tech-12585}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
