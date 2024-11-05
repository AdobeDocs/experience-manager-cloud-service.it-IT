---
title: Fase di implementazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica sulla fase di implementazione in Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
feature: Migration
role: Admin
source-git-commit: f86d681c8f8cb6d602058ef30b648c53ff7bad69
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---

# Fase di implementazione in Cloud Acceleration Manager {#implementation-phase-cam}

La fase di implementazione include:

* [Sviluppo locale](#local-development)
* [Refactoring del codice](#code-refactoring)
* [Implementazione di AEM as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Content Transfer](#content-transfer)


Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto e passare alla sezione **Implementazione**, come illustrato nella figura seguente.

![Pagina di destinazione del progetto - Implementazione](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Per ulteriori informazioni, vedere [Creazione e gestione di un progetto in Cloud Acceleration Manager](getting-started-cam.md#create-project).


## Utilizzo della scheda Sviluppo locale {#local-development}

La scheda Sviluppo locale fornisce tutti i contenuti pertinenti che possono aiutarti a configurare l’ambiente di sviluppo AEM locale quando inizi la fase di implementazione del percorso di migrazione.

Segui questa sezione per esplorare la scheda dell’attività Sviluppo locale:

1. Fai clic su **Visualizza** dalla scheda **Sviluppo locale**.

   ![Scheda Sviluppo Locale](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Un carosello di contenuti mostra le informazioni rilevanti per questa fase del percorso di migrazione.

   ![Carosello di sviluppo locale](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Utilizzo della scheda di refactoring del codice {#code-refactoring}

La scheda dell’attività Refactoring del codice fornisce tutte le informazioni pertinenti ed evidenzia le aree di refactoring del codice da rivedere e risolvere durante il passaggio ad AEM as a Cloud Service.

Segui questa sezione per esplorare la scheda dell’attività Refactoring del codice:

1. Fai clic su **Rivedi** dalla scheda attività **Refactoring del codice**.

   ![Scheda di refactoring del codice](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. Nella pagina viene visualizzato l’elenco delle attività di refactoring del codice organizzate in base al livello di gravità. Per saperne di più, fai clic sulle due icone evidenziate.

   Nella pagina vengono visualizzate le considerazioni sul refactoring del codice in tre diverse schede:

   * Panoramica
   * Dispatcher
   * Test

>[!NOTE]
>Rivedi il contenuto di queste schede per comprendere alcune aree aggiuntive non coperte da Best Practices Analyzer.

La scheda **Dispatcher** fornisce informazioni su come strutturare le configurazioni di AEM as a Cloud Service Apache e Dispatcher e su come convalidarle ed eseguirle localmente prima di distribuirle negli ambienti Cloud. Descrive anche il debug in ambienti Cloud.

![Scheda Dispatcher](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

La scheda **Test** fornisce informazioni sui test funzionali, dell&#39;audit dell&#39;esperienza e dell&#39;interfaccia utente.

![Scheda Test](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Utilizzo della scheda di implementazione di AEM as a Cloud Service {#aem-as-a-cloud-service-deployment}

La scheda Distribuzione di AEM as a Cloud Service fornisce tutti i contenuti rilevanti per la distribuzione del codice in AEM as a Cloud Service.

Leggi questa sezione per esplorare la scheda di attività Scheda di distribuzione AEM as a Cloud Service:

1. Fai clic su **Visualizza** dalla scheda attività **Distribuzione AEM as a Cloud Service**.

   ![Distribuzione AEM as a Cloud Service - scheda](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Un carosello di contenuti mostra le informazioni rilevanti per questa fase del percorso di migrazione.

   ![Distribuzione AEM as a Cloud Service - carosello](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Utilizzo della scheda Content Transfer {#content-transfer}

La scheda Content Transfer (Trasferimento contenuti) consente di avviare e gestire il trasferimento dei contenuti dall’istanza AEM corrente ad AEM as a Cloud Service.

Segui questa sezione per esplorare la scheda delle attività di Trasferimento contenuti:

1. Fai clic su **Rivedi** dalla scheda attività **Trasferimento contenuti**.

   ![Trasferimento contenuti - Revisione](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Per avviare un trasferimento di contenuti, devi creare un set di migrazione. Fare clic su **Crea set di migrazione**. Un set di migrazione consente di trasferire i contenuti ad AEM as a Cloud Service.

   ![Crea set di migrazione](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Un set di migrazione scade dopo un periodo prolungato di inattività. Per informazioni dettagliate, consulta [Scadenza set di migrazione](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry).

   >[!NOTE]
   >Consulta [prerequisiti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=it) e le [best practice e linee guida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it) prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti).

1. Scarica e installa lo strumento Content Transfer (Trasferimento contenuti) per popolare il set di migrazione e completare la fase di estrazione del trasferimento dei contenuti. Consulta [Guida introduttiva allo strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it) per scoprire come utilizzare lo strumento Content Transfer.

1. Per acquisire i contenuti dal set di migrazione in un ambiente su AEM as a Cloud Service, devi avviare un’acquisizione. Passa a **Processi di acquisizione** e fai clic su **Nuova acquisizione**. Rivedi [Acquisizione del contenuto in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per scoprire come completare la fase di acquisizione del trasferimento dei contenuti.

   ![Processi di acquisizione](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![Content Transfer Tool calculator](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## Passaggio successivo {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come utilizzare la fase di implementazione, puoi passare alla revisione del passaggio successivo della [fase di lancio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
