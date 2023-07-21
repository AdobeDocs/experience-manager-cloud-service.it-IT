---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 39b2afda66e3bcb7db8ae63a2d0dcd27014ce377
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 66%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 12790 {#release-12790}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 12790, rilasciata pubblicamente il 21 luglio 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12697.

2023.7.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-12790}

Nessuno.

### Problemi risolti {#fixed-issues-112790}

- SLING-11974 - È stata corretta la regressione in SlingHttpServletRequest#getUserPrincipal per le richieste non autenticate. La correzione assicura che venga restituita un’entità principale anche per le richieste non autenticate.

### Problemi noti {#known-issues-12790}

Nessuno.

### Tecnologie incorporate {#embedded-tech-12790}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
