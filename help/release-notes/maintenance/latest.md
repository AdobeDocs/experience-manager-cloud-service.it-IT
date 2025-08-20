---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 90e92cfb15a6dfe5a8a474996f52c8a0c689f5e6
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 38%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21994 {#21994}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21994, rilasciata al pubblico il mercoledì 19 agosto 2025. La versione di manutenzione precedente era la 21772.

Con la versione di attivazione funzioni 2025.8.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Nuove funzioni  {#new-features-21994}

Nessuna.

### Miglioramenti {#enhancements-21994}

* GRANITE-53488: migliorare la gestione degli errori dell’endpoint deleteconf.json.
* GRANITE-59968: consente di configurare REPLICATION_FORCE_READY_MILLIES.
* GRANITE-60183: Apache commons-fileupload 1.6.0.
* GRANITE-60306: Apache commons-lang 3.18.0.
* GRANITE-60637: Apache commons-codec su 1.19.0.
* GRANITE-60645: Apache commons-ui 2.20.0.
* GRANITE-60663: Apache commons-text 1.14.0.
* GRANITE-60714: Driver Java Mongo 5.2.
* GRANITE-60778: Filevault 4.0.0.
* GRANITE-60823: Jackrabbit 2.22.2.
* GRANITE-60967: crea metriche per il tracciamento del tempo di compilazione clientlib.
* SKYOPS-105469: aggiunta del supporto per acsredirectMgr nell’api di correzione automatica.
* SKYOPS-113929: aggiungi metriche per il controllo della disponibilità per la replica.
* SKYOPS-84821: motore Sling 2.16.6.
* SKYOPS-114322: aumentare il linguaggio del compilatore di chiusura nel livello a `ECMASCRIPT_2018`.

### Problemi risolti {#fixed-issues-21994}

* GRANITE-60167: l’aggiornamento dell’indice asincrono in Skyline non supporta i dati CSV.
* GRANITE-60532: la modifica degli interruttori di valore non viene selezionata.
* SITES-34277: è stato corretto un errore di blocco nei flussi di lavoro di traduzione per le pagine.
* SKYOPS-105471: supporta la correzione dambaseredirect per l’autocorrezione aso.
* SKYOPS-109532: attivazione/disattivazione del collegamento per la rimozione della funzione.

#### Guide AEM {#guides-21994}

* GUIDES-26688: i file di layout CSS e Pagina nei modelli PDF nativi presentano un comportamento di blocco dei file incoerente, che consente di apportare modifiche anche quando i file sono bloccati.
* GUIDES-30900: la copia di una cartella con un numero elevato di risorse dall’interfaccia utente di Assets causa un timeout dell’API. L’operazione continua a essere eseguita nel backend e viene completata dopo un certo periodo di tempo, ma nell’interfaccia utente non viene visualizzato alcun messaggio di esito positivo o negativo o di notifica.
* GUIDES-29090: nell’output PDF nativo, l’elenco degli indici (LOI) viene visualizzato in ordine non alfabetico e i termini degli indici nidificati non vengono raggruppati correttamente, rendendo difficile la navigazione nell’indice.
* GUIDES-11227: Copiando una mappa DITA dall&#39;interfaccia utente di Assets, anche la Baseline associata viene copiata nella nuova mappa.
* GUIDE-31506: la home page rimane vuota quando uno dei file elencati nel widget File recenti è basato su un modello il cui modello di origine non include una miniatura.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-21994}

* Apache HTTPD versione 2.4.65 introduce modifiche che possono interessare determinate configurazioni a causa di nuove restrizioni implementate come parte di correzioni di sicurezza. Queste correzioni risolvono alcune vulnerabilità garantendo che le direttive come `RequestHeader set`, `edit` e `edit_r` utilizzate per modificare l&#39;intestazione Content-Type siano ora limitate correttamente alle intestazioni di richiesta. Questa modifica impedisce modifiche non desiderate alle intestazioni di risposta, in particolare per il contenuto statico.

### Funzioni e API obsolete {#deprecated-21994}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21994}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 2 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-21994}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,84,0 | [API Oak API 1.84.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
