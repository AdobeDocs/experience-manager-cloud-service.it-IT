---
title: Profili immagine Dynamic Medie
description: Scopri come creare profili immagine Dynamic Medie contenenti impostazioni per maschera di contrasto, ritaglio avanzato, campione avanzato o entrambi. Quindi, applica il profilo a una cartella di risorse immagine.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions,Best Practices
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 35f31c95e92148ff5f3472f26ea9c40fa5a17947
workflow-type: tm+mt
source-wordcount: '3555'
ht-degree: 5%

---

# Profili immagine Dynamic Medie {#image-profiles}

Durante il caricamento delle immagini, puoi ritagliarle automaticamente al momento del caricamento applicando un profilo immagine alla cartella.

>[!IMPORTANT]
>
>I profili immagine non sono applicabili ai file PDF, animated GIF o INDD (Adobe InDesign).

## Maschera definizione dettagli, opzione {#unsharp-mask}

Quando crei un profilo immagine, puoi utilizzare **[!UICONTROL Maschera definizione dettagli]** per regolare con precisione un effetto filtro di nitidezza sull&#39;immagine ricampionata verso il basso finale. È possibile controllare l&#39;intensità dell&#39;effetto, il raggio in pixel e una soglia di contrasto ignorata. Questo effetto utilizza le stesse opzioni del filtro &quot;Maschera definizione dettagli&quot; di Adobe Photoshop.

>[!NOTE]
>
>La maschera di contrasto viene applicata solo alle rappresentazioni ridotte all&#39;interno del file PTIFF (piramide tiff) con ricampionamento verso il basso di oltre il 50%. Ciò significa che le rappresentazioni di dimensioni maggiori all’interno del file PTIFF non sono influenzate da una maschera di contrasto. mentre le rappresentazioni di dimensioni più piccole, come le miniature, vengono modificate (e mostrano la maschera di contrasto).

In entrata **[!UICONTROL Maschera definizione dettagli]**, sono disponibili le seguenti opzioni di filtro:

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Quantità</td>
   <td>Controlla il contrasto applicato ai pixel del bordo. Il valore predefinito è 1,75. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5. Considera Importo come una misura dell’intensità del filtro. L'intervallo è 0-5.</td>
  </tr>
  <tr>
   <td>Raggio</td>
   <td>Determina il numero di pixel circostanti il bordo che influiscono sulla nitidezza. Per le immagini ad alta risoluzione, immettere da 1 a 2. Un valore basso agisce solo sui pixel del bordo; un valore alto agisce su una banda più ampia di pixel. Il valore corretto dipende dalle dimensioni dell'immagine. Il valore predefinito è 0,2. L'intervallo è 0-250.</td>
  </tr>
  <tr>
   <td>Soglia</td>
   <td><p>Determina l'intervallo di contrasto da ignorare quando si applica il filtro Maschera di contrasto. In altre parole, questa opzione determina quanto devono differire i pixel resi più nitidi dall’area circostante prima che vengano considerati pixel del bordo e resi più nitidi. Per evitare di introdurre disturbi, prova con valori compresi tra 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

La nitidezza è descritta in [Nitidezza delle immagini](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opzioni di ritaglio {#crop-options}

Quando implementi il ritaglio avanzato sulle immagini, Adobe consiglia la procedura consigliata di seguito e applica il seguente limite:

| Risorsa - Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| **Immagine** - Numero di ritagli avanzati per immagine | 5 | 100 |

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

Le coordinate di ritaglio avanzato dipendono dalle proporzioni. Per le impostazioni di ritaglio avanzato in un profilo immagine, se le proporzioni sono le stesse per le dimensioni aggiunte nel profilo immagine, le stesse proporzioni vengono inviate a Dynamic Medie. L’Adobe consiglia di utilizzare la stessa area di ritaglio. In questo modo si evita un impatto sulle diverse dimensioni utilizzate nel profilo immagine.

Ogni generazione di ritaglio avanzato creata richiede un’elaborazione aggiuntiva. Ad esempio, l’aggiunta di più di cinque proporzioni di ritaglio avanzato può causare un rallentamento del tasso di acquisizione delle risorse. Può anche causare un aumento del carico sui sistemi. Poiché puoi applicare lo strumento di ritaglio avanzato a livello di cartella, l’Adobe consiglia di utilizzarlo nelle cartelle *solo* dove è necessario.

**Linee guida per definire il ritaglio avanzato in un profilo immagine**
Per tenere sotto controllo l’utilizzo di Smart Crop e ottimizzarne il tempo di elaborazione e la conservazione, l’Adobe consiglia di seguire le linee guida e i suggerimenti seguenti:

* Le risorse immagine a cui verrà applicato un ritaglio avanzato devono essere di almeno 50 x 50 pixel.
* Idealmente, avere 10-15 ritagli intelligenti per immagine per ottimizzare i rapporti dello schermo e il tempo di elaborazione.
* Denomina gli smart crop in base alle dimensioni di ritaglio, non all’utilizzo finale. In questo modo è possibile ottimizzare i duplicati in cui una singola dimensione viene utilizzata su più pagine.
* Crea profili immagine in base al tipo di pagina/risorsa per cartelle e sottocartelle specifiche, anziché un profilo di ritaglio avanzato comune applicato a tutte le cartelle o a tutte le risorse.
* Un profilo immagine applicato alle sottocartelle sostituisce un profilo immagine applicato alla cartella.
* Non è consentito un profilo immagine contenente dimensioni di ritaglio avanzato duplicate.
* I profili immagine con nome duplicato per i quali sono impostate opzioni di ritaglio avanzato non sono consentiti.

Sono disponibili due opzioni di ritaglio immagine: Ritaglio pixel e Ritaglio avanzato. Puoi anche scegliere di automatizzare la creazione di campioni di colore e immagini o di mantenere il contenuto di ritaglio nelle diverse risoluzioni di destinazione.

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutte le colture e i campioni generati per assicurarsi che siano appropriati e pertinenti per il marchio e i valori.

| Opzione | Quando utilizzare | Descrizione |
| --- | --- | --- |
| **[!UICONTROL Ritaglio pixel]** | Ritaglia in blocco le immagini solo in base alle dimensioni. | Dalla sezione **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio pixel]**.<br>Per ritagliare dai lati di un&#39;immagine, immettere il numero di pixel da ritagliare da qualsiasi lato o da ogni lato dell&#39;immagine. La quantità di immagine ritagliata dipende dall&#39;impostazione ppi (pixel per pollice) nel file di immagine.<br>Il ritaglio di un pixel di un profilo immagine viene riprodotto nel modo seguente:<br>· I valori sono Top, Bottom, Left e Right.<br>· Viene considerata la parte superiore sinistra `0,0` e il ritaglio di pixel viene calcolato da lì.<br>· Punto iniziale di ritaglio: X a sinistra e Y in alto<br>· Calcolo orizzontale: dimensioni orizzontali dei pixel dell&#39;immagine originale meno Sinistra e quindi meno Destra.<br>· Calcolo verticale: altezza verticale in pixel meno Superiore e quindi meno Inferiore.<br>Ad esempio, supponiamo di avere un&#39;immagine di 4000 x 3000 pixel. Si utilizzano i seguenti valori: Top=250, Bottom=500, Left=300, Right=700.<br>Dal ritaglio in alto a sinistra (300.250) utilizzando lo spazio di riempimento di (4000-300-700, 3000-250-500 o 3000.2250). |
| **[!UICONTROL Ritaglio avanzato]** | Ritaglia in blocco le immagini in base al loro punto focale visivo. | Smart Crop utilizza la potenza dell’intelligenza artificiale in Adobe Sensei per automatizzare rapidamente il ritaglio di immagini in blocco. Il ritaglio avanzato rileva automaticamente e ritaglia fino al punto focale di qualsiasi immagine per acquisire il punto di interesse desiderato, indipendentemente dalle dimensioni dello schermo.<br>Dalla sezione **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio avanzato]**, quindi a destra di **[!UICONTROL Ritaglio immagine reattivo]**, attiva (attiva) la funzione.<br>Dimensioni predefinite dei punti di interruzione (**[!UICONTROL Grande]**, **[!UICONTROL Medio]**, **[!UICONTROL Piccolo]**) coprono l&#39;intera gamma di dimensioni utilizzate dalla maggior parte delle immagini su dispositivi mobili e tablet, desktop e banner. Se lo si desidera, è possibile modificare i nomi predefiniti di Grande, Medio e Piccolo.<br>Per aggiungere altri punti di interruzione, seleziona **[!UICONTROL Aggiungi ritaglio]**; per eliminare un ritaglio, seleziona l’icona Cestino. |
| **[!UICONTROL Campione colore e immagine]** | Genera un campione di immagine per ogni immagine. | **Nota**: campione avanzato non supportato in Dynamic Media Classic.<br>Individua e genera automaticamente campioni di alta qualità da immagini di prodotti che mostrano colori o texture.<br>Dalla sezione **[!UICONTROL Opzioni di ritaglio]** elenco a discesa, seleziona **[!UICONTROL Ritaglio avanzato]**. Quindi a destra di **[!UICONTROL Campione colore e immagine]**, attiva (attiva) la funzione. Immetti un valore in pixel in **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** caselle di testo.<br>Mentre tutte le ritagli di immagini sono disponibili dalla barra Rappresentazioni, i campioni vengono utilizzati solo tramite **[!UICONTROL Copia URL]** funzionalità. Utilizza il tuo componente di visualizzazione per eseguire il rendering del campione sul tuo sito. L&#39;eccezione a questa regola sono i banner a carosello. Dynamic Medie fornisce il componente visualizzazione per il campione utilizzato nei banner carosello.<br><br>**Utilizzo dei campioni immagine**<br> L&#39;URL per i campioni di immagine è semplice:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Dove `:Swatch` viene aggiunto alla richiesta della risorsa.<br><br>**Utilizzo dei campioni colore**<br> Per utilizzare i campioni colore, è necessario effettuare una `req=userdata` richiede quanto segue:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Di seguito è riportato un esempio di risorsa campione in Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Ed ecco la risorsa campione corrispondente `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>Il `req=userdata` la risposta è la seguente:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Puoi anche richiedere un `req=userdata` risposta in formato XML o JSON, come nei seguenti esempi URL rispettivi:<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota**: per richiedere un campione di colore e analizzare il componente WCM, è necessario creare un componente personalizzato `SmartSwatchColor` attributo, rappresentato da un valore esadecimale RGB a 24 bit.<br>Vedi anche [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) nella Guida di riferimento dei visualizzatori. |
| **[!UICONTROL Mantieni contenuti di ritaglio nelle risoluzioni di destinazione]** | Per mantenere i contenuti di ritaglio con le stesse proporzioni | Utilizza quando crei un profilo di ritaglio avanzato.<br>Per generare nuovi contenuti di ritaglio mantenendo il punto focale per una determinata proporzione in diverse risoluzioni, deseleziona questa opzione <br>Se decidi di deselezionare questa casella, accertati che la risoluzione dell’immagine originale sia maggiore delle risoluzioni definite per il profilo di ritaglio avanzato.<br><br>Ad esempio, supponiamo di aver impostato i rapporti di formato su 600 x 600 (Large), 400 x 400 (Medium) e 300 x 300 (Small).<br>Quando **[!UICONTROL Mantieni contenuti di ritaglio nelle risoluzioni di destinazione]** l&#39;opzione è *selezionato*, lo stesso ritaglio viene visualizzato in tutte e tre le risoluzioni, in modo simile all’output di esempio seguente delle immagini (solo a scopo illustrativo):<br>![Opzione selezionata](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Quando **[!UICONTROL Mantieni contenuti di ritaglio nelle risoluzioni di destinazione]** l&#39;opzione è *non selezionato*, il contenuto di ritaglio è nuovo per tutte e tre le risoluzioni, simile al seguente output di esempio di immagini (solo a scopo illustrativo):<br>![Opzione deselezionata](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Formati di file immagine supportati per Ritaglio avanzato e Campioni colore

La risoluzione massima supportata per le dimensioni dei file di input è di 16K.

>[!NOTE]
>
>La risoluzione 16K è una risoluzione dello schermo con circa 16.000 pixel in orizzontale. La risoluzione 16K più comunemente discussa è 15360 × 8640, che raddoppia il numero di pixel di 8K UHD in ogni dimensione, per un totale di quattro volte il numero di pixel. Questa risoluzione ha 132,7 megapixel, un numero di pixel 16 volte superiore alla risoluzione 4K e un numero di pixel 64 volte superiore alla risoluzione 1080p.

| Formato immagine | Estensione file senza distinzione tra maiuscole e minuscole | Tipo MIME | Spazio colore di input supportato | Dimensione massima file di input supportata | Formato immagine supportato? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Sì |
| CMYK | | | | | Sì |
| EPS | | | | | No |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Sì; per la rappresentazione viene utilizzato il primo fotogramma del GIF animato. Non è possibile configurare o modificare il primo fotogramma. |
| JPEG | `.jpg` e `.jpeg` | image/jpeg | sRGB | 15 GB | Sì |
| PNG | `.png` | image/png | sRGB | 15 GB | Sì |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Sì |
| SVG | | | | | No |
| TIFF | `.tif` e `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | Sì |
| WebP/WebP animato | | | | | No |

## Creare profili immagine Dynamic Medie {#creating-image-profiles}

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](config-dm.md#configuring-asset-processing).

Consulta [Informazioni sui profili immagine e video di Dynamic Medie](/help/assets/dynamic-media/about-image-video-profiles.md).

Vedi anche [Best practice per organizzare le risorse digitali per l’utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).

**Per creare profili immagine Dynamic Medie:**

1. Seleziona il logo Adobe Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Per aggiungere un profilo immagine, seleziona **[!UICONTROL Crea]**.
1. Immettete il nome di un profilo e i valori per maschera di contrasto, ritaglio o campione o entrambi.

   Suggerimento: utilizza un nome di profilo specifico per lo scopo previsto. Ad esempio, supponiamo che si desideri creare un profilo che generi solo campioni. In altre parole, Ritaglio avanzato è disattivato e Campione colore e immagine è attivato. In questi casi, puoi utilizzare il nome del profilo &quot;Campioni avanzati&quot;.

   Consulta anche la sezione [Opzioni di ritaglio avanzato e campione avanzato](#crop-options) e [Maschera definizione dettagli](#unsharp-mask).

   ![ritagliare](assets/crop.png)

1. Seleziona **[!UICONTROL Salva]**. Il profilo creato viene visualizzato nell’elenco dei profili disponibili.

## Modificare o eliminare i profili immagine Dynamic Medie {#editing-or-deleting-image-profiles}

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da modificare o rimuovere. Per modificarlo, seleziona **[!UICONTROL Modifica profilo elaborazione immagine]**. Per rimuoverlo, seleziona **[!UICONTROL Elimina profilo elaborazione immagine]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se stai eseguendo una modifica, salva le modifiche. In caso di eliminazione, conferma di voler rimuovere il profilo.

## Applicare un profilo immagine Dynamic Medie alle cartelle {#applying-an-image-profile-to-folders}

Quando si assegna un profilo immagine a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. È quindi possibile assegnare un solo profilo immagine a una cartella. Considera quindi con attenzione la struttura di cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo immagine diverso a una cartella, il nuovo profilo sostituisce quello precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse che vengono aggiunte alla cartella in un secondo momento.

Le cartelle a cui è assegnato un profilo sono indicate nell’interfaccia utente con il nome del profilo visualizzato nella scheda.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puoi applicare i profili immagine a cartelle specifiche o a livello globale a tutte le risorse.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo immagine modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo averne modificato il profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Applicare profili immagine Dynamic Medie a cartelle specifiche {#applying-image-profiles-to-specific-folders}

È possibile applicare un profilo immagine a una cartella dall’interno di **[!UICONTROL Strumenti]** o se ti trovi nella cartella, da **[!UICONTROL Proprietà]**.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo averne modificato il profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Applicazione dei profili immagine di Dynamic Medie alle cartelle dall’interfaccia utente Profili {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da applicare a una o più cartelle.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleziona **[!UICONTROL Applicare il profilo di elaborazione alle cartelle]** e seleziona la cartella o le cartelle da utilizzare per ricevere le risorse appena caricate, quindi fai clic su **[!UICONTROL Applica]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicare profili immagine Dynamic Medie alle cartelle da Proprietà {#applying-image-profiles-to-folders-from-properties}

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Risorse]**.
1. Passa a *cartella* (non una risorsa) alla quale desideri applicare un profilo immagine.
1. A seconda della vista in cui ti trovi, effettua una delle seguenti operazioni:
   * In Vista a schede, posiziona il puntatore del mouse sulla cartella, quindi seleziona il segno di spunta per selezionarla.
   * In Vista a colonne o Vista a elenco selezionare la casella di controllo a sinistra del nome della cartella.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Elaborazione Dynamic Medie]** scheda.
1. Sotto **[!UICONTROL Profilo immagine]**, dalla **[!UICONTROL Nome profilo]** dall&#39;elenco a discesa, selezionare il profilo da applicare.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Applicare un profilo immagine Dynamic Medie a livello globale {#applying-an-image-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale. A qualsiasi contenuto caricato in Experience Manager Assets in qualsiasi cartella è applicato il profilo selezionato.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo averne modificato il profilo di elaborazione](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Per applicare un profilo immagine Dynamic Medie a livello globale:**

1. Effettua una delle operazioni seguenti:

   * Accedi a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applica il profilo appropriato e seleziona **[!UICONTROL Salva]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * Passa a CRXDE Liti al seguente nodo: `/content/dam/jcr:content`.

     Aggiungi la proprietà `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e seleziona **[!UICONTROL Salva tutto]**.

     ![configure_image_profiles](assets/configure_image_profiles.png)

## Modificare il ritaglio o il campione avanzato di una singola immagine {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutti i ritagli avanzati e i campioni avanzati generati per assicurarti che siano appropriati e pertinenti per il tuo marchio e i tuoi valori.

Puoi riallineare o ridimensionare manualmente la finestra di ritaglio avanzato di un’immagine per perfezionarne ulteriormente il punto focale.

Dopo aver modificato un ritaglio avanzato e aver salvato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

>[!IMPORTANT]
>
>Quando si riallinea o ridimensiona manualmente la finestra di ritaglio avanzato di una risorsa, tale modifica viene mantenuta anche se successivamente si decide di rielaborare la risorsa. Tuttavia, se si modificano la larghezza, l&#39;altezza o entrambe nel **[!UICONTROL Ritaglio immagine reattivo]** del profilo immagine, la risorsa è soggetta a rielaborazione.
>Consulta [Rielaborare le risorse Dynamic Medie in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Se necessario, puoi eseguire nuovamente il ritaglio avanzato per generare di nuovo i ritagli aggiuntivi.

Vedi anche [Modificare il ritaglio o il campione avanzato di più immagini](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Per modificare il ritaglio o il campione avanzato di una singola immagine:**

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Risorse]**, quindi alla cartella a cui è applicato un profilo immagine di ritaglio o campione avanzato.
1. Per aprire il contenuto, seleziona la cartella.
1. Seleziona l’immagine di cui desideri regolare il ritaglio o il campione avanzato.
1. Nella barra degli strumenti, seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Effettua una delle seguenti operazioni:

   * Nell&#39;angolo superiore destro della pagina trascinare la barra di scorrimento verso sinistra o verso destra per aumentare o diminuire la visualizzazione dell&#39;immagine.
   * Sull’immagine, trascina una maniglia d’angolo per regolare le dimensioni dell’area visualizzabile del ritaglio o campione.
   * Sull’immagine, trascina il riquadro/campione in una nuova posizione. Potete modificare solo i campioni immagine; i campioni colore sono statici.
   * Sopra l&#39;immagine, seleziona  **[!UICONTROL Ripristina]** per annullare tutte le modifiche e ripristinare il ritaglio o il campione originale.
   * Utilizzare i tasti freccia della tastiera per ritagliare le dimensioni del frame o riposizionare l&#39;immagine o entrambi.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Modificare il ritaglio o il campione avanzato di più immagini {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>L’Adobe consiglia di esaminare tutti i ritagli avanzati e i campioni avanzati generati per assicurarti che siano appropriati e pertinenti per il tuo marchio e i tuoi valori.

Dopo aver applicato un profilo immagine contenente Ritaglio avanzato a una cartella, a tutte le immagini in tale cartella viene applicato un ritaglio. Se lo desideri, puoi *manualmente* riallineare o ridimensionare la finestra di ritaglio avanzato in più immagini per perfezionare ulteriormente il punto focale.

Dopo aver modificato un ritaglio avanzato e aver salvato, la modifica viene propagata ovunque si utilizzi il ritaglio per le immagini specifiche.

>[!IMPORTANT]
>
>Quando si riallinea o ridimensiona manualmente la finestra di ritaglio avanzato per più risorse, le modifiche vengono mantenute anche se successivamente si decide di rielaborare tali risorse. Tuttavia, se si modificano la larghezza, l’altezza o entrambe nell’area **[!UICONTROL Ritaglio immagine reattivo]** del profilo immagine, le risorse verranno rielaborate.
>Consulta [Rielaborare le risorse Dynamic Medie in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Se necessario, puoi eseguire nuovamente il ritaglio avanzato per generare di nuovo i ritagli aggiuntivi.

**Per modificare il ritaglio o il campione avanzato di più immagini:**

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Risorse]**, quindi a una cartella a cui è applicato un profilo immagine di ritaglio o campione avanzato.
1. Nella cartella, seleziona la **[!UICONTROL Altre azioni]** (...) , quindi seleziona **[!UICONTROL Ritaglio avanzato]**.

1. Il giorno **[!UICONTROL Modifica ritagli avanzati]** eseguire una delle operazioni seguenti:

   * Regola le dimensioni di visualizzazione delle immagini sulla pagina.

     A destra dell&#39;elenco a discesa Nome punto di interruzione, trascinare la barra di scorrimento verso sinistra o verso destra per modificare le dimensioni della visualizzazione dell&#39;immagine visualizzabile.

     ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtra l’elenco delle immagini visualizzabili in base ai nomi dei punti di interruzione. Nell’esempio seguente, le immagini vengono filtrate in base al nome del punto di interruzione &quot;Medium&quot;.

     Dall’elenco a discesa nell’angolo in alto a destra della pagina, seleziona un nome di punto di interruzione per filtrare in base alle immagini visualizzate. (Vedi l’immagine precedente).

     ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Ridimensiona la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascina la maniglia d’angolo della casella di ritaglio sull’immagine. Regola le dimensioni dell’area visibile del ritaglio.
      * Se l&#39;immagine presenta sia un ritaglio avanzato che un campione avanzato, trascinate la maniglia d&#39;angolo della casella di ritaglio. Regola le dimensioni dell’area visibile del ritaglio. In alternativa, seleziona il campione avanzato sotto l’immagine (i campioni di colore sono statici), quindi trascina la maniglia d’angolo della casella di ritaglio. Regola le dimensioni dell&#39;area visualizzabile del campione.

     ![Ridimensionamento del ritaglio avanzato di un’immagine](assets/edit_smart_crops-resize.png).

   * Spostare la casella di ritaglio avanzato. Effettua una delle seguenti operazioni:

      * Se l’immagine dispone solo di un ritaglio avanzato o di un campione avanzato, trascina la casella di ritaglio in una nuova posizione sull’immagine.
      * Se l’immagine dispone sia di un ritaglio avanzato che di un campione avanzato, trascina la casella di ritaglio avanzato in una nuova posizione. In alternativa, seleziona il campione avanzato sotto l’immagine (i campioni di colore sono statici), quindi trascina la casella di ritaglio del campione avanzato in una nuova posizione.

     ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Annulla tutte le modifiche e ripristina il ritaglio avanzato o il campione avanzato originale (si applica solo alla sessione di modifica corrente).

     Seleziona **[!UICONTROL Ripristina]** sopra l&#39;immagine.

     ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Chiudi]** per tornare alla cartella delle risorse.

## Rimuovere un profilo immagine dalle cartelle {#removing-an-image-profile-from-folders}

Quando rimuovi un profilo immagine da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, qualsiasi elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

È possibile rimuovere un profilo immagine da una cartella dall’interno di **[!UICONTROL Strumenti]** o se ti trovi nella cartella, da **[!UICONTROL Proprietà]**.

### Rimuovere i profili immagine di Dynamic Medie dalle cartelle tramite l’interfaccia utente Profili {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleziona il logo di Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili immagine]**.
1. Seleziona il profilo immagine da rimuovere da una o più cartelle.
1. Seleziona **[!UICONTROL Rimuovi profilo elaborazione da cartelle]** e seleziona la cartella o le cartelle da cui vuoi rimuovere il profilo e fai clic su **[!UICONTROL Rimuovi]**.

   Puoi confermare che il profilo immagine non è più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimuovere i profili immagine di Dynamic Medie dalle cartelle tramite Proprietà {#removing-image-profiles-from-folders-via-properties}

1. Seleziona il logo di Experience Manager e naviga **[!UICONTROL Risorse]** e quindi alla cartella da cui desideri rimuovere un profilo immagine.
1. Sulla cartella, seleziona il segno di spunta per selezionarla, quindi fai clic su **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Profili immagine]** scheda.
1. Dalla sezione **[!UICONTROL Nome profilo]** elenco a discesa, seleziona **[!UICONTROL Nessuno]**, quindi seleziona **[!UICONTROL Salva e chiudi]**.

   Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
