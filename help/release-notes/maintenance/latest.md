---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 82%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15860 {#release-15860}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15860, rilasciata al pubblico il giovedì 10 aprile 2024. La versione di manutenzione precedente era 15787.

Con l’attivazione delle funzioni 2024.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15860}

Nessuno.

### Problemi risolti {#fixed-issues-15860}

* Corregge la regressione per la visualizzazione della console Lanci quando un lancio fa riferimento a una pagina eliminata o spostata.

### Problemi noti {#known-issues-15860}

Nessuno.

### Funzioni e API obsolete {#deprecated-15860}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Dai un&#39;occhiata a [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato dichiarato obsoleto o rimosso in AEM as a Cloud Service.

### Notifica di modifica {#change-notice-15860}

**Azioni richieste**

#### Impostare la versione Java CM su 11 {#set-java-version-11}

La nuova versione di aem-sdk-api contiene classi compilate con una destinazione Java 11, che non è compatibile con l’ambiente di build predefinito di Cloud Manager versione 1.8 di JDK. Questo aggiornamento richiede l’esecuzione di Maven con JDK 11.

Si consiglia di aggiungere un file `.cloudmanager/java-version` nella directory principale del relativo archivio Git con il contenuto: `11`. Consulta [Ambiente di build/Impostazione della versione JDK di Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologie incorporate {#embedded-tech-15860}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=it) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.24.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
