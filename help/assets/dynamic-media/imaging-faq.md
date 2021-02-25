---
title: Smart imaging
description: La funzione di imaging intelligente applica le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento.
translation-type: tm+mt
source-git-commit: 20e37c385c2d3df91e37095bcf8a630fbfccbd16
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 2%

---


# Imaging avanzato {#smart-imaging}

## Cos&#39;è &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

La tecnologia Smart Imaging si applica  funzionalità di Adobe Sensei AI e funziona con i &quot;predefiniti per immagini&quot; esistenti. Funziona per migliorare le prestazioni di distribuzione delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo del CDN fornito con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

La tecnologia Smart Imaging offre inoltre un ulteriore vantaggio in termini di prestazioni grazie all&#39;integrazione completa con il servizio CDN (Content Delivery Network) di livello superiore  Adobe. Questo servizio trova il percorso Internet ottimale tra server, reti e punti di pari livello. Si tratta della latenza più bassa, o della percentuale di perdita di pacchetti più bassa, o di entrambi, anziché semplicemente utilizzare la route predefinita su Internet.

Gli esempi di risorse di immagine seguenti descrivono l’ottimizzazione per Smart Imaging aggiunta:

| Image<br>(URL) | Miniatura  | Dimensioni<br> (JPEG) | Dimensioni (WebP)<br> (con Smart Imaging) | % riduzione |
|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Media = 51% |

Come già detto,  Adobe ha anche eseguito un test con 7009 URL dai siti dei clienti live. Sono stati in grado di ottenere una media del 38% di ulteriore ottimizzazione delle dimensioni dei file per JPEG. Per i file PNG con formato WebP, sono stati in grado di ottenere un&#39;ottimizzazione media del 31% delle dimensioni dei file. Questo tipo di ottimizzazione è possibile grazie alla capacità di Smart Imaging.

## Quali sono i vantaggi principali dell&#39;ultima generazione di Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

Le immagini costituiscono la maggior parte del tempo di caricamento di una pagina. Di conseguenza, qualsiasi miglioramento delle prestazioni può avere un impatto profondo su tassi di conversione più elevati, sul tempo trascorso su un sito e su tassi di rimbalzo inferiori.

Miglioramenti nell&#39;ultima versione di Smart Imaging:

* Trasmette immediatamente il contenuto ottimizzato (in fase di esecuzione).
* Utilizza  tecnologia Adobe Sensei per la conversione in base alla qualità (qlt) specificata nella richiesta di immagini.
* La funzione Smart Imaging può essere disattivata utilizzando il parametro URL &quot;bfc&quot;.
* TTL (Time To Live) indipendente. Precedentemente, era obbligatorio un limite minimo di 12 ore per l&#39;utilizzo di Smart Imaging.
* Precedentemente, sia le immagini originali che quelle derivate erano memorizzate nella cache, e si trattava di un processo in due fasi per annullare la validità della cache. Nella versione più recente di Smart Imaging, solo i derivati vengono memorizzati nella cache, consentendo un processo di annullamento della validità della cache a un solo passaggio.
* Clienti che utilizzano intestazioni personalizzate nel set di regole. Ad esempio, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot; come suggerito in [Aggiunta di un valore intestazione personalizzato alle risposte alle immagini|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) beneficiano dell&#39;ultima Smart Imaging. Queste intestazioni non sono bloccate, a differenza della versione precedente di Smart Imaging.

## Esistono costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Smart Imaging è incluso nella licenza esistente. Questa regola è valida per Dynamic Media Classic o  Dynamic Media Experience Manager (On-Prem, AMS e  Experience Manager come Cloud Service).

>[!NOTE]
>
>Le immagini intelligenti non sono disponibili per i clienti ibridi di Dynamic Media.


## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Quando un&#39;immagine viene richiesta da un consumatore, Smart Imaging ne verifica le caratteristiche. Viene quindi convertita nel formato immagine appropriato in base al browser in uso. Queste conversioni del formato vengono effettuate in modo da non compromettere la fedeltà visiva. La funzione di imaging intelligente converte automaticamente le immagini in diversi formati, in base alla funzionalità del browser, nel modo seguente.

* Converti automaticamente in WebP per i seguenti browser:
   * Effetto cromatura
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14 solo con iOS 14.0 e versioni successive e macOS BigSur e versioni successive
   * Android
   * Opera
* Supporto browser legacy per i seguenti elementi:

   | Browser | Versione browser/sistema operativo | Formato |
   | --- | --- | --- |
   | Safari | iOS 14.0 o versioni precedenti | JPEG2000 |
   | Edge | 18 o versioni precedenti | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
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

La funzione Smart Imaging funziona con i &quot;predefiniti per immagini&quot; esistenti. Osserva tutte le impostazioni dell’immagine eccetto qualità (qlt) e formato (fmt) se il formato file richiesto è JPEG o PNG. Per la conversione del formato, la funzione Smart Imaging mantiene la fedeltà visiva completa, come definito dalle impostazioni del predefinito per immagini, ma con file di dimensioni inferiori. Se le dimensioni dell&#39;immagine originale sono inferiori a quelle generate da Smart Imaging, viene trasmessa l&#39;immagine originale.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## È necessario modificare URL, predefiniti per immagini o distribuire sul sito un nuovo codice per Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Smart Imaging funziona perfettamente con gli URL esistenti delle immagini e i predefiniti per immagini se configurate Smart Imaging sul dominio personalizzato esistente. Inoltre, per rilevare il browser di un utente non è necessario aggiungere codice al sito Web. Tutte queste funzionalità vengono gestite automaticamente.

Se devi configurare un nuovo dominio personalizzato per l’utilizzo di Smart Imaging, gli URL devono essere aggiornati per riflettere questo dominio personalizzato.

Per comprendere i prerequisiti per l&#39;imaging intelligente, vedere [Sono idoneo all&#39;utilizzo di Smart Imaging?](#am-i-eligible-to-use-smart-imaging).

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## Smart Imaging funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart Imaging funziona con immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Posso utilizzare la tecnologia di imaging intelligente? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare la funzione Smart Imaging, l&#39;account Dynamic Media Classic o Dynamic Media della società deve soddisfare i seguenti requisiti:

* Utilizzate la rete CDN  (Content Delivery Network) inclusa nel Adobe come parte della licenza.
* Utilizzate un dominio dedicato (ad esempio, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

Per trovare i domini, accedi al tuo account o account della società.

Toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**. Cercare il campo con l&#39;etichetta **[!UICONTROL Nome server pubblicato]**. Se al momento si utilizza un dominio generico, è possibile richiedere di passare al proprio dominio personalizzato. Eseguite questa richiesta di transizione quando inviate un ticket di assistenza tecnica.

Il primo dominio personalizzato non prevede costi aggiuntivi con una licenza Dynamic Media.

## Qual è la procedura per attivare la funzione Smart Imaging per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Avviate la richiesta per l’utilizzo di immagini intelligenti; non è abilitata automaticamente.

1. [Utilizzate l&#39;Admin Console  per creare un caso di supporto.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Fornite le seguenti informazioni nel caso di assistenza:

   1. Nome contatto principale, email, telefono.
   1. Tutti i domini da abilitare per l&#39;imaging intelligente (ovvero `images.company.com` o `mycompany.scene7.com`).

      Per trovare i domini, accedi al tuo account o account della società.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cercare il campo con l&#39;etichetta **[!UICONTROL Nome server pubblicato]**.
   1. Verificate di utilizzare la CDN tramite  Adobe e di non essere gestiti con una relazione diretta.
   1. Verificare di utilizzare un dominio dedicato, ad esempio `images.company.com` o `mycompany.scene7.com`, e non un dominio generico, ad esempio `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, accedi al tuo account o account della società.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cercare il campo con l&#39;etichetta **[!UICONTROL Nome server pubblicato]**. Se utilizzate un dominio Dynamic Media Classic generico, potete richiedere il passaggio al dominio personalizzato come parte di questa transizione.
   1. Indicate se desiderate che funzioni su HTTP/2.

1.  l&#39;Assistenza clienti di Adobe aggiunge all&#39;Elenco di attesa clienti Smart Imaging in base all&#39;ordine in cui vengono inviate le richieste.
1. Quando  Adobe è pronto per gestire la richiesta, l&#39;Assistenza clienti ti contatta per coordinare e impostare una data di destinazione.
1. **Facoltativo**: Facoltativamente, potete testare l&#39;imaging intelligente in Staging prima che  Adobe introduca la nuova funzione in produzione.
1. Una volta completato il rapporto, l&#39;Assistenza clienti riceverà una notifica.
1. Per ottimizzare le prestazioni di Smart Imaging,  Adobe consiglia di impostare il tempo di trasmissione (TTL) su 24 ore o più. Il TTL definisce il tempo in cui le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzate Dynamic Media Classic, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini]**. Impostare il valore **[!UICONTROL Tempo cache client predefinito su Live]** su 24 o più.
   1. Se utilizzate Dynamic Media, seguite le [presenti istruzioni](config-dm.md). Impostare il valore **[!UICONTROL Scadenza]** su 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dal supporto tecnico, in base all&#39;Elenco di attesa.

>[!NOTE]
Talvolta, il tempo di attesa è lungo perché l&#39;attivazione di Smart Imaging implica la cancellazione  Adobe della cache. Pertanto, è possibile gestire solo alcune transizioni cliente in un dato momento.

## Quali sono i rischi legati al passaggio all&#39;immagine per l&#39;utilizzo di Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Non c&#39;è alcun rischio per una pagina Web del cliente. Tuttavia, la transizione a Smart Imaging elimina la cache CDN. Questa operazione comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media in  Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate nella cache hanno colpito direttamente  server  origine di Adobe fino a quando la cache non viene ricreata. Come tale,  Adobe pianifica di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili quando si richiamano le richieste dall&#39;origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente alla rete CDN entro circa 1 - 2 giorni.

## Come posso verificare se la funzione di imaging intelligente funziona come previsto?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato l’account con la funzione di imaging intelligente, caricate nel browser un URL immagine Dynamic Media Classic (Scene7)/Dynamic Media.
1. Aprite il riquadro per gli sviluppatori di Chrome facendo clic su **[!UICONTROL Visualizza > Sviluppatore > Strumenti per sviluppatori]** nel browser. Oppure, scegliete uno strumento di sviluppo browser a vostra scelta.

1. Accertatevi che la cache sia disattivata quando gli strumenti di sviluppo sono aperti.

   * In Windows: individuate le impostazioni nel riquadro degli strumenti dello sviluppatore, quindi selezionate la casella di controllo **[!UICONTROL Disattiva cache (mentre i devtools sono aperti)]**.
   * In Mac - nel riquadro dello sviluppatore, nella scheda **[!UICONTROL Rete]**, selezionare **[!UICONTROL disable cache]** .

1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un&#39;immagine PNG convertita dinamicamente in WebP su Chrome.
1. Ripetete questo test su diversi browser e condizioni utente.

>[!NOTE]
Non tutte le immagini sono convertite. La funzione Smart Imaging decide se la conversione è necessaria per migliorare le prestazioni. A volte, se non si prevede alcun guadagno di prestazioni o se il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## È possibile disattivare l&#39;immagine intelligente per qualsiasi richiesta?{#turning-off-smart-imaging}

Sì. Potete disattivare l&#39;immagine avanzata aggiungendo all&#39;URL il modificatore `bfc=off`.

## Quale &quot;tuning&quot; è disponibile? Esistono impostazioni o comportamenti che possono essere definiti? (#tuning-settings)

Attualmente, è possibile attivare o disattivare l&#39;imaging avanzato. Non sono disponibili altre impostazioni di sintonizzazione.

## Se Smart Imaging gestisce le impostazioni di qualità, è possibile impostare valori minimi e massimi? Ad esempio, è possibile impostare &quot;non inferiore a 60&quot; e &quot;non superiore a 80 qualità&quot;? (#Minimum-Maximum)

L&#39;attuale funzione di provisioning di Smart Imaging non è disponibile.

## A volte un&#39;immagine JPEG viene restituita a Chrome invece di un&#39;immagine WebP. Perché cambia? (#jpeg-webp)

La funzione di imaging intelligente determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione restituisce un file di dimensioni inferiori con qualità comparabile.
