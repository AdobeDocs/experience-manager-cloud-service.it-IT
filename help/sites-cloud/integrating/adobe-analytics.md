---
title: 'Integrazione con Adobe Analytics '
description: 'Integrazione con Adobe Analytics '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione  Adobe Analytics e AEM come Cloud Service consente di tenere traccia dell’attività della pagina Web:

* Una configurazione Adobe Analytics  consente AEM l&#39;autenticazione con  Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics .

I dati includono i dati di pagina e utente, ad esempio:

* dati raccolti AEM componenti
* clic collegamento
* informazioni sull’utilizzo video
* il numero di visite di pagina da  Adobe Analytics

Le pagine elencate di seguito possono facilitare la configurazione dell&#39;integrazione. Da notare che Launch by Adobe è lo strumento di fatto per la strumentazione di un sito AEM con  funzionalità Analytics (librerie JS). Pertanto, l&#39;integrazione AEM come Cloud Service con Launch e  Adobe Analytics va di pari passo.

* [Connessione a  Adobe Analytics e creazione di framework](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - Notate che  framework Analytics sono precedenti in AEM e la loro creazione non funziona AEM come Cloud Service perché richiede l&#39;interfaccia classica. È consigliabile utilizzare i Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione delle librerie JS alle pagine.
* [Integrare Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrare AEM con  lancio Adobe tramite  I/O Adobe](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Integrazione AEM con Launch by Adobe,  Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configurazione del tracciamento dei collegamenti per  Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mappatura dei dati dei componenti con  delle proprietà Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configurazione del tracciamento video per  Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificazioni  Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
> Adobe Experience Manager come clienti di Cloud Service che non dispongono di un account  Analytics esistente, può richiedere l&#39;accesso al  Analytics Foundation Pack per  Experience Cloud.  Questo Foundation Pack fornisce un utilizzo limitato del volume di  Analytics.

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch by Adobe è preconfigurata in AEM come Cloud Service. Gli utenti non devono creare questa configurazione.

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione della  integrazione](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) Adobe Analytics per informazioni sullo sviluppo di componenti che raccolgono dati utente e la personalizzazione del framework Adobe Analytics . I &quot; framework Analytics&quot; sono precedenti in AEM e la loro creazione non funziona in AEM come Cloud Service perché richiede l&#39;interfaccia classica. È consigliabile utilizzare i Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione delle librerie JS alle pagine.
* L&#39;articolo della knowledge base, [integrazione con Adobe Analytics - risoluzione dei problemi](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all&#39;integrazione  Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configura:
>
>* **Day Commons HTTP Client 3.1** per configurare l&#39;API 3.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configurazione** proxy dei componenti Apache HTTP per configurare l&#39;API 4.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>


