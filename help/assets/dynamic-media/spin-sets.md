---
title: Set 360 gradi
description: Scopri come utilizzare i set 360 gradi in Dynamic Media
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Set 360 gradi{#spin-sets}

Un set 360 gradi simula la rotazione reale di un oggetto per esaminarlo. I set 360 gradi consentono di visualizzare gli elementi da qualsiasi angolo, ottenendo i dettagli visivi chiave da qualsiasi angolazione.

Un set 360 gradi simula un’esperienza di visualizzazione a 360 gradi. Dynamic Media offre set 360 gradi con asse singolo in cui gli utenti possono ruotare un elemento. Inoltre, gli utenti possono effettuare lo zoom &quot;a mano libera&quot; e scorrere qualsiasi visualizzazione con pochi semplici clic del mouse. In questo modo, gli utenti possono esaminare un elemento più da vicino da un particolare punto di vista.

I set 360 gradi sono contrassegnati da un banner con la parola **[!UICONTROL SPINSET]**. Inoltre, se il set 360 gradi è pubblicato, la data di pubblicazione indicata dall’icona **[!UICONTROL Mondo]** si trova sul banner insieme all’ultima data di modifica, indicata dall’icona **[!UICONTROL Matita]** .

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente Risorse, consulta [Gestione delle risorse con l’interfaccia](/help/assets/manage-digital-assets.md)touch.

## Avvio rapido: Set 360 gradi {#quick-start-spin-sets}

Per iniziare rapidamente a usare i set 360 gradi, effettuate le seguenti operazioni:

1. [Caricate le immagini per più viste.](#uploading-assets-for-spin-sets)

   Per un set 360 gradi monodimensionale, sono necessari almeno 8-12 scatti di un elemento e 16-24 scatti per un set 360 gradi bidimensionale. Le riprese devono essere effettuate a intervalli regolari per dare l’impressione che l’elemento stia ruotando e sia capovolto. Ad esempio, se un set 360 gradi monodimensionale include 12 scatti, ruotate l’elemento di 30 gradi (360/12) per ciascuna ripresa.

1. [Creare set 360 gradi.](#creating-spin-sets)

   Per creare un set 360 gradi, selezionate **[!UICONTROL Crea > Set]** 360 gradi, quindi assegnate un nome al set, scegliete le risorse e scegliete l’ordine di visualizzazione delle immagini.

   See [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

   >[!NOTE]
   >
   >Potete anche creare i set 360 gradi automaticamente tramite i predefiniti per set di [batch](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **** Importante:I set di batch vengono creati dall’IPS (Image Production System) come parte dell’assimilazione delle risorse.

1. Impostate i predefiniti [](/help/assets/dynamic-media/managing-viewer-presets.md)per visualizzatori di set 360 gradi in base alle vostre esigenze.

   Gli amministratori possono creare o modificare i predefiniti per visualizzatori di set 360 gradi. Per visualizzare il set 360 gradi con un predefinito per visualizzatori, selezionate il set 360 gradi e nel menu a discesa a sinistra selezionate **Visualizzatori**.

   Consultate **[!UICONTROL Strumenti > Risorse > Predefiniti]** visualizzatore per creare o modificare i predefiniti per visualizzatori.

   Consultate [Aggiunta e modifica dei predefiniti per visualizzatori.](/help/assets/dynamic-media/managing-viewer-presets.md)

   Potete visualizzare e accedere ai set creati mediante i predefiniti per set di batch in tre modi diversi. (i set creati utilizzando i predefiniti per set di batch *non* vengono visualizzati nell’interfaccia utente).

1. [Anteprima set 360 gradi](/help/assets/dynamic-media/previewing-assets.md)

   Selezionate il set 360 gradi ed effettuate l’anteprima. Ruotate il set 360 gradi. Potete scegliere diversi visualizzatori dal menu **[!UICONTROL Visualizzatori]** , disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare Set 360 gradi](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   Quando si pubblica un set 360 gradi, vengono attivate l’URL e la stringa da incorporare. Inoltre, dovete [pubblicare il predefinito](/help/assets/dynamic-media/managing-viewer-presets.md)per visualizzatori.

1. [Collegare gli URL all’applicazione](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) Web o [incorporare il visualizzatore](/help/assets/dynamic-media/embed-code.md)video o immagini.

   Risorse AEM crea richieste URL per i set 360 gradi e le attiva dopo la pubblicazione dei set 360 gradi. Potete copiare questi URL quando visualizzate l’anteprima delle risorse. In alternativa, potete incorporarli nel sito Web.

   Selezionate il set 360 gradi, quindi nel menu a discesa della barra a sinistra selezionate **[!UICONTROL Visualizzatori]**.

   Consultate [Collegamento di un set 360 gradi a una pagina](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) Web e [Incorporazione di un visualizzatore](/help/assets/dynamic-media/embed-code.md)video o di immagini.

Se necessario, potete [modificare i set](#editing-spin-sets)360 gradi. Inoltre, potete visualizzare e modificare le proprietà [del set](/help/assets/manage-digital-assets.md#editing-properties)360 gradi.

## Caricamento delle risorse per i set 360 gradi {#uploading-assets-for-spin-sets}

Per un set 360 gradi monodimensionale, sono necessari almeno 8-12 scatti di un elemento e 16-24 scatti per un set 360 gradi bidimensionale. Le riprese devono essere effettuate a intervalli regolari per dare l’impressione che l’elemento stia ruotando e sia capovolto. Ad esempio, se un set 360 gradi monodimensionale include 12 scatti, ruotate l’elemento di 30 gradi (360/12) per ciascuna ripresa.

Potete caricare le immagini per i set 360 gradi come fareste per [caricare qualsiasi altra risorsa in AEM Assets](/help/assets/manage-digital-assets.md).

### Linee guida per l’acquisizione di immagini per il set 360 gradi {#guidelines-for-shooting-spin-set-images}

Di seguito sono riportate alcune best practice per le immagini dei set 360 gradi. In generale, più immagini si trovano in un set 360 gradi, migliore sarà l’effetto di rotazione dell’immagine. Tuttavia, l’inclusione di molte immagini nel set aumenta anche il tempo necessario al caricamento delle immagini. AEM consiglia di seguire queste linee guida per lo scatto di immagini da usare nei set 360 gradi:

* Utilizzate almeno 8-12 immagini in un set 360 gradi monodimensionale e 16-24 immagini in un set 360 gradi bidimensionale. Per poter ruotare di 360 gradi è necessario disporre di almeno 8 immagini. I set 360 gradi monodimensionali sono più comuni quando la creazione di set 360 gradi bidimensionali richiede molta manodopera.
* Utilizzare un formato senza perdita di dati; Si consigliano TIFF e PNG.
* Mascherate tutte le immagini in modo che l’elemento venga visualizzato su uno sfondo bianco puro o su un altro sfondo ad alto contrasto. Se necessario, aggiungete ombre.
* Accertatevi che i dettagli del prodotto siano ben illuminati e messi a fuoco.
* Scattare immagini per capi di abbigliamento di moda con un manichino o un modello. Spesso il manichino è completamente mascherato (utilizzando un manichino in vetro) oppure nell’immagine è visibile un manichino/un set di cornici stilizzato. Potete creare un set 360 gradi su un modello definendo il numero di angoli. Contrassegnare ogni angolo con nastro sul pavimento per guidare il modello a passo e guardare nella direzione di ogni ripresa.

## Creazione di set 360 gradi {#creating-spin-sets}

Questa sezione descrive come creare i set 360 gradi.

>[!NOTE]
>
>Potete anche creare i set 360 gradi automaticamente tramite i predefiniti per set di [batch](/help/assets/dynamic-media/config-dm.md). **** Importante:I set di batch vengono creati dall’IPS (Image Production System) come parte dell’assimilazione delle risorse.
>
>Consultate &quot;Creazione di predefiniti per set di batch per generare automaticamente set di immagini e set 360 gradi&quot; in [Configurazione di elementi multimediali](/help/assets/dynamic-media/config-dm.md)dinamici.

>[!NOTE]
>
>Ordine in cui le immagini vengono visualizzate in un set 360 gradi Accertatevi di ordinarli in modo che la rotazione sia una vista a 360 gradi uniforme.

**Per creare dei set 360 gradi**

1. In Risorse, individuate il punto in cui desiderate creare un set 360 gradi, fate clic su **[!UICONTROL Crea]** e selezionate Set **** 360 gradi. Potete anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set 360 gradi.

   ![6_5_spinset-createpullmenu](assets/6_5_spinset-createpulldownmenu.png)

1. Nell’Editor set 360 gradi, nel campo **[!UICONTROL Titolo]** , inserite un nome per il set 360 gradi. Il nome viene visualizzato nel banner lungo il set 360 gradi. Facoltativamente, immettete una descrizione.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Quando create il set 360 gradi, potete modificare la miniatura del set 360 gradi o consentire ad AEM di selezionare la miniatura automaticamente in base alle risorse del set 360 gradi. Per selezionare una miniatura, fate clic su **[!UICONTROL Cambia miniatura]** e selezionate una qualsiasi immagine (per trovare anche le immagini potete spostarvi in altre cartelle). Se avete selezionato una miniatura e desiderate che AEM ne generi una dal set 360 gradi, selezionate **[!UICONTROL Passa alla miniatura]** automatica.

1. Effettuate una delle seguenti operazioni:

   * Nell’angolo superiore sinistro della pagina Editor set 360 gradi, toccate **[!UICONTROL Aggiungi risorsa]**.

   * Al centro della pagina Editor set 360 gradi, toccate **[!UICONTROL Toccate per aprire il selettore]** risorse.
   Toccate per selezionare le risorse da includere nel set 360 gradi. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine, toccate **[!UICONTROL Seleziona]** accanto all’angolo superiore destro della pagina.

   Con il selettore delle risorse, potete cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Return**. Potete anche applicare filtri per perfezionare i risultati della ricerca. Potete filtrare per percorso, raccolta, tipo di file e tag. Selezionate il filtro e toccate l’icona **[!UICONTROL Filtro]** sulla barra degli strumenti. Per modificare la visualizzazione, toccate l’icona Visualizza e selezionate Visualizzazione **** a colonne, Visualizzazione **[!UICONTROL a]** schede o Visualizzazione **** elenco.

   See [Working with Selectors](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Quando aggiungete delle risorse al set, queste vengono automaticamente aggiunte in ordine alfanumerico. Potete riordinare o ordinare manualmente le risorse dopo averle aggiunte.

   Se necessario, trascinate l’icona Riordina di una risorsa a destra del nome del file della risorsa per riordinare le immagini verso l’alto o verso il basso nell’elenco dei set.

   ![Riordinamento del fotogramma 11 nel set 360 gradi trascinandolo in una nuova posizione.](assets/6_5_spinset-reorderassets.png)

   Riordinamento del fotogramma 11 nel set 360 gradi trascinandolo in una nuova posizione.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per eliminare un’immagine, selezionatela e toccate **[!UICONTROL Elimina risorsa]**.

   * Per applicare un predefinito, toccate **[!UICONTROL Predefinito]** accanto all’angolo superiore destro della pagina, quindi selezionate un predefinito da applicare a tutte le risorse alla volta.

1. Fai clic su **[!UICONTROL Salva]**. Il set 360 gradi appena creato viene visualizzato nella cartella in cui è stato creato.

## Visualizzazione di set 360 gradi {#viewing-spin-sets}

Potete creare i set 360 gradi nell’interfaccia utente o automaticamente utilizzando i predefiniti per set di [batch](/help/assets/dynamic-media/config-dm.md). Tuttavia, i set creati utilizzando i predefiniti per set di batch *non* vengono visualizzati nell’interfaccia utente. Potete accedere ai set creati mediante i predefiniti per set di batch in tre modi diversi. (Questi metodi sono disponibili anche se avete creato i set 360 gradi nell’interfaccia utente).

>[!NOTE]
>
>Potete inoltre visualizzare i set mediante l’interfaccia utente come descritto in [Modifica di set](#editing-spin-sets)360 gradi.

**Per visualizzare i set 360 gradi**

1. Quando si aprono le proprietà di una singola risorsa. Le proprietà indicano i set di cui la risorsa selezionata è membro (in **[!UICONTROL Membro dei set]**). Fate clic sul nome del set per visualizzare l’intero set.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Da un’immagine membro di qualsiasi set. Selezionate il menu **[!UICONTROL Set]** per visualizzare i set di cui la risorsa è membro.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Dalla ricerca, potete selezionare **[!UICONTROL Filtri]**, quindi espandere File multimediali **** dinamici e selezionare **[!UICONTROL Set]**.

   La ricerca restituisce i set corrispondenti creati manualmente nell’interfaccia utente o automaticamente tramite i predefiniti per set di batch. Per i set automatizzati, la query di ricerca viene eseguita utilizzando criteri di `Starts with` ricerca diversi dalla ricerca AEM basata sui criteri di `Contains` ricerca. L&#39;impostazione del filtro su **[!UICONTROL Set]** è l&#39;unico modo per eseguire ricerche nei set automatizzati.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Modifica dei set 360 gradi {#editing-spin-sets}

Potete eseguire diverse attività di modifica sui set 360 gradi, ad esempio:

* Aggiungete immagini al set 360 gradi.
* Riordinare le immagini nel set 360 gradi.
* Potete eliminare le risorse nel set 360 gradi.
* Applicate i predefiniti per visualizzatori.
* Eliminate il set 360 gradi.

**Per modificare un set 360 gradi**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa set 360 gradi, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa set 360 gradi, toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi toccate **[!UICONTROL Modifica]** nella barra degli strumenti.

   * Toccate una risorsa set 360 gradi, quindi toccate **[!UICONTROL Modifica]** (icona matita) nella barra degli strumenti.

1. Per modificare il set 360 gradi, effettuate una delle seguenti operazioni:

   * Per riordinare le immagini, trascinate un’immagine in una nuova posizione (selezionate l’icona di riordinamento per spostare gli elementi).
   * Per ordinare gli elementi in ordine crescente o decrescente, fate clic sull’intestazione della colonna.
   * Per aggiungere una risorsa o aggiornare una risorsa esistente, fate clic su **[!UICONTROL Aggiungi risorsa]**. Andate a una risorsa, selezionatela, quindi toccate **[!UICONTROL Seleziona]** vicino all&#39;angolo superiore destro.
Se eliminate l’immagine utilizzata da AEM per la miniatura sostituendola con un’altra immagine, viene comunque visualizzata la risorsa originale.
   * Per eliminare una risorsa, selezionatela e toccate o fate clic su **[!UICONTROL Elimina risorsa]**.
   * Per applicare un predefinito, toccate o fate clic sull’icona del predefinito e selezionate un predefinito.
   * Per eliminare un intero set 360 gradi, selezionatelo e selezionate **[!UICONTROL Elimina]**
   >[!NOTE]
   >
   >Per modificare le immagini di un set 360 gradi, toccate il set, toccate Membri **** set nella parte sinistra, quindi toccate l’icona Matita su una singola risorsa per aprire la finestra di modifica.

1. Fate clic su **[!UICONTROL Salva]** al termine della modifica.

## Anteprima dei set 360 gradi {#previewing-spin-sets}

Consultate [Anteprima delle risorse](/help/assets/dynamic-media/previewing-assets.md).

## Pubblicazione di set 360 gradi {#publishing-spin-sets}

Consultate [Pubblicazione delle risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).