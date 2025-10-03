---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6cf380fd972888fa21f682b0e799cf5ab594e829
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 50%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 22758 {#22758}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 22758, rilasciata pubblicamente il giovedì 1 ottobre 2025. La versione di manutenzione precedente era la 22450.

Con la versione di attivazione funzioni 2025.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-22758}

* ASSETS-56227: rinomina il modificatore adobe-countdown-timer.
* CNTBF-493: salta la versione del bundle content-backflow al 2.0.28.
* CQ-4361110: Traduzioni in granito.
* CQ-4361112: Ultime traduzioni per AEM.
* GRANITE-56026: migliora le risposte del codice di stato API delle autorizzazioni.
* GRANITE-61015: aggiunto il pacchetto `org.apache.commons.io.channels` all&#39;elenco pubblico esportato.
* GRANITE-61167: Il registro Felix è stato aggiornato alle ultime specifiche OSGI.
* GRANITE-61167: aggiorna una serie di dipendenze Apache Felix.
* GRANITE-61169: migliorare il controllo delle stringhe protette.
* GRANITE-61622: aggiorna una serie di dipendenze Apache Sling.
* GRANITE-61663: aggiungi `com.adobe.granite.repository.indexdefs-1.0.2` a quickstart.
* GRANITE-61811: aggiungi `com.adobe.granite.repository-2.0.0` a quickstart.
* SITES-32014: ascolta eventi esterni per aggiornare le registrazioni del servizio.
* SITES-34277: corretto un errore di blocco nei flussi di lavoro di traduzione per le pagine.
* SKYOPS-108706: la versione aggiornata attiva il bundle all’ultima versione (memorizzazione in cache delle eTag).
* SKYOPS-114210: aggiornamento alla versione più recente del bundle aem.pss.service.
* SKYOPS-116171: aggiornamento a Sling ResourceResolver 1.12.12.
* SKYOPS-119811: versione rilasciata del dispatcher-pubblicazione 2.0.258.

### Problemi risolti {#fixed-issues-22758}

* GRANITE-61875: correggi i trigger per &quot;valutazione espressione non valida&quot; - Gli autori non possono salvare frammenti di contenuto e le risorse non possono essere scaricate.
* SITES-22059: Correggi l’errore JS nei componenti Visualizzatore PDF. Stringa non localizzata &quot;Anteprima file non disponibile&quot; nel sito dei componenti core > Visualizzatore PDF.
* GRANITE-59704: correggi htmllibmanager.debug causando un errore nella modalità di modifica.
* GRANITE-61042: integrazione di FELIX-6796 (correzione NPE ServiceTracker) nel bundle della console web Felix di AEM.
* GRANITE-61165: Workspace.copy() genera RepositoryException.
* GRANITE-61875: aggiorna ui.commons a 5.10.50.

### Problemi noti {#known-issues-22758}

Nessuna.

### Funzioni e API obsolete {#deprecated-22758}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-22758}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 13 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-22758}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,86,0 | [API Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.1 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
