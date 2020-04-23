---
title: Smart imaging
description: La tecnologia di imaging intelligente sfrutta le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento.
translation-type: tm+mt
source-git-commit: a934f28f74f0ff9ae68d7507290851dc5ca907e5

---


# Imaging avanzato {#smart-imaging}

## Cos&#39;è &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

La tecnologia Smart Imaging sfrutta le funzionalità di Adobe Sensei AI e lavora con i &quot;predefiniti per immagini&quot; esistenti per migliorare le prestazioni di distribuzione delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

La funzione Smart Imaging offre inoltre un ulteriore vantaggio in termini di prestazioni grazie all&#39;integrazione completa con il servizio CDN premium di Adobe. Questo servizio trova la via Internet ottimale tra server, reti e punti di peering con latenza minima e/o tasso di perdita dei pacchetti rispetto alla route predefinita su Internet.

Gli esempi di risorse di immagine seguenti descrivono l’ottimizzazione per Smart Imaging aggiunta:

| Image<br>(URL) | Miniatura    | Dimensioni<br> (JPEG) | Dimensioni (WebP)<br> (con Smart Imaging) | % riduzione |
|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Media = 51% |

Come già detto, Adobe ha anche eseguito un test con 7009 URL da siti di clienti live, e ha raggiunto una media di 38% di ottimizzazione ulteriore delle dimensioni dei file per JPEG e 31% di ottimizzazione aggiuntiva delle dimensioni dei file per PNG con formato WebP, grazie alla capacità di Smart Imaging.

## Quali sono i vantaggi principali dell&#39;ultima generazione di Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

Poiché le immagini costituiscono la maggior parte del tempo di caricamento di una pagina, il miglioramento delle prestazioni può avere un impatto profondo sui KPI aziendali, come conversione più elevata, tempo trascorso sul sito e tasso di bounce inferiore del sito.

Miglioramenti nell&#39;ultima versione di Smart Imaging:

* Consente di distribuire immediatamente contenuti ottimizzati (in fase di esecuzione).
* Utilizza la tecnologia Adobe Sensei per la conversione in base alla qualità (qlt) specificata nella richiesta di immagini.
* La funzione Smart Imaging può essere disattivata utilizzando il parametro URL &quot;bfc&quot;.
* TTL (Time To Live) indipendente. Precedentemente, era obbligatorio un limite minimo di 12 ore per l&#39;utilizzo di Smart Imaging.
* Precedentemente, sia le immagini originali che quelle derivate erano memorizzate nella cache, ed era un processo in due fasi per annullare la validità della cache. Nella versione più recente di Smart Imaging, solo i derivati vengono memorizzati nella cache, consentendo un singolo processo di annullamento della validità della cache.
* I clienti che utilizzano intestazioni personalizzate nel set di regole (ad esempio, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot; come suggerito in [Aggiunta di un valore intestazione personalizzato alle risposte alle immagini|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) trarranno vantaggio dall’ultima Smart Imaging, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart Imaging.

## Esistono costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. La funzione Smart Imaging è inclusa nella licenza esistente di Dynamic Media Classic (Scene7) o AEM Dynamic Media (On Prem, AMS e AEM come servizio Cloud).

>[!NOTE]
>
>La funzione Smart Imaging non è disponibile per i clienti di Dynamic Media - Hybrid.


## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Smart Imaging utilizza Adobe Sensei per convertire automaticamente le immagini nel formato, nelle dimensioni e nella qualità ottimali, in base alla capacità del browser:

* Converti automaticamente in WebP per browser quali Chrome, Firefox, Microsoft Edge, Android e Opera.
* Converti automaticamente in JPEG2000 per browser come Safari.
* Converti automaticamente in JPEG per browser come Internet Explorer 9+.
* Per i browser che non supportano questi formati, viene distribuito il formato immagine originariamente richiesto.

Se le dimensioni dell&#39;immagine originale sono inferiori a quelle generate da Smart Imaging, viene trasmessa l&#39;immagine originale.

## Quali formati immagine sono supportati? {#what-image-formats-are-supported}

I seguenti formati di immagine sono supportati per le immagini intelligenti:
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Come funziona l’imaging avanzato con i predefiniti per immagini già in uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging funziona con i &quot;predefiniti per immagini&quot; esistenti e osserva tutte le impostazioni delle immagini, ad eccezione di qualità (qlt) e formato (fmt), se il formato file richiesto è JPEG o PNG. Per la conversione del formato, manteniamo la fedeltà visiva completa, come definito dalle impostazioni del predefinito per immagini, ma con file di dimensioni inferiori. Se le dimensioni originali dell&#39;immagine sono inferiori a quelle generate da Smart Imaging, viene trasmessa l&#39;immagine originale.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Dovrò cambiare URL, predefiniti per immagini o distribuire un nuovo codice sul mio sito per Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

No. Le immagini intelligenti si integrano perfettamente con gli URL esistenti e con i predefiniti per immagini. Inoltre, per rilevare il browser di un utente non è necessario aggiungere codice al sito Web. Tutto questo viene gestito automaticamente.

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

Vedete [Posso usare le Smart Imaging?](#am-i-eligible-to-use-smart-imaging) per comprendere i prerequisiti per la funzione Smart Imaging.

## Smart Mmaging funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart Imaging funziona con immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Posso utilizzare la tecnologia di imaging intelligente? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare le immagini intelligenti, l’account della società Dynamic Media Classic o Dynamic Media su AEM deve soddisfare i seguenti requisiti:

* Utilizzate la rete CDN (Content Delivery Network) inclusa nel pacchetto Adobe come parte della licenza.
* Utilizzate un dominio dedicato (ad esempio `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

Per trovare i domini, accedi al tuo account o account della società.

Tap **[!UICONTROL Setup > Application Setup > General Settings]**. Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato. Se utilizzate un dominio generico, potete richiedere il passaggio al vostro dominio personalizzato come parte di questa transizione quando inviate un ticket di assistenza tecnica.

Il primo dominio personalizzato non prevede costi aggiuntivi con una licenza per contenuti multimediali dinamici.

## Qual è la procedura per attivare la funzione Smart Imaging per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

È necessario avviare la richiesta per utilizzare l&#39;imaging intelligente; non è abilitata automaticamente.

1. Avviate una richiesta di assistenza tecnica (e-mail: `s7support@adobe.com`).
1. Nella richiesta di assistenza, fornite le seguenti informazioni:

   1. Nome contatto principale, email, telefono.
   1. Tutti i domini da abilitare per l&#39;imaging intelligente (ossia `images.company.com` o `mycompany.scene7.com`).

      Per trovare i domini, accedi al tuo account o account della società.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato.
   1. Verifica di utilizzare la CDN tramite Adobe e di non essere gestito con una relazione diretta.
   1. Verifica di utilizzare un dominio dedicato, ad esempio `images.company.com` o `mycompany.scene7.com`, e non un dominio generico, ad esempio `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, accedi al tuo account o account della società.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato. Se utilizzate un dominio Dynamic Media Classic generico, potete richiedere il passaggio al dominio personalizzato come parte di questa transizione.
   1. Indicate se è necessario utilizzare anche questo metodo su HTTP/2.

1. Il supporto tecnico vi aggiunge all&#39;Elenco di attesa clienti Smart Imaging in base all&#39;ordine in cui sono state inviate le richieste.
1. Quando Adobe sarà pronta a gestire la richiesta, il supporto vi contatterà per coordinare e impostare una data di destinazione.
1. **Facoltativo**: Potete provare l&#39;imaging intelligente in Fase di sviluppo prima che Adobe introduca la nuova funzione in produzione.
1. Una volta completato il corso, riceverete una notifica.
1. Per ottimizzare le prestazioni delle Smart Imaging, Adobe consiglia di impostare il tempo di trasmissione (TTL) su 24 ore o più. Il TTL definisce il tempo in cui le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzate Dynamic Media Classic, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server]** immagini. Impostate il valore **[!UICONTROL Default Cache Time To Live]** (Tempo cache client predefinito su Live) su 24 o più.
   1. Se utilizzate Contenuti multimediali dinamici, seguite [queste istruzioni](config-dm.md). Impostate il valore **[!UICONTROL Scadenza]** su 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dal supporto tecnico, in base all&#39;Elenco di attesa.

>[!NOTE]
Il tempo di attesa potrebbe essere lungo, perché l&#39;attivazione di Smart Imaging implica la cancellazione della cache da parte di Adobe. Pertanto, è possibile gestire solo alcune transizioni cliente in un dato momento.

## Quali sono i rischi legati al passaggio all&#39;immagine per l&#39;utilizzo di Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Non c&#39;è alcun rischio per una pagina Web del cliente. Tuttavia, tenete presente che la transizione a Smart Imaging elimina la cache della rete CDN perché comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media su AEM.

Durante la transizione iniziale, le immagini non memorizzate nella cache arrivano direttamente sui server di origine Adobe fino a quando la cache non viene ricreata. Per questo motivo, Adobe pianifica di gestire alcune transizioni tra clienti alla volta, in modo da mantenere prestazioni accettabili quando si richiamano richieste dalla nostra origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente alla rete CDN entro circa 1-2 giorni.

## Come posso verificare se la funzione di imaging intelligente funziona come previsto?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato l’account con l’imaging intelligente, caricate nel browser l’URL di un elemento multimediale dinamico Classic (Scene7)/immagine multimediale dinamico.
1. Aprite il riquadro per gli sviluppatori di Chrome facendo clic su **[!UICONTROL Visualizza > Sviluppatore > Strumenti]** per sviluppatori nel browser. Oppure, scegliete uno strumento di sviluppo browser a vostra scelta.

1. Verificate che la cache sia disattivata quando gli strumenti di sviluppo sono aperti.

   * In Windows: individuate le impostazioni nel riquadro dello strumento di sviluppo, quindi selezionate la casella di controllo **[!UICONTROL Disattiva cache (mentre è aperto il dispositivo)]** .
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un&#39;immagine PNG convertita dinamicamente in WebP su Chrome.
1. Ripetete questo test su diversi browser e condizioni utente.

>[!NOTE]
Non tutte le immagini sono convertite. La funzione Smart Imaging decide se la conversione è necessaria per migliorare le prestazioni. In alcuni casi, se non si prevede alcun guadagno di prestazioni o se il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## È possibile disattivare la funzione Smart Imaging per qualsiasi richiesta? {#turning-off-smart-imaging}

Sì. Per disattivare l’immagine avanzata, aggiungete il modificatore `bfc=off` all’URL.

## Quale &quot;tuning&quot; è disponibile? Esistono impostazioni o comportamenti che possono essere definiti? (#tuning-settings)

Attualmente, è possibile attivare o disattivare l&#39;imaging avanzato. Non sono disponibili altre impostazioni di sintonizzazione.

## Se Smart Imaging gestisce le impostazioni di qualità, è possibile impostare valori minimi e massimi? Ad esempio, è possibile impostare &quot;non inferiore a 60&quot; e &quot;non superiore a 80 qualità&quot;? (#Minimum-Maximum)

L&#39;attuale funzione di provisioning di Smart Imaging non è disponibile.

## In alcuni casi, un&#39;immagine JPEG viene restituita a Chrome invece di un&#39;immagine WebP. Perché succede? (#jpeg-webp)

La funzione di imaging intelligente determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione restituisce un file di dimensioni inferiori con qualità comparabile.
