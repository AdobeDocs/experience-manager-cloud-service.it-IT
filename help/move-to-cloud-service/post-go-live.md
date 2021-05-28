---
title: Fase di post-pubblicazione
description: Fase di post-pubblicazione
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 63%

---

# Post-pubblicazione {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Risoluzione dei problemi AEM"
>abstract="Rivedi le best practice per lo sviluppo continuo e gestisci i registri insieme a strumenti come Developer Console e CRXDE Lite per aiutarti a risolvere i problemi relativi a AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Accesso e gestione dei registri"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM come strumenti di sviluppo del Cloud Service"


Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

Sono disponibili i seguenti strumenti per la risoluzione dei problemi relativi agli ambienti di AEM as a Cloud Service:

* **Console per sviluppatori**
* **CRX/DE Lite**
* **Gestione dei registri**


## Console per sviluppatori {#developer-console}

Gli ambienti di debug per sviluppatori di AEM as a Cloud Service sono disponibili nella Console per sviluppatori per ambienti di sviluppo, stage e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools).

## CRX/DE Lite {#crxde-lite}

Come utente, puoi accedere a CRX/DE Lite nell’ambiente di sviluppo, ma non in quello di stage o produzione.

>[!IMPORTANT]
>La scrittura in archivi immutabili come `/libs` e `/apps` in fase di runtime genera errori. Inoltre, in qualità di cliente, non puoi accedere agli strumenti per sviluppatori per gli ambienti di produzione e di staging.

Per informazioni su come sviluppare l’applicazione AEM utilizzando CRX/DE Lite, consulta [Sviluppo con CRX/DE Lite](/help/implementing/developing/tools/crxde.md).

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere ai registri e gestirli attraverso l’interfaccia o l’API tramite Cloud Manager, consulta [Accesso e gestione dei registri](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html).

### Ulteriore assistenza {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Aiuto e supporto"
>abstract="Rivolgiti al nostro team di supporto AEM per ottenere chiarimenti o per risolvere eventuali problemi."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Supporto per Experience Cloud"

Se hai domande sull&#39;accesso al Cloud Service, contatta il tuo rappresentante Adobe o [Supporto per l&#39;Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) per ulteriori dettagli.
