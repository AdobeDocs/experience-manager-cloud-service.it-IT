---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 63%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21570 {#21570}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21570, rilasciata pubblicamente il mercoledì 15 luglio 2025. La versione di manutenzione precedente era la 21484.

>[!NOTE]
>
>[La versione 21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484) è stata resa privata e sostituita da 21570 sulla versione.

Con la versione di attivazione funzioni 2025.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21570}

* Migrazione ad Apache Httpd 2.4.63

### Problemi risolti {#fixed-issues-21570}

* SKYOPS-112722 - È stato risolto un problema che impediva la risoluzione degli URL personalizzati

### Problemi noti {#known-issues-21570}

* Il SDK di AEM correlato ha un diverso ID versione (21575) ed è disponibile tramite il portale di distribuzione software.
* Apache HTTP Server versione 2.4.63 ha introdotto una modifica fondamentale nella gestione dei punti interrogativi (`mod_rewrite`) negli URL da parte di `?`. Questa modifica è stata implementata per impedire l&#39;utilizzo del flag `UnsafeAllow3F`, che è stato considerato un rischio per la sicurezza. Ciò influisce su tutte le direttive `RewriteRule` che si basano sul rilevamento del punto interrogativo nei modelli URL.

### Funzioni e API obsolete {#deprecated-21570}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21570}

Nessuna

### Tecnologie incorporate {#embedded-tech-21570}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Server HTTP Apache | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
