---
title: Fase di implementazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica sulla fase di implementazione in Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: cba5dccd3b66220bbcd6d3b4dd5298702902b0e5
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---

# Fase di implementazione in Cloud Acceleration Manager {#implementation-phase-cam}

La fase di implementazione include:

* [Sviluppo locale](#local-development)
* [Refactoring del codice](#code-refactoring)
* [Distribuzione as a Cloud Service AEM](#aem-as-a-cloud-service-deployment)
* [Trasferimento dei contenuti](#content-transfer)


Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto e passare alla sezione **Implementazione** come illustrato nella figura riportata di seguito.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Fai riferimento a [Creazione e gestione di un progetto in Cloud Acceleration Manager](getting-started-cam.md#create-project) per ulteriori informazioni.


## Utilizzo della scheda Sviluppo locale {#local-development}

La scheda Sviluppo locale fornisce tutti i contenuti rilevanti per la configurazione dell’ambiente di sviluppo AEM locale quando si avvia la fase di implementazione del percorso di migrazione.

Leggi questa sezione per esplorare la scheda dell’attività Sviluppo locale:

1. Fai clic sul pulsante **Visualizza** dal pulsante **Sviluppo locale** Card.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Un carosello di contenuti mostra le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Utilizzo della scheda di refactoring del codice {#code-refactoring}

La scheda delle attività di refactoring del codice fornisce tutte le informazioni pertinenti ed evidenzia le aree di refactoring del codice da rivedere e risolvere quando si passa a AEM as a Cloud Service.

Leggi questa sezione per esplorare la scheda dell’attività Refactoring del codice:

1. Fai clic sul pulsante **Revisione** dal pulsante **Refactoring del codice** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. Nella pagina viene visualizzato l’elenco delle attività di refactoring del codice organizzate in base al livello di gravità. Per saperne di più, fai clic sulle due icone evidenziate.

   Nella pagina vengono visualizzate le considerazioni sul refactoring del codice in tre diverse schede:

   * Panoramica
   * Dispatcher
   * Test

>[!NOTE]
>Controlla il contenuto di queste schede per comprendere alcune aree aggiuntive che non sono coperte da Best Practices Analyzer.

Il **Dispatcher** Questa scheda fornisce informazioni su come strutturare le configurazioni di Apache e Dispatcher as a Cloud Service per l’AEM, nonché su come convalidarle ed eseguirle localmente prima di distribuirle negli ambienti Cloud. Descrive anche il debug in ambienti Cloud.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

Il **Test** fornisce informazioni su test funzionali, audit dell’esperienza e test dell’interfaccia utente.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Utilizzo della scheda di implementazione as a Cloud Service dell’AEM {#aem-as-a-cloud-service-deployment}

La scheda Distribuzione as a Cloud Service dell’AEM fornisce tutti i contenuti pertinenti che ti aiuteranno a distribuire il codice in as a Cloud Service per l’AEM.

Leggi questa sezione per esplorare la scheda di attività Scheda di implementazione as a Cloud Service per AEM:

1. Fai clic sul pulsante **Visualizza** dal pulsante **Distribuzione as a Cloud Service AEM** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Un carosello di contenuti mostra le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Utilizzo della scheda Content Transfer {#content-transfer}

La scheda Content Transfer (Trasferimento contenuti) consente di avviare e gestire il trasferimento dei contenuti dall’istanza AEM corrente all’AEM as a Cloud Service.

Leggi questa sezione per esplorare la scheda delle attività di Content Transfer:

1. Fai clic sul pulsante **Revisione** dal pulsante **Trasferimento dei contenuti** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Per avviare un trasferimento di contenuti è necessario creare un set di migrazione. Fai clic su **Crea set di migrazione**. Un set di migrazione consente di trasferire i contenuti a AEM as a Cloud Service.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Un set di migrazione scadrà dopo un periodo prolungato di inattività. Rivedi [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) per i dettagli.

   >[!NOTE]
   >Rivedi il [prerequisiti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html) e [best practice e linee guida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it) prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti).

1. Per compilare il set di migrazione e completare la fase di estrazione del trasferimento dei contenuti, è necessario scaricare e installare lo strumento Content Transfer (Trasferimento contenuti). Revisione [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it) per scoprire come utilizzare lo strumento Content Transfer (Trasferimento contenuti).

1. Per acquisire i contenuti dal set di migrazione in un ambiente su AEM as a Cloud Service, è necessario avviare un’acquisizione. Accedi a **Processi di acquisizione** e fai clic su **Nuova acquisizione**. Revisione [Acquisizione di contenuti in Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) per scoprire come completare la fase di acquisizione del trasferimento dei contenuti.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## Passaggio successivo {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come utilizzare la fase di implementazione, puoi passare alla revisione del passaggio successivo nella [Vai alla fase live](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
