---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima i contenuti prima della pubblicazione.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b93bcb5d26a63babf0b81c92a4fd85d358bfbea7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 65%

---


# Anteprima del contenuto {#previewing-content}

AEM offre un servizio di anteprima Sites che consente agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Semplifica la visualizzazione in anteprima delle esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

>[!IMPORTANT]
>
>L’accesso all’ambiente di anteprima richiede la configurazione di un inserisco nell&#39;elenco Consentiti di IP. Per ulteriori dettagli, vedere [Accedere al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service#access-preview-service).
>
>Per ulteriori dettagli su tutti gli ambienti, vedi [Gestisci ambienti](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>Poiché il contenuto è *pubblicato* nell&#39;ambiente di anteprima, è accessibile tramite URL.

## Pubblicazione del contenuto in anteprima {#publishing-content-to-preview}

Puoi pubblicare i contenuti nel servizio di anteprima utilizzando la funzione **Pubblicazione gestita** dell’interfaccia utente.

1. Nella console Sites, seleziona le pagine da inviare all&#39;anteprima e fai clic sul pulsante **Gestisci pubblicazione**.
1. Nella procedura guidata seguente, selezionare **Anteprima** come destinazione.

   ![pubblicazione gestita](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Fai clic su **Avanti** e quindi su **Pubblica** per confermare.

1. Viene visualizzata una finestra di dialogo con gli URL per accedere al contenuto nell’ambiente di anteprima.

   >[!NOTE]
   >
   >Poiché il contenuto è *pubblicato* nell&#39;ambiente di anteprima, è accessibile tramite URL (quindi non è necessario accedere ad AEM).

Per visualizzare il contenuto dell’anteprima utilizzando gli URL nella procedura guidata, in alternativa, puoi anche anteporre `preview-` all’URL di pubblicazione dell’istanza di produzione.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Per ulteriori informazioni su come recuperare gli URL per i tuoi ambienti, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md).

Il contenuto può anche essere pubblicato in anteprima utilizzando un [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) con il parametro `agentId` impostato su `preview` oppure utilizzando [API di replica](/help/operations/replication.md#replication-api) con `AgentFilter` configurato per l’anteprima.

## Annullamento della pubblicazione di contenuti dall’ambiente di anteprima {#unpublishing-content-from-preview}

Per annullare la pubblicazione di contenuti dall’ambiente di **Anteprima** si segue sostanzialmente lo stesso processo richiesto per [annullare la pubblicazione delle pagine](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages) dall’ambiente di **Pubblicazione**.

L’unica differenza è che puoi impostare la **Destinazione** su **Anteprima**.
