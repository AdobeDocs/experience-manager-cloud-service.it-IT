---
title: Informazioni su profili immagine e profili video di Dynamic Media
description: Un profilo immagine o un profilo video è una ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse di immagini Dynamic Media per ritagliarle correttamente.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 8b878a26653874c94a671a404d9b35740e43a514
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---

# Informazioni su profili immagine e profili video di Dynamic Media{#about-dm-image-video-profiles}

Un profilo immagine o un profilo video è una ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse di immagini Dynamic Media per ritagliarle correttamente.

In Dynamic Media puoi creare due tipi di profili, descritti in dettaglio nei seguenti collegamenti:

* [Profili immagine Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Profili video Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Vedi anche [Profili metadati](/help/assets/metadata-profiles.md).

È necessario disporre dei diritti di amministratore per creare, modificare ed eliminare i profili immagine di Dynamic Media o i profili video di Dynamic Media.

Dopo aver creato il profilo immagine o il profilo video, lo assegni a una o più cartelle da utilizzare per le nuove risorse Dynamic Media caricate.

Vedi anche [Tecniche consigliate per l’organizzazione delle risorse digitali per l’utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).


>[!NOTE]
>
>Le risorse spostate da una cartella all’altra non vengono rielaborate. Ad esempio, supponiamo che alla cartella 1 sia assegnato il profilo A e alla cartella 2 il cui profilo B è assegnato. Se si spostano le risorse dalla cartella 1 alla cartella 2, le risorse spostate conservano l&#39;elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche quando si spostano le risorse tra due cartelle a cui è stato assegnato lo stesso profilo.

## Rielaborazione delle risorse Dynamic Media in una cartella {#reprocessing-assets}

Puoi rielaborare le risorse in una cartella che dispone già di un profilo immagine Dynamic Media o di un profilo video Dynamic Media che hai successivamente modificato.

Ad esempio, supponi di aver creato un profilo immagine Dynamic Media e di averlo assegnato a una cartella. Per tutte le risorse immagine caricate nella cartella, il profilo immagine viene automaticamente applicato alle risorse. Tuttavia, in seguito decidi di aggiungere una nuova proporzione di ritaglio avanzato al profilo immagine. Ora, invece di dover selezionare e ricaricare le risorse nella cartella completamente, è sufficiente eseguire il *Scene7: Rielaborazione delle risorse* workflow.

Puoi eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale l’elaborazione non è riuscita la prima volta. Anche se non hai modificato un profilo immagine o video, o hai già applicato un profilo immagine o un profilo video, puoi comunque eseguire il flusso di lavoro di rielaborazione su una cartella di risorse in qualsiasi momento.

Facoltativamente, puoi regolare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse fino a 1000 risorse. Quando esegui la _Scene7: Rielaborazione delle risorse_ le risorse vengono raggruppate in batch e quindi inviate al server Dynamic Media per l’elaborazione. Dopo l’elaborazione, i metadati di ogni risorsa nell’intero set di batch vengono aggiornati su [!DNL Adobe Experience Manager]. Se la dimensione del batch è grande, è possibile che si verifichi un ritardo nell&#39;elaborazione. Oppure, se la dimensione del batch è troppo piccola, può causare troppi viaggi nel server Dynamic Media.

Vedi [Regola le dimensioni batch del flusso di lavoro di rielaborazione](#adjusting-load).

>[!NOTE]
>
>Se esegui una migrazione in massa di risorse da Dynamic Media Classic a [!DNL Experience Manager], abilita l’agente di replica di migrazione sul server Dynamic Media. Al termine della migrazione, assicurati di disabilitare l’agente.
>
>L’agente di pubblicazione della migrazione deve essere disabilitato sul server Dynamic Media in modo che il flusso di lavoro Rielabora funzioni come previsto.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Per rielaborare le risorse Dynamic Media in una cartella:**

1. In [!DNL Experience Manager]Dalla pagina Risorse , passa a una cartella di risorse a cui è assegnato un profilo immagine o un profilo video e a cui desideri applicare il **Scene7: Rielabora risorsa** workflow.

   Le cartelle a cui è assegnato un profilo immagine o un profilo video presentano il nome del profilo e vengono visualizzate direttamente sotto il nome della cartella nella Vista a schede.

1. Seleziona una cartella.

   * Il flusso di lavoro considera in modo ricorsivo tutti i file presenti nella cartella selezionata.
   * Se sono presenti una o più sottocartelle con risorse nella cartella principale selezionata, il flusso di lavoro rielabora ogni risorsa nella gerarchia delle cartelle.
   * Come best practice, evita di eseguire questo flusso di lavoro in una gerarchia di cartelle con più di 1000 risorse.

1. Seleziona dall’elenco a discesa nell’angolo in alto a sinistra della pagina. **[!UICONTROL Timeline]**.
1. Nell’angolo in basso a sinistra della pagina, a destra della [!UICONTROL Commento] , seleziona l’icona del carrello ( **^** ).

   ![Schermata delle risorse nell’Experience Manager che mostra una cartella selezionata di risorse, l’elenco a discesa Timeline evidenziato, il pulsante Avvia flusso di lavoro evidenziato e anche l’icona del carrello a destra del campo Commento evidenziato.](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Seleziona **[!UICONTROL Avvia flusso di lavoro]**.
1. Da **[!UICONTROL Avvia flusso di lavoro]** elenco a discesa, scegli **[!UICONTROL Scene7: Rielaborazione delle risorse]**.
1. (Facoltativo) In **Immetti il titolo del flusso di lavoro** campo di testo, immetti un nome per il flusso di lavoro. Se necessario, puoi utilizzare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Schermata dell’interfaccia utente della Timeline con &quot;Scene7: Rielabora risorse&quot; selezionate dall’elenco a discesa Avvia flusso di lavoro ed evidenziato il pulsante Start .](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Seleziona **[!UICONTROL Inizio]**, quindi seleziona **[!UICONTROL Conferma]**.

   Per monitorare il flusso di lavoro o controllarne l’avanzamento, dai [!DNL Experience Manager] pagina della console principale, seleziona **[!UICONTROL Strumenti > Flusso di lavoro]**. Nella pagina Istanze flusso di lavoro , seleziona un flusso di lavoro. Nella barra dei menu, seleziona **[!UICONTROL Cronologia aperta]**. Puoi anche interrompere, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regola le dimensioni batch del flusso di lavoro di rielaborazione (facoltativo) {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è 50 risorse per processo. Questa dimensione batch ottimale è governata dalla dimensione media delle risorse e dai tipi MIME delle risorse su cui viene eseguita la rielaborazione. Un valore più alto indica che in un singolo processo di rielaborazione sono presenti molti file. Così, il banner di elaborazione rimane su [!DNL Experience Manager] risorse per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola-1 MB o inferiore, l’Adobe consiglia di aumentare il valore a diversi 100, ma mai più di 1000. Se la dimensione media del file è di centinaia di MB, Adobe consiglia di ridurre la dimensione del batch fino a 10.

**Per regolare facoltativamente la dimensione batch del flusso di lavoro di rielaborazione:**

1. In [!DNL Experience Manager], seleziona **[!UICONTROL Adobe Experience Manager]** per accedere alla console di navigazione globale, seleziona **[!UICONTROL Strumenti]** Icona (martello) > **[!UICONTROL Flusso di lavoro > Modelli]**.
1. Nella pagina Modelli di flusso di lavoro, seleziona Vista a schede o Vista a elenco **[!UICONTROL Scene7: Rielaborazione delle risorse]**.

   ![Schermata della pagina dei modelli di flusso di lavoro con &quot;Scene7: Rielabora il flusso di lavoro delle risorse selezionato nella vista Scheda dell’Experience Manager.](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. Nella barra degli strumenti, seleziona **[!UICONTROL Modifica]**. Viene visualizzata una nuova scheda del browser Scene7: Rielabora la pagina del modello di flusso di lavoro Assets.
1. Su Scene7: Rielabora la pagina del flusso di lavoro delle risorse, seleziona nell’angolo in alto a destra **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, seleziona il componente Caricamento in batch di Scene7 per aprire la barra degli strumenti, quindi seleziona **[!UICONTROL Configura]** nella barra degli strumenti.

   ![Schermata del componente &quot;Caricamento in batch di Scene7&quot; su &quot;Scene7: Rielabora le risorse&quot; con il puntatore del mouse che passa sopra l’icona &quot;Configura&quot;.](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. Sulla **[!UICONTROL Caricamento in batch in Scene7 - Proprietà passaggio]** impostare quanto segue:
   * In **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]** campi di testo, immettere un nuovo titolo e una nuova descrizione per il processo, se necessario.
   * Seleziona **[!UICONTROL Avanzamento gestore]** se il tuo handler passerà al passaggio successivo.
   * In **[!UICONTROL Timeout]** immetti il timeout del processo esterno (secondi).
   * In **[!UICONTROL Punto]** immettere un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * In **[!UICONTROL Campo batch]**, immetti il numero massimo di risorse (50-1000) da elaborare in un processo di caricamento batch di elaborazione batch del server Dynamic Media.
   * Seleziona **[!UICONTROL Avanzamento al timeout]** se desideri avanzare quando viene raggiunto il timeout. Deseleziona se desideri passare alla casella in entrata quando viene raggiunto il timeout.

   ![Schermata della pagina &quot;Caricamento in batch in Scene7 - Proprietà passaggio&quot;.](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Caricamento in batch in Scene7 - Proprietà passaggio]** finestra di dialogo, seleziona **[!UICONTROL Fine]**.

1. Nell’angolo in alto a destra di Scene7: Rielabora la pagina del modello di flusso di lavoro Assets, seleziona **[!UICONTROL Sincronizzazione]**. Quando vedi **[!UICONTROL Sincronizzato]**, il modello di runtime del flusso di lavoro viene sincronizzato correttamente e pronto per rielaborare le risorse in una cartella.

   ![Schermata delle risorse nell’Experience Manager che mostra una cartella selezionata di risorse, l’elenco a discesa Timeline evidenziato, il pulsante Avvia flusso di lavoro evidenziato e anche l’icona del carrello a destra del campo Commento evidenziato.](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Chiudi la scheda del browser che mostra Scene7: Rielabora il modello di flusso di lavoro Assets.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
