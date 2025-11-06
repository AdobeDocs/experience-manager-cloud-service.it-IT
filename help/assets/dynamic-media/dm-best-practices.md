---
title: Best practice per Dynamic Media
description: Scopri le best practice in Dynamic Media per l’utilizzo di immagini e video e le best practice per i visualizzatori Dynamic Media.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '4049'
ht-degree: 0%

---

# Best practice per Dynamic Media{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

{{see-also-dm}}

Le organizzazioni devono affrontare un&#39;esplosione di canali e dispositivi per interagire con gli utenti. Il percorso di clienti si estende su negozi fisici, web, dispositivi mobili, social media, e-mail e commercio. Per soddisfare questa domanda, Dynamic Media su Adobe Experience Manager (AEM) offre una soluzione completa. Ottimizza la distribuzione delle risorse, gestisce la personalizzazione e garantisce esperienze coerenti, performanti e allineate al brand tra canali e dispositivi.

Alcuni dei principi chiave di Dynamic Media includono:

* **Approccio a file singolo:** con Dynamic Media, viene archiviato un file di origine principale e tutte le varianti di dimensione e gli effetti visivi vengono creati e ottimizzati in modo dinamico al momento della consegna. Questo approccio consente di risparmiare sui costi di storage e di eliminare la complessità dei flussi di lavoro.
* **Effettivamente globale:** Smart Imaging, applicato durante la distribuzione del contenuto, riduce in modo significativo le dimensioni dell&#39;immagine e il peso della pagina senza compromettere la qualità visiva. È ottimizzato per la larghezza di banda della rete e i rapporti pixel del dispositivo.
* **Tecnologia AI:** Smart Crop, una funzionalità basata sull&#39;intelligenza artificiale, automatizza il ritaglio delle immagini e dei video point-of-interest. Consente di eliminare gli sforzi manuali e di scalare in modo efficiente per l&#39;uso aziendale.
* **Video semplificato:** carica i video di origine principali in Dynamic Media e li invia in streaming in più lingue con audio descrittivo.
* **Libreria visualizzatori di esperienze:** Personalizza e personalizza i visualizzatori di esperienze per immagini e video. Questi visualizzatori si integrano perfettamente nelle tue esperienze digitali.
* **Supporto di formati emergenti:** Dynamic Media consente la distribuzione di esperienze 3D e panoramiche.

Durante l&#39;esplorazione del [Percorso Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1), la revisione dell&#39;elenco consolidato delle best practice riportato di seguito può aiutarti a sfruttare al massimo le sue funzionalità. Adatta queste best practice di Dynamic Media al tuo contesto e ai requisiti del progetto specifici in modo da ottimizzare le tue esperienze su canali e dispositivi diversi.

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>Le best practice relative ai Dynamic Media descritte in questo articolo possono evolvere nel tempo man mano che emergono nuove tecnologie in Dynamic Media. Le informazioni seguenti sono aggiornate sulla versione più recente di Dynamic Media.


## Inserire risorse in Dynamic Media

**Caso di business:** *Gestire in modo efficiente grandi volumi di risorse e assicurarsi che solo i contenuti approvati pertinenti vengano consegnati agli utenti finali.*

Semplifica la gestione di un numero elevato di risorse in modo efficiente. Assicurati che solo il contenuto appropriato e autorizzato raggiunga gli utenti finali utilizzando le funzionalità di **Sincronizzazione selettiva** e **Pubblicazione selettiva** di Dynamic Media.

* **Sincronizzazione selettiva:**
Funzione proattiva che consente di scegliere quali risorse sincronizzare con Dynamic Media. Ad esempio, puoi decidere di sincronizzare solo le cartelle contenenti risorse che hanno ricevuto l’approvazione finale. Questo flusso di lavoro consente di mantenere il controllo sulle risorse che vengono preparate per la consegna ai clienti.

* **Pubblicazione selettiva:**
Dopo aver sincronizzato le risorse, la pubblicazione selettiva consente di controllare quali risorse sono visibili ai clienti. Grazie a questa funzionalità è possibile determinare quali risorse approvate vengono effettivamente consegnate tramite i canali, in modo che i clienti possano visualizzare solo i contenuti migliori e più rilevanti.

Queste due best practice consentono di migliorare il controllo, la governance e la produttività dei contenuti rich media.

Vuoi saperne di più? Vai a [Configura pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).


## Visualizzatori Dynamic Media

Le best practice per i visualizzatori Dynamic Media sono linee guida essenziali progettate per ottimizzare le prestazioni, le funzionalità e l’esperienza utente delle risorse Dynamic Media su AEM. Queste procedure garantiscono che le risorse siano sincronizzate, pubblicate e configurate correttamente per utilizzare tutte le funzionalità di Dynamic Media.

Seguendo queste best practice, puoi ottenere un’integrazione perfetta, una gestione efficiente delle risorse e interazioni migliorate con i visualizzatori. La sincronizzazione delle risorse, l’utilizzo del ritaglio intelligente e il rispetto delle linee guida di inclusione dei file di JavaScript sono tutte pratiche importanti. Questi consigli aiutano a mantenere l’integrità e l’affidabilità della distribuzione dei contenuti multimediali su varie piattaforme e dispositivi.

* **Sincronizza Assets visualizzatore:**
Prima di utilizzare il lettore, assicurati che tutte le risorse visualizzatore siano sincronizzate con Dynamic Media.

   * Accedere alla pagina di gestione esempi in `/libs/dam/gui/content/s7dam/samplemanager/samplemanager`. Questa pagina consente di risincronizzare le risorse di un visualizzatore, tra cui icone pronte all’uso, file CSS e predefiniti.
   * In caso di problemi con il visualizzatore, vai all&#39;articolo [Risoluzione dei problemi relativi ai visualizzatori Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#viewers).

* **Pubblica Assets:**
Assicurati che le risorse siano pubblicate prima di visualizzarle nei visualizzatori di consegna.
* **Riproduzione automatica video disattivata:**
Per la funzionalità di riproduzione automatica dei video, utilizza le impostazioni per la disattivazione dell’audio dei video, in quanto i browser limitano la riproduzione dei video con il volume.
* **Ritaglio avanzato:**
Utilizza il componente Immagine v3 per il ritaglio avanzato per migliorare la presentazione delle risorse immagine.
* **Inclusione di file JavaScript:**
Includi solo il file JavaScript del visualizzatore principale nella pagina. Evita di fare riferimento a file JavaScript aggiuntivi che la logica di runtime del visualizzatore potrebbe scaricare. In particolare, non collegare direttamente la libreria `Utils.js` di HTML5 SDK dal percorso di contesto `/s7viewers` (noto come SDK consolidato include). La logica del visualizzatore gestisce la posizione di `Utils.js` o di librerie di visualizzatori di runtime simili, che possono cambiare tra le versioni. Adobe non mantiene sul server versioni precedenti di inclusioni visualizzatore secondarie, pertanto il riferimento diretto ad esse può interrompere la funzionalità del visualizzatore negli aggiornamenti futuri.
* **Linee guida per l&#39;incorporamento:**
Utilizza la documentazione per incorporare le linee guida specifiche di ciascun visualizzatore.
Vuoi saperne di più? Vai a [Visualizzatori per AEM Assets](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers).
* **Esercitazione SDK ed esempi:**
Esaminare l&#39;[Esercitazione SDK per visualizzatori](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/library/c-tutorial) e gli [esempi di applicazioni HTML5 SDK](https://s7d9.scene7.com/s7sdk/2024.5/docs/jsdoc/index.html) per ottenere informazioni approfondite sulle API dei componenti SDK.


## Preparare le risorse per la consegna

### Organizzare le risorse

**Caso di business:** *Organizza in modo efficiente le risorse per semplificare i flussi di lavoro.*

Per un’organizzazione efficiente delle risorse in grado di semplificare i flussi di lavoro, utilizza una o più delle seguenti best practice:

* **Organizzare le risorse nelle cartelle:**
L’organizzazione efficace delle risorse comporta la loro classificazione in cartelle, in modo analogo all’organizzazione dei file su un computer. La denominazione corretta, la strutturazione delle sottocartelle e la gestione dei file all’interno di queste cartelle sono fondamentali per un’elaborazione efficiente delle risorse. L’implementazione di convenzioni di denominazione sistematica e pratiche per i metadati ottimizza l’utilità dell’archivio delle risorse digitali.
Vuoi saperne di più? Vai a [Organizzare le risorse nelle cartelle](/help/assets/organize-assets.md#organize-using-folders).
* **Organizzare le risorse utilizzando i tag:**
L’assegnazione tag alle risorse migliora la ricercabilità, la creazione di raccolte e la classificazione delle ricerche. L’intelligenza artificiale di Adobe Sensei utilizza un algoritmo di apprendimento automatico per l’assegnazione di tag precisi, che consente di recuperare rapidamente le risorse. Adobe Sensei riconosce e assegna inoltre tag rilevanti alle risorse, inclusi quelli personalizzati, semplificando la gestione delle risorse con l’assegnazione automatica di tag descrittivi.
Vuoi saperne di più? Vai a [Organizza le risorse utilizzando i tag](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **Organizza risorse come raccolte:**
Dynamic Media, insieme a Experience Manager Assets, consente di creare, modificare e condividere in modo efficiente le raccolte di risorse tra gli utenti. È possibile stabilire vari tipi di raccolta, inclusi gli elenchi statici e le compilazioni dinamiche basate su ricerche. Questi tipi di raccolte possono essere condivisi in diverse posizioni con diritti di accesso e modifica personalizzabili.
Vuoi saperne di più? Vai a [Organizza risorse come raccolte](/help/assets/manage-collections.md).
* **Organizzare le risorse utilizzando i profili:**
Un profilo di elaborazione automatizza la gestione delle risorse in cartelle specifiche, semplificando l’organizzazione. La standardizzazione di metadati, nomi di file e strutture di cartelle consente un’applicazione coerente e precisa di questi profili man mano che la raccolta di risorse digitali si espande.
Vuoi saperne di più? Vai a [Organizza le risorse utilizzando i profili](/help/assets/organize-assets.md#organize-to-use-profiles).



### Ottimizzare la qualità delle immagini

**Caso di business:** *Ottieni immagini di buona qualità da Dynamic Media.*

Per migliorare la qualità dell&#39;immagine è necessario considerare attentamente diversi fattori. Può richiedere molto tempo. Tuttavia, esistono alcune pratiche consolidate che possono aiutarti a raggiungere risultati desiderabili. Alcune di queste best practice includono come ottenere dimensioni ottimali dell’immagine, nitidezza e formati di immagine ottimali.

Vuoi saperne di più? Vai a [Best practice per ottimizzare la qualità delle immagini](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

Poiché la percezione della qualità dell&#39;immagine varia da persona a persona, a volte un approccio sistematico alla sperimentazione è essenziale per ottenere risultati desiderabili. Adobe Experience Manager facilita questo processo con più di 100 comandi Dynamic Media per il miglioramento delle immagini.

Vuoi saperne di più? Guarda [Snapshot Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minuti, 17 secondi).

Per valutare l’impatto di questi diversi comandi sulla qualità delle immagini, puoi caricare un’immagine in Dynamic Media, utilizzare l’interfaccia dello strumento all’URL specificato e applicare i comandi che desideri provare.

Vuoi provarlo? Avvia [Snapshot Dynamic Media](https://snapshot.scene7.com/)

### Standardizzazione degli stili applicati alle immagini

**Caso di business:** *Standardizza in modo efficiente lo stile e la trasformazione applicati alle risorse immagine.*

Utilizza i predefiniti per immagini regolarmente in Dynamic Media per regolare in modo coerente e dinamico le dimensioni, i formati e le proprietà delle immagini. Considera un predefinito immagine come una macro: è un set denominato di comandi per il dimensionamento e la formattazione. Ad esempio, se il sito necessita di immagini di prodotto in varie dimensioni e formati, con una compressione specifica per desktop e dispositivi mobili, i predefiniti immagine automatizzano questo processo in modo efficiente.

Vuoi provarlo? Vai a [Nozioni di base sulla creazione di predefiniti immagine per il rendering delle risorse](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### Regolare la messa a fuoco e l&#39;inquadratura di immagini e video

**Caso di business:** *Assicurati che il punto di interesse principale delle mie immagini o dei miei video rimanga attivo tra i dispositivi.*

Smart Crop è una funzione di Dynamic Media che utilizza Adobe Sensei, il framework di intelligenza artificiale e machine learning di Adobe, per automatizzare il ritaglio di immagini e video. Rileva e mette a fuoco in modo intelligente il soggetto principale o il punto di interesse in un&#39;immagine o in un video. Questa intelligenza assicura che il punto focale venga mantenuto su schermi di varie dimensioni su computer desktop e dispositivi mobili.

Una best practice prevede la creazione di un profilo immagine con Ritaglio avanzato. Nel profilo, puoi definire diverse dimensioni dello schermo e consentire ad Adobe Sensei di fare il resto, assicurandoti che le immagini e i video siano sempre ottimizzati per il dispositivo dell’utente.

Vuoi saperne di più? Guarda [Utilizzo di Ritaglio avanzato con AEM Assets Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minuti, 35 secondi) e [Utilizzo di Ritaglio avanzato Dynamic Media per video](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) (6 minuti, 22 secondi).

### Migliorare le classificazioni SEO

**Caso di business:** *Configura Dynamic Media per ottenere classificazioni SEO migliorate.*

Utilizza regolarmente le seguenti raccomandazioni per garantire che le immagini contribuiscano in modo efficace alla strategia SEO complessiva.

* **Nomi file immagine significativi:**
Utilizza nomi di file descrittivi che riflettono il contenuto dell’immagine. Ad esempio,

   * utilizza `myCompany-Silver-Wrist-Watch`
   * *evitare* `myCompany_Silver_Wrist_Watch` o `myCompanySilverWristWatch`

  In questo modo i motori di ricerca possono comprendere il contesto dell’immagine e migliorare la SEO (Search Engine Optimization). Google preferisce i trattini ai caratteri di sottolineatura o agli spazi nel nome di un file. Inoltre, evita di concatenare le parole in un nome di file.
* **Dominio personalizzato:**
Implementa un dominio personalizzato che includa la tua azienda o il tuo nome del brand per rafforzare il riconoscimento e la fiducia nel brand. Ad esempio,

   * utilizza `http://images.mycompany.com/is/image/companyname/`
   * *evitare* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`

* **Struttura delle cartelle compatibile con SEO:**
Organizza le immagini in una struttura di cartelle che includa il nome o il marchio della tua azienda per una migliore indicizzazione, come `http://images.mycompany.com/is/image/companyname/`.
* **Set di regole di Dynamic Media:**
Scopri come trasformare gli URL in modo condizionale in base a vari fattori, migliorando la SEO e l’esperienza utente.
Vuoi saperne di più? Vai a [Utilizza i set di regole per trasformare gli URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **Imaging avanzato e ritaglio avanzato:**
Utilizza le funzioni Smart Imaging e Ritaglio avanzato in Dynamic Media per distribuire immagini ottimizzate e reattive. In questo modo non solo migliora i tempi di caricamento delle pagine, ma contribuisce anche positivamente alle classificazioni SEO (Search Engine Optimization).
Vuoi saperne di più? Vai a [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) oppure guarda [Utilizzo di Smart Crop con AEM Assets Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minuti, 35 secondi).

Ricorda che queste best practice si allineano bene con le best practice Google per l’immagine SEO. Tali pratiche sottolineano l’importanza di fornire contesto e chiarezza ai motori di ricerca attraverso convenzioni di denominazione appropriate, dati strutturati e consegna di immagini ottimizzata.

Vuoi saperne di più? Vai a [Best practice per la struttura degli URL per Google](https://developers.google.com/search/docs/crawling-indexing/url-structure) e [Best practice SEO per le immagini Google](https://developers.google.com/search/docs/appearance/google-images)

### Miglioramento dinamico delle immagini e creazione di effetti visivi tramite comandi

**Caso di business:** *Applica effetti visivi avanzati alle immagini.*

Dynamic Media offre una suite di comandi per migliorare le immagini e creare effetti visivi in modo dinamico, senza la necessità di disporre di più risorse statiche. Di seguito sono riportate alcune brevi spiegazioni di alcuni di questi processi e alcuni esempi utili per guidarti:

#### Effetti nell&#39;immagine sorgente

| Attività | Cosa fare |
| --- | --- |
| **Carica e pubblica l&#39;immagine originale** | <ul><li> Per iniziare, carica l’immagine originale in Dynamic Media.</li><li> Assicurati che sia pubblicato e accessibile tramite un URL.</li><li> In questo esempio, viene caricata su Dynamic Media un’immagine d’archivio di un orologio con sfondo bianco (chiamiamola &quot;Immagine X&quot;).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer)</li></ul> |
| **Creare una maschera** | <ul><li> Sviluppare una maschera che definisca il soggetto (l&#39;area in cui si desidera applicare gli effetti) e lo sfondo (l&#39;area che si desidera modificare).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)</li><li> Le maschere sono in genere immagini in scala di grigio, dove il bianco rappresenta il soggetto e il nero rappresenta lo sfondo. Puoi creare maschere utilizzando strumenti come Adobe Photoshop.<br>Ulteriori informazioni? Vai a [Creazione e modifica di una maschera rapida in Photoshop](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).</li><li> Per &quot;Immagine X&quot;, creare una maschera che delinei con precisione il soggetto che si desidera migliorare. Ad esempio, una persona, un oggetto e così via.</li></ul> |
| **Applicare i comandi URL Dynamic Media per gli effetti** | Dopo aver inserito la maschera, usate i comandi URL per applicare effetti come un bagliore esterno o cambiate il colore di sfondo in &quot;Immagine X&quot;. Di seguito sono riportati due esempi:<ul><li> **Effetto bagliore esterno:**<br> Per aggiungere un effetto bagliore esterno lungo il limite del soggetto, modificare l&#39;URL in questo modo:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&effect=-1&pos=100,100&op_blur=75&op_grow=1&opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&effect=-1&pos=100,100&op_blur=75&op_grow=1&opac=25)<br>In questo URL, i parametri `op_blur`, `op_grow` e `opac` creano l&#39;effetto bagliore esterno.</li><li> **Modifica colore di sfondo:**<br> Per modificare il colore di sfondo, utilizzare l&#39;URL con un valore diverso per il colore di sfondo:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&maskUse=invert&color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&maskUse=invert&color=255,255,0)<br> In questo esempio, `color=255,255,0` imposta il colore di sfondo su giallo. Modifica lo sfondo con un colore specifico per un impatto visivo.</li></ul> |

#### Aggiungi un bordo immagine

Dynamic Media consente di manipolare le immagini direttamente tramite URL, rendendole uno strumento potente per la creazione di esperienze digitali dinamiche. Di seguito sono riportati alcuni esempi. Iniziamo con il seguente URL immagine originale: [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| Attività | Cosa fare |
| --- | --- |
| **Bordo bianco** | Per aggiungere un bordo bianco, utilizzare il seguente URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10)<br>In questo URL, il parametro `extend=10,10,10,10` specifica la dimensione del bordo di dieci pixel su tutti i lati. |
| **Sfocatura lungo il bordo bianco** | Per aggiungere un effetto sfocatura lungo il bordo bianco, è possibile modificare l&#39;URL nel modo seguente:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&op_blur=60&color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&op_blur=60&color=0,0,0)<br>In questo URL, il parametro `effect=-1` applica l&#39;effetto sfocatura e `op_blur=60` controlla l&#39;intensità della sfocatura. |
| **Abbassare l&#39;effetto ombreggiatura lungo il limite esterno** | Per aggiungere un effetto ombreggiatura esterna lungo il limite esterno, utilizzare questo URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&$shadow$&color=0,0,0)<br>Il parametro `$shadow$` crea l&#39;effetto ombreggiatura e `color=0,0,0` imposta il colore dell&#39;ombreggiatura su nero. |

Puoi sperimentare questi URL per ottenere gli effetti visivi desiderati.

#### Creare sovrapposizioni immagine

Se desideri sovrapporre un logo o un’icona a un’immagine esistente, Dynamic Media fornisce un modo semplice per farlo utilizzando i comandi URL. Suddividiamo i passaggi.

| Passaggio | Cosa fare |
| --- | --- |
| **Carica e pubblica l&#39;immagine di base** | Innanzitutto, carica e pubblica l&#39;immagine di base sulla quale vuoi sovrapporre il logo o l&#39;icona. È possibile utilizzare qualsiasi immagine come base.<br>Questa è un&#39;immagine di base:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **Carica e pubblica l&#39;immagine del logo o dell&#39;icona** | Quindi, carica e pubblica l’immagine che desideri sovrapporre all’immagine di base. L&#39;immagine deve essere un file PNG trasparente con il logo o l&#39;icona che si desidera sovrapporre.<br>Immagine PNG trasparente di un oggetto stella con effetti di trasparenza che verrà sovrapposta:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Applica l&#39;URL di Dynamic Media** | Ora crea un URL Dynamic Media che combina l’immagine di base con l’immagine del logo o dell’icona. Per ottenere questo effetto, puoi utilizzare i comandi URL.<br>La struttura dell&#39;URL è simile alla seguente:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&src=decorate-star&scale=1.25&posN=0.33,-.25&fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&src=decorate-star&scale=1.25&posN=0.33,-.25&fmt=png)<br>in cui la risorsa<ul><li> `hotspotRetailBaseImage` è l&#39;immagine di base.</li><li> `starxp` è l&#39;immagine del logo/icona.</li><li> `layer=1` specifica che il logo o l&#39;icona deve essere sovrapposto all&#39;immagine di base.</li><li> `scale=1.25` regola le dimensioni del logo o dell&#39;icona.</li><li> `posN=0.33,-.25` determina la posizione del logo/icona rispetto all&#39;immagine di base.</li><li> `fmt=png` assicura che l&#39;output sia in formato PNG.</li></ul> |

Per saperne di più Vai a [src](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) per ulteriori dettagli sul comando `src` e altri comandi URL Dynamic Media.


#### Sovrapposizione del testo promozionale

Di seguito sono riportati i passaggi per sovrapporre un messaggio di testo promozionale su un’immagine utilizzando HTML e CSS.

| Passaggio | Cosa fare |
| --- | --- |
| **Carica e pubblica l&#39;immagine di base** | Innanzitutto, carica e pubblica l’immagine di base sulla quale vuoi sovrapporre il testo. Puoi usare qualsiasi immagine ti piaccia. Esempio: <br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Applica operatori di testo Dynamic Media** | Dynamic Media consente di applicare operatori di testo per sovrapporre il testo dinamico direttamente sull’immagine. L&#39;URL di esempio seguente dimostra questa capacità:<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&posN=-0.3,-0.455&text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&posN=-0.3,-0.455&text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&size=370,70&textAttr=130&bgcolor=FF333&wid=600&hei=600) |

#### Ridimensionamento e ritaglio per vari casi d’uso

##### Nozioni di base sul ridimensionamento delle immagini

Il ridimensionamento dell&#39;immagine comporta la modifica delle dimensioni, della risoluzione e delle dimensioni del file di un&#39;immagine. Di seguito sono riportati alcuni punti chiave da considerare:

* **Composizione pixel:**
Le immagini digitali sono costituite da piccoli punti denominati pixel. Quando viene creata un&#39;immagine, questa ha un numero specifico di pixel. Il ridimensionamento comporta l&#39;aggiunta o la sottrazione di pixel per modificare le dimensioni, la risoluzione e le dimensioni del file dell&#39;immagine.
* **Proporzioni:**
Per evitare distorsioni, è fondamentale mantenere le proporzioni (rapporto tra larghezza e altezza). Indipendentemente dal fatto che un&#39;immagine sia ingrandita (upscaling) o ridotta (downscaling), il mantenimento delle proporzioni assicura la coerenza visiva.
* **Considerazioni sulla qualità:**
Il ridimensionamento può influire sulla qualità delle immagini. Evitare un aumento drastico del volume, in quanto può causare pixelazione. Piuttosto, è consigliabile riprodurre l&#39;immagine con dimensioni e risoluzione maggiori. Per le immagini più piccole, usate gli strumenti appropriati per mantenere la risoluzione.

##### Ritaglio e ridimensionamento

In Dynamic Media, il ritaglio e il ridimensionamento sono tecniche che consentono di trasformare le immagini in base ai vari casi d’uso, sia che si tratti della creazione di miniature, di immagini di visualizzazione del prodotto o di banner.

* **Ritaglio:**
Comporta la rimozione di parte di un&#39;immagine per modificarne la composizione e l&#39;inquadratura. Non modifica le dimensioni complessive, ma si concentra su un’area specifica.
* **Ridimensionamento:**
Regola le dimensioni, la risoluzione e le dimensioni del file dell&#39;intera immagine mantenendo le proporzioni.

Esaminiamo un caso d’uso che coinvolge la seguente immagine del salotto:

* **Immagine originale soggiorno:**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **Miniatura (200 px x 200 px):**
Una versione più piccola adatta per il caricamento o la visualizzazione rapidi.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&fit=crop)
* **Miniatura con ritaglio (200 px x 200 px):**
Ritagliato per concentrarsi sull&#39;area del divano.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&cropN=.24,.24,.6,.72&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&cropN=.24,.24,.6,.72&fit=crop)
* **Immagine di visualizzazione del prodotto (800 px x 600 px):**
Ritagliato e ridimensionato per esporre il divano.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&hei=600&cropN=.24,.24,.6,.72&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&hei=600&cropN=.24,.24,.6,.72&fit=crop)
* **Banner (1720 px x 820 px):**
Derivato dall&#39;immagine originale, enfatizzando la stanza.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&hei=820&cropN=0,.1,1,1&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&hei=820&cropN=0,.1,1,1&fit=crop)

Puoi esplorare queste varianti in base alle tue esigenze specifiche.
Vuoi saperne di più sui comandi disponibili all’interno di un URL? Vai a [Riferimento comando](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### Distribuisci immagini GIF

**Caso di business:** *Trasmetti file GIF tramite Dynamic Media*

Puoi caricare e distribuire GIF tramite Dynamic Media. Per eseguire il rendering di un GIF animato, sostituisci `is/image` con `is/content` nell&#39;URL. Ad esempio, se hai caricato `abc.gif`, utilizza quanto segue:

* Questo percorso URL esegue il rendering di una vista statica del GIF:

  ```
  https://your.domain.com/is/image/yourfolder/abc
  ```

* Questo percorso URL esegue il rendering della visualizzazione animata del GIF:

  ```
  https://your.domain.com/is/content/yourfolder/abc
  ```

>[!NOTE]
>
>Quando si utilizza `is/content` nel percorso URL, i comandi di trasformazione delle immagini non vengono applicati alla risorsa.

### Pubblica un video per il mio sito web

**Caso di business:** *Pubblica rapidamente un video per un sito di marketing.*

* **Selezionare un profilo video:**
Innanzitutto, in Dynamic Media, devi selezionare un profilo video appropriato. Puoi optare per il profilo *Codifica video adattiva* disponibile in AEM Assets alla voce Profili video. Queste impostazioni di codifica predefinite assicurano che il video sia ottimizzato per la riproduzione su vari dispositivi e condizioni di larghezza di banda. In alternativa, puoi creare un tuo profilo video adattivo.
* **Assegna il profilo:**
Assegna il profilo video scelto alle cartelle in cui il video verrà caricato. Questo passaggio garantisce che vengano applicate le impostazioni di codifica corrette durante il processo di caricamento.
* **Carica il video originale:**
Carica il file video originale. Assicurati che sia un video ad alta risoluzione di buona qualità. Migliore è il video sorgente, migliore è il risultato finale.
* **Anteprima e pubblicazione:**
Visualizza l’anteprima del video per assicurarti che tutto si presenti come previsto. Una volta soddisfatto, procedi e pubblicalo. Questo passaggio rende il video accessibile al pubblico.
* **Collegamento o incorporamento:**
Dopo la pubblicazione, sono disponibili due opzioni.

   * **Collegamento diretto:**
Utilizza l’URL fornito per il collegamento diretto al video. Inseriscilo nel collegamento appropriato sul sito di marketing.
   * **Incorpora il video:**
Copia il codice incorporato fornito e incollalo nel HTML della pagina web in cui desideri visualizzare il video. In questo modo il video può essere riprodotto direttamente sul sito.

Vuoi saperne di più? Vai a [Video](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### Configurare i video per una qualità e un coinvolgimento ottimali

**Caso di business:** *Configura i video per la qualità e il coinvolgimento migliori.*

Per garantire la qualità e il coinvolgimento migliori per i tuoi video, puoi implementare una combinazione delle seguenti strategie per le best practice:

* **Utilizza il visualizzatore video integrato di HTML5:**
I predefiniti per visualizzatore video Dynamic Media HTML5 sono lettori video affidabili. Utilizzali per evitare i problemi più comuni associati alla riproduzione di video HTML5 e ai dispositivi mobili.
Questi predefiniti risolvono problematiche quali la distribuzione di streaming con bitrate adattivo e la portata limitata del browser desktop.
Vuoi saperne di più? Vai a [Best practice: utilizzo del visualizzatore video di HTML 5](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **Usa profili video Dynamic Media:**
I profili video in Dynamic Media consentono una gestione video efficiente, una qualità coerente e uno streaming adattivo.
Vuoi saperne di più? Vai a [Profili video Dynamic Media](/help/assets/dynamic-media/video-profiles.md).

* **Best practice per la codifica video:**
Applicare profili di codifica video che mantengano la qualità video originale senza downscaling eccessivo durante la codifica.
Vuoi saperne di più? Vai a [Best practice per la codifica dei video](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **Adottare lo streaming adattivo invece dello streaming progressivo:**
Lo streaming adattivo regola la qualità video in base alla velocità di connessione Internet e alle funzionalità del dispositivo dell’utente.
Utilizza protocolli come HLS (HTTP Live Streaming) o DASH (`Dynamic Adaptive Streaming over HTTP`) per garantire una qualità di riproduzione ottimale.
A differenza dello streaming progressivo, che offre video in modo lineare, lo streaming adattivo riduce al minimo il buffering e offre un’esperienza di visualizzazione fluida.

### Internazionalizzazione dei video per il consumo multilingue

**Caso di business:** *Prepara i video per il consumo multilingue.*

L’internazionalizzazione dei video per il consumo multilingue è essenziale per raggiungere un pubblico globale. Dynamic Media fornisce funzioni che possono aiutarti a raggiungere questo obiettivo.

* **Carica i tuoi video:**
   * Crea un profilo di codifica video. Puoi utilizzare il profilo di codifica video adattivo predefinito fornito con Dynamic Media oppure creare un profilo personalizzato.
   * Associa il profilo di elaborazione video a una o più cartelle in cui carichi i video sorgente principali.
   * Carica i video sorgente principali in queste cartelle. Dynamic Media li codifica in base al profilo di elaborazione video assegnato.
   * Dynamic Media supporta principalmente video in formato breve (fino a 30 minuti) con una risoluzione minima superiore a 25 × 25. È possibile caricare file video fino a 15 GB ciascuno1.

* **Gestione dei video:**
   * Organizza, sfoglia e cerca risorse video in AEM.
   * Visualizzare in anteprima e pubblicare le risorse video.
   * Visualizza il video sorgente e le relative rappresentazioni codificate insieme alle miniature associate.
   * Modifica le proprietà del video, come titolo, descrizione e tag2.

* **Localizzazione:**
   * Per ogni area geografica/lingua di destinazione, create tracce audio e sottotitoli.
   * Aggiungi questi brani audio e sottotitoli ai tuoi video dall’interfaccia di AEM.
   * Durante la riproduzione dei video, gli utenti possono selezionare la lingua preferita per l&#39;audio e i sottotitoli.

* **Pubblicazione:**
   * Se utilizzi AEM come sistema di gestione dei contenuti web (WCM), puoi aggiungere video direttamente alle pagine web.
   * Se utilizzi un sistema WCM di terze parti, puoi collegare o incorporare video sulle pagine web utilizzando URL o codici di incorporamento.

Vuoi saperne di più? Vai a [Informazioni sul supporto di più didascalie e tracce audio per i video in Dynamic Media](/help/assets/dynamic-media/video.md#about-msma).


## Distribuire risorse ai clienti

### Ottimizzare le dimensioni delle immagini e ridurre i tempi di caricamento delle pagine

**Caso di business:** *Ottimizza le dimensioni delle immagini per qualsiasi browser o schermo e riduci il tempo di caricamento delle pagine.*

L’imaging avanzato Dynamic Media è uno strumento potente che migliora le prestazioni di consegna delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità dell’immagine in base alle funzionalità del browser del cliente.

Adobe consiglia di utilizzare le funzionalità di Smart Imaging anziché impostare manualmente il formato immagine su `webp` o `avif`. Ecco il motivo:

* **Compatibilità browser:**
La tecnologia Smart Imaging garantisce che il formato dell&#39;immagine fornita sia compatibile con il browser dell&#39;utente.
* **Compressione ottimale:**
Seleziona il formato migliore per la compressione in base al browser, alle condizioni di rete e alla risoluzione dello schermo.
* **Formati moderni:**
Sebbene `avif` sia un formato più recente che offre una compressione migliore, non è ancora supportato universalmente in tutti i browser.
* **Best practice:**
Per garantire il miglior formato ottimizzato per il Web, è possibile utilizzare Smart Imaging per effettuare la selezione del formato anziché utilizzare manualmente i comandi `fmt=webp` o `fmt=avif`.

Affidandoti a Smart Imaging, puoi garantire che le immagini vengano distribuite nel modo più efficiente possibile, su misura per l’ambiente di navigazione di ogni utente. Questo approccio semplifica il processo e può migliorare le prestazioni in termini di tempi di caricamento delle immagini e di esperienza d’uso complessiva.

Vuoi saperne di più? Vai a [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md).

### Consegna delle risorse ai clienti

**Caso di business:** *Dopo aver pubblicato nuovi contenuti o sovrascritto quelli esistenti, come è possibile garantire che le modifiche vengano visualizzate immediatamente sulla rete CDN?*

La rete CDN (Content Delivery Network) memorizza in cache le risorse Dynamic Media per consentirne la distribuzione rapida ai clienti. Quando vengono apportati aggiornamenti a queste risorse, è importante che le modifiche diventino effettive immediatamente sul sito web. Rimuovendo o annullando la validità della cache CDN, le risorse distribuite da Dynamic Media possono essere aggiornate rapidamente. Questo approccio elimina la necessità di attendere la scadenza della cache in base al valore TTL (Time To Live), che in genere è impostato su dieci ore. A seconda del caso d’uso specifico, puoi aggiornare di conseguenza le impostazioni TTL (Time to Live) della rete CDN.

Vuoi saperne di più? Vai a [Invalida la cache CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

