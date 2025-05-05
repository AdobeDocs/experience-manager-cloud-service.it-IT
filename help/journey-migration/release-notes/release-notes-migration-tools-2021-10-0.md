---
title: Note sulla versione 2021.10.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2021.11.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 7%

---

# Note sulla versione 2021.10.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>
>Per le ultime note sulla versione, consulta [Note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Cloud Acceleration Manager {#cam-release}

### Data di pubblicazione {#release-date-cam}

La data di rilascio per Cloud Acceleration Manager è il 25 ottobre 2021.

### Novità {#what-is-new-cam}

Cloud Acceleration Manager ora consente agli utenti di visualizzare i rapporti BPA storici in un rapporto linea di tendenza. Con questo rapporto, gli utenti possono visualizzare lo stato di avanzamento che stanno facendo in una rappresentazione grafica di facile utilizzo. Per ulteriori dettagli, vedere [Utilizzo della linea di tendenza della visualizzazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=it#trendline-view-cam).

### Data di pubblicazione {#release-date-october-cam}

La data di rilascio per Cloud Acceleration Manager è il 4 ottobre 2021.

### Novità {#what-is-new-cam-oct}

Cloud Acceleration Manager offre agli utenti la possibilità di visualizzare i rapporti BPA in un&#39;anteprima stampabile, che consente una semplice stampa o stampa su PDF per una facile condivisione. Consulta i passaggi 6 e 7 in [Utilizzo della scheda Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=it#best-practices-analysis).


## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt-oct}

* È stato migliorato lo strumento di mappatura utente con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori dettagli, vedere [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=it).
   * Verifica la connessione all’API User Management prima di eseguire la mappatura utente
   * Ignora gli errori e continua con l’attività Mappatura utenti
   * Il mapping degli utenti non ha più esito negativo se **il token di accesso** scade dopo 24 ore. La mappatura utente può essere eseguita nuovamente dal punto in cui è stata interrotta l’ultima volta.

* Per aumentare la robustezza dello strumento Content Transfer (Trasferimento contenuti), il contenuto può essere acquisito in un’istanza Author o Publish alla volta. Per ulteriori dettagli, vedere [Guida introduttiva allo strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it).

* Quando sono incluse le versioni, il percorso `/var/audit` viene incluso automaticamente per migrare gli eventi di controllo.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new-bpa-oct}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Possibilità di rilevare e segnalare le dimensioni totali dell’indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca la rappresentazione originale.
