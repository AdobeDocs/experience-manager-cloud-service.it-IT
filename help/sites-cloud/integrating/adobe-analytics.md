---
title: Integrazione con Adobe Analytics
description: 'Integrazione con Adobe Analytics '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a

---


# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM come servizio cloud consente di tenere traccia dell’attività della pagina Web:

* Una configurazione di Adobe Analytics consente ad AEM di effettuare l&#39;autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti di Adobe Analytics.

I dati includono i dati di pagina e utente, ad esempio:

* dati raccolti dai componenti AEM
* clic collegamento
* informazioni sull’utilizzo video
* il numero di visite di pagina da Adobe Analytics

Le pagine elencate di seguito possono facilitare la configurazione dell&#39;integrazione. È importante notare che Launch by Adobe è lo strumento di fatto per la strumentazione di un sito AEM con funzionalità di Analytics (librerie JS). Pertanto, l&#39;integrazione di AEM come servizio cloud con Launch e Adobe Analytics va di pari passo.

* [Connessione ad Adobe Analytics e Creazione di framework](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - I &quot;framework di Analytics&quot; sono legacy in AEM e la loro creazione non funziona in AEM come servizio cloud perché richiede l’interfaccia classica. Launch di Adobe deve essere utilizzato, sia per la mappatura delle variabili che per la distribuzione delle librerie JS alle pagine.
* [Integrate Launch di Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Integrare AEM con Adobe Launch tramite Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [Integrazione di AEM con Launch di Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Configurazione del tracciamento video per Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Classificazioni Adobe](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>I clienti di Adobe Experience Manager come servizio Cloud che non dispongono di un account Analytics, possono richiedere l&#39;accesso ad Analytics Foundation Pack per Experience Cloud.  Questo Foundation Pack fornisce un utilizzo limitato del volume di Analytics.

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch di Adobe è preconfigurata in AEM come servizio Cloud. Gli utenti non devono creare questa configurazione.

## Ulteriori informazioni {#further-information}

Vedi:

* [Estensione dell&#39;integrazione](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) di Adobe Analytics per informazioni sullo sviluppo di componenti che raccolgono dati utente e la personalizzazione del framework Adobe Analytics. I &quot;framework di Analytics&quot; sono legacy in AEM e la loro creazione non funziona in AEM come servizio cloud perché richiede l’interfaccia classica. Launch di Adobe deve essere utilizzato, sia per la mappatura delle variabili che per la distribuzione delle librerie JS alle pagine.
* L&#39;articolo della knowledge base, Integrazione di [Adobe Analytics - Risoluzione dei problemi](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all&#39;integrazione di Adobe Analytics.

>[!NOTE]
>
>Se utilizzate Adobe Analytics con una configurazione proxy personalizzata, dovete [configurare due bundle](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html) OSGi (ad esempio, con la console Web) necessari per le configurazioni proxy **Apache HTTP Client** . Entrambe sono necessarie in quanto alcune funzionalità di AEM utilizzano le API 3.x, mentre altre utilizzano le API 4.x. Configura:
>
>* **Day Commons HTTP Client 3.1** per configurare l&#39;API 3.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configurazione** proxy dei componenti Apache HTTP per configurare l&#39;API 4.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


