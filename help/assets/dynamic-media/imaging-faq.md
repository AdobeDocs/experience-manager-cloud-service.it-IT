---
title: Imaging avanzato
description: Scopri in che modo l’imaging intelligente con intelligenza artificiale di Adobe Sensei applica le caratteristiche di visualizzazione uniche di ogni utente per fornire automaticamente le immagini giuste ottimizzate per la propria esperienza, con conseguente miglioramento delle prestazioni e del coinvolgimento.
contentOwner: Rick Brough
feature: Asset Management,Renditions
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: c7555ef31d7657b4a90764224f4c8c58a6228157
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 1%

---

# Domande frequenti sulla tecnologia Smart Imaging {#smart-imaging}

## Informazioni sulla tecnologia Smart Imaging

La tecnologia di imaging intelligente applica le funzionalità di intelligenza artificiale di Adobe Sensei e funziona con i &quot;predefiniti immagine&quot; esistenti. Funziona per migliorare le prestazioni di consegna delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

E ora, ottieni un punteggio Google Core Web Vital migliore per LCP (Largest Contentful Paint) con Smart Imaging migliorato, che ora viene fornito con supporto sia AVIF che WebP.

>[!IMPORTANT]
>
>La tecnologia Smart Imaging richiede l’utilizzo della rete CDN (Content Delivery Network) predefinita in bundle con Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

>[!TIP]
>
>Provate e scoprite i vantaggi dei modificatori di immagini Dynamic Media e dell&#39;imaging avanzato con Dynamic Media [_Snapshot_](https://snapshot.scene7.com/).
>
> Snapshot è uno strumento di dimostrazione visiva, progettato per illustrare la potenza di Dynamic Media per la distribuzione di immagini ottimizzate e dinamiche. Sperimenta immagini di test o URL Dynamic Media per osservare visivamente l’output di vari modificatori di immagini Dynamic Media e ottimizzazioni Smart Imaging per i seguenti elementi:
>* Dimensione del file (con consegna WebP e AVIF)
>* Larghezza di banda di rete
>* DPR (Device Pixel Ratio, rapporto pixel dispositivo)
>
>Per scoprire quanto è facile utilizzare Snapshot, riprodurre il [Video di formazione sulle istantanee](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) (3 minuti e 17 secondi)

La tecnologia Smart Imaging ottimizza ulteriormente le prestazioni grazie alla piena integrazione con il migliore servizio CDN (Content Delivery Network) Adobe. Questo servizio individua il percorso Internet ottimale tra server, reti e punti di peering. Trova una route con latenza e velocità di perdita dei pacchetti più basse anziché utilizzare la route predefinita su Internet.

I seguenti esempi di risorse di immagini illustrano l’ottimizzazione Smart Imaging aggiunta:

| Immagine (URL) | Miniatura  | Dimensione (JPEG) | Dimensioni (WebP) con Smart Imaging | Formato (AVIF) con Smart Imaging | Riduzione % con WebP | % di riduzione con AVIF |
|---|---|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

Analogamente a quanto sopra, Adobe ha anche eseguito un test con un set di campioni più grande. Il formato AVIF forniva una riduzione delle dimensioni del 20% in più rispetto a WebP, che forniva una riduzione del 27% rispetto a JPEG. Tutto alla stessa qualità visiva. In totale, AVIF fornisce una riduzione media delle dimensioni fino al 41% rispetto a JPEG.

Confrontando WebP e AVIF con PNG, si può notare una riduzione delle dimensioni dell&#39;84% con WebP e dell&#39;87% con AVIF. Inoltre, poiché sia il formato WebP che AVIF supportano la trasparenza e le animazioni di più immagini, si tratta di una valida sostituzione per i file PNG e GIF trasparenti.

Vedi anche [Ottimizzazione delle immagini con formati immagine di nuova generazione (WebP e AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**Vantaggi della tecnologia Smart Imaging**

La tecnologia Smart Imaging migliora le prestazioni di consegna delle immagini ottimizzando automaticamente le dimensioni dei file immagine in base al browser client in uso, alla visualizzazione del dispositivo e alle condizioni di rete. Poiché le immagini rappresentano la maggior parte del tempo di caricamento di una pagina, qualsiasi miglioramento delle prestazioni può avere un impatto profondo sui KPI aziendali, ad esempio tassi di conversione più elevati, tempo trascorso su un sito e tassi di mancato recapito del sito più bassi.

I vantaggi più recenti della tecnologia Smart Imaging includono:

* Ora supporta il formato AVIF di nuova generazione.
* PNG in WebP e AVIF ora supporta la conversione con perdita di dati. Poiché PNG è un formato senza perdita di dati, le versioni precedenti di WebP e AVIF distribuite non avevano perdite.
* [Conversione formato browser](#bfc)
* [Proporzioni pixel dispositivo](#dpr)
* [Larghezza di banda di rete](#bandwidth)

### Informazioni sulla conversione del formato del browser {#bfc}

Attivare la conversione del formato del browser aggiungendo `bfc=on` all’URL dell’immagine converte automaticamente JPEG e PNG in AVIF con perdita di dati, WebP con perdita di dati, JPEGXR con perdita di dati, JPEG 2000 con perdita di dati per browser diversi. Per i browser che non supportano tali formati, la tecnologia Smart Imaging continua a essere utilizzata come JPEG o PNG. Insieme al formato, la qualità del nuovo formato viene ricalcolata da Smart Imaging.

È inoltre possibile disattivare la funzione Smart Imaging aggiungendo `bfc=off` all&#39;URL dell&#39;immagine.

Vedi anche [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) nell’API di server e rendering immagini di Dynamic Media.

### Informazioni sull&#39;ottimizzazione delle proporzioni pixel del dispositivo {#dpr}

Il rapporto pixel del dispositivo (DPR, Device Pixel Ratio), noto anche come rapporto pixel CSS, è la relazione tra i pixel fisici e i pixel logici di un dispositivo. Soprattutto con l&#39;avvento degli schermi retina, la risoluzione pixel dei dispositivi mobili moderni sta crescendo a un ritmo veloce.

Attivando l’ottimizzazione del rapporto pixel del dispositivo, l’immagine viene riprodotta alla risoluzione nativa dello schermo, rendendola più nitida.

Attualmente, la densità di pixel della visualizzazione proviene dai valori di intestazione della rete CDN di Akamai.

| Valori consentiti nell’URL di un’immagine | Descrizione |
|---|---|
| `dpr=off` | Disattiva l’ottimizzazione DPR a livello di singolo URL immagine. |
| `dpr=on,dprValue` | Sostituisci il valore DPR rilevato da Smart Imaging con un valore personalizzato (rilevato da qualsiasi logica lato client o in altro modo). Valore consentito per `dprValue` è un numero qualsiasi maggiore di 0. |

>[!NOTE]
>
>* È possibile utilizzare `dpr=on,dprValue` anche se l’impostazione DPR a livello aziendale è disattivata.
>* A causa dell&#39;ottimizzazione DPR, quando l&#39;immagine risultante è maggiore dell&#39;impostazione MaxPix Dynamic Media, la larghezza MaxPix viene sempre riconosciuta mantenendo le proporzioni dell&#39;immagine. —>


| Dimensione immagine richiesta | Valore rapporto pixel dispositivo (dpr) | Dimensioni immagine consegnata |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Vedi anche [Utilizzo delle immagini](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Quando si lavora con Ritaglio avanzato](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Informazioni sull&#39;ottimizzazione della larghezza di banda di rete {#bandwidth}

L&#39;attivazione della larghezza di banda consente di regolare automaticamente la qualità dell&#39;immagine trasmessa in base all&#39;effettiva larghezza di banda della rete. In caso di larghezza di banda insufficiente, l&#39;ottimizzazione DPR (Device Pixel Ratio) viene automaticamente disattivata, anche se è già attiva.

Se lo desideri, la tua azienda può scegliere di rinunciare all&#39;ottimizzazione della larghezza di banda a livello di singola immagine aggiungendo `network=off` all&#39;URL dell&#39;immagine.

| Valore consentito nell’URL di un’immagine | Descrizione |
|---|---|
| `network=off` | Disattiva l&#39;ottimizzazione della rete a livello di singolo URL immagine. |

I valori di DPR e larghezza di banda di rete si basano sui valori lato client rilevati per la rete CDN in bundle. Questi valori a volte sono imprecisi. IPhone5 con DPR=2 e iPhone12 con `dpr=3`, entrambi mostrano `dpr=2`. Per i dispositivi ad alta risoluzione, l&#39;invio `dpr=2` è migliore dell’invio `dpr=1`. Il modo migliore per superare questa imprecisione, tuttavia, è utilizzare il DPR lato client per fornire valori accurati al 100%. E funziona per qualsiasi dispositivo, sia esso Apple o qualsiasi altro dispositivo che è stato lanciato. Consulta [Utilizzo di Smart Imaging con proporzioni pixel del dispositivo lato client](/help/assets/dynamic-media/client-side-dpr.md).

**Vantaggi chiave aggiuntivi della tecnologia Smart Imaging**

* È stata migliorata la classificazione SEO di Google per le pagine web che utilizzano l’imaging avanzato più recente.
* Distribuisce immediatamente il contenuto ottimizzato (in fase di runtime).
* Utilizza la tecnologia Adobe Sensei per convertire in base alla qualità (`qlt`) specificata nella richiesta di immagine.
* TTL (Time To Live) indipendente. In precedenza, era obbligatorio un TTL minimo di 12 ore affinché l’imaging intelligente potesse funzionare.
* In precedenza, le immagini originali e derivate venivano memorizzate nella cache ed era un processo in due fasi per invalidare la cache. Nella tecnologia Smart Imaging più recente, vengono memorizzati nella cache solo i derivati, consentendo un processo di invalidamento della cache in un unico passaggio.
* I clienti che utilizzano intestazioni personalizzate nei propri set di regole beneficiano della tecnologia Smart Imaging più recente, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart Imaging. Ad esempio, &quot;Intervallo Consenti origine&quot;, &quot;X-Robot&quot; come suggerito in [Aggiungere un valore di intestazione personalizzato alle risposte immagine|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Come funziona l&#39;imaging intelligente**

Quando un’immagine viene richiesta da un utente, Smart Imaging controlla le caratteristiche dell’utente e la converte nel formato appropriato in base al browser in uso. Queste conversioni di formato vengono eseguite in modo da non compromettere la fedeltà visiva. La tecnologia Smart Imaging converte automaticamente le immagini in diversi formati in base alla funzionalità del browser, nel modo seguente.

* Converti automaticamente in AVIF se il browser supporta il formato
* Converti automaticamente in WebP se la conversione AVIF non è stata utile o se il browser non supporta AVIF
* Converti automaticamente in JPEG2000 se Safari non supporta WebP
* Converti automaticamente in JPEGXR per IE 9+ o se Edge non supporta WebP\
   | Formato immagine | Browser supportati | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEG | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* Per i browser che non supportano questi formati, viene fornito il formato immagine richiesto originariamente.

Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart Imaging, viene distribuita l&#39;immagine originale.

## Formati di immagine supportati nella tecnologia Smart Imaging

Per la creazione di immagini avanzate sono supportati i seguenti formati di immagine:

* JPEG
* PNG

Per il formato di file immagine JPEG, la qualità del nuovo formato viene ricalcolata da Smart Imaging.

Per i formati di file di immagine che supportano la trasparenza come PNG, puoi configurare Smart Imaging per fornire file AVIF e WebP con perdita di dati. Per la conversione di formato con perdita di dati, Smart Imaging utilizza la qualità indicata nell’URL dell’immagine oppure la qualità configurata nell’account aziendale di Dynamic Media.

## Comandi Image Server ignorati e supportati da Smart Imaging

Gli unici comandi Image Server ignorati da Smart Imaging sono `fmt` e `qlt`. Sono supportati tutti i comandi rimanenti.


+++**L&#39;imaging intelligente comporta costi di licenza?**

No. Smart Imaging è incluso nella licenza esistente. Questa regola è valida per Dynamic Media Classic o Experience Manager - Dynamic Media (on-prem, AMS e Experience Manager as a Cloud Service).

>[!IMPORTANT]
>
>Smart Imaging non è disponibile per i clienti Dynamic Media - Hybrid.

+++

+++**È possibile disattivare Smart Imaging per qualsiasi richiesta?**

Sì. È possibile disattivare Smart Imaging aggiungendo uno dei seguenti modificatori:

* `bfc=off` per disattivare Conversione formato browser. Vedi anche [Conversione formato browser](#bfc).
* `dpr=off` per disattivare Proporzioni pixel dispositivo. Vedi anche [Proporzioni pixel dispositivo](#dpr).
* `network=off` per disattivare la larghezza di banda della rete. Vedi anche [Larghezza di banda di rete](#network).

+++

+++**È possibile &quot;regolare&quot; la tecnologia Smart Imaging?**

Sì. Smart Imaging dispone di tre opzioni che è possibile abilitare o disabilitare.

* [Conversione formato browser](#bfc)
* [Proporzioni pixel dispositivo](#dpr)
* [Larghezza di banda di rete](#network)

+++

+++**Smart Imaging funziona con i miei predefiniti immagine esistenti?**

Sì. Smart Imaging funziona con i predefiniti immagine esistenti e osserva tutte le impostazioni immagine. Ciò che cambia è il formato dell’immagine, o l’impostazione della qualità, o entrambi. Per la conversione del formato, Smart Imaging mantiene la piena fedeltà visiva come definita dalle impostazioni predefinite dell&#39;immagine, ma con dimensioni di file inferiori.

Supponiamo ad esempio che un predefinito immagine sia definito con formato JPEG, dimensioni 500 x 500, qualità=85 e maschera di contrasto=0.1,1,5. Quando Smart Imaging rileva che un utente si trova su un browser Chrome, l’immagine viene convertita in formato WebP, con dimensioni 500 x 500. E, unsharp mask=0.1,1,5 è a una qualità WebP che corrisponde a una qualità JPEG di 85 il più vicino possibile. L’ingombro di tale conversione WebP viene confrontato con il JPEG e viene restituito il più piccolo dei due.

+++

+++**È necessario modificare URL, predefiniti immagine o distribuire nuovo codice sul sito?**

No. La tecnologia Smart Imaging funziona perfettamente con gli URL immagine e i predefiniti immagine esistenti. Inoltre, Smart Imaging non richiede di aggiungere codice al sito web per rilevare il browser di un utente. Tutte queste funzionalità vengono gestite automaticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++

+++**Smart Imaging funziona con HTTPS? E HTTP/2?**

Sì, a entrambe le domande. La tecnologia Smart Imaging funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

+++

+++**Posso utilizzare Smart Imaging?**

Dipende. Per utilizzare Smart Imaging, l’account Dynamic Media Classic o Dynamic Media dell’azienda su Experience Manager deve soddisfare i seguenti requisiti:

* Utilizza la rete CDN (Content Delivery Network) fornita dall’Adobe come parte della licenza.
* Utilizza un dominio dedicato (ad esempio, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com`, o `s7d13.scene7.com`).

Per trovare i domini, apri la [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account aziendale o a quelli della tua azienda.

Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato]**. Se al momento utilizzi un dominio generico, puoi richiedere di passare al dominio personalizzato. Effettua questa richiesta di transizione quando invii un caso di supporto.

Il primo dominio personalizzato non comporta costi aggiuntivi con una licenza Dynamic Media.

+++

+++**Posso abilitare Smart Imaging per il mio account?**

No. Viene avviata una richiesta di utilizzo di Smart Imaging, che non viene abilitata automaticamente.

Crea un caso di supporto come descritto di seguito. Nel tuo caso di supporto, assicurati di indicare quali delle seguenti funzionalità di Smart Imaging (una o più) desideri abilitare sul tuo account:

* WebP
* AVIF
* Ottimizzazione di larghezza di banda di rete e DPR
* PNG a AVIF con perdita di dati o WebP con perdita di dati

Se si dispone già di Smart Imaging abilitato con WebP, ma si desiderano altre nuove funzionalità come quelle elencate sopra, è necessario creare un caso di supporto.

**Per creare un caso di supporto per abilitare Smart Imaging sul tuo account:**

1. [Utilizza l’Admin Console per avviare la creazione di un nuovo caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Nome del contatto principale, e-mail, telefono.

   * Elencare quali delle seguenti funzionalità di Smart Imaging (una o più) si desidera abilitare sul proprio account:
      * WebP
      * AVIF
      * Ottimizzazione di larghezza di banda di rete e DPR
      * PNG a AVIF con perdita di dati o WebP con perdita di dati
   * Tutti i domini da abilitare per la tecnologia Smart Imaging (ovvero `images.company.com` o `mycompany.scene7.com`).

      Per trovare i domini, apri la [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account aziendale o a quelli della tua azienda.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato]**.

   * Verifica di utilizzare la rete CDN tramite Adobe e di non essere gestita con una relazione diretta.

   * Verifica di utilizzare un dominio dedicato come `images.company.com` o `mycompany.scene7.com`e non un dominio generico, ad esempio `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, apri la [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account aziendale o a quelli della tua azienda.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato]**. Se attualmente utilizzi un dominio Dynamic Media Classic generico, puoi richiedere di passare al dominio personalizzato come parte di questa transizione.

   * Indica se desideri che funzioni su HTTP/2.


1. L’Assistenza clienti Adobe ti aggiunge alla Lista d’attesa clienti di Smart Imaging in base all’ordine in cui vengono inviate le richieste.
1. Quando Adobe è pronto a gestire la richiesta, l’Assistenza clienti ti contatta per coordinare e impostare una data di scadenza.
1. **Facoltativo**: facoltativamente, puoi testare l’imaging avanzato in Staging prima che Adobe invii la nuova funzione in produzione.
1. Ricevi una notifica dopo il completamento da parte dell’Assistenza clienti.
1. Per massimizzare i miglioramenti delle prestazioni della tecnologia Smart Imaging, Adobe consiglia di impostare il valore TTL (Time To Live) su 24 ore o più. Il TTL definisce per quanto tempo le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzi Dynamic Media Classic, vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazione pubblicazione]** > **[!UICONTROL Server immagini]**. Imposta il **[!UICONTROL Durata predefinita cache client]** a 24 o più.
   1. Se utilizzi Dynamic Media, segui [queste istruzioni](config-dm.md). Imposta il **[!UICONTROL Scade]** 24 ore o più.

+++

+++**Quando il mio account è abilitato con Smart Imaging?**

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti, in base alla Lista d’attesa.

>[!NOTE]
>
>Il lead time può essere lungo perché l’abilitazione di Smart Imaging richiede la cancellazione della cache da parte di un Adobe. Pertanto, è possibile gestire solo poche transizioni cliente in un dato momento.

+++

+++**L&#39;uso di Smart Imaging comporta dei rischi?**

Non esiste alcun rischio per una pagina web del cliente. Tuttavia, la transizione a Smart Imaging elimina la cache CDN. Questa operazione comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media su Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate in cache hanno colpito direttamente i server di origine di Adobe fino a quando la cache non viene nuovamente generata. Adobe prevede quindi di gestire alcune transizioni cliente alla volta in modo da mantenere prestazioni accettabili durante il richiamo delle richieste dall’origine. Per la maggior parte dei clienti, la cache viene di nuovo completamente creata sulla rete CDN entro circa uno o due giorni.

+++

+++**Posso verificare se Smart Imaging funziona?**

Sì. È possibile effettuare le seguenti operazioni:

1. Dopo aver configurato l’account con Smart Imaging, carica un URL immagine Dynamic Media Classic o Adobe Experience Manager - Dynamic Media sul browser.
1. Apri il riquadro per sviluppatori di Chrome andando su **[!UICONTROL Visualizza]** > **[!UICONTROL Sviluppatore]** > **[!UICONTROL Strumenti per sviluppatori]** nel browser. In alternativa, scegli uno degli strumenti di sviluppo del browser desiderato.

1. Assicurati che la cache sia disabilitata quando gli strumenti di sviluppo sono aperti.

   * In Windows®, passa alle impostazioni nel riquadro Strumenti per sviluppatori, quindi seleziona **[!UICONTROL Disabilita la cache (mentre devtools è aperto)]** casella di controllo.
   * In macOS, nel riquadro dello sviluppatore, sotto **[!UICONTROL Rete]** , seleziona **[!UICONTROL disabilita cache]**.

1. Osserva che il Tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un’immagine PNG convertita dinamicamente in WebP su Chrome. Se nel dominio è abilitato AVIF, è anche possibile prevedere di visualizzare AVIF nel Tipo di contenuto.
1. Ripeti questo test su diversi browser e condizioni utente.

>[!NOTE]
>
>Non tutte le immagini vengono convertite. L&#39;imaging intelligente decide se la conversione può migliorare le prestazioni. Talvolta, se non è previsto alcun miglioramento delle prestazioni o se il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

+++

+++**Esiste un modo per conoscere i vantaggi della tecnologia Smart Imaging?**

Sì. L’intestazione Smart Imaging determina i vantaggi della tecnologia Smart Imaging. Quando Smart Imaging è abilitato, dopo aver richiesto un&#39;immagine, sotto **[!UICONTROL Intestazioni di risposta]** intestazione, puoi vedere `-X-Adobe-Smart-Imaging` come nell’esempio evidenziato seguente:

![Intestazione Smart Imaging](/help/assets/dynamic-media/assets/smartimagingheader.png)

Questa intestazione indica quanto segue:

* Smart Imaging funziona per l’azienda.
* Un valore positivo indica che la conversione è riuscita. In questo caso, viene restituita una nuova immagine WebP.
* Un valore negativo indica che la conversione non ha esito positivo. In tal caso, viene restituita l’immagine richiesta originale (JPEG per impostazione predefinita, se non specificata).
* Un valore positivo mostra la differenza in byte tra l’immagine richiesta e la nuova immagine. Nell&#39;esempio precedente, i byte salvati sono `75048` o circa 75 KB per un&#39;immagine.
* Un valore negativo indica che l’immagine richiesta è più piccola della nuova immagine. Viene visualizzata la differenza di dimensione negativa, ma l’immagine trasmessa è solo l’immagine originale richiesta.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 con WebP consegnato**
>
>Se il valore di `X-Adobe-Smart-Imaging` : -1 e WebP è ancora in fase di distribuzione, significa che Smart Imaging funziona ma i vantaggi in termini di dimensioni non sono stati calcolati a causa della cache obsoleta. È possibile utilizzare `cache=update` (una sola volta) nell’URL dell’immagine per risolvere questo problema.
>Esempio di utilizzo del modificatore:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Per invalidare l’intera cache, è necessario creare un caso di supporto.

+++

+++**È possibile disattivare l’ottimizzazione AVIF in Smart Imaging?**

Sì. Se si desidera tornare al WebP in servizio per impostazione predefinita, creare un caso di supporto per lo stesso. Come sempre, è possibile disattivare Smart Imaging aggiungendo il parametro `bfc=off` all&#39;URL dell&#39;immagine. Tuttavia, non è possibile selezionare WebP o AVIF nel modificatore URL per Smart Imaging. Questa funzionalità viene mantenuta a livello di account aziendale.

+++

+++**Perché la mia richiesta non riesce se dispongo di un URL con fmt=tif sul browser web Chrome?**

Questo errore non si verifica se Smart Imaging non è abilitato sul tuo account. Smart Imaging funziona solo con i formati JPEG o PNG.

Per evitare questo errore, puoi effettuare le seguenti operazioni:

* Specificare JPEG o PNG oppure
* Non utilizzare il `fmt` un modificatore, oppure
* Utilizza un formato preferito dal browser e definito da Smart Imaging. Ad esempio, puoi utilizzare WebP per il browser web Chrome.

+++

+++**Posso scaricare un&#39;immagine TIFF dall&#39;URL di un&#39;immagine?**

Sì. Aggiungi `fmt=tif` e `bfc=off` al percorso URL dell&#39;immagine.

+++

+++**Smart Imaging gestisce le impostazioni relative al formato e alla qualità delle immagini?**

Sì. La tecnologia Smart Imaging utilizza sia il formato che la qualità. Gli altri parametri rimangono invariati, se richiesto nell’URL dell’immagine.

+++

+++**È possibile impostare una qualità minima e massima?**

No. Attualmente non esiste un provisioning di questo tipo.

+++

+++**Smart Imaging regola l&#39;impostazione di qualità percentuale dell&#39;output?**

Sì. La tecnologia Smart Imaging regola automaticamente la percentuale di qualità. Questa percentuale di qualità è determinata utilizzando un algoritmo di apprendimento automatico sviluppato da Adobe. Questa percentuale non è specifica per l&#39;intervallo.

+++

+++**Solo JPEG e PNG vengono sostituiti da Smart Imaging?**

Sì. Questa funzionalità funziona solo per JPEG e PNG.

+++

+++**Perché JPEG a volte viene restituito a Chrome invece di WebP?**

La tecnologia Smart Imaging determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione è utile.

+++

+++**Perché Device Pixel Ratio (dpr) non funziona con le immagini composite?**

Se un&#39;immagine composita coinvolge troppi livelli, la funzionalità dpr potrebbe essere interessata durante l&#39;utilizzo di un modificatore di posizione. Questo problema è noto e verrà risolto nelle versioni future di Smart Imaging. Se altre funzionalità di Smart Imaging non funzionano come previsto, puoi creare un caso di supporto per segnalare il problema.

+++

+++**Perché Smart Imaging PNG viene convertito in WebP/AVIF senza perdita di dati?**

Poiché il PNG è un formato senza perdita di dati, le versioni precedenti di WebP e AVIF consegnate erano prive di perdita e quindi di dimensioni maggiori del previsto. La tecnologia Smart Imaging ora supporta la conversione con perdita di dati. È possibile utilizzare il modificatore `cache=update` (una sola volta) in una richiesta di immagine per risolvere il problema. Esempio di utilizzo del modificatore:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Per invalidare l’intera cache, devi creare un caso di supporto che richieda tale impegno.

+++

+++**Posso continuare a utilizzare il PNG per una conversione senza perdite in Smart Imaging?**

Sì. La tecnologia Smart Imaging ora supporta la conversione con perdita di dati in base al livello di qualità. Per continuare a utilizzare la conversione senza perdita di dati, puoi utilizzare la qualità 100 impostata tramite l’impostazione della tua azienda oppure tramite l’URL dell’immagine utilizzando `qlt=100` nel percorso.

+++



























<!-- ## If Smart Imaging manages the quality settings, are there minimums and maximums I can set? For example, is it possible to set "no lower than 60" and "no greater than 80 quality"? {#minimum-maximum}

There is no such provisioning ability in the current Smart Imaging. -->

<!-- ## Sometimes a JPEG image is returned to Chrome instead of a WebP image. Why does that change happen? {#jpeg-webp}

Smart Imaging determines if the conversion is beneficial or not. It returns the new image only if the conversion results in a smaller file size with comparable quality.

How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) -->
>