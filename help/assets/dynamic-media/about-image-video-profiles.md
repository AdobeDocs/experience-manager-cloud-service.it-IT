---
title: Informazioni sui profili immagine e video Dynamic Media
description: Un profilo immagine o un profilo video indica le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse immagine Dynamic Media per ritagliarle correttamente.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Informazioni sui profili immagine e video Dynamic Media{#about-dm-image-video-profiles}

Un profilo immagine o un profilo video indica le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse immagine Dynamic Media per ritagliarle correttamente.

In Dynamic Media, puoi creare due tipi di profili, descritti in dettaglio ai seguenti collegamenti:

* [Profili immagine Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Profili video Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Vedi anche [Profili metadati](/help/assets/metadata-profiles.md).

È necessario disporre dei diritti di amministratore per creare, modificare ed eliminare profili immagine Dynamic Media o profili video Dynamic Media.

Dopo aver creato il profilo immagine o video, assegnalo a una o più cartelle da utilizzare per le risorse Dynamic Media appena caricate.

Consulta anche [Best practice per organizzare l&#39;Assets digitale per l&#39;utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).


>[!NOTE]
>
>Assets che passi da una cartella a un’altra non viene rielaborato. Si supponga, ad esempio, di avere la cartella 1 a cui è assegnato il profilo A e la cartella 2 a cui è assegnato il profilo B. Se sposti le risorse dalla cartella 1 alla cartella 2, le risorse spostate mantengono l’elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche quando si spostano risorse tra due cartelle a cui è assegnato lo stesso profilo.

## Rielaborare le risorse Dynamic Media in una cartella {#reprocessing-assets}

È possibile rielaborare le risorse in una cartella che dispone già di un profilo immagine Dynamic Media esistente o di un profilo video Dynamic Media modificato successivamente.

Ad esempio, supponiamo che tu abbia creato un profilo immagine Dynamic Media e lo abbia assegnato a una cartella. Tutte le risorse di immagini caricate nella cartella disponevano automaticamente del profilo di immagine applicato alle risorse. Tuttavia, in seguito deciderai di aggiungere una nuova proporzione di ritaglio avanzato al profilo immagine. Invece di dover selezionare e ricaricare nuovamente le risorse nella cartella, è sufficiente eseguire il flusso di lavoro *Rielaborazione elemento multimediale dinamico*.

Puoi eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale la prima elaborazione non è riuscita. Anche se non hai modificato un profilo immagine o un profilo video, oppure hai già applicato un profilo immagine o un profilo video, puoi comunque eseguire il flusso di lavoro di rielaborazione su una cartella di risorse in qualsiasi momento.

Se necessario, puoi modificare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse a un massimo di 1000 risorse. Quando si esegue il flusso di lavoro _Rielaborazione elemento multimediale dinamico_ in una cartella, le risorse vengono raggruppate in batch e quindi inviate al server Dynamic Media per l&#39;elaborazione. Dopo l&#39;elaborazione, i metadati di ogni risorsa nell&#39;intero set di batch vengono aggiornati il [!DNL Adobe Experience Manager]. Se la dimensione del batch è grande, si può verificare un ritardo nell’elaborazione. In alternativa, se la dimensione del batch è troppo piccola, potrebbero verificarsi troppi round trip al server Dynamic Media.

Vedere [Regolare la dimensione del batch del flusso di lavoro di rielaborazione](#adjusting-load).

>[!NOTE]
>
>Se si sta eseguendo una migrazione in blocco di risorse da Dynamic Media Classic a [!DNL Experience Manager], abilitare l&#39;agente di replica di migrazione sul server Dynamic Media. Al termine della migrazione, assicurati di disabilitare l’agente.
>
>L’agente di pubblicazione della migrazione deve essere disabilitato sul server Dynamic Media in modo che il flusso di lavoro Rielabora funzioni come previsto.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Per rielaborare le risorse Dynamic Media in una cartella:**

1. In [!DNL Experience Manager], dalla pagina Assets, passa a una cartella di risorse a cui è assegnato un profilo immagine o un profilo video e per la quale desideri applicare il flusso di lavoro **Rielaborazione elemento multimediale dinamico**.

   Alle cartelle a cui è assegnato un profilo immagine o un profilo video è assegnato il nome del profilo, che viene visualizzato direttamente sotto il nome della cartella in Vista a schede.

1. Seleziona una cartella.

   * Il flusso di lavoro considera tutti i file nella cartella selezionata in modo ricorsivo.
   * Se nella cartella principale selezionata sono presenti una o più sottocartelle con risorse, il flusso di lavoro rielabora ogni risorsa nella gerarchia delle cartelle.
   * Come best practice, evita di eseguire questo flusso di lavoro su una gerarchia di cartelle con più di 1000 risorse.

1. Selezionare **[!UICONTROL Timeline]** dall&#39;elenco a discesa nell&#39;angolo superiore sinistro della pagina.
1. Nell&#39;angolo inferiore sinistro della pagina, a destra del campo [!UICONTROL Commento], selezionare l&#39;icona del carato ( **^** ).

   ![Schermata di Assets in Experience Manager che mostra una cartella selezionata di risorse, l&#39;elenco a discesa Timeline evidenziato, il pulsante Avvia flusso di lavoro evidenziato e anche l&#39;icona a forma di carat a destra del campo Commento evidenziato](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Seleziona **[!UICONTROL Avvia flusso di lavoro]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Avvia flusso di lavoro]**, scegliere **[!UICONTROL Rielaborazione elemento multimediale dinamico]**.
1. (Facoltativo) Nel campo di testo **Inserisci il titolo del flusso di lavoro**, immetti un nome per il flusso di lavoro. Se necessario, puoi utilizzare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Schermata dell&#39;interfaccia utente Timeline con l&#39;opzione &quot;Rielaborazione elemento multimediale dinamico&quot; selezionata dall&#39;elenco a discesa Avvia flusso di lavoro e il pulsante Start evidenziato](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. Seleziona **[!UICONTROL Inizio]**, quindi seleziona **[!UICONTROL Conferma]**.

   Per monitorare il flusso di lavoro o controllarne l&#39;avanzamento, dalla pagina della console principale [!DNL Experience Manager] selezionare **[!UICONTROL Strumenti > Flusso di lavoro]**. Nella pagina Istanze flusso di lavoro, seleziona un flusso di lavoro. Sulla barra dei menu, selezionare **[!UICONTROL Cronologia elementi aperti]**. È inoltre possibile terminare, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regolare la dimensione batch del flusso di lavoro di rielaborazione (facoltativo) {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è di 50 risorse per processo. Questa dimensione ottimale del batch è determinata dalla dimensione media delle risorse e dai tipi MIME di risorse su cui viene eseguita la rielaborazione. Un valore più alto indica che in un singolo processo di rielaborazione sono presenti molti file. Pertanto, il banner di elaborazione rimane su [!DNL Experience Manager] risorse per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola-1 MB o inferiore, Adobe consiglia di aumentare il valore a diversi 100, ma mai più di 1000. Se la dimensione media del file è di centinaia di megabyte, Adobe consiglia di ridurre la dimensione del batch fino a 10.

**Per modificare facoltativamente la dimensione del batch del flusso di lavoro di rielaborazione:**

1. In [!DNL Experience Manager], seleziona **[!UICONTROL Adobe Experience Manager]** per accedere alla console di navigazione globale, quindi seleziona l&#39;icona **[!UICONTROL Strumenti]** (martello) > **[!UICONTROL Flusso di lavoro > Modelli]**.
1. Nella pagina Modelli di flusso di lavoro, in Vista a schede o Vista a elenco, selezionare **[!UICONTROL Rielaborazione elemento multimediale dinamico]**.

   ![Schermata della pagina Modelli flusso di lavoro con il flusso di lavoro &quot;Rielaborazione elementi multimediali dinamici&quot; selezionato nella vista a schede di Experience Manager](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. Nella barra degli strumenti, seleziona **[!UICONTROL Modifica]**. Una nuova scheda del browser apre la pagina del modello di flusso di lavoro Rielaborazione elementi multimediali dinamici.
1. Nella pagina del flusso di lavoro di rielaborazione Dynamic Media, nell&#39;angolo superiore destro, selezionare **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, seleziona il componente Caricamento batch Scene7 per aprire la barra degli strumenti, quindi seleziona **[!UICONTROL Configura]** nella barra degli strumenti.

   ![Schermata del componente &quot;Caricamento batch Scene7&quot; nella pagina &quot;Rielaborazione Dynamic Media&quot; con il puntatore del mouse sopra l&#39;icona &quot;Configura&quot;](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. Nella finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà passaggio]**, imposta quanto segue:
   * Nei campi di testo **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]** immettere un nuovo titolo e una nuova descrizione per il processo, se necessario.
   * Seleziona **[!UICONTROL Avanzamento gestore]** se il gestore avanza al passaggio successivo.
   * Nel campo **[!UICONTROL Timeout]** immettere il timeout del processo esterno (secondi).
   * Nel campo **[!UICONTROL Periodo]** immettere un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * Nel campo **[!UICONTROL Batch]**, immettere il numero massimo di risorse (50-1000) da elaborare in un processo di caricamento batch di elaborazione batch del server Dynamic Media.
   * Seleziona **[!UICONTROL Avanza per timeout]** se desideri avanzare una volta raggiunto il timeout. Deseleziona questa opzione per passare alla casella in entrata una volta raggiunto il timeout.

   ![Schermata della pagina &quot;Caricamento batch in Scene7 - Proprietà passaggio&quot;](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. Nell&#39;angolo superiore destro della finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà passaggio]**, seleziona **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro della pagina del modello di flusso di lavoro Rielabora elemento multimediale dinamico, selezionare **[!UICONTROL Sincronizza]**. Quando viene visualizzato **[!UICONTROL Sincronizzato]**, il modello runtime del flusso di lavoro è stato sincronizzato correttamente ed è pronto per rielaborare le risorse in una cartella.

   ![Schermata di Assets in Experience Manager che mostra una cartella selezionata di risorse, l&#39;elenco a discesa Timeline evidenziato, il pulsante Avvia flusso di lavoro evidenziato e anche l&#39;icona a forma di carat a destra del campo Commento evidenziato](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Chiudi la scheda del browser che mostra il modello di flusso di lavoro Rielaborazione elementi multimediali dinamici.

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
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
