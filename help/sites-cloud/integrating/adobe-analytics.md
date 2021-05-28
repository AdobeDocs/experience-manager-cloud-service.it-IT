---
title: 'Integrazione con Adobe Analytics '
description: 'Integrazione con Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM come Cloud Service consente di monitorare l’attività della pagina web:

* Una configurazione Adobe Analytics consente AEM l’autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics.

I dati includono dati di pagina e utente, ad esempio:

* dati raccolti AEM componenti
* clic sui collegamenti
* informazioni sull&#39;utilizzo video
* il numero di visite di pagina da Adobe Analytics

Le pagine elencate di seguito possono essere utili per configurare l’integrazione. Da notare che Launch by Adobe è lo strumento di fatto per la strumentazione di un sito AEM con funzionalità di Analytics (librerie JS). Pertanto, l’integrazione di AEM come Cloud Service con Launch e Adobe Analytics va di pari passo.

* [Connessione ad Adobe Analytics e creazione di framework](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html)  - Tieni presente che i &quot;framework di Analytics&quot; sono legacy in AEM e la loro creazione non funziona in AEM come Cloud Service perché richiede l’interfaccia classica. È invece necessario utilizzare Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione di librerie JS nelle pagine.
* [Integrare Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrare AEM con Adobe Launch tramite Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Informazioni sull’integrazione AEM con Launch by Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configurazione del tracciamento video per Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificazioni Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>I clienti Adobe Experience Manager as a Cloud Service che non dispongono di un account Analytics esistente possono richiedere l’accesso ad Analytics Foundation Pack, ad Experience Cloud.  Questo Foundation Pack fornisce un utilizzo limitato del volume di Analytics.

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch by Adobe è preconfigurata in AEM come Cloud Service. Gli utenti non devono creare questa configurazione.

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione dell’](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) integrazione di Adobe Analytics per informazioni sullo sviluppo di componenti che raccolgono dati utente e sulla personalizzazione del framework Adobe Analytics. I &quot;framework di Analytics&quot; sono legacy in AEM e la loro creazione non funziona in AEM come Cloud Service perché richiede l’interfaccia classica. È invece necessario utilizzare Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione di librerie JS nelle pagine.
* L&#39;articolo della knowledge base, [Integrazione Adobe Analytics - risoluzione dei problemi](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all&#39;integrazione di Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configurazione:
>
>* **Day Commons HTTP Client 3.1** per configurare l&#39;API 3.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configurazione proxy dei componenti HTTP Apache** per configurare l’API 4.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>


