---
title: Procedure ottimali per ottimizzare la qualità delle immagini
description: Best practice per ottimizzare la qualità delle immagini in Dynamic Media
translation-type: tm+mt
source-git-commit: 21b2541b6a3c5011b6eca7edf85299291c361147

---


# Procedure ottimali per ottimizzare la qualità delle immagini {#best-practices-for-optimizing-the-quality-of-your-images}

L’ottimizzazione della qualità delle immagini può richiedere molto tempo, poiché molti fattori contribuiscono a ottenere risultati accettabili. Il risultato è in parte soggettivo perché gli individui percepiscono la qualità delle immagini in modo diverso. La sperimentazione strutturata è fondamentale.

AEM include più di 100 comandi per la distribuzione di immagini per file multimediali dinamici per ottimizzare le immagini e i risultati di rendering. Le seguenti linee guida possono aiutarti a semplificare il processo e ottenere rapidamente buoni risultati utilizzando alcuni comandi e procedure ottimali essenziali.

## Best practice per il formato immagine (`&fmt=`) {#best-practices-for-image-format-fmt}

* I formati JPG o PNG rappresentano la scelta migliore per la distribuzione di immagini di buona qualità e con dimensioni e peso gestibili.
* Se nell’URL non viene fornito alcun comando di formato, per impostazione predefinita viene utilizzato il formato JPG per la distribuzione delle immagini multimediali dinamiche.
* Il formato JPG si comprime con un rapporto di 10:1 e in genere produce file di dimensioni ridotte. Il formato PNG viene compresso con un rapporto di circa 2:1, tranne in alcuni casi, ad esempio quando le immagini contengono uno sfondo bianco. In genere, tuttavia, i file PNG sono di dimensioni maggiori rispetto ai file JPG.
* Il formato JPG utilizza la compressione con perdita di dati, ossia durante la compressione vengono omessi gli elementi immagine (pixel). Il formato PNG utilizza invece la compressione senza perdita di dati.
* Il formato JPG spesso comprime le immagini fotografiche con una fedeltà migliore rispetto alle immagini sintetiche con bordi netti e contrasto elevato.
* Se le immagini contengono trasparenze, usate il formato PNG perché il formato JPG non supporta la trasparenza.

Come procedura ottimale per il formato immagine, iniziate con l’impostazione più comune `&fmt=JPG`.

## Procedure ottimali per le dimensioni delle immagini {#best-practices-for-image-size}

La riduzione dinamica delle dimensioni delle immagini è una delle attività più comuni. Si tratta di specificare le dimensioni e, facoltativamente, la modalità di downsampling da usare per ridimensionare l’immagine.

* Per il ridimensionamento delle immagini, l’approccio migliore e più semplice consiste nell’usare `&wid=<value>` e `&hei=<value>,`o semplicemente `&hei=<value>`. Questi parametri impostano automaticamente la larghezza dell’immagine in base alle proporzioni.
* `&resMode=<value>`controlla l’algoritmo utilizzato per il downsampling. Cominciate con `&resMode=sharp2`. Questo valore offre la migliore qualità dell’immagine. L’utilizzo del downsampling `value =bilin` è più veloce, ma comporta spesso l’aliasing degli artefatti.

Come procedura ottimale per il ridimensionamento, l’utilizzo `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Procedure ottimali per la nitidezza delle immagini {#best-practices-for-image-sharpening}

La nitidezza delle immagini è l’aspetto più complesso del controllo delle immagini sul sito Web e in cui si verificano numerosi errori. Dedica del tempo a scoprire come funzionano la nitidezza e la maschera di contrasto in AEM, facendo riferimento alle seguenti risorse:

Il white paper sulle procedure ottimali [La nitidezza delle immagini in Adobe Scene7 Publishing System e sul server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf) immagini si applica anche ad AEM.

Su Adobe TV, guardate [Nitidezza di un’immagine con maschera](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html)di contrasto.

Con AEM, potete rendere le immagini più nitide in fase di assimilazione, distribuzione o entrambe. Nella maggior parte dei casi, tuttavia, è necessario rendere le immagini più nitide utilizzando un solo metodo, ma non entrambi. La nitidezza delle immagini al momento della distribuzione, con un URL, offre in genere i risultati migliori.

Esistono due metodi per rendere le immagini più nitide:

* Nitidezza semplice ( `&op_sharpen`): simile al filtro di nitidezza usato in Photoshop, la nitidezza semplice applica la nitidezza di base alla visualizzazione finale dell’immagine dopo il ridimensionamento dinamico. Tuttavia, questo metodo non è configurabile dall’utente. La procedura ottimale è quella di non utilizzare &amp;op_sharpen se non richiesto.
* Maschera di contrasto ( `&op_USM`) - Maschera di contrasto è un filtro di nitidezza standard di settore. La procedura ottimale consiste nel rendere le immagini più nitide con la maschera di contrasto in base alle linee guida riportate di seguito. La maschera di contrasto consente di controllare tre parametri:

   * `&op_sharpen=`amount,radius,threshold

      * **[!UICONTROL amount]** (0-5, intensità dell’effetto).
      * **[!UICONTROL radius]** (0-250, larghezza delle &quot;linee di nitidezza&quot; tracciate attorno all’oggetto, misurata in pixel).

         Ricordate che i parametri radius e amount funzionano l&#39;uno contro l&#39;altro. La riduzione del raggio può essere compensata aumentando la quantità. Raggio consente un controllo più preciso, poiché un valore inferiore rende più nitidi solo i pixel del bordo, mentre un valore più elevato rende più nitida una banda più ampia di pixel.

      * **[!UICONTROL threshold]** (0-255, sensibilità dell’effetto).

         Questo parametro determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel di un bordo, e il filtro li rende più nitidi. Il parametro **[!UICONTROL threshold]** consente di evitare l’eccessiva nitidezza delle aree con colori simili, ad esempio i toni della pelle. Ad esempio, con un valore di soglia pari a 12 vengono ignorate le variazioni lievi di luminosità nell’incarnato per evitare di aggiungere &quot;disturbo&quot;, mentre viene aumentato il contrasto lungo i bordi delle aree con maggior contrasto, ad esempio tra ciglia e pelle.
      Per ulteriori informazioni su come impostare questi tre parametri, comprese le best practice da utilizzare con il filtro, consultate le risorse seguenti:

      Argomento dell’Aiuto di AEM sulla nitidezza di un’immagine.

      White paper sulle procedure ottimali [Nitidezza delle immagini in Adobe Scene7 Publishing System e sul server](/help/assets/dynamic-media/assets/s7_sharpening_images.pdf)immagini.

   * AEM consente inoltre di controllare un quarto parametro: monocromatico (0,1). Questo parametro determina se la maschera di contrasto viene applicata separatamente a ciascun componente di colore utilizzando il valore 0 oppure alla luminosità/intensità dell’immagine utilizzando il valore 1.


Come procedura ottimale, iniziate con il parametro di maschera di contrasto radius. Le impostazioni del raggio con cui potete iniziare sono le seguenti:

* **[!UICONTROL Sito Web]**: 0,2-0,3 pixel
* **[!UICONTROL Stampa fotografica (250-300 ppi)]**: 0,3-0,5 pixel
* **[!UICONTROL Stampa offset (266-300 ppi)]**: 0,7-1,0 pixel
* **[!UICONTROL Stampa su tela (150 ppi)]**: 1,5-2,0 pixel

Aumentare gradualmente l&#39;importo da 1,75 a 4. Se la nitidezza non è ancora quella desiderata, aumentate il raggio di un punto decimale ed eseguite di nuovo il valore da 1,75 a 4. Ripetere l&#39;operazione come necessario.

Lasciate l’impostazione del parametro monocromatico su 0.

### Procedure ottimali per la compressione JPEF (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Questo parametro controlla la qualità di codifica JPG. Un valore più elevato indica un’immagine di qualità superiore ma con un file di grandi dimensioni; in alternativa, un valore inferiore indica un’immagine di qualità inferiore ma una dimensione file inferiore. L&#39;intervallo per questo parametro è compreso tra 0 e 100.
* Per ottimizzare la qualità, non impostate il valore del parametro su 100. La differenza tra un’impostazione di 90 o 95 e 100 è quasi impercettibile, ma 100 aumenta inutilmente la dimensione del file immagine. Pertanto, per ottimizzare la qualità ma evitare che i file di immagine diventino troppo grandi, impostate il valore `qlt= value` su 90 o 95.
* Per ottimizzare un file immagine di dimensioni ridotte ma mantenere la qualità accettabile, impostate il valore su 80. `qlt= value` Con valori inferiori a 70-75 si verifica un notevole degrado della qualità delle immagini.
* Come best practice, per rimanere nel mezzo, impostare il `qlt= value` su 85 per rimanere nel mezzo.
* Utilizzo del flag chroma in `qlt=`

   * Il `qlt=` parametro dispone di una seconda impostazione che consente di attivare il downsampling della cromaticità RGB utilizzando il valore `,1` o disattivandolo con il valore `,0`.
   * Per semplificare le cose, iniziate con il downsampling della cromaticità RGB disattivato (`,0`). Questa impostazione offre in genere una migliore qualità delle immagini, in particolare per le immagini sintetiche con bordi netti e contrasto elevato.

Si consiglia di utilizzare la compressione JPG `&qlt=85,0`.

## Procedure ottimali per il ridimensionamento JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize è un parametro utile per garantire che un’immagine non superi determinate dimensioni per la distribuzione su dispositivi con memoria limitata.

* Questo parametro è impostato in kilobyte (`jpegSize=&lt;size_in_kilobytes&gt;`). Definisce la dimensione massima consentita per la distribuzione delle immagini.
* `&jpegSize=` interagisce con il parametro di compressione JPG `&qlt=`. Se la risposta JPG con il parametro di compressione JPG specificato (`&qlt=`) non supera il valore jpegSize, l&#39;immagine viene restituita con `&qlt=` la definizione. In caso contrario, `&qlt=` viene ridotto gradualmente finché l&#39;immagine non rientra nelle dimensioni massime consentite, oppure finché il sistema non lo determina e restituisce un errore.

Come procedura ottimale, impostate `&jpegSize=` e aggiungete il parametro `&qlt=` se distribuite immagini JPG a dispositivi con memoria limitata.

## Riepilogo delle procedure ottimali {#best-practices-summary}

Per ottenere immagini di alta qualità e file di dimensioni ridotte, si consiglia di utilizzare la seguente combinazione di parametri:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Questa combinazione di impostazioni produce ottimi risultati nella maggior parte delle circostanze.

Se l’immagine richiede un’ulteriore ottimizzazione, regolate gradualmente i parametri di nitidezza (maschera di contrasto) iniziando con un raggio impostato su 0.2 o 0.3. Quindi, aumentate gradualmente l’importo da 1,75 a un massimo di 4 (equivalente a 400% in Photoshop). Verificate che il risultato desiderato sia raggiunto.

Se i risultati della nitidezza non sono ancora soddisfacenti, aumentate il raggio in incrementi decimali. Per ogni incremento decimale, riavviate il valore a 1,75 e aumentatelo gradualmente a 4. Ripetere questa procedura fino a ottenere il risultato desiderato. Anche se i valori sopra riportati sono un approccio convalidato dagli studi creativi, potete iniziare con altri valori e seguire altre strategie. Se i risultati sono soddisfacenti o meno è una questione soggettiva, quindi la sperimentazione strutturata è fondamentale.

Per ottimizzare il flusso di lavoro, potete inoltre trovare utili i seguenti suggerimenti generali:

* Provate a utilizzare parametri diversi in tempo reale, direttamente su un URL o mediante la funzionalità di regolazione delle immagini di Scene7 Publishing System, che fornisce anteprime in tempo reale per le operazioni di regolazione.
* Come procedura ottimale, potete raggruppare i comandi Dynamic Media Image Serving in un predefinito per immagini. Un predefinito per immagini è in pratica una macro di comandi URL con nomi predefiniti personalizzati, ad esempio `$thumb_low$` e `&product_high$`. Il nome del predefinito personalizzato in un percorso URL richiama questi predefiniti. Questa funzionalità consente di gestire comandi e impostazioni di qualità per diversi pattern di utilizzo delle immagini sul sito Web e di ridurre la lunghezza complessiva degli URL.
* AEM offre inoltre metodi più avanzati per ottimizzare la qualità delle immagini, ad esempio l’applicazione della nitidezza alle immagini al momento dell’assimilazione. Per i casi d’uso avanzati in cui questa può rappresentare un’opzione per ottimizzare ulteriormente i risultati di rendering, [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) può aiutarti con approfondimenti personalizzati e procedure ottimali.

