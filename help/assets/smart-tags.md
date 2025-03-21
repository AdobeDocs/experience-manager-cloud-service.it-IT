---
title: Come si aggiungono tag avanzati alle risorse in AEM?
description: Aggiungi tag avanzati alle risorse in AEM con un servizio artificialmente intelligente che applica tag aziendali contestuali e descrittivi.
contentOwner: AG
feature: Smart Tags
role: Admin, User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 7%

---


# Aggiungere tag avanzati alle risorse in AEM {#smart-tags-assets-aem}

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

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/enhanced-smart-tags.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più spesso il vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave che i dipendenti, i partner e i clienti utilizzano comunemente per fare riferimento alle proprie risorse digitali e per ricercarle. L’assegnazione dei tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificarle e recuperarle facilmente nelle ricerche.

Rispetto ai vocabolari del linguaggio naturale, l’assegnazione di tag basati sulla tassonomia aziendale consente di allineare le risorse con le attività aziendali di un’azienda e assicura che le risorse più rilevanti vengano visualizzate nelle ricerche. Ad esempio, un produttore di automobili può taggare le immagini dell’auto con i nomi dei modelli in modo da visualizzare solo le immagini pertinenti quando viene effettuata la ricerca per progettare una campagna promozionale.

In background, la funzionalità utilizza il framework artificialmente intelligente di [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) per addestrare l&#39;algoritmo di riconoscimento delle immagini in base alla struttura dei tag e alla tassonomia aziendale. Questa content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse. Per impostazione predefinita, AEM applica automaticamente i tag avanzati alle risorse caricate.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipi di risorse supportati per i tag avanzati in AEM {#smart-tags-supported-file-formats}

Puoi assegnare i tag ai seguenti tipi di risorse:

* **Immagini**: alle immagini in molti formati vengono assegnati tag mediante i servizi di contenuti avanzati di Adobe Sensei. [crea un modello di apprendimento](#train-model) e le immagini caricate vengono automaticamente taggate. I tag avanzati vengono applicati ai tipi di file supportati che generano rappresentazioni in formato JPG e PNG.
* **Risorse basate su testo**: [!DNL Experience Manager Assets] assegna tag automatici alle risorse basate su testo supportate al momento del caricamento.
* **Risorse video**: l&#39;assegnazione tag video è abilitata per impostazione predefinita in [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. [I video vengono contrassegnati con tag automatici](/help/assets/smart-tags-video-assets.md) quando carichi nuovi video o rielabora quelli esistenti.

| Immagini (tipi MIME) | Risorse basate su testo (formati di file) | Risorse video (formati di file e codec) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap | |  |
| image/x-xpixmap | |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

Per impostazione predefinita, AEM aggiunge automaticamente i tag avanzati alle risorse basate su testo e ai video. Per aggiungere automaticamente tag avanzati alle immagini, completa le seguenti attività.

* [Comprendere i modelli di tag e le linee guida](#understand-tag-models-guidelines).
* [Addestra il modello](#train-model).
* [Assegna tag alle risorse digitali](#tag-assets).
* [Gestione di tag e ricerche](#manage-smart-tags-and-searches).

## Comprendere modelli e linee guida per i tag {#understand-tag-models-guidelines}

Un modello di tag è un gruppo di tag correlati associati a vari aspetti visivi delle immagini a cui vengono assegnati tag. I tag si riferiscono agli aspetti visivi nettamente diversi delle immagini, in modo che, se applicati, aiutino a cercare tipi specifici di immagini. Ad esempio, una raccolta di scarpe può avere tag diversi, ma tutti i tag sono correlati alle scarpe e possono appartenere allo stesso modello di tag. Quando applicati, i tag consentono di trovare diversi tipi di scarpe, ad esempio in base alla progettazione o all’utilizzo. Per comprendere la rappresentazione del contenuto di un modello di apprendimento in [!DNL Experience Manager], visualizzare un modello di apprendimento come entità di livello principale composta da un gruppo di tag aggiunti manualmente e immagini di esempio per ogni tag. Ogni tag può essere applicato esclusivamente a un’immagine.

Prima di creare un modello di tag e addestrare il servizio, identifica un set di tag univoci che descrivono al meglio gli oggetti nelle immagini nel contesto della tua azienda. Assicurati che le risorse del set curato siano conformi alle [linee guida per la formazione](#training-guidelines).

### Linee guida per la formazione {#training-guidelines}

Assicurati che le immagini nel set di formazione siano conformi alle seguenti linee guida:

**Quantità e dimensioni:** almeno 10 immagini e massimo 50 immagini per tag.

**Coerenza**: verifica che le immagini di un tag siano visivamente simili. È consigliabile aggiungere i tag relativi agli stessi aspetti visivi (come lo stesso tipo di oggetti in un’immagine) in un unico modello di tag. Ad esempio, non è consigliabile assegnare a queste immagini il tag `my-party` (per la formazione), perché non sono visivamente simili.

![Immagini illustrative che illustrano le linee guida per la formazione](assets/do-not-localize/coherence.png)

**Copertura**: le immagini del corso di formazione devono essere sufficientemente diverse. L&#39;idea è quella di fornire alcuni esempi, ma ragionevolmente diversi, in modo che [!DNL Experience Manager] apprenda a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi per ogni tipo. Ad esempio, per il tag *model-down-pose*, includi più immagini di formazione simili all&#39;immagine evidenziata di seguito affinché il servizio identifichi più accuratamente immagini simili durante l&#39;assegnazione dei tag.

![Immagini illustrative che illustrano le linee guida per la formazione](assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: il servizio si addestra meglio alle immagini che hanno meno distrazione (sfondi prominenti, accompagnamenti non correlati, come oggetti/persone con il soggetto principale). Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per la formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali *raincoat* e *model-side-view*, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](assets/do-not-localize/completeness.png)

**Numero di tag**: Adobe consiglia di addestrare un modello utilizzando almeno due tag distinti e almeno dieci immagini diverse per ogni tag. In un singolo modello di tag, non aggiungere più di 50 tag.

**Numero di esempi**: per ogni tag, aggiungi almeno dieci esempi. Tuttavia, Adobe consiglia circa 30 esempi. Sono supportati un massimo di 50 esempi per tag.

**Impedisci falsi positivi e conflitti**: Adobe consiglia di creare un modello di tag singolo per un singolo aspetto visivo. Strutturare i modelli di tag in modo da evitare la sovrapposizione dei tag tra i modelli. Ad esempio, non utilizzare tag comuni come `sneakers` in due diversi modelli di tag con nomi `shoes` e `footwear`. Il processo di apprendimento sovrascrive un modello di tag addestrato con l’altro per una parola chiave comune.

**Esempi**: ulteriori esempi a titolo di guida:

* Crea un modello di tag che includa solo:

   * I tag relativi ai modelli di auto.
   * I tag relativi a giacche per adulti e bambini.

* Non creare,

   * Un modello di tag che include i modelli di auto rilasciati nel 2019 e nel 2020.
   * Più modelli di tag che includono gli stessi pochi modelli di auto.

**Immagini utilizzate per addestrare**: è possibile utilizzare le stesse immagini per addestrare diversi modelli di tag. Tuttavia, non associare un’immagine a più tag in un modello di tag. È possibile assegnare tag alla stessa immagine con tag diversi appartenenti a modelli di tag diversi.

Non è possibile annullare l’apprendimento. Le linee guida di cui sopra dovrebbero aiutarti a scegliere le immagini migliori da addestrare.

## Addestra il modello per i tag personalizzati {#train-model}

Per creare e addestrare un modello per i tag specifici per l’azienda, segui questi passaggi:

1. Crea i tag necessari e la struttura tag appropriata. Carica le immagini rilevanti nell’archivio DAM.
1. Nell&#39;interfaccia utente di [!DNL Experience Manager], accedere a **[!UICONTROL Assets]** > **[!UICONTROL Apprendimento dei tag avanzati]**.
1. Fai clic su **[!UICONTROL Crea]**. Fornisci un **[!UICONTROL Titolo]**, **[!UICONTROL Descrizione]**.
1. Fai clic sull&#39;icona della cartella nel campo **[!UICONTROL Tag]**. Viene visualizzata una finestra popup.
1. Cercare o selezionare i tag appropriati dai tag esistenti in `cq-tags` che si desidera aggiungere al modello. Fai clic su **[!UICONTROL Avanti]**.

   >[!NOTE]
   >
   >Puoi ordinare la struttura dei tag in ordine crescente o decrescente in base alla data **[!UICONTROL Name]** (ordine alfabetico), **[!UICONTROL Created]** o **[!UICONTROL Modified]**.


1. Nella finestra di dialogo **[!UICONTROL Seleziona Assets]**, fai clic su **[!UICONTROL Aggiungi Assets]** per ogni tag. Cerca nell’archivio DAM o sfoglia l’archivio per selezionare almeno 10 e al massimo 50 immagini. Seleziona le risorse e non la cartella. Dopo aver selezionato le immagini, fare clic su **[!UICONTROL Seleziona]**.

   ![Visualizza stato apprendimento](assets/smart-tags-training-status.png)

1. Per visualizzare in anteprima le miniature delle immagini selezionate, fai clic sul pannello a soffietto di fronte a un tag. Puoi modificare la selezione facendo clic su **[!UICONTROL Aggiungi Assets]**. Una volta effettuata la selezione, fare clic su **[!UICONTROL Invia]**. L’interfaccia utente visualizza una notifica nella parte inferiore della pagina che indica che il corso di formazione è stato avviato.
1. Controlla lo stato del corso di formazione nella colonna **[!UICONTROL Stato]** per ogni modello di tag. Gli stati possibili sono [!UICONTROL In sospeso], [!UICONTROL Addestrato] e [!UICONTROL Non riuscito].

![Flusso di lavoro per addestrare il modello di assegnazione tag per Tag avanzati](assets/smart-tag-model-training-flow.png)

*Figura: passaggi del flusso di lavoro di formazione per addestrare il modello di assegnazione tag.*

### Visualizza stato e rapporto del corso di formazione {#training-status}

Per verificare se il servizio Tag avanzati è stato addestrato sui tag nel set di apprendimento delle risorse, controlla il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il report **[!UICONTROL Apprendimento dei tag avanzati]** e fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi fare clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il report, fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Esamina i dettagli del rapporto. Il rapporto mostra lo stato di formazione per i tag che hai appreso. Il colore verde nella colonna **[!UICONTROL Training Status]** indica che il servizio Tag avanzati è stato addestrato per il tag. Il colore giallo indica che il servizio è parzialmente addestrato per un determinato tag. Per addestrare completamente il servizio per un tag, aggiungi altre immagini con il tag specifico ed esegui il flusso di lavoro di formazione. Se non trovi i tuoi tag in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.Tags
1. Per scaricare il report, selezionarlo dall&#39;elenco e fare clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo.

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

## Assegnare tag alle risorse con tag avanzati in AEM {#tag-assets}

Tutti i tipi di risorse supportate vengono automaticamente taggati da [!DNL Experience Manager Assets] al momento del caricamento. Per impostazione predefinita, l’assegnazione tag è attivata e funziona. AEM applica i tag avanzati appropriati quasi in tempo reale. <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* Per immagini e video, i tag avanzati si basano su alcuni aspetti visivi.

* Per le risorse basate su testo, l’efficacia dei tag avanzati non dipende dalla quantità di testo nella risorsa, ma dalle parole chiave o entità pertinenti presenti nel testo della risorsa. Per le risorse basate su testo, i tag avanzati sono le parole chiave visualizzate nel testo, ma quelle che meglio descrivono la risorsa. Per le risorse supportate, [!DNL Experience Manager] estrae già il testo, che viene quindi indicizzato e utilizzato per cercare le risorse. Tuttavia, i tag avanzati basati sulle parole chiave nel testo forniscono un facet di ricerca dedicato, strutturato e con priorità più elevata. Quest’ultimo consente di migliorare l’individuazione delle risorse rispetto a un indice di ricerca.

## Gestire tag avanzati e ricerche di risorse {#manage-smart-tags-and-searches}

Puoi curare i tag avanzati per rimuovere eventuali tag non accurati assegnati alle risorse del tuo marchio, in modo che vengano visualizzati solo i tag più rilevanti.

La moderazione dei tag avanzati consente inoltre di perfezionare le ricerche di risorse basate su tag, garantendo che le risorse vengano visualizzate nei risultati di ricerca per i tag più rilevanti. In sostanza, aiuta a eliminare la possibilità che risorse non correlate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare una classificazione più alta a un tag per aumentarne la rilevanza per la risorsa. La promozione di un tag per una risorsa aumenta le possibilità che la risorsa appaia nei risultati di ricerca quando viene eseguita una ricerca in base a tale tag.

Per moderare i tag avanzati delle risorse digitali:

1. Nel campo di ricerca, cerca le risorse digitali in base a un tag.

1. Per identificare le risorse digitali che non trovi rilevanti per la ricerca, controlla i risultati della ricerca.

1. Seleziona una risorsa, quindi seleziona ![Icona Gestisci tag](assets/do-not-localize/manage-tags-icon.png) dalla barra degli strumenti.

1. Nella pagina **[!UICONTROL Gestisci tag]**, controlla i tag. Se non desideri che la risorsa venga cercata in base a un tag specifico, seleziona il tag e fai clic sull&#39;![icona Elimina](assets/do-not-localize/delete-icon.png) nella barra degli strumenti. In alternativa, selezionare il simbolo `X` accanto all&#39;etichetta.

1. Per assegnare una classificazione superiore a un tag, selezionare il tag e selezionare ![Icona Promuovi](assets/do-not-localize/promote-icon.png) dalla barra degli strumenti. Il tag promosso è stato spostato nella sezione **[!UICONTROL Tag]**.

1. Seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]** per chiudere la finestra di dialogo [!UICONTROL Operazione riuscita].

1. Passa alla pagina [!UICONTROL Proprietà] della risorsa. Tieni presente che al tag promosso viene assegnata una rilevanza elevata e, pertanto, viene visualizzato più in alto nei risultati di ricerca.

### Comprendere i risultati della ricerca di [!DNL Experience Manager] con tag avanzati {#understand-search}

Per impostazione predefinita, la ricerca [!DNL Experience Manager] combina i termini di ricerca con una clausola `AND`. L’utilizzo di smart tag non modifica questo comportamento predefinito. L&#39;utilizzo di smart tag aggiunge una clausola `OR` per trovare i termini di ricerca negli smart tag applicati. Ad esempio, provare a cercare `woman running`. Assets con solo `woman` o solo `running` parola chiave nei metadati non viene visualizzata nei risultati della ricerca per impostazione predefinita. Tuttavia, una risorsa con tag `woman` o `running` tramite tag avanzati viene visualizzata in tale query di ricerca. I risultati della ricerca sono quindi una combinazione di:

* Assets con `woman` e `running` parole chiave nei metadati.

* Smart tag di Assets con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca nei tag avanzati. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrispondenze di `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` negli smart tag.
1. corrispondenze di `woman` o di `running` negli smart tag.

## Limitazioni e best practice relative ai tag {#limitations}

L’assegnazione tag avanzati migliorata si basa sull’apprendimento di modelli di immagini e dei relativi tag. Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente dei tag avanzati presenta le seguenti limitazioni:

* Incapacità di riconoscere le sottili differenze nelle immagini. Ad esempio, magliette o magliette.
* Impossibilità di identificare i tag in base a modelli o parti di un’immagine di dimensioni ridotte. Ad esempio, i logo sulle camicie.
* I tag sono supportati nelle lingue supportate da [!DNL Experience Manager].
* I tag non gestiti si riferiscono a:

   * Aspetti astratti e non visivi. Ad esempio, l’anno o la stagione di rilascio di un prodotto, l’umore o l’emozione evocati da un’immagine e una connotazione soggettiva di un video.
   * Differenze visive precise in prodotti come camicie con e senza colletto o logo di prodotto incorporati nei prodotti.

Per addestrare il modello, utilizzate le immagini più appropriate. Non è possibile ripristinare l’addestramento o rimuovere il modello di addestramento. La precisione dei tag dipende dall&#39;addestramento corrente, quindi esegui questa operazione con attenzione.

<!-- TBD: Add limitations related to text files. -->

Per cercare file con smart tag (regolari o avanzati), utilizzare la ricerca [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per i tag avanzati.

>[!NOTE]
>
>La capacità dei tag avanzati di addestrarsi sui tag e di applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per l’apprendimento.
>Per ottenere i migliori risultati, Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

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

>[!MORELIKETHIS]
>
>* [Comprendere come gli smart tag consentono di gestire i file digitali](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Usa tag avanzati per video](smart-tags-video-assets.md)
