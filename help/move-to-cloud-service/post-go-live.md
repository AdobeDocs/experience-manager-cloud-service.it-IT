---
title: Fase di post-live
description: Fase di post-live
translation-type: tm+mt
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Post Go-live {#post-go-live}

Nella fase post-live, devi garantire la pulizia dei file temporanei, esaminare le procedure ottimali per lo sviluppo continuo e gestire i registri.

Sono disponibili i seguenti strumenti per la risoluzione dei problemi relativi ad AEM come ambienti Cloud Service:

* **Console per sviluppatori**
* **CRX/DE Lite**
* **Gestione dei registri**


## Console per sviluppatori {#developer-console}

Il debug di AEM come ambienti per sviluppatori Cloud Service è disponibile in Developer Console per gli ambienti di sviluppo, fase e produzione.

Per ulteriori informazioni sugli strumenti di sviluppo, consulta [Implementazione per AEM come Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) .

## CRX/DE Lite {#crxde-lite}

L&#39;utente può accedere a CRX/DE Lite nell&#39;ambiente di sviluppo, ma non nell&#39;area di visualizzazione o nella produzione.

>[IMPORTANTE]
>La scrittura in archivi immutabili, ad esempio `/libs` e `/apps` in fase di esecuzione, genererà errori. Inoltre, in qualità di cliente, non potrete accedere agli strumenti di sviluppo per gli ambienti di produzione e di staging.

Fate riferimento a [Developing with CRX/DE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) (Sviluppo con CRX/DE Lite) per informazioni su come sviluppare l’applicazione AEM utilizzando CRX/DE Lite.

## Gestione dei registri {#managing-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Per informazioni su come accedere e gestire i registri tramite l’interfaccia utente o l’API tramite Cloud Manager, consulta [Accesso e Gestione registri](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) .

### Supporto aggiuntivo {#additional-support}

In caso di domande sull&#39;accesso ad Cloud Service, contattate il vostro rappresentante Adobe o il portale di assistenza Adobe AEM CQ.
