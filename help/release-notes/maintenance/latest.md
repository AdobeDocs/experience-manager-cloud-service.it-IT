---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2a7b83b99547637e02ec7cef9c92c5dd794a9adc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 36%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 24893 {#release-24893}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 24893, rilasciata al pubblico il mercoledì 17 marzo 2026. La versione di manutenzione precedente era la 24678.

Con la versione di attivazione funzioni 2026.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-24893}

* CNTBF-613: accesso corretto negato (JCR-101) - impossibile registrare i tipi di nodo.
* GRANITE-53957: Aggiornare Azure SDK V8 a V12 per oak-blob-azure.
* GRANITE-57035: utilizza Bouncy Castle come provider di sicurezza predefinito.
* GRANITE-59249: evita la registrazione di un provider di sicurezza nella JVM.
* GRANITE-61564: impossibile aprire la visualizzazione delle impostazioni in `/security/users.html` per gli amministratori.
* GRANITE-64748: OIDC: scadenza del cookie configurabile sling.oauth-request-key.
* SITES-39767: supporta il valore nonce tramite l’attributo di richiesta (CSP).
* SKYOPS-129301: imposta il livello di conformità javadoc jar delle API su 17.
* GRANITE-64962: Aggiornare Apache Jackrabbit Oak alla versione 1.92.0.
* GRANITE-64963: Aggiornare Apache Jackrabbit Filevault alla versione 4.2.0.
* GRANITE-64764: Aggiornamento del testo di Apache Commons alla versione 1.15.0.
* SKYOPS-131412: Aggiornamento Apache Commons Exec alla versione 1.6.0.
* SKYOPS-131432: Aggiornare Felix SCR al 2.2.14.
* SKYOPS-131907: aggiorna l’area geografica dell’API Sling al 1.1.10.
* SKYOPS-131938: aggiornare GSON alla versione 2.13.2.
* SKYOPS-132173: Aggiornamento del codec Apache Commons alla versione 1.21.0.
* SKYOPS-132182: aggiorna tenant Sling alla versione 1.1.8.
* SKYOPS-132267: Aggiorna org.osgi.service.component a 1.5.1.
* SKYOPS-132272: aggiorna il modello di feature Sling alla versione 2.0.4.
* SKYOPS-133689: aggiorna Dispatcher per utilizzare Apache httpd 2.4.66.

### Problemi risolti {#fixed-issues-24893}

* GRANITE-64443: `workflow.core` rimuovere le esportazioni obsolete di `log4j`.
* GRANITE-64543: la risposta alle restrizioni di autorizzazione deve corrispondere al contratto API.

#### AEM Guides {#guides-24893}

* GUIDES-38412 : Quando si modifica un file Schematron `(*.sch)` e si utilizza la funzione Trova e sostituisci, il pannello Trova e sostituisci appare parzialmente fuori schermo nella parte inferiore, impedendo l&#39;accesso ai relativi campi e controlli di input.
* GUIDE-37806: quando lo stesso argomento viene riutilizzato in più mappe con diversi predefiniti condizionali, la pubblicazione della mappa più recente in Salesforce sovrascrive il contenuto dell’argomento, causando la visualizzazione di dati errati agli utenti delle mappe pubblicate in precedenza.
* GUIDE-39394: quando un&#39;immagine inizialmente gestita come risorsa specifica per una lingua con una versione specifica (ad esempio, in `/en/`) viene spostata in una cartella globale con una versione aggiornata e viene eseguita un&#39;esportazione della linea di base, la nuova linea di base continua a fare riferimento a versioni obsolete specifiche per la lingua dell&#39;immagine, causando un&#39;esportazione della linea di base non riuscita.
* GUIDES-39054: durante la creazione di una linea di base dinamica, a volte l’editor non risponde a causa di più richieste API simultanee, causando l’arresto di tutte le altre operazioni.
* GUIDES-37781: quando si assegna un utente a un’attività di revisione, il menu a discesa elenca tutti gli utenti anziché solo quelli associati ai progetti selezionati, generando opzioni utente non valide.
* GUIDES-39385: quando si apre un rapporto per una mappa, si verifica un ritardo nel caricamento del pannello Filtri.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-24893}

Nessuna.

### Funzioni e API obsolete {#deprecated-24893}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-24893}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 9 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-24893}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1 92,0 | [API Oak 1.92.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
