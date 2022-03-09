---
title: Gestire i predefiniti per immagini
description: Scopri i predefiniti immagine e come creare, modificare e gestire i predefiniti immagine.
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: 77f1b744dabd72fc26d3b0607db9561e6cb7fa66
workflow-type: tm+mt
source-wordcount: '3629'
ht-degree: 8%

---

# Gestire i predefiniti per immagini{#managing-image-presets}

I predefiniti per immagini consentono ad Adobe Experience Manager Assets di distribuire dinamicamente immagini di dimensioni diverse, in formati diversi o con altre proprietà immagine generate in modo dinamico. Ogni predefinito per immagini rappresenta un insieme predefinito di comandi di ridimensionamento e formattazione per la visualizzazione delle immagini. Quando crei un predefinito per immagini, scegli una dimensione per la distribuzione delle immagini. È inoltre possibile scegliere i comandi di formattazione in modo che l&#39;aspetto dell&#39;immagine sia ottimizzato quando l&#39;immagine viene distribuita per la visualizzazione.

Gli amministratori possono creare predefiniti per l’esportazione delle risorse. Gli utenti possono scegliere un predefinito al momento dell’esportazione delle immagini, che riformatta anche le immagini in base alle specifiche specificate dall’amministratore.

Puoi anche creare predefiniti immagine reattivi. Se applichi un predefinito immagine reattiva alle risorse, questo cambia a seconda del dispositivo o delle dimensioni dello schermo su cui vengono visualizzate. È possibile configurare i predefiniti immagine per l’utilizzo di CMYK nello spazio colore, oltre a RGB o Grigio.

Questa sezione descrive come creare, modificare e gestire in genere i predefiniti per immagini. È possibile applicare un predefinito immagine a un&#39;immagine in qualsiasi momento in cui viene visualizzata in anteprima. Vedi [Applica predefiniti immagine](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Vedi [Imaging avanzato](/help/assets/dynamic-media/imaging-faq.md) per ulteriori informazioni.

## Informazioni sui predefiniti per immagini {#understanding-image-presets}

Come una macro, un predefinito per immagini è un insieme predefinito di comandi di ridimensionamento e formattazione salvati con un nome. Per comprendere il funzionamento dei predefiniti per immagini, supponiamo che il sito web richieda che ogni immagine del prodotto venga visualizzata in dimensioni diverse, in formati diversi e nei tassi di compressione per la distribuzione desktop e mobile.

Puoi creare due predefiniti immagine: uno con 500 x 500 pixel per la versione desktop e 150 x 150 pixel per la versione mobile. Puoi creare due predefiniti immagine, uno denominato `Enlarge` per visualizzare immagini a 500x500 pixel e una chiamata `Thumbnail` per visualizzare immagini a 150 x 150 pixel. Per distribuire le immagini `Enlarge` e `Thumbnail` Ad Experience Manager, trova la definizione di Ingrandisci predefinito immagine e Predefinito immagine miniatura. Quindi, Experience Manager genera in modo dinamico un&#39;immagine con le specifiche di dimensione e formattazione di ciascun predefinito per immagini.

Le immagini a dimensioni ridotte quando vengono consegnate in modo dinamico possono perdere nitidezza e dettagli. Per questo motivo, ogni predefinito per immagini contiene controlli di formattazione per l’ottimizzazione di un’immagine quando viene distribuita con una particolare dimensione. Questi controlli assicurano che le immagini siano nitide e chiare quando vengono inviate al sito Web o all&#39;applicazione.

Gli amministratori possono creare i predefiniti per immagini. Per creare un predefinito per immagini, puoi iniziare da zero o da uno esistente e salvarlo con un nuovo nome.

## Gestire i predefiniti per immagini {#managing-image-presets-1}

Per gestire i predefiniti immagine in Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi fai clic sull’icona Strumenti e passa a **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagine]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Eventuali predefiniti immagine creati sono disponibili anche come rappresentazioni dinamiche quando visualizzi l’anteprima o la distribuzione delle risorse.
>
>Lei lo fa *not* devono pubblicare i predefiniti per immagini quando i predefiniti per immagini vengono pubblicati automaticamente.
>
>Vedi [Pubblica predefiniti immagine](#publishing-image-presets).

>[!NOTE]
>
>Il sistema mostra varie rappresentazioni quando selezioni **[!UICONTROL Rendering]** in Vista dettagli di una risorsa. Puoi aumentare o diminuire il numero di predefiniti immagine da visualizzare. Vedi [Aumenta il numero di predefiniti immagine visualizzati](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Formati di file Adobe Illustrator (AI), PostScript® (EPS) e PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Se desideri supportare l’acquisizione di file AI, EPS e PDF in modo da poter generare rappresentazioni dinamiche di questi formati di file, controlla le seguenti informazioni prima di creare i predefiniti per immagini.

Il formato di file Adobe Illustrator è una variante di PDF. Le principali differenze nel contesto di Experience Manager Assets sono le seguenti:

* I documenti Adobe Illustrator sono costituiti da una singola pagina con più livelli. Ogni livello viene estratto come risorsa secondaria PNG sotto la risorsa principale Illustrator.
* I documenti PDF sono costituiti da una o più pagine. Ogni pagina viene estratta come risorsa secondaria PDF a pagina singola sotto il documento PDF principale con più pagine.

Le risorse secondarie vengono create dalla `Create Sub Asset process` nel complesso `DAM Update Asset` workflow. Per visualizzare questo componente del processo all’interno del flusso di lavoro, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Risorsa di aggiornamento DAM]** > **[!UICONTROL Modifica]**.

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

Puoi visualizzare le risorse secondarie o le pagine quando apri la risorsa, selezionare il menu Contenuto e selezionare **[!UICONTROL Risorse secondarie]** o **[!UICONTROL Pagine]**. Le risorse secondarie sono risorse reali. In altre parole, le pagine di PDF vengono estratte dal `Create Sub Asset` componente flusso di lavoro. Vengono quindi memorizzati come `page1.pdf`, `page2.pdf`, e così via, sotto la risorsa principale. Una volta memorizzati, il `DAM Update Asset` il flusso di lavoro li elabora.

Per utilizzare Dynamic Media per visualizzare in anteprima e generare rappresentazioni dinamiche per file AI, EPS o PDF, sono necessari i seguenti passaggi di elaborazione:

1. In `DAM Update Asset` flusso di lavoro, `Rasterize PDF/AI Image Preview Rendition` il componente di processo rasterizza la prima pagina della risorsa originale, utilizzando la risoluzione configurata, in un `cqdam.preview.png` rendering.

1. La `cqdam.preview.png` il rendering viene quindi ottimizzato in un PTIFF dal `Dynamic Media Process Image Assets` elabora il componente all’interno del flusso di lavoro.

>[!NOTE]
>
>Nel flusso di lavoro Risorsa di aggiornamento DAM, il passaggio **[!UICONTROL Miniature EPS]** genera le miniature per i file EPS.

#### Proprietà dei metadati delle risorse di PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Proprietà metadati** | **Descrizione** |
|---|---|
| dam:Physicalwidthinpollici | Larghezza documento in pollici. |
| dam:Physicalheightinpollici | Altezza del documento in pollici. |

Accesso `Rasterize PDF/AI Image Preview Rendition` opzioni dei componenti del processo tramite `DAM Update Asset` workflow.

Seleziona Adobe Experience Manager in alto a sinistra, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Nella pagina Modelli di flusso di lavoro , seleziona **[!UICONTROL Risorsa di aggiornamento DAM]**, quindi seleziona sulla barra degli strumenti **[!UICONTROL Modifica]**. Nella pagina del flusso di lavoro Aggiorna risorsa DAM , tocca due volte il pulsante `Rasterize PDF/AI Image Preview Rendition` per aprire la relativa finestra di dialogo Proprietà passaggio.

#### Rasterizzare le opzioni di rendering dell’anteprima immagine di PDF/AI {#rasterize-pdf-ai-image-preview-rendition-options}

![Argomenti per rasterizzare il flusso di lavoro di PDF o AI](assets/rasterize_pdf_ai_image_preview.png)

Argomenti per rasterizzare il flusso di lavoro di PDF o AI

| Argomento del processo | Impostazione predefinita | Descrizione |
|---|---|---|
| Tipi mime | application/pdf<br>application/postscript<br>applicazione/illustratore | Elenco di tipi di mime di documenti considerati come documenti PDF o Illustrator. |
| Larghezza max. | 2048 | Larghezza massima del rendering di anteprima generato, in pixel. |
| Altezza max. | 2048 | Altezza massima in pixel del rendering di anteprima generato. |
| Risoluzione | 72 | Risoluzione per rasterizzare la prima pagina, in ppi (pixel per pollice). |

Utilizzando gli argomenti di processo predefiniti, la prima pagina di un documento PDF/AI viene rasterizzata a 72 ppi e l’immagine di anteprima generata è dimensionata a 2048 x 2048 pixel. Per una distribuzione tipica, puoi aumentare la risoluzione fino a un minimo di 150 ppi o più. Ad esempio, un documento con dimensioni lettera USA a 300 ppi richiede rispettivamente una larghezza e un&#39;altezza massime di 2550 x 3300 pixel.

Larghezza massima e Altezza massima limitano la risoluzione a cui rasterizzare. Ad esempio, se i valori massimi sono invariati e la risoluzione è impostata su 300 ppi, un documento Lettera USA viene rasterizzato a 186 ppi. Cioè, il documento è di 1581 x 2046 pixel.

La `Rasterize PDF/AI Image Preview Rendition` il componente di processo ha un valore massimo definito per garantire che non crei immagini troppo grandi nella memoria. Immagini di grandi dimensioni possono sovraccaricare la memoria fornita alla JVM (Java™ Virtual Machine). È necessario prestare attenzione a fornire alla JVM memoria sufficiente per gestire il numero configurato di flussi di lavoro paralleli, ognuno dei quali ha il potenziale per creare un&#39;immagine alle dimensioni massime configurate.

### Formato di file InDesign (INDD) {#indesign-indd-file-format}

Se desideri supportare l’acquisizione di file INDD in modo da poter generare il rendering dinamico di questo formato di file, controlla le seguenti informazioni prima di creare i predefiniti per immagini.

Per i file InDesign, le risorse secondarie vengono estratte solo se Adobe InDesign Server è integrato con Experience Manager. Le risorse di riferimento sono collegate in base ai relativi metadati. InDesign Server non è necessario per il collegamento. Tuttavia, le risorse a cui si fa riferimento devono essere presenti in Experience Manager prima che i file InDesign vengano elaborati affinché i collegamenti possano essere creati tra i file InDesign e le risorse a cui si fa riferimento.

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

Il componente Processo di estrazione dei file multimediali nel `DAM Update Asset` Il flusso di lavoro esegue diversi script di estensione preconfigurati per elaborare i file InDesign.

![I percorsi ExtendScript negli argomenti del processo di estrazione di file multimediali](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

I percorsi ExtendScript negli argomenti del componente del processo di estrazione di file multimediali nel flusso di lavoro Aggiorna risorsa DAM .

I seguenti script vengono utilizzati dall’integrazione Dynamic Media:


| Nome ExtendScript | Predefiniti | Descrizione |
|---|---|---|
| ThumbnailExport.jsx | Sì | Genera un PPI 300 `thumbnail.jpg` rendering ottimizzato e trasformato in rendering PTIFF da `Dynamic Media Process Image Assets` componente processo. |
| JPEGPagesExport.jsx | Sì | Genera una risorsa secondaria PPI 300 JPEG per ogni pagina. La risorsa secondaria JPEG è una risorsa reale memorizzata nella risorsa InDesign. Viene inoltre ottimizzato e trasformato in un PTIFF tramite `DAM Update Asset` workflow. |
| PDFPagesExport.jsx | No | Genera una risorsa secondaria PDF per ogni pagina. La risorsa secondaria PDF viene elaborata come descritto in precedenza. Poiché PDF contiene una sola pagina, non vengono generate risorse secondarie. |

### Configurare le dimensioni delle miniature delle immagini {#configuring-image-thumbnail-size}

Puoi configurare le dimensioni delle miniature configurando tali impostazioni nella sezione **[!UICONTROL Risorsa di aggiornamento DAM]** workflow. Nel flusso di lavoro sono disponibili due passaggi per configurare la dimensione delle miniature delle risorse immagine. Uno (**[!UICONTROL Risorse immagine di processo Dynamic Media]**) viene utilizzata per le risorse di immagini dinamiche. L&#39;altro (**[!UICONTROL Miniature del processo]**) viene utilizzata per la generazione di miniature statiche o quando tutti gli altri processi non riescono a generare miniature. Indipendentemente dal fatto, *entrambi* devono avere le stesse impostazioni.

Con il passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**, le miniature vengono generate da Image Server e questa configurazione è indipendente da quella applicata al passaggio **[!UICONTROL Elabora miniature]**. La generazione delle miniature tramite il passaggio **[!UICONTROL Elabora miniature]** rappresenta il modo più lento e laborioso di creare le miniature, in termini di utilizzo della memoria.

Il dimensionamento delle miniature è definito nel seguente formato: **[!UICONTROL larghezza:height:centro]**, ad esempio `80:80:false`. La larghezza e l’altezza determinano le dimensioni in pixel della miniatura. Il valore centrale è falso o vero. Se è impostato su true, indica che l&#39;immagine in miniatura ha esattamente le dimensioni specificate nella configurazione. Se l&#39;immagine ridimensionata è più piccola, viene centrata all&#39;interno della miniatura.

>[!NOTE]
>
>* Le dimensioni delle miniature per i file EPS sono configurate nel **[!UICONTROL Miniature EPS]** nel **[!UICONTROL Argomenti]** sotto Miniature.
>
>* Le dimensioni delle miniature per i video sono configurate in **[!UICONTROL Miniature FFmpeg]** nel **[!UICONTROL Processo]** scheda sotto **[!UICONTROL Argomenti]**.
>


**Per configurare le dimensioni delle miniature delle immagini:**

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Risorsa di aggiornamento DAM]** > **[!UICONTROL Modifica]**.
1. Seleziona la **[!UICONTROL Risorse immagine di processo Dynamic Media]** e seleziona la **[!UICONTROL Miniature]** scheda . Modifica le dimensioni delle miniature in base alle esigenze, quindi seleziona **[!UICONTROL OK]**.

   ![6_5_dinamicmediaprocesseassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Seleziona la **[!UICONTROL Miniature del processo]** , quindi seleziona la **[!UICONTROL Miniature]** scheda . Modifica le dimensioni delle miniature in base alle esigenze, quindi seleziona **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >I valori nell’argomento miniature del passaggio **[!UICONTROL Elabora miniature]** devono corrispondere all’argomento miniature nel passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**.

1. Seleziona **[!UICONTROL Salva]** per salvare le modifiche al flusso di lavoro.

### Aumenta o diminuisce il numero di predefiniti immagine visualizzati {#increasing-or-decreasing-the-number-of-image-presets-that-display}

I predefiniti immagine creati sono disponibili come rappresentazioni dinamiche quando visualizzi in anteprima le risorse. Experience Manager mostra varie rappresentazioni dinamiche quando visualizzi una risorsa da **[!UICONTROL Vista dettagli > Rendering]**. Puoi aumentare o diminuire il limite di rappresentazioni visualizzate.

**Per aumentare o diminuire il numero di predefiniti immagine visualizzati:**

1. Passa a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Passa al nodo di elenco dei predefiniti immagine in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![Increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Passa alla sorgente dati del predefinito per immagini in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Nella proprietà limit , modifica il numero in base al numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Seleziona **[!UICONTROL Salva tutto]**.

### Creare predefiniti immagine {#creating-image-presets}

Crea i predefiniti per immagini in modo da poter applicare le impostazioni in modo coerente tra le immagini durante l’anteprima o la pubblicazione.

>[!NOTE]
>
>Se si utilizza Internet Explorer 9, la creazione di un predefinito non viene visualizzata nell’elenco dei predefiniti subito dopo il salvataggio. Per risolvere questo problema, disattiva la cache per IE9.

Se desideri supportare l’acquisizione di file AI, PDF e EPS in modo da generare il rendering dinamico di questi formati di file, controlla le informazioni seguenti prima di creare i predefiniti per immagini.

Vedi [Formati di file Adobe Illustrator (AI), PostScript® (EPS) e PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Se desideri supportare l’acquisizione di file INDD in modo da poter generare il rendering dinamico di questo formato di file, controlla le seguenti informazioni prima di creare i predefiniti per immagini.

Vedi [Formato di file InDesign (INDD)](#indesign-indd-file-format).

**Per creare predefiniti immagine:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagine]**.
1. Seleziona **[!UICONTROL Crea]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Per rendere dinamico questo predefinito immagine, cancella i valori nei campi **[!UICONTROL larghezza]** e **[!UICONTROL altezza]**, lasciandoli vuoti.

1. In **[!UICONTROL Modifica predefinito immagine]** immetti valori nella finestra **[!UICONTROL Base]** e **[!UICONTROL Avanzate]** , compreso un nome. Le opzioni sono descritte in [Opzioni predefinito immagine](#image-preset-options). I predefiniti vengono visualizzati nel riquadro a sinistra e possono essere usati all’istante con altre risorse.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Seleziona **[!UICONTROL Salva]**.

### Creazione di un predefinito per immagini reattive {#creating-a-responsive-image-preset}

Per creare un predefinito per immagini reattive, esegui i passaggi descritti in [Creare predefiniti immagine](#creating-image-presets). Quando immetti l’altezza e la larghezza nel **[!UICONTROL Modifica predefinito immagine]** cancella i valori e lasciali vuoti.

Lasciandoli vuoti, indica ad Experience Manager che questo predefinito per immagini è reattivo. Se necessario, puoi regolare gli altri valori.

>[!NOTE]
>
>Per visualizzare i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]** quando applichi un predefinito immagine a una risorsa, essa deve essere pubblicata.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>I predefiniti immagine e le risorse immagine vengono pubblicati automaticamente.

### Opzioni del predefinito immagine {#image-preset-options}

Quando crei o modifichi i predefiniti immagine, hai le opzioni descritte in questa sezione. Inoltre, l’Adobe consiglia di iniziare con le seguenti opzioni di &quot;best practice&quot;:

* **[!UICONTROL Formato]** scheda (**[!UICONTROL Base]**) - Seleziona **[!UICONTROL JPEG]** o un altro formato che rispetta i tuoi requisiti. Tutti i browser web supportano il formato immagine JPEG, in quanto offre un buon compromesso tra dimensioni ridotte dei file e qualità delle immagini. Tuttavia, le immagini in formato JPEG usano uno schema di compressione che causa la perdita di dati, con possibile introduzione di artefatti di immagine indesiderati, qualora l’impostazione di compressione sia troppo bassa. Per questo motivo, Adobe consiglia di impostare la qualità di compressione su 75. Questa impostazione offre un buon compromesso tra la qualità delle immagini e le dimensioni ridotte dei file.

* **[!UICONTROL Attiva nitidezza semplice]**: non selezionare **[!UICONTROL Attiva nitidezza semplice]** (il filtro di nitidezza offre un controllo inferiore rispetto alle impostazioni Maschera definizione dettagli).

* **[!UICONTROL Nitidezza: Modalità di ricampionamento]** - Seleziona **[!UICONTROL Bi-Cubic]**.

#### Opzioni della scheda Base {#basic-tab-options}

| Campo | Descrizione |
| --- | --- |
| **Nome** | Inserisci un nome descrittivo senza spazi vuoti. Per aiutare gli utenti a identificare questo predefinito per immagini, includi nel nome la specifica della dimensione dell’immagine. |
| **Larghezza e altezza** | Immettere in pixel le dimensioni in cui l&#39;immagine viene distribuita. Larghezza e altezza devono essere maggiori di 0 pixel. Se uno dei due valori è 0, non viene creato alcun predefinito. Se entrambi i valori sono vuoti, viene creato un predefinito per immagini reattive. |
| **Formato** | Scegli un formato dal menu.<br>Scelta **JPEG** offre le seguenti altre opzioni:<br>・ **Qualità** - La scala di qualità JPEG è 1-100. La scala è visibile quando si trascina il cursore.<br>・ **Abilita il downsampling della crominanza di JPG** - Poiché l&#39;occhio è meno sensibile alle informazioni sui colori ad alta frequenza rispetto alla luminanza ad alta frequenza, le immagini JPEG dividono le informazioni sulle immagini in componenti luminanza e colore. Quando un&#39;immagine JPEG viene compressa, il componente luminanza viene lasciato a risoluzione piena, mentre i componenti colore vengono sottoposti a sottocampionamento utilizzando una media di gruppi di pixel. Il sottocampionamento riduce il volume dei dati di mezzo o di un terzo, senza quasi alcun impatto sulla qualità percepita. Il campionamento non è applicabile alle immagini in scala di grigi. Questa tecnica riduce la quantità di compressione utile per le immagini con contrasto elevato (ad esempio, immagini con testo sovrapposto).<br><br>Scelta **GIF** o **GIF con alfa** fornisce questi **Quantizzazione colore GIF** opzioni:<br>・ **Tipo** - Seleziona **Adattivo** (predefinito), **Web** oppure **Macintosh**. Se si seleziona **GIF con Alpha**, l’opzione Macintosh non è disponibile.<br>・ **Dither** - Seleziona **Diffusore** o **Disattivato**.<br>・ **Numero di colori** - Inserire un numero 2 - 256.<br>・ **Elenco colori** - Inserire un elenco separato da virgole. Ad esempio, per bianco, grigio e nero, immetti `000000,888888,ffffff`.<br><br>Scelta **PDF**, **TIFF** oppure **TIFF con alfa** fornisce questa opzione aggiuntiva:<br>・ **Compressione** - Selezionare un algoritmo di compressione. Le opzioni dell’algoritmo per PDF sono **Nessuno**, **ZIP** e **Jpeg**; per TIFF sono **Nessuno**, **LZW**, **Jpeg** e **ZIP**; e per TIFF con Alpha sono **Nessuno**, **LZW** e **ZIP**.<br><br>Scelta **PNG**, **PNG con alfa** oppure **EPS** non fornisce opzioni aggiuntive. |
| **Nitidezza** | Seleziona **Attiva nitidezza semplice** per applicare all&#39;immagine un filtro di nitidezza di base dopo che è stata effettuata la modifica in scala. La nitidezza può contribuire a compensare la sfocatura che può verificarsi quando si visualizza un&#39;immagine con dimensioni diverse. |

#### Opzioni avanzate della scheda {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Spazio colore</strong></td>
   <td>Seleziona <strong>RGB, CMYK,</strong> o <strong>Scala di grigio</strong> per lo spazio colore.</td>
  </tr>
  <tr>
   <td><strong>Profilo colore</strong></td>
   <td>Seleziona il profilo dello spazio colore di output in cui vuoi convertire la risorsa se è diverso dal profilo di lavoro.</td>
  </tr>
  <tr>
   <td><strong>Intento di rendering</strong></td>
   <td>È possibile ignorare l'intento di rendering predefinito. Gli intenti di rendering determinano cosa succede ai colori che non possono essere riprodotti nel profilo del colore di destinazione (fuori gamma). L’Intento di rendering viene ignorato se non è compatibile con il profilo ICC.
    <ul>
     <li>Seleziona <strong>Percettivo</strong> per comprimere la gamma totale da uno spazio colore a un altro spazio colore quando uno o più colori nell'immagine originale non rientrano nella gamma dello spazio colore di destinazione.</li>
     <li>Seleziona <strong>Colorimetrico relativo</strong> quando un colore nello spazio colore corrente non rientra nella gamma nello spazio colore di destinazione. Inoltre, è possibile mapparlo al colore più vicino possibile all'interno della gamma dello spazio colore di destinazione senza influire su altri colori. </li>
     <li>Seleziona <strong>Saturazione</strong> per riprodurre la saturazione del colore dell'immagine originale durante la conversione nello spazio colore di destinazione. </li>
     <li>Seleziona <strong>Colorimetrico assoluto</strong> per abbinare i colori senza alcuna regolazione del punto bianco o del punto nero che alteri la luminosità dell'immagine.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensazione punto nero</strong></td>
   <td>Seleziona questa opzione se il profilo di output supporta questa funzione. La compensazione blackpoint viene ignorata se non è compatibile con il profilo ICC specificato.</td>
  </tr>
  <tr>
   <td><strong>Dithering</strong></td>
   <td>Selezionare questa opzione per evitare o ridurre gli artefatti di striatura del colore. </td>
  </tr>
  <tr>
   <td><strong>Tipo di nitidezza</strong></td>
   <td><p>Seleziona <strong>Nessuno</strong>, <strong>Nitidezza</strong>oppure <strong>Maschera definizione dettagli</strong>. </p>
    <ul>
     <li>Seleziona <strong>Nessuno</strong> per disattivare la nitidezza.</li>
     <li>Seleziona <strong>Nitidezza </strong>per applicare all'immagine un filtro di nitidezza di base dopo che è stata effettuata la modifica in scala. La nitidezza può contribuire a compensare la sfocatura che può verificarsi quando si visualizza un'immagine con dimensioni diverse. </li>
     <li>Seleziona<strong> Maschera definizione dettagli</strong> per ottimizzare un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Puoi controllare l’intensità dell’effetto, il raggio in pixel e una soglia di contrasto da ignorare. L’effetto utilizza le stesse opzioni del filtro “Maschera definizione dettagli” di Photoshop.</li>
    </ul> <p>In <strong>Maschera definizione dettagli</strong>, sono disponibili le seguenti opzioni:</p>
    <ul>
     <li><strong>Importo</strong> - Controlla la quantità di contrasto applicata ai pixel del bordo. Il valore predefinito del numero reale è 1,0. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5,0. Considera il valore come una misura dell'intensità del filtro.</li>
     <li><strong>Raggio</strong> - Determina il numero di pixel intorno ai pixel del bordo che influiscono sulla nitidezza. Per le immagini ad alta risoluzione, immetti un numero reale da 1 a 2. Un valore basso rende più nitidi solo i pixel del bordo; un valore elevato rende più nitida una banda più ampia di pixel. Il valore corretto dipende dalle dimensioni dell’immagine.</li>
     <li><strong>Soglia</strong> - Determina l'intervallo di contrasto da ignorare quando viene applicato il filtro Maschera definizione dettagli. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e resi più nitidi. Per evitare di introdurre rumore, prova con valori interi compresi tra 2 e 20. </li>
     <li><strong>Applica a</strong> - Determina se la nitidezza viene applicata a ogni colore o luminosità.</li>
    </ul>
    <div>
      La nitidezza è descritta in
     <a href="https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media">Utilizzo della nitidezza delle immagini con Experience Manager Dynamic Media</a> video, in <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/using/master-files/sharpening-image.html#master-files">Nitidezza di un’immagine</a> argomento della Guida in linea e <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">Best practice per la nitidezza delle immagini in Dynamic Media Classic</a> PDF scaricabile.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modalità ricampionamento</strong></td>
   <td>Seleziona una <strong>Modalità di ricampionamento</strong> opzione . Queste opzioni consentono di aumentare la nitidezza dell’immagine durante il ricampionamento verso il basso:
    <ul>
     <li><strong>Bilineare</strong> - Il metodo di ricampionamento più veloce. Alcuni artefatti di aliasing sono evidenti.</li>
     <li><strong>Bi-Cubic</strong> - Aumenta l'utilizzo della CPU ma produce immagini più nitide con artefatti di aliasing meno evidenti.</li>
     <li><strong>Sharp2</strong> - Può produrre risultati leggermente più nitidi rispetto a Bi-Cubic, ma a un costo di CPU ancora più elevato.</li>
     <li><strong>Bi-Sharp</strong> - Seleziona il ricampionamento predefinito di Photoshop per ridurre le dimensioni dell'immagine, che viene chiamato <strong>asino bicubico</strong> in Adobe Photoshop.</li>
     <li><strong>Ogni colore</strong> e <strong>Luminosità</strong> - ogni metodo può essere basato sul colore o sulla luminosità. Per impostazione predefinita <strong>Ogni colore</strong> è selezionato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Risoluzione di stampa</strong></td>
   <td>Selezionare una risoluzione per stampare l'immagine; Il valore predefinito è 72 pixel.</td>
  </tr>
  <tr>
   <td><strong>Modificatore immagine</strong></td>
   <td><p>Oltre alle impostazioni comuni dell’immagine disponibili nell’interfaccia utente, Dynamic Media supporta numerose modifiche avanzate alle immagini che è possibile specificare nel <strong>Modificatori immagine</strong> campo . Questi parametri sono definiti nella variabile <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview.html">Riferimento al comando Protocollo di Image Server</a>.</p> <p>Importante: Le seguenti funzionalità elencate nell’API non sono supportate:</p>
    <ul>
     <li>Comandi di base per il modello e il rendering del testo: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandi di localizzazione: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> non è disponibile per l'utilizzo generale.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servizi Dynamic Media non principali: SVG, Image Rendering e Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Consente di definire le opzioni del predefinito immagine con i modificatori di immagine {#defining-image-preset-options-with-image-modifiers}

Oltre alle opzioni disponibili nelle schede Base e Avanzate , è possibile definire modificatori di immagine per fornire ulteriori opzioni durante la definizione dei predefiniti per immagini. Il rendering delle immagini si basa sull’API di rendering delle immagini di Dynamic Media ed è definito in dettaglio nella sezione [Riferimento al protocollo HTTP](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction.html#image-rendering-api).

Di seguito sono riportati alcuni esempi di base delle operazioni che puoi eseguire con i modificatori di immagini.

>[!NOTE]
>
>Alcuni modificatori di immagini [non può essere utilizzato in Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html) - Inverte ogni componente colore per un effetto immagine negativo.

   ```xml {.line-numbers}
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html) - Applica un filtro di sfocatura all&#39;immagine.

   ```xml {.line-numbers}
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandi combinati - op_blur e op-invert

   ```xml {.line-numbers}
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_bright](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html) - Diminuisce o aumenta la luminosità.

   ```xml {.line-numbers}
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-luminosità](assets/6_5_imagepreset-edit-brightness.png)

* [opaca](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html) - Regola l&#39;opacità dell&#39;immagine. Consente di ridurre l’opacità in primo piano.

   ```xml {.line-numbers}
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### Modificare i predefiniti per immagini {#modifying-image-presets}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagine]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Seleziona un predefinito e quindi seleziona **[!UICONTROL Modifica]**. La **[!UICONTROL Modifica predefinito immagine]** si apre la finestra.
1. Apporta modifiche e seleziona **[!UICONTROL Salva]** per salvare le modifiche o **[!UICONTROL Annulla]** per annullare le modifiche.

### Pubblicare predefiniti per immagini {#publishing-image-presets}

I predefiniti immagine vengono pubblicati automaticamente.

### Eliminare i predefiniti per immagini {#deleting-image-presets}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale e fai clic sull’icona Strumenti .
1. Passa a **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagine]**.
1. Seleziona un predefinito, quindi seleziona **[!UICONTROL Elimina]**. Dynamic Media conferma che si desidera eliminarlo. Seleziona **[!UICONTROL Elimina]** per rimuovere o selezionare **[!UICONTROL Annulla]** per tornare ai predefiniti per immagini.
