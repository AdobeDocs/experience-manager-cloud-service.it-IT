---
title: Gestione predefiniti immagine
description: Scopri i predefiniti per immagini e come crearli, modificarli e gestirli.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 6%

---

# Gestione predefiniti immagine{#managing-image-presets}

I predefiniti per immagini consentono ad Adobe Experience Manager Assets di distribuire immagini in modo dinamico a diverse dimensioni, in formati diversi o con altre proprietà dell’immagine generate in modo dinamico. Ogni predefinito immagine rappresenta una raccolta predefinita di comandi di ridimensionamento e formattazione per la visualizzazione delle immagini. Quando crei un predefinito immagine, scegli una dimensione per la consegna delle immagini. È inoltre possibile scegliere i comandi di formattazione in modo che l&#39;aspetto dell&#39;immagine venga ottimizzato quando l&#39;immagine viene distribuita per la visualizzazione.

Gli amministratori possono creare predefiniti per esportare le risorse. Gli utenti possono scegliere un predefinito al momento dell&#39;esportazione delle immagini, che consente anche di riformattarle in base alle specifiche specificate dall&#39;amministratore.

È inoltre possibile creare predefiniti immagine dinamici. Se applichi un predefinito immagine reattivo alle risorse, questo varia a seconda del dispositivo o delle dimensioni dello schermo su cui vengono visualizzate. È possibile configurare i predefiniti immagine in modo che utilizzino CMYK nello spazio colore oltre a RGB o Gray.

Questa sezione descrive come creare, modificare e in genere gestire i predefiniti immagine. Potete applicare un predefinito immagine a un&#39;immagine in qualsiasi momento. Consulta [Applica predefiniti immagine](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>L&#39;imaging avanzato funziona con i predefiniti immagine esistenti e utilizza l&#39;intelligenza all&#39;ultimo millisecondo per ridurre ulteriormente le dimensioni del file immagine in base alla velocità della connessione del browser o di rete. Per ulteriori informazioni, vedere [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md).

## Informazioni sui predefiniti per immagini {#understanding-image-presets}

Analogamente a una macro, un predefinito immagine è un insieme predefinito di comandi di ridimensionamento e formattazione salvati con un nome. Per capire come funzionano i predefiniti per immagini, supponiamo che il sito web richieda che ogni immagine del prodotto sia visualizzata in dimensioni, formati e tassi di compressione diversi per la consegna su desktop e dispositivi mobili.

Potete creare due predefiniti immagine: 500 x 500 pixel per desktop e 150 x 150 pixel per dispositivi mobili. Si creano due predefiniti immagine, uno denominato `Enlarge` per visualizzare immagini a 500x500 pixel e uno denominato `Thumbnail` per visualizzare immagini a 150 x 150 pixel. Per distribuire immagini con le dimensioni `Enlarge` e `Thumbnail`, Experience Manager trova la definizione di `Enlarge Image Preset` e `Thumbnail Image Preset`. A questo punto Experience Manager genera un’immagine in modo dinamico in base alle dimensioni e alle specifiche di formattazione di ciascun predefinito immagine.

Le immagini di dimensioni ridotte, quando vengono distribuite in modo dinamico, possono perdere nitidezza e dettagli. Per questo motivo, ogni predefinito immagine contiene controlli di formattazione per ottimizzare un’immagine quando viene distribuita con una dimensione specifica. Questi controlli garantiscono che le immagini siano nitide e chiare quando vengono inviate al sito Web o all&#39;applicazione.

Gli amministratori possono creare predefiniti per immagini. Per creare un predefinito immagine, puoi iniziare da zero oppure da uno esistente e salvarlo con un nuovo nome.

## Gestione predefiniti immagine {#managing-image-presets-1}

Per gestire i predefiniti immagine in Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, fai clic sull&#39;icona Strumenti e vai a **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti immagine]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Tutti i predefiniti immagine creati sono disponibili anche come rappresentazioni dinamiche quando visualizzi l’anteprima o distribuisci le risorse.
>
>*non* devi pubblicare i predefiniti immagine perché i predefiniti immagine vengono pubblicati automaticamente.
>
>Consulta [Pubblica predefiniti immagine](#publishing-image-presets).

>[!NOTE]
>
>Il sistema mostra varie rappresentazioni quando si selezionano **[!UICONTROL Rappresentazioni]** nella visualizzazione Dettagli di una risorsa. Puoi aumentare o diminuire il numero di predefiniti immagine visualizzati. Vedere [Aumentare il numero di predefiniti immagine visualizzati](#increasing-or-decreasing-the-number-of-image-presets-that-display).

## Correlazione dei predefiniti immagine con le rappresentazioni {#how-image-presets-relate-to-renditions}

I predefiniti per immagini definiscono il modo in cui Dynamic Media distribuisce le immagini, inclusi il dimensionamento, la formattazione, la compressione e altri parametri di visualizzazione. I predefiniti non generano essi stessi le rappresentazioni. Si basano invece su rappresentazioni create durante l’elaborazione delle risorse.

### Generazione di rappresentazioni in AEM as a Cloud Service{#rendition-generation-in-aemaacs}

In AEM as a Cloud Service, le rappresentazioni vengono generate utilizzando [Asset Microservices](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use#). Il flusso di lavoro Risorsa di aggiornamento DAM non è disponibile per la personalizzazione in Cloud Service.

Considerazioni importanti includono quanto segue:

* Le rappresentazioni vengono generate al momento del caricamento.
* Le modifiche a un profilo di elaborazione interessano le nuove risorse caricate. Se sono necessarie nuove rappresentazioni, le risorse esistenti devono essere rielaborate.
* La personalizzazione del modello di flusso di lavoro non è supportata in AEM as a Cloud Service per la generazione di rappresentazioni.

I predefiniti immagine fanno riferimento alle rappresentazioni disponibili al momento della consegna. Assicurati che siano presenti le rappresentazioni richieste prima di configurare o utilizzare i predefiniti per immagini.

**Per controllare quali rendering vengono generati:**

1. Crea o modifica un [profilo di elaborazione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use#).
2. Configura le definizioni di rappresentazione richieste.
3. Applica il profilo di elaborazione alla cartella appropriata.

Quando le risorse vengono caricate in una cartella a cui è applicato un profilo di elaborazione, i microservizi per le risorse generano automaticamente le rappresentazioni definite.

<!--
### Adobe Illustrator (AI), PostScript&reg; (EPS), and PDF file formats {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

If you intend to support the ingestion of AI, EPS, and PDF files so that you can generate dynamic renditions of these file formats, review the following information before you create Image Presets.

Adobe Illustrator's file format is a variant of PDF. The main differences, in the context of Experience Manager Assets, are the following:

* Adobe Illustrator documents consist of a single page with multiple layers. Each layer is extracted as a PNG subasset under the main Illustrator asset.
* PDF documents consist of one or more pages. Each page is extracted as a single page PDF subasset under the main multi-page PDF document.

The `Create Sub Asset process` component creates the subassets within the overall `DAM Update Asset` workflow. To see this process component within the workflow, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.

See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file).

You can view the subassets or the pages when you open the asset, select the Content menu, and select **[!UICONTROL Subassets]** or **[!UICONTROL Pages]**. The subassets are real assets. The `Create Sub Asset` workflow component extracts the PDF pages. They are then stored as `page1.pdf`, `page2.pdf`, and so on, below the main asset. After they are stored, the `DAM Update Asset` workflow processes them.

To use Dynamic Media to preview and generate dynamic renditions for AI, EPS or PDF files, the following processing steps are required:

1. In the `DAM Update Asset` workflow, the `Rasterize PDF/AI Image Preview Rendition` process component rasterizes the first page of the original asset &ndash; using the configured resolution &ndash; into a `cqdam.preview.png` rendition.

1. The `Dynamic Media Process Image Assets` process component within the workflow optimizes the `cqdam.preview.png` rendition into a PTIFF.

>[!NOTE]
>
>In the DAM Update Asset workflow, the **[!UICONTROL EPS thumbnails]** step generates thumbnails for EPS files.

#### PDF/AI/EPS asset metadata properties {#pdf-ai-eps-asset-metadata-properties}

| **Metadata property** |**Description** |
|---|---|
| `dam:Physicalwidthininches` |Document width in inches. |
| `dam:Physicalheightininches` |Document height in inches. |

You access `Rasterize PDF/AI Image Preview Rendition` process component options by way of the `DAM Update Asset` workflow.

Select Adobe Experience Manager in the upper left, the click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**. On the Workflow Models page, select **[!UICONTROL DAM Update Asset]**, then on the toolbar select **[!UICONTROL Edit]**. On the DAM Update Asset workflow page, double-select the `Rasterize PDF/AI Image Preview Rendition` process component to open its Step Properties dialog box.

#### Rasterize PDF/AI Image Preview Rendition options {#rasterize-pdf-ai-image-preview-rendition-options}

![Arguments to rasterize PDF or AI workflow](assets/rasterize_pdf_ai_image_preview.png)

Arguments to rasterize PDF or AI workflow

|Process Argument | Default setting | Description |
|---|---|---|
| Mime Types | application/pdf<br>application/postscript<br>application/illustrator| List of document mime-types that are considered to be PDF or Illustrator documents. |
| Max Width | 2048 | Maximum width of the generated preview rendition, in pixels.|
| Max Height | 2048| Maximum height of the generated preview rendition, in pixels. |
| Resolution | 72 | Resolution to rasterize the first page, in ppi (pixels per inch). |

Using the default process arguments, the first page of a PDF/AI document is rasterized at 72 ppi and the generated preview image is sized at 2048 x 2048 pixels. For a typical deployment, you can increase the resolution to a minimum of 150 ppi or more. For example, a US letter size document at 300 ppi requires a maximum width and height of 2550 x 3300 pixels, respectively.

Max Width and Max Height limit the resolution at which to rasterize. For example, if the maximums are unchanged, and Resolution is set to 300 ppi, a US Letter document is rasterized at 186 ppi. That is, the document is 1581 x 2046 pixels.

The `Rasterize PDF/AI Image Preview Rendition` process component has a maximum defined to ensure that it does not create overly large images in memory. Such large images can overflow the memory provided to the JVM (Java&trade; Virtual Machine). Care must be taken to provide the JVM with enough memory to manage the configured number of parallel workflows, with each having the potential to create an image at the maximum configured size. -->

<!--
### InDesign (INDD) file format {#indesign-indd-file-format}

If you intend to support the ingestion of INDD files so that you can generate dynamic rendition of this file format, review the following information before you create Image Presets.

For InDesign files, sub assets are extracted only if the Adobe InDesign Server is integrated with Experience Manager. Referenced assets are linked based on their metadata. InDesign Server is not required for linking. However, the referenced assets must be present within Experience Manager before the InDesign files are processed for the links to be created between the InDesign files and the referenced assets.

See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md).

The Media Extraction process component in the `DAM Update Asset` workflow runs several pre-configured Extend Scripts to process InDesign files.

![The ExtendScript paths in the arguments of Media Extraction process](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

The ExtendScript paths in the arguments of the Media Extraction process component in the DAM Update Asset workflow.

The following scripts are used by Dynamic Media integration:


|ExtendScript name | Default | Description |
|---|---|---|
| ThumbnailExport.jsx | Yes  | Generates a 300 PPI `thumbnail.jpg` rendition that is optimized and turned into a PTIFF rendition by `Dynamic Media Process Image Assets` process component.  |
| JPEGPagesExport.jsx | Yes | Generates a 300 PPI JPEG subasset for each page. The JPEG subasset is a real asset stored under the InDesign asset. The `DAM Update Asset` workflow optimizes and converts it into a PTIFF. |
| PDFPagesExport.jsx | No | Generates a PDF subasset for each page. The PDF subasset gets processed as described earlier. Because the PDF contains a single page only, no subassets are generated. |
-->

<!--
### Configure the image thumbnail size {#configuring-image-thumbnail-size}

You can configure the size of thumbnails by configuring those settings in the **[!UICONTROL DAM Update Asset]** workflow. There are two steps in the workflow where you can configure the thumbnail size of image assets. One (**[!UICONTROL Dynamic Media Process Image Assets]**) is used for dynamic image assets. The other (**[!UICONTROL Process Thumbnails]**) is used for static thumbnail generation or when all other processes fail to generate thumbnails. Regardless, *both* must have the same settings.

The **[!UICONTROL Dynamic Media Process Image Assets]** step uses the image server to generate thumbnails, independently of the configuration applied to the **[!UICONTROL Process Thumbnails]** step. Generating thumbnails through the **[!UICONTROL Process Thumbnails]** step is the slowest and most memory intensive way to create thumbnails.

Thumbnail sizing is defined in the following format: **[!UICONTROL width:height:center]**, for example, `80:80:false`. The width and height determine the size in pixels of the thumbnail. The center value is either false or true. If set to true, it indicates that the thumbnail image has exactly the size given in the configuration. If the resized image is smaller, it is centered within the thumbnail.

>[!NOTE]
>
>* Thumbnail sizes for EPS files are configured in the **[!UICONTROL EPS thumbnails]** step, in the **[!UICONTROL Arguments]** tab under Thumbnails.
>
>* Thumbnail sizes for videos are configured in the **[!UICONTROL FFmpeg thumbnails]** step, in the **[!UICONTROL Process]** tab under **[!UICONTROL Arguments]**.
>

**To configure the image thumbnail size:**

1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL DAM Update Asset]** > **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Dynamic Media Process Image Assets]** step and select the **[!UICONTROL Thumbnails]** tab. Change the thumbnail size, as needed, then select **[!UICONTROL OK]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Select the **[!UICONTROL Process Thumbnails]** step, then select the **[!UICONTROL Thumbnails]** tab. Change the thumbnail size, as needed, then select **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >The values in the thumbnails argument in the **[!UICONTROL Process Thumbnails]** step must match the thumbnails argument in the **[!UICONTROL Dynamic Media Process Image Assets]** step.

1. Select **[!UICONTROL Save]** to save the changes to the workflow.
-->

## Aumenta o diminuisce il numero di immagini preimpostate visualizzate {#increasing-or-decreasing-the-number-of-image-presets-that-display}

I predefiniti immagine creati sono disponibili come rappresentazioni dinamiche quando visualizzi l’anteprima delle risorse. Experience Manager mostra varie rappresentazioni dinamiche quando si visualizza una risorsa da **[!UICONTROL Vista dettagli > Rappresentazioni]**. Puoi aumentare o diminuire il limite delle rappresentazioni visualizzate.

**Per aumentare o diminuire il numero di predefiniti immagine visualizzati:**

1. Passa a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Passa al nodo elenco predefiniti immagine in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![incremento_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Passa all&#39;origine dati del predefinito immagine in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Nella proprietà limit, modifica il numero impostando il numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Seleziona **[!UICONTROL Salva tutto]**.

## Creare predefiniti immagine {#creating-image-presets}

Crea predefiniti immagine per applicare le impostazioni in modo coerente tra le immagini durante l&#39;anteprima o la pubblicazione.

>[!NOTE]
>
>Se si utilizza Internet Explorer 9, la creazione di un predefinito non viene visualizzata nell&#39;elenco dei predefiniti subito dopo il salvataggio. Per risolvere il problema, disabilita la cache per IE9.

Se desideri supportare l’acquisizione di file AI, PDF e EPS in modo da poter generare una rappresentazione dinamica di questi formati di file, controlla le informazioni seguenti prima di creare predefiniti immagine.

Consulta [Formati di file Adobe Illustrator (AI), PostScript® (EPS) e PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Se intendete supportare l&#39;acquisizione di file INDD in modo da poter generare una rappresentazione dinamica di questo formato di file, consultate le seguenti informazioni prima di creare predefiniti immagine.

Vedere [Formato file InDesign (INDD)](#indesign-indd-file-format).

**Per creare predefiniti immagine:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti immagine]**.
1. Seleziona **[!UICONTROL Crea]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Per rendere dinamico questo predefinito immagine, cancella i valori nei campi **[!UICONTROL larghezza]** e **[!UICONTROL altezza]**, lasciandoli vuoti.

1. Nella finestra **[!UICONTROL Modifica predefinito immagine]**, immetti i valori desiderati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, compreso un nome. Le opzioni sono descritte in [Opzioni predefinito immagine](#image-preset-options). I predefiniti vengono visualizzati nel riquadro a sinistra e possono essere usati all’istante con altre risorse.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Seleziona **[!UICONTROL Salva]**.

## Creare un predefinito immagine reattivo {#creating-a-responsive-image-preset}

Per creare un predefinito immagine reattivo, esegui i passaggi descritti in [Creare predefiniti immagine](#creating-image-presets). Quando immetti l&#39;altezza e la larghezza nella finestra **[!UICONTROL Modifica predefinito immagine]**, cancella i valori e lasciali vuoti.

Se non specificate alcun valore, il predefinito immagine è dinamico per Experience Manager. È possibile regolare gli altri valori in modo appropriato.

>[!NOTE]
>
>Per visualizzare i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]** quando applichi un predefinito immagine a una risorsa, la risorsa deve essere pubblicata.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>I predefiniti per immagini e le risorse di immagini vengono pubblicati automaticamente.

### Opzioni predefinito immagine {#image-preset-options}

Quando si creano o si modificano i predefiniti immagine, sono disponibili le opzioni descritte in questa sezione. Inoltre, Adobe consiglia di iniziare dalle seguenti opzioni di &quot;best practice&quot;:

* **[!UICONTROL Formato]** (**[!UICONTROL Base]** scheda) - Seleziona **[!UICONTROL JPEG]** o un altro formato che soddisfa i tuoi requisiti. Tutti i browser web supportano il formato immagine JPEG, in quanto offre un buon compromesso tra dimensioni ridotte dei file e qualità delle immagini. Tuttavia, le immagini in formato JPEG usano uno schema di compressione che causa la perdita di dati, con possibile introduzione di artefatti di immagine indesiderati, qualora l’impostazione di compressione sia troppo bassa. Per questo motivo, Adobe consiglia di impostare la qualità di compressione su 75. Questa impostazione offre un buon compromesso tra la qualità delle immagini e le dimensioni ridotte dei file.

* **[!UICONTROL Abilita nitidezza semplice]**: non selezionare **[!UICONTROL Abilita nitidezza semplice]** (il filtro di nitidezza offre un controllo inferiore rispetto alle impostazioni Maschera definizione dettagli).

* **[!UICONTROL Nitidezza: Metodo Ricampionamento]** - Selezionare **[!UICONTROL Nitidezza2]**.

### Opzioni di base delle schede {#basic-tab-options}

| Campo | Descrizione |
| --- | --- |
| **Nome** | Inserisci un nome descrittivo senza spazi vuoti. Per aiutare gli utenti a identificare questo predefinito immagine, includi nel nome la specifica della dimensione dell’immagine. |
| **Larghezza e altezza** | Immettete la dimensione in pixel dell&#39;immagine trasmessa. Larghezza e altezza devono essere maggiori di 0 pixel. Se uno dei due valori è 0, non viene creato alcun predefinito. Se entrambi i valori sono vuoti, viene creato un predefinito immagine reattivo. |
| **Formato** | Scegliete un formato dal menu.<br>La scelta di **JPEG** offre le altre opzioni seguenti:<br>· **Qualità** - La scala di qualità di JPEG è 1-100. La scala è visibile quando si trascina il dispositivo di scorrimento.<br>· **Abilita downsampling crominanza JPG** - Poiché l&#39;occhio è meno sensibile alle informazioni di colore ad alta frequenza rispetto alla luminanza ad alta frequenza, le immagini JPEG dividono le informazioni dell&#39;immagine in componenti di luminanza e colore. Quando un&#39;immagine JPEG viene compressa, il componente di luminanza viene lasciato a risoluzione massima, mentre i componenti di colore vengono ricampionati verso il basso calcolando la media di gruppi di pixel. Il downsampling riduce il volume dei dati a metà o un terzo con un impatto minimo sulla qualità percepita. Il downsampling non è applicabile alle immagini in scala di grigio. Questa tecnica riduce la quantità di compressione utile per le immagini con contrasto elevato (ad esempio, immagini con testo sovrapposto).<br><br>La scelta di **GIF** o **GIF con alfa** fornisce le seguenti opzioni aggiuntive di **Quantizzazione colore GIF**:<br>· **Tipo** - Selezionare **Adattivo** (impostazione predefinita), **Web** o **Macintosh**. Se si seleziona **GIF con Alpha**, l&#39;opzione Macintosh non è disponibile.<br>· **Dithering** - Selezionare **Diffuse** o **Off**.<br>· **Numero di colori** - Immettere un numero compreso tra 2 e 256.<br>· **Elenco colori** - Immettere un elenco separato da virgole. Ad esempio, per bianco, grigio e nero, immettere `000000,888888,ffffff`.<br><br>La scelta di **PDF**, **TIFF** o **TIFF con Alfa** fornisce questa opzione aggiuntiva:<br>· **Compressione** - Selezionare un algoritmo di compressione. Le opzioni algoritmo per PDF sono **None**, **Zip** e **Jpeg**; per TIFF sono **None**, **LZW**, **Jpeg** e **Zip**; per TIFF con Alpha sono **None**, **LZW** e **Zip**.<br><br>La scelta di **PNG**, **PNG con Alpha** o **EPS** non fornisce opzioni aggiuntive. |
| **Nitidezza** | Selezionare **Attiva nitidezza semplice** per applicare un filtro di nitidezza di base all&#39;immagine dopo il ridimensionamento. La nitidezza può aiutare a compensare la sfocatura che può verificarsi quando si visualizza un&#39;immagine a dimensioni diverse. |

### Opzioni scheda avanzate {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Spazio colore</strong></td>
   <td>Selezionare <strong>RGB, CMYK,</strong> o <strong>Gradazioni di grigio</strong> per lo spazio colore.</td>
  </tr>
  <tr>
   <td><strong>Profilo colore</strong></td>
   <td>Seleziona il profilo dello spazio colore di output in cui vuoi convertire la risorsa, se diverso dal profilo di lavoro.</td>
  </tr>
  <tr>
   <td><strong>Intento di rendering</strong></td>
   <td>È possibile ignorare l'intento di rendering predefinito. Gli intenti di rendering determinano cosa accade ai colori che non possono essere riprodotti nel profilo colore di destinazione (fuori gamma). L'intento di rendering viene ignorato se non è compatibile con il profilo ICC.
    <ul>
     <li>Selezionare <strong>Percettivo</strong> per comprimere la gamma totale da uno spazio colore in un altro quando uno o più colori nell'immagine originale non rientrano nella gamma dello spazio colore di destinazione.</li>
     <li>Selezionare <strong>Colorimetrico relativo</strong> quando un colore nello spazio colore corrente non rientra nella gamma dello spazio colore di destinazione. E si vuole mappare il tutto sulla gamma di colori di destinazione più vicina senza alterare gli altri colori. </li>
     <li>Selezionare <strong>Saturazione</strong> per riprodurre la saturazione del colore dell'immagine originale durante la conversione nello spazio colore di destinazione. </li>
     <li>Selezionare <strong>Colorimetrico assoluto</strong> per far corrispondere i colori esattamente senza alcuna regolazione per il punto bianco o nero che modificherebbe la luminosità dell'immagine.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensazione punto nero</strong></td>
   <td>Selezionate questa opzione se il profilo di output supporta questa funzione. La compensazione del punto nero viene ignorata se non è compatibile con il profilo ICC specificato.</td>
  </tr>
  <tr>
   <td><strong>Dithering</strong></td>
   <td>Selezionate questa opzione per evitare o ridurre possibili artefatti di striature di colore. </td>
  </tr>
  <tr>
   <td><strong>Tipo di nitidezza</strong></td>
   <td><p>Selezionare <strong>Nessuna</strong>, <strong>Nitidezza</strong> o <strong>Maschera definizione dettagli</strong>. </p>
    <ul>
     <li>Selezionare <strong>Nessuno</strong> se si desidera disattivare la nitidezza.</li>
     <li>Selezionare <strong>Contrasta </strong> per applicare un filtro di nitidezza di base all'immagine dopo il ridimensionamento. La nitidezza può aiutare a compensare la sfocatura che può verificarsi quando si visualizza un'immagine a dimensioni diverse. </li>
     <li>Selezionare <strong> Maschera definizione dettagli</strong> se si desidera ottimizzare un effetto filtro di nitidezza sull'immagine ricampionata verso il basso finale. È possibile controllare l'intensità dell'effetto, il raggio (misurato in pixel) e una soglia di contrasto ignorata. Questo effetto utilizza le stesse opzioni del filtro "Maschera definizione dettagli" di Photoshop.</li>
    </ul> <p>In <strong>Maschera definizione dettagli</strong> sono disponibili le seguenti opzioni:</p>
    <ul>
     <li><strong>Importo</strong> - Controlla la quantità di contrasto applicata ai pixel del bordo. Il valore numerico reale predefinito è 1,0. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5.0. Considera Importo come una misura dell’intensità del filtro.</li>
     <li><strong>Raggio</strong> - Determina il numero di pixel attorno ai pixel del bordo che influiscono sulla nitidezza. Per le immagini ad alta risoluzione, immettere un numero reale compreso tra 1 e 2. Un valore basso agisce solo sui pixel del bordo; un valore alto agisce su una banda più ampia di pixel. Il valore corretto dipende dalle dimensioni dell'immagine.</li>
     <li><strong>Soglia</strong> - Determina l'intervallo di contrasto da ignorare quando viene applicato il filtro Maschera di contrasto. In altre parole, questa opzione definisce quanto i pixel resi più nitidi devono differire dall’area circostante per essere considerati pixel del bordo e più nitidi. Per evitare di introdurre disturbi, prova con valori interi compresi tra 2 e 20. </li>
     <li><strong>Applica a</strong> - Determina se l'annullamento della nitidezza viene applicato a ogni colore o luminosità.</li>
    </ul>
    <div>
      La nitidezza è descritta in
     <a href="https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media">Utilizzo della nitidezza delle immagini con il video di Experience Manager Dynamic Media</a>, <a href="https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/master-files/sharpening-image#master-files">Nitidezza di un'immagine</a> nella Guida in linea e <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf?lang=it">Best practice per la nitidezza delle immagini in Dynamic Media Classic</a> PDF scaricabile.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modalità ricampionamento</strong></td>
   <td>Selezionare un'opzione <strong>Ricampionamento modalità</strong>. Queste opzioni migliorano la nitidezza dell'immagine ricampionata verso il basso:
    <ul>
     <li><strong>Bilineare</strong> - Il metodo di ricampionamento più veloce. Alcuni artefatti di alias sono visibili.</li>
     <li><strong>Bicubico</strong> - Aumenta l'utilizzo di CPU ma genera immagini più nitide con artefatti di aliasing meno evidenti.</li>
     <li><strong>Nitido2</strong> - Può produrre risultati leggermente più nitidi rispetto a Bicubico, ma a un costo CPU ancora più elevato.</li>
     <li><strong>Bi-Sharp</strong> - Seleziona il ricampionatore predefinito di Photoshop per ridurre le dimensioni dell'immagine, denominato <strong>bicubic sharper</strong> in Adobe Photoshop.</li>
     <li><strong>Ogni colore</strong> e <strong>Luminosità</strong> - ogni metodo può essere basato sul colore o sulla luminosità. Per impostazione predefinita, è selezionato <strong>Ogni colore</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Risoluzione di stampa</strong></td>
   <td>Selezionare una risoluzione per la stampa dell'immagine. Il valore predefinito è 72 pixel.</td>
  </tr>
  <tr>
   <td><strong>Modificatore immagine</strong></td>
   <td><p>Oltre alle comuni impostazioni per le immagini disponibili nell'interfaccia utente, Dynamic Media supporta numerose modifiche avanzate per le immagini che puoi specificare nel campo <strong>Modificatori immagine</strong>. Questi parametri sono definiti nel riferimento del comando <a href="https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview">Image Server Protocol</a>.</p> <p>Importante: le seguenti funzionalità elencate nell’API non sono supportate:</p>
    <ul>
     <li>Comandi di base per la creazione di modelli e il rendering del testo: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandi di localizzazione: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> non è disponibile per l’utilizzo generale.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servizi Dynamic Media non core: SVG, Image Rendering e Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definire le opzioni del predefinito immagine con i modificatori immagine {#defining-image-preset-options-with-image-modifiers}

Oltre alle opzioni disponibili nelle schede Base e Avanzate, puoi definire modificatori di immagini per avere più opzioni quando definisci i predefiniti immagine. Image Rendering si basa sull&#39;API di rendering delle immagini di Dynamic Media ed è definito in dettaglio nella [documentazione del protocollo HTTP](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction#image-rendering-api).

Di seguito sono riportati alcuni esempi di base delle operazioni che è possibile eseguire con i modificatori di immagini.

>[!NOTE]
>
>Alcuni modificatori di immagini [&#x200B; non possono essere utilizzati in Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert) - Inverte ogni componente di colore per ottenere un effetto immagine negativo.

  ```xml {.line-numbers}
  &op_invert=1
  ```

  ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur) - Applica un filtro di sfocatura all&#39;immagine.

  ```xml {.line-numbers}
  &op_blur=7
  ```

  ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandi combinati - op_blur e op-invert

  ```xml {.line-numbers}
  &op_invert=1&op_blur=7
  ```

  ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness) - Diminuisce o aumenta la luminosità.

  ```xml {.line-numbers}
  &op_brightness=58
  ```

  ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac) - Regola l&#39;opacità dell&#39;immagine. Consente di ridurre l&#39;opacità in primo piano.

  ```xml {.line-numbers}
  opac=29
  ```

  ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Modificare i predefiniti immagine {#modifying-image-presets}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti immagine]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Selezionare un predefinito, quindi selezionare **[!UICONTROL Modifica]**. Viene visualizzata la finestra **[!UICONTROL Modifica predefinito immagine]**.
1. Apporta le modifiche e seleziona **[!UICONTROL Salva]** per salvarle oppure **[!UICONTROL Annulla]** per annullare le modifiche.

## Pubblicare predefiniti immagine {#publishing-image-presets}

I predefiniti per immagini vengono pubblicati automaticamente.

## Elimina predefiniti immagine {#deleting-image-presets}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi fai clic sull’icona Strumenti.
1. Passa a **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti immagine]**.
1. Selezionare un predefinito, quindi selezionare **[!UICONTROL Elimina]**. Dynamic Media conferma che desideri eliminarlo. Seleziona **[!UICONTROL Elimina]** per rimuovere o seleziona **[!UICONTROL Annulla]** per tornare ai predefiniti immagine.
