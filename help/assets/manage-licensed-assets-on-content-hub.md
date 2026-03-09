---
title: Gestire risorse con licenza in Content Hub
description: Scopri come aggiungere un campo di licenza al modulo dei metadati delle risorse, applicare la proprietà dei metadati della licenza alle cartelle di risorse e approvare le risorse con le licenze per l’utilizzo.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# Gestire risorse con licenza in Content Hub {#manage-licensed-assets-on-content-hub}

In qualità di amministratore, modifica il modulo metadati in modo da includere il campo licenza risorsa in modo che venga visualizzato in Proprietà risorsa nell’ambiente di authoring di AEM. Puoi quindi approvare la risorsa e la relativa licenza per renderla disponibile e concessa in licenza su Content Hub.

Esegui i passaggi seguenti:

1. Modifica il modulo metadati per includere un nuovo campo di testo con i dettagli della licenza. Mappa il campo di testo sulla proprietà `dc:license`. Per ulteriori informazioni su come aggiungere campi a un modulo di metadati e definire le proprietà, vedere [Configurare Forms](/help/assets/metadata-assets-view.md#metadata-forms) metadati.
   ![estrazione zip](/help/assets/assets/metadata-form-edit.png)
1. Applica il modulo metadati alla cartella risorse per applicare le impostazioni incorporate nel passaggio 1. Per informazioni su come assegnare un modulo metadati alla cartella risorse, vedere [Assegnare il modulo metadati a una cartella](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Approva il PDF con licenza](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Seleziona la risorsa e fai clic su **Dettagli** per visualizzarne le proprietà. Nel campo di licenza aggiunto al passaggio 1, definisci il percorso assoluto della licenza per la risorsa approvata al passaggio 3 o già approvata in precedenza. Il percorso assoluto di Content Hub segue il seguente pattern standard: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Ad esempio, /content/dam/teamA/projects/documents/file1.pdf
   ![percorso assoluto](/help/assets/assets/absolute-path.png)
1. Approva la risorsa per renderla disponibile in Content Hub e fai clic su **Salva**. Per informazioni su come approvare una risorsa, consulta [Impostare lo stato della risorsa](/help/assets/manage-organize-assets-view.md#set-asset-status).

## Domande frequenti {#faqs-manage-licensed-assets-content-hub}

### Qual è lo scopo della gestione delle risorse concesse in licenza su AEM Assets Content Hub?

La gestione delle risorse concesse in licenza in Content Hub consente agli amministratori di garantire che siano disponibili per l’uso solo le risorse approvate con licenze valide, mantenendo la conformità e il corretto tracciamento dei metadati all’interno dell’ambiente di authoring di AEM.

### Come posso aggiungere un campo licenza alle proprietà delle risorse in Experience Manager as a Cloud Service?

È possibile aggiungere un campo licenza alle proprietà delle risorse modificando il modulo metadati per includere un nuovo campo di testo mappato alla proprietà `dc:license`. Questo campo viene quindi visualizzato nelle proprietà della risorsa nell’ambiente di authoring di AEM Assets.

### Come si applica un modulo di metadati a una cartella di risorse per includere il campo licenza nelle proprietà delle risorse?

Modifica il modulo metadati per includere il campo licenza. Applica questo modulo di metadati alla cartella di risorse desiderata per assicurarti che le nuove impostazioni siano incorporate per tutte le risorse all’interno di tale cartella.

### Come si specificano i dettagli della licenza di una risorsa?

Per specificare i dettagli della licenza, seleziona la risorsa, fai clic su **Dettagli** per visualizzarne le proprietà e immetti il percorso assoluto della licenza della risorsa approvata nel campo della licenza aggiunto al modulo dei metadati.

### Qual è il formato richiesto per il percorso assoluto di Content Hub per una licenza per risorse?

Il percorso assoluto di Content Hub deve seguire il pattern: /content/dam/(Gerarchia di cartelle della risorsa all’interno dell’archivio DAM)/(nome_risorsa).(file_extension). Ad esempio, `/content/dam/teamA/projects/documents/file1.pdf`.

### Perché è importante approvare sia la risorsa che la relativa licenza per renderla disponibile su AEM Assets Content Hub?

L’approvazione sia della risorsa che della relativa licenza garantisce che solo le risorse autorizzate e con licenza appropriata siano rese disponibili su AEM Assets Content Hub, garantendo al contempo la conformità e i diritti di utilizzo corretti.

### Come posso rendere disponibile una risorsa in AEM Assets Content Hub dopo aver approvato la relativa licenza?

Dopo aver definito il percorso di licenza nelle proprietà della risorsa, approva la risorsa e fai clic su Salva. Questa azione rende la risorsa concessa in licenza disponibile in AEM Assets Content Hub.

### Chi è responsabile della gestione delle risorse concesse in licenza in Content Hub?

Gli amministratori sono responsabili della modifica dei moduli di metadati, dell’assegnazione di tali moduli alle cartelle di risorse e dell’approvazione delle risorse e delle relative licenze in Content Hub.
