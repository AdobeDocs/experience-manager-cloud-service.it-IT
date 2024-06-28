---
title: Modificare le immagini
description: Modifica le immagini utilizzando le opzioni baate su [!DNL Adobe Express] e salva le immagini aggiornate come versioni.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 23b43f22b62451c9d0a5460999fcd43479438d7e
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 33%

---

# Modificare le immagini in [!DNL Assets view] {#edit-images-in-assets-view}

La vista Assets consente di modificare le immagini di base, tra cui ridimensionamento, rimozione dello sfondo, ritaglio e conversione tra i formati JPEG e PNG. Inoltre, permette di realizzare editing avanzato attraverso l&#39;integrazione con Adobe Express. Dopo aver modificato un’immagine, puoi salvarla come nuova versione. Se necessario, il controllo delle versioni consente di ripristinare la risorsa originale in un secondo momento. Per modificare un’immagine: [apri l’anteprima](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets) e fai clic su **Modifica immagine**.

>[!NOTE]
>
>È possibile modificare le immagini PNG e JPEG utilizzando [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Modifica immagine {#edit-image}

Arriva su Assets View, utilizzando il collegamento - [Vista Assets](https://experience.adobe.com/#/assets) e selezionando l’archivio appropriato. Per ricevere l’accesso, contatta l’amministratore della tua organizzazione.
Per ulteriori informazioni di riferimento, fare riferimento a [Introduzione all’utilizzo della visualizzazione Adobe Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Interfaccia utente di visualizzazione di Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation), e [Casi di utilizzo della visualizzazione Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Modifica immagine nella vista Assets tramite Adobe Express {#edit-image-on-assets-view-using-adobe-express}

Dopo aver effettuato l’atterraggio sulla vista Assets, fai clic su **Assets**, selezionare un&#39;immagine e quindi fare clic su **Modifica** dalla barra superiore. Nella nuova schermata vengono visualizzate le opzioni di modifica disponibili, tra cui il ridimensionamento, la rimozione dello sfondo, il ritaglio e la conversione tra i formati JPEG e PNG.

#### Ridimensionare l’immagine {#resize-image-using-express}

Spesso occorre ridimensionare un’immagine a una dimensione specifica. Assets View consente di ridimensionare rapidamente le immagini per adattarle alle dimensioni comuni delle foto, fornendo nuove risoluzioni precalcolate per dimensioni specifiche. Per ridimensionare l&#39;immagine utilizzando Vista Assets, effettuare le seguenti operazioni:

1. Clic **Ridimensiona immagine** dal riquadro di sinistra.
1. Seleziona la piattaforma per social media appropriata dall’elenco a discesa Ridimensiona e scegli le dimensioni dell’immagine dalle opzioni visualizzate.
1. Ridimensiona l’immagine, se necessario, utilizzando il campo **Scala immagine**.
1. Fai clic su **[!UICONTROL Applica]** per applicare le modifiche.
   ![Editing di immagini con Adobe Express](assets/adobe-express-resize-image.png)

   L’immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-resize-save.png)

#### Rimuovere lo sfondo {#remove-background-using-express}

Per rimuovere lo sfondo da un&#39;immagine, effettuare le seguenti operazioni:

1. Clic **Rimuovi sfondo** dal riquadro di sinistra. In Experience Manager Assets l’immagine viene visualizzata senza sfondo.
1. Fai clic su **[!UICONTROL Applica]** per applicare le modifiche.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-remove-background.png)

   L’immagine modificata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

#### Ritagliare un’immagine {#crop-image-using-express}

La trasformazione di un&#39;immagine in una dimensione perfetta è semplice con l&#39;utilizzo di [!DNL Adobe Express] azioni rapide.

1. Clic **[!UICONTROL Ritaglia immagine]** dal riquadro di sinistra.
2. Trascina le maniglie agli angoli dell’immagine per creare il ritaglio desiderato.
3. Fai clic su **[!UICONTROL Applica]**.
   ![Salvare un’immagine con Adobe Express](assets/adobe-express-crop-image.png)
L’immagine ritagliata è disponibile per il download. Puoi salvare la risorsa modificata come nuova versione della stessa risorsa oppure salvarla come nuova risorsa.

#### Converti tra tipi di file immagine {#convert-image-types-using-express}

Potete convertire rapidamente i formati di immagine JPEG e PNG utilizzando Adobe Express. Esegui i passaggi seguenti:

1. Clic **Da JPEG a PNG** o **PNG a JPEG** dal riquadro di sinistra.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. Fai clic su **[!UICONTROL Scarica]**.

#### Limitazioni {#limitations-adobe-express}

* Risoluzione immagine supportata: minima 50 pixel, massima 6000 pixel per dimensione.

* Dimensione file massima supportata: 17 MB.

### Modificare le immagini nell’editor incorporato di Adobe Express {#edit-images-in-adobe-express-embedded-editor}

Gli utenti che dispongono del diritto Express possono utilizzare l’editor Express incorporato nella vista Assets per modificare facilmente i contenuti e crearne di nuovi con GenAI da Adobe Firefly. Ciò migliora il riutilizzo dei contenuti e velocizza la loro esecuzione. Puoi anche utilizzare elementi predefiniti per rendere la risorsa straordinaria o eseguire azioni rapide per modificare l’immagine con pochi clic.
![interfaccia utente express in essentials](/help/assets/assets/express-in-essentials-ui.jpg)
Per modificare le immagini mediante [!DNL Adobe Express] nell’editor incorporato, segui i passaggi seguenti:

1. Accedi alla visualizzazione AEM Assets utilizzando il collegamento - [Vista AEM Assets](https://experience.adobe.com/#/assets) e seleziona l’archivio appropriato.
1. Clic **Assets**, immetti una cartella e seleziona un&#39;immagine.
1. Clic **Apri in Adobe Express**. L’immagine si apre su un’area di lavoro express.
1. Apportare le modifiche necessarie all&#39;immagine.
1. Se il progetto richiede l’aggiunta di altre pagine, fai clic su **Aggiungi**, seleziona le risorse, immetti una cartella, seleziona un’immagine da portare sulla pagina dell’area di lavoro, quindi apporta le modifiche necessarie all’immagine.
1. Per salvare le immagini, fai clic su **Salva**. Viene visualizzata la finestra di dialogo Salva.

   >[!NOTE]
   >
   > **1. Per pagina singola**
   >
   > **Salva come versione:** Questa funzione supporta il salvataggio di una sola risorsa. Selezionate questa opzione per esportare l&#39;immagine come nuova versione (mantenendo il formato originale) e salvarla nella stessa cartella.
   > **Salva come nuova risorsa:** Seleziona questa opzione per esportare la risorsa in un formato diverso da quello originale e salvarla in una cartella come nuova risorsa.
   >  
   > **2. Per più pagine**
   >
   > **Salva come versione:** Questa funzione supporta il salvataggio di una sola risorsa. Se vuoi salvare una singola pagina da più pagine, seleziona questa opzione per salvare la risorsa nel formato e nella posizione originali.\
   > **Salva come nuova risorsa:** Con questa opzione, esportate più risorse o una singola risorsa in qualsiasi cartella e salvatele come nuove risorse con il loro formato di file originale o diverso.

1. Nella finestra di dialogo Salva:
   1. Immetti un nome per il file nella sezione **Salva con nome** campo.
   1. Seleziona una cartella di destinazione.
   1. Facoltativo: fornisci dettagli quali nome del progetto o della campagna, parole chiave, canali, intervallo di tempo e area geografica.
1. Clic **Salva come versione** o **Salva come nuova risorsa** per salvare le risorse.

#### Limitazioni della modifica delle immagini in Express Editor {#limitations-of-editing-images-in-the-express-editor}

* Tipo di file supportato: JPEG o PNG.
* Dimensione file massima supportata: 40 MB.
* Intervallo di larghezza e altezza supportato: tra 50 e 8000 pixel.
* Ricarica la pagina per visualizzare la nuova risorsa salvata più di recente nella cartella di origine.

### Creare nuove risorse con Adobe Express {#create-new-embedded-editor}

[!DNL Assets view] consente di creare un nuovo modello da zero utilizzando l’editor integrato [!DNL Adobe Express]. Per creare una nuova risorsa tramite [!DNL Adobe Express], effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Il mio Workspace]** e fai clic su **[!UICONTROL Crea]** all’interno del banner di Adobe Express visualizzato nella parte superiore. Un’area di lavoro vuota di [!DNL Adobe Express] viene visualizzata all’interno dell’interfaccia utente di [!DNL Assets view].
1. Crea i contenuti utilizzando i [modelli](https://helpx.adobe.com/it/express/using/work-with-templates.html). In caso contrario, passa a **[!UICONTROL Le tue risorse]** per modificare contenuti esistenti.
1. Dopo aver completato la modifica, fai clic su **[!UICONTROL Salva]**.
1. Specifica il percorso di destinazione della risorsa creata e fai clic su **[!UICONTROL Salva come nuova risorsa]**.

#### Limitazioni {#limitations}

* Puoi modificare solo le immagini in formato `JPEG` e `PNG`.
* La dimensione della risorsa deve essere inferiore a 40 MB.
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

* Fornire feedback sul prodotto utilizzando [!UICONTROL Feedback] disponibile nell’interfaccia utente di visualizzazione di Assets.

* Fornisci feedback sulla documentazione utilizzando [!UICONTROL Modifica questa pagina], ![modifica la pagina](assets/do-not-localize/edit-page.png) o [!UICONTROL Segnala un problema], ![crea un problema GitHub](assets/do-not-localize/github-issue.png) disponibili sulla barra laterale a destra.

* Contatta il [Servizio clienti](https://experienceleague.adobe.com/i?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Azioni rapide nell’Adobe Express](https://helpx.adobe.com/it/express/using/resize-image.html)
>* [Visualizzare la cronologia delle versioni di una risorsa](navigate-assets-view.md)
