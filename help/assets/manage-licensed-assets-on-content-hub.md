---
title: Gestire Assets con licenza su Content Hub
description: Scopri come aggiungere un campo di licenza al modulo dei metadati delle risorse, applicare la proprietà dei metadati della licenza alle cartelle di risorse e approvare le risorse con le licenze per l’utilizzo.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Gestire Assets con licenza su Content Hub {#manage-licensed-assets-on-content-hub}

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza Adobe Acrobat AI Assistant per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

In qualità di amministratore, modifica il modulo metadati per includere il campo licenza risorsa in modo che venga visualizzato in Proprietà risorsa nell’ambiente di authoring AEM. Puoi quindi approvare la risorsa e la relativa licenza per renderla disponibile e concessa in licenza su Content Hub.

Esegui i passaggi seguenti:

1. Modifica il modulo metadati per includere un nuovo campo di testo con i dettagli della licenza. Mappa il campo di testo sulla proprietà `dc:license`. Per ulteriori informazioni su come aggiungere campi a un modulo di metadati e definire le proprietà, vedere [Configurare Forms](/help/assets/metadata-assets-view.md#metadata-forms) metadati.
   ![estrazione zip](/help/assets/assets/metadata-form-edit.png)
1. Applica il modulo metadati alla cartella risorse per applicare le impostazioni incorporate nel passaggio 1. Per informazioni su come assegnare un modulo metadati alla cartella risorse, vedere [Assegnare il modulo metadati a una cartella](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Approva il PDF con licenza](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Seleziona la risorsa e fai clic su **Dettagli** per visualizzarne le proprietà. Nel campo di licenza aggiunto al passaggio 1, definisci il percorso assoluto della licenza per la risorsa approvata al passaggio 3 o già approvata in precedenza. Il percorso assoluto di Content Hub segue il seguente pattern standard: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Ad esempio, /content/dam/teamA/projects/documents/file1.pdf
   ![percorso assoluto](/help/assets/assets/absolute-path.png)
1. Approva la risorsa per renderla disponibile in Content Hub e fai clic su **Salva**. Per informazioni su come approvare una risorsa, consulta [Impostare lo stato della risorsa](/help/assets/manage-organize-assets-view.md#set-asset-status).
