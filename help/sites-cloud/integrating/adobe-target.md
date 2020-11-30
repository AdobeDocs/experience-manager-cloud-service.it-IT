---
title: Integrazione con Adobe Target
description: 'Integrazione con Adobe Target '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 4%

---


# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte dell&#39;Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) consente di aumentare la pertinenza dei contenuti attraverso il targeting e la misurazione su tutti i canali.  Adobe Target è utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare segmenti di pubblico pronti (basati sul comportamento) e automatizzare il targeting dei contenuti e delle esperienze online. AEM come Cloud Service ha adottato il flusso di lavoro di targeting utilizzato in  Adobe Target Standard. Se utilizzate Target, avrete familiarità con l&#39;ambiente di modifica del targeting in AEM come Cloud Service.

Integra i tuoi siti AEM con  Adobe Target per personalizzare il contenuto delle tue pagine:

* Implementate il targeting dei contenuti.
* Utilizzate le audience di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tenere traccia dei tassi di conversione.

>[!NOTE]
>
>Adobe Experience Manager, come clienti di Cloud Service che non dispongono di un account Target esistente, può richiedere l&#39;accesso a Target Foundation Pack per  Experience Cloud.  Foundation Pack fornisce un utilizzo limitato del volume di Target.


Per effettuare l&#39;integrazione con Target, effettuate le seguenti operazioni:

* [Eseguire le operazioni](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html)preliminari: Effettuate la registrazione con  Adobe Target e configurate alcuni aspetti dell’istanza AEM di creazione. L&#39;account Adobe Target  deve disporre di autorizzazioni a livello di **approver** al minimo. Inoltre, è necessario proteggere le impostazioni dell&#39;attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

* Launch by Adobe è lo strumento di fatto per la strumentazione di un sito AEM con funzionalità Target (librerie JS). Pertanto, l&#39;integrazione AEM come Cloud Service con Launch e  Adobe Target va di pari passo (vedete i collegamenti di seguito).

   * [Integrazione con  Adobe Target tramite  Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrare Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrare AEM con  Adobe Launch tramite  Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Integrazione AEM con Launch by Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch by Adobe è preconfigurata in AEM come Cloud Service. Gli utenti non devono creare questa configurazione.

1. [Configura attività](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associate le attività alla configurazione cloud di Target.

>[!CAUTION]
>
>In AEM come Cloud Service, l&#39;agente di replica che sincronizza Offerte e Attività da AEM a  Adobe Target è disabilitato per impostazione predefinita. Se è necessario riabilitare l&#39;agente di replica, contattare il team di assistenza [del](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) Adobe.

>[!NOTE]
>
>Se utilizzate Target con una configurazione proxy personalizzata, è necessario configurare sia le configurazioni proxy HTTP Client in quanto alcune funzionalità di AEM utilizzano le API 3.x, sia quelle di 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

Al termine dell&#39;integrazione, potete [creare contenuto](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) mirato che invia i dati dei visitatori a  Adobe Target. I componenti della pagina richiedono codice specifico per abilitare il targeting dei contenuti. Consultate [Sviluppo per contenuti](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)mirati.

>[!NOTE]
>
>Quando eseguite il targeting di un componente in AEM autore, il componente effettua una serie di chiamate lato server  Adobe Target per registrare la campagna, impostare le offerte e recuperare  segmenti Adobe Target (se configurato). Nessuna chiamata lato server viene effettuata da AEM pubblicazione a  Adobe Target.

## Origini informazioni di base {#background-information-sources}

Per integrare AEM come Cloud Service con  Adobe Target è necessario conoscere  Adobe Target, AEM gestione delle attività e AEM gestione dell&#39;audience. È necessario avere familiarità con le seguenti informazioni:

*  Adobe Target (consultare la documentazione [di](https://docs.adobe.com/content/help/en/target/using/target-home.html)Adobe Target).
* AEM console Attività (Vedere [Gestione delle attività](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html).
* AEM Audiences (Vedete [Gestione dell&#39;audience](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Quando lavorate con  Adobe Target, quanto segue indica il numero massimo di artefatti consentiti in una campagna:
>
>* 50 località
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting

>


