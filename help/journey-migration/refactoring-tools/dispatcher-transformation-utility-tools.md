---
title: Strumento AEM Dispatcher Converter
description: Scopri come convertire le configurazioni esistenti su AEM Dispatcher in configurazioni su AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 28%

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

Consulta la [panoramica di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per scoprire come Dispatcher esegue la memorizzazione nella cache, restituisce documenti ed esegue il bilanciamento del carico.

### Configurazione e test di Apache e Dispatcher {#dispatcher-configurations-cloud}

Scopri come strutturare le configurazioni di AEM as a Cloud Service Apache e Dispatcher e come convalidarle ed eseguirle localmente prima di distribuirle negli ambienti Cloud.

Per ulteriori informazioni, vedi [Dispatcher nel cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=it).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter fornisce la funzionalità di refactoring delle configurazioni esistenti di Managed Services Dispatcher on-premise o Adobe per la configurazione di Dispatcher compatibile con AEM as a Cloud Service.

## Utilizzo di AEM Dispatcher Converter {#using-dispatcher-converter}

* Tramite Adobe Developer CLI: Adobe consiglia di utilizzare il convertitore Dispatcher AEM tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in di refactoring del codice AEM as a Cloud Service per Adobe Developer CLI).

  Consulta **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per informazioni su come installare e utilizzare il plug-in.

* Come utilità autonoma: lo strumento AEM Dispatcher Converter può anche essere eseguito come utilità autonoma.

  Consulta **[Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** per informazioni sull&#39;utilizzo e sulla risoluzione dei problemi di questo strumento.

>[!IMPORTANT]
>AEM Dispatcher Converter è sviluppato utilizzando NodeJS. L’Adobe consiglia di installare NodeJS 10.0+.
