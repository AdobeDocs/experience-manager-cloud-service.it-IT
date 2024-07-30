---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: dc7150c6ce971aa6f89fa24f7ca387cbb28db1f2
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 63%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 17258 {#release-17258}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 17258, rilasciata pubblicamente il mercoledì 30 luglio 2024. La versione di manutenzione precedente era 17098.

Con la versione di attivazione funzioni 2024.8.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-17258}

* ASSETS-31445 - Funzioni di modelli iniziali di Dynamic Medie
* ASSETS-40399 - Impostazioni della coda di trascrizione automatica DM aggiornate
* ASSETS-40873 - Consente di impostare il numero massimo di righe per l’esportazione dei metadati tramite la configurazione OSGI

### Problemi risolti {#fixed-issues-17258}

* ASSETS-30613 - La sostituzione della risorsa non elimina e non aggiunge la risorsa nel nuovo livello di consegna
* ASSETS-31882 - Accesso al file manifesto in streaming non consentito nell’ambiente di authoring
* ASSETS-39598 - Impossibile eliminare dal backend S3 le risorse il cui nome contiene caratteri speciali
* CNTBF-209 - Miglioramenti alla cancellazione dei processi di backflow
* SCRNS-3762 - Migliora playerLogger nel canale Sequence per inserire i registri nella console durante l&#39;anteprima del canale sul browser
* SCRNS-4455 - Pulsante &quot;Gestisci pubblicazione&quot; e &quot;Publish rapido&quot; mancante per gli utenti NON AMMINISTRATORI nel provider di contenuti per i canali
* SITES-22940 - Impossibile visualizzare il frammento di contenuto come payload del flusso di lavoro

### Problemi noti {#known-issues-17258}

Nessuno

### Notifica di modifica {#change-notice-17258}

* A partire da settembre 2024, AEM as a Cloud Service disabiliterà la serializzazione dei Risolutori risorse tramite il framework Sling Model Exporter. Per ulteriori dettagli, consulta la [documentazione](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md).

### Funzioni e API obsolete {#deprecated-17258}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Tecnologie incorporate {#embedded-tech-17258}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak API 1.66.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API SLING AEM | 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.25.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
