---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e1fa4b3bcb04ab3e834b34f507f1350fb536b513
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 51%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21005 {#21005}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21005, rilasciata pubblicamente il mercoledì 27 maggio 2025. La versione di manutenzione precedente era la 20626.

Con la versione di attivazione funzioni 2025.5.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21005}

* GRANITE-58927: Miglioramenti dell’attivazione/disattivazione della ricerca semantica.
* GRANITE-58800: Aggiornamento delle raccolte di Apache Commons alla versione 4.5.0.
* GRANITE-58866: aggiornamento di Oak alla versione 1.80.0.
* SKYOPS-106509: compatibilità GSON migliorata tramite l’accesso riflessivo in Java 21.
* SKYOPS-107761: Aggiornamento di Sling Models Jackson Exporter alla versione 1.1.6.
* SKYOPS-107813: aggiornamento a Sling ResourceResolver 1.12.8.

### Problemi risolti {#fixed-issues-21005}

* CNTBF-443: proprietà SearchSlingJob `EVENT_JOB_TOPIC` corretta.
* GRANITE-57853: sono stati risolti dei problemi di allineamento a discesa nell’interfaccia utente di.
* GRANITE-58107: sono stati corretti gli errori 404 in Pubblicazione disabilitando l’affinità del pod basata sull’utente nel gestore OAuth.
* GRANITE-58276, SLING-12755: sono stati corretti alcuni cicli di dipendenza OSGi che potevano impedire il corretto avvio della factory del motore di script HTL, causando errori di rendering lato server intermittenti.
* SKYOPS-105151: è stato corretto l’errore NPE durante l’accesso all’elenco dei bundle.
* SKYOPS-83910, SKYOPS-82371 - Sono stati risolti i problemi di concorrenza relativi alla compilazione JSP.

#### Guide AEM {#guides}

* GUIDES-26919 : Quando si apre una mappa DITA con la shell unificata abilitata, l&#39;editor viene aggiornato in modo intermittente.
* GUIDES-26282: se non si chiudono le connessioni della sessione JCR durante l’aggiornamento o la creazione di argomenti, si verificano perdite di memoria e tempi di inattività del servizio.
* GUIDES-26434: la pubblicazione nativa di PDF continua a tempo indeterminato se il contenuto DITA ha un collegamento a web senza ambito come `external`.
* GUIDES-26516: la pubblicazione di PDF nativi e di siti AEM si blocca e viene messa in coda, quando si verificano errori nel contenuto.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-21005}

Nessuna.

### Funzioni e API obsolete {#deprecated-21005}

* GRANITE-54164: rimosso `org.apache.jackrabbit.oak.plugins.blob` dall&#39;API pubblica.
* GRANITE-54280: rimosso `org.apache.jackrabbit.oak.cache` dall&#39;API pubblica.
* GRANITE-58332: `org.apache.jackrabbit.oak.plugins.memory` è obsoleto nell&#39;API pubblica.
* La funzionalità [Experience Cloud Setup Automation](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) è stata dichiarata obsoleta.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21005}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 5 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Notifica di modifica {#change-notice-21005}

* Questa versione contiene le seguenti nuove versioni dell’indice del prodotto:
   * **damAssetLucene-12**

Eventuali versioni personalizzate delle precedenti versioni dell’indice verranno unite automaticamente alla nuova versione dell’indice del prodotto. Dovrai applicare ulteriori aggiornamenti personalizzati alla versione unita.

#### Aggiornare aem-cloud-testing-client {#update-aem-cloud-testing-clients-21005}

Le prossime modifiche richiederanno l&#39;aggiornamento della libreria [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) utilizzata nei test funzionali personalizzati almeno alla versione **1.2.1** (consigliato: ultima versione 1.2.9)

Assicurati che la dipendenza in `it.tests/pom.xml` sia stata aggiornata.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

Questa modifica deve essere eseguita prima del 15 giugno 2025.
Se non si aggiorna la libreria di dipendenze, si verificheranno errori di pipeline nel passaggio &quot;Test funzionale personalizzato&quot;.

### Tecnologie incorporate {#embedded-tech-21005}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,80,0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
