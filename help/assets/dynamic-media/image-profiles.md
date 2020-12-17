---
title: Profili immagine di Dynamic Media
description: Create profili immagine Dynamic Media contenenti impostazioni per maschera di contrasto, ritaglio avanzato, campioni avanzati o entrambi, quindi applicate il profilo a una cartella di risorse immagine.
translation-type: tm+mt
source-git-commit: 59c532d8893f6dc6b94d7ec45a4af87ff1e37fff
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 11%

---


# Profili immagine di Dynamic Media {#image-profiles}

Quando caricate le immagini, potete ritagliare automaticamente l’immagine al momento del caricamento applicando un profilo immagine alla cartella.

>[!IMPORTANT]
>
>I profili immagine non sono applicabili ai file PDF, GIF animata o INDD ( Adobe InDesign).

## Opzioni di ritaglio {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

Le coordinate di ritaglio avanzato dipendono dalle proporzioni. Vale a dire, per le diverse impostazioni di ritaglio avanzato in un profilo immagine, se le proporzioni sono le stesse per le dimensioni aggiunte nel profilo immagine, le stesse proporzioni vengono inviate ad Dynamic Media. Per questo motivo,  Adobe consiglia di utilizzare la stessa area di ritaglio. In questo modo non si verificherà alcun impatto sulle diverse dimensioni utilizzate nel profilo immagine.

Tenete presente che ogni generazione di Smart Crop creata richiede un’elaborazione aggiuntiva. Ad esempio, l’aggiunta di più di cinque proporzioni di SmartCrop può determinare una lenta velocità di assimilazione delle risorse. Può anche causare un maggiore carico sui sistemi. Poiché è possibile applicare Smart Crop a livello di cartella,  Adobe consiglia di utilizzarlo nelle cartelle *solo* in cui è necessario.

Potete scegliere tra due opzioni di ritaglio immagine. Potete anche automatizzare la creazione di campioni di colore e immagini.

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Quando utilizzare</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Ritaglio pixel</td>
   <td>Ritagliate in massa le immagini in base solo alle dimensioni.</td>
   <td><p>Per utilizzare questa opzione, selezionare <strong>Ritaglio pixel</strong> dall'elenco a discesa Opzioni di ritaglio.</p> <p>Per ritagliare dai lati di un’immagine, immettete il numero di pixel da ritagliare da ogni lato o da ciascun lato dell’immagine. La quantità di immagine che viene ritagliata dipende dall’impostazione ppi (pixel per pollice) nel file immagine.</p> <p>Il rendering dei pixel di un profilo immagine viene eseguito nel modo seguente:<br /> </p>
    <ul>
     <li>I valori sono In alto, In basso, A sinistra e A destra.</li>
     <li>In alto a sinistra viene considerato 0,0 e il ritaglio pixel viene calcolato da tale punto.</li>
     <li>Punto di partenza del ritaglio: A sinistra è X e In alto è Y</li>
     <li>Calcolo orizzontale: dimensione in pixel orizzontale dell’immagine originale meno sinistra e quindi meno destra.</li>
     <li>Calcolo verticale: altezza in pixel verticale meno in alto, quindi meno in basso in basso.</li>
    </ul> <p>Ad esempio, supponete di avere un’immagine da 4000 x 3000 pixel. Vengono utilizzati i valori: Top=250, Bottom=500, Left=300, Right=700.</p> <p>Dall’alto a sinistra (300.250) ritagliare utilizzando lo spazio di riempimento di (4000-300-700, 3000-250-500 o 3000.2250).</p> </td>
  </tr>
  <tr>
   <td>Ritaglio avanzato</td>
   <td>Ritagliare in massa le immagini in base al loro punto focale visivo.</td>
   <td><p>Smart Crop utilizza l'intelligenza artificiale di  Adobe Sensei per automatizzare rapidamente il ritaglio delle immagini in massa. Smart Crop rileva e ritaglia automaticamente il punto focale di qualsiasi immagine per catturare il punto di interesse desiderato, indipendentemente dalle dimensioni dello schermo.</p> <p>Per utilizzare Smart Crop, selezionate <strong>Smart Crop</strong> dall'elenco a discesa Opzioni di ritaglio, quindi a destra di Ritaglio immagine reattivo, attivate (attivate) la funzione.</p> <p>Le dimensioni predefinite dei punti di interruzione, grandi, medi e piccoli, coprono in genere l’intera gamma di dimensioni che la maggior parte delle immagini vengono utilizzate su dispositivi mobili e tablet, desktop e banner. Se necessario, potete modificare i nomi predefiniti di Large, Medium e Small.</p> <p>Per aggiungere altri punti di interruzione, fare clic su <strong>Aggiungi ritaglio</strong>; per eliminare un ritaglio, fate clic sull’icona Garbage Can.</p> </td>
  </tr>
  <tr>
   <td>Campione immagine e colore</td>
   <td>Generare in massa un campione immagine per ciascuna immagine.</td>
   <td><p><strong>Nota</strong>: Lo Smart Swatch non è supportato in Dynamic Media Classic.</p> <p>Individuate e generate automaticamente campioni di alta qualità dalle immagini di prodotto che mostrano colore o texture.</p> <p>Per utilizzare il colore e il campione immagine, selezionate <strong>Smart Crop</strong> dall’elenco a discesa Opzioni di ritaglio, quindi a destra del colore e del campione immagine, attivate (attivate) la funzione. Immettete un valore in pixel nelle caselle di testo Larghezza e Altezza.</p> <p>Anche se tutti i ritagli immagine sono disponibili dalla barra Rendering, i campioni vengono utilizzati solo tramite la funzione Copia URL. Per eseguire il rendering del campione sul sito, dovete usare un componente di visualizzazione personalizzato. (L’eccezione a questo è rappresentata dai banner carosello. Dynamic Media fornisce il componente di visualizzazione per il campione usato nei banner del carosello.</p> <p><strong>Utilizzo dei campioni immagine</strong></p> <p>L’URL per i campioni immagine è semplice. Ovvero:</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>dove <code>:Swatch</code> viene aggiunto alla richiesta di risorse.</p> <p><strong>Utilizzo dei campioni colore</strong></p> <p>Per utilizzare i campioni colore, è necessario effettuare una richiesta <code>req=userdata</code> con le seguenti caratteristiche:</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>Ad esempio, di seguito è riportata una risorsa campione in Dynamic Media Classic:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>ed ecco l'URL corrispondente della risorsa campione <code>req=userdata</code>:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>La risposta <code>req=userdata</code> è la seguente:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>Potete anche richiedere una risposta <code>req=userdata</code> in formato XML o JSON, come negli esempi URL seguenti:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## Maschera di contrasto {#unsharp-mask}

Usa **[!UICONTROL Maschera definizione dettagli]** per regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Puoi controllare l’intensità dell’effetto, il raggio in pixel e una soglia di contrasto da ignorare. L’effetto utilizza le stesse opzioni del filtro “Maschera definizione dettagli” di Adobe Photoshop.

>[!NOTE]
>
>La maschera di contrasto viene applicata solo alle rappresentazioni ridimensionate nel PTIFF (piramide tiff) con downsampling superiore al 50%. Ciò significa che le rappresentazioni di grandi dimensioni all’interno del font non vengono influenzate da una maschera di contrasto, mentre le rappresentazioni di dimensioni più piccole, come le miniature, vengono modificate (e mostreranno la maschera di contrasto).

In **[!UICONTROL Maschera di contrasto]** sono disponibili le seguenti opzioni di filtro:

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Quantità</td>
   <td>Controlla la quantità di contrasto applicata ai pixel lungo i bordi. Il valore predefinito è 1,75. Per le immagini ad alta risoluzione, è possibile aumentare la risoluzione fino a 5. Considerate l'importo come una misura dell'intensità del filtro. L'intervallo è 0-5.</td>
  </tr>
  <tr>
   <td>Raggio</td>
   <td>Determina quanti pixel attorno al bordo vengono interessati dalla nitidezza. Per le immagini ad alta risoluzione, inserite un valore da 1 a 2. Un valore basso agisce solo sui pixel del bordo; un valore più elevato agisce su una fascia più ampia di pixel. Il valore adatto dipende dalle dimensioni dell'immagine. Il valore predefinito è 0.2. L'intervallo è compreso tra 0 e 250.</td>
  </tr>
  <tr>
   <td>Soglia</td>
   <td><p>Determina l’intervallo di contrasto da ignorare quando viene applicato il filtro maschera di contrasto. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel di un bordo e quindi resi più nitidi. Per evitare di introdurre disturbo, provate con valori compresi tra 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

La nitidezza è descritta in [Immagini di nitidezza.](/help/assets/dynamic-media/assets/sharpening_images.pdf)

## Creazione di profili immagine Dynamic Media {#creating-image-profiles}

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consultate [Configuring Asset Processing](config-dm.md#configuring-asset-processing) (Configurazione dell&#39;elaborazione delle risorse).

Consultate [I profili immagine e video di Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Vedi anche [Best practice per l&#39;organizzazione delle risorse digitali per l&#39;utilizzo dei profili di elaborazione](/help/assets/dynamic-media/best-practices-for-file-management.md).

**Per creare profili immagine Dynamic Media**

1. Toccate il logo AEM e andate a **[!UICONTROL Strumenti > Risorse > Profili immagine]**.
1. Toccate **[!UICONTROL Crea]** per aggiungere un nuovo profilo immagine.
1. Immettete un nome di profilo e valori per maschera di contrasto, ritaglio o campione oppure per entrambi.

   Potrebbe essere utile utilizzare un nome di profilo specifico per lo scopo previsto. Ad esempio, se desiderate creare un profilo che genera solo i campioni, vale a dire se la funzione Smart Crop è disabilitata (disattivata) e se è attivata (attivata) l’opzione Colore e campione immagine, potete usare il nome di profilo &quot;Smart Swatches&quot;.

   Consulta anche la sezione [Opzioni di ritaglio avanzato e campione avanzato](#crop-options) e [Maschera definizione dettagli](#unsharp-mask).

   ![ritaglio](assets/crop.png)

1. Toccate **[!UICONTROL Salva]**. Il nuovo profilo creato viene visualizzato nell’elenco dei profili disponibili.

## Modifica o eliminazione di profili immagine Dynamic Media {#editing-or-deleting-image-profiles}

1. Toccate il logo AEM e andate a **[!UICONTROL Strumenti > Risorse > Profili immagine]**.
1. Selezionate il profilo immagine da modificare o rimuovere. Per modificarlo, selezionare **[!UICONTROL Modifica profilo elaborazione immagine]**. Per rimuoverlo, selezionare **[!UICONTROL Elimina profilo elaborazione immagine]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. In caso di modifica, salvate le modifiche. Se eliminate, confermate che desiderate rimuovere il profilo.

## Applicazione di un profilo immagine Dynamic Media alle cartelle {#applying-an-image-profile-to-folders}

Quando assegnate un profilo immagine a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. Potete quindi assegnare un solo profilo immagine a una cartella. Considerate quindi attentamente la struttura delle cartelle in cui caricare, memorizzare, usare e archiviare le risorse.

Se a una cartella è stato assegnato un altro profilo immagine, quest’ultimo sostituisce il profilo precedente. Le risorse di cartella esistenti in precedenza restano invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nella scheda.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Potete applicare profili immagine a cartelle specifiche o globalmente a tutte le risorse.

Potete rielaborare le risorse presenti in una cartella che dispone già di un profilo immagine esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Applicazione dei profili immagine Dynamic Media a cartelle specifiche {#applying-image-profiles-to-specific-folders}

È possibile applicare un profilo immagine a una cartella utilizzando il menu **[!UICONTROL Strumenti]** o se si è nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili immagine alle cartelle in entrambi i modi.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Potete rielaborare le risorse in una cartella che dispone già di un profilo video esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Applicazione dei profili immagine Dynamic Media alle cartelle dall&#39;interfaccia utente Profili {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Toccate il logo AEM e andate a **[!UICONTROL Strumenti > Risorse > Profili immagine]**.
1. Selezionate il profilo immagine da applicare a una o più cartelle.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Toccate **[!UICONTROL Applica profilo di elaborazione alle cartelle]** e selezionate la cartella o le cartelle che desiderate utilizzare per ricevere le risorse appena caricate, quindi toccate o fate clic su **[!UICONTROL Applica]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicazione dei profili immagine Dynamic Media alle cartelle da Proprietà {#applying-image-profiles-to-folders-from-properties}

1. Toccate il logo AEM e andate a **[!UICONTROL Risorse]**, quindi alla cartella a cui desiderate applicare un profilo immagine.
1. Sulla cartella, toccare il segno di spunta per selezionarlo, quindi toccare **[!UICONTROL Properties]**.
1. Tocca la scheda **[!UICONTROL Profili immagine]**. Seleziona il profilo dall’elenco a discesa **[!UICONTROL Nome profilo]**, quindi tocca **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Applicazione di un profilo immagine Dynamic Media a livello globale {#applying-an-image-profile-globally}

Oltre ad applicare un profilo a una cartella, potete anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato AEM risorse di qualsiasi cartella sia applicato il profilo selezionato.

Potete rielaborare le risorse in una cartella che dispone già di un profilo video esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Per applicare un profilo immagine Dynamic Media a livello globale**:

1. Effettua una delle operazioni seguenti:

   * Andate a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applicate il profilo appropriato, quindi toccate **[!UICONTROL Salva]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Passa al CRXDE Lite al seguente nodo: `/content/dam/jcr:content`.

      Aggiungete la proprietà `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e toccate **[!UICONTROL Salva tutto]**.

      ![configure_image_profile](assets/configure_image_profiles.png)

## Modifica del ritaglio avanzato o del campione avanzato di una singola immagine {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

Potete riallineare o ridimensionare manualmente la finestra di ritaglio avanzato di un’immagine per perfezionarne ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

Se necessario, potete eseguire nuovamente il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

Vedere anche [Modifica del campione avanzato o avanzato di più immagini](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Per modificare il ritaglio avanzato o il campione avanzato di una singola immagine**

1. Toccate il logo AEM e passate a **[!UICONTROL Risorse]**, quindi alla cartella a cui è stato applicato un profilo immagine di ritaglio avanzato o di campione avanzato.

1. Toccate la cartella per aprirne il contenuto.
1. Toccate l’immagine di cui desiderate regolare il ritaglio avanzato o il campione avanzato.
1. Nella barra degli strumenti, toccare **[!UICONTROL Smart Crop]**.

1. Effettua una delle operazioni seguenti:

   * Nell’angolo superiore destro della pagina, trascinate la barra di scorrimento verso sinistra o destra per aumentare o diminuire rispettivamente la visualizzazione dell’immagine.
   * Sull’immagine, trascinate una maniglia d’angolo per regolare la dimensione dell’area visibile del ritaglio o del campione.
   * Sull’immagine, trascinate la casella o il campione in una nuova posizione. Potete modificare solo i campioni immagine; i campioni colore sono statici.
   * Sopra l&#39;immagine, toccate **[!UICONTROL Ripristina]** per annullare tutte le modifiche e ripristinare il ritaglio o il campione originale.
   * Utilizzare i tasti freccia della tastiera per ritagliare le dimensioni del fotogramma, riposizionare l&#39;immagine o entrambi.

1. Nell&#39;angolo superiore destro della pagina, toccate **[!UICONTROL Salva]**, quindi toccate **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Modifica del ritaglio avanzato o del campione avanzato di più immagini {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Dopo aver applicato a una cartella un profilo immagine contenente lo Smart Crop, a tutte le immagini in quella cartella viene applicato un ritaglio. Se necessario, potete *riallineare o ridimensionare manualmente* la finestra di ritaglio avanzato in più immagini per perfezionare ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

Se necessario, potete eseguire nuovamente il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

**Per modificare il ritaglio avanzato o il campione avanzato di più immagini**

1. Toccate il logo AEM e passate a **[!UICONTROL Risorse]**, quindi a una cartella a cui è applicato un profilo immagine di ritaglio avanzato o di campione avanzato.
1. Sulla cartella, toccare l&#39;icona **[!UICONTROL Altre azioni]** (...), quindi toccare **[!UICONTROL Smart Crop]**.

1. Nella pagina **[!UICONTROL Edit Smart Crops]**, effettuate una delle seguenti operazioni:

   * Regolate le dimensioni di visualizzazione delle immagini sulla pagina.

      A destra dell’elenco a discesa del nome del punto di interruzione, trascinate la barra di scorrimento verso sinistra o destra per modificare le dimensioni della visualizzazione dell’immagine visualizzabile.

      ![edit_smart_packages-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtrare l’elenco di immagini visualizzabili in base ai nomi dei punti di interruzione. Nell’esempio seguente, le immagini vengono filtrate sul nome del punto di interruzione &quot;Medium&quot;.

      Nell’angolo superiore destro della pagina, dall’elenco a discesa, selezionate un nome per punto di interruzione per filtrare le immagini visualizzate. (Vedete l’immagine qui sopra).

      ![edit_smart_Ritagini-elenco a discesa](assets/edit_smart_crops-dropdownlist.png)

   * Ridimensionate la casella di ritaglio avanzato. Effettuate una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio per regolare le dimensioni dell’area visibile del ritaglio.
      * Se l’immagine dispone sia di un ritaglio avanzato che di un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio per regolare le dimensioni dell’area visibile del ritaglio. Oppure, toccate o fate clic sul campione avanzato sotto l’immagine (i campioni colore sono statici), quindi trascinate la maniglia d’angolo della casella di ritaglio per regolare la dimensione dell’area visibile del campione.

      ![Ridimensionamento del ritaglio avanzato di un’immagine.](assets/edit_smart_crops-resize.png)

   * Spostate la casella di ritaglio avanzato. Effettuate una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascinate la casella di ritaglio in una nuova posizione.
      * Se l’immagine dispone sia di un ritaglio avanzato che di un campione avanzato, trascinate la casella di ritaglio avanzato in una nuova posizione. Oppure, toccate o fate clic sul campione avanzato sotto l’immagine (i campioni colore sono statici), quindi trascinate la casella di ritaglio campione avanzato in una nuova posizione.

      ![edit_smart_ritagriturismo](assets/edit_smart_crops-move.png)

   * Annullate tutte le modifiche e ripristinate il ritaglio avanzato o il campione avanzato originale (applicabile solo alla sessione di modifica corrente).

      Toccate **[!UICONTROL Ripristina]** sopra l&#39;immagine.

      ![edit_smart_ritorni-revert](assets/edit_smart_crops-revert.png)



1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva]**. quindi toccate **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Rimozione di un profilo immagine dalle cartelle {#removing-an-image-profile-from-folders}

Quando rimuovete un profilo immagine da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla cartella principale. Tuttavia, l&#39;elaborazione dei file che si è verificata all&#39;interno delle cartelle rimane intatta.

È possibile rimuovere un profilo immagine da una cartella dal menu **[!UICONTROL Strumenti]** o, se si è nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come rimuovere i profili immagine dalle cartelle in entrambi i modi.

### Rimozione di profili immagine Dynamic Media dalle cartelle tramite l&#39;interfaccia utente Profili {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Toccate il logo AEM e andate a **[!UICONTROL Strumenti > Risorse > Profili immagine]**.
1. Selezionate il profilo immagine da rimuovere da una o più cartelle.
1. Tocca **[!UICONTROL Rimuovi profilo elaborazione da cartelle]** e seleziona una o più cartelle da cui vuoi rimuovere il profilo, infine tocca **[!UICONTROL Rimuovi]**.

   Potete confermare che il profilo immagine non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione di profili immagine Dynamic Media dalle cartelle tramite Proprietà {#removing-image-profiles-from-folders-via-properties}

1. Toccate il logo AEM e individuate **[!UICONTROL Risorse]**, quindi la cartella da cui desiderate rimuovere un profilo immagine.
1. Sulla cartella, toccare il segno di spunta per selezionarlo, quindi toccare **[!UICONTROL Properties]**.
1. Selezionate la scheda **[!UICONTROL Profili immagine]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Nome profilo]**, selezionare **[!UICONTROL Nessuno]**, quindi toccare **[!UICONTROL Salva e chiudi]**.

   Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
