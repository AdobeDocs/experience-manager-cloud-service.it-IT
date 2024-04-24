---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f15b42e4012385c461b5440b92f53c4e58fb8ac2
workflow-type: ht
source-wordcount: '213'
ht-degree: 100%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15977 {#release-15977}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15977, rilasciata al pubblico il 19 aprile 2024. La versione di manutenzione precedente era 15939.

Con l’attivazione delle funzioni 2024.4.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15977}

* GRANITE-51335: ottimizza il controllo dello stato di AEM per aumentare la stabilità dell’istanza.

### Problemi risolti {#fixed-issues-15977}

* CQ-4357226: correggi la regressione nel supporto delle configurazioni IMS per le credenziali OAuth.
* GRANITE-51335: aggiornamento di rateLimit alla versione 5.0.4. Risolti i problemi delle registrazioni di Felix Health Check.

### Problemi noti {#known-issues-15977}

Nessuno.

### Funzioni e API obsolete {#deprecated-15977}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Dai un&#39;occhiata a [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato dichiarato obsoleto o rimosso in AEM as a Cloud Service.

### Tecnologie incorporate {#embedded-tech-15977}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.24.6 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
