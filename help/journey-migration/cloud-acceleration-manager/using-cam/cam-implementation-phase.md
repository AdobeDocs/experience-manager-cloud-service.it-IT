---
title: Fase di implementazione in Cloud Acceleration Manager
description: Questa pagina fornisce una panoramica della fase di implementazione in Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 24331b974ded34ef949cc3d6fb157b124c145dee
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# Fase di implementazione in Cloud Acceleration Manager {#implementation-phase-cam}

La fase di implementazione include:

* [Sviluppo locale](#local-development)
* [Refactoring del codice](#code-refactoring)
* [Distribuzione as a Cloud Service AEM](#aem-as-a-cloud-service-deployment)
* [Trasferimento dei contenuti](#content-transfer)


Fai clic sulla scheda del progetto per aprire la pagina di destinazione del progetto e passare alla **Implementazione** come illustrato nella figura riportata di seguito.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Fai riferimento a [Creazione e gestione di un progetto in Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) per saperne di più.


## Utilizzo della scheda di sviluppo locale {#local-development}

La scheda Sviluppo locale fornisce tutti i contenuti pertinenti che consentono di configurare l’ambiente di sviluppo AEM locale all’avvio della fase di implementazione del percorso di migrazione.

Segui questa sezione per esplorare la scheda dell&#39;attività Sviluppo locale :

1. Fai clic sul pulsante **Visualizza** dal pulsante **Sviluppo locale** il Card.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Un carosello di contenuti visualizza le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Utilizzo della scheda di refactoring del codice {#code-refactoring}

La scheda dell’attività Refactoring del codice fornisce tutte le informazioni pertinenti ed evidenzia le aree di refactoring del codice che devi rivedere e risolvere quando passi a AEM as a Cloud Service.

Leggi questa sezione per esplorare la scheda dell’attività Refactoring del codice :

1. Fai clic sul pulsante **Revisione** dal pulsante **Refactoring del codice** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. Nella pagina viene visualizzato l’elenco delle attività di refactoring del codice organizzate in base al livello di gravità. Per saperne di più, fai clic sulle due icone evidenziate.

   La pagina visualizza le considerazioni sul refactoring del codice in tre schede diverse:

   * Panoramica
   * Dispatcher
   * Test

>[!NOTE]
>Controlla il contenuto di queste schede per comprendere alcune aree aggiuntive non coperte da Best Practices Analyzer.

La **Dispatcher** scheda fornisce informazioni su come strutturare le configurazioni di Apache e Dispatcher as a Cloud Service AEM nonché su come convalidarle ed eseguirle localmente prima di distribuirle negli ambienti Cloud. Descrive anche il debug negli ambienti Cloud.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

La **Test** La scheda fornisce informazioni su funzionalità, controllo esperienza e test dell’interfaccia utente.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Utilizzo AEM scheda di distribuzione as a Cloud Service {#aem-as-a-cloud-service-deployment}

AEM scheda Implementazione as a Cloud Service fornisce tutti i contenuti pertinenti che consentono di distribuire il codice AEM as a Cloud Service.

Segui questa sezione per esplorare AEM scheda attività Scheda distribuzione as a Cloud Service:

1. Fai clic sul pulsante **Visualizza** dal pulsante **Distribuzione as a Cloud Service AEM** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Un carosello di contenuti visualizza le informazioni rilevanti per questa fase del percorso di migrazione.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Utilizzo della scheda di trasferimento dei contenuti {#content-transfer}

La scheda Content Transfer (Trasferimento contenuti) consente di avviare e gestire il trasferimento dei contenuti dall’istanza AEM corrente a AEM as a Cloud Service.

Leggi questa sezione per esplorare la scheda delle attività Content Transfer (Trasferimento contenuti):

1. Fai clic sul pulsante **Revisione** dal pulsante **Trasferimento dei contenuti** scheda attività.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Per avviare un trasferimento di contenuti, devi creare un set di migrazione. Fai clic su **Creare un set di migrazione**. Un set di migrazione consente di trasferire i contenuti in AEM as a Cloud Service.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Controlla la [prerequisiti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) e [best practice e linee guida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti).

1. Sarà necessario scaricare e installare lo strumento Content Transfer (Trasferimento contenuti) per popolare il set di migrazione e completare la fase di estrazione del trasferimento di contenuti. Revisione [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it) per scoprire come utilizzare lo strumento Content Transfer (Trasferimento contenuti).

1. Per acquisire contenuti dal set di migrazione in un ambiente su AEM as a Cloud Service, dovrai avviare un’acquisizione. Passa a **Processi di acquisizione** e fai clic su **Nuova acquisizione**. Revisione [Inserimento di contenuto in Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) per scoprire come completare la fase di acquisizione del trasferimento dei contenuti.

   ![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### Stima del tempo di trasferimento dei contenuti {#calculating}

È stato fornito un calcolatore dello strumento Content Transfer (Trasferimento contenuti) per stimare quanto tempo potrebbe essere necessario per completare l’attività di trasferimento dei contenuti. Puoi utilizzare il cursore delle dimensioni dell’archivio dei contenuti per selezionare le dimensioni da applicare al progetto. I tempi di trasferimento variano per le fasi di estrazione e acquisizione.

![immagine](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>Questi tempi sono solo stime. In queste stime non sono stati presi in considerazione fattori quali la velocità di rete e il tempo necessario per aumentare le istanze.

Per stimare le dimensioni dell&#39;archivio AEM, è possibile eseguire il rapporto Utilizzo disco in `http://HOST:PORT/etc/reports/diskusage.html`.

Puoi anche stimare la dimensione di percorsi di archivio specifici utilizzando la `path` ad esempio, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## Prossimi passaggi {#whats-next}

Dopo aver appreso come accedere a Cloud Acceleration Manager e come utilizzare la fase di implementazione, ora puoi passare alla revisione del passaggio successivo in [Vai alla fase live](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
