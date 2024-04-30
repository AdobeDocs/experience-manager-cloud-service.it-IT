---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 62%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15977 {#release-15977}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15977, rilasciata al pubblico il 19 aprile 2024. La versione di manutenzione precedente era 15939.

Con l’attivazione delle funzioni 2024.4.0 viene fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-15977}

* GRANITE-51335: ottimizza il controllo dello stato di AEM per aumentare la stabilità dell’istanza.

### Problemi risolti {#fixed-issues-15977}

* CQ-4357226: correggi la regressione nel supporto delle configurazioni IMS per le credenziali OAuth.
* GRANITE-51335: aggiornamento di rateLimit alla versione 5.0.4. Risolti i problemi delle registrazioni di Felix Health Check.

### Problemi noti {#known-issues-15977}

* **(Solo per AEM Forms)** Dopo aver installato le 15977 sulla versione di manutenzione di AEM Cloud Foundation, i campi del modulo adattivo vengono riprodotti in ordine errato durante la creazione dei moduli e per i moduli pubblicati. Se utilizzi AEM Forms, l’Adobe consiglia di non eseguire l’aggiornamento alla versione 15977 fino a quando il problema non viene risolto nella prossima versione di manutenzione. Così facendo si può evitare qualsiasi inconveniente.

### Funzioni e API obsolete {#deprecated-15977}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* A decorrere dal 1° maggio 2024, Adobe Dynamic Medie cesserà il supporto per i seguenti elementi:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * Le seguenti crittografie deboli in TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Per sapere cosa è obsoleto o rimosso in AEM as a Cloud Service, vedi [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-15977}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.24.6 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
