---
title: Integrazione con Adobe Target
description: Integrazione con Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 65e1ede4cdc8035657e8b37fe206ebed4ab7bb24
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 4%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte del Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) consente di aumentare la pertinenza dei contenuti mediante il targeting e la misurazione su tutti i canali. Adobe Target viene utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare all’istante segmenti di pubblico (in base al comportamento) e automatizzare il targeting di contenuti ed esperienze online. AEM as a Cloud Service ha adottato il flusso di lavoro di targeting utilizzato in Adobe Target Standard. Se utilizzi Target, acquisisci familiarità con l’ambiente di modifica del targeting in AEM as a Cloud Service.

Integra i tuoi siti di AEM con Adobe Target per personalizzare i contenuti delle tue pagine:

* Implementa il targeting dei contenuti.
* Utilizza i tipi di pubblico di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tieni traccia dei tassi di conversione.

>[!NOTE]
>
>I clienti Adobe Experience Manager as a Cloud Service che non dispongono di un account Target esistente possono richiedere l’accesso a Target Foundation Pack, ad Experience Cloud.  Foundation Pack fornisce un uso limitato del volume di Target.


Per eseguire l’integrazione con Target, esegui le seguenti attività:

* [Esegui attività preliminari](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html): Registrati ad Adobe Target e configura alcuni aspetti dell’istanza di authoring AEM. Il tuo account Adobe Target deve avere **approvatore** autorizzazioni di livello minimo. Inoltre, devi proteggere le impostazioni dell’attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

* Launch by Adobe è lo strumento di fatto per la strumentazione di un sito AEM con funzionalità di Target (librerie JS). Pertanto, l’integrazione di AEM as a Cloud Service con Launch e Adobe Target procede di pari passo (consulta i collegamenti di seguito).

   * [Integrazione con Adobe Target tramite Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrare Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrare AEM con Adobe Launch tramite Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Informazioni sull’integrazione AEM con Launch by Adobe, Analytics e Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Launch by Adobe è preconfigurata in AEM as a Cloud Service. Gli utenti non devono creare questa configurazione.

1. [Configurare le attività](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html): Associa le attività alla configurazione cloud di Target.

>[!CAUTION]
>
>In AEM as a Cloud Service, l’agente di replica che sincronizza offerte e attività da AEM ad Adobe Target è disattivato per impostazione predefinita. Contatta il [Supporto Adobe](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) se devi riabilitare l’agente di replica.

>[!NOTE]
>
>Se utilizzi Target con una configurazione proxy personalizzata, devi configurare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x e altre le API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>È necessario proteggere il nodo delle impostazioni dell’attività **cq:ActivitySettings** nell’istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Vedi [Prerequisiti per l’integrazione con Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) per informazioni dettagliate.

Una volta completata l’integrazione, puoi [contenuto di destinazione dell&#39;autore](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) che invia i dati dei visitatori ad Adobe Target. I componenti pagina richiedono codice specifico per abilitare il targeting dei contenuti. (Vedi [Sviluppo per contenuti mirati](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>Quando esegui il targeting di un componente AEM autore, il componente effettua una serie di chiamate lato server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti Adobe Target (se configurati). Da AEM pubblicazione ad Adobe Target non vengono effettuate chiamate lato server.

## Origini dell&#39;informazione di base {#background-information-sources}

L’integrazione di AEM as a Cloud Service con Adobe Target richiede la conoscenza di Adobe Target, la gestione delle attività di AEM e la gestione AEM audience. Devi avere familiarità con le seguenti informazioni:

* Adobe Target (consulta [Documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html)).
* AEM console Attività (consulta [Gestione delle attività](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html).
* Pubblico AEM (Vedi [Gestione dei tipi di pubblico](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>Quando si lavora con Adobe Target, il seguente è il numero massimo di artefatti consentiti in una campagna:
>
>* 50 posizioni
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting

