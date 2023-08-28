---
title: Modificare le immagini
description: Modifica le immagini utilizzando le opzioni baate su [!DNL Adobe Photoshop Express] e salva le immagini aggiornate come versioni.
role: User
exl-id: fc21a6ee-bf23-4dbf-86b0-74695a315b2a
source-git-commit: 30b8c9b8eaee6292323dde4b436c29fe8290c910
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 52%

---

# Modificare le immagini in [!DNL Assets view] {#edit-images}

[!DNL Assets view] offre opzioni di modifica intuitive basate su [!DNL Adobe Express] e [!DNL Adobe Photoshop Express]. Le azioni di modifica disponibili tramite [!DNL Adobe Express] sono Ridimensiona immagine, Rimuovi sfondo, Ritaglia immagine e Converti JPEG in PNG.

Dopo aver modificato un’immagine, puoi salvarla come nuova versione. Se necessario, il controllo delle versioni consente di ripristinare la risorsa originale in un secondo momento. Per modificare un&#39;immagine: [apri l’anteprima](/help/assets/navigate-assets-view.md) e fai clic su **[!UICONTROL Modifica immagine]**.

>[!NOTE]
>
>È possibile modificare le immagini dei tipi di file PNG e JPEG utilizzando [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Modifica immagini con Adobi Express {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Integrazione Adobe Express"
>abstract="Strumenti di editing delle immagini semplici e intuitivi basati su Adobi Express disponibili direttamente in AEM Assets per aumentare il riutilizzo dei contenuti e velocizzarne la realizzazione."

### Ridimensionare l’immagine {#resize-image-using-express}

Spesso occorre ridimensionare un’immagine a una dimensione specifica. [!DNL Assets view] consente di ridimensionare rapidamente le immagini per adattarle alle dimensioni comuni delle foto, fornendo nuove risoluzioni precalcolate per dimensioni specifiche. Per ridimensionare l&#39;immagine utilizzando [!DNL Assets view], effettua le seguenti operazioni:

1. Seleziona un’immagine e fai clic su **Modifica**.
2. Clic **[!DNL Resize Image]** dalle azioni rapide disponibili nel riquadro a sinistra.
3. Seleziona la piattaforma di social media appropriata dalla sezione **[!UICONTROL Ridimensiona per]** e selezionare le dimensioni dell&#39;immagine tra le opzioni visualizzate.
4. Ridimensionare l&#39;immagine, se necessario, utilizzando **[!UICONTROL Scala immagine]** campo.
5. Clic **[!DNL Apply]** per applicare le modifiche.
   ![Editing di immagini con Adobi Express](assets/adobe-express-resize-image.png)

   L&#39;immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.
   ![Salva immagine con Adobe Express](assets/adobe-express-resize-save.png)

### Rimuovi sfondo {#remove-background-using-express}

È possibile rimuovere lo sfondo da un&#39;immagine in pochi semplici passaggi, come indicato di seguito:

1. Seleziona un’immagine e fai clic su **Modifica**.
2. Clic **[!DNL Remove Background]** dalle azioni rapide disponibili nel riquadro a sinistra. In Experience Manager Assets l&#39;immagine viene visualizzata senza sfondo.
3. Clic **[!DNL Apply]** per applicare le modifiche.
   ![Salva immagine con Adobe Express](assets/adobe-express-remove-background.png)

   L&#39;immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

### Ritaglia immagine {#crop-image-using-express}

La trasformazione di un&#39;immagine in una dimensione perfetta è facile grazie all&#39;utilizzo di [!DNL Adobe Express] azioni rapide.

1. Seleziona un’immagine e fai clic su **Modifica**.
2. Clic **[!DNL Crop Image]** dalle azioni rapide disponibili nel riquadro a sinistra.
3. Trascina le maniglie sugli angoli dell’immagine per creare il ritaglio desiderato.
4. Fai clic su **[!DNL Apply]**.
   ![Salva immagine con Adobe Express](assets/adobe-express-crop-image.png)
L’immagine ritagliata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

### Converti JPEG in PNG {#convert-jpeg-to-png-using-express}

Potete convertire rapidamente un&#39;immagine JPEG in formato PNG utilizzando Adobi Express. Esegui i seguenti passaggi:

1. Seleziona un’immagine e fai clic su **Modifica**.
2. Clic **[!DNL JPEG to PNG]** dalle azioni rapide disponibili nel riquadro a sinistra.
   ![Converti in PNG con Adobe Express](assets/adobe-express-convert-image.png)
3. Fai clic su **[!UICONTROL Scarica]**.

### Limitazioni {#limitations-adobe-express}

* Risoluzione immagine supportata: minima - 50 pixel, massima - 6000 pixel per dimensione

* Dimensione massima del file supportata: 17 MB

## Modifica immagini tramite [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](//help/navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->

### Correggere immagini al volo {#spot-heal-images-using-photoshop-express}

Se in un’immagine sono presenti piccole macchie o oggetti indesiderati, puoi modificarli e rimuoverli utilizzando il pennello Correzione al volo fornito da Adobe Photoshop.

Il pennello campiona l’area ritoccata e fa sì che i pixel riparati si fondano perfettamente nel resto dell’immagine. Utilizza una dimensione del pennello solo leggermente più grande del punto da correggere.

![Opzione di modifica con correzione al volo](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->

### Ritagliare e raddrizzare le immagini {#crop-straighten-images-using-photoshop-express}

Utilizzando l’opzione di ritaglio e raddrizzamento è possibile eseguire ritaglio di base, ruotare l’immagine, capovolgerla in orizzontale o in verticale e ritagliarla con le dimensioni adatte ai social media più diffusi.

Per salvare le modifiche, fai clic su **[!UICONTROL Ritaglia immagine]**. Dopo la modifica, puoi salvare la nuova immagine come versione.

![Opzione per ritagliare e raddrizzare](assets/edit-crop-straighten.png)

Molte opzioni predefinite consentono di ritagliare l’immagine alle proporzioni più adatte a vari profili e post di social media.

### Ridimensionare l’immagine {#resize-image-using-photoshop-express}

Puoi visualizzare le dimensioni comuni delle foto in centimetri o pollici per conoscerne la grandezza. Per impostazione predefinita, il metodo di ridimensionamento mantiene le proporzioni originali. Per modificare manualmente le proporzioni, fai clic su ![](assets/do-not-localize/lock-closed-icon.png).

Inserisci le dimensioni e fai clic su **[!UICONTROL Ridimensiona immagine]** per ridimensionare l’immagine. Prima di salvare le modifiche come versione, puoi fare clic su [!UICONTROL Annulla] per annullare tutte le modifiche apportate prima di salvarle; oppure, per modificare un passaggio di modifica specifico, fai clic su [!UICONTROL Ripristina].

![Opzioni per ridimensionre un’immagine](assets/resize-image.png)

### Regolare l’immagine {#adjust-image-using-photoshop-express}

[!DNL Assets view] consente di regolare il colore, il tono, il contrasto e molto altro con pochi clic. Fai clic su **[!UICONTROL Regola immagine]** nella finestra di modifica. Nella barra laterale a destra sono disponibili le seguenti opzioni:

* **Popolare**: [!UICONTROL Contrasto e dettagli elevati], [!UICONTROL Contrasto insaturo], [!UICONTROL Foto invecchiata], [!UICONTROL Bianco e nero morbido] e [!UICONTROL Tonalità seppia bianco e nero].
* **Colore**: [!UICONTROL Naturale], [!UICONTROL Luminosità], [!UICONTROL Contrasto elevato], [!UICONTROL Contrasto elevato e dettagli], [!UICONTROL Vivace] e [!UICONTROL Opaco].
* **Creativo**: [!UICONTROL Contrasto insaturo], [!UICONTROL Luce fredda], [!UICONTROL Turchese e rosso], [!UICONTROL Foschia leggera], [!UICONTROL Istante vintage], [!UICONTROL Contrasto caldo], [!UICONTROL Semplice e verde], [!UICONTROL Opacità sollevata rossa], [!UICONTROL Ombre calde] e [!UICONTROL Foto invecchiata].
* **Bianco e nero**: [!UICONTROL Paesaggio bianco e nero], [!UICONTROL Bianco e nero con contrasto elevato], [!UICONTROL Risalto bianco e nero], [!UICONTROL Bianco e nero con contrasto ridotto], [!UICONTROL Bianco e nero semplice], [!UICONTROL Bianco e nero morbido], [!UICONTROL Bianco e nero infrarossi], [!UICONTROL Tonalità selenio bianco e nero], [!UICONTROL Tonalità seppia bianco e nero] e [!UICONTROL Divisioni toni bianco e nero].
* **Vignettatura**: [!UICONTROL Nessuna], [!UICONTROL Chiara], [!UICONTROL Media] e [!UICONTROL Scura].

![Regolare l’immagine con modifiche](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### Passaggi successivi {#next-steps}

* Fornisci feedback sui prodotti utilizzando l’opzione [!UICONTROL Feedback] disponibile nell’interfaccia utente della vista Risorse

* Fornisci feedback alla documentazione utilizzando [!UICONTROL Modifica questa pagina] ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema] ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibile sulla barra laterale destra

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support)

>[!MORELIKETHIS]
>
>* [Visualizzare la cronologia delle versioni di una risorsa](/help/assets/navigate-assets-view.md)
