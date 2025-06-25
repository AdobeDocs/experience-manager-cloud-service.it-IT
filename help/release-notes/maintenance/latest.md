---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: ht
source-wordcount: '380'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21193 {#21193}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21193, rilasciata pubblicamente il 10 giugno 2025. La versione di manutenzione precedente era la 21005.

Con la versione di attivazione funzioni 2025.6.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21193}

* ASSETS-51245: prestazioni migliorate per gli elenchi di cartelle di grandi dimensioni nell’interfaccia touch.
* ASSETS-51686: sono stati apportati miglioramenti al processo di operazioni in blocco, tra cui una più semplice cancellazione del processo, una registrazione avanzata e il download di audit per risultati di grandi dimensioni.
* CQ-4360131: è stata migliorata la risposta di errore per gli endpoint OpenAPI, consentendo ai client API di ricevere informazioni di errore strutturate correttamente.

### Problemi risolti {#fixed-issues-21193}

* ASSETS-41007: le risorse eliminate potrebbero rimanere visibili in Content Hub.
* ASSETS-50994: AemRequestEventFilter causa un’eccessiva contesa del thread Jetty.
* ASSETS-50155: attivati eventi di modifica dei metadati duplicati.
* ASSETS-50716: l’ordinamento per titolo nella vista a elenco delle risorse non funziona come previsto.
* ASSETS-50820: assicurati che le richieste non valide per l’API delle relazioni con le risorse vengano rifiutate correttamente con un errore 400.
* ASSETS-50562: l’API di caricamento risorse deve creare una versione in base al comportamento predefinito in caso di conflitto sul nome.
* ASSETS-50992: l’endpoint initiateUpload.json delle API di Assets dovrebbe restituire il tipo di contenuto “application/json”.
* ASSETS-51322: rimozione automatica e scadenza delle barricate asincrone che rimangono persistenti a tempo indefinito dopo un processo non riuscito.
* ASSETS-51809: l’editor CSV non mostrava le modifiche salvate di recente a causa della memorizzazione nella cache del browser.
* SITES-31678: i frammenti di esperienza (XF) con riferimenti in base al contesto non hanno risolto la directory principale della lingua corretta nell’API di pubblicazione XF.


### Problemi noti {#known-issues-21193}

Nessuna.

### Funzioni e API obsolete {#deprecated-21193}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21193}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 2 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-21193}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
