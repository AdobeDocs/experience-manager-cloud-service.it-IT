---
title: Integrazione con Adobe Target
description: Integrazione con Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 0af1f7dcc330a2ee5300088f274150a3ea79efe8
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 94%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Experience Cloud, [Adobe Target](https://business.adobe.com/it/products/target/adobe-target.html) consente di aumentare la rilevanza dei contenuti mediante il targeting e la valutazione su tutti i canali. Adobe Target viene utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare all’istante segmenti di pubblico (in base al comportamento) e automatizzare il targeting di contenuti ed esperienze online. AEM as a Cloud Service ha adottato il flusso di lavoro di targeting utilizzato in Adobe Target Standard. Se utilizzi Target, acquisisci familiarità con l’ambiente di modifica del targeting in AEM as a Cloud Service.

Integra i tuoi siti di AEM Sites con Adobe Target per personalizzare i contenuti delle tue pagine:

* Implementa il targeting dei contenuti.
* Utilizza il pubblico di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tieni traccia delle percentuali di conversione.

>[!NOTE]
>
>I clienti che non dispongono di un account Target esistente possono richiedere l’accesso a Target Foundation Pack per Experience Cloud. Foundation Pack fornisce un uso limitato del volume di Target.

Per eseguire l’integrazione con Target, esegui le seguenti attività:

* [Esegui attività preliminari](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=it): registrati ad Adobe Target e configura alcuni aspetti dell’istanza di authoring AEM. Il tuo account Adobe Target deve disporre dei permessi di livello **approvatore** come requisito minimo. Inoltre, devi proteggere le impostazioni dell’attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

* Experience Platform Launch è lo strumento per la strumentazione di un sito AEM con funzionalità di Target (librerie JS). Pertanto, l’integrazione di AEM as a Cloud Service con Launch e Adobe Target procede di pari passo (consulta i collegamenti di seguito).

   * [Integrare Experience Platform Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=it)
   * [Integrare AEM con Adobe Launch mediante Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=it)
   * [Informazioni sull’integrazione AEM con Experience Platform Launch, Analytics e Target](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html?lang=it)

>[!NOTE]
>
>La configurazione IMS (account tecnici) per Experience Platform Launch in AEM as a Cloud Service è preconfigurata. Gli utenti non devono creare questa configurazione.

1. [Configurare le attività](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=it): associa le attività alla configurazione cloud di Target.

>[!CAUTION]
>
>In AEM as a Cloud Service, l’agente di replica che sincronizza offerte e attività da AEM ad Adobe Target è disattivato per impostazione predefinita. Se è necessario riabilitare l’agente di replica, contatta il Team [di supporto Adobe](https://experienceleague.adobe.com/?support-solution=General&lang=it#support).

>[!NOTE]
>
>Se utilizzi Target con una configurazione proxy personalizzata, è necessario impostare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano API 3.x e altre API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Proteggere il nodo delle impostazioni delle attività **cq:ActivitySettings** nell&#39;istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Consulta [Prerequisiti per l&#39;integrazione con Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html?lang=it#securing-the-activity-settings-node) per informazioni dettagliate.

Una volta completata l’integrazione, puoi [contenuto mirato dell&#39;autore](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html?lang=it) che invia i dati dei visitatori ad Adobe Target. I Componenti pagina richiedono un codice specifico per abilitare il targeting dei contenuti. (Vedi [Sviluppo per contenuti mirati](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html?lang=it).

>[!NOTE]
>
>Quando esegui il targeting di un componente in AEM author, il componente effettua una serie di chiamate lato server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti Adobe Target (se configurati). Da AEM Publish ad Adobe Target non vengono effettuate chiamate lato server.

## Origini dell&#39;informazione di base {#background-information-sources}

L’integrazione di AEM as a Cloud Service con Adobe Target richiede la conoscenza di Adobe Target, AEM Activities management e AEM Audiences management. Devi avere familiarità con le seguenti informazioni:

* Adobe Target (consulta [Documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=it)).
* Console Attività di AEM (consulta [Gestione delle attività](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html?lang=it)).
* Tipi di pubblico di AEM (consulta [Gestione dei tipi di pubblico](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html?lang=it)).

>[!NOTE]
>
>Quando si lavora con Adobe Target, il numero massimo di artefatti consentiti in una campagna è il seguente:
>
>* 50 posizioni
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting
