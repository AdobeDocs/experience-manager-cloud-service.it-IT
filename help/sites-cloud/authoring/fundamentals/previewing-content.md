---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima i contenuti prima della pubblicazione.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 5a804895013e19592f918341bbc7921261b26945
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 91%

---


# Anteprima del contenuto {#previewing-content}

AEM offre un servizio di anteprima Sites che consente agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Semplifica la visualizzazione in anteprima delle esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

Per ulteriori dettagli sugli ambienti di anteprima, consulta il documento [Gestire gli ambienti](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>La pubblicazione di un frammento di esperienza in Anteprima segue sostanzialmente la stessa procedura applicata a una pagina, ma viene eseguita dalla console o dall’editor Frammenti di esperienza.

## Pubblicazione del contenuto in anteprima {#publishing-content-to-preview}

Puoi pubblicare i contenuti nel servizio di anteprima utilizzando la funzione **Pubblicazione gestita** dell’interfaccia utente.

1. Nella console Sites, seleziona le pagine da inviare all’anteprima e fai clic sul pulsante **Gestisci pubblicazione**.
1. Nella procedura guidata seguente, seleziona **Anteprima** come destinazione

   ![pubblicazione gestita](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Fai clic su **Avanti** e quindi su **Pubblica** per confermare.

1. Viene visualizzata una finestra di dialogo con gli URL per accedere al contenuto nell’ambiente di anteprima.


Per visualizzare il contenuto dell’anteprima utilizzando gli URL nella procedura guidata, in alternativa, puoi anche anteporre `preview-` all’URL di pubblicazione dell’istanza di produzione.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Per ulteriori informazioni su come recuperare gli URL per i tuoi ambienti, consulta il documento [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md).

Il contenuto può anche essere pubblicato in anteprima utilizzando un [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) con il parametro `agentId` impostato su `preview` oppure utilizzando [API di replica](/help/operations/replication.md#replication-api) con `AgentFilter` configurato per l’anteprima.

## Annullamento della pubblicazione di contenuti dall’anteprima {#unpublishing-content-from-preview}

Annullamento della pubblicazione di contenuti **Anteprima** l&#39;ambiente è sostanzialmente lo stesso processo [annullamento della pubblicazione delle pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) dal **Pubblica** ambiente.

L’unica differenza è che è possibile selezionare il **Destinazione** essere **Anteprima**.

## Configurazione delle impostazioni OSGi per il livello di anteprima {#configuring-osgi-settings-for-the-preview-tier}

I valori delle proprietà OSGi del livello di anteprima vengono ereditati dal livello di pubblicazione. Tuttavia, i valori del livello di anteprima possono essere distinti dal livello di pubblicazione impostando il parametro `service` al valore `preview`. L’esempio seguente di una proprietà OSGi determina l’URL di un endpoint di integrazione.

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

* Nella [Console per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleziona **-- Tutte le anteprime --** oppure un ambiente di produzione che includa **prev** nel nome
* Genera le informazioni rilevanti per l’istanza di anteprima 
Per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md).
