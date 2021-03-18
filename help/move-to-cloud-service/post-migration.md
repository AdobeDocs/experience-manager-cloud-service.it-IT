---
title: Fase di post-migrazione
description: Fase di post-migrazione
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---


# Post-migrazione {#post-migration}

Nella fase di post-migrazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

Sono disponibili i seguenti strumenti per la risoluzione dei problemi relativi agli ambienti di AEM as a Cloud Service:

* **Console per sviluppatori**
* **CRXDE Lite**
* **Gestione dei registri**


## Console per sviluppatori {#developer-console}

Gli ambienti di debug per sviluppatori di AEM as a Cloud Service sono disponibili nella Console per sviluppatori per ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Come utente, puoi accedere a **CRXDE Lite** nell’ambiente di sviluppo ma non in quello di stage o produzione.

>[!IMPORTANT]
>La scrittura in archivi immutabili come `/libs` e `/apps` in fase di runtime genera errori. Inoltre, in qualità di cliente, non puoi accedere agli strumenti per sviluppatori per gli ambienti di produzione e di staging.

Per informazioni su come sviluppare l’applicazione AEM utilizzando CRXDE Lite, consulta l’articolo sullo [sviluppo con CRXDE Lite](/help/implementing/developing/tools/crxde.md).

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere ai registri e gestirli attraverso l’interfaccia o l’API tramite Cloud Manager, consulta [Accesso e gestione dei registri](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html).

### Ulteriore assistenza {#additional-support}

Se hai domande sull’accesso a Cloud Service, contatta il tuo rappresentante Adobe o visita il Portale di assistenza Adobe AEM CQ.
