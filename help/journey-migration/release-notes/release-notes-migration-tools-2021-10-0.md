---
title: Note sulla versione 2021.10.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2021.11.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 11%

---

# Note sulla versione 2021.10.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2021.10.0 degli strumenti di migrazione in AEM as a Cloud Service.

>[!NOTE]
>Per visualizzare le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=it).

## Cloud Acceleration Manager {#cam-release}

### Data di rilascio {#release-date-cam}

La data di pubblicazione di Cloud Acceleration Manager è il 25 ottobre 2021.

### Novità {#what-is-new-cam}

Cloud Acceleration Manager ora consente agli utenti di visualizzare i rapporti BPA storici in un rapporto della linea di tendenza. Con questo rapporto, gli utenti possono visualizzare lo stato di avanzamento che stanno facendo in una rappresentazione grafica di facile utilizzo. Consulta [Utilizzo della linea di tendenza della vista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#trendline-view-cam) per ulteriori dettagli.

### Data di rilascio {#release-date-october-cam}

La data di pubblicazione di Cloud Acceleration Manager è il 4 ottobre 2021.

### Novità {#what-is-new-cam-oct}

Cloud Acceleration Manager ora consente agli utenti di visualizzare i rapporti BPA in un’anteprima stampabile, che può essere stampata o stampata su PDF per facilitarne la condivisione. Vedere i passaggi 6 e 7 in [Utilizzo della scheda Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#best-practices-analysis).


## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt-oct}

* È stato migliorato lo strumento di mappatura utente con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori dettagli, consulta [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html).
   * Verifica la connessione all’API User Management prima di eseguire la mappatura utente
   * Ignora gli errori e continua con l’attività Mappatura utenti
   * La mappatura degli utenti non ha più esito negativo se **Token di accesso** scade dopo 24 ore. La mappatura utente può essere eseguita nuovamente dal punto in cui è stata interrotta l’ultima volta.

* Per aumentare la robustezza dello strumento Content Transfer (Trasferimento contenuti), il contenuto può essere acquisito nell’istanza di authoring o di pubblicazione alla volta. Consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it) per ulteriori dettagli.

* Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per migrare gli eventi di controllo.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new-bpa-oct}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Possibilità di rilevare e segnalare le dimensioni totali dell’indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca la rappresentazione originale.
