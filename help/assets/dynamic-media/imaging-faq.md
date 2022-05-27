---
title: Smart imaging
description: Scopri come l’imaging intelligente con Adobe Sensei AI applica le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, ottenendo prestazioni e coinvolgimento migliori.
feature: Asset Management,Renditions
role: User
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 743782e2716aa79491adee2f32da6d746bcc40a7
workflow-type: tm+mt
source-wordcount: '2629'
ht-degree: 1%

---

# Imaging avanzato {#smart-imaging}

## Cos’è l’imaging intelligente? {#what-is-smart-imaging}

La tecnologia Smart Imaging applica le funzionalità di Adobe Sensei AI e funziona con i &quot;predefiniti immagine&quot; esistenti. Funziona per migliorare le prestazioni di distribuzione delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

>[!IMPORTANT]
>
>L’imaging avanzato richiede l’utilizzo della rete CDN preconfigurata (Content Delivery Network) fornita in bundle con Adobe Experience Manager - Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

L’imaging intelligente trae inoltre vantaggio dal miglioramento delle prestazioni dell’integrazione completa con il servizio premium CDN (Content Delivery Network) di Adobe. Questo servizio trova il percorso Internet ottimale tra server, reti e punti di peer. Trova un percorso che ha la latenza più bassa e la velocità di perdita più bassa del pacchetto invece di utilizzare il percorso predefinito su Internet.

Gli esempi di risorse immagine seguenti illustrano l’ottimizzazione Smart Imaging aggiunta:

| Immagine<br>(URL) | Miniatura  | Dimensione<br> (JPEG) | Dimensioni (WebP)<br> (con Smart imaging) | Riduzione del % |
|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Media = 51% |

Simile a quanto sopra, Adobe ha anche eseguito un test con 7009 URL dai siti dei clienti live. Sono stati in grado di ottenere in media un ulteriore ottimizzazione del 38% delle dimensioni dei file per JPEG. Per PNG con formato WebP, sono stati in grado di raggiungere una media di 31% ulteriore ottimizzazione delle dimensioni del file. Questo tipo di ottimizzazione è possibile grazie alla capacità di Smart imaging.

Sul web mobile, le sfide sono aggravate da due fattori:

* Ampia varietà di dispositivi con diversi fattori di forma e display ad alta risoluzione.
* Larghezza di banda di rete vincolata.

In termini di immagini, l&#39;obiettivo è quello di offrire immagini di qualità ottimale nel modo più efficiente possibile.

### Informazioni sull’ottimizzazione del rapporto pixel del dispositivo {#dpr}

Il rapporto pixel del dispositivo (DPR), noto anche come rapporto pixel CSS, è la relazione tra i pixel fisici di un dispositivo e i pixel logici. Soprattutto con l&#39;avvento degli schermi Retina, la risoluzione dei pixel dei moderni dispositivi mobili sta crescendo a un ritmo veloce.

Attivando l’ottimizzazione del rapporto pixel del dispositivo, l’immagine viene riprodotta alla risoluzione nativa dello schermo, che la rende più nitida.

Attivando la configurazione di Smart imaging DPR, l&#39;immagine richiesta viene regolata automaticamente in base alla densità di pixel del display da cui viene servita la richiesta. Attualmente, la densità di pixel del display proviene dai valori di intestazione CDN di Akamai.

| Valori consentiti nell’URL di un’immagine | Descrizione |
|---|---|
| `dpr=off` | Disattiva l’ottimizzazione DPR a livello di singolo URL immagine. |
| `dpr=on,dprValue` | Sostituisci il valore DPR rilevato da Smart Imaging con un valore personalizzato (rilevato da qualsiasi logica lato client o con altri metodi). Valore consentito per `dprValue` è un numero qualsiasi maggiore di 0. I valori specificati di 1.5, 2 o 3 sono tipici. |

>[!NOTE]
>
>* È possibile utilizzare `dpr=on,dprValue` anche se l’impostazione DPR a livello aziendale è disattivata.
>* Grazie all’ottimizzazione DPR, quando l’immagine risultante è maggiore dell’impostazione MaxPix Dynamic Media, la larghezza MaxPix viene sempre riconosciuta mantenendo le proporzioni dell’immagine.


| Dimensione immagine richiesta | Valore DPR | Dimensione dell&#39;immagine |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632x1000 |

Vedi anche [Quando si lavora con le immagini](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Quando si lavora con Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Informazioni sull&#39;ottimizzazione della larghezza di banda della rete {#network-bandwidth-optimization}

L&#39;attivazione della larghezza di banda della rete regola automaticamente la qualità dell&#39;immagine fornita in base all&#39;effettiva larghezza di banda della rete. Per una larghezza di banda di rete insufficiente, l&#39;ottimizzazione DPR viene automaticamente disattivata, anche se è già attivata.

Se lo desideri, la tua azienda può rinunciare all&#39;ottimizzazione della larghezza di banda di rete a livello delle singole immagini aggiungendo `network=off` all’URL dell’immagine.

| Valore consentito nell’URL di un’immagine | Descrizione |
|---|---|
| `network=off` | Disattiva l&#39;ottimizzazione della rete a livello di singolo URL immagine. |

I valori DPR e della larghezza di banda di rete si basano sui valori rilevati lato client della rete CDN inclusa nel pacchetto. Questi valori a volte sono imprecisi. Ad esempio, iPhone5 con DPR=2 e iPhone12 con `dpr=3`, entrambi `dpr=2`. Still, per dispositivi ad alta risoluzione, invio `dpr=2` è migliore dell’invio `dpr=1`. <!-- The best way to overcome this inaccuracy, however, is to use client-side DPR to give you 100% accurate values. And it works for any device, whether it is Apple or any other device that was launched. See [Use Smart Imaging with client-side Device Pixel Ratio](/help/assets/dynamic-media/client-side-dpr.md) -->


Il DPR lato client fornisce valori precisi al 100% e funziona per qualsiasi dispositivo, sia che si tratti di Apple o di qualsiasi altro nuovo dispositivo appena avviato.

## Quali sono i vantaggi principali dell&#39;ultima generazione di Smart imaging? {#what-are-the-key-benefits-of-smart-imaging}

Le immagini costituiscono la maggior parte del tempo di caricamento di una pagina. Di conseguenza, qualsiasi miglioramento delle prestazioni può avere un impatto profondo su tassi di conversione più elevati, sul tempo trascorso su un sito e su tassi di mancato recapito del sito più bassi.

Miglioramenti all&#39;ultima versione di Smart imaging:

* È stata migliorata la classificazione SEO di Google per le pagine web che utilizzano l’immagine avanzata più recente.
* Distribuisce immediatamente il contenuto ottimizzato (in fase di runtime).
* Utilizza la tecnologia Adobe Sensei per convertire in base alla qualità (`qlt`) specificata nella richiesta di immagine.
* L&#39;immagine intelligente può essere disattivata utilizzando `bfc` Parametro URL.
* TTL (Time To Live) indipendente. Precedentemente, per il funzionamento di Smart imaging era obbligatorio un TTL minimo di 12 ore.
* Precedentemente, sia le immagini originali che quelle derivate venivano memorizzate nella cache ed era un processo in due fasi per annullare la validità della cache. Nell’ultimo Smart imaging, solo i derivati vengono memorizzati nella cache, consentendo un processo di invalidazione della cache a un solo passaggio.
* I clienti che utilizzano intestazioni personalizzate nel loro set di regole beneficiano dell’ultima Smart imaging, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart imaging. Ad esempio, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot; come suggerito in [Aggiungi un valore di intestazione personalizzato alle risposte alle immagini|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Sono presenti costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Smart imaging è incluso nella licenza esistente. Questa regola è valida per Dynamic Media Classic o Experience Manager - Dynamic Media (On-Prem, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>La funzione Smart imaging non è disponibile per i clienti ibridi di Dynamic Media.

## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Quando un&#39;immagine viene richiesta da un consumatore, Smart imaging controlla le caratteristiche dell&#39;utente e la conversione nel formato immagine appropriato in base al browser in uso. Queste conversioni di formato vengono effettuate in modo da non compromettere la fedeltà visiva. La funzione Smart imaging converte automaticamente le immagini in formati diversi in base alla funzionalità del browser nel modo seguente.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* Converti automaticamente in WebP per i seguenti browser:
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari (in iOS, macOS, iPadOS), supporto del browser e della versione del sistema operativo WebP
   * Android™
   * Opera
* Supporto di browser legacy per i seguenti elementi:

   | Browser | Versione browser/sistema operativo | Formato |
   | --- | --- | --- |
   | Safari | Precedente ad iOS/iPad 14.0 o macOS BigSur | JPEG2000 |
   | Bordo | Anteriore a 18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Per i browser che non supportano questi formati, viene distribuito il formato immagine richiesto originariamente.

Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart imaging, l&#39;immagine originale viene servita.

## Quali formati immagine sono supportati? {#what-image-formats-are-supported}

I seguenti formati immagine sono supportati per Smart imaging:

* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Come funziona l’imaging avanzato con i predefiniti immagine esistenti già in uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

L’imaging avanzato funziona con i &quot;predefiniti immagine&quot; esistenti. Osserva tutte le impostazioni dell&#39;immagine tranne la qualità (`qlt`) e il formato (`fmt`) se il formato di file richiesto è JPEG o PNG. Per la conversione del formato, l&#39;imaging intelligente mantiene la fedeltà visiva completa, come definita dalle impostazioni del predefinito per immagini, ma con dimensioni file inferiori. Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart imaging, l&#39;immagine originale viene servita.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Devo modificare URL, predefiniti per immagini o distribuire un nuovo codice sul mio sito per Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

La funzione Smart Imaging funziona direttamente con gli URL delle immagini esistenti e i predefiniti per immagini se configuri Smart Imaging sul dominio personalizzato esistente. Inoltre, Smart imaging non richiede di aggiungere codice sul sito web per rilevare il browser di un utente. Viene gestito tutto automaticamente.

Se devi configurare un nuovo dominio personalizzato per l’utilizzo di Smart imaging, gli URL devono essere aggiornati per riflettere questo dominio personalizzato.

Per comprendere i prerequisiti per l’imaging intelligente, consulta [Posso utilizzare le Smart imaging?](#am-i-eligible-to-use-smart-imaging)

<!-- OLD No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## L’imaging avanzato funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart imaging funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Posso utilizzare le Smart imaging? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare Smart imaging, l’account Dynamic Media Classic o Dynamic Media della tua azienda deve soddisfare i seguenti requisiti:

* Utilizza la rete CDN (Content Delivery Network) in bundle Adobe come parte della tua licenza.
* Utilizza un dominio dedicato (ad esempio, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com`oppure `s7d13.scene7.com`).

Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**. Se al momento utilizzi un dominio generico, puoi richiedere di passare al dominio personalizzato. Esegui questa richiesta di transizione quando invii un ticket di assistenza tecnica.

Il tuo primo dominio personalizzato non comporta costi aggiuntivi con una licenza Dynamic Media.

## Qual è il processo per abilitare Smart imaging per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Avviate la richiesta per utilizzare Smart imaging; non è abilitato automaticamente.

Per impostazione predefinita, Smart imaging DPR e l’ottimizzazione della rete sono disabilitati (disattivati) per un account aziendale Dynamic Media. Se desideri abilitare (attivare) uno o entrambi questi miglioramenti predefiniti, crea un caso di supporto come descritto di seguito.

<!-- NOW AVAILABLE IN ALL THREE REGIONS AS OF AUGUST 2. 2021. SEE CQDOC- 17915 The release schedule for Smart Imaging DPR and network optimization is available in North as follows:

| Region | Target date |
|---|---|
| North America | Live | 
| Europe, Middle East, Africa | 13 August 2021 | 
| Asia-Pacific | 22 July 2021 | -->

1. [Utilizza l’Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   1. Nome contatto principale, e-mail, telefono.
   1. Tutti i domini da abilitare per l’imaging intelligente (ovvero, `images.company.com` o `mycompany.scene7.com`).

      Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**.
   1. Verifica di utilizzare la CDN tramite Adobe e di non gestirla con una relazione diretta.
   1. Verifica di utilizzare un dominio dedicato come `images.company.com` o `mycompany.scene7.com`e non un dominio generico come `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**. Se utilizzi un dominio Dynamic Media Classic generico, puoi richiedere il passaggio al dominio personalizzato come parte di questa transizione.
   1. Indica se desideri che funzioni su HTTP/2.

1. L’Assistenza clienti di Adobe ti aggiunge all’Elenco di attesa clienti di Smart imaging in base all’ordine in cui vengono inviate le richieste.
1. Quando Adobe è pronto per gestire la richiesta, l&#39;Assistenza clienti ti contatta per coordinare e impostare una data di destinazione.
1. **Facoltativo**: Facoltativamente, puoi testare l’imaging avanzato nell’ambiente di staging prima che Adobe introduca la nuova funzione in produzione.
1. Dopo il completamento dell’attività, riceverai una notifica dall’Assistenza clienti.
1. Per ottimizzare le prestazioni dell’imaging avanzato, Adobe consiglia di impostare il valore TTL (Time To Live) a 24 ore o più. Il TTL definisce per quanto tempo le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzi Dynamic Media Classic, vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Pubblica installazione]** > **[!UICONTROL Server immagini]**. Imposta la **[!UICONTROL Durata predefinita cache client]** a 24 o più.
   1. Se utilizzi Dynamic Media, segui [queste istruzioni](config-dm.md). Imposta la **[!UICONTROL Scadenza]** 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con Smart imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti, in base all’Elenco di attesa.

>[!NOTE]
>
>Ci può essere un lungo tempo di lead perché l’abilitazione di Smart imaging comporta ad Adobe la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni dei clienti in un dato momento.

## Quali sono i rischi connessi al passaggio all’app per l’utilizzo di Smart imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Non vi è alcun rischio per una pagina web del cliente. Tuttavia, la transizione a Smart imaging cancella la cache CDN. Questa operazione comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media all’Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate nella cache colpiscono direttamente i server di origine di Adobe fino a quando la cache non viene ricostruita nuovamente. Di conseguenza, Adobe prevede di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili durante l’estrazione delle richieste dall’origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente nella rete CDN entro circa 1 - 2 giorni.

## Come posso verificare se l’imaging intelligente funziona come previsto?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato il tuo account con Smart imaging, carica un URL immagine Dynamic Media Classic o Adobe Experience Manager - Dynamic Media sul browser.
1. Apri il riquadro per sviluppatori di Chrome andando in **[!UICONTROL Visualizza]** > **[!UICONTROL Sviluppatore]** > **[!UICONTROL Strumenti per gli sviluppatori]** nel browser. Oppure, scegli uno strumento per sviluppatori di browser a tua scelta.

1. Assicurati che la cache sia disabilitata quando gli strumenti per sviluppatori sono aperti.

   * In Windows®, passare alle impostazioni nel riquadro degli strumenti per sviluppatori, quindi selezionare **[!UICONTROL Disattiva la cache (mentre devtools è aperto)]** casella di controllo.
   * In macOS, nel riquadro dello sviluppatore, sotto la sezione **[!UICONTROL Rete]** scheda , seleziona **[!UICONTROL disattiva cache]**.

1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un&#39;immagine PNG convertita dinamicamente in WebP su Chrome.
1. Ripeti questo test su diversi browser e condizioni utente.

>[!NOTE]
>
>Non tutte le immagini vengono convertite. L’imaging intelligente decide se la conversione può migliorare le prestazioni. A volte, quando non si prevede alcun guadagno di prestazioni o il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## È possibile disattivare l&#39;imaging intelligente per qualsiasi richiesta?{#turning-off-smart-imaging}

Sì. Per disattivare l’imaging avanzato, aggiungi il modificatore `bfc=off` all’URL.

## Posso richiedere che DPR e l&#39;ottimizzazione della rete siano disattivati a livello aziendale? {#dpr-companylevel-turnoff}

Sì. Per disabilitare il DPR e l’ottimizzazione della rete nella tua azienda, crea un caso di assistenza come descritto in precedenza in questo argomento.

## Quale &quot;tuning&quot; è disponibile? Esistono impostazioni o comportamenti che possono essere definiti? {#tuning-settings}

Attualmente, è possibile abilitare o disabilitare l&#39;imaging avanzato. Nessun&#39;altra sintonizzazione disponibile.

## Se Smart imaging gestisce le impostazioni di qualità, posso impostare valori minimi e massimi? Ad esempio, è possibile impostare &quot;non inferiore a 60&quot; e &quot;non superiore a 80 qualità&quot;? {#minimum-maximum}

L&#39;attuale Smart imaging non è in grado di effettuare il provisioning.

## A volte un&#39;immagine di JPEG viene restituita a Chrome invece di un&#39;immagine WebP. Perché cambia? {#jpeg-webp}

L’imaging intelligente determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione si traduce in una dimensione file più piccola con qualità comparabile.

Come funziona l’ottimizzazione DPR per Smart imaging con i componenti Adobe Experience Manager Sites e i visualizzatori Dynamic Media?

* I componenti core di Experience Manager Sites sono configurati per impostazione predefinita per l’ottimizzazione DPR. Per evitare immagini di dimensioni eccessive dovute all’ottimizzazione DPR Smart imaging lato server, `dpr=off` viene sempre aggiunto alle immagini Dynamic Media dei componenti core Experience Manager Sites.
* Dato che il componente Dynamic Media Foundation è configurato per impostazione predefinita per l’ottimizzazione DPR, per evitare immagini di dimensioni eccessive a causa dell’ottimizzazione DPR Smart imaging lato server, `dpr=off` viene sempre aggiunto alle immagini dei componenti di Dynamic Media Foundation. Anche se il cliente deseleziona l’ottimizzazione DPR nel componente di base DM, Smart imaging DPR lato server non viene avviato. In sintesi, nel componente di base DM, l’ottimizzazione DPR entra in vigore solo in base all’impostazione a livello di componente di base DM.
* L’ottimizzazione DPR lato visualizzatore funziona in parallelo con l’ottimizzazione DPR per le immagini avanzate lato server e non produce immagini di dimensioni eccessive. In altre parole, ogni volta che il visualizzatore gestisce il DPR, ad esempio la visualizzazione principale solo in un visualizzatore abilitato per lo zoom, i valori DPR per l’imaging intelligente lato server non vengono attivati. Allo stesso modo, ogni volta che gli elementi del visualizzatore, come campioni e miniature, non dispongono di gestione DPR, viene attivato il valore DPR per l’imaging intelligente lato server.

Vedi anche [Quando si lavora con le immagini](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Quando si lavora con Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Ottimizzazione delle immagini con i formati di immagine WebP e AVIF di nuova generazione.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
>

