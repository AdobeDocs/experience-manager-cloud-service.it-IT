---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82be9b2b328343e827b90bd8266d93127757f477
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 39%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17569 {#release-17569}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17569, rilasciata al pubblico il mercoledì 27 agosto 2024. La precedente versione di manutenzione era la 17465.

Con la versione di attivazione della funzione 2024.9.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17569}

* CQ-4353778: Eventi del processo di traduzione.
* CQ-4354583: invia eventi del processo di traduzione tramite la pipeline Adobe.
* CQ-4356479: consenti solo al codice Adobe di utilizzare il contesto del servlet /adobe.
* CQ-4358133: ottimizzare l’utilizzo di Jenkins worker.
* CQ-4358226: la funzionalità Salva parola chiave di traduzione non funziona per un particolare formato stringa.
* CQ-4358270: Kit di traduzione AEM: 8 agosto.
* CQ-4358310: aggiungi oak-compat-query-spi-1.2 a quickstart.
* GRANITE-36205: Aggiornamento automatico per il rilascio interno di oak in QS.
* GRANITE-49833: supporto del batch per il mittente dell’evento e il proxy.
* GRANITE-52053: Rimuovi gli utilizzi di Commons Collections 3: Platform other.
* GRANITE-52492: recupero asincrono elastico in caso di ripristino PIT.
* GRANITE-53086: Aggiorna la versione del plug-in jacoco al 0.8.12 in AEMaaCS.
* GRANITE-53099: Aggiornamento ad Apache Felix Http Jetty 5.1.24.
* GRANITE-53125: aggiungi la classificazione a CloudEvent.
* GRANITE-53328: Aggiornamento di Filevault a 3.8.0-T20240726111512-3cc11d50 contenente miglioramenti alla registrazione dello stashing.
* GRANITE-53340: AEM660: controllo delle versioni e ramificazione corretti per 660 CQ/Platform.
* GRANITE-53341: non visualizzare avvisi sull’utilizzo di ACS Commons 6.
* GRANITE-53453: aggiornamento di commons-lang alla versione 3.15.0.
* GRANITE-53473: impostazioni Sling non obsolete.
* GRANITE-53478: Aggiornare Filevault alla versione 3.8.0.
* GRANITE-53505: Aggiornare QS a commons-collections-3.2.2-adobe-2.
* GRANITE-53528: Aggiornare la versione degli artefatti della piattaforma.
* GRANITE-53547: fornisci API alternative evitando l’utilizzo di Apache Commons Lang 2.
* GRANITE-53575: utilizzare BSAFE 6.2.5 in CS.
* GRANITE-53608: Aggiornare Oak all’ultima versione pubblica (1.68.0).
* SITES-23583: i test di Sites Evergreen non riescono su Java 17.
* SKYOPS-79535: aggiornamento allo script rum v2.
* SKYOPS-79816: abilitare l’attività di Sling Feature Analyzer per le mappature degli utenti del servizio in FACT Tool.
* SKYOPS-81179: l’AEM crea dei test per l’attivazione dei bundle.
* SKYOPS-81866: visualizza avvisi per i bundle noti per essere incompatibili con Java 21.
* SKYOPS-82660: aggiorna l’API Sling alla versione 2.27.6.
* SKYOPS-82961: aggiornamento a Sling ResourceResolver 1.12.0-T20240723153354-a0270a0.
* SKYOPS-83356: crea un dashboard globale per il tracciamento delle versioni JVM utilizzate nelle distribuzioni AEM.
* SKYOPS-83436: il rollout di Java Runtime 21 interrompe la creazione di moduli adattivi AEM Forms.
* SKYOPS-84272: registra la versione Java utilizzata all’avvio del modulo di avvio di AEM.

### Problemi risolti {#fixed-issues-17569}

* CMGR-60225: errore di esecuzione della pipeline identificato sul cliente AEM Sites CS durante la convalida dell’aggiornamento alle 17486 sulla versione AEM.
* GRANITE-45919: Paesi soggetti a embargo nell’elenco Paese in Modifica impostazioni utente.
* GRANITE-51715: il selettore a volte non immette la selezione nel campo di testo.
* GRANITE-53290: controlla correttamente il protocollo durante l’analisi dell’URL nel controllo XSS.
* GRANITE-53576: definizione errata della classificazione del servizio nelle configurazioni OSGi.
* SKYOPS-82129: Memoryleak nei modelli Sling.

### Problemi noti {#known-issues-17569}

Nessuno.

### Notifica di modifica {#change-notice-17569}

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-17569}

Si noti che è in corso l’aggiornamento di `com.day.cq.wcm.api` e con la versione corrente sono stati contrassegnati come `@Deprecated` alcuni dei relativi metodi e classi. Questi verranno rimossi nelle versioni future, quindi se utilizzi uno di questi, valuta di passare alle alternative suggerite.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-17569}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 4 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-17569}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,68,0 | [API Oak API 1.68.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API SLING AEM | 2.27.6 | [API Sling Apache 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2,26,0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
