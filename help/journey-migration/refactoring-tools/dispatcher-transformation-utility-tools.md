---
title: Strumento AEM Dispatcher Converter
description: Scopri come convertire le configurazioni esistenti nel Dispatcher AEM in configurazioni nel Dispatcher as a Cloud Service AEM.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 33%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter converte le configurazioni esistenti in AEM Dispatcher in configurazioni di AEM as a Cloud Service Dispatcher."

Adobe Experience Manager Dispatcher Converter converte le configurazioni esistenti in AEM Dispatcher in configurazioni di AEM as a Cloud Service Dispatcher.

## Introduzione a Dispatcher {#introduction-dispatcher}

Dispatcher è lo strumento di caching o bilanciamento del carico di Adobe Experience Manager, o entrambi. L’utilizzo di AEM Dispatcher consente inoltre di proteggere il server AEM da eventuali attacchi. Pertanto, puoi aumentare la sicurezza dell’istanza AEM utilizzando Dispatcher con un server web di classe enterprise.

>[!NOTE]
>Dispatcher viene utilizzato in genere per memorizzare nella cache le risposte di un’**istanza di pubblicazione di AEM** e per aumentare la reattività e la sicurezza del sito web pubblicato per gli utenti esterni.

Consulta [Panoramica di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per scoprire come Dispatcher esegue la memorizzazione nella cache, restituisce i documenti ed esegue il bilanciamento del carico.

### Configurazione e test di Apache e Dispatcher {#dispatcher-configurations-cloud}

Scopri come strutturare le configurazioni di Apache e Dispatcher as a Cloud Service per l’AEM e come convalidarle ed eseguirle localmente prima di distribuirle negli ambienti Cloud.

Consulta [Dispatcher nel cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=it) per ulteriori informazioni.

## AEM Dispatcher Converter {#aem-dispatcher-converter}

Il convertitore del Dispatcher AEM fornisce la funzionalità di refactoring delle configurazioni del Dispatcher On-Premise o Adobe Managed Services esistenti per la configurazione del Dispatcher compatibile con l’AEM as a Cloud Service.

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

* Tramite Adobe Developer CLI : Adobe consiglia di utilizzare il convertitore del Dispatcher AEM tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in di refactoring del codice as a Cloud Service AEM per Adobe Developer CLI).

  Consulta **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** in questo modo puoi imparare a installare e utilizzare il plug-in.

* Come utility indipendente : Lo strumento AEM Dispatcher Converter può essere eseguito anche come utility indipendente.

  Consulta **[Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** per informazioni sull’utilizzo e sulla risoluzione dei problemi di questo strumento.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando NodeJS. L’Adobe consiglia di installare NodeJS 10.0+.
