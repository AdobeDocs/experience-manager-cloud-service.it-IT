---
title: Come gestire  [!DNL Dynamic Media]  modelli?
description: Scopri come creare  [!DNL Dynamic Media] modelli utilizzando un editor di modelli di WYSIWYG e includere più livelli di immagini, testi e forme per creare rapidamente banner e volantini e utilizzarli nelle applicazioni a valle.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 69e6b5a50f4625b9ef868216f6e44381771bf05b
workflow-type: tm+mt
source-wordcount: '3415'
ht-degree: 1%

---


# [!DNL Dynamic Media] modelli{#dynamic-media-templates}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
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

Creare modelli personalizzabili in tempo reale per banner e volantini utilizzando i modelli [!DNL Dynamic Media], un editor di modelli WYSIWYG. Pubblica il modello [!DNL Dynamic Media] e utilizzalo nelle applicazioni a valle. Un modello [!DNL Dynamic Media] include livelli immagine e testo. Aggiungi parametri ai livelli immagine e testo del modello e utilizza [[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/it/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) per riposizionare e ridimensionare il livello e aggiornarne il contenuto in tempo reale.

Alcune delle caratteristiche principali includono:

* **[!DNL Dynamic Media]Editor modelli WYSIWYG:** Creare banner personalizzabili con livelli immagine e testo.
* **Parametrizzazione livello:** Definisci coppie chiave-valore dinamiche per i livelli per abilitare gli aggiornamenti in tempo reale.
* Supporto URL **[!DNL Dynamic Media]:** Utilizza [!DNL Dynamic Media] URL per i modelli, integrando valori personalizzati da applicazioni di prima parte o di terze parti.
* **Controllo visibilità livello:** nascondere o mostrare dinamicamente i livelli in base alle esigenze.
* **Ridimensionamento automatico del testo:** Adatta automaticamente le dimensioni del testo alle aree designate.

Alcuni dei vantaggi principali dei modelli [!DNL Dynamic Media] includono:

* **Ottimizzare 1:1 Personalization:** Personalizzare il contenuto ai segnali dei clienti in tempo reale.
* **Riduzione dello sforzo manuale:** Automatizzazione e accelerazione della creazione e della gestione dei contenuti.
* **Assicurare Esperienze omnicanale coerenti:** Mantenere la coerenza del brand tra i canali.
* **Riutilizzare il contenuto in modo efficace:** evitare contenuti monouso e scalare con modelli dinamici con parametri.
* **Riduci rischi:** Aggiorna prezzi, sconti e collegamenti in tempo reale.
* **Migliora il coinvolgimento dei clienti:** esperienze interattive e contestualmente rilevanti.

>[!NOTE]
>
>I clienti con abbonamenti allo SKU Sicurezza avanzata non possono utilizzare alcuna funzionalità [!DNL Dynamic Media], inclusi i modelli [!DNL Dynamic Media], in tale programma Cloud Services.

Scopri come creare un modello [!DNL Dynamic Media] passo dopo passo in questo video.
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Prima di iniziare{#prerequisites-for-dynamic-media-wysiwyg-template}

Soddisfare i seguenti requisiti per creare un modello [!DNL Dynamic Media] e generarne l&#39;URL di consegna:

1. Accesso a [!DNL Dynamic Media].
1. Nella home page di [!DNL Assets View] è presente una cartella in **[!UICONTROL Dynamic Media Assets]** per salvare il modello. [Crea una cartella](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets &#x200B;]**&#x200B;per replicare tale cartella in&#x200B;**[!UICONTROL &#x200B; Dynamic Media Assets &#x200B;]**.
1. [Sincronizza le immagini disponibili nell&#39;istanza  [!DNL AEM Assets] con [!DNL Dynamic Media] per utilizzarle per creare il modello](/help/assets/dynamic-media/config-dm.md).
1. Pubblica le immagini da utilizzare per creare il modello per generare l’URL di consegna del modello dopo averlo creato. L’URL di consegna può essere utilizzato nelle applicazioni a valle.
1. Per utilizzare un tipo di carattere diverso da quello predefinito di [!UICONTROL Adobe Sans F2] nel livello testo del modello, [carica e pubblica il file del tipo di carattere in AEM e Dynamic Media simultaneamente](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation). [I formati di file dei caratteri supportati sono AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Assicurati inoltre di [rielaborare](/help/assets/reprocessing-assets-view.md) i font esistenti per utilizzarli. Per ulteriori informazioni, vedere [Tipi di carattere](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/support-files/fonts).<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. verifica quanto segue nell’interfaccia utente touch:
   * Nella pagina **[!UICONTROL Modifica configurazione [!DNL Dynamic Media]]**, la modalità di sincronizzazione **[!UICONTROL [!DNL Dynamic Media]]** impostata su **[!UICONTROL Disabilitata per impostazione predefinita]** non è applicata a tutte le cartelle di AEM (**[!UICONTROL Sincronizza tutto il contenuto]** non è selezionata). Per ulteriori informazioni, vedere [configurazione di Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md).
   * La modalità di sincronizzazione **[!UICONTROL [!DNL Dynamic Media]]** è impostata su **[!UICONTROL Abilita per le sottocartelle]** per la cartella o sottocartella di destinazione in cui verrà salvato il modello dopo la creazione. Per ulteriori informazioni, vedere [configurazione [!DNL Dynamic Media] di Cloud Service](/help/assets/dynamic-media/config-dm.md).

## Crea modello [!DNL Dynamic Media]{#how-to-create-dynamic-media-template}

Eseguire la procedura seguente per creare un modello [!DNL Dynamic Media]:
<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->
1. [Creare un’area di lavoro vuota](#create-a-canvas)
1. [Aggiungere immagini all’area di lavoro](#add-images-to-the-canvas)
1. [Aggiungere livelli di testo all&#39;area di lavoro](#add-text-to-the-canvas)
1. [Aggiungere forme all&#39;area di lavoro](#add-shapes-to-the-canvas)
1. [Modificare o eliminare un livello](#edit-or-delete-a-layer)
1. [Livelli parametrizzati](#parameterise-a-layer)

### Creare un’area di lavoro vuota{#create-a-canvas}

Per creare un’area di lavoro vuota, effettua le seguenti operazioni:

1. Passa a [!DNL Assets View], seleziona **[!UICONTROL Dynamic Media Assets]** disponibile nel pannello a sinistra e passa alla cartella per salvare il modello in tale cartella.

   ![Modelli Dynamic Media](/help/assets/assets/DM-Assets1.png)

1. Seleziona **[!UICONTROL Crea modello]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Nuovo modello]**.
   ![come creare modelli dinamici personalizzabili in tempo reale](/help/assets/assets/new-template.png)
   >[!NOTE]
   >
   >  Il modello viene salvato nel percorso in cui è stato creato. Nella home page di [!DNL Assets View], seleziona **[!UICONTROL Dynamic Media Assets]** e fai clic su **[!UICONTROL Crea modello]** per salvare il modello nella cartella principale di **[!UICONTROL Dynamic Media Assets]**.

1. Specifica un nome di modello, definisci la larghezza e l&#39;altezza dell&#39;area di lavoro e fai clic su **[!UICONTROL Crea]**. Viene visualizzata un&#39;area di lavoro vuota con opzioni di menu su entrambi i lati da utilizzare per la creazione del modello. Passa il puntatore del mouse sulle opzioni del menu per visualizzarne la descrizione comando.
   ![modello personalizzabile in tempo reale](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > L&#39;intervallo consentito di larghezza e altezza è compreso tra 50 e 5000.

**Opzioni di menu nel riquadro di destra:** Utilizzare queste opzioni per aggiungere all&#39;area di lavoro le immagini e i livelli di testo necessari.

* ![Modelli DM](/help/assets/assets/add-image.svg): fare clic per aggiungere immagini all&#39;area di lavoro.
* ![modelli personalizzabili](/help/assets/assets/add-text.svg): fare clic per aggiungere testi all&#39;area di lavoro.
* ![modelli personalizzabili](/help/assets/assets/show-layers-list.svg): fare clic per visualizzare l&#39;elenco di tutti i livelli (immagine e testo) nell&#39;area di lavoro. Ogni immagine e testo aggiunti all’area di lavoro viene rappresentato come un livello separato.

**Opzioni di menu nel riquadro di sinistra:** Utilizzare queste opzioni per le seguenti azioni comuni dell&#39;editor.

* ![Modelli DM](/help/assets/assets/layer-selector.svg): seleziona ![Modelli DM](/help/assets/assets/layer-selector.svg) e fai clic su un livello nell&#39;area di lavoro per selezionarlo.
* ![modelli che supportano la personalizzazione](/help/assets/assets/bring-forward.svg): fare clic su ![modelli che supportano la personalizzazione](/help/assets/assets/bring-forward.svg) o utilizzare la scelta rapida da tastiera, **Ctrl** + **&rbrack;** (Windows) o **Cmd** + **&rbrack;** (Mac) per portare avanti un livello selezionato.
* ![come creare un modello che possa essere personalizzato facilmente](/help/assets/assets/send-backward.svg): fare clic su ![come creare un modello che possa essere personalizzato facilmente](/help/assets/assets/send-backward.svg) o utilizzare la scelta rapida da tastiera, **Ctrl** + **&lbrack;** (Windows) o **Cmd** + **&lbrack;** (Mac) per inviare indietro un livello selezionato.
* ![crea un modello personalizzabile all&#39;istante](/help/assets/assets/undo.svg): fai clic su ![crea un modello personalizzabile all&#39;istante](/help/assets/assets/undo.svg) oppure usa la scelta rapida da tastiera, **Ctrl** + **Z** (Windows) o **Cmd** + **Z** (Mac) per annullare l&#39;ultima azione.
* ![modello per creare rapidamente i banner](/help/assets/assets/redo.svg): fare clic su ![modello per creare rapidamente i banner](/help/assets/assets/redo.svg) oppure utilizzare la scelta rapida da tastiera **Ctrl** + **Y** (Windows) o **Cmd** + **Y** (Mac) per ripetere l&#39;ultima azione.
* ![modello per creare rapidamente i volantini](/help/assets/assets/zoom-in.svg): fare clic su ![modello per creare rapidamente i volantini](/help/assets/assets/zoom-in.svg) oppure utilizzare la scelta rapida da tastiera **Ctrl** + **+** (Windows) o **Cmd** + **+** (Mac) per ingrandire l&#39;area di lavoro.
* ![modello per creare rapidamente i banner](/help/assets/assets/Zoom-out.svg): fai clic su ![modello per creare rapidamente i banner](/help/assets/assets/Zoom-out.svg) oppure utilizza la scelta rapida da tastiera, **Ctrl** + **-** (Windows) o **Cmd** + **-** (Mac) per ridurre l&#39;area di lavoro.
* Premi **backspace** o **delete** per eliminare il livello selezionato se non si sta modificando testo o proprietà.

Fai clic su ![modello per creare rapidamente i volantini](/help/assets/assets/show-layers-list.svg) e seleziona altre opzioni (![](/help/assets/assets/three-dots.svg)) sul livello Area di lavoro per modificare le dimensioni dell&#39;area di lavoro in qualsiasi momento durante la creazione del modello.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> I modelli consentono un massimo di 20 livelli, incluso Canvas.

### Aggiungere immagini all’area di lavoro{#add-images-to-the-canvas}

Per aggiungere immagini all’area di lavoro, effettua le seguenti operazioni:

1. Fai clic su ![crea un banner in poco tempo](/help/assets/assets/add-image.svg) per aprire il pannello [Selettore risorse](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). Nel pannello vengono visualizzate le immagini dell&#39;istanza AEM Assets sincronizzate con [!DNL Dynamic Media].
1. Sfoglia il pannello o usa le parole chiave nella barra di ricerca per trovare un’immagine specifica.
1. Trascina e rilascia un’immagine nell’area di lavoro per utilizzarla. Vedere il [**[!UICONTROL pannello Proprietà]**](#reposition-resize-delete-a-layer) per ridimensionare o riposizionare un livello nell&#39;area di lavoro.
   ![crea un banner in pochi secondi](/help/assets/assets/add-image-to-canvas.png)
1. Attiva l&#39;interruttore **[!UICONTROL Raggio uniforme]** e utilizza il cursore **[!UICONTROL Raggio angolo]** per regolare uniformemente la rotondità di tutti e quattro gli angoli di un&#39;immagine. Disattivate l&#39;interruttore per personalizzare la rotondità degli angoli assegnando valori di raggio specifici a ciascun angolo.
   ![regola la rotondità degli angoli dell&#39;immagine](/help/assets/assets/enable-uniform-radius-image.png)

### Aggiungere livelli di testo all&#39;area di lavoro{#add-text-to-the-canvas}

Per aggiungere livelli di testo all’area di lavoro, effettua le seguenti operazioni:

1. Fai clic su ![creazione rapida di nuovi banner](/help/assets/assets/add-text.svg) per aggiungere un livello di testo all&#39;area di lavoro e aprire il pannello Proprietà.
1. Selezionate il livello e fate clic sul testo per aggiornarlo.
1. Selezionare **[!UICONTROL Ridimensionamento automatico del testo]** nel pannello Proprietà per regolare automaticamente la lunghezza del testo e la dimensione del font in modo che si adattino in modo ottimale all&#39;area designata.
   ![banner meglio personalizzabili](/help/assets/assets/add-text-layer.png)

Vedere il [**[!UICONTROL pannello Proprietà]**](#reposition-resize-delete-a-layer) per riposizionare, ridimensionare, ruotare o eliminare il livello. Formatta il testo con il font, le dimensioni, il colore, lo stile e l&#39;allineamento richiesti (nel livello) modificandone i valori nei rispettivi campi nella sezione **[!UICONTROL Testo]** del pannello. Nel campo **[!UICONTROL Famiglia di caratteri]** sono visualizzati il tipo di carattere predefinito [!UICONTROL Adobe Sans F2], i tipi di carattere esistenti rielaborati e i tipi di carattere appena caricati e pubblicati. Per ulteriori informazioni, vedere il punto 5 della sezione [Prima di iniziare](#prerequisites-for-dynamic-media-wysiwyg-template).

### Aggiungere forme all&#39;area di lavoro {#add-shapes-to-the-canvas}

Per aggiungere forme all&#39;area di lavoro, eseguire la procedura seguente:

1. Fare clic su ![creazione forme](/help/assets/assets/Shapes.svg), selezionare una forma (rettangolo o cerchio) per aggiungerla all&#39;area di lavoro. Utilizzare il [[!UICONTROL pannello Proprietà]](#reposition-resize-delete-a-layer) della forma per riposizionare, ridimensionare, ruotare o eliminare il livello.
1. Scorri fino alla sezione **[!UICONTROL Stile]** del pannello, definisci un codice esadecimale nel campo **[!UICONTROL Colore forma]** o utilizza il selettore colore per riempire il colore nella forma selezionata.
1. Attiva l&#39;interruttore **[!UICONTROL Raggio uniforme]** e utilizza il cursore **[!UICONTROL Raggio angolo]** per regolare uniformemente la rotondità di tutti e quattro gli angoli del rettangolo. Disattivate l&#39;interruttore per personalizzare la rotondità degli angoli assegnando valori di raggio specifici a ciascun angolo.
   ![regolare la rotondità degli angoli delle forme](/help/assets/assets/enable-uniform-radius-shape.png)
1. [Aggiungi il parametro **[!UICONTROL Nascondi]** al livello selezionato](#parameterise-a-layer) per mostrare o nascondere il livello nel modello in tempo reale utilizzando l&#39;URL del modello.
1. Selezionare il livello per [aggiungervi un collegamento [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates), consentendo agli utenti di fare clic sulla forma come collegamento ipertestuale nel modello attivo.

### Modificare o eliminare un livello {#edit-or-delete-a-layer}

Per modificare o eliminare un livello area di lavoro, esegui la procedura seguente:

1. Fare clic su ![modelli con supporto per aggiornamenti dinamici](/help/assets/assets/show-layers-list.svg) e selezionare il livello nell&#39;area di lavoro o nell&#39;elenco Livelli.
1. Fai clic su **[!UICONTROL altre opzioni]** (![modelli con supporto per aggiornamenti in tempo reale](/help/assets/assets/three-dots.svg)) per modificare o eliminare il livello.
1. Fai clic su **[!UICONTROL Elimina]** per eliminare il livello.
1. Fai clic su **[!UICONTROL Modifica]** per modificare il livello utilizzando il [**[!UICONTROL pannello Proprietà]**](#reposition-resize-delete-a-layer).
   ![creazione rapida banner](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Pannello Proprietà{#properties-panel}

Il pannello [!UICONTROL Proprietà] include sezioni per [riposizionare](#reposition-resize-delete-a-layer), [ridimensionare](#reposition-resize-delete-a-layer) e [ruotare](#reposition-resize-delete-a-layer) un livello.  Fornisce inoltre opzioni di riempimento colore per [livelli forma](#add-shapes-to-the-canvas), [opzioni di formattazione testo](#text-formatting-options-on-properties-panel) per [livelli testo](#add-text-to-the-canvas) e un&#39;opzione per [aggiungere un collegamento [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates) a qualsiasi livello selezionato.
Per passare al pannello delle proprietà di un livello, fai clic su ![Creazione rapida contenuto](/help/assets/assets/show-layers-list.svg) e seleziona il livello dall&#39;elenco per visualizzare il relativo pannello [!UICONTROL Proprietà].

![creazione rapida dei contenuti](/help/assets/assets/properties-panel.png)

Dal pannello [!UICONTROL Proprietà] di un livello, seleziona un altro livello nell&#39;area di lavoro per passare al relativo pannello [!UICONTROL Proprietà].

#### Riposizionare, ridimensionare, ruotare o eliminare un livello{#reposition-resize-delete-a-layer}

Per modificare un livello testo o immagine, consulta le seguenti azioni di modifica dei livelli comuni:

* **Riposizionare il livello:** Trascinare il livello per spostarlo in qualsiasi punto dell&#39;area di lavoro. Questa azione aggiorna i valori X e Y nel pannello delle proprietà. X e Y sono le coordinate del centro del livello sul piano dell&#39;area di lavoro.
* **Ridimensiona il livello:** Seleziona il livello e trascina i relativi quadratini di ridimensionamento per ridimensionarlo. Questa azione aggiorna i valori W (larghezza) e H (altezza) nel pannello delle proprietà.
* **Ruotare il livello:** Trascinare la maniglia quadrata posizionata verticalmente sopra il livello per ruotarlo intorno al centro. Questa azione aggiorna i valori degli angoli nel pannello delle proprietà.
* **Eliminare il livello:** Premere **Backspace** o **delete** e quindi fare clic su **[!UICONTROL Confirm]** per eliminare il livello selezionato.

#### Opzioni di formattazione del testo{#text-formatting-options-on-properties-panel}

Formatta il testo con il carattere, le dimensioni, il colore, lo stile e l&#39;allineamento richiesti (all&#39;interno del livello) modificandone i valori nei rispettivi campi nella sezione **[!UICONTROL Testo]** del pannello.
Assicurarsi di includere **[!UICONTROL Ridimensionamento testo avanzato]**. [!UICONTROL Smart Text Resize] funziona sull&#39;algoritmo [Copyfit](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) per riempire in modo ottimale il testo nell&#39;area di testo, impedisce l&#39;overflow del testo e riduce al minimo lo spazio in eccesso nella parte inferiore del testo.

![creazione contenuto in pochissimo tempo](/help/assets/assets/smart-text-resize.png)

### Livelli parametrizzati {#parameterise-a-layer}

Dopo aver creato un modello con più livelli di immagini, testi e forme, impostate i parametri per i livelli selezionati. Quando un livello o la relativa proprietà sono parametrizzati, ottiene una coppia chiave-valore (detta anche parametro). Questo parametro può essere incluso nell’URL del modello per aggiornare la posizione, le dimensioni o il contenuto del livello in tempo reale, con conseguente personalizzazione del modello in un attimo.

Per parametrizzare un livello:

1. fai clic su ![creazione immediata contenuto](/help/assets/assets/show-layers-list.svg), seleziona un livello e fai clic su **[!UICONTROL Parametri]**. Viene visualizzato il pannello **[!UICONTROL Parametri]**.
1. Attiva **[!UICONTROL Includi parametro]** per parametrizzare una proprietà. Per informazioni sul comportamento della proprietà dopo la parametrizzazione, vedere l&#39;opzione [Parametri del pannello](#parameterisation-options-or-allowed-parameters).
1. **Facoltativo:** Rinominare il nome del parametro. Il nome di un parametro è seguito da un suffisso. Per un livello selezionato, tutte le relative proprietà con parametri condividono lo stesso nome di livello seguito da un suffisso variabile. Rinominate il nome del livello seguendo la convenzione di denominazione semantica in modo che, quando includete il parametro nell&#39;URL, il nome del parametro spieghi da solo il contenuto o lo scopo del livello.
1. Fai clic su **[!UICONTROL Salva]**.
   ![creazione immediata dei contenuti](/help/assets/assets/parameterise-a-layer.png)
Per passare dal pannello Parametri di un&#39;immagine al livello testo, selezionare il livello nell&#39;area di lavoro e fare clic su **[!UICONTROL Parametri]**.

#### Opzione del pannello Parametri {#parameterisation-options-or-allowed-parameters}

Le proprietà con parametri possono essere incluse come parametri URL nell’URL del modello per modificare il modello in tempo reale utilizzando l’URL.

**Parametri immagine:**

**[!UICONTROL X]:** Includere per spostare il livello orizzontalmente lungo la sua linea centrale, parallelamente all&#39;asse X del piano del modello, modificando il valore del parametro nell&#39;URL.
**[!UICONTROL Y]:** Includere per spostare il livello verticalmente lungo la sua linea centrale, parallelamente all&#39;asse Y del piano del modello, modificando il valore del parametro nell&#39;URL.
**[!UICONTROL Larghezza]:** Includere per regolare la larghezza del livello modificando il valore del parametro nell&#39;URL.
**[!UICONTROL Altezza]:** Includere per regolare l&#39;altezza del livello modificando il valore del parametro nell&#39;URL.
**[!UICONTROL Nascondi]:** Includi per nascondere o mostrare il livello nel modello utilizzando 0 (mostra) e 1 (nascondi).
**[!UICONTROL Source]:** Includi per sostituire l&#39;immagine del livello con una nuova immagine modificando il percorso dell&#39;immagine nel valore del parametro nell&#39;URL.

**Parametri di formattazione del testo:**

Includi i seguenti parametri per modificare il testo, il relativo font, colore e dimensione, dall’URL aggiornando i valori dei parametri nell’URL.

**[!UICONTROL Testo]:** Includere per aggiornare il testo dall&#39;URL.
**[!UICONTROL Famiglia di caratteri]:** Includere per aggiornare il carattere del testo dall&#39;URL.
**[!UICONTROL Dimensione font]:** Includere per aggiornare la dimensione font del testo dall&#39;URL.
**[!UICONTROL Colore testo]:** Includere per aggiornare il colore del carattere del testo dall&#39;URL.

### Raggruppare i livelli per controllarne contemporaneamente la visibilità{#group-layers}

Un altro modo per mantenere flessibili i modelli consiste nell&#39;utilizzare un singolo nome di parametro per controllare più livelli. Questa strategia è utile per il parametro di visibilità (nascondi o mostra livelli), per aggiornare la progettazione o gli elementi grafici da un singolo modello.

Segui questi passaggi per assegnare lo stesso nome ai parametri [!UICONTROL Nascondi] (![creazione rapida contenuto](/help/assets/assets/Visibility-icon.svg)) di più livelli, consentendo di nasconderli o visualizzarli contemporaneamente.

1. Passa al [**[!UICONTROL pannello Proprietà]**](#parameterise-a-layer) di un livello.
1. Attiva/disattiva il parametro **[!UICONTROL Nascondi]** se non è già stato impostato in precedenza come parametro.
1. **Facoltativo:** Rinomina il parametro **[!UICONTROL Nascondi]**.
1. Copia il nome del parametro **[!UICONTROL Nascondi]**.
1. Passa al pannello Parametri degli altri livelli selezionandoli dall&#39;area di lavoro e, se non sono parametrizzati, imposta il parametro **[!UICONTROL Nascondi]**.
1. Sostituisci il nome del **[!UICONTROL parametro]** con il nome copiato.
1. Fai clic su **[!UICONTROL Salva]** per raggruppare i livelli.
1. Eseguire i passaggi 3 e 4 nella sezione [**[!UICONTROL Anteprima e pubblicazione]**](#preview-and-publish-template-and-copy-template-deliver-url) per visualizzare le modifiche.

## Anteprima e pubblicazione del modello per copiare l’URL di consegna{#preview-and-publish-template-and-copy-template-deliver-url}

Per visualizzare in anteprima e pubblicare il modello e copiare l’URL di consegna, effettua le seguenti operazioni:

1. Nella pagina dell&#39;area di lavoro fare clic su **[!UICONTROL Anteprima]**. È inoltre possibile passare alla **[!UICONTROL visualizzazione Assets]** **>** **[!UICONTROL Assets Dynamic Media]** **>** trovare e selezionare il modello **>** fare clic su **[!UICONTROL Modifica modello]** **>** fare clic su **[!UICONTROL Anteprima]**. Nella pagina di anteprima vengono visualizzati il modello, i relativi parametri (livelli e proprietà con parametri), lo stato di pubblicazione e l&#39;opzione **[!UICONTROL Pubblica]**.
1. Seleziona i parametri dal pannello **[!UICONTROL Parametri modello]** per modificarne i valori e aggiornare immediatamente il contenuto, le dimensioni, la posizione o la formattazione del testo del livello del modello corrispondente nell&#39;anteprima. Ad esempio:
   1. Selezionare un livello di testo e modificarne il testo oppure
   1. Seleziona un livello immagine, fai clic su ![creazione rapida di contenuto](/help/assets/assets/add-image.svg), seleziona un&#39;immagine dal selettore risorse, quindi fai clic su **[!UICONTROL Aggiorna]**.

   Il modello viene aggiornato immediatamente, visualizzando il testo modificato e sostituendo l’immagine precedente con quella nuova. Inoltre, il valore del parametro immagine riflette il nuovo percorso immagine. Analogamente, potete ridimensionare un livello regolandone i valori e le modifiche vengono applicate al modello in tempo reale.
1. Selezionare dall&#39;elenco il parametro **[!UICONTROL Nascondi]** per [livelli raggruppati](#group-layers) per mostrarli o nasconderli nel modello.
1. **Facoltativo:** Modificare il valore del parametro **[!UICONTROL Hide]** tra 0 e 1 e fare clic su **[!UICONTROL Aggiorna]** per visualizzare le modifiche. I livelli con lo stesso parametro **[!UICONTROL Hide]** vengono nascosti o visualizzati insieme. Allo stesso modo, potete controllare la visibilità dei livelli dall&#39;URL.

   ![creazione rapida di contenuti](/help/assets/assets/dm-templates-publish-status.png)
Puoi anche attivare **[!UICONTROL Includi tutti i parametri]** per modificare tutti i valori dei parametri visualizzati e visualizzare gli aggiornamenti nell&#39;anteprima del modello.
   <br>
1. Per pubblicare il modello dalla pagina di anteprima, fai clic su **[!UICONTROL Pubblica]** e conferma la pubblicazione. Viene visualizzato un messaggio di **[!UICONTROL Pubblicazione completata]** e lo stato di pubblicazione viene aggiornato a **[!UICONTROL Pubblicato]**.

### Copiare l’URL di consegna

I parametri selezionati nella pagina **[!UICONTROL Anteprima]** diventano i parametri URL nell&#39;URL del modello.

Assicurati che le immagini nel modello siano già pubblicate in AEM e Dynamic Media per generare l’URL di consegna del modello.

Per copiare l’URL di consegna del modello, effettua le seguenti operazioni:

1. Fare clic su **[!UICONTROL Copia URL]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Copia URL]**. Seleziona e copia l’URL visualizzato. Il primo parametro nell&#39;URL inizia dopo un punto interrogativo **([!UICONTROL ?])** e una coppia chiave-valore iniziano con **[!UICONTROL $]** e terminano con **[!UICONTROL &amp;]**. La chiave e il valore sono separati da un segno di uguale **([!UICONTROL =])**, con la chiave a sinistra e il valore a destra.
1. Incolla questo URL nella scheda del browser e visualizza il modello live. Personalizza il modello in tempo reale aggiornando il valore del parametro richiesto (valore della chiave) nell&#39;URL direttamente come mostrato nel [passaggio 2](#preview-and-publish-template-and-copy-template-deliver-url) della sezione **Anteprima e pubblicazione**.
1. Utilizza questo URL per accelerare il merchandising dei tuoi prodotti o servizi. Puoi condividere questo URL con i clienti o integrarlo nel tuo sito web o in qualsiasi applicazione di terze parti a valle per visualizzare il banner e aggiornarlo in tempo reale per riflettere le offerte in corso.

## Aggiornamenti in tempo reale al modello dall’URL{#update-the-template-from-the-url}

Modificare i parametri direttamente nell’URL può essere noioso. Per semplificare:

1. Copia l’URL e incollalo in un blocco note.
1. Utilizzare Cmd+F (Mac) o Ctrl+F (Windows) per trovare e modificare i valori dei parametri. Ad esempio:
   * Trova e sostituisci i percorsi immagine per i livelli immagine.
   * Trova le coordinate [con parametri](#parameterise-a-layer) del livello, larghezza e altezza, per regolarne i valori.
   * Modificare testo, font, colore, dimensione o allineamento per i livelli di testo.
   * Modificate i valori di visibilità compresi tra 0 e 1.

Incolla questo URL aggiornato nel browser per visualizzare le modifiche.

## Modifica il modello{#edit-the-template}

Modifica il modello seguendo questi passaggi:

1. In [!DNL Assets view], fai clic su **[!UICONTROL Dynamic Media Assets]**.
2. Passa alla posizione del modello.
3. Seleziona il modello.
4. Fare clic su **[!UICONTROL Modifica modello]**. Nell&#39;area di lavoro del modello vengono visualizzati il modello e l&#39;elenco di tutti i relativi livelli nel pannello Livelli. Inizia a modificare il modello in base alle tue esigenze.

## Aggiungere un collegamento Call to action (CTA) al livello del modello{#add-CTA-in-dynamic-media-templates}

Trasforma qualsiasi livello immagine, testo o forma del modello [!DNL Dynamic Media] in un collegamento ipertestuale aggiungendo un collegamento CTA che indirizza gli utenti a una pagina di destinazione.

Per aggiungere un collegamento CTA a un livello, effettuate le seguenti operazioni:

1. Passa alla posizione del modello, seleziona il modello e fai clic su ![modifica](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL Modifica modello]**. Il modello viene visualizzato nell’area di lavoro.
1. Seleziona il livello del modello e [passa al relativo pannello delle proprietà](#edit-or-delete-a-layer) per aggiungervi un collegamento CTA.
1. Nel pannello delle proprietà, seleziona **[!UICONTROL Aggiungi CTA]**, specifica l&#39;URL di destinazione nel campo **[!UICONTROL URL]** e fai clic su **[!UICONTROL Salva]**.

   ![aggiungi CTA](/help/assets/assets/add-cta.png)

1. Fai clic su **[!UICONTROL Anteprima]** e seleziona **[!UICONTROL Pubblica]** per pubblicare il modello, se non già pubblicato in precedenza.
1. Passa alla cartella in cui è stato salvato il modello, selezionalo e fai clic su ![pagina dettagli](/help/assets/assets/details-page-icon.svg) **[!UICONTROL Dettagli]**.
1. Fai clic su **[!UICONTROL Opzioni copia]** e seleziona **[!UICONTROL Copia codice di incorporamento]**. Assicurarsi di pubblicare le immagini modello in [!DNL AEM and Dynamic Media] per copiare il codice da incorporare.

   ![copia codice da incorporare](/help/assets/assets/copy-options1.png)

   Di seguito è riportato un esempio di codice da incorporare:

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. Aggiungi il codice da incorporare copiato al file HTML del sito ed eseguilo nel browser per visualizzare il modello.

Fai clic sull’elemento CTA sul modello per passare alla pagina di destinazione.

Guarda questo video passo per passo per scoprire come aggiungere un collegamento CTA a un livello di modello.

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## Punti importanti da notare {#important-points-to-note}

* Dopo aver creato un modello con livelli immagine con parametri per gli aggiornamenti dinamici, assicuratevi che le immagini destinate agli aggiornamenti futuri condividano le stesse dimensioni delle immagini con parametri. In questo modo le immagini si adattano perfettamente ai livelli senza traboccare o lasciare spazi vuoti. Attualmente, il modello non supporta le regolazioni automatiche delle quote per adattare le immagini ai livelli.
* Non è disponibile alcun supporto per sottostringhe in un livello di testo. L’utente non può applicare proprietà di font diverse alla sottostringa di un livello di testo.
* Il supporto di più società [!DNL Dynamic Media] non è attualmente disponibile con [!DNL Dynamic Media] modelli.
* In caso di copia o spostamento, il selettore di destinazione mostra tutte le cartelle (incluse le cartelle non sincronizzate [!DNL Dynamic Media]). Inoltre, attualmente non visualizza le risorse Modello [!DNL Dynamic Media] (entrambe queste sono limitazioni del selettore di destinazione).
* Qualsiasi operazione di aggiornamento su una cartella (ad esempio, Pubblica o Elimina) da Assets influisce sui modelli [!DNL Dynamic Media] disponibili in tale cartella.
* Il cestino non funziona per i modelli [!DNL Dynamic Media]. Se una risorsa viene spostata nel cestino e quindi ripristinata, viene ripristinata in AEM ma non in [!DNL Dynamic Media]. Lo stesso vale per i modelli [!DNL Dynamic Media].

## Consulta anche

1. Esplora [[!DNL Dynamic Media]  e le relative funzionalità](/help/assets/dynamic-media/dynamic-media.md)
1. Esplora [[!DNL Dynamic Media] con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)