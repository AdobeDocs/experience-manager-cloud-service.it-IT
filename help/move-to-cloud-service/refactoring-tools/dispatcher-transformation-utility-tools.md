---
title: Strumento AEM Dispatcher Converter
description: Strumento AEM Dispatcher Converter
translation-type: tm+mt
source-git-commit: 50d26dbec8281afec07ca56595b4b2a7b915eca9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 53%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter converte le configurazioni AEM Dispatcher esistenti in AEM come configurazioni del Dispatcher Cloud Service.

## Introduzione a Dispatcher {#introduction-dispatcher}

Dispatcher è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager. L’utilizzo di AEM Dispatcher consente inoltre di proteggere il server AEM da eventuali attacchi. Di conseguenza, per aumentare la sicurezza della tua istanza di AEM, puoi utilizzare Dispatcher insieme a un server web di classe Enterprise.

>[!NOTE]
>Dispatcher viene utilizzato in genere per memorizzare nella cache le risposte di un’**istanza di pubblicazione di AEM** e per aumentare la reattività e la sicurezza del sito web pubblicato per gli utenti esterni.

Consulta la [panoramica di Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html) per scoprire come il dispatcher esegue la memorizzazione nella cache e il bilanciamento del carico, e come restituisce i documenti.

### Configurazione e test di Apache e Dispatcher {#dispatcher-configurations-cloud}

Devi imparare a strutturare le configurazioni di Apache e Dispatcher di AEM as a Cloud Service, nonché a convalidarlo ed eseguirlo localmente prima di implementarlo negli ambienti Cloud.

Per ulteriori informazioni, consulta [Dispatcher nel Cloud](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter consente di rielaborare le configurazioni del dispatcher dei servizi gestiti Adobe o locali esistenti per AEM come una configurazione del dispatcher compatibile con Cloud Service.

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

* Tramite  Adobe I/O CLI: Si consiglia di utilizzare AEM Dispatcher Converter tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM come Cloud Service plug-in di refactoring del codice per l&#39;interfaccia CLI  Adobe I/O).

   Fare riferimento a Risorse **[Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per imparare come installare e usare il plug-in.

* Come utilità indipendente : Lo strumento AEM Dispatcher Converter può essere eseguito anche come utilità standalone.

   Refer to **[Git Resource: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** to learn about the usage and troubleshooting for this tool.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando NodeJS. È consigliabile installare NodeJS 10.0+.

