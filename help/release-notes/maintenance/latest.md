---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e771913562b3770e5a504432d40c770804aadc4b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 34%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13804 {#release-13804}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13804, rilasciata pubblicamente il 10 ottobre 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 13665.

L’attivazione delle funzioni 2023.10.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-13804}

* GRANITE-47238: Manutenzione del registro di controllo: elimina i processi client per utilizzare la configurazione del cliente.
* GRANITE-47123: Publish (Sling) - Migliora il tempo di avvio inizializzando la cache dei percorsi personalizzati in modo asincrono per impostazione predefinita.
* GRANITE-46618: Pubblicazione (replica) - Migliora la velocità di avvio della pubblicazione tramite la gestione in batch dei messaggi di stato della replica.
* GRANITE-47136: indicizzazione (download) - Migliora la velocità di download del nuovo download dell’indice parallelo (disabilitando la convalida del checksum).
* GRANITE-47211: pubblicazione (Infra): migliora la separazione delle distribuzioni a livello di pubblicazione (memorizzando e recuperando il nome della revisione dell’archivio segmenti).
* GRANITE-47267: Aggiornamento ad Apache Felix Http Jetty 4.2.18 (include la correzione di bug per la gestione dei parametri delle richieste ([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625)) con miglioramenti delle prestazioni per gli sviluppi locali e RDE).
* GRANITE-47247: aggiornamento a Sling Servlets Resolver 2.9.14 con miglioramenti delle prestazioni nella risoluzione dei servlet.

### Problemi risolti {#fixed-issues-13804}

* GRANITE-47376: Author (Infra) - Correzione di errori DiscoveryTopologyUndefined dopo il riavvio continuo.
* CQ-4353436: la console web AEM (Sling) - Configurazioni vuote in ServiceUserMapperImpl Validators (Principal/User) interrompe l’istanza AEM ([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912)).
* SKYOPS-63925: processo di trasformazione - Evitare errori TransformJob con JDK 11 - ZipException: errori di intestazione CEN non validi (con flag JVM disableZip64ExtraFieldValidation).
* SKYOPS-63361: processo di trasformazione (registrazione) Registrazione migliorata con processi di trasformazione (sottoparagrafo CUSTOMER_EXTRACT).
* SKYOPS-64103: Strumento FACT (Registrazione) - Riduce o tronca i messaggi di errore e di avviso relativi alla compilazione Clientlib.
* SKYOPS-65109: strumento FACT (Gestione errori) - I pacchetti di contenuti con dipendenze non risolte generano un errore segnalato correttamente.
* SKYOPS-65368: strumento FACT (Gestione errori): lo strumento viene eseguito in un ciclo di inclusione senza fine e alla fine si interrompe per l’incorporamento circolare di Clientlibs.
* SKYOPS-64031: RDE - ComponentCacheImpl può entrare in uno stato incoerente a causa di una registrazione ResourceResolverFactory duplicata ([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019)).
* ASSETS-29105: RDE - Provider di restrizioni mancante da SecurityProviderRegistration requiredServicePids nel modello di funzionalità RDE.
* GRANITE-44674: CoralUI - La funzionalità del campo obbligatorio Datepicker non è corretta.

### Problemi noti {#known-issues-13804}

* CQ-4354836: impossibile avviare il flusso di lavoro o creare l’attività dalla console Progetti.
* CQ-4354834 : Gli utenti non possono aggiungere commenti in un’attività casella in entrata.

### Tecnologie incorporate {#embedded-tech-13804}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,56-T20230927085643-189caed | [API Oak API 1.56.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
