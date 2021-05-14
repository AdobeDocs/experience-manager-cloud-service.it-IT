---
title: Set di file multimediali diversi
description: Scopri come utilizzare i set di file multimediali diversi in Dynamic Media.
feature: Set di file multimediali diversi
role: Business Practitioner
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 23%

---

# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire una combinazione di immagini, set di immagini, set 360 gradi e video in una presentazione.

I set di file multimediali diversi sono indicati da un banner con la parola **[!UICONTROL MixedMediaSet]**. Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente Assets, consulta [Gestione delle risorse con l’interfaccia Touch](/help/assets/manage-digital-assets.md).

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettua le seguenti operazioni:

1. [Carica le risorse](#uploading-assets).

   Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Se necessario, crea i [Set di immagini](/help/assets/dynamic-media/image-sets.md) e i [Set 360 gradi](/help/assets/dynamic-media/spin-sets.md). Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di file multimediali diversi, assicurati di tenere conto dello zoom quando scegli le immagini. Assicurati che le immagini siano di almeno 2000 pixel nelle dimensioni più grandi.

1. [Creare set di file multimediali diversi](#creating-mixed-media-sets).

   Per creare un set di file multimediali diversi, dalla pagina Risorse tocca **[!UICONTROL Crea > Set di file multimediali diversi]**, quindi assegna un nome al set, scegli le risorse e stabilisci l’ordine in cui vengono visualizzate le immagini.

   Vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

1. Imposta i [predefiniti visualizzatore di file multimediali diversi](/help/assets/dynamic-media/managing-viewer-presets.md), a seconda delle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set di file multimediali diversi predefiniti. Per visualizzare i file multimediali diversi con un predefinito per visualizzatori, seleziona il set di file multimediali diversi e fai clic su **[!UICONTROL Visualizzatori]** nel menu a discesa della barra a sinistra.

   Per creare o modificare i predefiniti visualizzatore, consulta **[!UICONTROL Strumenti > Risorse > Predefiniti visualizzatore]**.

   Consulta [Aggiunta e modifica di predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Anteprima di set di file multimediali diversi](#previewing-mixed-media-sets).

   Seleziona il set di file multimediali diversi e puoi visualizzarlo in anteprima. Per esaminare il set di file multimediali diversi nel visualizzatore selezionato, fai clic sulle icone delle miniature. Puoi scegliere diversi visualizzatori dal menu a discesa **[!UICONTROL Visualizzatori]** , disponibile nella barra a sinistra.

1. [Pubblicare Set Di File Multimediali Misti](#publishing-mixed-media-sets).

   La pubblicazione di un set di file multimediali diversi attiva l’URL e la stringa di incorporamento. Inoltre, devi [pubblicare il predefinito visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Collega gli URL all’](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) applicazione Web o  [incorpora il visualizzatore](/help/assets/dynamic-media/embed-code.md) video o immagini.

   Adobe Experience Manager Assets crea chiamate URL per set di file multimediali diversi e li attiva dopo la pubblicazione dei set di file multimediali diversi. Puoi copiare questi URL quando visualizzi l’anteprima delle risorse. In alternativa è possibile incorporarli sul sito Web.

   Seleziona il set di file multimediali diversi, quindi seleziona **[!UICONTROL Visualizzatori]** dal menu a discesa della barra a sinistra.

   Consulta le sezioni [Collegamento di un set di file multimediali diversi a una pagina web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporamento di un visualizzatore di video o immagini](/help/assets/dynamic-media/embed-code.md).

Se necessario, puoi modificare [Set di file multimediali diversi](#editing-mixed-media-sets). Inoltre, puoi visualizzare e modificare le proprietà del [set di file multimediali diversi](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>In caso di problemi durante la creazione dei set, consulta [Risoluzione dei problemi relativi a Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Caricamento delle risorse {#uploading-assets}

Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Ricorda che gli utenti possono ingrandire le immagini nel visualizzatore di set di file multimediali diversi. Scegliere le immagini con questa funzionalità di zoom. Assicurati che le immagini siano di almeno 2000 pixel nelle dimensioni più grandi.

Inoltre, se desideri aggiungere set 360 gradi o set di immagini al set di file multimediali diversi, creali pure.

## Creazione di set di file multimediali diversi {#creating-mixed-media-sets}

Puoi aggiungere immagini, set di immagini, set 360 gradi e video al set di file multimediali diversi. Assicurati che i file, i set di immagini e i set 360 gradi siano pronti per la pubblicazione prima di aggiungerli al set di file multimediali diversi.

Quando aggiungi delle risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

**Per creare un set di file multimediali diversi:**

1. In Assets, individua il punto in cui vuoi creare un set di file multimediali diversi, fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Set di file multimediali diversi]**. Puoi anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set di file multimediali diversi.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Nell’Editor set di file multimediali diversi, in **[!UICONTROL Titolo]**, immetti un nome per il set di file multimediali diversi. Il nome viene visualizzato nel banner nel set di file multimediali diversi. Facoltativamente, immetti una descrizione.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Quando crei il set di file multimediali diversi, puoi modificare la miniatura del set di file multimediali diversi o consentire ad Experience Manager di selezionarla automaticamente in base alle risorse nel set di file multimediali diversi. Per selezionare una miniatura, fai clic su **[!UICONTROL Cambia miniatura]** e seleziona una qualsiasi immagine (puoi passare ad altre cartelle per trovare anche le immagini). Se hai selezionato una miniatura e vuoi che l&#39;Experience Manager ne generi una dal set di file multimediali diversi, seleziona **[!UICONTROL Passa alla miniatura automatica]**.

1. Per selezionare le risorse da includere nel set di file multimediali diversi, tocca il selettore delle risorse. Selezionali e fai clic su **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e tocca l’icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona **[!UICONTROL Visualizza]** e fai clic su **[!UICONTROL Vista a elenco]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a schede]**.

   Vedere [Utilizzo dei selettori](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Riordinare le risorse trascinandole verso l’alto o verso il basso nell’elenco (deve selezionare l’icona **[!UICONTROL Riordina]** ), a seconda delle necessità.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere delle miniature, fai clic sull’icona **+** **[!UICONTROL miniatura]** accanto all’immagine e individua la miniatura desiderata. Dopo aver selezionato tutte le miniature, fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Per aggiungere risorse, tocca **[!UICONTROL Aggiungi risorsa]**.

1. Per eliminare una risorsa, seleziona la casella di controllo corrispondente e tocca **[!UICONTROL Elimina risorsa]**.
1. Per applicare un predefinito, tocca **[!UICONTROL Predefinito]** nell’angolo in alto a destra e seleziona un predefinito da applicare alle risorse.
1. Fai clic su **[!UICONTROL Salva]**. Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modifica di set di file multimediali diversi {#editing-mixed-media-sets}

Puoi eseguire varie attività di modifica alle risorse in Set di file multimediali diversi direttamente nell’interfaccia utente [come qualsiasi risorsa in Assets](/help/assets/manage-digital-assets.md). In Set di file multimediali diversi è inoltre possibile effettuare le seguenti operazioni:

* Aggiungi le risorse al set di file multimediali diversi.
* Riordinare le risorse nel set di file multimediali diversi.
* Elimina le risorse nel set di file multimediali diversi.
* Applica i predefiniti visualizzatore.
* Modifica la miniatura predefinita.

**Per modificare un set di file multimediali diversi:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, quindi tocca **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, tocca **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi tocca **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Tocca una risorsa Set di file multimediali diversi, quindi tocca **[!UICONTROL Modifica]** (icona a forma di matita) sulla barra degli strumenti.

1. Nell’Editor set di file multimediali diversi, effettua una delle seguenti operazioni:

   * Per riordinare le risorse: nel pannello a sinistra, tocca **[!UICONTROL Risorse]** (icona immagine), trascina una risorsa in una nuova posizione.
   * Per aggiungere risorse, tocca **[!UICONTROL Aggiungi risorsa]** sulla barra degli strumenti. Passa alle risorse. Per ogni risorsa da aggiungere, passa il cursore del mouse sull’immagine della risorsa (non sul nome della risorsa), quindi tocca l’icona a forma di segno di spunta. Nell’angolo in alto a destra, tocca **[!UICONTROL Seleziona]**.

   * Per eliminare una risorsa: nel pannello a sinistra tocca **[!UICONTROL Risorse]** (icona immagine), quindi seleziona la risorsa. Nella barra degli strumenti, tocca **[!UICONTROL Elimina risorsa]**.

   * Per ordinare le risorse in base al loro nome in ordine crescente o decrescente, nel pannello a sinistra tocca **[!UICONTROL Risorse]** (icona immagine). A destra dell’intestazione **[!UICONTROL Risorse]** , tocca le icone del cursore verso l’alto o il basso.

      >[!NOTE]
      >
      >* Per eliminare un intero set di file multimediali diversi, da qualsiasi modalità di visualizzazione (ad esempio **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a colonne]**) passa al set di file multimediali diversi. Passa il puntatore del mouse sulla risorsa, quindi tocca l’icona del segno di spunta per selezionarla. Premere **[!UICONTROL Backspace]** sulla tastiera oppure fare clic su **[!UICONTROL Altro]** (tre punti) sulla barra degli strumenti, quindi toccare **[!UICONTROL Elimina]**.
         >
         >
      * Per modificare le risorse in un set di file multimediali diversi, passa al set . Nella barra a sinistra, tocca **[!UICONTROL Membri set]**, quindi tocca l’icona **[!UICONTROL Matita]** su una singola risorsa per aprire la finestra di modifica.


1. Al termine della modifica, tocca **[!UICONTROL Salva]** .

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passa a Set di file multimediali diversi. Toccate (non selezionate) il set per aprirlo nella pagina Anteprima set di Experienci Manager . Nella barra a sinistra, fai clic sul cursore verso il basso per aprire l’elenco a discesa, quindi tocca **[!UICONTROL Imposta membri]**. Nella pagina Membri set , passa il puntatore del mouse su una risorsa, quindi tocca **[!UICONTROL Modifica]** (icona a forma di matita) per aprire la pagina di modifica.
      >
      >
   * Per eliminare un intero set di file multimediali diversi: da qualsiasi modalità di visualizzazione (come Vista a schede o Vista a colonne), vai al set di file multimediali diversi. Passa il puntatore del mouse sul set, quindi tocca **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Premere **[!UICONTROL Backspace]** sulla tastiera oppure toccare **[!UICONTROL Altro]** (riga di tre punti), quindi toccare **[!UICONTROL Elimina]**.


## Anteprima dei set di file multimediali diversi {#previewing-mixed-media-sets}

Per informazioni dettagliate su come visualizzare in anteprima i set di file multimediali diversi, consulta [Anteprima delle risorse](/help/assets/dynamic-media/previewing-assets.md) .

## Pubblicazione di set di file multimediali diversi {#publishing-mixed-media-sets}

Per informazioni dettagliate su come pubblicare set di file multimediali diversi, consulta [Pubblicazione di risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) .

>[!NOTE]
>
>Se il set di file multimediali diversi non termina completamente nel servizio di consegna al primo momento della pubblicazione, pubblica il set di file multimediali diversi una seconda volta.
