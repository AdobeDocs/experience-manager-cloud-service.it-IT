---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: ht
source-wordcount: '693'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18751 {#18751}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18751, rilasciata pubblicamente l’11 dicembre 2024. La versione di manutenzione precedente era la 18598.

Con la versione di attivazione funzioni 2025.1.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18751}

* SKYOPS-88509: supporto Java 21 per l’SDK di AEM.

### Problemi risolti {#fixed-issues-18751}

* ASSETS-42802: il pulsante Indietro su MFE non funziona sempre e mostra una finestra di dialogo aggiuntiva.
* ASSETS-44148: correzione dell’evento NODE_MOVE in AEM che può causare NPE.
* ASSETS-44418: correzione del problema relativo alla configurazione errata dell’ambiente corretto su Skyline.
* ASSETS-44821: correzione dell’aggiornamento del filtro eventi per includere i dati codificati con modulo URL per gli eventi di caricamento.
* CNTBF-298: correzione del problema a causa del quale la copia del contenuto fallisce a causa di conflitti UUID.
* CNTBF-331: [content-copy-bundle] versione 2.0.14.
* FORMS-16572: rimozione degli errori di test del flusso di lavoro per la build SDK Java 21.
* GRANITE-36205: aggiornamento automatico per la versione interna di Oak in QS.
* GRANITE-53704: miglioramento di Sling Discovery nel servizio di archivio.
* GRANITE-54300: aggiornamento di Oak all’ultima versione pubblica (1.70.0).
* GRANITE-54416: aggiornamento di Filevault alla versione 3.8.2.
* GRANITE-54462: configurazione di SubscriberAgents per l’utilizzo di hc.tags di “systemready”.
* GRANITE-54542: aggiornamento della dipendenza commons-io a 2.17.0.
* GRANITE-54658: aggiunta di configurazioni OSGi delayFactor e batch-size per fullGC in QS.
* GRANITE-54696: ampliamento dell’intervallo di importazione per l’API Jackrabbit.
* GRANITE-54803: disabilitazione di ClusterAtExchange in AEM quando imsauth è attivo.
* GRANITE-55095: aggiornamento di Oak all’ultima versione pubblica (1.72.0).
* GUIDES-20006: lo stato del documento contrassegnato con Fine ritorna allo stato Bozza prima di salvare una nuova versione, in modo che lo stato Fine non persista in alcuna versione del documento.
* GUIDES-21840: nell’output di PDF nativi, i titoli dei capitoli non sono presenti nel sommario, generando una gerarchia errata.
* GUIDES-19558: la modifica e il seguente salvataggio una linea di base su una configurazione cloud provoca un timeout dopo 1 minuto se la linea di base contiene un numero elevato di argomenti o mappe.
* GUIDES-19733: la traduzione delle mappe tramite l’utilizzo della linea di base diventa lenta e alla fine non riesce a caricare l’elenco di tutti gli argomenti e i file di mappe associati.
* SITES-26798: la promozione automatica di un lancio non aggiorna lo stato della promozione (data della promozione).
* SITES-27137: rimozione della dipendenza delle metriche Sling commons dal core MSM.
* SKYOPS-75446: correzione del problema per cui AEM a volte restituisce un errore 404 o pagine con contenuto mancante.
* SKYOPS-76366: nessuna metrica Jetty Threadpool nelle versioni AEM 15977 e successive.
* SKYOPS-82371: java.io.IOException: classFile.delete() non riuscito.
* SKYOPS-83369: l’avvio delle distribuzioni AEM non riesce se l’esecuzione del processo di trasformazione non genera bundle.
* SKYOPS-83910: correzione dei problemi di concorrenza rilevati in SKYOPS-82371.
* SKYOPS-84821: impostazione della configurazione sling.include.checkcontenttype del servlet principale Sling su true.
* SKYOPS-85798: correzione del processo di trasformazione che genera definizioni di indice vuote.
* SKYOPS-86251: aggiornamento ad AEM Analyser core 1.5.6 e abilitazione product-package-import analyser nel processo di trasformazione.
* SKYOPS-86710: rimozione degli errori di test Minify per la build SDK Java 21.
* SKYOPS-86745: aggiornamento a Sling ResourceResolver 1.12.2.
* SKYOPS-89616: è stato risolto il problema che impediva di creare un account tecnico in Adobe Developer Console.
* SKYOPS-89691: è stato corretto un ID artefatto non corretto utilizzato per gli avvisi ASM.
* SKYOPS-89699: avvertenze mancanti per le versioni precedenti di Groovy incorporate nella versione “orbinson” della Console Groovy.
* SKYOPS-88664: registra e proteggi dal caso in cui il file di mappa scaricato ha una riga superiore al limite di 1024.
* SKYOPS-89734: rilascio dell’immagine di Dispatcher 2.0.235.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in Experience Manager Guides, vedi [Roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-18751}

Nessuno.

### Funzioni e API obsolete {#deprecated-18751}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-18751}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 3 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-18751}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
