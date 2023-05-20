---
title: Esaminare le risorse in cartelle e raccolte
description: Imposta i flussi di lavoro di revisione per le risorse all’interno di una cartella o di una raccolta e condividili con i revisori o i partner creativi per ottenere un feedback.
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 24%

---

# Esaminare le risorse in cartelle e raccolte {#review-folder-assets-and-collections}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Con Adobe Experience Manager Assets puoi impostare flussi di lavoro di revisione ad hoc per le risorse presenti in una cartella o in una raccolta. Puoi condividerlo con revisori o partner creativi per chiedere il loro feedback. È possibile associare un flusso di lavoro di revisione a un progetto o creare un&#39;attività di revisione indipendente.

Dopo aver condiviso le risorse, i revisori possono approvarle o rifiutarle. Le notifiche vengono inviate in varie fasi del flusso di lavoro per notificare ai destinatari interessati il completamento di varie attività. Ad esempio, quando si condivide una cartella o una raccolta, il revisore riceve una notifica che indica che una cartella o una raccolta è stata condivisa per la revisione.

Al termine della revisione (approvazione o rifiuto delle risorse), il revisore riceve una notifica di completamento della revisione.

## Creazione di un&#39;attività di revisione per le cartelle {#creating-a-review-task-for-folders}

1. Dall’interfaccia utente di Assets, seleziona la cartella per la quale desideri creare un’attività di revisione.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Crea attività di revisione]** per aprire la pagina **[!UICONTROL Attività di revisione]**. Se l’icona non è visibile nella barra degli strumenti, tocca o fai clic su **[!UICONTROL More (Altro)]**, quindi seleziona l’icona.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Facoltativo) Da **[!UICONTROL Progetto]** selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, il **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Solo i progetti per i quali si dispone di autorizzazioni a livello di editor (o superiori) sono visibili in **[!UICONTROL Progetti]** elenco.

1. Immettere un nome per il task di revisione e selezionare un approvatore dal campo **[!UICONTROL Assegna a]** elenco.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nel **[!UICONTROL Assegna a]** elenco.

1. Immettere una descrizione, la priorità del task e la data di scadenza del task di revisione.

   ![dettagli_attività](assets/task_details.png)

1. Nella scheda Avanzate, immetti un’etichetta da utilizzare per creare l’URI.

   ![review_name](assets/review_name.png)

1. Tocca o fai clic su **[!UICONTROL Invia]**, quindi tocca o fai clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Experience Manager Assets] come Approvatore, passa all’interfaccia utente Assets. Per approvare le risorse, tocca o fai clic su **[!UICONTROL Notifiche]** e quindi selezionare il task di revisione dall&#39;elenco.

   ![notifica](assets/notification.png)

1. Nella pagina **[!UICONTROL Rivedi attività]**, esamina i dettagli dell’attività di revisione, quindi tocca o fai clic su **[!UICONTROL Review (Verifica)]**.
1. Nella pagina **[!UICONTROL Rivedi attività]**, seleziona le risorse, quindi tocca o fai clic sull’icona **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare, a seconda delle necessità.

   ![task_revisione](assets/review_task.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e tocca o fai clic su  **[!UICONTROL Completa]** per confermare.
1. Passa all’interfaccia utente Assets e apri la cartella. Le icone dello stato di approvazione per le risorse vengono visualizzate sia nella vista a schede che in quella a elenco.

   **Vista a schede**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Vista a elenco**

   ![review_status_listview](assets/review_status_listview.png)

## Creazione di un&#39;attività di revisione per le raccolte {#creating-a-review-task-for-collections}

1. Nella pagina Raccolte selezionare la raccolta per la quale si desidera creare un task di revisione.
1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Crea attività di revisione]** per aprire la pagina **[!UICONTROL Attività di revisione]**. Se l’icona non è visibile nella barra degli strumenti, tocca o fai clic su **[!UICONTROL More (Altro)]**, quindi seleziona l’icona.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Facoltativo) Dal menu **[!UICONTROL Progetto]** selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, il **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Solo i progetti per i quali si dispone di autorizzazioni a livello di editor (o superiori) sono visibili in **[!UICONTROL Progetti]** elenco.

1. Immettere un nome per il task di revisione e selezionare un approvatore dal campo **[!UICONTROL Assegna a]** elenco.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nel **[!UICONTROL Assegna a]** elenco.

1. Immettere una descrizione, la priorità del task e la data di scadenza del task di revisione.

   ![task_details-collection](assets/task_details-collection.png)

1. Tocca o fai clic su **[!UICONTROL Invia]**, quindi tocca o fai clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Experience Manager Assets] come Approvatore, passa alla console Risorse. Per approvare le risorse, tocca o fai clic su **[!UICONTROL Notifiche]** e quindi selezionare il task di revisione dall&#39;elenco.
1. Nella pagina **[!UICONTROL Rivedi attività]**, esamina i dettagli dell’attività di revisione, quindi tocca o fai clic su **[!UICONTROL Review (Verifica)]**.
1. Tutte le risorse della raccolta sono visibili nella pagina di revisione. Seleziona le risorse e tocca o fai clic su **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare le risorse, a seconda delle necessità.

   ![review_task_collection](assets/review_task_collection.png)

1. Tocca o fai clic sul pulsante **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e tocca o fai clic su **[!UICONTROL Completa]** per confermare.
1. Passa alla console Raccolte e apri la raccolta. Le icone dello stato di approvazione per le risorse vengono visualizzate sia nella vista a schede che in quella a elenco.

   **Vista a schede**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Vista a elenco**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati da Assets](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
