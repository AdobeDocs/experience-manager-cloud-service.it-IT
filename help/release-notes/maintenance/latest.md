---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a3c414f9b5e575856a942e02661e8c70a7083495
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 89%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19149 {#19149}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 19149, rilasciata pubblicamente il 21 gennaio 2025. La versione di manutenzione precedente era la 18751.

Con la versione di attivazione funzioni 2025.1.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19149}

* ASSETS-45286: mostra l’avanzamento granulare del processo asincrono di archiviazione dei download.
* ASSETS-46296: supporto dei modelli Dynamic Media nel selettore risorse.
* ASSETS-44796: attiva gli eventi Assets per i processi delle risorse asincrone DAM.

### Problemi risolti {#fixed-issues-19149}

* GRANITE-55074: assicurati che le intestazioni di risposta CORS siano impostate sulle risposte di errore.
* ASSETS-43755: miglioramenti della scalabilità per correlare le risorse in blocco.
* ASSETS-45399: reindirizza alla console Assets dopo la creazione della Live Copy delle risorse.
* ASSETS-45462: problemi di memorizzazione in cache del browser con le miniature di cartelle personalizzate.
* ASSETS-46398: nasconde le azioni di download e rielaborazione dei modelli DM.
* ASSETS-44484: problemi durante il nuovo salvataggio della configurazione di Risorse collegate.
* ASSETS-44122: il processo di copia asincrona delle risorse non rinomina la cartella di destinazione durante la copia nella cartella corrente.
* ASSETS-44463: il pulsante Download CSV (Scarica CSV) non è visibile in caso di esportazione corretta dei metadati.
* ASSETS-45134: il processo di spostamento con il titolo della destinazione sovrascrive tutti i titoli delle cartelle.
* ASSETS-45137: conflitti con caricamenti in blocco tramite la vista Risorse.
* ASSETS-45758: dopo l’aggiunta di una relazione, le relazioni tra risorse ottengono un’animazione di carico/lavoro infinita.
* ASSETS-44148: l’evento NODE_MOVED in AEM può causare NPE spuria nei registri.
* ASSETS-28607: errore JS durante l’impostazione della miniatura video personalizzata.
* GRANITE-55781: migliore sincronizzazione dei gruppi tra Adobe Developer Console e AEM. Per ulteriori dettagli consulta [Modifiche alla sincronizzazione del gruppo utenti e profili di prodotto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).
* GRANITE-55754: assicurarsi che gli script di avvio di SDK supportino Java 21.
* GRANITE-54248: impossibile scorrere tutti gli elementi in una cartella risorse di grandi dimensioni.
* SCRNS-4597: miglioramenti alla visualizzazione dell’elenco dei risultati della ricerca.


### Problemi noti {#known-issues-19149}

Nessuno.

### Funzioni e API obsolete {#deprecated-19149}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

#### Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto

Quando si utilizza Adobe Admin Console per la gestione delle autorizzazioni, i seguenti gruppi NON DEVONO essere utilizzati in quanto non saranno più sincronizzati con AEM:
* Gruppi AEM che terminano con _GROUP_NAME_SUFFIX.
* Profili di prodotto da altri ambienti, programmi o prodotti.

Per ulteriori dettagli, controlla [Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Obsolescenza dell’editor SPA {#deprecate-spa-editor}

[L&#39;editor SPA](/help/implementing/developing/hybrid/introduction.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 2025.1.0. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless nell’AEM sono:

* [Editor universale](/help/edge/wysiwyg-authoring/authoring.md) per la modifica visiva.
* [Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo.

### Correzioni di sicurezza {#security-19149}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 4 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-19149}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
