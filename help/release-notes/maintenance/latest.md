---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80affbf9d68de5cdba884ea7c7b277d834816613
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 42%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 25194 {#25194}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 25194, rilasciata al pubblico il giovedì 1 aprile 2026. La versione di manutenzione precedente era la 24678.

Con la versione di attivazione delle funzioni 2026.4.0 viene fornito il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

>[!NOTE]
>
>Il 24893 sulla versione è stato reso privato.

### Miglioramenti {#enhancements-25194}

* ASSETS-65127: metadati personalizzati di eventi: è stata migliorata la gestione dei nomi dei metadati.
* ASSETS-63313: creazione automatica di collegamenti correlati per risorse esportate e elementi principali basati su manifesti C2PA.
* ASSETS-10995: limita il numero di risorse in uno zip di download.

### Problemi risolti {#fixed-issues-25194}

* ASSETS-62882: visualizzazione Amministratore: la descrizione comando info si interrompe quando vengono caricati più nomi di file non validi.
* ASSETS-63642: il collegamento di condivisione non riesce a eseguire il rendering della risorsa in alcuni ambienti di sviluppo (SLA3).
* ASSETS-59267: NPE durante il caricamento dei metadati dell’applicazione per il payload di consegna.
* ASSETS-59227: esportazione metadati: le proprietà non selezionate non sono più incluse a causa della corrispondenza regex.
* ASSETS-65187: anteprima CSV in Cloud quando i dati della colonna contengono virgole di escape.
* ASSETS-63441: assicurati che tutti gli utenti abbiano le autorizzazioni per leggere la configurazione di Assets Omnisearch.
* SITES-40095: Editor metadati: i riferimenti dei frammenti di contenuto locali superano le 10 voci.

#### AEM Guides {#guides-25194}

* GUIDES-38412 : Quando si modifica un file Schematron `(*.sch)` e si utilizza la funzione Trova e sostituisci, il pannello Trova e sostituisci appare parzialmente fuori schermo nella parte inferiore, impedendo l&#39;accesso ai relativi campi e controlli di input.
* GUIDE-37806: quando lo stesso argomento viene riutilizzato in più mappe con diversi predefiniti condizionali, la pubblicazione della mappa più recente in Salesforce sovrascrive il contenuto dell’argomento, causando la visualizzazione di dati errati agli utenti delle mappe pubblicate in precedenza.
* GUIDE-39394: quando un&#39;immagine inizialmente gestita come risorsa specifica per una lingua con una versione specifica (ad esempio, in `/en/`) viene spostata in una cartella globale con una versione aggiornata e viene eseguita un&#39;esportazione della linea di base, la nuova linea di base continua a fare riferimento a versioni obsolete specifiche per la lingua dell&#39;immagine, causando un&#39;esportazione della linea di base non riuscita.
* GUIDES-39054: durante la creazione di una linea di base dinamica, a volte l’editor non risponde a causa di più richieste API simultanee, causando l’arresto di tutte le altre operazioni.
* GUIDES-37781: quando si assegna un utente a un’attività di revisione, il menu a discesa elenca tutti gli utenti anziché solo quelli associati ai progetti selezionati, generando opzioni utente non valide.
* GUIDES-39385: quando si apre un rapporto per una mappa, si verifica un ritardo nel caricamento del pannello Filtri.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-25194}

Nessuna.

### Funzioni e API obsolete {#deprecated-25194}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-25194}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 9 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-25194}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,90,0 | [API Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
