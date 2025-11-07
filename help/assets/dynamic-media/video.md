---
title: Video in Dynamic Media
description: Scopri come utilizzare i video in Dynamic Media. Rivedi le best practice per la codifica di video, la pubblicazione di video in YouTube, la visualizzazione di rapporti video e l’aggiunta di sottotitoli o marcatori capitolo ai video.
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '10063'
ht-degree: 2%

---

# Video {#video}

Questa sezione descrive come lavorare con i video in Dynamic Media.

## Guida introduttiva: Video {#quick-start-videos}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a utilizzare i set per video adattivi in Dynamic Media. Dopo ogni passaggio, sono disponibili riferimenti incrociati alle intestazioni degli argomenti in cui è possibile trovare ulteriori informazioni.

>[!NOTE]
>
>Prima di lavorare con i video in Dynamic Media, accertati che l’amministratore di Adobe Experience Manager abbia già abilitato e configurato i servizi cloud per elementi multimediali dinamici.
>
>* Consulta [Configurare i servizi cloud Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media e [Risolvere i problemi relativi a Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).
>

1. **Carica i video Dynamic Media** effettuando le seguenti operazioni:

   * Crea un tuo profilo di codifica video. In alternativa, puoi semplicemente utilizzare il profilo predefinito _Codifica video adattivo_ fornito con Dynamic Media.

      * [Crea un profilo di codifica video](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * La risoluzione massima di codifica video in uscita è 8.192 × 4.320 o 4.320 × 8.192.md.
      * Ulteriori informazioni su [Best practice per la codifica video](#best-practices-for-encoding-videos).

   * Associa il profilo di elaborazione video a una o più cartelle in cui stai per caricare i video sorgente principali.

      * [Applicare un profilo video alle cartelle](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Ulteriori informazioni su [Organizzare risorse digitali](/help/assets/organize-assets.md).

   * Carica i video sorgente principali nelle cartelle specificate. Una volta aggiunti, i video vengono codificati in base al profilo di elaborazione video assegnato alla cartella.

      * Dynamic Media supporta principalmente video in formato breve con una lunghezza massima di 30 minuti e una risoluzione minima superiore a 25 × 25.
      * La risoluzione video in ingresso massima supportata è 16.384 × 16.384.
      * Puoi caricare file video con una capacità massima di 15 GB ciascuno.
      * [Carica i tuoi video](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Ulteriori informazioni sui [Formati di file di input supportati](/help/assets/file-format-support.md).

   * Monitora l&#39;avanzamento della codifica [video](#monitoring-video-encoding-and-youtube-publishing-progress) dalla visualizzazione della risorsa o del flusso di lavoro.

1. **Gestisci i video Dynamic Media** eseguendo una delle seguenti operazioni:

   * Organizzare, sfogliare e cercare risorse video

      * [Organizzare le risorse digitali](/help/assets/organize-assets.md)
      * [Ricerca risorse video](/help/assets/search-assets.md#custompredicates) o [Ricerca risorse](/help/assets/manage-digital-assets.md#search-assets)

   * Visualizzare in anteprima e pubblicare le risorse video

      * Visualizza il video sorgente e le relative rappresentazioni codificate, insieme alle miniature associate:
        [Anteprima video](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) o [Anteprima risorse](/help/assets/dynamic-media/previewing-assets.md)
        [Gestione rappresentazioni video](/help/assets/manage-digital-assets.md#managing-renditions)

      * [Gestire i predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [Pubblicazione delle risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * Utilizzare i metadati video

      * Modifica le proprietà del video come il titolo, la descrizione, i tag e i campi di metadati personalizzati:
        [Modifica proprietà video](/help/assets/manage-digital-assets.md#editing-properties)

      * [Gestire i metadati per le risorse digitali](/help/assets/manage-metadata.md)
      * [Schemi di metadati](/help/assets/metadata-schemas.md)

   * Rivedi, approva e commenta video e mantieni il controllo completo della versione

      * [Annota video](/help/assets/manage-video-assets.md#annotate-video-assets) o [Aggiunta di annotazioni alle risorse](/help/assets/manage-digital-assets.md#annotating)

      * [Crea una versione](/help/assets/manage-digital-assets.md#asset-versioning)
      * [Avviare un flusso di lavoro su una risorsa](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [Esaminare le risorse della cartella](/help/assets/bulk-approval.md)
      * [Progetti](/help/sites-cloud/authoring/projects/overview.md)

1. **Pubblica i tuoi video Dynamic Media** effettuando una delle seguenti operazioni:

   * Se utilizzi Experience Manager come sistema WCM (Web Content Management), puoi aggiungere video direttamente alle pagine web.

      * [Aggiungi video alle pagine Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

   * Se utilizzi un sistema WCM di terze parti, puoi collegare o incorporare video nelle pagine web.

      * Integra video tramite URL:
        [Collega URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integra video utilizzando il codice di incorporamento in una pagina web:
        [Incorpora il visualizzatore video in una pagina Web](/help/assets/dynamic-media/embed-code.md).

   * [Genera report video](#viewing-video-reports).

   * [Aggiungere più didascalie e tracce audio a un video](#about-msma).

## Utilizzare i video in Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media è una soluzione end-to-end che consente di pubblicare facilmente video adattivi di alta qualità per lo streaming su più schermi, inclusi desktop, tablet e dispositivi mobili. Un set video adattivo raggruppa le versioni dello stesso video che sono codificate in diversi formati e bit rate, ad esempio 400 kbps, 800 kbps e 1000 kbps. Il computer desktop o il dispositivo mobile rileva la larghezza di banda disponibile.

Ad esempio, su un dispositivo mobile iOS rileva una larghezza di banda, come 3G, 4G o Wi-Fi. Quindi seleziona automaticamente il video codificato giusto tra i vari bit rate video all’interno del set video adattivo. Il video viene inviato in streaming a desktop, dispositivi mobili o tablet.

Inoltre, la qualità video viene commutata automaticamente se cambiano le condizioni di rete sul desktop o sul dispositivo mobile. Inoltre, se un cliente entra in modalità a tutto schermo su un desktop, il set video adattivo risponde con una risoluzione migliore, migliorando l’esperienza di visualizzazione del cliente. L’utilizzo di set video adattivi offre la migliore esperienza di visualizzazione possibile ai clienti che riproducono video Dynamic Media su più schermi e dispositivi.

La logica utilizzata da un lettore video per determinare quale video codificato riprodurre o selezionare durante la riproduzione si basa sul seguente algoritmo:

1. Il lettore video carica il frammento video iniziale in base al bitrate più vicino al valore impostato per &quot;bitrate iniziale&quot; nel lettore stesso.
1. Il lettore video cambia in base alle modifiche apportate alla velocità della larghezza di banda utilizzando i seguenti criteri:

   1. Il lettore sceglie il flusso di larghezza di banda più alto al di sotto o uguale alla larghezza di banda stimata.
   1. Il lettore considera solo l’80% della larghezza di banda disponibile. Tuttavia, in caso di passaggio, è più prudente con solo il 70% per evitare di sovrastimare e tornare subito indietro.

Per informazioni tecniche dettagliate sull&#39;algoritmo, vedere [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Durante la gestione di un singolo video e di set di video adattivi, sono supportati i seguenti elementi:

* Caricamento di video da numerosi formati video e formati audio supportati. Codifica del video in formato MP4 H.264 per la riproduzione su più schermi. È possibile utilizzare predefiniti per video adattivi, predefiniti per codifica video singola o personalizzare la propria codifica per controllare la qualità e le dimensioni del video.

   * Quando viene generato un set video adattivo, questo include video MP4.
   * **Nota**: i video principali/di origine non vengono aggiunti a un set di video adattivi.

* Sottotitoli video in tutti i visualizzatori video HTML5.
* Organizza, sfoglia e cerca video con supporto completo per i metadati, per una gestione efficiente delle risorse video.
* Distribuisci set video adattivi per web e desktop, tablet e dispositivi mobili.

Lo streaming video adattivo è supportato su varie piattaforme iOS. Consulta la [Guida di riferimento per i visualizzatori Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Riproduci il video utilizzando i predefiniti visualizzatore video Dynamic Media, tra cui:

   * Visualizzatori video singoli.
   * Visualizzatori di file multimediali diversi che combinano contenuti sia video che immagini.

* Configura i lettori video in base alle tue esigenze di branding.
* Integra il video nel tuo sito web, sito mobile o app mobile con un semplice URL o codice da incorporare.

<!-- GIVES a 404 See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Vedere anche [Visualizzatori per Experience Manager Assets e Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc) e [Visualizzatori solo per Experience Manager Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) nella [Guida di riferimento visualizzatori Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).

## Best practice: utilizzo del visualizzatore video HTML5 {#best-practice-using-the-html-video-viewer}

I predefiniti visualizzatore video Dynamic Media HTML5 sono lettori video affidabili. Puoi utilizzarli per evitare molti problemi comuni associati alla riproduzione di video HTML5 e problemi associati ai dispositivi mobili. Ad esempio, una mancanza di distribuzione di streaming bitrate adattivo e una portata limitata del browser desktop.

Dal lato della progettazione del lettore, puoi progettare le funzionalità del lettore video utilizzando gli strumenti di sviluppo web standard. Ad esempio, puoi progettare pulsanti, controlli e sfondo personalizzato per le immagini del poster utilizzando HTML5 e CSS per raggiungere i clienti con un aspetto personalizzato.

Sul lato di riproduzione del visualizzatore, rileva automaticamente la funzionalità video del browser. Distribuisce quindi il video utilizzando HLS o DASH, noto anche come streaming video adattivo. In alternativa, se tali metodi di distribuzione non sono presenti, viene utilizzato HTML5 progressive.

È possibile combinare in un unico lettore la possibilità di progettare i componenti di riproduzione utilizzando HTML5 e CSS. Può avere una riproduzione incorporata e utilizzare uno streaming adattivo e progressivo a seconda delle funzionalità del browser. Tutte queste funzionalità consentono di estendere la portata dei contenuti rich media agli utenti desktop e mobili e di garantire un&#39;esperienza video semplificata.

Vedi anche [Visualizzatori solo per Experience Manager Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) nella [Guida di riferimento per visualizzatori Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).


### Riproduzione di video su computer desktop e dispositivi mobili mediante il visualizzatore video HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Per lo streaming video adattivo per desktop e dispositivi mobili, i video utilizzati per il passaggio a bit rate si basano su tutti i video MP4 nel set di video adattivi.

La riproduzione del video viene eseguita mediante HLS o DASH oppure mediante il download di video progressivi. Nelle versioni precedenti di Experience Manager, come 6.0, 6.1 e 6.2, i video venivano inviati in streaming tramite HTTP.

Tuttavia, in Experience Manager 6.3 e versioni successive, i video vengono ora inviati in streaming tramite HTTPS (ovvero HLS o DASH) perché l’URL del servizio gateway DM utilizza sempre HTTPS. Questo comportamento predefinito non ha alcun impatto sul cliente. Lo streaming video si verifica sempre tramite HTTPS se il browser lo supporta. Vedi la tabella seguente.

Pertanto,

* Se disponi di un sito web HTTPS con streaming video HTTPS, lo streaming va bene.
* Se disponi di un sito web HTTP con streaming video HTTPS, lo streaming va bene e non vi sono problemi di contenuti misti dal browser web.

DASH è lo standard internazionale e HLS è uno standard Apple. Entrambi vengono utilizzati per lo streaming video adattivo. Entrambe le tecnologie regolano automaticamente la riproduzione in base alla capacità della larghezza di banda della rete. Consente inoltre al cliente di &quot;cercare&quot; in qualsiasi punto del video senza dover attendere il download del resto del video.

Il video progressivo viene distribuito scaricando e memorizzando il video localmente sul sistema desktop o sul dispositivo mobile di un utente.

Nella tabella seguente vengono descritti il dispositivo, il browser e il metodo di riproduzione dei video su computer desktop e dispositivi mobili che utilizzano [Visualizzatore video Dynamic Media HTML5](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video#interactive-video).

<table>
 <tbody>
  <tr>
   <td><strong>Dispositivo</strong></td>
   <td><strong>Browser</strong></td>
   <td><strong>Modalità di riproduzione video</strong></td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Internet Explorer 9 e 10</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Internet Explorer 11+</td>
   <td>In Windows® 8 e Windows® 10 - Forza l'uso di HTTPS ogni volta che viene richiesto DASH o HLS. Limitazione nota: HTTP su DASH o HLS non funziona in questa combinazione browser/sistema operativo<br /> <br /> In Windows® 7 - Download progressivo. Usa la logica standard per il protocollo HTTP rispetto a HTTPS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 23-44</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 45 o versione successiva</td>
   <td>Streaming bitrate adattivo HLS o DASH*</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Chrome</td>
   <td>Streaming bitrate adattivo HLS o DASH*</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Safari (Mac)</td>
   <td>Streaming bitrate adattivo HLS</td>
  </tr>
  <tr>
   <td>Dispositivo mobile</td>
   <td>Chrome (Android™ 6 o versioni precedenti)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Dispositivo mobile</td>
   <td>Chrome (Android™ 7 o versione successiva)</td>
   <td>Streaming/td bitrate adattivo HLS o DASH*&gt;
  </tr>
  <tr>
   <td>Dispositivo mobile</td>
   <td>Android™ (browser predefinito)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Dispositivo mobile</td>
   <td>Safari (iOS)</td>
   <td>Streaming bitrate adattivo HLS</td>
  </tr>
  <tr>
   <td>Dispositivo mobile</td>
   <td>Chrome (iOS)</td>
   <td>Streaming bitrate adattivo HLS</td>
  </tr>
 </tbody>
</table>

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Architettura della soluzione video Dynamic Media {#architecture-of-dynamic-media-video-solution}

L’immagine seguente mostra il flusso di lavoro complessivo per l’authoring dei video caricati e codificati tramite DMGateway (in modalità ibrida Dynamic Media) e resi disponibili al pubblico.

![chlimage_1-427](assets/chlimage_1-427.png)

## Architettura di pubblicazione ibrida per video {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Best practice per la codifica dei video {#best-practices-for-encoding-videos}

Il flusso di lavoro **Codifica video elementi multimediali dinamici** codifica video se hai attivato gli elementi multimediali dinamici e hai impostato Cloud Services per video. Questo flusso di lavoro acquisisce la cronologia del processo del flusso di lavoro e le informazioni di errore. Se hai attivato Dynamic Media e hai impostato Video Cloud Services, il flusso di lavoro **[!UICONTROL Codifica video elementi multimediali dinamici]** viene applicato automaticamente al momento di caricare un video. Se non utilizzi Dynamic Media, viene applicato il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.

Di seguito sono riportati alcuni suggerimenti sulle best practice per la codifica di file video sorgente.

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### File video Source {#source-video-files}

Quando codificate un file video, utilizzate un file video sorgente della massima qualità possibile. Evita di utilizzare file video codificati in precedenza perché sono già compressi e un’ulteriore codifica crea un video di qualità inferiore.

* Dynamic Media supporta principalmente video in formato breve con una lunghezza massima di 30 minuti e una risoluzione minima superiore a 25 × 25.
* È possibile caricare file video di origine primari fino a 15 GB ciascuno.

La tabella seguente descrive le dimensioni, le proporzioni e la velocità bit minima consigliate per i file video sorgente prima di codificarli:

| Dimensione | Proporzioni | Velocità bit minima |
|--- |--- |--- |
| 1024 × 768 | 4:3 | 4500 kbps per la maggior parte dei video. |
| 1280 × 720 | 16:9 | 3000 - 6000 kbps, in base alla quantità di movimento nel video. |
| 1920 × 1080 | 16:9 | 6000 - 8000 kbps, a seconda della quantità di movimento nel video. |

### Ottenere i metadati di un file {#obtaining-a-file-s-metadata}

Puoi ottenere i metadati di un file visualizzandone i metadati utilizzando uno strumento di modifica per video o un’applicazione progettata per ottenere i metadati. Di seguito sono riportate le istruzioni per l’utilizzo di MediaInfo, un’applicazione di terze parti, per ottenere i metadati di un file video:

1. Vai a [Download di MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Selezionare e scaricare il programma di installazione per la versione GUI e seguire le istruzioni di installazione.
1. Dopo l&#39;installazione, fare clic con il pulsante destro del mouse sul file video (solo Windows®) e selezionare MediaInfo, oppure aprire MediaInfo e trascinare il file video nell&#39;applicazione. Puoi visualizzare tutti i metadati associati al file video, compresi quelli relativi a larghezza, altezza e fps.

### Proporzioni {#aspect-ratio}

Quando scegliete o create un predefinito di codifica video per il file video sorgente principale, assicuratevi che il predefinito abbia le stesse proporzioni. Questo approccio garantisce la coerenza con il file video sorgente principale. Le proporzioni corrispondono al rapporto tra la larghezza e l&#39;altezza del video.

Per determinare le proporzioni di un file video, recuperate i metadati del file. Prendi nota della larghezza e dell’altezza del file (vedi Ottenere i metadati di un file qui sopra). Quindi utilizza questa formula per determinare le proporzioni:

larghezza/altezza = proporzioni

Nella tabella seguente viene descritto come i risultati della formula si traducono in scelte di proporzioni comuni:

| Risultato formula | Proporzioni |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16:9 |
| 0,56 | 9:16 |

Ad esempio, un video con larghezza 1440 × altezza 1080 ha proporzioni 1440/1080 o 1,33. In questo caso, scegliete un predefinito di codifica video con proporzioni 4:3 per codificare il file video.

### Bitrate {#bitrate}

Il bitrate è la quantità di dati codificati per formare un singolo secondo di riproduzione video. Il bitrate viene misurato in kilobit al secondo (Kbps).

>[!NOTE]
>
>Poiché tutti i codec utilizzano la compressione con perdita di dati, il bitrate è il fattore più importante nella qualità video. Con la compressione con perdita di dati, più si comprime un file video, più la qualità si riduce. Per questo motivo, tutte le altre caratteristiche sono uguali (risoluzione, frame rate e codec), minore è il bitrate, minore è la qualità del file compresso.

Quando si seleziona una codifica bitrate, è possibile scegliere tra due tipi:

* **[!UICONTROL Codifica bitrate costante]** (CBR): durante la codifica CBR, il bitrate o il numero di bit al secondo viene mantenuto invariato durante tutto il processo di codifica. La codifica CBR mantiene la velocità dati impostata sull’impostazione per l’intero video. Inoltre, la codifica CBR non ottimizza i file multimediali per la qualità, ma consente di risparmiare spazio di archiviazione.
Utilizzate CBR se il video contiene un livello di movimento simile per l&#39;intero video. CBR viene utilizzato più comunemente per lo streaming di contenuti video. Vedi anche [Utilizzare parametri di codifica video personalizzati](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codifica bitrate variabile]** (VBR) - La codifica VBR regola la velocità dati verso il basso e al limite superiore impostato, in base ai dati richiesti dal compressore. Questa funzionalità significa che durante un processo di codifica VBR il bitrate del file multimediale aumenta o diminuisce in modo dinamico a seconda delle esigenze di bitrate del file multimediale.
La codifica VBR richiede più tempo, ma produce i risultati più favorevoli; la qualità del file multimediale è superiore. VBR viene utilizzato in genere per la distribuzione progressiva http di contenuti video.

Quando si utilizza VBR rispetto a CRB?
Quando selezioni VBR rispetto a CBR, si consiglia quasi sempre di utilizzare VBR per i file multimediali. VBR fornisce file di qualità superiore a bitrate competitivi. Quando si utilizza VBR, assicurarsi di utilizzare con la codifica a due passate e impostare il bitrate massimo su 1,5 volte il bitrate video di destinazione.

Quando scegli un predefinito di codifica video, accertati di tenere conto della velocità di connessione dell&#39;utente target. Scegli un predefinito con una velocità dati pari all’80% di quella velocità. Ad esempio, se la velocità di connessione dell&#39;utente target è di 1000 Kbps, il predefinito migliore è quello con una velocità dati video di 800 Kbps.

Questa tabella descrive la velocità dati delle velocità di connessione tipiche.

| Velocità (Kbps) | Tipo di connessione |
|--- |--- |
| 256 | Connessione remota. |
| 800 | Connessione mobile tipica. Per questa connessione, esegui il targeting di una velocità di dati compresa tra 400 e un massimo di 800 per le esperienze 3G. |
| 2000 | Connessione desktop a banda larga tipica. Per questa connessione, eseguire il targeting di una velocità di dati nell&#39;intervallo 800-2000 Kbps, con la maggior parte delle destinazioni in media 1200-1500 Kbps. |
| 5000 | Tipica connessione a banda larga. La codifica in questo intervallo superiore non è consigliata perché la distribuzione di video a questa velocità non è disponibile per la maggior parte dei consumatori. |

### Risoluzione {#resolution}

**La risoluzione** descrive l&#39;altezza e la larghezza in pixel di un file video. La maggior parte dei video sorgente viene memorizzata ad alta risoluzione (ad esempio, 1920 × 1080). Ai fini dello streaming, il video sorgente viene compresso a una risoluzione inferiore (640 × 480 o inferiore).

La risoluzione e la velocità dei dati sono due fattori strettamente collegati che determinano la qualità video. Per mantenere la stessa qualità video, maggiore è il numero di pixel in un file video (maggiore è la risoluzione), maggiore è la velocità dati. Ad esempio, si consideri il numero di pixel per fotogramma in un file video con risoluzione 320 × 240 e 640 × 480:

| Risoluzione | Pixel per frame |
|--- |--- |
| 320 × 240 | 76.800 |
| 640 × 480 | 307.200 |

Il file 640 × 480 ha un numero di pixel per fotogramma quattro volte superiore. Per ottenere la stessa velocità dati per queste due risoluzioni di esempio, applicate una compressione quattro volte superiore al file 640 × 480, riducendo in tal modo la qualità del video. Di conseguenza, una velocità di dati video di 250 Kbps produce una visualizzazione di alta qualità con una risoluzione di 320 × 240, ma non con una risoluzione di 640 × 480.

In generale, maggiore è la velocità di dati utilizzata, migliore è la visualizzazione del video e maggiore è la risoluzione utilizzata, maggiore è la velocità di dati da mantenere la qualità di visualizzazione (rispetto a risoluzioni inferiori).

Poiché la risoluzione e la velocità dati sono collegate, durante la codifica del video sono disponibili due opzioni:

* Scegli una velocità dati e quindi codificala alla risoluzione più alta che sembra buona alla velocità dati scelta.
* Scegliete una risoluzione e quindi codificate alla velocità dati necessaria per ottenere video di alta qualità alla risoluzione desiderata.

Quando scegli (o crei) un predefinito di codifica video per il file video sorgente principale, utilizza questa tabella per individuare la risoluzione corretta:

| Risoluzione | Altezza (pixel) | Dimensioni dello schermo |
|--- |--- |--- |
| 240P | 240 | Schermo piccolo |
| 300P | 300 | Schermo piccolo in genere per dispositivi mobili |
| 360P | 360 | Schermo piccolo |
| 480P | 480 | Schermata Medium |
| 720P | 720 | Schermo grande |
| 1080P | 1080 | Schermo ad alta definizione di grandi dimensioni |

La risoluzione video in ingresso massima supportata è 16.384 × 16.384. La risoluzione massima di codifica video in uscita è 8.192 × 4.320 o 4.320 × 8.192.

### Fps (frame al secondo) {#fps-frames-per-second}

Negli Stati Uniti e in Giappone, la maggior parte del video è girata a 29,97 fps; in Europa, la maggior parte del video è girata a 25 fps. Un film viene girato a 24 fps.

Scegli un predefinito di codifica video che corrisponda alla velocità fps del file video sorgente principale. Ad esempio, se il video sorgente principale è a 25 fps, scegliete un predefinito di codifica con 25 fps. Per impostazione predefinita, tutta la codifica personalizzata utilizza il fps del file video sorgente principale. Per questo motivo, non è necessario specificare esplicitamente l&#39;impostazione fps quando si crea un predefinito di codifica video.

### Dimensioni di codifica video {#video-encoding-dimensions}

Per risultati ottimali, seleziona dimensioni di codifica tali che il video sorgente sia un multiplo di tutti i video codificati.

Per calcolare questo rapporto, si divide la larghezza dell&#39;origine per la larghezza codificata per ottenere il rapporto di larghezza. Quindi, per ottenere il rapporto di altezza, dividi l’altezza sorgente per altezza codificata.

Se il rapporto risultante è un numero intero, significa che il video è ridimensionato in modo ottimale. Se il rapporto risultante non è un numero intero, influisce sulla qualità video lasciando sul display gli artefatti di pixel rimanenti. Questo effetto è più evidente quando il video contiene del testo.

Ad esempio, supponiamo che il video sorgente sia 1920 × 1080. Nella tabella seguente, i tre video codificati forniscono le impostazioni di codifica ottimali da utilizzare.

| Tipo di video | Larghezza × altezza | Rapporto larghezza | Rapporto altezza |
|--- |--- |--- |--- |
| Origine | 1920 × 1080 | 1 | 1 |
| Codificato | 960 × 540 | 2 | 2 |
| Codificato | 640 × 360 | 3 | 3 |
| Codificato | 480 × 270 | 4 | 4 |

### Formato file video codificato {#encoded-video-file-format}

Dynamic Media consiglia di utilizzare i predefiniti di codifica video MP4 H.264. Poiché i file MP4 utilizzano il codec video H.264, questo offre video di alta qualità ma in dimensioni di file compressi.

## Visualizzare rapporti video {#viewing-video-reports}

>[!NOTE]
>
>I rapporti video sono disponibili solo quando si esegue Dynamic Media in modalità ibrida.

I report video visualizzano diverse metriche aggregate in un determinato periodo di tempo per aiutarti a monitorare che *video pubblicati* singoli e aggregati stiano ottenendo le prestazioni previste. I seguenti dati sulle metriche principali sono aggregati per tutti i video pubblicati sull’intero sito web:

* Inizio video
* Tasso di completamento
* Tempo medio sul video
* Tempo totale su video
* Video per visita

È inoltre presente una tabella di tutti i video *pubblicati* che ti consente di tenere traccia dei video visualizzati più in alto sul tuo sito Web in base al totale degli avvii dei video.

Quando selezioni un nome video nell’elenco, viene visualizzato il rapporto di conservazione del pubblico (a discesa) del video sotto forma di un grafico a linee. Il grafico mostra il numero di visualizzazioni per un dato momento della riproduzione video. Quando si riproduce il video, la barra verticale viene sincronizzata con l&#39;indicatore di tempo nel lettore. Le cadute nei dati del grafico a linee indicano dove il pubblico abbandona il disinteresse.

Se il video è stato codificato al di fuori di Adobe Experience Manager Dynamic Media, il grafico di mantenimento del pubblico (a discesa) e i dati della percentuale di riproduzione nella tabella non sono disponibili.

>[!NOTE]
>
>I dati di tracciamento e reporting si basano esclusivamente sull’utilizzo del lettore video di Dynamic Media e del relativo predefinito per lettore video. Di conseguenza, non è possibile tenere traccia dei video riprodotti da altri lettori video e creare rapporti su di essi.

Per impostazione predefinita, la prima volta che si immettono i rapporti video, il rapporto visualizza i dati video a partire dal primo del mese corrente e termina con la data del mese corrente. Tuttavia, puoi sovrascrivere l’intervallo di date predefinito specificando un intervallo di date personalizzato. La volta successiva in Rapporti video viene utilizzato l’intervallo di date specificato.

Affinché i rapporti video funzionino correttamente, viene creato automaticamente un ID suite di rapporti quando viene configurato Dynamic Media Cloud Services. Allo stesso tempo, l’ID suite di rapporti viene inviato al server di pubblicazione, in modo che sia disponibile per la funzione Copia URL quando visualizzi l’anteprima delle risorse. Tuttavia, questa funzionalità richiede che il server di pubblicazione sia già configurato. Se il server di pubblicazione non è configurato, puoi comunque eseguire la pubblicazione per visualizzare il rapporto video. Tuttavia, devi tornare alla configurazione cloud di Dynamic Media e selezionare **[!UICONTROL OK]**.

**Per visualizzare i report video:**

1. Nell’angolo in alto a sinistra di Experience Manager, seleziona il logo Experience Manager. Nella barra a sinistra, fai clic su ![Icona Martello](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti video]**.
1. Nella pagina Rapporti video eseguire una delle operazioni seguenti:

   * Nell&#39;angolo superiore destro selezionare l&#39;icona **[!UICONTROL Aggiorna report video]**.
È possibile utilizzare Aggiorna solo se la data di fine del rapporto è il giorno corrente. Questa funzione ti consente di visualizzare il tracciamento video che si è verificato dall’ultima volta che hai eseguito il rapporto.

   * Nell&#39;angolo superiore destro, seleziona l&#39;icona **[!UICONTROL Selezione data]**.
Specificare l&#39;intervallo di date iniziale e finale per il quale si desidera visualizzare i dati video, quindi selezionare **[!UICONTROL Esegui report]**.

   La casella di gruppo Metriche principali identifica varie misurazioni aggregate per tutti i video *published* nel sito.

1. Nella tabella in cui sono elencati i video più pubblicati, seleziona un nome per riprodurre il video e consulta il rapporto sulla fidelizzazione del pubblico (drop-off) del video.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## Informazioni sul supporto di più didascalie e tracce audio per video in Dynamic Media{#about-msma}

Grazie alla funzionalità di didascalia multipla e traccia audio in Dynamic Media, è possibile aggiungere facilmente più tracce audio. È inoltre possibile aggiungere più file di didascalia utilizzando i propri file `.vtt` (Video Text Track) o i file di didascalia generati da IA. I sottotitoli generati dall’intelligenza artificiale in Dynamic Media sono progettati per migliorare l’accessibilità e il coinvolgimento video generando automaticamente sottotitoli accurati e sincronizzati. Questa tecnologia utilizza algoritmi di intelligenza artificiale avanzati per trascrivere i contenuti parlati in testo, che viene quindi visualizzato come didascalie nel video. Di seguito sono riportate alcune delle caratteristiche principali di questa tecnologia:

* **Trascrizione automatica:** Il sistema di intelligenza artificiale trascrive le parole pronunciate in testo in tempo reale, garantendo che le didascalie vengano generate rapidamente e con precisione.
* **Supporto multilingue:** i sottotitoli possono essere consegnati automaticamente in più di 60 lingue, facilitando il raggiungimento di un pubblico globale.
* **Accessibilità migliorata:** fornendo didascalie, i video diventano più accessibili agli utenti non udenti o con problemi di udito o alle persone che preferiscono guardare video con l&#39;audio disattivato.
* **Coinvolgimento migliorato:** I sottotitoli possono contribuire a mantenere l&#39;attenzione del visualizzatore e a migliorare la comprensione, soprattutto in ambienti rumorosi o quando la lingua nativa del visualizzatore è diversa dalla lingua del video.

Queste funzioni rendono i sottotitoli basati sull’intelligenza artificiale uno strumento utile per i creatori di contenuti che desiderano migliorare l’accessibilità e il coinvolgimento dei contenuti video.

![Scheda Sottotitoli e tracce audio in Dynamic Media insieme a una tabella che mostra i file di didascalia .VTT caricati e i file di traccia audio .MP3 caricati per un video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)

Alcuni dei casi d’uso da considerare per aggiungere più didascalie e tracce audio al video principale sono i seguenti:

| Tipo | Caso d’uso |
|--- |--- |
| **Sottotitoli** | Supporto di più lingue |
|  | Testo descrittivo per accessibilità |
| **Brani audio** | Supporto di più lingue |
|  | Brani di commento |
|  | Audio descrittivo |

Tutti i formati video [supportati in Dynamic Media](/help/assets/file-format-support.md) e tutti i visualizzatori video Dynamic Media, ad eccezione del visualizzatore *Video_360* di Dynamic Media, sono supportati per l&#39;utilizzo con più didascalie e tracce audio.

### Aggiungere più didascalie e tracce audio al video {#add-msma}

Prima di aggiungere più didascalie e tracce audio al video, assicurati di avere già le seguenti informazioni:

* Dynamic Media è configurato in un ambiente AEM.
* Un profilo video [Dynamic Media viene applicato alla cartella in cui vengono acquisiti i video](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

I sottotitoli aggiunti sono supportati nei formati WebVTT e Adobe VTT. Inoltre, i file di traccia audio aggiunti sono supportati con il formato MP3.

>[!IMPORTANT]
>
>Per i video caricati *prima* che abilitano il supporto per più didascalie/tracce audio o le didascalie generate da AI sul tuo account Dynamic Media, [devi rielaborarle](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). Questo passaggio di rielaborazione garantisce che questi video possano utilizzare le funzioni multiple caption/audio track e caption generate dall’intelligenza artificiale. Dopo la rielaborazione, gli URL del video continuano a funzionare e a essere riprodotti come al solito.

**Per aggiungere più didascalie e tracce audio al video:**

1. [Carica il video principale in una cartella](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) a cui è già stato assegnato un profilo video.
1. Passa alla risorsa video caricata a cui desideri aggiungere più didascalie e tracce audio.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
   ![Risorsa video selezionata con segno di spunta sull&#39;immagine miniatura video e Proprietà visualizzazione evidenziate sulla barra degli strumenti.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Risorsa video selezionata nella vista a schede.*
1. Nella pagina Proprietà del video, seleziona la scheda **[!UICONTROL Sottotitoli e tracce audio]**.

   >[!TIP]
   >Se la scheda **[!UICONTROL Brani audio e didascalie]** non è visualizzata, significa che è presente uno dei due elementi seguenti:
   >
   >* Alla cartella in cui si trova il video selezionato non è assegnato alcun profilo video. In tal caso, vedere [Applicare un profilo video alla cartella](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* In alternativa, Dynamic Media deve rielaborare il video. In questo caso, consulta [Rielaborare le risorse Dynamic Media in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
   >
   >Dopo aver completato una delle attività di cui sopra, torna a questi passaggi.

   ![Scheda Brani audio e didascalie nella pagina Proprietà.](/help/assets/dynamic-media/assets/msma-audiotracks.png)
   *Scheda Brani didascalia e audio nella pagina Proprietà del video.*

1. Per aggiungere una o più tracce audio a un video, effettuate le seguenti operazioni:
   1. Seleziona **[!UICONTROL Carica tracce audio]**.
   1. Passa a uno o più file .mp3 e selezionali, quindi aprili.
   1. Affinché le tracce audio siano visibili nell&#39;elenco a comparsa **[!UICONTROL Seleziona audio o didascalia]** sul lettore multimediale, è necessario aggiungere i dettagli richiesti su ciascun file di traccia audio. In questo modo, tutte le tracce audio sono elencate e accessibili correttamente. Fai clic sull&#39;icona ![Disegna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a destra del nome di un file di traccia audio. Nella finestra di dialogo **Modifica traccia audio** immettere i dettagli richiesti seguenti:

      | Metadati traccia audio | Descrizione |
      |--- |--- |
      | Nome file | Il nome file predefinito è derivato dal nome file originale. Il nome del file può essere modificato solo durante il caricamento e non può essere modificato in un secondo momento. I requisiti di carattere per il nome file sono gli stessi di AEM Assets.<br>Impossibile utilizzare lo stesso nome di file per altri file di traccia audio o di didascalia. |
      | Lingua | Selezionate la lingua corretta della traccia audio. |
      | Tipo | Selezionate il tipo di traccia audio in uso.<br>**Originale** - La traccia audio originariamente allegata al video e rappresentata come `[Original]` nell&#39;etichetta con la lingua `English` selezionata per impostazione predefinita. Anche se è possibile modificare **[!UICONTROL Label]** e **[!UICONTROL Language]** nella finestra di dialogo **[!UICONTROL Modifica traccia audio]**, se il video principale viene rielaborato, per impostazione predefinita vengono utilizzati i valori originali.<br>**Standard** - Traccia audio aggiuntiva per una lingua diversa dall&#39;originale.<br>**Descrizione audio**: traccia audio che include anche una narrazione descrittiva delle azioni non verbali e dei gesti nel video, rendendo il contenuto più accessibile agli utenti ipovedenti. |
      | Etichetta | Testo visualizzato come nome della traccia audio nell&#39;elenco a comparsa **[!UICONTROL Seleziona audio o didascalia]** nel lettore multimediale. L’etichetta è ciò che il cliente vede e che corrisponde a una traccia audio. Ad esempio, `English [Original]`. L&#39;etichetta audio associata a un video è impostata su `[Original]` per impostazione predefinita. |

      Se necessario, potete modificare i metadati della traccia audio in un secondo momento. Quando il video viene pubblicato, questi dettagli si riflettono sugli URL pubblici nei video pubblicati.

   1. Nell&#39;angolo superiore destro della pagina, nel menu a discesa **[!UICONTROL Salva e chiudi]**, fai clic su **[!UICONTROL Salva]**.
   1. Effettua una delle seguenti operazioni:
      * Ripetete questa procedura per ogni file di traccia audio caricato.
      * Procedi al passaggio successivo per aggiungere sottotitoli a un video.

1. Per aggiungere uno o più file di didascalia a un video, scegli quale dei seguenti casi d’uso si adatta meglio allo scenario:

   |  | Caso d’uso | Opzione Crea didascalia da utilizzare |
   | --- | --- | --- |
   | **Opzione 1** | Ho i miei file di didascalia preesistenti nelle lingue che voglio usare.<br>Vedere **Opzione 1** di seguito. | **[!UICONTROL Carica file]** |
   | **Opzione 2** | Desidero che AI generi i miei file di didascalia in più lingue.<br>Vedere **Opzione 2** di seguito. | **[!UICONTROL Converti tracce audio]** |
   | **Opzione 3** | È necessario correggere il testo di un file di didascalia (`.vtt`), ricaricarlo per sostituire il file `.vtt` precedente, quindi far tradurre il file corretto da AI.<br>Vedere **Opzione 3** di seguito. | **[!UICONTROL Traduci didascalia]** |

   ![Opzioni per la creazione dei sottotitoli.](/help/assets/dynamic-media/assets/msma-createcaption.png)
   *Il menu a discesa Crea didascalia offre tre opzioni: Carica file, Converti tracce audio e Traduci didascalia.*

   +++**Opzione 1:** *Ho i miei file di didascalia preesistenti nelle lingue che voglio utilizzare* (**[!UICONTROL Carica file]**)

   1. Nella parte superiore destra della pagina, fai clic su **[!UICONTROL Crea didascalia]** > **[!UICONTROL Carica file]**.
   1. Passare a uno o più file `.vtt` preesistenti e selezionarli.
   1. Affinché i sottotitoli siano visibili sul lettore multimediale, *devi* aggiungere i dettagli richiesti su *ogni* file di sottotitoli che carichi. Fai clic sull&#39;icona ![Disegna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a destra del nome di un file di didascalia. Nella finestra di dialogo **Modifica didascalia** immettere i dettagli richiesti seguenti sul file:

      | Metadati didascalia | Descrizione |
      |--- |--- |
      | Nome file | Il nome file predefinito è derivato dal nome file originale. Il nome del file può essere modificato solo durante il caricamento e non può essere modificato in un secondo momento. I requisiti di carattere per il nome file sono gli stessi di AEM Assets.<br>Impossibile utilizzare lo stesso nome di file per ulteriori file di didascalia e tracce audio. |
      | Lingua | Selezionare la lingua della didascalia. Dopo l&#39;elaborazione di un file di didascalia, questo campo della lingua diventa non modificabile (inattivo) |
      | Tipo | Selezionare il tipo di didascalia in uso.<br>**Sottotitolo**: il testo della didascalia visualizzato con il video che traduce o trascrive la finestra di dialogo.<br>**Didascalia** - Il testo della didascalia include i rumori di fondo, la differenziazione degli altoparlanti e altri dettagli rilevanti, insieme alla traduzione o alla trascrizione del dialogo, migliorando l&#39;accessibilità per gli individui non udenti o ipoudenti. |
      | Etichetta | Testo visualizzato per il nome della didascalia nell&#39;elenco a comparsa **[!UICONTROL Seleziona audio o didascalia]** nel lettore multimediale. L’etichetta è ciò che vede il cliente e corrisponde a un sottotitolo o a una traccia di didascalia. Ad esempio, `English (CC)`. |

      Se necessario, puoi modificare i metadati dei sottotitoli in un secondo momento. Quando il video viene pubblicato, questi dettagli si riflettono sugli URL pubblici nei video pubblicati.

   1. Nell&#39;angolo superiore destro della pagina, nel menu a discesa **[!UICONTROL Salva e chiudi]**, fai clic su **[!UICONTROL Salva]**. I file vengono caricati e inizia l&#39;elaborazione dei metadati, come mostrato nella colonna **Stato** dell&#39;interfaccia.

      >[!NOTE]
      >
      >In base alle impostazioni di caching dell’istanza, l’elaborazione dei metadati può richiedere diversi minuti prima che venga visualizzata nell’anteprima e negli URL pubblicati.

   1. Se hai selezionato **[!UICONTROL Salva e chiudi]** nel passaggio precedente, invece di selezionare **[!UICONTROL Salva]**, puoi comunque visualizzare lo stato di elaborazione dei file caricati. Consulta [Visualizzare lo stato del ciclo di vita dei file di didascalia e traccia audio caricati](#lifecycle-status-video).
   1. Continuare con il passaggio 8.

   +++

   +++**Opzione 2:** *Desidero che AI generi i miei file di didascalia in più lingue* (**[!UICONTROL Opzione Converti tracce audio]**)

   1. Fai clic su **[!UICONTROL Crea didascalia]** > **[!UICONTROL Converti tracce audio]** nell&#39;angolo superiore destro della pagina.

      ![Finestra di dialogo Converti tracce audio.](/help/assets/dynamic-media/assets/msma-convertaudiotracks.png)
      *La finestra di dialogo Converti tracce audio utilizza l&#39;intelligenza artificiale per generare file di didascalia in più lingue.*

   1. Nella finestra di dialogo **Converti tracce audio**, impostare le opzioni seguenti:

      | Opzione | Descrizione |
      |--- |--- |
      | Traccia audio da convertire | Fai clic sull&#39;icona ![freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi scegli il file di traccia audio caricato dal quale desideri generare i sottotitoli con IA. |
      | Lingue di output | Fai clic sull&#39;icona ![freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi seleziona una o più lingue in cui vuoi visualizzare il file di didascalia.<br>Per rimuovere una lingua selezionata, fare clic sull&#39;icona ![Chiudi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg).<br>Durante la riproduzione del video, l&#39;elenco delle lingue viene visualizzato nel lettore multimediale nell&#39;ordine in cui sono state selezionate qui. |

   1. Fai clic su **[!UICONTROL Fine]**.
   1. Nell&#39;angolo superiore destro della pagina, nel menu a discesa **[!UICONTROL Salva e chiudi]**, fai clic su **[!UICONTROL Salva]**.
   1. Fai di nuovo clic sulla scheda **[!UICONTROL Didascalie e tracce audio]**. Vengono creati uno o più file di didascalia e inizia l&#39;elaborazione, come mostrato nella colonna **Stato** dell&#39;interfaccia. Vedi anche [Visualizzare lo stato del ciclo di vita dei file di didascalia e di traccia audio caricati](#lifecycle-status-video).

      >[!NOTE]
      >
      >In base alle impostazioni di caching dell’istanza, l’elaborazione dei metadati può richiedere diversi minuti prima che venga visualizzata nell’anteprima e negli URL pubblicati.

   1. (Facoltativo) Fai clic su ![Icona Disegno](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a destra del nome di un file di didascalia. Nella finestra di dialogo **Modifica didascalia** è possibile modificare i dettagli seguenti sul file:

      | Metadati didascalia | Descrizione |
      | --- | --- |
      | Tipo | Selezionare il tipo di didascalia in uso.<br>**Sottotitolo**: il testo della didascalia visualizzato con il video che traduce o trascrive la finestra di dialogo.<br>**Didascalia** - Il testo della didascalia include i rumori di sottofondo e la differenziazione degli altoparlanti. Comprende anche altre informazioni pertinenti, insieme alla traduzione o trascrizione della finestra di dialogo. Questo approccio rende i contenuti più accessibili per gli individui non udenti o ipoudenti. |
      | Etichetta | Testo visualizzato per il nome della didascalia nell&#39;elenco a comparsa **[!UICONTROL Seleziona audio o didascalia]** nel lettore multimediale. L’etichetta è ciò che vede il cliente e corrisponde a un sottotitolo o a una traccia di didascalia. Ad esempio, `English (CC)`. |

      Se necessario, puoi modificare alcuni metadati di didascalia in un secondo momento. Quando il video viene pubblicato, i dettagli dei metadati si riflettono sugli URL pubblici nei video pubblicati.
   1. Continuare con il passaggio 8.

   +++

   +++**Opzione 3:** *È necessario correggere il testo di un file di didascalia (`.vtt`), ricaricarlo per sostituire il file `.vtt` precedente, quindi fare in modo che AI traduca il file corretto* (**[!UICONTROL Traduci didascalie]**)

   1. Fai clic su **[!UICONTROL Crea didascalia]** > **[!UICONTROL Traduci didascalie]**. Questa opzione è disponibile se uno o più file di didascalia sono già stati aggiunti ed elaborati.

      ![Finestra di dialogo Traduci didascalie.](/help/assets/dynamic-media/assets/msma-translate-captions.png)
      *La finestra di dialogo Traduci didascalie consente di utilizzare un file di didascalia esistente per generare nuovi file di didascalia in più lingue.*

   1. Nella finestra di dialogo **Traduci didascalie**, imposta le opzioni seguenti:

      | Opzione | Descrizione |
      |--- |--- |
      | Didascalia da tradurre | Fai clic sull&#39;icona ![freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi scegli un file di didascalia da cui desideri generare le didascalie utilizzando l&#39;intelligenza artificiale. |
      | Lingue di output | Fai clic sull&#39;icona ![freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi seleziona una o più lingue in cui vuoi visualizzare il file di didascalia.<br>Per rimuovere una lingua selezionata, fare clic sull&#39;icona ![Chiudi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg).<br>Durante la riproduzione del video, l&#39;elenco delle lingue viene visualizzato nel lettore multimediale nell&#39;ordine in cui sono state selezionate qui. |

   1. Fai clic su **[!UICONTROL Fine]**.
   1. Nell&#39;angolo superiore destro della pagina, nel menu a discesa **[!UICONTROL Salva e chiudi]**, fai clic su **[!UICONTROL Salva]**.
   1. Fai di nuovo clic sulla scheda **[!UICONTROL Didascalie e tracce audio]**. Vengono creati uno o più file di didascalia e inizia l&#39;elaborazione, come mostrato nella colonna **Stato** dell&#39;interfaccia. Vedi anche [Visualizzare lo stato del ciclo di vita dei file di didascalia e di traccia audio caricati](#lifecycle-status-video).

      >[!NOTE]
      >
      >In base alle impostazioni di caching dell’istanza, l’elaborazione dei metadati può richiedere diversi minuti prima che venga visualizzata nell’anteprima e negli URL pubblicati.

   1. (Facoltativo) Fai clic su ![Icona Disegno](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a destra del nome di un file di didascalia. Nella finestra di dialogo **Modifica didascalia** è possibile modificare i dettagli seguenti sul file:

      | Metadati didascalia | Descrizione |
      | --- | --- |
      | Tipo | Selezionare il tipo di didascalia in uso.<br>**Sottotitolo**: il testo della didascalia visualizzato con il video che traduce o trascrive la finestra di dialogo.<br>**Didascalia** - Il testo della didascalia include anche i rumori di sottofondo e la differenziazione degli altoparlanti. Comprende anche altre informazioni pertinenti, insieme alla traduzione o trascrizione della finestra di dialogo. Questo approccio rende i contenuti più accessibili per gli individui non udenti o ipoudenti. |
      | Etichetta | Testo visualizzato per il nome della didascalia nell&#39;elenco a comparsa **[!UICONTROL Seleziona audio o didascalia]** nel lettore multimediale. L’etichetta è ciò che vede il cliente e corrisponde a un sottotitolo o a una traccia di didascalia. Ad esempio, `English (CC)`. |

      Se necessario, puoi modificare alcuni metadati di didascalia in un secondo momento. Quando il video viene pubblicato, i dettagli dei metadati si riflettono sugli URL pubblici nei video pubblicati.

   1. Continuare con il passaggio 8.

   +++

1. (Facoltativo) Visualizza l&#39;anteprima del video prima della pubblicazione per assicurarti che i sottotitoli e l&#39;audio funzionino come previsto. Vedi [Anteprima di un video con più sottotitoli e tracce audio](#preview-video-audio-subtitle).
1. Pubblica il video. Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

#### Informazioni sull&#39;aggiunta di file di didascalia e traccia audio a un video già pubblicato

Dopo aver caricato ulteriori file di didascalia o di traccia audio in un video pubblicato, questi file hanno lo stato `Processed` dopo essere stati preparati. È quindi possibile visualizzare in anteprima il video in Dynamic Media per visualizzare o ascoltare i nuovi file.

Dopo l&#39;anteprima, tuttavia, è necessario *pubblicare* di nuovo il video per pubblicare anche i file di didascalia o di traccia audio appena aggiunti. Dopo la pubblicazione, i sottotitoli o l’audio diventano disponibili con l’URL pubblico di Dynamic Media.

>[!NOTE]
>
>In base alle impostazioni di caching dell’istanza, gli aggiornamenti dei metadati possono richiedere alcuni minuti prima che vengano visualizzati nell’anteprima e negli URL pubblicati.

Se hai configurato Dynamic Media per la pubblicazione immediata, il caricamento di file di didascalia o audio aggiuntivi attiva immediatamente la pubblicazione del video in seguito al caricamento di file di didascalia o audio.

>[!CAUTION]
>
>Quando si caricano file di didascalia o file audio in un video pubblicato o non pubblicato, i file vengono eliminati se si [*rielabora*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) il video. Solo l&#39;audio originale del video rimane intatto. In questi casi, è necessario caricare nuovamente i file di didascalia e di traccia audio nel video.

#### Aggiungere più sottotitoli a un video che ha un URL esistente con modificatore sottotitoli

Dynamic Media supporta l’aggiunta di una didascalia singola con video tramite un modificatore URL. Vedi [Aggiungere didascalie al video](#adding-captions-to-video).

Le modifiche apportate a più sottotitoli hanno la precedenza su una didascalia aggiunta tramite un modificatore URL per i video pubblicati.

**Per aggiungere più sottotitoli a un video che ha un URL esistente con modificatore di sottotitoli:**

1. Carica il file di didascalia già aggiunto come modificatore al video, in modo da poter gestire il file esplicitamente.
1. Carica eventuali file di didascalia aggiuntivi, se necessario.
1. Pubblica il video come di consueto.
L’URL esistente con il modificatore didascalia ora può caricare più didascalie.


### Modifica sottotitoli video

Puoi modificare i sottotitoli delle risorse video direttamente nell’interfaccia utente di Dynamic Media. Questa funzione consente di modificare i file dei sottotitoli `.vtt`, visualizzare in anteprima gli aggiornamenti e pubblicare le modifiche senza problemi.

* Quando si pubblicano i sottotitoli, tutte le modifiche vengono sincronizzate e pubblicate automaticamente.
* Se si verificano errori di modifica ed è necessario rigenerare i sottotitoli:
   * Elimina il file dei sottotitoli esistente.
   * Utilizzare l&#39;opzione 2 (Converti tracce audio) nel passaggio 7 di [Aggiungere più didascalie e tracce audio al video](#add-msma).
   * Fai clic su **Salva** o **Salva e chiudi** per generare un nuovo file di sottotitoli.
* L’anteprima dei sottotitoli all’interno dell’editor è solo a scopo di modifica e non riflette l’aspetto dei sottotitoli nell’interfaccia utente di riproduzione video finale.

**Per modificare i sottotitoli video:**

1. Passa alla risorsa video di cui desideri modificare i sottotitoli.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina Proprietà, seleziona la scheda **[!UICONTROL Didascalie e tracce audio]**.
1. Sotto l&#39;intestazione **Sottotitoli**, fare clic su ![icona](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ProjectEdit_18_N.svg) a destra del nome di un file di sottotitoli.

   ![Icona Modifica sottotitoli sotto l&#39;intestazione Sottotitoli](/help/assets/dynamic-media/assets/msma-editcaption.png)

1. Nella finestra di dialogo **Modifica sottotitolo**, modificare il testo nel file WebVTT in base alle esigenze.

   ![Finestra di dialogo Modifica sottotitolo](/help/assets/dynamic-media/assets/msma-editsubtitle-dialogbox.png)

1. Nell’angolo inferiore a destra della finestra di dialogo, fai clic su **Salva**.


### Visualizzare lo stato del ciclo di vita dei file di didascalia e traccia audio caricati {#lifecycle-status-video}

Puoi osservare lo stato del ciclo di vita di qualsiasi file di didascalia o traccia audio caricato nel video principale. Puoi farlo dalla scheda **Brani audio e didascalie** di **Proprietà**.

**Per visualizzare lo stato del ciclo di vita di un video:**

1. Passa alla risorsa video di cui desideri visualizzare lo stato del ciclo di vita.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina **Proprietà**, seleziona la scheda **[!UICONTROL Didascalie e tracce audio]**.
1. Nella colonna **[!UICONTROL Stato]**, annota lo stato di ogni didascalia o file audio.

| Stato dei sottotitoli e delle tracce audio | Descrizione |
| --- | --- |
| Elaborazione | Quando viene aggiunta e salvata una nuova didascalia o un nuovo file di traccia audio, il file entra in uno stato di &quot;Elaborazione&quot;. Dynamic Media elabora il file allegando il manifesto di streaming al video principale. |
| Elaborato | Al termine dell&#39;elaborazione, il file di didascalia o di traccia audio, o la traccia audio originale associata al video principale, viene visualizzato in stato &quot;Elaborato&quot;. Puoi visualizzare in anteprima i file di didascalia e di traccia audio che appaiono come &quot;Elaborati&quot; *prima* che il video venga pubblicato live. |
| Pubblicato | Uno stato &quot;Pubblicato&quot; rappresenta uno stato simile a &quot;Pubblicato&quot; per un video principale. Le Assets vengono pubblicate quando il video principale viene pubblicato e sono disponibili sull’URL pubblico di Dynamic Media. |
| Non riuscito | Lo stato &quot;Non riuscito&quot; indica che l&#39;elaborazione di un file di didascalia o di traccia audio non è stata completata. Elimina la didascalia o il file di traccia audio e caricalo di nuovo. |
| La pagina di cui è stata annullata la pubblicazione   | Quando si annulla esplicitamente la pubblicazione di un video principale pubblicato, vengono annullati anche i file di didascalia o di traccia audio aggiunti al video. |


### Impostare l&#39;audio predefinito per un video con più tracce audio

Per impostazione predefinita, l&#39;audio originale di un video è impostato come audio predefinito da riprodurre.

Tuttavia, tutti i file di traccia audio caricati possono essere impostati come audio predefinito da riprodurre dopo il caricamento di un video nel visualizzatore. Nell&#39;interfaccia utente Proprietà, nella scheda **Sottotitoli e tracce audio**, l&#39;etichetta `Default` viene applicata a destra del file di traccia audio per la riproduzione video.

>[!NOTE]
>
>La riproduzione dell’audio predefinito può anche dipendere da quanto impostato nei seguenti browser:
>
>* Chrome: viene riprodotto l’audio predefinito impostato nel video.
>* Safari: se la lingua predefinita è impostata in Safari, l’audio viene riprodotto con la lingua predefinita impostata, se disponibile con il manifesto del video. In caso contrario, viene riprodotto l&#39;audio predefinito impostato come parte delle proprietà di un video.

**Per impostare l&#39;audio predefinito per un video con più tracce audio:**

1. Passa alla risorsa video di cui desideri impostare la traccia audio predefinita.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina Proprietà, seleziona la scheda **[!UICONTROL Didascalie e tracce audio]**.
1. Sotto l&#39;intestazione **Tracce audio**, selezionare il file di traccia audio che si desidera impostare come predefinito del video.
1. Fai clic sull&#39;![icona audio](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Audio_18_N.svg) **[!UICONTROL Imposta come predefinito]**.
1. Nella finestra di dialogo **Imposta come predefinito** fare clic su **[!UICONTROL Sostituisci]**.

   ![L&#39;intestazione Tracce audio con il nome del file di traccia audio selezionato ed evidenziato il pulsante Imposta come predefinito.](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*Impostazione della traccia audio predefinita per un video.*

1. Nell&#39;angolo superiore destro fare clic su **[!UICONTROL Salva e chiudi]**.
1. Pubblica il video. Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

### Visualizzare in anteprima un video con più sottotitoli e tracce audio {#preview-video-audio-subtitle}

Una volta caricati in un video e elaborati i file di didascalia e di traccia audio, è possibile utilizzare il visualizzatore video Dynamic Media per visualizzare in anteprima tutte le diverse tracce. In questo modo è possibile vedere l&#39;aspetto e l&#39;audio del video per i clienti e assicurarsi che si comporti come previsto.

Se il video è soddisfacente, puoi [pubblicarlo](publishing-dynamicmedia-assets.md) utilizzando uno dei seguenti metodi.

Vedi [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md).
Consulta [Collegare gli URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Consulta [Aggiungere Dynamic Media Assets alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

>[!NOTE]
>
>La scheda Anteprima Experience Manager predefinita non mostra più didascalie e tracce audio. Il motivo è che questi brani sono associati a Dynamic Media e possono essere visualizzati solo utilizzando l’anteprima del visualizzatore Dynamic Media.

**Per visualizzare in anteprima un video con più didascalie e tracce audio:**

1. In **[!UICONTROL Assets]**, passa a un video esistente a cui sono stati aggiunti più sottotitoli e tracce audio.
1. Fai clic sulla risorsa video per aprirla in modalità anteprima.
1. Nella pagina di anteprima, nell&#39;angolo superiore sinistro della pagina, fai clic sull&#39;icona ![Barra a sinistra](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi seleziona **[!UICONTROL Visualizzatori]**.

   ![Elenco a discesa con l&#39;opzione Visualizzatori.](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. Nell&#39;angolo superiore sinistro della pagina fare clic sull&#39;icona ![Barra a sinistra](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) Visualizzatori ![Icona freccia giù](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), quindi selezionare un visualizzatore da utilizzare per l&#39;anteprima video.

1. Nell’angolo in basso a destra della pagina, fai clic sull’icona del fumetto, quindi seleziona l’audio o il sottotitolo/didascalia che desideri ascoltare o visualizzare, oppure entrambi.

   ![Elenco a comparsa Audio e didascalie nel visualizzatore video.](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*Simulazione di un utente che seleziona l&#39;audio e la didascalia per la riproduzione del video.*

1. Per iniziare la riproduzione, fare clic sull&#39;icona ![PLay](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg).
Se lo desideri, fai clic sull&#39;icona ![Ingrandisci](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Maximize_22_N.svg) per ingrandire la finestra di visualizzazione.
Osserva i pulsanti **[!UICONTROL URL]** e **[!UICONTROL Incorpora]** nell&#39;angolo inferiore sinistro della pagina. Utilizza questi pulsanti per [collegare l&#39;URL del video all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o per [incorporare il video rispettivamente in una pagina Web](/help/assets/dynamic-media/embed-code.md).
1. Fai clic su **[!UICONTROL Chiudi]** nell&#39;angolo superiore destro della pagina di anteprima.

### Eliminare i file di didascalia o di traccia audio da un video

Potete eliminare file di didascalia o di traccia audio da un video. L’eliminazione dei file di didascalia o di traccia audio pubblicati si riflette automaticamente nell’URL pubblicato del video.

Non è possibile eliminare la traccia audio originale estratta da un video principale.

**Per eliminare i file di didascalia o di traccia audio da un video:**

1. Passa alla risorsa video di cui desideri impostare la traccia audio predefinita.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina Proprietà, seleziona la scheda **[!UICONTROL Didascalie e tracce audio]**.
1. Effettua una delle operazioni seguenti:

   * Sottotitoli: sotto l&#39;intestazione **Sottotitoli**, seleziona uno o più file di sottotitoli da eliminare dal video, quindi fai clic sull&#39;icona ![Elimina](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Elimina]**.
   * Tracce audio - Sotto l&#39;intestazione **Tracce audio**, seleziona uno o più file di tracce audio da eliminare dal video, quindi fai clic sull&#39;icona ![Elimina](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Elimina]**.

1. Nella finestra di dialogo Elimina fare clic su **[!UICONTROL OK]**.
1. Pubblica il video.

### Scarica i file di didascalia o di traccia audio caricati in un video

Puoi scaricare i file di didascalia o di traccia audio caricati per un video. È possibile scaricare tutti i file selezionati come `.zip` o creare una cartella di download separata per ciascun file.

Non è possibile scaricare la traccia audio originale estratta da un file video principale.

**Caso d&#39;uso:** Il download di un file di didascalia potrebbe essere necessario se si verifica un errore in un file `.vtt`. È sufficiente scaricare il file `.vtt` errato, aprirlo in un editor di testo normale e apportare le correzioni necessarie. Dopo aver salvato il file `.vtt`, caricalo di nuovo. Quindi, utilizza l&#39;opzione **[!UICONTROL Traduci didascalie]** per tradurre nuovamente il file `.vtt` corretto.

**Per scaricare i file di didascalia o di traccia audio caricati in un video:**

1. Passa alla risorsa video di cui desideri impostare la traccia audio predefinita.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina **Proprietà**, seleziona la scheda **[!UICONTROL Didascalie e tracce audio]**.
1. Effettua una delle operazioni seguenti:

   * Sottotitoli: sotto l&#39;intestazione **Sottotitoli**, seleziona uno o più file di sottotitoli da scaricare dal video, quindi fai clic sull&#39;icona ![Scarica](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Scarica]**.
   * Tracce audio - Sotto l&#39;intestazione **Tracce audio**, seleziona uno o più file di tracce audio da scaricare dal video, quindi fai clic sull&#39;icona ![Scarica](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Scarica]**.

1. Nella finestra di dialogo Scarica impostare le opzioni seguenti:

   | Opzione di download | Descrizione |
   |--- |--- |
   | Salva con nome | Utilizzare il nome file predefinito specificato nel campo di testo Salva con nome oppure specificare un nome personalizzato. |
   | Crea una cartella separata per ogni risorsa | Creare una cartella per ogni file di didascalia o di traccia audio selezionato per il download. |
   | E-mail | Utilizza il tuo programma e-mail predefinito per inviare il file .zip a un indirizzo e-mail specificato. |
   | Risorse | Specifica il numero di file da scaricare e la dimensione totale combinata di tutti i file selezionati. Deselezionando questa opzione, il pulsante **[!UICONTROL Scarica]** viene disattivato, impedendo di scaricare qualsiasi file. |
   | Rappresentazioni | Una rappresentazione si riferisce a una versione alternativa o a un’anteprima del file originale, in genere una versione più piccola o a risoluzione inferiore. Se è visualizzato come 0 B, probabilmente significa che non è disponibile alcuna versione alternativa o che è troppo piccolo per registrare una dimensione. |

1. Seleziona **[!UICONTROL Scarica]**.
1. Pubblica il video. Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

<!-- ## About AI-generated captions for videos in Dynamic Media

AI-powered captions in Dynamic Media are designed to enhance video accessibility and engagement by automatically generating accurate and synchronized subtitles. This technology uses advanced AI algorithms to transcribe spoken content into text, which is then displayed as captions on the video. Here are some key features.

* **Automatic Transcription:** The AI system transcribes spoken words from an existing audio file into text in real-time, ensuring that captions are generated quickly and accurately.
* **Multilingual Support:** It supports more than 60 languages, making it easier to reach a global audience. You can even translate your existing captions to different languages.
* **Enhanced Accessibility:** By providing captions, videos become more accessible to viewers who are deaf or hard of hearing, as well as those who prefer to watch videos with the sound off.
* **Improved Engagement:** Captions can help retain viewer attention and improve comprehension, especially in noisy environments or when the viewer's native language is different from the video's language.

These features in Dynamic Media make AI-powered video aptions a valuable tool for content creators looking to enhance their video content's accessibility and engagement. -->

## Aggiungi sottotitoli codificati al video {#adding-captions-to-video}

Puoi estendere la portata dei tuoi video ai mercati globali aggiungendo sottotitoli ai singoli video o ai set di video adattivi. Aggiungendo i sottotitoli, si evita di duplicare l&#39;audio o di utilizzare madrelingua per registrare nuovamente l&#39;audio per ogni lingua. Il video viene riprodotto nella lingua in cui è stato registrato. I sottotitoli delle lingue straniere vengono visualizzati in modo che persone di lingue diverse possano ancora comprendere la porzione audio.

I sottotitoli codificati consentono inoltre una maggiore accessibilità per le persone non udenti o ipoudenti.

>[!NOTE]
>
>Il lettore video utilizzato deve supportare la visualizzazione di sottotitoli codificati.

Vedi anche [Accessibilità in Dynamic Media](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media può convertire i file di didascalia in formato JSON (JavaScript Object Notation). Questa conversione ti consente di incorporare il testo JSON in una pagina web come trascrizione nascosta ma completa del video. I motori di ricerca possono quindi eseguire la ricerca per indicizzazione/indicizzare il contenuto per rendere i video più facilmente individuabili e fornire ai clienti maggiori dettagli sul contenuto video.

Per ulteriori informazioni sull&#39;utilizzo della funzione JSON in un URL, vedere [Server static (non-image) contents](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api).

**Per aggiungere didascalie a un video:**

1. Utilizza un’applicazione o un servizio di terze parti per creare il file di sottotitoli video.

   Assicurati che il file creato segua lo standard WebVTT (Web Video Text Track). L&#39;estensione del nome file dei sottotitoli è `.vtt`. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

   Vedere [WebVTT: formato delle tracce di testo per video Web](https://w3c.github.io/webvtt/).

   Esistono molti siti web che offrono strumenti e servizi gratuiti e avanzati che puoi utilizzare per creare file di sottotitoli WebVTT al di fuori di Dynamic Media.

Seguire le istruzioni visualizzate da un sito per creare e salvare il file WebVTT. Al termine, copiate il contenuto del file di didascalia e incollatelo in un editor di testo normale e salvatelo con un&#39;estensione VTT.

>[!NOTE]
>
>Per il supporto globale dei sottotitoli video in più lingue, lo standard WebVTT richiede la creazione di `.vtt` file e chiamate separati per ogni lingua che si desidera supportare.

In genere, si desidera assegnare al file di didascalia `.vtt` lo stesso nome del file video e aggiungerlo alle impostazioni locali della lingua, ad esempio -EN, -FR o -DE. In questo modo, può essere utile automatizzare la generazione degli URL video utilizzando il sistema WCM esistente.

1. In Experience Manager, carica il file di didascalia WebVTT in DAM.
1. Passa alla risorsa video *published* per associarla al file di didascalia caricato.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse.

   Consulta [Pubblicare risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Effettua una delle seguenti operazioni:

   * Per visualizzare un video popup, fai clic sul pulsante **[!UICONTROL URL]**. Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo. Aggiungi all’URL copiato del video la seguente sintassi:

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     Annotare `,1` alla fine del percorso della didascalia. Subito dopo l&#39;estensione del nome file VTT nel percorso, è possibile abilitare (attivare) o disabilitare (disattivare) il pulsante dei sottotitoli codificati sulla barra del lettore video impostando rispettivamente su `,1` o `,0`.

   * Per un&#39;esperienza di visualizzazione video incorporata, fare clic su **[!UICONTROL Codice di incorporamento]**. Nella finestra di dialogo Incorpora codice, seleziona e copia il codice da incorporare negli Appunti, quindi incolla il codice in un semplice editor di testo. Aggiungi il codice da incorporare copiato con la seguente sintassi:

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     Osserva `,1` alla fine del percorso della didascalia. Subito dopo l&#39;estensione del nome file VTT nel percorso, è possibile abilitare (attivare) o disabilitare (disattivare) il pulsante dei sottotitoli codificati sulla barra del lettore video impostando rispettivamente su `,1` o `,0`.

## Aggiungere marcatori capitolo al video {#adding-chapter-markers-to-video}

Per semplificare la visualizzazione e la navigazione dei video lunghi, aggiungi marcatori capitolo ai singoli video o ai set di video adattivi. Quando un utente riproduce il video, può selezionare i contrassegni dei capitoli sulla timeline del video (noti anche come scorrimento video). Possono facilmente spostarsi nel punto di interesse o passare immediatamente a nuovi contenuti, corsi di formazione e dimostrazioni.

>[!NOTE]
>
>Il lettore video utilizzato deve supportare l’uso dei contrassegni dei capitoli. I lettori video Dynamic Media supportano i marcatori capitolo, ma non i lettori video di terze parti.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Per creare un elenco di capitoli per il video è necessario seguire le stesse procedure utilizzate per creare i sottotitoli. In altre parole, si crea un file WebVTT. Tuttavia, questo file deve essere separato da qualsiasi file di didascalia WebVTT. Non è possibile combinare sottotitoli e capitoli in un unico file WebVTT.

L&#39;esempio seguente può essere utilizzato come esempio del formato utilizzato per creare un file WebVTT con navigazione nei capitoli:

### File WebVTT con navigazione capitolo video {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

Nell&#39;esempio precedente, `Chapter 1` è l&#39;identificatore del cue ed è facoltativo. L&#39;ora di cue di `00:00:000 --> 01:04:364` specifica l&#39;ora di inizio e l&#39;ora di fine del capitolo, nel formato `00:00:000`. Le ultime tre cifre sono millisecondi e possono essere lasciate come `000`, se lo si desidera. Il titolo del capitolo di `The bicycle store behind it all` è la descrizione effettiva del contenuto del capitolo. L’identificatore del cue, l’ora di inizio del cue e il titolo del capitolo vengono visualizzati in un pop-up nel lettore video quando un utente passa il puntatore del mouse su un punto di cue visivo nella timeline.

Poiché si utilizza un visualizzatore video HTML5, assicurarsi che il file del capitolo creato segua lo standard WebVTT (Web Video Text Tracks). L&#39;estensione del nome file del capitolo è `.vtt`. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

Vedere [WebVTT: formato delle tracce di testo per video Web](https://w3c.github.io/webvtt/).

**Per aggiungere marcatori capitolo a un video:**

1. Salvare il file `.vtt` nella codifica UTF8 per evitare problemi con la rappresentazione dei caratteri nel testo del titolo del capitolo.

   In genere, si desidera assegnare al file VTT del capitolo lo stesso nome del file video e aggiungerlo ai capitoli. In questo modo, può essere utile automatizzare la generazione degli URL video utilizzando il sistema WCM esistente.
1. In Experience Manager, carica il file del capitolo WebVTT.

   Consulta [Caricare risorse](/help/assets/manage-digital-assets.md#uploading-assets).

1. Effettua una delle seguenti operazioni:

   <table>
     <tbody>
      <tr>
       <td>Per un'esperienza di visualizzazione video pop-up:</td>
       <td>
       <ol>
       <li>Passa alla risorsa video <i>pubblicata </i> per associarla al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Vedi <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Pubblicazione di Assets.</a></li>
       <li>Dal menu a discesa, selezionare <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, seleziona il nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, fai clic sul pulsante <strong>URL</strong>.</li>
       <li>Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo.</li>
       <li>Aggiungi l'URL copiato del video con la seguente sintassi per associarlo all'URL copiato nel file del capitolo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Per un'esperienza di visualizzazione video incorporata,<br /> </td>
       <td>
       <ol>
       <li>Passa alla risorsa video <i>pubblicata </i> per associarla al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Vedi <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Pubblicazione di Assets.</a></li>
       <li>Dal menu a discesa, selezionare <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, seleziona il nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, seleziona <strong>Incorpora</strong>.</li>
       <li>Nella finestra di dialogo Incorpora codice, seleziona e copia l’intero codice negli Appunti, quindi incollalo in un semplice editor di testo.</li>
       <li>Aggiungi il codice di incorporamento del video con la seguente sintassi per associarlo all’URL copiato nel file del capitolo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>


## Informazioni sulle miniature video {#about-video-thumbnails}

Una miniatura video è una versione di dimensioni ridotte di un fotogramma video o di una risorsa immagine che rappresenta il video per il cliente. La miniatura dovrebbe servire a incoraggiare un cliente a selezionare il video.

A tutti i video in Experience Manager deve essere associata una miniatura. Per impostazione predefinita, quando caricate un video in Experience Manager, il primo fotogramma viene utilizzato come miniatura. Tuttavia, è possibile personalizzare la miniatura a scopo di branding o di ricerca visiva. Quando si personalizza una miniatura video, è possibile riprodurre il video e metterlo in pausa sul fotogramma che si desidera utilizzare. In alternativa, puoi selezionare una risorsa immagine che hai già caricato e *pubblicato* nel tuo gestore di risorse digitali.

Quando si modifica la miniatura di un video, viene ignorata la generazione della miniatura tramite il servizio Asset Compute durante la rielaborazione del video.

La possibilità di personalizzare una miniatura video è disponibile solo dopo aver applicato un profilo video alla cartella in cui si trova il video.

### Aggiungi una miniatura video personalizzata {#adding-a-custom-video-thumbnail}

1. Accertati di aver già eseguito le seguenti operazioni:

   * È stata creata una cartella per le risorse video.
   * [Ha applicato un profilo video alla cartella](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   * [I tuoi video sono stati caricati nella cartella](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).


1. Passa a una risorsa video caricata di cui desideri modificare l’immagine in miniatura.
1. In modalità di selezione delle risorse, da ![Visualizza icona scheda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista a schede) o ![Visualizza icona elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista a elenco), seleziona la risorsa video.
1. Sulla barra degli strumenti fare clic su ![Icona informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Proprietà.
1. Nella pagina Proprietà del video, fai clic su **[!UICONTROL Cambia miniatura]**.
1. Nella finestra di dialogo Cambia miniatura eseguire una delle operazioni seguenti:

   * Per utilizzare un fotogramma del video come nuova miniatura:

      * Sulla barra degli strumenti fare clic sulla scheda **[!UICONTROL Seleziona frame da video]**.
      * Fai clic sull&#39;icona ![Play](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg).
      * Fare clic sull&#39;icona ![Pausa](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PauseCircle_22_N.svg) del fotogramma che si desidera acquisire come nuova miniatura del video.

   * Per utilizzare una risorsa immagine come nuova miniatura:

      * Sulla barra degli strumenti fare clic sulla scheda **[!UICONTROL Seleziona miniatura da Assets]**.
      * Fare clic sul pulsante **[!UICONTROL Seleziona miniatura]**.
      * Passa a una risorsa immagine caricata e pubblicata in precedenza che desideri utilizzare. La risorsa viene ridimensionata automaticamente in modo da fungere da immagine miniatura per il video.
      * Seleziona la risorsa immagine, quindi fai clic su **[!UICONTROL Seleziona]**.

1. Nella finestra di dialogo Cambia miniatura fare clic su **[!UICONTROL Salva modifica]**.
1. Nella pagina Proprietà del video, nell&#39;angolo superiore destro, fai clic su **[!UICONTROL Salva e chiudi]** o **[!UICONTROL Salva]**.



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 &times; 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## Modificare l’URL di Dynamic Media per le risorse Dynamic Media

I visualizzatori predefiniti possono riprodurre i video elaborati in Dynamic Media. Puoi anche riprodurli accedendo direttamente agli URL del manifesto e utilizzando visualizzatori personalizzati. Di seguito è riportata l’API per recuperare gli URL del manifesto di un video.

### Informazioni sull’API getVideoManifestURI

L&#39;API `getVideoManifestURI`è esposta tramite c`q-scene7-api:com.day.cq.dam.scene7.api` e può essere utilizzata per generare i seguenti URL manifesto:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Parametri API getVideoManifestURI

Questa API accetta i tre parametri seguenti:

| Parametro | Descrizione |
| --- | --- |
| `resource` | Risorsa corrispondente al video acquisito da Dynamic Media. |
| `manifestType` | Può essere `ManifestType.DASH` o `ManifestType.HLS` |
| `onlyIfPublished` | Imposta su true se l’URI del manifesto viene generato solo se è pubblicato e disponibile sul livello di consegna. |

Per recuperare gli URL del manifesto per i video utilizzando il metodo descritto sopra, aggiungere un [profilo di codifica video](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) a una cartella &quot;carica video&quot;. Dynamic Media elabora questi video in base alle codifiche trovate nel file di codifica video assegnato alla cartella. Ora puoi richiamare la precedente API per recuperare gli URL del manifesto per i video caricati.

### Scenari di errore

L’API restituisce null in caso di errori. Le eccezioni vengono registrate nei registri di errore di Experience Manager. Tutti gli errori registrati iniziano con `Could not generate Video Manifest URI`. Gli errori possono verificarsi nei seguenti scenari:

* `IllegalArgumentException` viene registrato per uno dei seguenti elementi:

   * Il parametro `resource` passato è nullo.
   * Il parametro `resource` passato non è un video.
   * Il parametro `manifestType` passato è nullo.
   * Il parametro `onlyIfPublished` viene passato come true, ma il video non viene pubblicato.
   * Il video non è stato acquisito utilizzando un set di video adattivi da Dynamic Media.

* `IOException` viene registrato quando si verifica un problema di connessione a Dynamic Media.
* `UnsupportedOperationException` viene registrato quando un parametro `manifestType` passato è `ManifestType.DASH`, mentre il video non è stato elaborato utilizzando il formato DASH.

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->


<!-- REMOVED THE FOLLOWING TOPIC AS PER EMAIL FROM RIYA MIDHA, WEDNESDAY, MARCH 5, 2025; TOPIC IS OBSOLETE/NO LONGER NEEDED BECAUSE THE FEATURES IT DESCRIBES ARE NOW GA WITHIN THE SOFTWARE

## Enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account {#enable-dash}

You can enable support in Dynamic Media for:

* DASH
* Multi-captions and audio tracks
* AI-generated captions (Limited Availability)

By creating and submitting an Adobe Customer Support case. 

Enabling any of the above three capabilities, enables all of them. So, if you only want DASH enabled, you are actually enabling all three capabilities listed above.  

| Capability | Description |
| --- | --- |
| DASH | DASH (Digital Adaptive Streaming over HTTP) is the international standard for video streaming and is widely adopted across different video viewers. When DASH is enabled on your account, you get the option to choose from either DASH or HLS for adaptive video streaming. Or, you can opt for both with automatic switching between players when **[!UICONTROL auto]** is selected as the playback type in the Viewer preset.<br>Some key benefits from enabling DASH on your account include the following:<ul><li>Package DASH stream video for adaptive bitrate streaming. This method leads to higher efficiency of delivery. Adaptive streaming ensures the best viewing experience for your customers.</li><li>Browser optimized streaming with Dynamic Media players switches between HLS and DASH streaming to ensure the best quality of service. The video player auto-switches to HLS when a Safari browser is used.</li><li>You can configure your preferred streaming method (HLS or DASH) by editing the video viewer preset.</li><li>Optimized video encoding ensures that no additional storage is used while enabling DASH capability. A single set of video encodings is created for both HLS and DASH to optimize video storage costs.</li><li>Helps make video delivery more accessible for your customers.</li><li>Get the streaming URL by way of APIs, too.</li></ul>|
| Multi-captions and audio tracks | You can benefit from having multiple caption and audio track support automatically enabled. After enablement, all subsequent videos that you upload are processed with a new backend architecture that includes support for adding multiple caption and audio tracks to your videos. |
| AI-generated captions (Limited Availability) | Create captions for your videos powered by AI. Using AI, it creates the transcript of the video and converts it into captions. Even the timeline is defined, too. |

>[!IMPORTANT]
>
>Any videos that you uploaded *before* enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account:** 

1. [Use the Admin Console to start the creation of a new support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. To create a support case, follow the instructions while ensuring you provide the following information:

    * Primary contact name, email, phone.
    * Your Cloud Services environment (program ID and environment ID).
    * Your Dynamic Media company account name.
    * Your Dynamic Media region: North America (NA), Asia-Pacific (APAC), or Europe-Middle East-Asia (EMEA).
    * Specify that you want DASH, multi-captions and multi-audio tracks, and AI-generated captions (Limited Availability) support enabled on your Dynamic Media account, on AEM as a Cloud Service.
   
1. Adobe Customer Support adds you to the Customer Wait List based on the order in which requests are submitted.
1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate and set a target date for enablement.
1. Adobe Customer Support notifies you after completion.
1. Now, do one or more of the following:

    * Create your [video viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) as usual.
    * Create your [video profile](/help/assets/dynamic-media/video-profiles.md) as usual.
    * [Add multiple captions and audio tracks](#add-msma) to your video. -->


<!-- 
## About multiple caption and audio track support for videos in Dynamic Media{#about-msma}

With multiple caption and audio track capability in Dynamic Media, you can easily add multiple captions and audio tracks to a primary video. This capability means that your videos are accessible to a global audience. You can customize a single, published primary video to a global audience in multiple languages and adhere with accessibility guidelines for different geographical regions. Authors can also manage the captions and audio tracks from a single tab in the user interface.

   ![Captions and audio tracks tab in Dynamic Media along with a table showing uploaded .VTT caption files and uploaded .MP3 audio track files for a video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)


Some of the use cases to consider for adding multiple captions and audio tracks to your primary video include the following:

| Type | Use case |
| --- | --- |
| Captions | Multiple language support<br>Descriptive text for accessibility |
| Audio tracks | Multiple language support<br>Commentary tracks<br>Descriptive audio |


All [video formats supported in Dynamic Media](/help/assets/file-format-support.md) and all Dynamic Media video viewers-except the Dynamic Media Video_360 viewer-are supported for use with multiple captions and audio tracks.

Multi-caption and multi-audio track capability is available for your Dynamic Media account by way of a feature toggle that must be enabled (turned on) by Adobe Customer Support.

### Add multiple captions and audio tracks to your video {#add-msma}

Before you add multiple caption and audio tracks to your video, be sure you already have the following in-place:

* Dynamic Media is set up in an AEM environment.
* A [Dynamic Media Video profile is applied to the folder where your videos are ingested](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Multi-caption, and multi-audio track is enabled on your Dynamic Media account](/help/assets/dynamic-media/video.md#enable-dash).

Added captions and captions are supported with WebVTT and Adobe VTT formats. And, added audio track files are supported with MP3 format.

>[!IMPORTANT]
>
>Any videos that you uploaded before enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To add multiple captions and audio tracks to your video:**

1. [Upload your primary video to a folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) that already has a video profile assigned to it.
1. Navigate to the uploaded video asset that you want to add multiple caption and audio tracks.
1. In asset selection mode, either from the List View or the Card View, select the video asset.
1. On the toolbar, select the Properties icon (a circle with an "i" in it). 

   ![Asset properties button.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Selected video asset in Card View.*

1. On the video's Properties page, select the **[!UICONTROL Captions & Audio tracks]** tab.


   >[!TIP]
   >If you do not see the [!UICONTROL Captions & Audio tracks] tab, it means either one of two things:
   >* The folder in which the selected video resides does not have a video profile assigned to it. In which case, see [Apply a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Or, Dynamic Media must reprocess the video. In which case, see [Reprocess Dynamic Media assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

    When you have completed either one of the above tasks, return to these steps.

   ![Asset properties](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Captions and audio tracks tab on the video's Properties page.*

1. (Optional) To add one or more caption files to a video, do the following:

    * Select **[!UICONTROL Upload Captions]**.
    * Navigate to, and select, one or more `.vtt` (Video Text Tracks) files and open them.
    * For captions to be visible on the media player, you must add required details (metadata) about each caption file that you uploaded. Select the pencil icon to the right of a caption file name. In the Edit Caption dialog box, enter the following required details about the file, then select **[!UICONTROL Save]**. Repeat this process for each caption file that you uploaded:


    | Caption metadata | Description | 
    | --- | --- | 
    Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional caption files and audio track files. |
    | Language | Select the language of the caption. |
    | Type | Select the type of caption that you are using.<br>**Subtitle** - The caption text displayed with the video that translates or transcribes the dialogue.<br>**Caption** - The caption text includes background noises and speaker identification. It also includes other relevant details alongside the translation or transcription of dialogue. This functionality makes the content more accessible to individuals who are deaf or hard of hearing. |
    | Label | The text that is displayed for the caption's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to a subtitle or caption track. For example, English (CC). |

    You can change or edit caption metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. (Optional) To add one or more audio tracks to a video, do the following:

    * Select **[!UICONTROL Upload Audio Tracks]**.
    * Navigate to, and select, one or more .mp3 files and open them.
    * To make audio tracks visible in the **[!UICONTROL Select audio or caption]** pop-up list on the media player, add the required details for each audio track file. Ensure you include all necessary information for proper display. Select the pencil icon to the right of an audio track file name. In the Edit Audio Track dialog box, enter the following required details, then select **[!UICONTROL Save]**. Repeat this process for each audio track file that you uploaded.

    | Audio Track metadata | Description |
    | --- | --- |
    | Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional audio track files or caption files.| 
    | Language | Select the language of the audio track. |
    | Type | Select the type of audio track that you are using.<br>**Original** - The audio track originally attached to the video and represented as `[Original]` in the label with English language selected by default. While **[!UICONTROL Label]** and **[!UICONTROL Language]** can be changed in the **[!UICONTROL Edit Audio Track]** dialog box, it defaults to the original values if the primary video is reprocessed.<br>**Standard** - An add-on audio track for a language other than the original.<br>**Audio description** - An audio track that also includes a descriptive narration of non-verbal actions and gestures in the video, making content more accessible for individuals who are visually impaired. |
    | Label | The text that is displayed as the audio track's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to an audio track. For example, `English [Original]`. The label of audio attached to a video is set to `[Original]` by default. |

    You can change or edit this audio track metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. In the upper-right corner of the page, from the **[!UICONTROL Save & Close]** drop-down list, select **[!UICONTROL Save]**. The files are uploaded and metadata processing begins, as seen in the Status column of the interface.

    >[!NOTE]
    >
    >Based on the caching settings of your instance, the metadata processing can take several minutes before it is reflected in preview and in published URLs.

1. (Optional) If you selected **[!UICONTROL Save & Close]** in the previous step, instead of selecting **[!UICONTROL Save]**, you can still view the processing status of the uploaded files. See [View the lifecycle status of uploaded caption and audio track files](/help/assets/dynamic-media/video.md#lifecycle-status-video).

1. (Optional) Preview the video before publishing to ensure the captions and audio work as expected. See [Preview a video that has multiple captions and audio tracks](/help/assets/dynamic-media/video.md#preview-video-audio-subtitle).

1. Publish the video. See [Publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md). -->






