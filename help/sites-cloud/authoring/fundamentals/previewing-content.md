---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima i contenuti prima di iniziare a utilizzare il servizio.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: e70e6ee055c2542752e66e53aa70a9378b1bc5c0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Anteprima del contenuto {#previewing-content}

AEM offre un servizio di anteprima Sites che consente agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione ed sia disponibile pubblicamente.

Consente di visualizzare in anteprima le esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

Per ulteriori dettagli sugli ambienti di anteprima, consulta il documento [Gestire gli ambienti.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Pubblicazione del contenuto nell’anteprima {#publishing-content-to-preview}

Puoi pubblicare i contenuti nel servizio di anteprima utilizzando la funzione **Pubblicazione gestita** Interfaccia utente.

1. Nella console Siti , seleziona le pagine da inviare all’anteprima e fai clic sul pulsante **Gestisci pubblicazione** pulsante
1. Nella procedura guidata seguente, seleziona **Anteprima** come destinazione

   ![pubblicazione gestita](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Fai clic su **Successivo** e quindi **Pubblica** per confermare.

1. Viene visualizzata una finestra di dialogo con gli URL per accedere al contenuto nell’ambiente di anteprima.


In alternativa, per visualizzare il contenuto dell’anteprima, puoi utilizzare gli URL visualizzati nella procedura guidata. `preview-` all’URL di pubblicazione dell’istanza di produzione.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Vedere il documento [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) per ulteriori informazioni su come recuperare gli URL per i tuoi ambienti.

Il contenuto può anche essere pubblicato in anteprima utilizzando un [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) con `agentId` impostato su `preview` o utilizzando [API di replica](/help/operations/replication.md#replication-api) con `AgentFilter` configurato per l&#39;anteprima.

## Configurazione delle impostazioni OSGi per il livello di anteprima {#configuring-osgi-settings-for-the-preview-tier}

I valori delle proprietà OSGi del livello di anteprima vengono ereditati dal livello di pubblicazione. Tuttavia, i valori del livello di anteprima possono essere distinti dal livello di pubblicazione impostando il `service` al valore `preview`. L&#39;esempio seguente di una proprietà OSGi determina l&#39;URL di un endpoint di integrazione.

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

Per ulteriori informazioni, consulta [questa sezione](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) della documentazione di configurazione OSGi.

## Eseguire il debug dell’anteprima tramite la Console per sviluppatori {#debugging-preview-using-the-developer-console}

Segui questi passaggi per eseguire il debug del livello di anteprima utilizzando la Console per sviluppatori:

* In [Console per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleziona **— Anteprima intera —** o un ambiente di produzione che includa **prev** a nome
* Genera le informazioni rilevanti per l&#39;istanza di anteprima Vedi [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti.
