---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e035c1c27f652af231034588eb1359354182dcb0
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 62%

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
