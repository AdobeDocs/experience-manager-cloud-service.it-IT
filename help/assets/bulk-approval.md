---
title: Esaminare le risorse in cartelle e raccolte
description: Imposta i flussi di lavoro di revisione per le risorse all’interno di una cartella o di una raccolta e condividili con i revisori o i partner creativi per ottenere un feedback.
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 10%

---

# Esaminare le risorse in cartelle e raccolte {#review-folder-assets-and-collections}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Con Adobe Experience Manager Assets puoi impostare flussi di lavoro di revisione ad hoc per le risorse presenti in una cartella o in una raccolta. Puoi condividerlo con revisori o partner creativi per chiedere il loro feedback. È possibile associare un flusso di lavoro di revisione a un progetto o creare un&#39;attività di revisione indipendente.

Dopo aver condiviso le risorse, i revisori possono approvarle o rifiutarle. Le notifiche vengono inviate in varie fasi del flusso di lavoro per notificare ai destinatari interessati il completamento di varie attività. Ad esempio, quando si condivide una cartella o una raccolta, il revisore riceve una notifica che indica che una cartella o una raccolta è stata condivisa per la revisione.

Al termine della revisione (approvazione o rifiuto delle risorse), il revisore riceve una notifica di completamento della revisione.

## Creazione di un&#39;attività di revisione per le cartelle {#creating-a-review-task-for-folders}

1. Dall’interfaccia utente di Assets, seleziona la cartella per la quale desideri creare un’attività di revisione.
1. Dalla barra degli strumenti, seleziona l&#39;icona **[!UICONTROL Crea attività di revisione]** per aprire la pagina **[!UICONTROL Attività di revisione]**. Se l&#39;icona non è visibile nella barra degli strumenti, selezionare **[!UICONTROL Altro]**, quindi selezionare l&#39;icona.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Facoltativo) Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, l&#39;opzione **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Nell&#39;elenco **[!UICONTROL Progetti]** sono visibili solo i progetti per i quali si dispone di autorizzazioni a livello di editor o superiori.

1. Immettere un nome per l&#39;attività di revisione e selezionare un approvatore dall&#39;elenco **[!UICONTROL Assegna a]**.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nell&#39;elenco **[!UICONTROL Assegna a]**.

1. Immettere una descrizione, la priorità del task e la data di scadenza del task di revisione.

   ![dettagli_attività](assets/task_details.png)

1. Nella scheda Avanzate, immetti un’etichetta da utilizzare per creare l’URI.

   ![nome_revisione](assets/review_name.png)

1. Seleziona **[!UICONTROL Invia]**, quindi seleziona **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Experience Manager Assets] come Approvatore e passa all&#39;interfaccia utente di Assets. Per approvare le risorse, seleziona l&#39;icona **[!UICONTROL Notifiche]**, quindi l&#39;attività di revisione dall&#39;elenco.

   ![notifica](assets/notification.png)

1. Nella pagina **[!UICONTROL Rivedi attività]**, esaminare i dettagli dell&#39;attività di revisione, quindi selezionare **[!UICONTROL Rivedi]**.
1. Nella pagina **[!UICONTROL Rivedi attività]**, seleziona le risorse e l&#39;icona **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare, a seconda delle necessità.

   ![attività_di_revisione](assets/review_task.png)

1. Seleziona l&#39;icona **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e seleziona **[!UICONTROL Completa]** per confermare.
1. Passa all’interfaccia utente di Assets e apri la cartella. Le icone dello stato di approvazione per le risorse vengono visualizzate sia nella vista a schede che in quella a elenco.

   **Vista a schede**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Vista a elenco**

   ![review_status_listview](assets/review_status_listview.png)

## Creazione di un&#39;attività di revisione per le raccolte {#creating-a-review-task-for-collections}

1. Nella pagina Raccolte selezionare la raccolta per la quale si desidera creare un task di revisione.
1. Dalla barra degli strumenti, seleziona l&#39;icona **[!UICONTROL Crea attività di revisione]** per aprire la pagina **[!UICONTROL Attività di revisione]**. Se l&#39;icona non è visibile nella barra degli strumenti, selezionare **[!UICONTROL Altro]**, quindi selezionare l&#39;icona.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Facoltativo) Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, l&#39;opzione **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Nell&#39;elenco **[!UICONTROL Progetti]** sono visibili solo i progetti per i quali si dispone di autorizzazioni a livello di editor o superiori.

1. Immettere un nome per l&#39;attività di revisione e selezionare un approvatore dall&#39;elenco **[!UICONTROL Assegna a]**.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nell&#39;elenco **[!UICONTROL Assegna a]**.

1. Immettere una descrizione, la priorità del task e la data di scadenza del task di revisione.

   ![raccolta_dettagli_attività](assets/task_details-collection.png)

1. Seleziona **[!UICONTROL Invia]**, quindi seleziona **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Experience Manager Assets] come Approvatore e passa alla console Assets. Per approvare le risorse, seleziona l&#39;icona **[!UICONTROL Notifiche]**, quindi l&#39;attività di revisione dall&#39;elenco.
1. Nella pagina **[!UICONTROL Rivedi attività]**, esaminare i dettagli dell&#39;attività di revisione, quindi selezionare **[!UICONTROL Rivedi]**.
1. Tutte le risorse della raccolta sono visibili nella pagina di revisione. Seleziona le risorse e fai clic sull&#39;icona **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare le risorse, a seconda delle necessità.

   ![raccolta_attività_revisione](assets/review_task_collection.png)

1. Seleziona l&#39;icona **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e seleziona **[!UICONTROL Completa]** per confermare.
1. Passa alla console Raccolte e apri la raccolta. Le icone dello stato di approvazione per le risorse vengono visualizzate sia nella vista a schede che in quella a elenco.

   **Vista a schede**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Vista a elenco**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
