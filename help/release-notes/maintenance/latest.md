---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18311 {#18311}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18311, rilasciata pubblicamente il 22 ottobre 2024. La versione di manutenzione precedente era la 18175.

Con la versione di attivazione funzioni 2024.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18311}

* ASSETS-41820 : miglioramenti dell’indicizzazione per il watchdog di elaborazione.
* ASSETS-43720 : miglioramenti funzionali al watchdog di elaborazione.
* ASSETS-42554 : miglioramenti delle prestazioni per le cartelle di grandi dimensioni.
* SKYOPS-77603: gestione dei reindirizzamenti da parte degli utenti aziendali.

### Problemi risolti {#fixed-issues-18311}

* ASSETS-37534: modifiche nella ricerca per non esporre la proprietà utilizzata per la destinazione di approvazione.
* ASSETS-38322: rimozione della configurazione del provider dei criteri di pubblicazione Rimozione della funzione evento di pubblicazione.
* ASSETS-40482: problema di accessibilità nei pulsanti Riproduci/Pausa e Disattiva audio/Riattiva audio nel lettore video Scene7.
* ASSETS-40593: pagina di errore si verifica dopo aver fatto clic sul pulsante “Proprietà” in Risorse > File.
* ASSETS-40598: sincronizzazione di ritagli avanzati quando una risorsa non sincronizzata viene spostata in una cartella abilitata alla sincronizzazione.
* ASSETS-40743: problemi relativi all’attivazione della finestra di dialogo Sostituisci risorsa quando sono presenti determinati caratteri nel nome del file.
* ASSETS-40825: i facet di ricerca delle risorse scompaiono dopo la modifica del modulo di ricerca.
* ASSETS-41007: l’eliminazione in AEM talvolta lascia risorse orfane al momento della consegna.
* ASSETS-41172: i caratteri speciali dei modelli Dynamic Media non sono consentiti nel nome.
* ASSETS-41896: risorse menzionate in cq: le proprietà eliminate nella cartella NON devono essere pubblicate su Brand Portal.
* ASSETS-42067: Modelli Dynamic Media - Il download restituisce un errore.
* ASSETS-42070: Modelli Dynamic Media - Gli utenti non amministratori devono avere accesso alla creazione/modifica dei modelli.
* ASSETS-42344: sincronizzazione di collegamento delle risorse disconnessa - Riconnessione e consigli per il cliente.
* ASSETS-42620: problema con l’opzione di anteprima delle versioni della risorsa - mostra un’anteprima vuota quando viene aperta la risorsa.
* ASSETS-42701: problema di ritaglio e consegna delle immagini ottimizzate per il web.
* ASSETS-42966: la barricata asincrona può sbloccarsi per errore se più processi condividono lo stesso percorso.
* ASSETS-43072: Modelli Dynamic Media - La ricerca dei riferimenti del modello viene interrotta a causa di un riferimento non valido.
* ASSETS-43212: problemi di internazionalizzazione nell’editor schema metadati.
* ASSETS-43202: correzioni per la selezione di annotazioni da stampare dalla timeline.
* ASSETS-43502: nome del predefinito immagine esistente di AEM CS non visualizzato nella pagina di modifica.
* ASSETS-43538: il processo di copia asincrona delle risorse utilizza una proprietà non corretta per il percorso di origine.
* ASSETS-43798: controllo del percorso di destinazione prima che le risorse siano copiate.
* ASSETS-43945: aumento del ritardo dei tentativi a 20 minuti per la coda dei processi delle risorse asincrone.
* ASSETS-44025: il processo di eliminazione asincrona delle risorse non riesce quando vengono selezionate risorse singole.
* SITES-26128: eccezione di class cast in CreateLiveCopyStep.
* SCRNS-4551: il canale [Pool SG] Screens contenente il componente video mostra un “Errore generale di pagina” nell’anteprima e nel lettore del browser.

### Problemi noti {#known-issues-18311}

* FORMS-15818: la voce del descrittore del componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` non ha trovato istruzioni nei registri del server. Queste sono innocue istruzioni di registro.

### Funzioni e API obsolete {#deprecated-18311}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-18311}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 3 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-18311}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
