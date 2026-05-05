---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82b3b4bdcd09aa86974518f4f62e73c9f377c83f
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 30%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## 25821 sulla versione {#release-25821}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 25821, rilasciata pubblicamente il 5 maggio 2026. La versione di manutenzione precedente era 25520.

L’attivazione della funzione 2026.5.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-25821}

* CQ-4362304: creare linee guida front-end e aggiornare l’interfaccia utente di configurazione LLM.
* GRANITE-39546: Aggiornare Apache Tika a 3.x.
* GRANITE-53957: Aggiornare Azure SDK V8 a V12 per oak-blob-azure.
* GRANITE-61245: rimuovere tutti gli utilizzi di commons-lang (sostituire con commons-lang3).
* GRANITE-64748: Gestore di autenticazione OIDC Bump.
* GRANITE-64764: Aggiornare il testo di Apache Commons alla versione 1.15.0.
* GRANITE-64963: Aggiornare Filevault alla versione 4.2.0.
* GRANITE-66197: aggiunta del supporto e-mail API del grafico Microsoft per i tenant M365.
* GRANITE-66449: Aggiornamento dei plug-in Maven per il supporto dell’API Java 17.
* GRANITE-66473: Aggiungere una libreria cache di caffeina a base-granite.
* GRANITE-66836: Aggiornare Quickstart ad Oak 2.0.0.
* SKYOPS-129301: imposta il livello di conformità Javadoc Jar delle API su Java 17.
* SKYOPS-129351: Aggiornare i flussi reattivi e il reactor-core per garantire la compatibilità con MCP SDK.
* SKYOPS-131412: Aggiornamento di Apache Commons Exec alla versione più recente.
* SKYOPS-131432: Aggiornare Felix SCR al 2.2.14.
* SKYOPS-131907: Aggiorna regioni API Sling al 1.1.10.
* SKYOPS-131938: aggiornare GSON alla versione più recente.
* SKYOPS-132173: aggiorna il codec Apache Commons alla versione più recente.
* SKYOPS-132182: aggiorna il bundle tenant Sling.
* SKYOPS-132267: aggiorna annotazione `org.osgi.service.component`.
* SKYOPS-132272: aggiorna il bundle Sling Feature Model.
* SKYOPS-132525: aggiungi Quickstart Analyzer per impedire nuove rimozioni API.
* SKYOPS-134408: Aggiornamento da `com.adobe.granite.asset.core` a 2.2.82.
* SKYOPS-137750: Aggiornamento da `com.adobe.granite.comments` a 1.0.40.
* SKYOPS-137759: Aggiornare `com.adobe.granite.jobs.async.ui.commons` alla versione 3.2.4.
* SKYOPS-138356: Aggiornamento da `com.adobe.granite.oauth.server` a 1.1.36.
* SKYOPS-138739: Aggiorna SnakeYAML a 2.6.

### Problemi risolti {#fixed-issues-25821}

* ASSETS-59546: rimuovi le dipendenze dalla libreria commons-lang obsoleta.
* ASSETS-64831: il conteggio dei tentativi di reimpostazione di AssetProcessorProcess causa il blocco delle risorse.
* ASSETS-66683: ciclo di approvazione causato da un errore uploadBlob.
* CNTBF-613: accesso corretto negato (JCR-101) durante la registrazione dei tipi di nodo.
* GRANITE-44537: stringa in &quot;Country/Region&quot; non localizzata in AEM.
* GRANITE-61760: correzione dell’attivazione di AdminUserInitializer non riuscita.
* GRANITE-64543: la risposta alle restrizioni di autorizzazione non segue la struttura API.
* GRANITE-66692: il caricatore di classi interno non è sensibile agli aggiornamenti dei pacchetti.
* GRANITE-66732: utilizza attivatori invece dei componenti del servizio per i bundle di livello 1 iniziali.
* GRANITE-66846: l&#39;API delle autorizzazioni di AEM non mostra la restrizione `rep:ntNames`.
* SITES-39267: Ripristina pagePath nelle voci della catena di relazioni.
* SITES-43715: la convalida delle autorizzazioni non riesce a leggere lo stato della risorsa.

#### AEM Guides {#guides-25821}

* GUIDES-45110: quando si seleziona un&#39;immagine nell&#39;editor utilizzando la finestra di dialogo **Seleziona file**, vengono visualizzati solo i formati raster (ad esempio JPG, PNG e GIF). I file vettoriali (ad esempio `.ai` e `.eps`) non vengono visualizzati e non possono essere selezionati.
* GUIDES-41938: se si crea un argomento in una cartella il cui nome contiene spazi, viene erroneamente creata una cartella duplicata in cui gli spazi vengono sostituiti da trattini e l&#39;argomento viene salvato in tale cartella al posto della cartella originale.
* GUIDES-38377: quando si applicano alle mappe esistenti le modifiche a un predefinito di output in un profilo Cartella, viene reimpostato il **contesto di pubblicazione** salvato per il predefinito AEM Sites.
* GUIDES-43547: quando si aprono argomenti o mappe di grandi dimensioni, l’istanza di authoring non risponde e in alcuni casi viene richiesto un riavvio.
* GUIDES-32520: quando si utilizza Backspace sugli elementi, l&#39;Editor scorre fino alla parte superiore dell&#39;argomento indipendentemente dalla posizione del cursore (Editor 2.0).

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-25821}

Nessuna.

### Funzioni e API obsolete {#deprecated-25821}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-25821}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione affronta 19 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-25821}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 2.0.0 | [API Oak 2.0.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
