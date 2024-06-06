---
title: Best practice per ottimizzare la qualità delle immagini
description: Scopri le best practice per ottimizzare la qualità delle risorse di immagini con Dynamic Medie.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 7820492f462d2b5824e408429332b5adf2e67aab
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# Best practice per ottimizzare la qualità delle immagini {#best-practices-for-optimizing-the-quality-of-your-images}

L&#39;ottimizzazione della qualità delle immagini può richiedere molto tempo, poiché molti fattori contribuiscono al rendering di risultati accettabili. Il risultato è in parte soggettivo perché gli individui percepiscono la qualità dell&#39;immagine in modo diverso. La sperimentazione strutturata è fondamentale.

Adobe Experience Manager include più di 100 comandi Dynamic Medie per la consegna delle immagini che consentono di ottimizzare e ottimizzare le immagini e i risultati del rendering. Le seguenti linee guida possono essere utili per semplificare il processo e ottenere rapidamente buoni risultati utilizzando alcuni comandi essenziali e best practice.

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Abilitare Smart Imaging in Dynamic Medie {#bp-enable-smart-imaging}

**Imaging intelligente:**

* L’abilitazione di Smart Imaging in Dynamic Medie consente di ottimizzare automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.
Vuoi saperne di più? Vai a [Imaging avanzato](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq).
* Migliora le prestazioni di consegna delle immagini regolando dinamicamente questi parametri.
* È possibile valutare Smart Imaging utilizzando lo strumento di autovalutazione [Snapshot](https://snapshot.scene7.com/).

**Formati immagine:**

* Evita l’utilizzo di `fmt=webp` o `fmt=avif` comandi in un URL, a meno che non siano specificatamente necessari per un caso d’uso.
* La tecnologia Smart Imaging seleziona automaticamente il formato migliore, ottimizzando l&#39;ampiezza di banda.

**Comportamento predefinito:**

* Se nell’URL non è specificato alcun comando di formato e Smart Imaging non è abilitato, per impostazione predefinita la consegna delle immagini Dynamic Medie viene eseguita in formato JPEG.

Scegliendo con cognizione di causa i formati delle immagini e abilitando l&#39;imaging avanzato, si può avere un impatto significativo sulle prestazioni e sull&#39;esperienza utente.


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Best practice per selezionare l’immagine sorgente {#bp-select-source-image}

Considerazioni essenziali sull&#39;utilizzo delle immagini di origine:

* **Formato immagine di origine:**
   * L’utilizzo di formati senza perdita di dati come PNG, TIFF o PSD garantisce che la qualità dell’immagine rimanga elevata senza artefatti di compressione.
   * Questi formati conservano tutti i dati originali e li rendono ideali per l&#39;editing e l&#39;ulteriore elaborazione.
* **Dimensione immagine di origine:**
   * Iniziare con un&#39;immagine ad alta risoluzione fornisce più dettagli e flessibilità.
   * Quando le immagini devono essere visualizzate in dimensioni diverse (ad esempio, tra dispositivi o risoluzioni dello schermo), una sorgente di immagine più grande consente una migliore scalabilità.
   * Per le immagini che supportano lo zoom (come le foto di prodotto), mirare a dimensioni di circa 2.000 pixel o più sul lato più lungo.
   * I logo o i banner che non richiedono lo zoom possono essere caricati nella dimensione più grande necessaria per l&#39;uso previsto.

Effettuando queste scelte accurate a livello di origine, puoi contribuire in modo significativo alla qualità complessiva del contenuto visivo.

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## Best practice per le dimensioni delle immagini {#best-practices-for-image-size}

La riduzione dinamica delle dimensioni delle immagini è una delle attività più comuni. Implica di specificare le dimensioni e, facoltativamente, la modalità di downsampling da utilizzare per ridimensionare l’immagine.

* Per il dimensionamento delle immagini, l&#39;approccio migliore e più semplice consiste nell&#39;utilizzare `&wid=<value>` e `&hei=<value>,`o semplicemente `&hei=<value>`. Questi parametri impostano automaticamente la larghezza dell&#39;immagine in base alle proporzioni.
* `&resMode=<value>`controlla l&#39;algoritmo utilizzato per il downsampling. Inizia con `&resMode=sharp2`. Questo valore offre la migliore qualità dell&#39;immagine. Durante il downsampling `value =bilin` è più veloce, spesso determina l’aliasing degli artefatti.

Come best practice per il dimensionamento delle immagini, utilizza `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Procedure consigliate per la nitidezza delle immagini {#best-practices-for-image-sharpening}

La nitidezza delle immagini è l’aspetto più complesso del controllo delle immagini sul sito web e in cui vengono commessi molti errori. Per ulteriori informazioni sul funzionamento della nitidezza e della maschera di contrasto, consultate, ad Experience Manager, le risorse utili riportate di seguito.

* White paper sulle best practice [Tecniche consigliate per la qualità delle immagini e la nitidezza di Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) si applica anche ad Experience Manager.

* Osserva [Utilizzare la nitidezza delle immagini con Experience Manager - Dynamic Medie](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

Ad Experience Manager, puoi rendere più nitide le immagini al momento dell’acquisizione, della consegna o di entrambe. Di solito, tuttavia, è meglio rendere più nitide le immagini utilizzando un solo metodo o l’altro, ma non entrambi. La nitidezza delle immagini alla consegna, su un URL, in genere offre i risultati migliori.

Esistono due metodi per la nitidezza delle immagini:

* Nitidezza semplice ( `&op_sharpen`) - Simile al filtro di nitidezza utilizzato in Photoshop, la nitidezza semplice applica la nitidezza di base alla visualizzazione finale dell&#39;immagine dopo il ridimensionamento dinamico. Tuttavia, questo metodo non è configurabile dall’utente. La best practice prevede di evitare l’utilizzo di `&op_sharpen` a meno che non sia richiesto.
* Maschera di contrasto ( `&op_USM`) - Maschera di contrasto è un filtro di nitidezza standard. La best practice prevede di rendere più nitide le immagini con una maschera di contrasto seguendo le linee guida riportate di seguito. Il mascheramento di contrasto consente di controllare i tre parametri seguenti:

   * `&op_sharpen=`quantità,raggio,soglia

      * **[!UICONTROL quantità]** (0-5, intensità dell&#39;effetto).
      * **[!UICONTROL raggio]** (0-250, larghezza delle &quot;linee di nitidezza&quot; disegnate attorno all&#39;oggetto nitidezza, misurata in pixel).

     Tenete presente che il raggio e la quantità dei parametri funzionano l&#39;uno contro l&#39;altro. La riduzione del raggio può essere compensata aumentando la quantità. Raggio consente un controllo più preciso, poiché un valore inferiore agisce solo sui pixel del bordo, mentre un valore più elevato agisce su una banda di pixel più ampia.

      * **[!UICONTROL soglia]** (0-255, sensibilità dell&#39;effetto).

     Questo parametro determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e che il filtro li renda più nitidi. Il **[!UICONTROL soglia]** Questo parametro consente di evitare l&#39;eccessiva nitidezza delle aree con colori simili, ad esempio i toni della pelle. Ad esempio, con un valore di soglia pari a 12 vengono ignorate le variazioni lievi di luminosità nell&#39;incarnato per evitare di aggiungere &quot;disturbo&quot;, mentre viene aumentato il contrasto lungo i bordi delle aree dove è più presente, ad esempio tra ciglia e pelle.

     Per ulteriori informazioni sull’impostazione di questi tre parametri, comprese le best practice da utilizzare con il filtro, consulta le risorse seguenti:

      * White paper sulle best practice [Tecniche consigliate per la qualità delle immagini e la nitidezza di Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) si applica anche ad Experience Manager.

      * Osserva [Utilizzare la nitidezza delle immagini con Experience Manager - Dynamic Medie](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

      * Experience Manager consente inoltre di controllare un quarto parametro: monocromatico (0,1). Questo parametro determina se la maschera di contrasto viene applicata separatamente a ogni componente di colore utilizzando il valore 0 oppure alla luminosità/intensità dell&#39;immagine utilizzando il valore 1.

Come best practice, inizia con il parametro del raggio della maschera di contrasto. Le impostazioni del raggio che potete iniziare sono le seguenti:

* **[!UICONTROL Sito Web]**: 0,2-0,3 pixel
* **[!UICONTROL Stampa fotografica (250-300 ppi)]**: 0,3-0,5 pixel
* **[!UICONTROL Stampa offset (266-300 ppi)]**: 0,7-1,0 pixel
* **[!UICONTROL Stampa su tela (150 ppi)]**: 1,5-2,0 pixel

Aumentare gradualmente l&#39;importo da 1,75 a 4. Se la nitidezza non è ancora quella desiderata, aumentate il raggio di un punto decimale e rieseguite il valore da 1,75 a 4. Ripetere l&#39;operazione in base alle esigenze.

Lascia il parametro monocromatico impostato su 0.

### Best practice per la compressione JPEF (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Questo parametro controlla la qualità della codifica JPG. Un valore più alto indica un&#39;immagine di qualità superiore ma con dimensioni di file maggiori; in alternativa, un valore più basso indica un&#39;immagine di qualità inferiore ma con dimensioni di file inferiori. L&#39;intervallo per questo parametro è 0-100.
* Per ottimizzare la qualità, non impostate il valore del parametro su 100. La differenza tra un&#39;impostazione di 90 o 95 e 100 è quasi impercettibile. Eppure 100 aumenta inutilmente la dimensione del file di immagine. Pertanto, per ottimizzare la qualità, ma evitare che i file di immagine diventino troppo grandi, impostare `qlt= value` a 90 o 95.
* Per ottimizzare un file immagine di dimensioni ridotte mantenendo la qualità a un livello accettabile, impostare `qlt= value` a 80. Valori inferiori a 70-75 causano un significativo deterioramento della qualità dell&#39;immagine.
* Come best practice, per rimanere al centro, imposta il `qlt= value` a 85 per rimanere al centro.
* Utilizzo del flag chroma in `qlt=`

   * Il `qlt=` Il parametro dispone di una seconda impostazione che consente di attivare il downsampling della cromaticità RGB utilizzando il valore `,1` o disattivato utilizzando il valore `,0`.
   * Per semplificare la procedura, iniziare con il downsampling della cromaticità RGB disattivato (`,0`). Questa impostazione di solito produce una migliore qualità dell&#39;immagine, specialmente per le immagini sintetiche con molti bordi nitidi e contrasto.

Come best practice per la compressione JPG `&qlt=85,0`.

## Best practice per il dimensionamento JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

Il parametro `jpegSize` è utile se si desidera garantire che un&#39;immagine non superi una determinata dimensione per la distribuzione a dispositivi con memoria limitata.

* Questo parametro è impostato in kilobyte (`jpegSize=&lt;size_in_kilobytes&gt;`). Definisce la dimensione massima consentita per la consegna delle immagini.
* `&jpegSize=` interagisce direttamente con il parametro di compressione JPG `&qlt=`. Se la risposta del JPG con il parametro di compressione JPG specificato (`&qlt=`) non supera il valore jpegSize, l’immagine viene restituita con `&qlt=` come definito. Altrimenti, `&qlt=` viene gradualmente ridotta fino a quando l’immagine non rientra nelle dimensioni massime consentite. Oppure, finché il sistema non determina che non può rientrare e restituisce un errore.

Come best practice, imposta `&jpegSize=` e aggiungi il parametro `&qlt=` se si consegnano immagini JPG a dispositivi con memoria limitata.

## Riepilogo delle best practice {#best-practices-summary}

Come best practice, per ottenere una qualità immagine elevata e dimensioni file ridotte, inizia con la seguente combinazione di parametri:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Nella maggior parte dei casi, questa combinazione di impostazioni produce risultati eccellenti.

Se l&#39;immagine richiede un&#39;ulteriore ottimizzazione, regolare gradualmente i parametri di nitidezza (maschera di contrasto) iniziando con un raggio impostato su 0.2 o 0.3. Quindi, aumentare gradualmente l&#39;importo da 1,75 a un massimo di 4 (equivalente al 400% in Photoshop). Verificare che sia stato raggiunto il risultato desiderato.

Se i risultati della nitidezza non sono ancora soddisfacenti, aumentare il raggio con incrementi decimali. Per ogni incremento decimale, riavvia il valore a 1,75 e aumentalo gradualmente a 4. Ripetere questa procedura fino a ottenere il risultato desiderato. Anche se i valori di cui sopra sono un approccio convalidato dagli studi creativi, ricorda che puoi iniziare con altri valori e seguire altre strategie. Se i risultati sono soddisfacenti o meno è una questione soggettiva, quindi la sperimentazione strutturata è fondamentale.

Durante la sperimentazione, i seguenti suggerimenti generali sono utili per ottimizzare il flusso di lavoro:

* Prova e testa diversi parametri in tempo reale, direttamente su un URL.
* Come best practice, ricorda che puoi raggruppare i comandi di Dynamic Medie Image Server in un predefinito per immagini. Un predefinito immagine è fondamentalmente una macro di comando URL con nomi predefiniti personalizzati, ad esempio `$thumb_low$` e `&product_high$`. Il nome del predefinito personalizzato in un percorso URL chiama questi predefiniti. Questa funzionalità consente di gestire i comandi e le impostazioni di qualità per diversi pattern di utilizzo delle immagini sul sito web e di ridurre la lunghezza complessiva degli URL.
* Experience Manager offre inoltre metodi più avanzati per regolare la qualità delle immagini, ad esempio l’applicazione di immagini più nitide al momento dell’acquisizione. Per ottimizzare i risultati del rendering: [Servizi di consulenza Adobe](https://business.adobe.com/customers/consulting-services/main.html) può aiutarti con informazioni approfondite e best practice personalizzate.
