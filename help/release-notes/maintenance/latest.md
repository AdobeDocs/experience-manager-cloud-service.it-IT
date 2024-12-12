---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 37%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18751 {#18751}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18751, rilasciata pubblicamente il giovedì 11 dicembre 2024. La versione di manutenzione precedente era la 18598.

Con la versione di attivazione funzioni 2025.1.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18751}

* SKYOPS-88509: supporto Java 21 per l’SDK dell’AEM.

### Problemi risolti {#fixed-issues-18751}

* ASSETS-42802: il pulsante Indietro su MFE non funziona sempre e mostra una finestra di dialogo aggiuntiva.
* ASSETS-44148: l’evento NODE_MOVE corretto nell’AEM può causare NPE.
* ASSETS-44418: l’env di Correzione fissa non è configurato sulla skyline.
* ASSETS-44821: è stato corretto il filtro eventi di aggiornamento per includere dati con codifica URL modulo per gli eventi di caricamento.
* CNTBF-298: la copia a contenuto fisso non riesce e si verificano conflitti UUID.
* CNTBF-331: [content-copy-bundle] versione 2.0.14.
* FORMS-16572: rimozione degli errori dei test del flusso di lavoro per la build SDK Java 21.
* GRANITE-36205: aggiornamento automatico per la versione interna di oak in QS.
* GRANITE-53704: rivalutare l’individuazione Sling nel servizio archivio.
* GRANITE-54300: aggiornamento di Oak all’ultima versione pubblica (1.70.0).
* GRANITE-54416: aggiornamento di Filevault alla versione 3.8.2.
* GRANITE-54462: configura SubscriberAgents per utilizzare hc.tags di &quot;systemready&quot;.
* GRANITE-54542: aggiorna la dipendenza commons-io alla versione 2.17.0.
* GRANITE-54658: aggiungi le configurazioni OSGi delayFactor e batch-size per fullGC in QS.
* GRANITE-54696: amplia l’intervallo di importazione per l’API Jackrabbit.
* GRANITE-54803: disabilita ClusterAtExchange in AEM quando imsauth è attivo.
* GRANITE-55095: aggiornamento di Oak all’ultima versione pubblica (1.72.0).
* GUIDES-20006: lo stato del documento contrassegnato come Fine ritorna allo stato Bozza prima di salvare una nuova versione, in modo che lo stato Fine non persista in nessuna versione del documento.
* GUIDES-21840: nell’output di Native PDF, i titoli dei capitoli non sono presenti nel sommario, generando una gerarchia errata.
* GUIDES-19558: se la baseline contiene un numero elevato di argomenti o mappe, dopo 1 minuto si verifica un timeout durante la modifica e il salvataggio di una baseline in una configurazione cloud.
* GUIDES-19733: la traduzione delle mappe utilizzando la linea di base diventa lenta e alla fine non riesce a caricare l’elenco di tutti gli argomenti e i file di mappe associati.
* SITES-26798: La promozione automatica di Launch non aggiorna lo stato della promozione (data della promozione).
* SITES-27137: rimuovi la dipendenza delle metriche comuni Sling dal core MSM.
* SKYOPS-75446: l’AEM fisso talvolta restituisce una pagina 404 o pagine con contenuto mancante.
* SKYOPS-76366: nessuna metrica di Jetty Threadpool nelle 15977 sulla versione AEM e successive.
* SKYOPS-82371: java.io.IOException: classFile.delete() non riuscito.
* SKYOPS-83369: l’avvio delle distribuzioni AEM non riesce se l’esecuzione del processo di trasformazione non genera bundle.
* SKYOPS-83910: sono stati risolti i problemi di concorrenza in SKYOPS-82371.
* SKYOPS-84821: imposta la configurazione sling.include.checkcontenttype del servlet principale Sling su true.
* SKYOPS-85798: il processo di trasformazione fissa genera definizioni di indice vuote.
* SKYOPS-86251: effettua l’aggiornamento a AEM Analyzer Core 1.5.6 e abilita product-package-import analyzer nel processo di trasformazione.
* SKYOPS-86710: rimozione degli errori di test Minify per la build sdk Java 21.
* SKYOPS-86745: aggiornamento a Sling ResourceResolver 1.12.2.
* SKYOPS-89616: risolto Impossibile creare un account tecnico in Adobe Developer Console.
* SKYOPS-89691: è stato corretto un ID artefatto non corretto utilizzato per gli avvisi ASM.
* SKYOPS-89699: avvertenze mancanti per le versioni precedenti di Groovy incorporate nel sapore &quot;orbinson&quot; della Console di Groovy.
* SKYOPS-88664: registra e proteggi da un caso quando il file di mappa scaricato ha una riga superiore al limite 1024.
* SKYOPS-89734: rilascia l’immagine del dispatcher 2.0.235.

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
| AEM Oak | 1 72,0 | [API Oak API 1.72.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
