---
title: Strumento AEM Dispatcher Converter
description: Strumento AEM Dispatcher Converter
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 61%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter converte le configurazioni di AEM Dispatcher esistenti in configurazioni di AEM as a Cloud Service Dispatcher."

Adobe Experience Manager Dispatcher Converter converte le configurazioni di AEM Dispatcher esistenti in configurazioni di AEM as a Cloud Service Dispatcher.

## Introduzione a Dispatcher {#introduction-dispatcher}

Dispatcher è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager. L’utilizzo di AEM Dispatcher consente inoltre di proteggere il server AEM da eventuali attacchi. Di conseguenza, per aumentare la sicurezza della tua istanza di AEM, puoi utilizzare Dispatcher insieme a un server web di classe Enterprise.

>[!NOTE]
>Dispatcher viene utilizzato in genere per memorizzare nella cache le risposte di un’**istanza di pubblicazione di AEM** e per aumentare la reattività e la sicurezza del sito web pubblicato per gli utenti esterni.

Consulta la [panoramica di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per scoprire come il dispatcher esegue la memorizzazione nella cache e il bilanciamento del carico, e come restituisce i documenti.

### Configurazione e test di Apache e Dispatcher {#dispatcher-configurations-cloud}

Devi imparare a strutturare le configurazioni di Apache e Dispatcher di AEM as a Cloud Service, nonché a convalidarlo ed eseguirlo localmente prima di implementarlo negli ambienti Cloud.

Per ulteriori informazioni, consulta [Dispatcher nel Cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=it).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

Il convertitore del Dispatcher AEM fornisce la funzionalità di refactoring delle configurazioni del Dispatcher On-Premise o Adobe Managed Services esistenti per la configurazione del Dispatcher compatibile con l’AEM as a Cloud Service.

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

* Tramite CLI Adobe I/O : si consiglia di utilizzare il convertitore del Dispatcher AEM tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in per il refactoring del codice as a Cloud Service AEM per Adobe I/O CLI).

   Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utility indipendente : Lo strumento AEM Dispatcher Converter può anche essere eseguito come utility indipendente.

   Fai riferimento a **[Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** per informazioni sull&#39;utilizzo e sulla risoluzione dei problemi di questo strumento.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
