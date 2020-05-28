---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter converte le configurazioni del dispatcher AMS esistenti in AEM come configurazioni del dispatcher del servizio cloud.

## Introduzione al dispatcher {#introduction-dispatcher}

Dispatcher è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager. L’utilizzo di AEM Dispatcher consente inoltre di proteggere il server AEM da eventuali attacchi. Di conseguenza, per aumentare la sicurezza della tua istanza di AEM, puoi utilizzare Dispatcher insieme a un server web di classe Enterprise.

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

Fare riferimento a Panoramica [del](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) dispatcher per apprendere come il dispatcher esegue il caching, restituisce i documenti ed esegue il bilanciamento del carico.

### Configurazione e test Apache e Dispatcher {#dispatcher-configurations-cloud}

Devi imparare a strutturare AEM come una configurazione Apache di servizio cloud e Dispatcher, nonché a convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud.

Per ulteriori informazioni, consulta [Dispatcher in Cloud](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) .

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter è un&#39;utility per la conversione delle configurazioni di AMS Dispatcher in AEM come configurazioni di Cloud Service Dispatcher. Questa utility è per le istanze AMS.

Il convertitore implementato è **AEMDispatcherConfigConverter** che segue le linee guida di trasformazione.

Fare riferimento a [Conversione di un AMS in Adobe Experience Manager come configurazione](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) del dispatcher di servizi cloud per la conversione di un AMS in un Adobe Experience Manager come configurazione del dispatcher di servizi cloud.

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

La sezione seguente descrive le risorse e le informazioni necessarie per utilizzare lo strumento AEM Dispatcher Converter.

Fare riferimento a Risorse **[Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**per informazioni su utilizzo, limitazioni e risoluzione dei problemi di questo strumento.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando Python 3.7.3. Si consiglia di installare Python 3.5 o versione successiva.

## Limitazioni  {#limitations}

AEM Dispatcher Converter funziona partendo dal presupposto che la struttura della cartella di configurazione del dispatcher fornita sia simile a quella descritta nella configurazione del dispatcher di Cloud Manager.


