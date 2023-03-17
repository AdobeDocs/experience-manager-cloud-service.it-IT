---
title: Profili immagine di Dynamic Media
description: Scopri come creare profili immagine di Dynamic Media contenenti impostazioni per maschere non nitide, ritaglio avanzato o campione avanzato o entrambi. Quindi, applica il profilo a una cartella di risorse di immagini.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: fa29504ba4abf68131d96a5a8ecbd62b7a9299f9
workflow-type: tm+mt
source-wordcount: '3536'
ht-degree: 8%

---

# Profili immagine di Dynamic Media {#image-profiles}

Quando carichi le immagini, puoi ritagliare automaticamente l’immagine al momento del caricamento applicando un profilo immagine alla cartella.

>[!IMPORTANT]
>
>I profili immagine non sono applicabili ai file PDF, animated GIF o INDD (Adobe InDesign).

## Opzione Maschera definizione dettagli {#unsharp-mask}

Quando crei un profilo immagine, puoi utilizzare la funzione **[!UICONTROL Maschera definizione dettagli]** per regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Puoi controllare l’intensità dell’effetto, il raggio in pixel e una soglia di contrasto da ignorare. Questo effetto utilizza le stesse opzioni del filtro &quot;Maschera definizione dettagli&quot; di Adobe Photoshop.

>[!NOTE]
>
>Maschera definizione dettagli viene applicata solo alle rappresentazioni ridimensionate all’interno del PTIFF (TIFF piramidale) che vengono sottoposte a sottocampionamento superiore al 50%. Ciò significa che le rappresentazioni di grandi dimensioni all’interno del font non sono influenzate da una maschera definizione dettagli. Le rappresentazioni di piccole dimensioni, come le miniature, vengono invece modificate e mostrano la maschera di contrasto.

In **[!UICONTROL Maschera definizione dettagli]**, sono disponibili le seguenti opzioni di filtro:

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Quantità</td>
   <td>Controlla la quantità di contrasto applicata ai pixel del bordo. Il valore predefinito è 1,75. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5. Considera Importo come una misura dell'intensità del filtro. L'intervallo è compreso tra 0 e 5.</td>
  </tr>
  <tr>
   <td>Raggio</td>
   <td>Determina quanti pixel attorno al bordo vengono interessati dalla nitidezza. Per le immagini ad alta risoluzione, inserite un valore da 1 a 2. Un valore basso agisce solo sui pixel del bordo; un valore più elevato agisce su una fascia più ampia di pixel. Il valore adatto dipende dalle dimensioni dell'immagine. Il valore predefinito è 0,2. Intervallo compreso tra 0 e 250.</td>
  </tr>
  <tr>
   <td>Soglia</td>
   <td><p>Determina l'intervallo di contrasto da ignorare quando viene applicato il filtro Maschera definizione dettagli. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e resi più nitidi. Per evitare di introdurre rumore, prova con valori compresi tra 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

La nitidezza è descritta in [Nitidezza delle immagini](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opzioni di ritaglio {#crop-options}

Quando implementi il ritaglio avanzato sulle immagini, Adobe consiglia le seguenti best practice e applica il seguente limite:

| Risorsa - Tipo limite | Best practice | Limite imposto |
| --- | --- | --- |
| **Immagine** - Numero di ritagli avanzati per immagine | 5 | 100 |

Vedi anche [Limiti Dynamic Media](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

Le coordinate di ritaglio avanzato dipendono dalle proporzioni. Per le impostazioni di ritaglio avanzato in un profilo immagine, se le proporzioni sono le stesse per le dimensioni aggiunte nel profilo immagine, le stesse proporzioni vengono inviate a Dynamic Media. Adobe consiglia di utilizzare la stessa area di ritaglio. In questo modo si garantisce che non vi sia alcun impatto sulle diverse dimensioni utilizzate nel profilo immagine.

Per ogni generazione di ritaglio intelligente creata è necessaria un’elaborazione aggiuntiva. Ad esempio, l’aggiunta di più di cinque rapporti di formato di ritaglio avanzato potrebbe causare un tasso di inserimento delle risorse lento. Può anche causare un aumento del carico sui sistemi. Poiché è possibile applicare Smart Crop a livello di cartella, Adobe consiglia di utilizzarlo nelle cartelle *only* dove è necessario.

**Linee guida per la definizione del ritaglio avanzato in un profilo immagine**
Per tenere sotto controllo l’utilizzo di Smart Crop e ottimizzare il tempo di lavorazione e la conservazione delle colture, l’Adobe consiglia le seguenti linee guida e suggerimenti:

* Evita di creare profili di ritaglio avanzati duplicati con gli stessi valori di larghezza e altezza.
* Denomina le colture avanzate in base alle dimensioni di ritaglio, non in base all&#39;utilizzo finale. In questo modo è possibile ottimizzare i duplicati in cui una singola dimensione viene utilizzata su più pagine.
* Crea profili immagine per tipo di pagina/risorsa per cartelle e sottocartelle specifiche invece di un profilo di ritaglio avanzato comune applicato a tutte le cartelle o a tutte le risorse.
* Un profilo immagine applicato alle sottocartelle sostituisce un profilo immagine applicato alla cartella.
* Crea profili immagine per tipo di pagina/risorsa per cartelle e sottocartelle specifiche invece di un profilo di ritaglio avanzato comune applicato a tutte le cartelle o a tutte le risorse.
* Un profilo immagine applicato alle sottocartelle sostituisce un profilo immagine applicato alla cartella.
* Idealmente, puoi utilizzare 10-15 ritagli avanzati per immagine per ottimizzare i rapporti dello schermo e il tempo di elaborazione.

<!--
* Image assets that are going to have a smart crop applied to them must be a minimum of 50 x 50 pixels or larger. CQDOC-20087
* An Image Profile that contains duplicate smart crop dimensions is not permitted. CQDOC-20087
* Duplicate named Image Profiles that have smart crop options set are not permitted. CQDOC-20087
* Create page-wise/asset type-wise Image Profiles for specific folders and subfolders instead of a common smart crop profile that is applied to all folders or all assets.
* An Image Profile that you apply to subfolders overrides an Image Profile that is applied to the folder.
* Ideally, have 10-15 smart crops per image to optimize for screen ratios and processing time. -->
<!-- * Avoid creating duplicate smart crop profiles that have the same width and height values. 
* Name smart crops based on crop dimensions, not on end usage. Doing so helps to optimize for duplicates where a single dimension is used on multiple pages. -->

È possibile scegliere tra due opzioni di ritaglio immagine. È inoltre possibile scegliere di automatizzare la creazione di campioni di colore e immagine o di mantenere il contenuto di ritaglio nelle risoluzioni di destinazione.

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutte le colture e i campioni generati per assicurarsi che siano appropriati e pertinenti per il marchio e i valori.

| Opzione | Quando utilizzare | Descrizione |
| --- | --- | --- |
| **[!UICONTROL Ritaglio pixel]** | Le immagini ritagliate in blocco in base solo alle dimensioni. | Da **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio pixel]**.<br>Per ritagliare dai lati di un’immagine, immetti il numero di pixel da ritagliare da qualsiasi lato o lato dell’immagine. La quantità di immagine ritagliata dipende dall’impostazione ppi (pixel per pollice) nel file di immagine.<br>Il rendering di un ritaglio pixel del profilo immagine avviene nel modo seguente:<br>・ I valori sono Superiore, Inferiore, Sinistra e Destra.<br>・ In alto a sinistra è considerato `0,0` e il ritaglio pixel viene calcolato da lì.<br>・ Punto di partenza del ritaglio: La sinistra è X e la parte superiore è Y<br>・ Calcolo orizzontale: dimensioni pixel orizzontali dell&#39;immagine originale meno sinistro e poi meno destro.<br>・ Calcolo verticale: altezza pixel verticale meno superiore, quindi meno inferiore.<br>Ad esempio, supponiamo di avere un&#39;immagine di 4000 x 3000 pixel. I valori vengono utilizzati: Top=250, Bottom=500, Left=300, Right=700.<br>Dall’alto a sinistra (300.250) ritagliare utilizzando lo spazio di riempimento di (4000-300-700, 3000-250-500, o 3000.2250). |
| **[!UICONTROL Ritaglio avanzato]** | Ritaglio in serie di immagini in base al loro punto focale visivo. | Smart Crop utilizza la potenza dell&#39;intelligenza artificiale in Adobe Sensei per automatizzare rapidamente il ritaglio delle immagini in blocco. Smart Crop rileva e ritaglia automaticamente il punto focale in qualsiasi immagine per acquisire il punto di interesse desiderato, indipendentemente dalle dimensioni dello schermo.<br>Da **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio avanzato]**, poi a destra di **[!UICONTROL Ritaglio immagine reattivo]**, abilita (attiva) la funzione.<br>Le dimensioni predefinite dei punti di interruzione (**[!UICONTROL Grande]**, **[!UICONTROL Media]**, **[!UICONTROL Piccolo]**) copre l&#39;intera gamma di dimensioni che la maggior parte delle immagini vengono utilizzate su dispositivi mobili e tablet, desktop e banner. Se lo desideri, puoi modificare i nomi predefiniti di Grande, Medio e Piccolo.<br>Per aggiungere altri punti di interruzione, seleziona **[!UICONTROL Aggiungi ritaglio]**; per eliminare un ritaglio, seleziona l’icona Garbage Can . |
| **[!UICONTROL Campione immagine e colore]** | Bulk genera un campione immagine per ogni immagine. | **Nota**: Lo Smart Swatch non è supportato in Dynamic Media Classic.<br>Individua e genera automaticamente campioni di alta qualità dalle immagini dei prodotti che mostrano colore o texture.<br>Da **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio avanzato]**. Poi a destra di **[!UICONTROL Colore e campione immagine]**, abilita (attiva) la funzione. Immetti un valore pixel nel **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** caselle di testo.<br>Mentre tutti i ritagli immagine sono disponibili nella barra Rendering , i campioni vengono utilizzati solo tramite **[!UICONTROL Copia URL]** funzionalità. Utilizza il tuo componente di visualizzazione per eseguire il rendering del campione sul sito. L’eccezione a questa regola sono i banner a carosello. Dynamic Media fornisce il componente di visualizzazione per il campione utilizzato nei banner a carosello.<br><br>**Utilizzo dei campioni immagine**<br> L’URL per i campioni immagine è semplice:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Dove `:Swatch` viene aggiunto alla richiesta di risorse.<br><br>**Utilizzo dei campioni colore**<br> Per utilizzare i campioni colore, effettuate una `req=userdata` richiedere quanto segue:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Ad esempio, di seguito è riportata una risorsa campione in Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Ed ecco il corrispondente della risorsa campione `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>La `req=userdata` la risposta è la seguente:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Puoi anche richiedere un `req=userdata` risposta in formato XML o JSON, come nei seguenti esempi URL:<br>・`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>・`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota**: Per richiedere un campione di colore e analizzare il `SmartSwatchColor` , rappresentato da un valore esadecimale RGB a 24 bit.<br>Vedi anche [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) nella Guida di riferimento visualizzatori. |
| **[!UICONTROL Mantieni i contenuti di ritaglio nelle risoluzioni di destinazione]** | Per mantenere il contenuto di ritaglio nelle stesse proporzioni | Da utilizzare per creare un profilo di ritaglio avanzato.<br>Per generare nuovi contenuti di ritaglio, mantenendo comunque il punto focale, per una determinata proporzione tra diverse risoluzioni, deseleziona questa opzione <br>Se deselezioni questa casella, accertati che la risoluzione originale dell’immagine sia maggiore delle risoluzioni definite per il profilo Smart Crop.<br><br>Ad esempio, supponiamo che le proporzioni siano impostate su 600 x 600 (grande), 400 x 400 (medio) e 300 x 300 (piccolo).<br>Quando **[!UICONTROL Mantenere il contenuto raccolto nelle risoluzioni di destinazione]** opzione *controllato*, lo stesso ritaglio viene visualizzato in tutte e tre le risoluzioni, in modo simile al seguente output campione di immagini (solo a scopo illustrativo):<br>![Opzione selezionata](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Quando **[!UICONTROL Mantenere il contenuto raccolto nelle risoluzioni di destinazione]** opzione *non selezionato*, il contenuto di ritaglio è nuovo per tutte e tre le risoluzioni, simile al seguente output di esempio di immagini (solo a scopo illustrativo):<br>![Opzione deselezionata](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Formati di file immagine supportati per ritaglio avanzato e campioni colore

La risoluzione massima supportata del file di input è di 16 K.

>[!NOTE]
>
>La risoluzione 16K è una risoluzione del display con circa 16.000 pixel in orizzontale. La risoluzione 16K più comunemente discussa è di 15360 × 8640, che raddoppia il numero di pixel di 8K UHD in ogni dimensione, per un totale di quattro volte il numero di pixel. Questa risoluzione ha 132,7 megapixel, risoluzione 16 volte superiore a quella 4K e risoluzione 64 volte superiore a quella 1080p.

| Formato immagine | Estensione dei file senza distinzione tra maiuscole e minuscole | Tipo MIME | Spazio colore di ingresso supportato | Dimensione massima del file di input supportato | Formato immagine supportato? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Sì |
| CMYK |  |  |  |  | Sì |
| EPS |  |  |  |  | No |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Sì; per il rendering viene utilizzato il primo fotogramma di GIF animato. Non è possibile configurare o modificare il primo fotogramma. |
| JPEG | `.jpg` e `.jpeg` | image/jpeg | sRGB | 15 GB | Sì |
| PNG | `.png` | image/png | sRGB | 15 GB | Sì |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Sì |
| SVG |  |  |  |  | No |
| TIFF | `.tif` e `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | Sì |
| WebP/Animated WebP |  |  |  |  | No |

## Creare profili immagine Dynamic Media {#creating-image-profiles}

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](config-dm.md#configuring-asset-processing).

Vedi [Informazioni su profili immagine e profili video di Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Vedi anche [Tecniche consigliate per l’organizzazione delle risorse digitali per l’utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).

**Per creare profili immagine Dynamic Media:**

1. Seleziona il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Per aggiungere un profilo immagine, seleziona **[!UICONTROL Crea]**.
1. Inserisci un nome di profilo e valori per maschera non affilata, ritaglio o campione o entrambi.

   Suggerimento: Utilizza un nome di profilo specifico per lo scopo a cui è destinato. Ad esempio, supponi di voler creare un profilo che generi solo campioni. Il ritaglio avanzato è disattivato (disattivato) e il campo Colore e campione immagine è attivato (attivato). In questi casi, puoi utilizzare il nome di profilo &quot;Campioni avanzati&quot;.

   Consulta anche la sezione [Opzioni di ritaglio avanzato e campione avanzato](#crop-options) e [Maschera definizione dettagli](#unsharp-mask).

   ![coltura](assets/crop.png)

1. Seleziona **[!UICONTROL Salva]**. Il nuovo profilo creato viene visualizzato nell’elenco dei profili disponibili.

## Modificare o eliminare i profili immagine di Dynamic Media {#editing-or-deleting-image-profiles}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da modificare o rimuovere. Per modificarlo, seleziona **[!UICONTROL Modifica profilo elaborazione immagine]**. Per rimuoverlo, seleziona **[!UICONTROL Elimina profilo elaborazione immagine]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. In caso di modifica, salva le modifiche. Se si esegue l’eliminazione, confermare la rimozione del profilo.

## Applicare un profilo immagine Dynamic Media alle cartelle {#applying-an-image-profile-to-folders}

Quando assegni un profilo immagine a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla relativa cartella principale. Puoi quindi assegnare un solo profilo immagine a una cartella. Considera attentamente la struttura delle cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo immagine diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è stato assegnato un profilo sono indicate nell’interfaccia utente con il nome del profilo visualizzato nella scheda.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

È possibile applicare profili immagine a cartelle specifiche o globalmente a tutte le risorse.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo immagine esistente che hai successivamente modificato. Vedi [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Applicare profili immagine Dynamic Media a cartelle specifiche {#applying-image-profiles-to-specific-folders}

Puoi applicare un profilo immagine a una cartella dall’interno di **[!UICONTROL Strumenti]** o se ti trovi nella cartella, da **[!UICONTROL Proprietà]**.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. Vedi [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Applicare profili immagine Dynamic Media alle cartelle dall&#39;interfaccia utente Profili {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da applicare a una o più cartelle.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleziona **[!UICONTROL Applica profilo di elaborazione alle cartelle]** e seleziona la cartella o più cartelle da utilizzare per ricevere le risorse appena caricate, quindi seleziona **[!UICONTROL Applica]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili immagine Dynamic Media alle cartelle da Proprietà {#applying-image-profiles-to-folders-from-properties}

1. Tocca il logo Experience Manager e naviga per **[!UICONTROL Risorse]**.
1. Passa a un *cartella* (non una risorsa) a cui applicare un profilo immagine.
1. A seconda della visualizzazione in cui ti trovi, effettua una delle seguenti operazioni:
   * In Vista a schede, posiziona il puntatore sulla cartella, quindi seleziona il segno di spunta per selezionarla.
   * In Vista a colonne o Vista a elenco, seleziona la casella di controllo a sinistra del nome della cartella.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Elaborazione Dynamic Media]** scheda .
1. Sotto **[!UICONTROL Profilo immagine]**, dal **[!UICONTROL Nome profilo]** dall’elenco a discesa, seleziona il profilo da applicare.
1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Applicare un profilo immagine Dynamic Media a livello globale {#applying-an-image-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale. A qualsiasi contenuto caricato in Experience Manager Assets in qualsiasi cartella viene applicato il profilo selezionato.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. Vedi [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Per applicare un profilo immagine Dynamic Media a livello globale:**

1. Effettua una delle operazioni seguenti:

   * Passa a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applicare il profilo appropriato e selezionare **[!UICONTROL Salva]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`.

      Aggiungi la proprietà `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e seleziona **[!UICONTROL Salva tutto]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Modificare il ritaglio avanzato o il campione avanzato di una singola immagine {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutte le raccolte avanzate e i campioni avanzati generati per assicurarsi che siano appropriati e pertinenti per il marchio e i valori.

È possibile riallineare o ridimensionare manualmente la finestra di ritaglio avanzato di un’immagine per perfezionarne ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

>[!IMPORTANT]
>
>Quando riallineate o ridimensionate manualmente la finestra di ritaglio avanzato di una risorsa, la modifica viene mantenuta e mantenuta, anche se successivamente decidete di rielaborare la risorsa. Tuttavia, se modifichi la larghezza, l’altezza o entrambi nel **[!UICONTROL Ritaglio immagine reattivo]** nell’area del profilo immagine, la risorsa viene rielaborata.
>Vedi [Rielaborazione delle risorse Dynamic Media in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Se necessario, potete eseguire di nuovo il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

Vedi anche [Modificare il ritaglio avanzato o il campione avanzato di più immagini](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Per modificare il ritaglio avanzato o il campione avanzato di una singola immagine:**

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Risorse]**, quindi alla cartella a cui è applicato un profilo immagine di ritaglio avanzato o campione avanzato.
1. Per aprirne il contenuto, seleziona la cartella .
1. Selezionate l’immagine di cui desiderate regolare il ritaglio avanzato o il campione avanzato.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Effettua una delle seguenti operazioni:

   * Nell’angolo in alto a destra della pagina, trascinate la barra di scorrimento verso sinistra o verso destra per aumentare o diminuire rispettivamente la visualizzazione dell’immagine.
   * Sull&#39;immagine, trascinate una maniglia d&#39;angolo per regolare le dimensioni dell&#39;area visibile del ritaglio o del campione.
   * Sull’immagine, trascinate la casella o il campione in una nuova posizione. È possibile modificare solo i campioni immagine; i campioni colore sono statici.
   * Sopra l&#39;immagine, seleziona  **[!UICONTROL Ripristina]** per annullare tutte le modifiche e ripristinare il ritaglio o il campione originale.
   * Utilizzare i tasti freccia della tastiera per ritagliare le dimensioni della cornice, riposizionare l&#39;immagine o entrambi.

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Modificare il ritaglio avanzato o il campione avanzato di più immagini {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutte le raccolte avanzate e i campioni avanzati generati per assicurarsi che siano appropriati e pertinenti per il marchio e i valori.

Dopo aver applicato un profilo immagine contenente ritaglio avanzato a una cartella, a tutte le immagini in quella cartella viene applicato un ritaglio. Se lo desideri, puoi *manuale* riallineare o ridimensionare la finestra di ritaglio avanzato in più immagini per perfezionare ulteriormente il punto focale.

Dopo aver modificato e salvato un ritaglio avanzato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

>[!IMPORTANT]
>
>Se si riallinea o ridimensiona manualmente la finestra di ritaglio avanzato per più risorse, le modifiche vengono mantenute anche se successivamente si decide di rielaborare le risorse. Tuttavia, se si modificano la larghezza, l’altezza o entrambe nell’area **[!UICONTROL Ritaglio immagine reattivo]** del profilo immagine, le risorse verranno rielaborate.
>Vedi [Rielaborazione delle risorse Dynamic Media in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Se necessario, potete eseguire di nuovo il ritaglio avanzato per generare di nuovo il raccolto aggiuntivo.

**Per modificare il ritaglio avanzato o il campione avanzato di più immagini:**

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Risorse]**, quindi a una cartella a cui è applicato un profilo immagine di ritaglio avanzato o campione avanzato.
1. Nella cartella, seleziona la **[!UICONTROL Altre azioni]** Icona (..), quindi seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Sulla **[!UICONTROL Modifica ritaglio avanzato]** eseguire una delle operazioni seguenti:

   * Regola le dimensioni di visualizzazione delle immagini sulla pagina.

      A destra dell’elenco a discesa Nome punto di interruzione , trascina la barra di scorrimento a sinistra o a destra per modificare le dimensioni della visualizzazione dell’immagine visualizzabile.

      ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtra l’elenco delle immagini visualizzabili in base ai nomi dei punti di interruzione. Nell’esempio seguente, le immagini vengono filtrate sul nome del punto di interruzione &quot;Medium&quot;.

      Seleziona un nome di punto di interruzione dall’elenco a discesa nell’angolo in alto a destra della pagina per filtrare le immagini visualizzate. (Vedi l&#39;immagine qui sopra).

      ![edit_smart_crop-elenco a discesa](assets/edit_smart_crops-dropdownlist.png)

   * Ridimensiona la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine presenta solo un ritaglio avanzato o un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio. Regolare le dimensioni dell&#39;area visibile del ritaglio.
      * Se l’immagine presenta sia un ritaglio avanzato che un campione avanzato, trascinate sull’immagine la maniglia d’angolo della casella di ritaglio. Regolare le dimensioni dell&#39;area visibile del ritaglio. In alternativa, selezionate il campione avanzato sotto l’immagine (i campioni colore sono statici), quindi trascinate la maniglia d’angolo della casella di ritaglio. Regolare le dimensioni dell’area visibile del campione.

      ![Ridimensionamento del ritaglio avanzato di un’immagine](assets/edit_smart_crops-resize.png).

   * Spostate la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascinate la casella di ritaglio in una nuova posizione.
      * Se l’immagine presenta sia un ritaglio avanzato che un campione avanzato, trascinate la casella di ritaglio avanzato in una nuova posizione. In alternativa, selezionate il campione avanzato sotto l’immagine (i campioni colore sono statici), quindi trascinate la casella di ritaglio campione avanzato in una nuova posizione.

      ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Annulla tutte le modifiche e ripristina il ritaglio avanzato o il campione avanzato originale (applicabile solo alla sessione di modifica corrente).

      Seleziona **[!UICONTROL Ripristina]** sopra l&#39;immagine.

      ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)



1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Rimuovere un profilo immagine dalle cartelle {#removing-an-image-profile-from-folders}

Quando rimuovi un profilo immagine da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, l’elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo immagine da una cartella direttamente da **[!UICONTROL Strumenti]** o se ti trovi nella cartella, da **[!UICONTROL Proprietà]**.

### Rimuovere i profili immagine Dynamic Media dalle cartelle tramite l&#39;interfaccia utente Profili {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleziona il logo dell’Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da rimuovere da una o più cartelle.
1. Seleziona **[!UICONTROL Rimuovi profilo elaborazione da cartelle]** e seleziona la cartella o le cartelle multiple da cui vuoi rimuovere il profilo e seleziona **[!UICONTROL Rimuovi]**.

   Puoi confermare che il profilo immagine non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimuovere i profili immagine Dynamic Media dalle cartelle tramite Proprietà {#removing-image-profiles-from-folders-via-properties}

1. Seleziona il logo dell’Experience Manager e naviga **[!UICONTROL Risorse]** e quindi alla cartella da cui desideri rimuovere un profilo immagine.
1. Nella cartella, selezionare il segno di spunta per selezionarlo, quindi selezionare **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Profili immagine]** scheda .
1. Da **[!UICONTROL Nome profilo]** elenco a discesa, seleziona **[!UICONTROL Nessuno]**, quindi seleziona **[!UICONTROL Salva e chiudi]**.

   Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
