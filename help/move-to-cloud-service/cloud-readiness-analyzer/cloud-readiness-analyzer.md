---
title: Valutazione della complessità del passaggio al servizio cloud
description: Valutazione della complessità del passaggio al servizio cloud
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Analizzatore di prontezza del cloud {#accesing-complexity}

## Panoramica {#overview}

Il servizio CRA (Cloud Readiness Analyzer) consente di controllare le istanze AEM esistenti per verificare se sono pronte a spostarsi nel servizio Cloud rilevando pattern che:

* Utilizzare una funzione AEM 6.x che al momento non è supportata nel servizio cloud

* Violazione di determinate regole che saranno interessate dal passaggio al servizio Cloud

>[!NOTE]
>L&#39;output del CRA velocizza la valutazione dello sforzo di sviluppo che sarà richiesto per passare al servizio Cloud.

## Configurazione di Cloud Readiness Analyzer {#setting-up-cra}

Il CRA viene rilasciato come pacchetto che funziona su tutte le versioni AEM di origine da XX e versioni successive, esplorando lo spostamento a Cloud Service.

È disponibile nel portale di distribuzione del software e può essere installato utilizzando Package Manager.

### Utilizzo di Cloud Ready Analyzer {#using-cra}

>[!NOTE]
> CRA può essere eseguito su qualsiasi ambiente, comprese le istanze di sviluppo locale.

>[IMPORTANTE]
>Tuttavia, al fine di aumentare il tasso di rilevamento ed evitare eventuali rallentamenti nei casi business critical, è consigliabile eseguirlo in ambienti di pre-produzione il più vicino possibile a quelli di produzione nelle aree delle applicazioni utente, dei contenuti e delle configurazioni

### Visualizzazione dell&#39;output nell&#39;analizzatore di prontezza di Cloud {#viewing-output-cra}


1. Andate alla console Web di AEM sfogliando la console di configurazione **di** Adobe Experience Manager tramite `https://serveraddress:serverport/system/console/configMgr`.

1. Selezionate Stato - Analizzatore di prontezza cloud come illustrato nell&#39;immagine seguente.

1. Puoi anche visualizzare l’output tramite una normale interfaccia JSON basata su testo reattivo.

>[!NOTE]
> Per ulteriori informazioni su questi metodi, consultate Rilevatore [](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) pattern. È necessario aggiungere questa sezione una volta che CRA è pronta per l&#39;uso.

## Passaggi successivi sulla disponibilità del cloud {#the-next-steps}

Per ottenere ulteriori informazioni sulla disponibilità del servizio Cloud, Adobe deve valutare l&#39;output del CRA.

Per restituire il file, effettuate le operazioni seguenti:

1. Andate alla console Web di AEM e scaricate il file xx come illustrato nell&#39;immagine seguente.

1. Apri un ticket DayCare per inviare il file ad Adobe tramite:
   1. Registrazione di un ticket di supporto in Daycare con titolo come output di **Cloud Readiness Analyzer**
   1. Collegamento di un file di output al ticket

