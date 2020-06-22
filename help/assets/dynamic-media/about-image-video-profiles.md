---
title: Profili immagine e profili video di Dynamic Media
description: Un profilo immagine o un profilo video è una ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, potete specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse di immagini Dynamic Media per ritagliarle correttamente.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 2%

---


# Profili immagine e profili video di Dynamic Media{#about-dm-image-video-profiles}

Un profilo immagine o un profilo video è una ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, potete specificare la codifica video da applicare alle risorse video Dynamic Media caricate. Oppure, quale profilo immagine applicare alle risorse di immagini Dynamic Media per ritagliarle correttamente.

In Dynamic Media, potete creare due tipi di profili, descritti dettagliatamente nei seguenti collegamenti:

* [Profili immagine Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Profili video Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consultate anche Profili [di](/help/assets/metadata-profiles.md)metadati.

È necessario disporre dei diritti di amministratore per creare, modificare ed eliminare profili immagine Dynamic Media o Dynamic Media Video.

Dopo aver creato il profilo immagine o il profilo video, potete assegnarlo a una o più cartelle da usare come destinazione per le risorse Dynamic Media appena caricate.

Consultate anche [Tecniche consigliate per l’organizzazione delle risorse digitali per l’utilizzo dei profili immagine o video](/help/assets/dynamic-media/best-practices-for-file-management.md).

>[!NOTE]
>
>Le risorse spostate da una cartella all’altra non vengono rielaborate. Ad esempio, supponiamo che alla cartella 1 sia assegnato il profilo A e che alla cartella 2 sia assegnato il profilo B. Se spostate le risorse dalla cartella 1 alla cartella 2, le risorse spostate conservano l’elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche per lo spostamento di risorse tra due cartelle alle quali è assegnato lo stesso profilo.

## Rielaborazione delle risorse Dynamic Media in una cartella {#reprocessing-assets}

Potete rielaborare le risorse in una cartella che dispone già di un profilo immagine Dynamic Media o di un profilo video Dynamic Media precedentemente modificato.

Ad esempio, se avete creato un profilo immagine Dynamic Media e lo avete assegnato a una cartella, Per tutte le risorse di immagine caricate nella cartella, alle risorse è stato applicato automaticamente il profilo immagine. Tuttavia, in seguito si decide di aggiungere un nuovo rapporto di ritaglio avanzato al profilo immagine. Ora, invece di dover selezionare e caricare nuovamente le risorse nella cartella completamente, è sufficiente eseguire *Scene7: Rielabora il flusso di lavoro delle risorse* .

Potete eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale l&#39;elaborazione non è riuscita per la prima volta. Anche se non avete modificato un profilo immagine o video o avete già applicato un profilo immagine o video, potete comunque eseguire il flusso di lavoro di rielaborazione su una cartella di risorse in qualsiasi momento.

Facoltativamente potete regolare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse fino a 1000 risorse. Quando eseguite _Scene7: Elaborate nuovamente il flusso di lavoro delle risorse_ in una cartella, le risorse vengono raggruppate in batch e quindi inviate al server Dynamic Media per l’elaborazione. Dopo l’elaborazione, i metadati di ciascuna risorsa dell’intero set di batch vengono aggiornati in AEM. Se le dimensioni del batch sono molto grandi, potrebbe verificarsi un ritardo nell&#39;elaborazione. Oppure, se la dimensione del batch è troppo piccola, può causare troppi viaggi di andata e ritorno al server Dynamic Media.

Consultate [Regolazione delle dimensioni batch del flusso di lavoro](#adjusting-load)di rielaborazione.

>[!NOTE]
>
>Se state eseguendo una migrazione di massa di risorse da Dynamic Media Classic ad AEM, dovete attivare l’agente di replica della migrazione sul server Dynamic Media. Al termine della migrazione, accertatevi di disabilitare l’agente.
L’agente di pubblicazione della migrazione deve essere disabilitato sul server Dynamic Media, in modo che il flusso di lavoro di rielaborazione funzioni come previsto.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Per rielaborare le risorse Dynamic Media in una cartella**:
1. In AEM, dalla pagina Risorse, individuate la cartella di risorse Dynamic Media a cui è assegnato un profilo immagine o video e per la quale desiderate applicare **Scene7: Rielabora flusso di lavoro risorse** ,

   Le cartelle a cui è già stato assegnato un profilo immagine o video sono indicate dalla visualizzazione del nome del profilo direttamente sotto il nome della cartella nella vista a schede.

1. Selezionate una cartella.

   * Il flusso di lavoro considera in modo ricorsivo tutti i file presenti nella cartella selezionata.
   * Se sono presenti una o più sottocartelle con le risorse nella cartella principale selezionata, il flusso di lavoro rielaborerà tutte le risorse nella gerarchia delle cartelle.
   * Come procedura ottimale, evitate di eseguire questo flusso di lavoro in una gerarchia di cartelle con più di 1000 risorse.

1. Fai clic su **[!UICONTROL Timeline]** dall’elenco a discesa nell’angolo in alto a sinistra della pagina.
1. Nell&#39;angolo inferiore sinistro della pagina, a destra del campo Commento, fate clic sull&#39;icona del carrello ( **^** ) .

   ![Rielabora flusso di lavoro risorse 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Fate clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Dall’elenco a discesa **[!UICONTROL Avvia flusso di lavoro]** , scegliete **[!UICONTROL Scene7: Rielabora risorse]**.
1. (Facoltativo) Nel campo di testo **Immettere il titolo del flusso di lavoro** , immettere un nome per il flusso di lavoro. Se necessario, potete usare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Rielaborare le risorse 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Fate clic su **[!UICONTROL Avvia]**, quindi su **[!UICONTROL Conferma]**.

   Per monitorare il flusso di lavoro o controllarne l’avanzamento, dalla pagina della console principale di AEM fate clic su **[!UICONTROL Strumenti > Flusso di lavoro]**. Nella pagina Istanze flusso di lavoro, selezionate un flusso di lavoro. Nella barra dei menu, fate clic su **[!UICONTROL Apri cronologia]**. È inoltre possibile terminare, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regolazione delle dimensioni batch del flusso di lavoro di rielaborazione {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è 50 risorse per processo. Questa dimensione batch ottimale è determinata dalla dimensione media delle risorse e dai tipi mime di risorse su cui viene eseguito il riprocesso. Con un valore più elevato potete inserire molti file in un singolo processo di rielaborazione. Di conseguenza, il banner di elaborazione rimane sulle risorse AEM per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola-1 MB o inferiore, Adobe consiglia di aumentare il valore a diverse centinaia, ma mai più di 1000. Se la dimensione media del file è grande centinaia di MB, Adobe consiglia di ridurre la dimensione del batch fino a 10.

**Per regolare facoltativamente la dimensione batch del flusso di lavoro di rielaborazione**

1. In Experience Manager, tocca **[!UICONTROL Adobe Experience Manager]** per accedere alla console di navigazione globale, quindi tocca l’icona **[!UICONTROL Strumenti]** (martello) > **[!UICONTROL Flusso di lavoro > Modelli]**.
1. Nella pagina Modelli flusso di lavoro, nella vista a schede o a elenco, selezionate **[!UICONTROL Scene7: Rielabora risorse]**.

   ![Pagina Modelli di workflow con Scene7: Rielabora flusso di lavoro risorse selezionato nella vista a schede](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. Nella barra degli strumenti, fate clic su **[!UICONTROL Modifica]**. Viene aperta una nuova scheda del browser che consente di aprire Scene7: Rielabora la pagina del modello del flusso di lavoro Risorse.
1. In Scene7: Rielabora la pagina del flusso di lavoro delle risorse, nell’angolo in alto a destra, tocca **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, selezionate il componente Caricamento batch di Scene7 per aprire la barra degli strumenti, quindi toccate **[!UICONTROL Configura]** nella barra degli strumenti.

   ![Componente Caricamento batch Scene7](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. Nella finestra di dialogo Caricamento **[!UICONTROL batch in Scene7 - Proprietà]** passaggio, impostate quanto segue:
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * Selezionate **[!UICONTROL Avanzamento]** gestore se il gestore procederà al passaggio successivo.
   * Nel campo **[!UICONTROL Timeout]** , immettere il timeout del processo esterno (secondi).
   * Nel campo **[!UICONTROL Periodo]** , immettete un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * Selezionate **[!UICONTROL Anticipo su timeout]** se desiderate avanzare quando viene raggiunto il timeout. Deselezionate questa opzione se desiderate passare alla inbox quando viene raggiunto il timeout.

   ![Proprietà, finestra di dialogo](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. Nell’angolo in alto a destra della finestra di dialogo Caricamento **[!UICONTROL batch in Scene7 - Proprietà]** passaggio, toccate **[!UICONTROL Fine]**.

1. Nell’angolo in alto a destra di Scene7: Rielabora la pagina del modello del flusso di lavoro Risorse, tocca **[!UICONTROL Sincronizza]**. Quando viene visualizzato **[!UICONTROL Sincronizzato]**, il modello runtime del flusso di lavoro viene sincronizzato correttamente e pronto per rielaborare le risorse in una cartella.

   ![Sincronizzazione del modello di workflow](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Chiudete la scheda del browser che mostra Scene7: Rielabora il modello di flusso di lavoro Risorse.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
