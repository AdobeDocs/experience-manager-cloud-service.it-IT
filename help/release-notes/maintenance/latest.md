---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 38%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18311 {#18311}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18311, rilasciata pubblicamente il mercoledì 22 ottobre 2024. La versione di manutenzione precedente era la 18175.

Con la versione di attivazione funzioni 2024.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18311}

* ASSETS-41820 : miglioramenti dell’indicizzazione per il watchdog di elaborazione.
* ASSETS-43720 : miglioramenti funzionali all’watchdog di elaborazione.
* ASSETS-42554 : miglioramenti delle prestazioni per le cartelle di grandi dimensioni.
* SKYOPS-77603: gestione dei reindirizzamenti da parte degli utenti aziendali.

### Problemi risolti {#fixed-issues-18311}

* ASSETS-37534 : cambia nella ricerca per non esporre la proprietà utilizzata per il target di approvazione.
* ASSETS-38322 : rimuovi la configurazione del provider dei criteri di pubblicazione Rimuovi la funzione evento di pubblicazione.
* ASSETS-40482: problema di accessibilità nei pulsanti Riproduci/Pausa e Disattiva audio/Riattiva audio nel lettore video Scene7.
* ASSETS-40593: La pagina di errore si verifica dopo aver fatto clic sul pulsante &quot;Proprietà&quot; in Assets > File.
* ASSETS-40598: sincronizza gli smart crop quando una risorsa non sincronizzata viene spostata in una cartella sincronizzata.
* ASSETS-40743 : problemi relativi all’attivazione della finestra di dialogo Sostituisci risorsa quando sono presenti determinati caratteri nel nome file.
* ASSETS-40825 : I Facet Di Ricerca Di Assets Scompaiono Dopo La Modifica Del Modulo Di Ricerca.
* ASSETS-41007: l’eliminazione nell’AEM talvolta lascia orfano Assets al momento della consegna.
* ASSETS-41172 : i caratteri speciali dei modelli Dynamic Medie non sono consentiti nel nome.
* ASSETS-41896: l’Assets menzionato nella proprietà cq:discarded della cartella NON deve essere pubblicato in Brand Portal.
* ASSETS-42067 : Modelli Dynamic Medie - Il download restituisce un errore.
* ASSETS-42070 : Modelli Dynamic Medie - Gli utenti non amministratori devono avere accesso alla creazione/modifica dei modelli.
* ASSETS-42344 : Sincronizzazione Assets connessa disconnessa - Riconnessione e consigli per il cliente.
* ASSETS-42620 : problema con l’opzione di anteprima versioni risorsa - mostra un’anteprima vuota quando si apre la risorsa.
* ASSETS-42701: problema di consegna e ritaglio delle immagini ottimizzate per il web.
* ASSETS-42966: le barricate asincrone possono sbloccarsi per errore a causa della condivisione dello stesso percorso da parte di più processi.
* ASSETS-43072 : Modelli Dynamic Medie - I riferimenti al modello non funzionano più se si utilizza un riferimento non valido.
* ASSETS-43212: problemi di internazionalizzazione nell’editor schema metadati.
* ASSETS-43202 : Correzioni per la selezione di annotazioni da stampare dalla timeline.
* ASSETS-43502: nome del predefinito immagine esistente di AEM CS non visualizzato nella pagina di modifica.
* ASSETS-43538: il processo di copia asincrona delle risorse utilizza una proprietà non corretta per il percorso di origine.
* ASSETS-43798 : controlla il percorso di destinazione prima di copiare le risorse.
* ASSETS-43945: aumento del ritardo dei tentativi a 20 minuti per la coda dei processi delle risorse asincrone.
* ASSETS-44025: il processo di eliminazione asincrona delle risorse non riesce per quando vengono selezionate singole risorse.
* SITES-26128 : Eccezione del cast di classe in CreateLiveCopyStep.
* SCRNS-4551 : [I pool SG] nel canale Screens contenente il componente video viene visualizzato &quot;Errore generale di pagina&quot; nell&#39;anteprima e nel lettore del browser

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
