---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 65%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15575 {#release-15575}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15575, rilasciata al pubblico il mercoledì 19 marzo 2024. La versione di manutenzione precedente era 15262.

Con l’attivazione delle funzioni 2024.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15575}

Nessuno.

### Problemi risolti {#fixed-issues-15575}

* ASSETS-36358: non è possibile eseguire il rendering del rapporto di caricamento.
* GRANITE-50774: GraniteContent deve utilizzare l’ordine deterministico dei valori proprietà al momento dell’avvio.

### Problemi noti {#known-issues-15575}

Nessuno.

### Notifica di modifica {#change-notice-15575}

**Azioni richieste**

#### Imposta versione Java CM su 11 {#set-java-version-11}

La nuova versione di aem-sdk-api contiene classi compilate con una destinazione Java 11, che non è compatibile con l’ambiente di build predefinito di Cloud Manager versione 1.8 di JDK. Questo aggiornamento richiede che Maven venga eseguito utilizzando JDK 11.

Si consiglia ai clienti di aggiungere una `.cloudmanager/java-version` nella directory principale del relativo archivio Git con il contenuto: `11`. Consulta [Ambiente di build/Impostazione della versione JDK di Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### Aggiorna client-test-cloud-aem alla versione 1.2.1 {#update-aem-cloud-testing-clients}

Le prossime modifiche richiederanno la libreria [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) utilizzata nei test funzionali personalizzati per l’aggiornamento almeno alla versione **1.2.1**

Assicurati che la dipendenza in `it.tests/pom.xml` sia stata aggiornata.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Questa modifica deve essere eseguita prima del 6 aprile 2024.

Se non si aggiorna la libreria di dipendenze, si verificheranno errori di pipeline nel passaggio &quot;Test funzionale personalizzato&quot;.

### Tecnologie incorporate {#embedded-tech-15575}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak API 1.60.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=it) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
