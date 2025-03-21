---
title: Gestire risorse con licenza in Content Hub
description: Scopri come aggiungere un campo di licenza al modulo dei metadati delle risorse, applicare la proprietà dei metadati della licenza alle cartelle di risorse e approvare le risorse con le licenze per l’utilizzo.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 19%

---

# Gestire risorse con licenza in Content Hub {#manage-licensed-assets-on-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

In qualità di amministratore, modifica il modulo metadati in modo da includere il campo licenza risorsa in modo che venga visualizzato in Proprietà risorsa nell’ambiente di authoring di AEM. Puoi quindi approvare la risorsa e la relativa licenza per renderla disponibile e concessa in licenza su Content Hub.

Esegui i passaggi seguenti:

1. Modifica il modulo metadati per includere un nuovo campo di testo con i dettagli della licenza. Mappa il campo di testo sulla proprietà `dc:license`. Per ulteriori informazioni su come aggiungere campi a un modulo di metadati e definire le proprietà, vedere [Configurare Forms](/help/assets/metadata-assets-view.md#metadata-forms) metadati.
   ![estrazione zip](/help/assets/assets/metadata-form-edit.png)
1. Applica il modulo metadati alla cartella risorse per applicare le impostazioni incorporate nel passaggio 1. Per informazioni su come assegnare un modulo metadati alla cartella risorse, vedere [Assegnare il modulo metadati a una cartella](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Approva il PDF con licenza](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Seleziona la risorsa e fai clic su **Dettagli** per visualizzarne le proprietà. Nel campo di licenza aggiunto al passaggio 1, definisci il percorso assoluto della licenza per la risorsa approvata al passaggio 3 o già approvata in precedenza. Il percorso assoluto di Content Hub segue il seguente pattern standard: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Ad esempio, /content/dam/teamA/projects/documents/file1.pdf
   ![percorso assoluto](/help/assets/assets/absolute-path.png)
1. Approva la risorsa per renderla disponibile in Content Hub e fai clic su **Salva**. Per informazioni su come approvare una risorsa, consulta [Impostare lo stato della risorsa](/help/assets/manage-organize-assets-view.md#set-asset-status).
