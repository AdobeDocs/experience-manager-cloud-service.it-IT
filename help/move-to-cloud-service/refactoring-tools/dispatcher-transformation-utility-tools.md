---
title: Strumento AEM Dispatcher Converter
description: Strumento AEM Dispatcher Converter
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 94%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter converte le configurazioni di AMS Dispatcher esistenti in configurazioni di AEM as a Cloud Service Dispatcher.

## Introduzione a Dispatcher {#introduction-dispatcher}

Dispatcher è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager. L’utilizzo di AEM Dispatcher consente inoltre di proteggere il server AEM da eventuali attacchi. Di conseguenza, per aumentare la sicurezza della tua istanza di AEM, puoi utilizzare Dispatcher insieme a un server web di classe Enterprise.

>[!NOTE]
>Dispatcher viene utilizzato in genere per memorizzare nella cache le risposte di un’**istanza di pubblicazione di AEM** e per aumentare la reattività e la sicurezza del sito web pubblicato per gli utenti esterni.

Consulta la [panoramica di Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html) per scoprire come il dispatcher esegue la memorizzazione nella cache e il bilanciamento del carico, e come restituisce i documenti.

### Configurazione e test di Apache e Dispatcher {#dispatcher-configurations-cloud}

Devi imparare a strutturare le configurazioni di Apache e Dispatcher di AEM as a Cloud Service, nonché a convalidarlo ed eseguirlo localmente prima di implementarlo negli ambienti Cloud.

Per ulteriori informazioni, consulta [Dispatcher nel Cloud](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter è una utility per la conversione delle configurazioni esistenti di AMS Dispatcher in configurazioni di AEM as a Cloud Service Dispatcher. Questa utility è per le istanze AMS.

Il convertitore implementato è **AEMDispatcherConfigConverter**, il quale segue le linee guida di trasformazione.

Consulta l’articolo su come [convertire una configurazione di Dispatcher da AMS ad Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration).

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

La sezione seguente descrive le risorse e le informazioni necessarie per utilizzare lo strumento AEM Dispatcher Converter.

Consulta **[Git Resource: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**per informazioni su utilizzo, limitazioni e risoluzione dei problemi di questo strumento.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando Python 3.7.3. Si consiglia di installare Python 3.5 o versione successiva.

## Limitazioni  {#limitations}

AEM Dispatcher Converter funziona partendo dal presupposto che la struttura della cartella di configurazione del dispatcher fornita sia simile a quella descritta nella configurazione del dispatcher di Cloud Manager.


