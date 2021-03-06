---
title: Set di file multimediali diversi
description: Scopri come utilizzare i set di file multimediali diversi in Dynamic Media.
feature: Mixed Media Sets
role: User
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: b31fa5af7bcaa944d8bd7b0bb7d7b8deb36906a8
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 14%

---

# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire una combinazione di immagini, set di immagini, set 360 gradi e video in una presentazione.

I set di file multimediali diversi sono indicati da un banner con la parola **[!UICONTROL MixedMediaSet]**. Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente di Assets, consulta [Gestire le risorse con l’interfaccia utente touch](/help/assets/manage-digital-assets.md).

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettua le seguenti operazioni:

1. [Caricare le risorse](#uploading-assets).

   Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Se necessario, crea i [Set di immagini](/help/assets/dynamic-media/image-sets.md) e i [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md). Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di file multimediali diversi, assicurati di tenere conto dello zoom quando scegli le immagini. Assicurati che le immagini siano di almeno 2000 pixel nelle dimensioni più grandi.

   Vedi [Dynamic Media - Formati immagine raster supportati](/help/assets/file-format-support.md#image-support-dynamic-media) per un elenco dei formati supportati dai set di file multimediali diversi.

1. [Creare set di file multimediali diversi](#creating-mixed-media-sets).

   Per creare un set di file multimediali diversi, dalla pagina Risorse vai a **[!UICONTROL Crea]** > **[!UICONTROL Set di file multimediali diversi]** quindi assegna un nome al set, scegli le risorse e scegli l’ordine in cui vengono visualizzate le immagini.

   Vedi [Utilizzare i selettori](/help/assets/dynamic-media/working-with-selectors.md).

1. Configurazione [Predefiniti visualizzatore di file multimediali diversi](/help/assets/dynamic-media/managing-viewer-presets.md), se necessario.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set di file multimediali diversi predefiniti. Per visualizzare i file multimediali diversi con un predefinito per visualizzatori, seleziona il set di file multimediali diversi e fai clic su **[!UICONTROL Visualizzatori]** nel menu a discesa della barra a sinistra.

   Per creare o modificare i predefiniti visualizzatore, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti visualizzatore]**.

   Vedi [Aggiungere e modificare i predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Anteprima set di file multimediali diversi](#previewing-mixed-media-sets).

   Seleziona il set di file multimediali diversi e puoi visualizzarlo in anteprima. Per esaminare il set di file multimediali diversi nel visualizzatore selezionato, seleziona le icone delle miniature. Puoi scegliere diversi visualizzatori dal **[!UICONTROL Visualizzatori]** disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare set di file multimediali diversi](#publishing-mixed-media-sets).

   La pubblicazione di un set di file multimediali diversi attiva l’URL e la stringa di incorporamento. Inoltre, devi [pubblicare il predefinito visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Collegare gli URL all’applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [Incorporare il visualizzatore di video o immagini](/help/assets/dynamic-media/embed-code.md).

   Adobe Experience Manager Assets crea chiamate URL per set di file multimediali diversi e li attiva dopo la pubblicazione dei set di file multimediali diversi. Puoi copiare questi URL quando visualizzi l’anteprima delle risorse. In alternativa è possibile incorporarli sul sito Web.

   Seleziona il set di file multimediali diversi, quindi seleziona dal menu a discesa della barra a sinistra **[!UICONTROL Visualizzatori]**.

   Vedi [Collegamento di un set di file multimediali diversi a una pagina web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporare il visualizzatore di video o immagini](/help/assets/dynamic-media/embed-code.md).

Se necessario, puoi modificare [Set di file multimediali diversi](#editing-mixed-media-sets). Inoltre, puoi visualizzare e modificare [Proprietà set di file multimediali diversi](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>In caso di problemi nella creazione dei set, vedi [Risolvere i problemi relativi a Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Caricare le risorse {#uploading-assets}

Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Ricorda che gli utenti possono ingrandire le immagini nel visualizzatore di set di file multimediali diversi. Scegliere le immagini con questa funzionalità di zoom. Assicurati che le immagini siano di almeno 2000 pixel nelle dimensioni più grandi.

Inoltre, se desideri aggiungere set 360 gradi o set di immagini al set di file multimediali diversi, creali pure.

Vedi [Dynamic Media - Formati immagine raster supportati](/help/assets/file-format-support.md#image-support-dynamic-media) per un elenco dei formati supportati dai set di file multimediali diversi.

## Creare set di file multimediali diversi {#creating-mixed-media-sets}

Puoi aggiungere immagini, set di immagini, set 360 gradi e video al set di file multimediali diversi. Assicurati che i file, i set di immagini e i set 360 gradi siano pronti per la pubblicazione prima di aggiungerli al set di file multimediali diversi.

Quando aggiungi delle risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

**Per creare set di file multimediali diversi:**

1. In Assets, individua il punto in cui vuoi creare un set di file multimediali diversi e seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set di file multimediali diversi]**. Puoi anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set di file multimediali diversi.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Nell’Editor set di file multimediali diversi, in **[!UICONTROL Titolo]**, immetti un nome per il set di file multimediali diversi. Il nome viene visualizzato nel banner nel set di file multimediali diversi. Facoltativamente, immetti una descrizione.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Quando crei il set di file multimediali diversi, puoi modificare la miniatura del set di file multimediali diversi o consentire ad Experience Manager di selezionarla automaticamente in base alle risorse nel set di file multimediali diversi. Per selezionare una miniatura, seleziona **[!UICONTROL Modifica miniatura]** e seleziona qualsiasi immagine (puoi passare ad altre cartelle per trovare anche le immagini). Se hai selezionato una miniatura e vuoi che l’Experience Manager ne generi una dal set di file multimediali diversi, seleziona **[!UICONTROL Passa alla miniatura automatica]**.

1. Per selezionare le risorse da includere nel set di file multimediali diversi, seleziona il selettore delle risorse. Selezionali e seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e selezionando **[!UICONTROL Ritorno]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e quindi seleziona la **[!UICONTROL Filtro]** dalla barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona **[!UICONTROL Visualizza]** e fai clic su **[!UICONTROL Vista a elenco]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a schede]**.

   Vedi [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Riordinare le risorse trascinandole verso l’alto o verso il basso nell’elenco (è necessario selezionare la **[!UICONTROL Riordina]** (icona), se necessario.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere le miniature, seleziona la **+** **[!UICONTROL miniatura]** accanto all’immagine e passa alla miniatura desiderata. Dopo aver selezionato tutte le miniature, seleziona **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Per aggiungere risorse, seleziona **[!UICONTROL Aggiungi risorsa]**.

1. Per eliminare una risorsa, seleziona la casella di controllo corrispondente e seleziona **[!UICONTROL Elimina risorsa]**.
1. Per applicare un predefinito, seleziona **[!UICONTROL Predefinito]** nell’angolo in alto a destra e seleziona un predefinito da applicare alle risorse.
1. Seleziona **[!UICONTROL Salva]**. Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modifica set di file multimediali diversi {#editing-mixed-media-sets}

Puoi eseguire varie attività di modifica alle risorse in Set di file multimediali diversi direttamente nell’interfaccia utente [come qualsiasi risorsa in Assets](/help/assets/manage-digital-assets.md). In Set di file multimediali diversi è inoltre possibile effettuare le seguenti operazioni:

* Aggiungi le risorse al set di file multimediali diversi.
* Riordinare le risorse nel set di file multimediali diversi.
* Elimina le risorse nel set di file multimediali diversi.
* Applica i predefiniti visualizzatore.
* Modifica la miniatura predefinita.

**Per modificare i set di file multimediali diversi:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Seleziona una risorsa Set di file multimediali diversi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) sulla barra degli strumenti.

1. Nell’Editor set di file multimediali diversi, effettua una delle seguenti operazioni:

   * Per riordinare le risorse: nel pannello a sinistra, seleziona **[!UICONTROL Risorse]** (icona immagine), trascina una risorsa in una nuova posizione.
   * Per aggiungere risorse, seleziona nella barra degli strumenti **[!UICONTROL Aggiungi risorsa]**. Passa alle risorse. Per ogni risorsa da aggiungere, passa il cursore del mouse sull’immagine della risorsa (non sul nome della risorsa), quindi seleziona l’icona a forma di segno di spunta. Nell’angolo in alto a destra, seleziona **[!UICONTROL Seleziona]**.

   * Per eliminare una risorsa - Nel pannello a sinistra, seleziona **[!UICONTROL Risorse]** (icona immagine), quindi seleziona la risorsa. Nella barra degli strumenti, seleziona **[!UICONTROL Elimina risorsa]**.

   * Per ordinare le risorse in base al loro nome in ordine crescente o decrescente, nel pannello a sinistra seleziona **[!UICONTROL Risorse]** (icona immagine). A destra del **[!UICONTROL Risorse]** intestazione, selezionare le icone del cursore verso l’alto o verso il basso.

      >[!NOTE]
      >
      >* Per eliminare un intero set di file multimediali diversi da qualsiasi modalità di visualizzazione (ad esempio **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a colonne]**) passa al set di file multimediali diversi. Passa il puntatore del mouse sulla risorsa, quindi seleziona l’icona del segno di spunta per selezionarla. Press **[!UICONTROL Backspace]** sulla tastiera, oppure seleziona **[!UICONTROL Altro]** (tre punti) sulla barra degli strumenti, quindi seleziona **[!UICONTROL Elimina]**.
      >
      >* Per modificare le risorse in un set di file multimediali diversi, passa al set . Nella barra a sinistra, seleziona **[!UICONTROL Imposta membri]**, quindi seleziona la **[!UICONTROL Matita]** su una singola risorsa per aprire la finestra di modifica.


1. Seleziona **[!UICONTROL Salva]** al termine della modifica.

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passa a Set di file multimediali diversi. Toccate (non selezionate) il set per aprirlo nella pagina Anteprima set di Experienci Manager . Nella barra a sinistra, seleziona il cursore verso il basso per aprire l’elenco a discesa, quindi seleziona **[!UICONTROL Imposta membri]**. Nella pagina Membri set , passa il puntatore del mouse su una risorsa, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) per aprire la pagina di modifica.
   >
   >* Per eliminare un intero set di file multimediali diversi: da qualsiasi modalità di visualizzazione (come Vista a schede o Vista a colonne), vai al set di file multimediali diversi. Passa il puntatore del mouse sul set, quindi seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Press **[!UICONTROL Backspace]** sulla tastiera, oppure seleziona **[!UICONTROL Altro]** (riga di tre punti), quindi seleziona **[!UICONTROL Elimina]**.


## Anteprima set di file multimediali diversi {#previewing-mixed-media-sets}

Vedi [Anteprima delle risorse](/help/assets/dynamic-media/previewing-assets.md) per informazioni dettagliate su come visualizzare in anteprima i set di file multimediali diversi.

## Pubblicare set di file multimediali diversi {#publishing-mixed-media-sets}

Vedi [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare set di file multimediali diversi.

>[!NOTE]
>
>Se il set di file multimediali diversi non termina completamente nel servizio di consegna al primo momento della pubblicazione, pubblica il set di file multimediali diversi una seconda volta.
