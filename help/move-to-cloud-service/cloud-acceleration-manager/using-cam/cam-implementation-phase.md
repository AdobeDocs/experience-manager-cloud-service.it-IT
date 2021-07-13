---
title: Fase di implementazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica della fase di implementazione in Cloud Acceleration Manager.
source-git-commit: 4041e3fd9a479a64ed38e2bf1a6251fda39e55c2
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Fase di implementazione in Cloud Acceleration Manager {#implementation-phase-cam}

La fase di implementazione include:

* [Sviluppo locale](#local-development)
* [Refactoring del codice](#code-refactoring)
* [Distribuzione AEM come Cloud Service](#aem-as-a-cloud-service-deployment)
* [Trasferimento dei contenuti](#content-transfer)


Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto e passa alla sezione **Implementazione** , come illustrato nella figura seguente.

![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Per ulteriori informazioni, consulta [Creazione e gestione di un progetto in Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) .


## Utilizzo della scheda di sviluppo locale {#local-development}

La scheda Sviluppo locale fornisce tutti i contenuti pertinenti che consentono di configurare l’ambiente di sviluppo AEM locale all’avvio della fase di implementazione del percorso di migrazione.

Segui questa sezione per esplorare la scheda dell&#39;attività Sviluppo locale :

1. Fai clic sul pulsante **Visualizza** dalla scheda **Sviluppo locale** .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. Viene visualizzato un carosello di contenuti con le informazioni pertinenti per questa fase del percorso di migrazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## Utilizzo della scheda di refactoring del codice {#code-refactoring}

La scheda dell’attività Refactoring del codice fornisce tutte le informazioni pertinenti ed evidenzia le aree di refactoring del codice che devi rivedere quando passi a AEM come Cloud Service.

Leggi questa sezione per esplorare la scheda dell’attività Refactoring del codice :

1. Fai clic sul pulsante **Rivedi** dalla scheda di attività **Refactoring del codice** .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. Nella pagina viene visualizzato l’elenco delle attività di refactoring del codice organizzate in base al livello di gravità. Per saperne di più, fai clic sulle due icone evidenziate.

   >[!NOTE]
   >Inoltre, controlla il contenuto delle schede nella pagina per comprendere alcune aree aggiuntive non coperte da Best Practices Analyzer.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## Utilizzo di AEM come scheda di distribuzione del Cloud Service {#aem-as-a-cloud-service-deployment}

AEM come scheda di distribuzione del Cloud Service fornisce tutto il contenuto pertinente che ti aiuterà a distribuire il codice in AEM come Cloud Service.

Segui questa sezione per esplorare AEM come scheda attività Cloud Service della scheda di distribuzione:

1. Fai clic sul pulsante **Visualizza** dalla scheda di attività **AEM come Cloud Service Deployment** .

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. Viene visualizzato un carosello di contenuti con le informazioni pertinenti per questa fase del percorso di migrazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Utilizzo della scheda di trasferimento dei contenuti {#content-transfer}

La scheda dell’attività Content Transfer (Trasferimento contenuti) fornisce indicazioni e considerazioni da rivedere quando si utilizza lo strumento Content Transfer (Trasferimento contenuti) per spostare i contenuti dall’istanza AEM corrente a AEM come Cloud Service.

Leggi questa sezione per esplorare la scheda delle attività Content Transfer (Trasferimento contenuti):

1. Fai clic sul pulsante **Visualizza** dalla scheda di attività **Trasferimento contenuti**.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. Viene visualizzato un carosello di contenuti con le informazioni pertinenti per questa fase del percorso di migrazione.

   ![immagine](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >Leggi i [prerequisiti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) e le [best practice e linee guida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti).

### Stima dell’attività dello strumento Content Transfer (Trasferimento contenuti) {#calculating}

È stato fornito un nuovo calcolatore dello strumento Content Transfer (Trasferimento contenuti) per stimare quanto tempo potrebbe essere necessario per completare l’attività di trasferimento dei contenuti. Puoi utilizzare il cursore delle dimensioni dell’archivio dei contenuti per selezionare le dimensioni da applicare al progetto. I tempi di trasferimento variano per le fasi di estrazione e acquisizione.

Per stimare le dimensioni dell&#39;archivio AEM, è possibile eseguire il rapporto Utilizzo disco in `http://HOST:PORT/etc/reports/diskusage.html`.

Puoi anche stimare le dimensioni di percorsi di archivio specifici utilizzando il parametro `path` , ad esempio `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## Novità {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come utilizzare la fase di implementazione, ora sei pronto per passare alla revisione del passaggio successivo, [Utilizzo di Go Live Phase](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
