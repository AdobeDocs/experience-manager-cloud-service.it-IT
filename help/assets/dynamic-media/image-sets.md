---
title: Set di immagini
description: Scopri come utilizzare i set di immagini in Dynamic Medie.
contentOwner: Rick Brough
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 5%

---

# Set di immagini {#image-sets}

I set di immagini offrono agli utenti un&#39;esperienza di visualizzazione integrata, in cui gli utenti possono visualizzare diverse visualizzazioni di un elemento facendo clic su un&#39;immagine di anteprima. I set di immagini consentono di presentare viste alternative di un elemento e il visualizzatore offre strumenti di zoom per esaminare da vicino le immagini.

I set di immagini sono indicati da un banner con la parola `IMAGESET`. Inoltre, se il set di immagini è pubblicato, la data di pubblicazione, indicata dalla **[!UICONTROL Mondo]** sul banner. Inoltre, la data dell’ultima modifica, indicata dalla **[!UICONTROL Matita]** viene visualizzata l&#39;icona.

![chlimage_1-133](assets/chlimage_1-339.png)

All&#39;interno del set di immagini, potete anche creare dei campioni creando un set di immagini e aggiungendo delle miniature.

Questa applicazione è utile quando si desidera visualizzare un elemento con un colore, un motivo o una finitura diversi. Per creare un set di immagini con campioni di colore, è necessario disporre di un&#39;immagine per ogni colore, motivo o finitura da presentare agli utenti. È inoltre necessario un campione di colore, motivo o finitura per ciascun colore, motivo o finitura.

Si supponga, ad esempio, di voler presentare immagini di maiuscole con distinte di colore diverso, ovvero rosso, verde e blu. In questo caso, sono necessari tre scatti dello stesso tappo. Serve un colpo con un rosso, uno con un verde e uno con un conto blu. È inoltre necessario un campione di colore rosso, verde e blu. I campioni colore fungono da miniature su cui l’utente fa clic nel Visualizzatore set di campioni per visualizzare il cappuccio con fattura rossa, fattura verde o fattura blu.

>[!NOTE]
>
>Per informazioni sull’interfaccia utente di Assets, consulta [Gestire le risorse con l’interfaccia utente touch](/help/assets/manage-digital-assets.md).

Quando crei un set di immagini, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| Numero di risorse duplicate per set | Nessun duplicato | 20 |
| Numero massimo di immagini per set | 5-10 immagini per set | 1000 |

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/dynamic-media/limitations.md).

## Guida introduttiva: Set di immagini {#quick-start-image-sets}

Per iniziare subito a utilizzare il prodotto:

1. Facoltativo. [Creare un predefinito per set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md) e applicarlo a una nuova cartella in cui vengono caricate le immagini del set 360 gradi.

   Un predefinito per set di batch consente di automatizzare la creazione del set di immagini.

   >[!IMPORTANT]
   >
   >I set di batch vengono creati dall’IPS (Image Production System) come parte dell’inserimento delle risorse.

1. [Carica le immagini sorgente principali per più viste](#uploading-assets-in-image-sets).

   Carica le immagini per i set di immagini. Gli utenti possono ingrandire le immagini nel Visualizzatore set di immagini. Scegliere quindi con attenzione le immagini. Assicurati che le dimensioni delle immagini siano di almeno 2000 pixel.

   Consulta [Dynamic Medie - Formati di immagine raster supportati](/help/assets/file-format-support.md#image-support-dynamic-media) per un elenco di formati supportati dai set di immagini.

1. [Crea set di immagini](#creating-image-sets).

   In Set di immagini, gli utenti possono fare clic su immagini in miniatura nel Visualizzatore set di immagini.

   Per creare un set di immagini in Assets, seleziona **[!UICONTROL Crea]** > **[!UICONTROL Set di immagini]**. Quindi, aggiungi le immagini e fai clic su **[!UICONTROL Salva]**.

   Consulta [Preparare le risorse del set di immagini per il caricamento e il caricamento dei file](#uploading-assets-in-image-sets).

   Consulta [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

1. Aggiungi [Predefiniti visualizzatore set immagini](/help/assets/dynamic-media/managing-viewer-presets.md), in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore set di immagini. Per visualizzare il set di immagini con un predefinito visualizzatore, seleziona il set di immagini e, nell’elenco a discesa della barra a sinistra, seleziona **[!UICONTROL Visualizzatori]**.

   Per creare o modificare i predefiniti visualizzatore, vedi **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti visualizzatore]**.

1. (Facoltativo) [Visualizza set di immagini](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) create utilizzando predefiniti per set di batch.
1. [Anteprima set immagini](/help/assets/dynamic-media/previewing-assets.md).

   Seleziona il set di immagini e puoi visualizzarlo in anteprima. Per esaminare il set di immagini nel visualizzatore selezionato, seleziona le icone delle miniature. È possibile scegliere visualizzatori diversi da **[!UICONTROL Visualizzatori]** disponibile dall’elenco a discesa della barra a sinistra.

1. [Pubblica set di immagini](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Quando si pubblica un set di immagini, vengono attivati l’URL e la stringa di incorporamento. Inoltre, devi [pubblicare un predefinito visualizzatore personalizzato](/help/assets/dynamic-media/managing-viewer-presets.md) creato. I predefiniti visualizzatore predefiniti sono già pubblicati.

1. [Collegare gli URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [Incorporare il visualizzatore di video o immagini](/help/assets/dynamic-media/embed-code.md).

   Experience Manager Assets crea chiamate URL per i set di immagini e li attiva dopo la pubblicazione dei set di immagini. Puoi copiare questi URL quando visualizzi in anteprima le risorse. In alternativa, puoi incorporarli sul tuo sito web.

   Seleziona il set di immagini, quindi seleziona nell’elenco a discesa della barra a sinistra **[!UICONTROL Visualizzatori]**.

   Consulta [Collegare un set di immagini a una pagina web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporare il visualizzatore di video o immagini](/help/assets/dynamic-media/embed-code.md).

Per modificare i set di immagini, consulta [modifica di set di immagini](#editing-image-sets). Inoltre, è possibile visualizzare e modificare [Proprietà set immagini](/help/assets/manage-digital-assets.md#editing-properties).

In caso di problemi durante la creazione dei set, consultate Immagini e set in [Risoluzione dei problemi di Dynamic Medie](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Caricare risorse per set di immagini {#uploading-assets-in-image-sets}

Per iniziare, carica le risorse immagine per i set di immagini. Gli utenti possono ingrandire le immagini nel Visualizzatore set di immagini. Scegliere quindi con attenzione le immagini. Assicurati che le immagini abbiano una dimensione minima di 2000 pixel per ottenere un dettaglio di zoom ottimale. Dynamic Medie è in grado di eseguire il rendering di immagini fino a 25 megapixel ciascuna. Ad esempio, puoi utilizzare un’immagine da 5000 x 5000 megapixel o qualsiasi altra combinazione di dimensioni fino a 25 megapixel.

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

Consulta [Dynamic Medie - Formati di immagine raster supportati](/help/assets/file-format-support.md#image-support-dynamic-media) per un elenco di formati supportati dai set di immagini.

Per i set di immagini puoi caricare le immagini come faresti [caricare qualsiasi altra risorsa in Assets](/help/assets/manage-digital-assets.md#uploading-assets).

### Prepara risorse set immagini per il caricamento {#preparing-image-set-assets-for-upload}

Prima di creare i set di immagini, accertatevi che le immagini siano delle dimensioni e del formato corretti.

Per creare un set di immagini con più viste, è necessario disporre di immagini che mostrino un elemento da diversi punti di vista o che mostrino aspetti diversi dello stesso elemento. L’obiettivo è quello di evidenziare le funzioni importanti di un elemento in modo che gli utenti abbiano un’immagine completa di come appare o cosa fa.

Poiché gli utenti possono ingrandire le immagini in Set immagini, accertatevi che le dimensioni siano di almeno 2000 pixel. Experience Manager Assets supporta molti formati di file immagine, ma si consiglia di utilizzare immagini TIFF, PNG e EPS senza perdita di dati.

>[!NOTE]
>
>Se utilizzi le miniature per indicare i campioni di prodotto, procedi come segue:
>
>Creare vignettature o diverse riprese della stessa immagine, visualizzandole in diversi colori, motivi o finiture. Sono inoltre necessari file di miniature corrispondenti ai diversi colori, motivi o finiture. Ad esempio, per presentare le miniature con un set di immagini che mostra la stessa giacca in nero, marrone e verde, è necessario:
>
>* Un colpo nero, marrone e verde della stessa giacca.
>* Miniatura di colore nero, marrone e verde.

## Crea set di immagini {#creating-image-sets}

Puoi creare set di immagini tramite l’interfaccia utente o tramite l’API.

>[!NOTE]
>
>Potete anche creare automaticamente i set di immagini tramite [predefiniti set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**Importante:** i set di batch vengono creati dall’IPS (Image Production System) come parte dell’inserimento delle risorse.

Quando aggiungi risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo che sono state aggiunte.

>[!NOTE]
>
>I set di immagini non sono supportati per le risorse il cui nome file contiene &quot;,&quot; (virgola).

Quando crei un set di immagini, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| Numero di risorse duplicate per set | Nessun duplicato | 20 |
| Numero massimo di immagini per set | 5-10 immagini per set | 1000 |

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/dynamic-media/limitations.md).

**Per creare i set di immagini:**

1. In Adobe Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Tocca **[!UICONTROL Navigazione]** > **[!UICONTROL Risorse]**. Passa alla posizione in cui desideri creare un set di immagini, quindi vai a **[!UICONTROL Crea]** > **[!UICONTROL Set immagini]** per aprire la pagina Editor set di immagini.

   Puoi anche creare il set dall’interno di una cartella contenente le risorse.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Nella pagina Editor set di immagini, in **[!UICONTROL Titolo]** , immettere un nome per il set di immagini. Il nome viene visualizzato nel banner del set di immagini. È possibile inserire una descrizione.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Effettuare una delle seguenti operazioni:

   * Nell&#39;angolo superiore sinistro della pagina Editor set di immagini selezionare **[!UICONTROL Aggiungi risorsa]**.

   * Al centro della pagina Editor set di immagini, seleziona **[!UICONTROL Toccate per aprire il selettore risorse]**.

   Tocca per selezionare le risorse da includere nel set di immagini. Le risorse selezionate presentano un’icona a forma di segno di spunta. Al termine, vicino all’angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e selezionando **[!UICONTROL Ritorno]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e quindi fai clic su **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]**, o **[!UICONTROL Vista a elenco]**.

   Consulta [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Quando aggiungi risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

   Se necessario, trascina l’icona Riordina di una risorsa a destra del nome del file della risorsa per riordinare le immagini verso l’alto o verso il basso nell’elenco dei set.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Per modificare una miniatura o un campione, fai clic sull’icona **+** **miniatura** accanto all’immagine e individua la miniatura o il campione desiderato. Dopo aver selezionato tutte le immagini, fai clic su **[!UICONTROL Salva]**.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per eliminare un’immagine, selezionala e seleziona **[!UICONTROL Elimina risorsa]**.

   * Per applicare un predefinito, fai clic su nell’angolo superiore destro della pagina **[!UICONTROL Predefinito]**, quindi seleziona un predefinito da applicare a tutte le risorse contemporaneamente.

   >[!NOTE]
   >
   >Durante la creazione del set di immagini, è possibile modificare la miniatura del set di immagini. In alternativa, puoi consentire a Experience Manager di selezionare automaticamente la miniatura in base alle risorse nel set di immagini. Per selezionare una miniatura, seleziona **[!UICONTROL Cambia miniatura]** sopra il campo Titolo nella pagina Editor set di immagini. Quindi, seleziona un’immagine (puoi passare anche ad altre cartelle per trovare le immagini). Se hai selezionato una miniatura e vuoi che Experience Manager ne generi una dal set di immagini, seleziona **[!UICONTROL Passa a]** **[!UICONTROL Miniatura automatica]**.

1. Fai clic su **[!UICONTROL Salva]**. Il set di immagini creato viene visualizzato nella cartella in cui è stato creato.

## Visualizza set di immagini {#viewing-image-sets}

Puoi creare set di immagini nell’interfaccia utente o automaticamente utilizzando [predefiniti set di batch](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>I set di batch vengono creati dall&#39;IPS [Image Production System] come parte dell’inserimento delle risorse.

Tuttavia, i set creati utilizzando i predefiniti per set di batch, esegui *non* nell&#39;interfaccia utente. È possibile visualizzare questi set in tre modi diversi. Questi metodi sono disponibili anche se avete creato i set di immagini nell&#39;interfaccia utente.

* Apri le proprietà di una risorsa. Le proprietà indicano i set a cui fa riferimento la risorsa selezionata o un membro di. Per visualizzare l&#39;intero set, selezionate il nome del set.

  ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* Da un’immagine inclusa in un qualsiasi set. Seleziona la **[!UICONTROL Set]** per visualizzare i set di cui fa parte la risorsa.

  ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Dalla ricerca, puoi selezionare **[!UICONTROL Filtro]**, quindi espandi **[!UICONTROL Dynamic Medie]** e seleziona **[!UICONTROL Set]**.

  La ricerca restituisce i set corrispondenti creati manualmente nell’interfaccia utente o automaticamente tramite i predefiniti per set di batch. Per i set automatizzati, la query di ricerca viene eseguita utilizzando &quot;Inizia con&quot;. Questo criterio di ricerca è diverso da Experience Manager, che si basa sull’utilizzo di &quot;Contiene&quot;. Impostazione del filtro su **[!UICONTROL Set]** è l&#39;unico modo per cercare i set automatizzati.

  ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>I set possono essere visualizzati tramite l’interfaccia utente, come descritto in [Modifica dei set di immagini](#editing-image-sets).

## Modifica set di immagini {#editing-image-sets}

È possibile eseguire varie attività di modifica sui set di immagini, ad esempio:

* Aggiunge immagini al set di immagini.
* Riordinare le immagini nel set di immagini.
* Eliminare le risorse nel set di immagini.
* Applicare i predefiniti visualizzatore.
* Elimina il set di immagini.

**Per modificare i set di immagini:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa set di immagini, quindi seleziona **[!UICONTROL Modifica]** (icona della matita).
   * Passa il puntatore del mouse su una risorsa set di immagini, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** nella barra degli strumenti.
   * Tocca una risorsa set di immagini, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) nella barra degli strumenti.

1. Per modificare le immagini nel set di immagini, effettuate una delle seguenti operazioni:

   * Per riordinare le risorse, trascina un’immagine in una nuova posizione (seleziona l’icona Riordina per spostare gli elementi).
   * Per ordinare gli elementi in ordine crescente o decrescente, fare clic sull&#39;intestazione della colonna.
   * Per aggiungere una risorsa o aggiornare una risorsa esistente, fai clic sul pulsante **[!UICONTROL Aggiungi risorsa]**. Passa a una risorsa, selezionala, quindi seleziona **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro della pagina.
     >[!NOTE]
     >
     >Se elimini l’immagine utilizzata da Experience Manager per la miniatura sostituendola con un’altra immagine, la risorsa originale viene comunque visualizzata.
   * Per eliminare una risorsa, selezionala e seleziona **[!UICONTROL Elimina risorsa]**.
   * Per applicare un predefinito, fai clic su nell’angolo superiore destro della pagina **[!UICONTROL Predefinito]**, quindi seleziona un predefinito visualizzatore.
   * Per aggiungere o modificare una miniatura, seleziona l’icona della miniatura accanto a destra della risorsa. Passa alla nuova miniatura o risorsa campione, selezionala, quindi fai clic su **[!UICONTROL Seleziona]**.
   * Per eliminare un intero set di immagini, passa al set di immagini, selezionalo e seleziona **[!UICONTROL Elimina]**.

   >[!NOTE]
   >
   >È possibile modificare le immagini in un set di immagini. Passa al set e seleziona **[!UICONTROL Membri set]** nella barra a sinistra. Per aprire la finestra di modifica, seleziona l’icona a forma di matita su una risorsa.

1. Tocca **[!UICONTROL Salva]** al termine della modifica.

## Anteprima set immagini {#previewing-image-sets}

Consulta [Visualizzare in anteprima le risorse](/help/assets/dynamic-media/previewing-assets.md).

## Pubblicazione dei set di immagini {#publishing-image-sets}

Consulta [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
