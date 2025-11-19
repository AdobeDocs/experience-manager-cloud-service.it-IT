---
title: Modificare le immagini
description: Modifica le immagini utilizzando le opzioni basate su [!DNL Adobe Express] e salva le immagini aggiornate come versioni.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: cbda4b0735190f0fcaaa1c573e4fc327ab903de1
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 75%

---

# Modificare le immagini in [!DNL Assets view] {#edit-images-in-assets-view}

L’interfaccia utente di visualizzazione di Assets consente di modificare le immagini di base con tecnologia Adobe Express, integrata nell’interfaccia utente. Questa modifica include il ridimensionamento, la rimozione dello sfondo, il ritaglio e la conversione tra i formati JPEG e PNG. Inoltre, consente la modifica avanzata tramite l’interfaccia Adobe Express incorporata nell’interfaccia di visualizzazione Assets.

Dopo aver modificato un’immagine, puoi salvarla come nuova versione. Il controllo delle versioni consente di ripristinare la risorsa originale in un secondo momento, se necessario. Per modificare un’immagine: [apri l’anteprima](https://experienceleague.adobe.com/it/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets) e fai clic su **Modifica immagine**.

>[!NOTE]
>
>È possibile modificare le immagini PNG e JPEG utilizzando [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Editing delle immagini {#edit-image}

Passa all&#39;interfaccia utente di visualizzazione di Assets utilizzando il collegamento [Visualizzazione Assets](https://experience.adobe.com/#/assets) e selezionando l&#39;archivio appropriato. Per ricevere l’accesso, contatta l’amministratore dell’organizzazione.
Per ulteriori informazioni di riferimento, fare riferimento a: [Introduzione all&#39;utilizzo di Adobe Experience Manager Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Interfaccia utente di Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation) e [Casi di utilizzo di Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Modifica immagine nella vista Assets con Adobe Express {#edit-image-on-assets-view-using-adobe-express}

Dopo essere passati alla visualizzazione Assets, fai clic su **Assets**, seleziona un&#39;immagine e quindi fai clic su **Modifica** nella barra superiore. Nella nuova schermata vengono visualizzate le opzioni di modifica disponibili gestite da Adobe Express, tra cui il ridimensionamento, la rimozione dello sfondo, il ritaglio e la conversione tra i formati JPEG e PNG.

#### Ridimensionare l’immagine {#resize-image-using-express}

Spesso occorre ridimensionare un’immagine a una dimensione specifica. Assets View consente di ridimensionare rapidamente le immagini per adattarle alle dimensioni comuni delle foto, fornendo nuove risoluzioni precalcolate per dimensioni specifiche. Per ridimensionare l&#39;immagine utilizzando Vista Assets, effettuare le seguenti operazioni:

1. Fai clic su **Ridimensiona immagine** dal riquadro a sinistra. In una finestra di dialogo vengono visualizzate le funzionalità di ridimensionamento dell’immagine gestite da Adobe Express.
1. Seleziona la piattaforma di social media appropriata dall’elenco a discesa Ridimensiona e seleziona le dimensioni dell’immagine tra le opzioni visualizzate.
1. Ridimensiona l’immagine, se necessario, utilizzando il campo **Scala immagine**.
1. Fai clic su **[!UICONTROL Applica]** per applicare le modifiche.
   ![Editing di immagini con Adobe Express](assets/adobe-express-resize-image.png)

   L’immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-resize-save.png)

#### Rimuovere lo sfondo {#remove-background-using-express}

È possibile rimuovere lo sfondo da un’immagine in pochi semplici passaggi, come indicato di seguito:

1. Fai clic su **Rimuovi sfondo** dal riquadro a sinistra. In Experience Manager Assets l’immagine viene visualizzata senza sfondo.
1. Fai clic su **[!UICONTROL Applica]** per applicare le modifiche.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-remove-background.png)

   L’immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

#### Ritagliare un’immagine {#crop-image-using-express}

Utilizzando alcune azioni rapide di [!DNL Adobe Express], è facile trasformare un’immagine affinché sia di dimensioni perfette.

1. Fai clic su **[!UICONTROL Ritaglia immagine]** dal riquadro a sinistra.
2. Trascina le maniglie agli angoli dell’immagine per creare il ritaglio desiderato.
3. Fai clic su **[!UICONTROL Applica]**.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-crop-image.png)
L’immagine ritagliata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

#### Convertire da JPEG in PNG {#convert-image-types-using-express}

Puoi convertire rapidamente un’immagine JPEG in formato PNG utilizzando Adobe Express. Esegui i passaggi seguenti:

1. Fai clic su **Da JPEG a PNG** o **Da PNG a JPEG** dal riquadro a sinistra.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. Fai clic su **[!UICONTROL Scarica]**.

#### Limitazioni {#limitations-adobe-express}

* Risoluzione immagine supportata: minima 50 pixel, massima 6000 pixel per dimensione.
* Dimensione file massima supportata: 17 MB.

### Modificare le immagine nell’editor integrato Adobe Express {#edit-images-in-adobe-express-embedded-editor}

Gli utenti che dispongono del diritto Express possono utilizzare l’editor Express integrato nella vista Assets per modificare facilmente i contenuti e crearne di nuovi con GenAI di Adobe Firefly. Questa funzione migliora il riutilizzo dei contenuti e ne accelera la velocità. Puoi anche utilizzare elementi predefiniti per migliorare la risorsa o eseguire azioni rapide per modificare l’immagine con pochi clic.

![express nell&#39;interfaccia utente di essentials](/help/assets/assets/express-in-essentials-ui.jpg)
Per modificare le immagini utilizzando l&#39;editor incorporato [!DNL Adobe Express], effettuare le seguenti operazioni:

1. Passa alla visualizzazione AEM Assets utilizzando il collegamento [Visualizzazione AEM Assets](https://experience.adobe.com/#/assets) e seleziona l&#39;archivio appropriato.
1. Fai clic su **Risorse**, immetti una cartella e seleziona un’immagine.
1. Fai clic su **Apri in Adobe Express**. L’immagine si apre in un’area di lavoro Express.
1. Apporta le modifiche necessarie all’immagine.
1. Se il progetto richiede l’aggiunta di ulteriori pagine, fai clic su **Aggiungi**, seleziona Risorse, immetti una cartella, seleziona un’immagine da inserire nella pagina dell’area di lavoro, quindi apporta all’immagine le modifiche necessarie.
1. Per salvare una o più risorse, fai clic su **Salva**. Nella finestra di dialogo Salva vengono visualizzate le opzioni di salvataggio. Per scegliere tra le opzioni di salvataggio, segui una delle istruzioni seguenti che risponda alle tue esigenze:
   1. Per salvare una singola pagina, fai clic su **Salva come versione** per esportare l’immagine come una nuova versione (mantenendo il formato originale) e salvarla nella stessa cartella.

   1. Per salvare una singola pagina, fai clic su **Salva come nuova risorsa** per esportare la risorsa in un formato diverso e salvarla in qualsiasi cartella come una nuova risorsa.

   1. Se vuoi salvare una singola pagina da più pagine, fai clic su **Salva come versione** per salvare la risorsa nel formato e nella posizione originali.

   1. Per salvare più pagine o una singola pagina tra più pagine, fai clic su **Salva come nuova risorsa**. Con questa azione si esportano le risorse singole o multiple in qualsiasi cartella e si salvano come una nuova risorsa o nuove risorse nel formato originale o in un formato diverso.

1. Nella finestra di dialogo Salva:
   1. Immetti un nome per il file nel campo **Salva con nome**.
   1. Seleziona una cartella di destinazione.
   1. Facoltativo: fornisci dettagli quali nome del progetto o della campagna, parole chiave, canali, arco temporale e area geografica.
1. Fai clic su **Salva come versione** o **Salva come nuova risorsa** per salvare le risorse.

#### Limitazioni della modifica delle immagini nell’editor di Express {#limitations-of-editing-images-in-the-express-editor}

* Tipo di file supportato: JPEG o PNG.
* Dimensione file massima supportata: 40 MB.
* Intervallo di larghezza e altezza supportato: 65MP (ad esempio, 8K x 8K o 16K x 4K).
* Ricarica la pagina per visualizzare l’ultima nuova risorsa salvata nella cartella di origine.

### Creare nuove risorse con Adobe Express {#create-new-embedded-editor}

[!DNL Assets view] consente di creare un nuovo modello da zero utilizzando l’editor integrato [!DNL Adobe Express]. Per creare una nuova risorsa tramite [!DNL Adobe Express], effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Il mio Workspace]** e fai clic su **[!UICONTROL Crea]** all&#39;interno del banner di Adobe Express visualizzato nella parte superiore. Un’area di lavoro vuota di [!DNL Adobe Express] viene visualizzata all’interno dell’interfaccia utente di [!DNL Assets view].
1. Crea i contenuti utilizzando i [modelli](https://helpx.adobe.com/it/express/using/work-with-templates.html). In caso contrario, passa a **[!UICONTROL Le tue risorse]** per modificare contenuti esistenti.
1. Dopo aver completato la modifica, fai clic su **[!UICONTROL Salva]**.
1. Specifica il percorso di destinazione per la risorsa creata e fai clic su **[!UICONTROL Salva come nuova risorsa]**.

#### Limitazioni {#limitations}

* Puoi modificare solo le immagini in formato `JPEG` e `PNG`.
* La dimensione della risorsa deve essere inferiore a 80 MB per i dispositivi desktop e a 40 MB per i dispositivi mobili.
* La gamma di larghezza e altezza supportata è di 65 MP (ad esempio, 8K x 8K o 16K x 4K).
* Puoi salvare un’immagine in formato `PDF`, `JPEG` o `PNG`.

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### Passaggi successivi {#next-steps}

* Fornisci feedback sul prodotto utilizzando l&#39;opzione [!UICONTROL Feedback] disponibile nell&#39;interfaccia utente di visualizzazione di Assets.

* Fornisci feedback sulla documentazione utilizzando [!UICONTROL Modifica questa pagina], ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema], ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibili sulla barra laterale a destra.

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/it?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Azioni rapide in Adobe Express](https://helpx.adobe.com/it/express/using/resize-image.html)
>* [Visualizzare la cronologia delle versioni di una risorsa](navigate-assets-view.md)
