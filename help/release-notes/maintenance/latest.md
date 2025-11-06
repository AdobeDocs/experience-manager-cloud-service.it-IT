---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 45%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

>[!NOTE]
>
>Le 23122 sulla versione sono diventate private il 3 novembre.

## Versione 22943 {#22943}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 22943, rilasciata pubblicamente il mercoledì 14 ottobre 2025. La versione di manutenzione precedente era la 22758.

Con la versione di attivazione delle funzioni 2025.10.0 viene fornito il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-22943}

* ASSETS-57809: aggiornamento della definizione dell’indice per damAssetLucene-13.
* ASSETS-36521: è stato migliorato il flusso di lavoro di ricaricamento DM per garantire una post-elaborazione coerente.
* ASSETS-56400: aggiunta nuova rappresentazione OOTB Zoom PNG per le risorse con trasparenza.
* ASSETS-55326: è stata abilitata la vista di configurazione della cartella di metadati di IA tramite eventi HTTP.
* ASSETS-56905: supporta la connessione a Indesign tramite proxy.
* ASSETS-48286: aggiungi le proprietà CAI a Algolia per GenStudio.
* ASSETS-48653: applica la filigrana invisibile nella fase di preelaborazione.
* ASSETS-55874: migrazione del predefinito immagine da scene7 a DMWithOpenapi.
* SITES-30452: miglioramenti API del contenuto per ASO sull’endpoint /content/definition.

### Problemi risolti {#fixed-issues-22943}

* ASSETS-56301: è stata corretta l’esportazione selettiva dei metadati per includere PredictedTags nel file CSV.
* ASSETS-55543: logica di elaborazione asincrona refactoring in un bundle riutilizzabile.
* ASSETS-54789: è stato corretto l’errore NPE in ACLPermissionsValidator quando DM ACL è abilitato.
* ASSETS-55888: è stata corretta la rappresentazione di malware visualizzata nel pannello delle rappresentazioni dell’interfaccia utente.
* GRANITE-62236: è stato corretto un problema di localizzazione delle parole chiave nelle ricerche salvate per raccolte avanzate.
* GRANITE-61875: è stato corretto un problema di hotfix relativo alla &quot;valutazione di espressioni non valide&quot; che impediva il salvataggio di frammenti di contenuto e download di risorse.
* SITES-24074: È stata corretta la navigazione mobile nascosta che riceveva lo stato attivo durante la navigazione tramite tastiera.
* SITES-33611: problema di panoramica della Live Copy fissa per i mercati a volume elevato.

#### AEM Guides {#guides-22943}

* GUIDE-31421: quando più mappe o argomenti DITA sono aperti e uno degli argomenti è chiuso, il pulsante **>>** che mostra tutte le schede aperte si sovrappone alle altre schede aperte sulla barra delle schede.
* GUIDES-33229: durante la generazione di PDF, le regole di filtro in un file DITAVAL vengono ignorate se un nome di proprietà contiene un punto.
* GUIDES-33720: quando si ingrandisce la schermata dell’interfaccia utente di traduzione, il pulsante Invia per traduzione si sposta sotto i puntini di sospensione e viene attivato anche senza selezionare alcuna risorsa.
* GUIDES-33590: quando un revisore completa un’attività di revisione o l’iniziatore aggiorna un’attività di revisione senza inserire commenti, nell’e-mail di notifica inviata viene visualizzato il commento precedente più recente.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Funzioni e API obsolete {#deprecated-22943}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-22943}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 14 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Notifica di modifica

* Questa versione contiene le seguenti nuove versioni dell’indice del prodotto:
* **damAssetLucene-13**

### Tecnologie incorporate {#embedded-tech-22943}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.86.0 | [API Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.2. | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
