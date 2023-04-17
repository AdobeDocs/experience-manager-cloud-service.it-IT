---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima i contenuti prima della pubblicazione.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 100%

---


# Anteprima del contenuto {#previewing-content}

AEM offre un servizio di anteprima Sites che consente agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Semplifica la visualizzazione in anteprima delle esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

Per ulteriori dettagli sugli ambienti di anteprima, consulta il documento [Gestire gli ambienti](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

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

## Annullamento della pubblicazione di contenuti dall’ambiente di anteprima {#unpublishing-content-from-preview}

Per annullare la pubblicazione di contenuti dall’ambiente di **Anteprima** si segue sostanzialmente lo stesso processo richiesto per [annullare la pubblicazione delle pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) dall’ambiente di **Pubblicazione**.

L’unica differenza è che puoi impostare la **Destinazione** su **Anteprima**.

## Ulteriori informazioni {#further-information}

Consulta anche:

* [Configurazione delle impostazioni OSGi per il livello di anteprima](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [Eseguire il debug dell’anteprima tramite la Console per sviluppatori](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)