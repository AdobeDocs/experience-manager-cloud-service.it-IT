---
title: 'Integrazione con Adobe Analytics '
description: 'Integrazione con Adobe Analytics '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: ht
source-wordcount: '545'
ht-degree: 100%

---


# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM as a Cloud Service consente di tracciare l’attività della pagina web:

* Una configurazione Adobe Analytics consente a AEM l’autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics.

I dati includono dati della pagina e dell’utente, ad esempio:

* dati raccolti dai componenti AEM
* clic sui collegamenti
* informazioni sull&#39;utilizzo dei video
* il numero di visite alla pagina da Adobe Analytics

Le pagine elencate di seguito possono essere utili per configurare l’integrazione. Da notare che Launch by Adobe è lo strumento di fatto per dotare un sito AEM delle funzionalità di Analytics (librerie JS). Pertanto, l’integrazione di AEM as a Cloud Service con Launch e Adobe Analytics è strettamente collegata.

* [Connessione ad Adobe Analytics e Creazione di framework](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html?lang=it): tieni presente che i “framework di Analytics“ in AEM sono legacy e che la loro creazione non funziona in AEM as a Cloud Service perché richiede l’interfaccia classica. È invece necessario utilizzare Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione di librerie JS nelle pagine.
* [Integrare Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html?lang=it)
* [Integrare AEM con Adobe Launch tramite Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=it)
* [Informazioni sull’integrazione AEM con Launch by Adobe, Analytics e Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=it)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html?lang=it)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html?lang=it)
* [Configurazione del tracciamento video per Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html?lang=it)
* [Classificazioni Adobe](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html?lang=it)

>[!CAUTION]
>
>I clienti di Adobe Experience Manager as a Cloud Service che non dispongono di un account Analytics esistente possono richiedere l’accesso ad Analytics Foundation Pack per Experience Cloud.  Tale Foundation Pack fornisce un utilizzo limitato del volume di Analytics.

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch by Adobe in AEM as a Cloud Service è preconfigurata. Gli utenti non devono creare questa configurazione.

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione dell’integrazione di Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html?lang=it) per informazioni sullo sviluppo di componenti che raccolgono dati utente e sulla personalizzazione del framework di Adobe Analytics. Tieni presente che i “framework di Analytics“ in AEM sono legacy e che la loro creazione non funziona in AEM as a Cloud Service perché richiede l’interfaccia classica. È invece necessario utilizzare Launch by Adobe, sia per la mappatura delle variabili che per la distribuzione di librerie JS nelle pagine.
* L’articolo della knowledge base, [Integrazione di Adobe Analytics - risoluzione dei problemi](https://helpx.adobe.com/it/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all’integrazione di Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=it) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configurare:
>
>* **Client HTTP Day Commons 3.1** per configurare l’API 3.x;
>  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configurazione proxy dei componenti HTTP Apache** per configurare l’API 4.x;
>  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

