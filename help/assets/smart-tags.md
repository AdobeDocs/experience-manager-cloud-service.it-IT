---
title: Assegnare tag automatici alle risorse con  [!DNL Adobe Sensei] servizio avanzato
description: Assegna tag alle risorse un servizio intelligente artificialmente che applica tag aziendali contestuali e descrittivi.
contentOwner: AG
feature: Tag avanzati, assegnazione tag
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '2346'
ht-degree: 6%

---


# Aggiungere tag avanzati alle risorse per migliorare l’esperienza di ricerca {#smart-tag-assets-for-faster-search}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave a cui i dipendenti, i partner e i clienti utilizzano comunemente per fare riferimento e cercare le loro risorse digitali. L’assegnazione di tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificare e recuperare facilmente le risorse nelle ricerche.

Rispetto ai vocabolari linguistici naturali, l’assegnazione di tag basati sulla tassonomia aziendale consente di allineare le risorse al business di un’azienda e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche. Ad esempio, un produttore di automobili può assegnare tag alle immagini di un&#39;automobile con nomi di modello in modo che vengano visualizzate solo le immagini pertinenti quando viene eseguita una ricerca per progettare una campagna promozionale.

In background, la funzionalità utilizza il framework artificialmente intelligente di [Adobe Sensei](https://www.adobe.com/it/sensei/experience-cloud-artificial-intelligence.html) per addestrare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e sulla tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse. [!DNL Experience Manager Assets] per impostazione  [!DNL Adobe Developer Console] predefinita, le distribuzioni sono integrate con .

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipi di risorse supportate {#smart-tags-supported-file-formats}

Puoi assegnare i tag ai seguenti tipi di risorse:

* **Immagini**: Le immagini in molti formati vengono taggate utilizzando i servizi di contenuti avanzati di Adobe Sensei. Crea un modello di formazione [e quindi le immagini caricate vengono automaticamente taggate. ](#train-model) I tag avanzati vengono applicati ai tipi di file supportati che generano rappresentazioni in formato JPG e PNG.
* **Risorse** basate su testo:  [!DNL Experience Manager Assets] assegna automaticamente i tag alle risorse basate su testo supportate al momento del caricamento.
* **Risorse** video: L’assegnazione tag video è abilitata per impostazione predefinita in  [!DNL Adobe Experience Manager] come  [!DNL Cloud Service]. [I video vengono contrassegnati automaticamente ](/help/assets/smart-tags-video-assets.md) quando carichi nuovi video o rielabori quelli esistenti.

| Immagini (tipi MIME) | Risorse basate su testo (formati di file) | Risorse video (formati di file e codec) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| immagine/x-portatile-anymap | PPTX |  |
| immagine/x-portatile-bitmap | RTF |  |
| immagine/x-portatile-grigio | SRT |  |
| immagine/x-portatile-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| immagine/photoshop |  |  |
| immagine/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] aggiunge automaticamente i tag avanzati alle risorse basate su testo e ai video per impostazione predefinita. Per aggiungere automaticamente tag avanzati alle immagini, completa le seguenti attività.

* [Comprendere i modelli e le linee guida dei tag](#understand-tag-models-guidelines).
* [Addestra il modello](#train-model).
* [Assegna tag alle risorse](#tag-assets) digitali.
* [Gestisci i tag e le ricerche](#manage-smart-tags-and-searches).

## Comprendere i modelli e le linee guida dei tag {#understand-tag-models-guidelines}

Un modello di tag è un gruppo di tag correlati associati a vari aspetti visivi delle immagini a cui viene applicato un tag. I tag si riferiscono a diversi aspetti visivi delle immagini, in modo che, se applicati, i tag contribuiscano alla ricerca di specifici tipi di immagini. Ad esempio, una raccolta di scarpe può avere tag diversi, ma tutti i tag sono correlati alle scarpe e possono appartenere allo stesso modello di tag. Quando applicati, i tag consentono di trovare diversi tipi di scarpe, ad esempio per progettazione o per uso. Per comprendere la rappresentazione dei contenuti di un modello di formazione in [!DNL Experience Manager], visualizza un modello di formazione come entità di livello superiore composta da un gruppo di tag aggiunti manualmente e immagini di esempio per ciascun tag. Ogni tag può essere applicato esclusivamente a un’immagine.

Prima di creare un modello di tag e di addestrare il servizio, identifica un set di tag univoci che descrivono al meglio gli oggetti contenuti nelle immagini nel contesto della tua attività. Assicurati che le risorse nel set curato siano conformi alle [linee guida di formazione](#training-guidelines).

### Linee guida per la formazione {#training-guidelines}

Assicurati che le immagini del set di addestramento siano conformi alle seguenti linee guida:

**Quantità e dimensioni:** almeno 10 immagini e un massimo di 50 immagini per tag.

**Coerenza**: Assicurati che le immagini di un tag siano visivamente simili. È consigliabile aggiungere tag sugli stessi aspetti visivi (come lo stesso tipo di oggetti in un’immagine) insieme in un unico modello di tag. Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coherence.png)

**Copertura**: Dovrebbe esserci una varietà sufficiente nelle immagini nell&#39;addestramento. L&#39;idea è quella di fornire alcuni esempi, ma abbastanza diversi, in modo che [!DNL Experience Manager] impari a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi di ogni tipo. Ad esempio, per il tag *model-down-pose*, includi più immagini di formazione simili all&#39;immagine evidenziata qui sotto per consentire al servizio di identificare immagini simili con maggiore precisione durante l&#39;assegnazione dei tag.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: Il servizio si allena meglio sulle immagini che hanno meno distrazioni (sfondi ben visibili, accompagnamento indipendenti, come oggetti/persone con il soggetto principale). Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per l&#39;addestramento.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali *raincoat* e *model-side-view*, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](assets/do-not-localize/completeness.png)

**Numero di tag**: Adobe consiglia di addestrare un modello utilizzando almeno due tag distinti e almeno dieci immagini diverse per ciascun tag. In un singolo modello di tag, non aggiungere più di 50 tag.

**Numero di esempi**: Per ogni tag, aggiungi almeno dieci esempi. Tuttavia, l&#39;Adobe consiglia circa 30 esempi. Sono supportati un massimo di 50 esempi per tag.

**Prevenire falsi positivi e conflitti**: Adobe consiglia di creare un singolo modello di tag per un singolo aspetto visivo. Crea una struttura per i modelli di tag in modo da evitare sovrapposizioni di tag tra i modelli. Ad esempio, non utilizzare tag comuni come `sneakers` in due nomi di modelli di tag diversi `shoes` e `footwear`. Il processo di formazione sovrascrive un modello di tag addestrato con l’altro per una parola chiave comune.

**Esempi**: Altri esempi di indicazioni sono:

* Creare un modello di tag che includa solo:

   * I tag relativi ai modelli di auto.
   * I tag relativi alle giacche per donne e uomini.

* Non creare,

   * Un modello di tag che include modelli di auto rilasciati nel 2019 e 2020.
   * Modelli di tag multipli che includono gli stessi pochi modelli di auto.

**Immagini utilizzate per la formazione**: Puoi utilizzare le stesse immagini per addestrare diversi modelli di tag. Tuttavia, non associare un’immagine a più tag in un modello di tag. È possibile assegnare tag alla stessa immagine con tag diversi appartenenti a modelli di tag diversi.

Non è possibile annullare la formazione. Le linee guida di cui sopra dovrebbero aiutarti a scegliere buone immagini da addestrare.

## Addestra il modello per i tag personalizzati {#train-model}

Per creare e addestrare un modello per i tag specifici dell’azienda, effettua le seguenti operazioni:

1. Crea i tag necessari e la struttura tag appropriata. Carica le immagini rilevanti nell’archivio DAM.
1. Nell&#39;interfaccia utente [!DNL Experience Manager], accedi a **[!UICONTROL Risorse]** > **[!UICONTROL Formazione di tag avanzati]**.
1. Fai clic su **[!UICONTROL Crea]**. Fornire un **[!UICONTROL Titolo]**, **[!UICONTROL Descrizione]**.
1. Sfogliare e selezionare i tag esistenti in `cq:tags` per i quali si desidera addestrare il modello. Fai clic su **[!UICONTROL Avanti]**.
1. Nella finestra di dialogo **[!UICONTROL Seleziona risorse]**, fai clic su **[!UICONTROL Aggiungi risorse]** rispetto a ciascun tag. Cerca nell’archivio DAM o sfoglia l’archivio per selezionare almeno 10 e al massimo 50 immagini. Seleziona le risorse e non la cartella. Dopo aver selezionato le immagini, fai clic su **[!UICONTROL Seleziona]**.

   ![Visualizza stato formazione](assets/smart-tags-training-status.png)

1. Per visualizzare in anteprima le miniature delle immagini selezionate, fai clic sul pannello a soffietto davanti a un tag. Per modificare la selezione, fai clic su **[!UICONTROL Aggiungi risorse]**. Una volta effettuata la selezione, fare clic su **[!UICONTROL Invia]**. L’interfaccia utente visualizza una notifica nella parte inferiore della pagina che indica che il training è stato avviato.
1. Controlla lo stato del corso di formazione nella colonna **[!UICONTROL Stato]** per ogni modello di tag. Gli stati possibili sono [!UICONTROL Pending], [!UICONTROL Tradotto] e [!UICONTROL Non riuscito].

![Flusso di lavoro per addestrare il modello di assegnazione tag per tag avanzati](assets/smart-tag-model-training-flow.png)

*Figura: Passaggi del flusso di lavoro di formazione per addestrare il modello di assegnazione tag.*

### Visualizzare lo stato e il rapporto della formazione {#training-status}

Per verificare se il servizio Tag avanzati è addestrato sui tag nel set di risorse di formazione, controlla il rapporto del flusso di lavoro di formazione dalla console Rapporti .

1. Nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il rapporto **[!UICONTROL Formazione tag avanzati]**, quindi fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi, fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il rapporto, fai clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Rivedi i dettagli del rapporto. Il rapporto mostra lo stato di formazione per i tag che hai appreso. Il colore verde nella colonna **[!UICONTROL Stato formazione]** indica che per il tag è stato eseguito il training del servizio Tag avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag. Se i tag non vengono visualizzati in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.Tags
1. Per scaricare il rapporto, selezionalo dall’elenco e fai clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo [!DNL Microsoft Excel].

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## Assegnare tag alle risorse con tag avanzati {#tag-assets}

Quando viene caricato, tutti i tipi di risorse supportate ricevono automaticamente i tag di [!DNL Experience Manager Assets] . L’assegnazione tag è abilitata per impostazione predefinita. [!DNL Experience Manager] applica i tag appropriati in tempo quasi reale.  <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

Per immagini e video, i tag avanzati vengono derivati in base ad alcuni aspetti visivi.

Per le risorse basate su testo, l’efficacia di Tag avanzati non dipende dalla quantità di testo nella risorsa, ma dalle parole chiave o entità pertinenti presenti nel testo della risorsa. Per le risorse basate su testo, i tag avanzati sono le parole chiave che compaiono nel testo ma quelle che descrivono meglio la risorsa. Per le risorse supportate, [!DNL Experience Manager] estrae già il testo, che viene quindi indicizzato e utilizzato per cercare le risorse. Tuttavia, i tag avanzati basati su parole chiave nel testo forniscono un facet di ricerca dedicato, strutturato e con priorità più elevata, utilizzato per migliorare l’individuazione delle risorse rispetto all’indice di ricerca completa.

## Gestione di tag avanzati e ricerche delle risorse {#manage-smart-tags-and-searches}

È possibile curare gli smart tag per rimuovere eventuali tag non accurati assegnati alle risorse del brand, in modo da visualizzare solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche delle risorse in base ai tag, garantendo che le risorse vengano visualizzate nei risultati di ricerca per i tag più rilevanti. In sostanza, aiuta a eliminare le possibilità che risorse non correlate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare un rango più alto a un tag per aumentare la pertinenza del tag per la risorsa. La promozione di un tag per una risorsa aumenta le possibilità che la risorsa appaia nei risultati della ricerca quando viene eseguita una ricerca in base al tag specifico.

Per moderare gli smart tag delle risorse:

1. Nel campo di ricerca cerca le risorse basate su un tag .

1. Inspect mostra i risultati della ricerca per identificare le risorse che non sono pertinenti alla ricerca.

1. Seleziona la risorsa, quindi seleziona ![Icona Gestisci tag](assets/do-not-localize/manage-tags-icon.png) dalla barra degli strumenti.

1. Dalla pagina **[!UICONTROL Gestione tag]** , controlla i tag . Se non desideri che la risorsa venga cercata in base a un tag specifico, seleziona il tag e seleziona ![Icona Elimina](assets/do-not-localize/delete-icon.png) dalla barra degli strumenti. In alternativa, seleziona il simbolo `X` accanto all’etichetta.

1. Per assegnare un rango più alto a un tag, selezionalo e seleziona ![Icona Promuovi](assets/do-not-localize/promote-icon.png) dalla barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]** .

1. Seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]** per chiudere la finestra di dialogo [!UICONTROL Success].

1. Passa alla pagina [!UICONTROL Proprietà] della risorsa. Osserva che al tag promosso è assegnata un’elevata rilevanza e, quindi, appare più alta nei risultati della ricerca.

### Comprendere i risultati di ricerca [!DNL Experience Manager] con gli smart tag {#understand-search}

Per impostazione predefinita, la ricerca [!DNL Experience Manager] combina i termini di ricerca con una clausola `AND`. L’utilizzo di smart tag non modifica questo comportamento predefinito. L’utilizzo di tag avanzati aggiunge una clausola `OR` per trovare uno dei termini di ricerca negli smart tag applicati. Ad esempio, è consigliabile cercare `woman running`. Le risorse con una semplice `woman` o una semplice `running` parola chiave nei metadati non vengono visualizzate nei risultati di ricerca per impostazione predefinita. Tuttavia, una risorsa con tag `woman` o `running` utilizzando tag avanzati viene visualizzata in una query di ricerca di questo tipo. Quindi i risultati della ricerca sono una combinazione di:

* risorse con `woman` e `running` parole chiave nei metadati.

* risorse con tag avanzati con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrisponde a `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` negli smart tag.
1. corrispondenze di `woman` o di `running` negli smart tag.

## Limitazioni e best practice per l’assegnazione di tag {#limitations}

L’assegnazione tag avanzati è basata su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente dei tag avanzati presenta le seguenti limitazioni:

* Incapacità di riconoscere sottili differenze nelle immagini. Ad esempio, camicie slim-fit contro le magliette normali.
* Impossibile identificare i tag in base a pattern o parti di un’immagine di dimensioni ridotte. Ad esempio, i loghi sulle camicie.
* L’assegnazione tag è supportata nelle lingue supportate da [!DNL Experience Manager]. Per un elenco delle lingue, consulta [Note sulla versione del Servizio di contenuti avanzati](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* I tag che non vengono gestiti in modo realistico sono correlati a:

   * Aspetti non visivi e astratti. Ad esempio, l&#39;anno o la stagione di rilascio di un prodotto, l&#39;umore o le emozioni evocate da un&#39;immagine, la connotazione soggettiva di un video e così via.
   * Differenze visive fini in prodotti quali camicie con e senza collari o loghi di prodotti di piccole dimensioni incorporati nei prodotti.

<!-- TBD: Add limitations related to text-based assets. -->

Per cercare le risorse con tag avanzati (regolari o migliorati), utilizza la ricerca [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per gli smart tag.

>[!NOTE]
>
>La capacità dei tag avanzati di addestrare i tag e applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione.
>Per ottenere risultati ottimali, l’Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

>[!MORELIKETHIS]
>
>* [Informazioni sulla gestione delle risorse tramite tag avanzati](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Assegnare tag avanzati alle risorse video](smart-tags-video-assets.md)

