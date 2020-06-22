---
title: Fase di post-pubblicazione
description: Fase di post-pubblicazione
translation-type: tm+mt
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 82%

---


# Post-pubblicazione {#post-go-live}

Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

Sono disponibili i seguenti strumenti per la risoluzione dei problemi relativi agli ambienti di AEM as a Cloud Service:

* **Console per sviluppatori**
* **CRX/DE Lite**
* **Gestione dei registri**


## Console per sviluppatori {#developer-console}

Gli ambienti di debug per sviluppatori di AEM as a Cloud Service sono disponibili nella Console per sviluppatori per ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRX/DE Lite {#crxde-lite}

L&#39;utente può accedere a CRX/DE Lite nell&#39;ambiente di sviluppo, ma non nell&#39;area di visualizzazione o nella produzione.

>[IMPORTANTE]
>La scrittura in archivi immutabili come `/libs` e `/apps` in fase di runtime genera errori. Inoltre, in qualità di cliente, non puoi accedere agli strumenti per sviluppatori per gli ambienti di produzione e di staging.

Refer to [Developing with CRX/DE Lite](https://docs.adobe.com/help/it-IT/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) to learn how to develop your AEM application using CRX/DE Lite.

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere ai registri e gestirli attraverso l’interfaccia o l’API tramite Cloud Manager, consulta [Accesso e gestione dei registri](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html).

### Ulteriore assistenza {#additional-support}

Se hai domande sull’accesso a Cloud Service, contatta il tuo rappresentante Adobe o visita il Portale di assistenza Adobe AEM CQ.
