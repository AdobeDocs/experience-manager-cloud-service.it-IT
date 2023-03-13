---
title: Video in Dynamic Media
description: Scopri come utilizzare i video in Dynamic Media. Rivedi le best practice per la codifica di video, la pubblicazione di video in YouTube, la visualizzazione di rapporti video e l’aggiunta di sottotitoli, sottotitoli o marcatori capitolo ai video.
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 2009e549eadd97d4d2bfcccd728ece17ecfeede5
workflow-type: tm+mt
source-wordcount: '10122'
ht-degree: 4%

---

# Video {#video}

Questa sezione descrive come lavorare con i video in Dynamic Media.

## Guida introduttiva: Video {#quick-start-videos}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a utilizzare i set video adattivi in Dynamic Media. Dopo ogni passaggio, sono disponibili riferimenti incrociati alle intestazioni degli argomenti in cui è possibile trovare ulteriori informazioni.

>[!NOTE]
>
>Prima di lavorare con i video in Dynamic Media, accertati che l’amministratore di Adobe Experience Manager abbia già abilitato e configurato i Cloud Services Dynamic Media.
>
>* Consulta [Configurare Cloud Services Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media e [Risoluzione dei problemi di Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).
>


1. **Carica i video Dynamic Media** effettuando le seguenti operazioni:

   * Crea un tuo profilo di codifica video. Oppure, puoi semplicemente utilizzare il predefinito _Codifica video adattiva_ profilo fornito con Dynamic Media.

      * [Creare un profilo di codifica video](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Ulteriori informazioni su [Best practice per la codifica video](#best-practices-for-encoding-videos).
   * Associa il profilo di elaborazione video a una o più cartelle in cui stai per caricare i video sorgente principali.

      * [Applicare un profilo video alle cartelle](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Ulteriori informazioni su [Organizzare le risorse digitali](/help/assets/organize-assets.md).
   * Carica i video sorgente principali nelle cartelle. Quando aggiungi video alla cartella, questi vengono codificati in base al profilo di elaborazione video assegnato alla cartella.

      * Dynamic Media supporta principalmente video in formato breve con una durata massima di 30 minuti e una risoluzione minima superiore a 25 x 25.
      * Puoi caricare file video con una capacità massima di 15 GB ciascuno.
      * [Carica i video](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Ulteriori informazioni su [Formati di file di input supportati](/help/assets/file-format-support.md).
   * Monitorare come [codifica video in corso](#monitoring-video-encoding-and-youtube-publishing-progress) dalla vista delle risorse o del flusso di lavoro.




1. **Gestire i video Dynamic Media** effettuando una delle seguenti operazioni:

   * Organizzare, sfogliare e cercare risorse video

      * [Organizzare le risorse digitali](/help/assets/organize-assets.md)
      * [Cercare risorse video](/help/assets/search-assets.md#custompredicates) o [Ricerca risorse](/help/assets/manage-digital-assets.md#search-assets)
   * Visualizzare in anteprima e pubblicare le risorse video

      * Visualizza il video sorgente e le rappresentazioni codificate del video insieme alle miniature associate:
         [Anteprima video](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) o [Visualizzare in anteprima le risorse](/help/assets/dynamic-media/previewing-assets.md)
         [Gestire le rappresentazioni video](/help/assets/manage-digital-assets.md#managing-renditions)

      * [Gestire i predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [Pubblicazione delle risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
   * Utilizzare i metadati video

      * Modifica le proprietà del video come il titolo, la descrizione, i tag e i campi di metadati personalizzati:
         [Modifica delle proprietà video](/help/assets/manage-digital-assets.md#editing-properties)

      * [Gestione dei metadati per le risorse digitali](/help/assets/manage-metadata.md)
      * [Schemi metadati](/help/assets/metadata-schemas.md)
   * Rivedi, approva e commenta video e mantieni il controllo completo della versione

      * [Aggiunta di annotazioni ai video](/help/assets/manage-video-assets.md#annotate-video-assets) o [Aggiunta di annotazioni alle risorse](/help/assets/manage-digital-assets.md#annotating)

      * [Creazione di una versione](/help/assets/manage-digital-assets.md#asset-versioning)
      * [Avvio di un flusso di lavoro su una risorsa](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [Esaminare le risorse della cartella](/help/assets/bulk-approval.md)
      * [Progetti](/help/sites-cloud/authoring/projects/overview.md)




1. **Pubblicare i video Dynamic Media** effettuando una delle seguenti operazioni:

   * Se utilizzi Experience Manager come sistema WCM (Web Content Management), puoi aggiungere video direttamente alle pagine web.

      * [Aggiungere video alle pagine web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
   * Se utilizzi un sistema di gestione dei contenuti web di terze parti, puoi collegare o incorporare video nelle pagine web.

      * Integra video tramite URL:
         [Collegamento degli URL all’applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integra il video utilizzando il codice di incorporamento nella pagina web:
         [Incorporare il visualizzatore video in una pagina web](/help/assets/dynamic-media/embed-code.md).
   * [Pubblicare video su YouTube](#publishing-videos-to-youtube).
   * [Generare rapporti video](#viewing-video-reports).

   * [Aggiungi didascalie al video](#adding-captions-to-video).



## Utilizzare i video in Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media è una soluzione end-to-end che consente di pubblicare facilmente video adattivi di alta qualità per lo streaming su più schermi, inclusi desktop, tablet e dispositivi mobili. Un set video adattivo raggruppa le versioni dello stesso video che sono codificate in diversi formati e bit rate, ad esempio 400 kbps, 800 kbps e 1000 kbps. Il computer desktop o il dispositivo mobile rileva la larghezza di banda disponibile.

Ad esempio, su un dispositivo mobile iOS rileva una larghezza di banda come 3G, 4G o Wi-Fi. Quindi seleziona automaticamente il video codificato giusto tra i vari bit rate video all’interno del set video adattivo. Il video viene inviato in streaming a desktop, dispositivi mobili o tablet.

Inoltre, la qualità video viene commutata automaticamente se cambiano le condizioni di rete sul desktop o sul dispositivo mobile. Inoltre, se un cliente entra in modalità a tutto schermo su un desktop, il set video adattivo risponde con una risoluzione migliore, migliorando l’esperienza di visualizzazione del cliente. L’utilizzo di set video adattivi offre la migliore riproduzione possibile per i clienti che riproducono video Dynamic Media su più schermi e dispositivi.

La logica utilizzata da un lettore video per determinare quale video codificato riprodurre o selezionare durante la riproduzione si basa sul seguente algoritmo:

1. Il lettore video carica il frammento video iniziale in base al bitrate più vicino al valore impostato per &quot;bitrate iniziale&quot; nel lettore stesso.
1. Il lettore video cambia in base alle modifiche apportate alla velocità della larghezza di banda utilizzando i seguenti criteri:

   1. Il lettore sceglie il flusso di larghezza di banda più alto al di sotto o uguale alla larghezza di banda stimata.
   1. Il lettore considera solo l&#39;80% della larghezza di banda disponibile. Tuttavia, in caso di passaggio, è più prudente con solo il 70% per evitare di sovrastimare e tornare subito indietro.

Per informazioni tecniche dettagliate sull’algoritmo, consulta [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Per la gestione di set video singoli e adattivi, sono supportati i seguenti elementi:

* Caricamento di video da numerosi formati video supportati e formati audio e codifica video in formato MP4 H.264 per la riproduzione su più schermi. È possibile utilizzare predefiniti per video adattivi, predefiniti per codifica video singola o personalizzare la propria codifica per controllare la qualità e le dimensioni del video.

   * Quando viene generato un set video adattivo, questo include video MP4.
   * **Nota**: i video principali/sorgente non vengono aggiunti a un set di video adattivi.

* Sottotitoli video in tutti i visualizzatori video di HTML5.
* Organizza, sfoglia e cerca video con supporto completo per i metadati, per una gestione efficiente delle risorse video.
* Distribuisci set video adattivi per web e desktop, tablet e dispositivi mobili.

Lo streaming video adattivo è supportato su varie piattaforme iOS. Consulta [Guida di riferimento per i visualizzatori di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Riproduci il video utilizzando i predefiniti visualizzatore video Dynamic Media, inclusi i seguenti elementi:

   * Visualizzatori video singoli.
   * Visualizzatori di file multimediali diversi che combinano contenuti sia video che immagini.

* Configura i lettori video in base alle tue esigenze di branding.
* Integra il video nel tuo sito web, sito mobile o app mobile con un semplice URL o codice da incorporare.

Consulta [Riproduzione video dinamica](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) esempio.

Vedi anche [Visualizzatori per Experience Manager Assets e Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) e [Visualizzatori solo per Experience Manager Assets](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) nel [Guida di riferimento per i visualizzatori di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

## Best practice: utilizzo del visualizzatore video di HTML5 {#best-practice-using-the-html-video-viewer}

I predefiniti visualizzatore video di Dynamic Media HTML5 sono lettori video affidabili. Puoi utilizzarli per evitare molti problemi comuni associati alla riproduzione di video HTML5 e problemi associati ai dispositivi mobili. Ad esempio, una mancanza di distribuzione di streaming bitrate adattivo e una portata limitata del browser desktop.

Dal lato della progettazione del lettore, puoi progettare le funzionalità del lettore video utilizzando gli strumenti di sviluppo web standard. Ad esempio, puoi progettare pulsanti, controlli e sfondo personalizzato per l’immagine del poster utilizzando HTML5 e CSS per raggiungere i clienti con un aspetto personalizzato.

Sul lato di riproduzione del visualizzatore, rileva automaticamente la funzionalità video del browser. Distribuisce quindi il video utilizzando HLS o DASH, noto anche come streaming video adattivo. Oppure, se tali metodi di consegna non sono presenti, viene utilizzato invece HTML5 progressive.

>[!NOTE]
>
>Per utilizzare DASH per i video, è necessario prima attivarlo tramite il supporto tecnico Adobe sul tuo account. Consulta [Abilita DASH sul tuo account](#enable-dash).)

Puoi combinare in un singolo lettore la possibilità di progettare i componenti di riproduzione utilizzando HTML5 e CSS. Può avere una riproduzione incorporata e utilizzare uno streaming adattivo e progressivo a seconda delle funzionalità del browser. Tutte queste funzionalità consentono di estendere la portata dei contenuti rich media agli utenti desktop e mobili e di garantire un&#39;esperienza video semplificata.

Vedi anche [Visualizzatori solo per Experience Manager Assets](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) nel [Guida di riferimento per i visualizzatori di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).


### Riproduzione di video su computer desktop e dispositivi mobili mediante il visualizzatore video di HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Per lo streaming video adattivo per desktop e dispositivi mobili, i video utilizzati per il passaggio a bit rate si basano su tutti i video MP4 nel set di video adattivi.

La riproduzione video viene eseguita utilizzando HLS o DASH oppure tramite download progressivo di video. Nelle versioni precedenti di Experience Manager, come 6.0, 6.1 e 6.2, i video venivano inviati in streaming tramite HTTP.

Tuttavia, nell’Experience Manager 6.3 e versioni successive, i video vengono ora inviati in streaming tramite HTTPS (ovvero, HLS o DASH) perché l’URL del servizio gateway DM utilizza sempre HTTPS. Questo comportamento predefinito non ha alcun impatto sul cliente. In altre parole, lo streaming video avverrà sempre tramite HTTPS, a meno che non sia supportato dal browser. (vedere la tabella seguente).

Quindi,

* Se disponi di un sito web HTTPS con streaming video HTTPS, lo streaming va bene.
* Se disponi di un sito web HTTP con streaming video HTTPS, lo streaming va bene e non vi sono problemi di contenuti misti dal browser web.

DASH è lo standard internazionale e HLS è uno standard Apple. Entrambi vengono utilizzati per lo streaming video adattivo. Entrambe le tecnologie regolano automaticamente la riproduzione in base alla capacità della larghezza di banda della rete. Consente inoltre al cliente di &quot;cercare&quot; in qualsiasi punto del video senza dover attendere il download del resto del video.

Il video progressivo viene distribuito scaricando e memorizzando il video localmente sul sistema desktop o sul dispositivo mobile di un utente.

La tabella seguente descrive il dispositivo, il browser e il metodo di riproduzione dei video su computer desktop e dispositivi mobili che utilizzano [Visualizzatore video di Dynamic Media HTML5](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

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
   <td>In Windows® 8 e Windows® 10 - Forza l’uso di HTTPS ogni volta che viene richiesto DASH o HLS. Limitazione nota: HTTP su DASH o HLS non funziona in questa combinazione browser/sistema operativo<br /> <br /> Su Windows® 7 - Download progressivo. Utilizza la logica standard per selezionare il protocollo HTTP rispetto al protocollo HTTPS.</td>
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
   <td>Mobile</td>
   <td>Chrome (Android™ 6 o versioni precedenti)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (Android™ 7 o versione successiva)</td>
   <td>HLS o DASH* adaptive bitrate streaming/td&gt;
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Android™ (browser predefinito)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Safari (iOS)</td>
   <td>Streaming bitrate adattivo HLS</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (iOS)</td>
   <td>Streaming bitrate adattivo HLS</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Per utilizzare DASH per i video, è necessario prima attivarlo con l&#39;assistenza tecnica Adobe sul tuo account. Consulta [Abilita DASH sul tuo account](#enable-dash).)

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

Il **Codifica video Dynamic Media** se hai attivato Dynamic Media e hai impostato Cloud Services video, workflow codifica video. Questo flusso di lavoro acquisisce la cronologia del processo del flusso di lavoro e le informazioni di errore. Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress). Se hai attivato Dynamic Media e configurato Cloud Services video, il **[!UICONTROL Codifica video Dynamic Media]** il flusso di lavoro viene applicato automaticamente al caricamento di un video. Se non utilizzi Dynamic Media, il **[!UICONTROL Aggiorna risorsa DAM]** il flusso di lavoro ha effetto.)

Di seguito sono riportati alcuni suggerimenti sulle best practice per la codifica di file video sorgente.

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### File video sorgente {#source-video-files}

Quando codificate un file video, utilizzate un file video sorgente della massima qualità possibile. Evita di utilizzare file video codificati in precedenza perché sono già compressi e un’ulteriore codifica crea un video di qualità inferiore.

* Dynamic Media supporta principalmente video in formato breve con una durata massima di 30 minuti e una risoluzione minima superiore a 25 x 25.
* È possibile caricare file video di origine primari fino a 15 GB ciascuno.

La tabella seguente descrive le dimensioni, le proporzioni e la velocità bit minima consigliate per i file video sorgente prima di codificarli:

| Dimensione | Proporzioni | Velocità bit minima |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps per la maggior parte dei video. |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps, in base alla quantità di movimento nel video. |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps, a seconda della quantità di movimento nel video. |

### Ottenere i metadati di un file {#obtaining-a-file-s-metadata}

Puoi ottenere i metadati di un file visualizzandone i metadati utilizzando uno strumento di modifica per video o un’applicazione progettata per ottenere i metadati. Di seguito sono riportate le istruzioni per l’utilizzo di MediaInfo, un’applicazione di terze parti, per ottenere i metadati di un file video:

1. Vai a [Download di MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Selezionare e scaricare il programma di installazione per la versione GUI e seguire le istruzioni di installazione.
1. Dopo l&#39;installazione, fare clic con il pulsante destro del mouse sul file video (solo Windows®) e selezionare MediaInfo, oppure aprire MediaInfo e trascinare il file video nell&#39;applicazione. Puoi visualizzare tutti i metadati associati al file video, compresi quelli relativi a larghezza, altezza e fps.

### Proporzioni {#aspect-ratio}

Quando scegliete o create un predefinito di codifica video per il file video sorgente principale, assicuratevi che il predefinito abbia le stesse proporzioni del file video sorgente principale. Le proporzioni corrispondono al rapporto tra la larghezza e l&#39;altezza del video.

Per determinare le proporzioni di un file video, recuperate i metadati del file e annotate la larghezza e l&#39;altezza del file (consultate Ottenere i metadati di un file qui sopra). Quindi utilizza questa formula per determinare le proporzioni:

larghezza/altezza = proporzioni

Nella tabella seguente viene descritto come i risultati della formula si traducono in scelte di proporzioni comuni:

| Risultato formula | Proporzioni |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

Ad esempio, un video con larghezza 1440 x altezza 1080 ha proporzioni 1440/1080 o 1,33. In questo caso, scegliete un predefinito di codifica video con proporzioni 4:3 per codificare il file video.

### Bitrate {#bitrate}

Bitrate è la quantità di dati codificati per costituire un singolo secondo di riproduzione video. Il bitrate viene misurato in kilobit al secondo (Kbps).

>[!NOTE]
>
>Poiché tutti i codec utilizzano la compressione con perdita di dati, il bitrate è il fattore più importante nella qualità video. Con la compressione con perdita di dati, più si comprime un file video, più la qualità si riduce. Per questo motivo, tutte le altre caratteristiche sono uguali (risoluzione, frame rate e codec), minore è il bitrate, minore è la qualità del file compresso.

Quando si seleziona una codifica bitrate, è possibile scegliere tra due tipi:

* **[!UICONTROL Codifica bitrate costante]** (CBR) - Durante la codifica CBR, il bitrate o il numero di bit al secondo viene mantenuto invariato durante il processo di codifica. La codifica CBR mantiene la velocità dati impostata sull’impostazione per l’intero video. Inoltre, la codifica CBR non ottimizza i file multimediali per la qualità, ma consente di risparmiare spazio di archiviazione.
Utilizzate CBR se il video contiene un livello di movimento simile per l&#39;intero video. CBR viene utilizzato più comunemente per lo streaming di contenuti video. Vedi anche [Utilizzare parametri di codifica video personalizzati](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codifica bitrate variabile]** (VBR) - La codifica VBR regola la velocità dati verso il basso e al limite superiore impostato, in base ai dati richiesti dal compressore. Questa funzionalità significa che durante un processo di codifica VBR il bitrate del file multimediale aumenta o diminuisce in modo dinamico a seconda delle esigenze di bitrate dei file multimediali.
La codifica VBR richiede più tempo, ma produce i risultati più favorevoli; la qualità del file multimediale è superiore. VBR viene utilizzato in genere per la distribuzione progressiva http di contenuti video.

Quando si utilizza VBR rispetto a CRB?
Quando selezioni VBR rispetto a CBR, si consiglia quasi sempre di utilizzare VBR per i file multimediali. VBR fornisce file di qualità superiore a bitrate competitivi. Quando si utilizza VBR, assicurarsi di utilizzare con la codifica a due passate e impostare il bitrate massimo su 1,5 volte il bitrate video di destinazione.

Quando scegli un predefinito di codifica video, accertati di tenere conto della velocità di connessione dell’utente finale di destinazione. Scegli un predefinito con una velocità dati pari all’80% di quella velocità. Ad esempio, se la velocità di connessione dell&#39;utente finale è di 1000 Kbps, il valore predefinito migliore è 800 Kbps.

Questa tabella descrive la velocità dati delle velocità di connessione tipiche.

| Velocità (Kbps) | Tipo di connessione |
|--- |--- |
| 256 | Connessione remota. |
| 800 | Connessione mobile tipica. Per questa connessione, esegui il targeting di una velocità di dati compresa tra 400 e un massimo di 800 per le esperienze 3G. |
| 2000 | Connessione desktop a banda larga tipica. Per questa connessione, eseguire il targeting di una velocità di dati nell&#39;intervallo 800-2000 Kbps, con la maggior parte delle destinazioni in media 1200-1500 Kbps. |
| 5000 | Tipica connessione a banda larga. La codifica in questo intervallo superiore non è consigliata perché la distribuzione di video a questa velocità non è disponibile per la maggior parte dei consumatori. |

### Risoluzione {#resolution}

**Risoluzione** descrive l&#39;altezza e la larghezza in pixel di un file video. La maggior parte dei video sorgente viene memorizzata ad alta risoluzione (ad esempio, 1920 x 1080). Ai fini dello streaming, il video sorgente viene compresso a una risoluzione inferiore (640 x 480 o inferiore).

La risoluzione e la velocità dei dati sono due fattori strettamente collegati che determinano la qualità video. Per mantenere la stessa qualità video, maggiore è il numero di pixel in un file video (maggiore è la risoluzione), maggiore è la velocità dati. Ad esempio, si consideri il numero di pixel per fotogramma in un file video con risoluzione 320 x 240 e 640 x 480:

| Risoluzione | Pixel per frame |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

Il file 640 x 480 ha un numero di pixel per frame quattro volte superiore. Per ottenere la stessa velocità dati per queste due risoluzioni di esempio, applicate una compressione quattro volte superiore al file 640 x 480, riducendo in tal modo la qualità del video. Di conseguenza, una velocità di dati video di 250 Kbps produce una visualizzazione di alta qualità con una risoluzione di 320 x 240, ma non con una risoluzione di 640 x 480.

In generale, maggiore è la velocità di dati utilizzata, migliore è la visualizzazione del video e maggiore è la risoluzione utilizzata, maggiore è la velocità di dati da mantenere la qualità di visualizzazione (rispetto a risoluzioni inferiori).

Poiché la risoluzione e la velocità dati sono collegate, durante la codifica del video sono disponibili due opzioni:

* Scegli una velocità dati e quindi codificala alla risoluzione più alta che sembra buona alla velocità dati scelta.
* Scegliete una risoluzione e quindi codificate alla velocità dati necessaria per ottenere video di alta qualità alla risoluzione desiderata.

Quando scegli (o crei) un predefinito di codifica video per il file video sorgente principale, utilizza questa tabella per individuare la risoluzione corretta:

| Risoluzione | Altezza (pixel) | Dimensioni dello schermo |
|--- |--- |--- |
| 240p | 240 | Schermo piccolo |
| 300p | 300 | Schermo piccolo in genere per dispositivi mobili |
| 360p | 360 | Schermo piccolo |
| 480p | 480 | Schermo medio |
| 720p | 720 | Schermo grande |
| 1080p | 1080 | Schermo ad alta definizione di grandi dimensioni |

### Fps (frame al secondo) {#fps-frames-per-second}

Negli Stati Uniti e in Giappone, la maggior parte dei video viene girata a 29,97 fps; in Europa, la maggior parte dei video viene girata a 25 fps. Il film viene girato a 24 fps.

Scegli un predefinito di codifica video che corrisponda alla velocità fps del file video sorgente principale. Ad esempio, se il video sorgente principale è a 25 fps, scegliete un predefinito di codifica con 25 fps. Per impostazione predefinita, tutta la codifica personalizzata utilizza il fps del file video sorgente principale. Per questo motivo, non è necessario specificare esplicitamente l&#39;impostazione fps quando si crea un predefinito di codifica video.

### Dimensioni di codifica video {#video-encoding-dimensions}

Per risultati ottimali, seleziona dimensioni di codifica tali che il video sorgente sia un multiplo di tutti i video codificati.

Per calcolare questo rapporto, si divide la larghezza dell&#39;origine per la larghezza codificata per ottenere il rapporto di larghezza. Quindi, per ottenere il rapporto di altezza, dividi l’altezza sorgente per altezza codificata.

Se il rapporto risultante è un numero intero, significa che il video è ridimensionato in modo ottimale. Se il rapporto risultante non è un numero intero, influisce sulla qualità video lasciando sul display gli artefatti di pixel rimanenti. Questo effetto è più evidente quando il video contiene del testo.

Ad esempio, supponiamo che il video sorgente sia 1920 x 1080. Nella tabella seguente, i tre video codificati forniscono le impostazioni di codifica ottimali da utilizzare.

| Tipo di video | Larghezza x altezza | Rapporto larghezza | Rapporto altezza |
|--- |--- |--- |--- |
| Sorgente | 1920x1080 | 1 | 1 |
| Codificato | 960 x 540 | 2 | 2 |
| Codificato | 640 x 360 | 3 | 3 |
| Codificato | 480 x 270 | 4 | 4 |

### Formato file video codificato {#encoded-video-file-format}

Dynamic Media consiglia di utilizzare i predefiniti di codifica video MP4 H.264. Poiché i file MP4 utilizzano il codec video H.264, questo offre video di alta qualità ma in dimensioni di file compressi.

### Abilita DASH sul tuo account {#enable-dash}

DASH (Digital Adaptive Streaming over HTTP) è lo standard internazionale per lo streaming video ed è ampiamente adottato tra diversi visualizzatori video. Quando DASH è abilitato sul tuo account, puoi scegliere tra DASH o HLS per lo streaming video adattivo. Oppure, è possibile optare per entrambi con cambio automatico tra i lettori quando **[!UICONTROL auto]** viene selezionato come tipo di riproduzione nel predefinito Visualizzatore.

Alcuni vantaggi chiave dell&#39;attivazione di DASH sul tuo account includono:

* Video con flusso DASH del pacchetto per lo streaming con bitrate adattivo. Questo metodo porta a una maggiore efficienza nella consegna. Lo streaming adattivo assicura la migliore esperienza di visualizzazione per i clienti.
* Lo streaming ottimizzato per il browser con i lettori Dynamic Media passa dallo streaming HLS a quello DASH per garantire la migliore qualità del servizio. Il lettore video passa automaticamente a HLS quando si utilizza un browser Safari.
* Puoi configurare il metodo di streaming preferito (HLS o DASH) modificando il predefinito visualizzatore video.
* La codifica video ottimizzata garantisce che non venga utilizzata alcuna risorsa di archiviazione aggiuntiva durante l’abilitazione della funzionalità DASH. Viene creato un unico set di codifiche video sia per HLS che per DASH per ottimizzare i costi di archiviazione video.
* Consente di rendere la distribuzione di video più accessibile ai clienti.
* Ottieni l’URL di streaming anche tramite API.

   >[!IMPORTANT]
   >
   >L’abilitazione di DASH sul tuo account è attualmente disponibile solo in Nord America.

Viene avviata una richiesta per l&#39;utilizzo di DASH, che non viene abilitata automaticamente sul tuo account.

Per abilitare DASH sul tuo account, crea un caso di assistenza clienti come descritto di seguito. Nel caso di supporto, specifica di voler abilitare DASH sul tuo account Dynamic Media e su Experience Manager.

**Per abilitare DASH sul tuo account:**

1. [Utilizza l’Admin Console per avviare la creazione di un nuovo caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Segui le istruzioni per creare un caso di supporto e accertati di fornire le seguenti informazioni:

   * Nome del contatto principale, e-mail, telefono.
   * Nome dell’account Dynamic Media.
   * Specifica che il DASH deve essere abilitato sul tuo account Dynamic Media e su Experience Manager.

1. L’Assistenza clienti Adobe ti aggiunge alla lista d’attesa dei clienti DASH in base all’ordine in cui vengono inviate le richieste.
1. Quando Adobe è pronto a gestire la richiesta, l’Assistenza clienti ti contatta per coordinare e impostare una data limite per l’abilitazione di DASH.
1. Ricevi una notifica dopo il completamento da parte dell’Assistenza clienti.
1. Crea [predefinito visualizzatore video](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) come al solito.

## Pubblicare video su YouTube {#publishing-videos-to-youtube}

Puoi pubblicare le risorse video gestite in Experience Manager Assets direttamente su un canale YouTube creato in precedenza.

Per pubblicare risorse video in YouTube, devi assegnare tag alle risorse video in Experience Manager Assets. Associa questi tag a un canale YouTube. Se il tag di una risorsa video corrisponde a quello di un canale YouTube, il video viene pubblicato in YouTube. La pubblicazione su YouTube viene eseguita insieme alla normale pubblicazione del video, purché venga utilizzato un tag associato.

YouTube esegue la propria codifica. Di conseguenza, il file video originale caricato in Experience Manager viene pubblicato in YouTube invece di qualsiasi rendering video creato dalla codifica di Dynamic Media. Anche se non è necessario per elaborare i video utilizzando Dynamic Media, è previsto che lo facciano nel caso in cui sia necessario un predefinito visualizzatore per la riproduzione.

Quando salti il profilo di elaborazione video e pubblichi direttamente in YouTube, significa semplicemente che la risorsa video in Experience Manager Asset non riceve una miniatura visualizzabile. Significa anche che i video non codificati non funzionano con nessuno dei tipi di risorse Dynamic Media.

La pubblicazione di risorse video sui server YouTube prevede il completamento delle seguenti attività per garantire una verifica server-to-server sicura con YouTube:

1. [Configurare le impostazioni di Google Cloud](#configuring-google-cloud-settings)
1. [Creare un canale YouTube](#creating-a-youtube-channel)
1. [Aggiungi tag per la pubblicazione](#adding-tags-for-publishing)
1. [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem)
1. [(Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Pubblicare video sul canale YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Facoltativo) Verifica il video pubblicato su YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Collegare gli URL di YouTube all’applicazione web](#linking-youtube-urls-to-your-web-application)

È inoltre possibile [annullare la pubblicazione dei video per rimuoverli da YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Configurare le impostazioni di Google Cloud {#configuring-google-cloud-settings}

Per pubblicare su YouTube, è necessario un account Google. Se si dispone di un account GMAIL, si dispone già di un account Google; se non si dispone di un account Google, è possibile crearne facilmente uno. L’account è necessario perché sono necessarie credenziali per pubblicare risorse video in YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

Non è necessario che l’account utilizzato con Google Cloud e l’account Google utilizzato per YouTube siano gli stessi.

Google modifica periodicamente l’interfaccia utente. Di conseguenza, i passaggi per pubblicare video in YouTube possono variare leggermente rispetto a quanto documentato di seguito. Questa avvertenza si applica anche ad YouTube quando tenti di verificare se i video sono stati caricati su di esso.

>[!NOTE]
>
>I seguenti passaggi erano accurati al momento della scrittura. Tuttavia, Google aggiorna periodicamente le pagine web cloud senza preavviso. Di conseguenza, alcune opzioni di configurazione nell’interfaccia utente di Google potrebbero essere denominate in modo leggermente diverso rispetto al nome utilizzato nei passaggi.

**Per configurare le impostazioni di Google Cloud:**

1. Crea un account Google.
   [https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp](https://accounts.google.com/signup/v2?service=mail&amp;flowName=GlifWebSignIn&amp;flowEntry=SignUp)

   Se disponi già di un account Google, puoi passare al passaggio successivo.

1. Vai a [https://cloud.google.com/](https://cloud.google.com/).
1. Il giorno **[!UICONTROL Google Cloud]** nell&#39;angolo superiore destro, seleziona **[!UICONTROL Console]**.

   Se necessario, **[!UICONTROL Accedi]** utilizzo delle credenziali dell&#39;account Google per visualizzare **[!UICONTROL Console]** opzione.

1. Il giorno **[!UICONTROL Dashboard]** a destra di **[!UICONTROL Piattaforma Google Cloud]**, seleziona la **[!UICONTROL Progetto]** elenco a discesa per aprire **[!UICONTROL Seleziona un progetto]** .
1. In **[!UICONTROL Seleziona un progetto]** finestra di dialogo, seleziona **[!UICONTROL Nuovo progetto]**.
1. In **[!UICONTROL Nuovo progetto]** nella finestra di dialogo **[!UICONTROL Nome progetto]** digitare il nome del nuovo progetto.

   L&#39;ID progetto si basa sul nome del progetto. Pertanto, scegli attentamente il nome del progetto, che non può essere modificato dopo la creazione. Inoltre, devi immettere nuovamente lo stesso ID progetto quando configuri YouTube in Experience Manager in un secondo momento. Pertanto, trascrivilo.

1. Seleziona **[!UICONTROL Crea]**.

1. Effettuare una delle seguenti operazioni:

   * Nel dashboard del progetto, nella sezione **[!UICONTROL Guida introduttiva]** , seleziona **[!UICONTROL Esplora e abilita API]**.
   * Nel dashboard del progetto, nella sezione **[!UICONTROL API]** , seleziona **[!UICONTROL Vai alla panoramica delle API]**.

1. Vicino alla parte superiore centrale del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL ABILITA API E SERVIZI]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. Il giorno **[!UICONTROL Libreria API]** pagina, a sinistra, sotto **[!UICONTROL Categoria]**, seleziona **[!UICONTROL YouTube]**. Sul lato destro della pagina, seleziona **[!UICONTROL YouTube]**.
1. Il giorno **[!UICONTROL YouTube]** pagina, seleziona **[!UICONTROL API dati YouTube v3]**.
1. Il giorno **[!UICONTROL API dati YouTube v3]** pagina, seleziona **[!UICONTROL GESTISCI]**.

   ![6_5_googleaccount-apis-manage](assets/6_5_googleaccount-apis-manage.png)

1. Per utilizzare l’API, sono necessarie le credenziali. Se necessario, sul lato sinistro del **[!UICONTROL API e servizi]** pagina, seleziona **[!UICONTROL Credenziali]**.
1. Il giorno **[!UICONTROL Credenziali]** nella parte superiore, seleziona **[!UICONTROL CREA CREDENZIALI]**, quindi seleziona **[!UICONTROL ID client OAuth]**.
1. Il giorno **[!UICONTROL Crea ID client OAuth]** pagina, nella **[!UICONTROL Tipo di applicazione]** elenco a discesa, seleziona **[!UICONTROL Applicazione web]**.

   ![6_5_googleaccount-apis-applicationtype](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Effettua una delle operazioni seguenti:

   * In **[!UICONTROL Nome]** immetti un nome univoco per il client OAuth 2.0.
   * Utilizza il nome predefinito già fornito da Google nel **[!UICONTROL Nome]** campo.

1. Sotto **[!UICONTROL Origini JavaScript autorizzate]** intestazione, seleziona **[!UICONTROL AGGIUNGI URI]**.

   ![6_5_googleaccount-apis-namepermissions](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. In **[!UICONTROL URI]** immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all&#39;elenco:

   `https://<servername.domain>:<port_number>`

   Esempio, `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >L’esempio del percorso URI riportato sopra è ipotetico e solo a scopo illustrativo.

1. Sotto **[!UICONTROL URI di reindirizzamento autorizzati]** , selezionare ADD URI.
1. In **[!UICONTROL URI]** immettere il seguente percorso, sostituendo il proprio dominio e il proprio numero di porta nel percorso, quindi premere **[!UICONTROL Invio]** per aggiungere il percorso all&#39;elenco:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Esempio, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >L’esempio del percorso URI riportato sopra è ipotetico e solo a scopo illustrativo.

1. Vicino alla parte inferiore del **[!UICONTROL Crea ID client OAuth]** pagina, seleziona **[!UICONTROL Crea]**.
1. Il giorno **[!UICONTROL Client OAuth creato]** eseguire le operazioni seguenti:

   * (Facoltativo) Copia i valori in **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** e salvare.
   * Seleziona **[!UICONTROL SCARICA JSON]**, quindi salva il file JSON.

   Questo file JSON scaricato è necessario per la configurazione di YouTube in Adobe Experience Manager in un secondo momento.

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. Il giorno **[!UICONTROL Client OAuth creato]** finestra di dialogo, seleziona **[!UICONTROL OK]**.
1. Esci dal tuo account Google. Ora crea un canale YouTube.

### Creare un canale YouTube {#creating-a-youtube-channel}

La pubblicazione di video in YouTube richiede la presenza di uno o più canali. Se hai già creato un canale YouTube, puoi saltare questa attività e passare a [Aggiungi tag per la pubblicazione](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Verifica di aver già configurato uno o più canali in YouTube *prima di* aggiungi canali in Impostazioni YouTube in Experience Manager (consulta [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem) di seguito). Se non si esegue la configurazione del canale, non viene visualizzato alcun avviso relativo all&#39;assenza di canali esistenti. Tuttavia, la verifica Google si verifica ancora quando si aggiunge un canale, ma non è possibile scegliere quale canale inviare il video.

**Per creare un canale YouTube:**

1. Vai a [https://www.youtube.com](https://www.youtube.com/) e accedi utilizzando le credenziali del tuo account Google.
1. Nell’angolo in alto a destra della pagina YouTube, seleziona l’immagine del profilo (può anche apparire come lettera all’interno di un cerchio di colore uniforme), quindi seleziona **[!UICONTROL Impostazioni di YouTube]** (icona a forma di ingranaggio circolare).
1. Nella pagina Overview (Panoramica), sotto l’intestazione Additional Features (Caratteristiche aggiuntive), seleziona **[!UICONTROL Visualizza tutti i miei canali o crea un canale]**.
1. Nella pagina Canali, seleziona **[!UICONTROL Crea un nuovo canale]**.
1. Nella pagina Account marchio, immetti il nome di una società o di qualsiasi altro nome di canale scelto per la pubblicazione delle risorse video nel campo Nome account marchio, quindi seleziona **[!UICONTROL Crea]**.

   Ricorda il nome che immetti qui; devi immetterlo nuovamente quando devi impostare YouTube in Experience Manager.

1. Se necessario, aggiungi altri canali.

   Ora puoi aggiungere tag per la pubblicazione.

### Aggiungi tag per la pubblicazione {#adding-tags-for-publishing}

Per pubblicare i video in YouTube, Experience Manager associa i tag a uno o più canali di YouTube. Per aggiungere tag per la pubblicazione, consulta [Amministrare i tag](/help/sites-cloud/authoring/features/tags.md).

Oppure, se desideri utilizzare i tag predefiniti in Experience Manager, puoi saltare questa attività e passare a [Configurare YouTube in Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Una volta configurato il Cloud Service, non è necessaria un’altra configurazione per abilitare l’agente di replica YouTube Publish in questo momento. Il motivo è che è stato abilitato quando è stata salvata la configurazione del Cloud Service.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configurare YouTube in Experience Manager {#setting-up-youtube-in-aem}

A partire dall’Experience Manager 6.4, è stato introdotto un nuovo metodo di interfaccia utente touch per configurare la pubblicazione YouTube in Experience Manager. In base all&#39;istanza installata di Experience Manager in uso, eseguire una delle operazioni seguenti:

* Per configurare YouTube in Experience Manager prima della versione 6.4, consulta [Configurare YouTube in Experience Manager prima della versione 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Per configurare YouTube nell’Experience Manager 6.4 o versione successiva, consulta [Configurare YouTube all’Experience Manager 6.4 e versioni successive](#setting-up-youtube-in-aem-and-later).

#### Configurare YouTube all’Experience Manager 6.4 e versioni successive {#setting-up-youtube-in-aem-and-later}

1. Accertati di accedere alla tua istanza di Dynamic Media come amministratore.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]**(icona a forma di martello) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione pubblicazione YouTube]**.
1. Seleziona **[!UICONTROL globale]** (non selezionarlo).

1. Nell’angolo superiore destro della pagina globale, seleziona **[!UICONTROL Crea]**.
1. Nella pagina Crea configurazione YouTube, seleziona Impostazioni piattaforma Google Cloud, quindi immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l’ID del progetto al momento della configurazione iniziale delle impostazioni di Google Cloud.
Lascia aperta la pagina Crea configurazione di YouTube; tornerai tra un attimo.

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività [Configurare le impostazioni di Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   Ora imposta i canali YouTube in Experience Manager.

1. Seleziona **[!UICONTROL Aggiungi canale]**.
1. Nel campo Nome canale, inserisci il nome del canale creato nell’attività **[!UICONTROL Aggiunta di uno o più canali ad YouTube]** prima.

   Facoltativamente, puoi aggiungere una descrizione, se necessario.

1. Seleziona **[!UICONTROL Aggiungi]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Inserisci il nome utente e la password di Google associati all’ID progetto Google e al testo JSON qui sopra.
   * A seconda di quanti canali dispone il tuo account, puoi visualizzare due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica, non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l’accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Services > YouTube, seleziona l’icona a forma di matita per modificare l’elenco di tag che desideri utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona a discesa dell’elenco (cursore a discesa).
1. Per aggiungerli, seleziona uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **[!UICONTROL X]**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL Salva]**.

   Ora pubblichi i video sul tuo canale YouTube.

#### Configurare YouTube in Experience Manager prima della versione 6.4 {#setting-up-youtube-in-aem-before}

1. Accertati di accedere alla tua istanza di Dynamic Media come amministratore.

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud Services]**.
1. Nell’intestazione Servizi di terze parti, in YouTube, seleziona **[!UICONTROL Configura ora]**.
1. Nella finestra di dialogo Crea configurazione, immetti un titolo (obbligatorio) e un nome (facoltativo) nei rispettivi campi.
1. Seleziona **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Impostazioni account di YouTube, immetti l’ID progetto Google nel campo **[!UICONTROL Nome applicazione]**.

   Hai specificato l’ID del progetto al momento della [impostazioni configurate di Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) prima.
Lascia aperta la finestra di dialogo YouTube Account Setting (Impostazioni account di Adobe Experience Cloud). Tornerai tra poco.

1. Utilizzando un editor di testo normale, apri il file JSON scaricato e salvato in precedenza nell’attività Configurazione delle impostazioni di Google Cloud.
1. Seleziona e copia l’intero testo JSON.
1. Torna alla finestra di dialogo Impostazioni account YouTube. Nel campo **[!UICONTROL Configurazione JSON]**, incolla il testo JSON.
1. Seleziona **[!UICONTROL OK]**.

   Ora imposta i canali YouTube in Experience Manager.

1. A destra di **[!UICONTROL Canali disponibili]**, seleziona **+** (icona del segno più).
1. Nella finestra di dialogo Impostazioni canale YouTube, fai clic sul campo Titolo e immetti il nome del canale creato nell’attività precedente **[!UICONTROL Aggiunta di uno o più canali a YouTube]**.

   Facoltativamente, puoi aggiungere una descrizione, se necessario.

1. Seleziona **[!UICONTROL OK]**.
1. Viene visualizzata la verifica YouTube/Google. Se non hai già effettuato l’accesso all’account Google Cloud, salta questo passaggio.

   * Inserisci il nome utente e la password di Google associati all’ID progetto Google e al testo JSON qui sopra.
   * A seconda di quanti canali dispone il tuo account, puoi visualizzare due o più elementi. Seleziona un canale. Non selezionare l&#39;indirizzo di posta elettronica, non è un canale.
   * Nella pagina successiva, seleziona **[!UICONTROL Accetta]** per consentire l’accesso a questo canale.

1. Seleziona **[!UICONTROL Consenti]**.

   Ora imposta i tag per la pubblicazione.

1. **[!UICONTROL Impostazione dei tag per la pubblicazione]** - Nella pagina Cloud Services > YouTube, seleziona l’icona a forma di matita per modificare l’elenco di tag che desideri utilizzare.
1. Per visualizzare l’elenco dei tag disponibili in Experience Manager, seleziona l’icona a discesa dell’elenco (cursore a discesa).
1. Per aggiungerli, seleziona uno o più tag.

   Per eliminare un tag aggiunto, selezionalo e seleziona **X**.

1. Dopo aver aggiunto i tag desiderati, seleziona **[!UICONTROL OK]**.

   Ora pubblichi i video sul tuo canale YouTube.

### (Facoltativo) Automatizza l&#39;impostazione delle proprietà predefinite di YouTube per i video caricati {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Facoltativamente, puoi automatizzare l’impostazione delle proprietà di YouTube al caricamento dei video. Crea un profilo di elaborazione metadati in Experience Manager.

Per creare il profilo di elaborazione dei metadati, devi prima copiare i valori dai campi **[!UICONTROL Etichetta campo]**, **[!UICONTROL Mappa su proprietà]** e **[!UICONTROL Scelte]**, tutti disponibili in Schemi metadati per i video. Quindi, aggiungi questi valori al profilo di elaborazione dei metadati video di YouTube.

**Per automatizzare l’impostazione delle proprietà predefinite di YouTube per i video caricati:**

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona **[!UICONTROL predefinito]**. (Non aggiungere un segno di spunta alla casella di selezione a sinistra di &quot;default&quot;).
1. Il giorno **[!UICONTROL predefinito]** , seleziona la casella a sinistra di **[!UICONTROL video]**, quindi seleziona **[!UICONTROL Modifica]**.
1. Nella pagina Editor schema metadati, seleziona la **[!UICONTROL Avanzate]** scheda.
1. Sotto l’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Categoria YouTube]**.
1. Sul lato destro della pagina, sotto **[!UICONTROL Impostazioni]** , eseguire le operazioni seguenti:

   * In **[!UICONTROL Mappa su proprietà]** testo, seleziona e copia il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito che desideri utilizzare (ad esempio Persone e blog o Scienza e tecnologia).
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Sotto l’intestazione Pubblicazione YouTube, seleziona **[!UICONTROL Privacy di YouTube]**.
1. Sul lato destro della pagina, sotto **[!UICONTROL Impostazioni]** , eseguire le operazioni seguenti:

   * In **[!UICONTROL Mappa su proprietà]** testo, seleziona e copia il valore.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

   * Sotto **[!UICONTROL Scelte]**, seleziona e copia il valore predefinito che desideri utilizzare. Notate che le scelte sono raggruppate in coppie di due. Il campo inferiore della coppia è il valore predefinito che si desidera copiare, ad esempio public, unlisted o private.
Incolla il valore copiato nell’editor di testo aperto. Questo valore sarà necessario in un secondo momento quando creerai il profilo di elaborazione dei metadati. Lascia aperto l’editor di testo.

1. Nell’angolo superiore destro della pagina Editor schema metadati, seleziona **[!UICONTROL Annulla]**.
1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**.

1. Nella pagina Profili metadati, nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Crea]**.
1. Nella finestra di dialogo Aggiungi profilo metadati, nel **[!UICONTROL Titolo profilo]** testo, immettere il nome `YouTube Video` quindi seleziona **[!UICONTROL Crea]**.
1. Nella pagina Editor profilo metadati, seleziona la **[!UICONTROL Avanza]** scheda.
1. Aggiungi al profilo i valori di pubblicazione di YouTube copiati effettuando le seguenti operazioni:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Genera modulo]** scheda.
   * (Facoltativo) Trascina il componente etichettato **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarlo nell&#39;area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Nella parte destra della pagina, nella scheda Impostazioni, nel campo di testo Etichetta campo, immetti `YouTube Publishing`.
   * Seleziona la **[!UICONTROL Genera modulo]** , quindi trascina il componente con l’etichetta **[!UICONTROL Testo con più valori]** e rilascialo sotto il **[!UICONTROL Pubblicazione YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Nella parte destra della pagina, nella scheda Impostazioni, incolla i valori di pubblicazione di YouTube (valore Etichetta campo e Mappa su valore proprietà) copiati in precedenza nei rispettivi campi del modulo. Incolla il valore Scelte nel campo Valore predefinito.

1. Aggiungi i valori di YouTube Privacy copiati al profilo effettuando le seguenti operazioni:

   * Sul lato destro della pagina, seleziona la **[!UICONTROL Genera modulo]** scheda.
   * (Facoltativo) Trascina il componente etichettato **[!UICONTROL Intestazione sezione]** a sinistra e rilasciarlo nell&#39;area del modulo.
   * (Facoltativo) Seleziona **[!UICONTROL Etichetta campo]** per selezionare il componente.
   * (Facoltativo) Nella parte destra della pagina, nella scheda Impostazioni, nel campo di testo Etichetta campo, immetti `YouTube Privacy`.
   * Seleziona la **[!UICONTROL Genera modulo]** , quindi trascina il componente con l’etichetta **[!UICONTROL Testo con più valori]** e rilascialo sotto il **[!UICONTROL Privacy di YouTube]** intestazione creata.

   * Per selezionare il componente, seleziona **[!UICONTROL Etichetta campo]**.
   * Nella parte destra della pagina, nella scheda Impostazioni, incolla i valori di pubblicazione di YouTube (valore Etichetta campo e Mappa su valore proprietà) copiati in precedenza nei rispettivi campi del modulo. Incolla il valore Scelte nel campo Valore predefinito.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.
1. Applica il profilo di metadati Pubblicazione YouTube alle cartelle in cui stai per caricare i video. Devi avere sia il Profilo metadati che il Profilo video impostati.

   Consulta le sezioni [Profili di metadati](/help/assets/metadata-profiles.md) e [Profili video](/help/assets/dynamic-media/video-profiles.md).

### Pubblicare video sul canale YouTube {#publishing-videos-to-your-youtube-channel}

Ora associ alle risorse video i tag aggiunti in precedenza. Questo consente agli Experienci Manager di sapere quali risorse pubblicare nel canale YouTube.

>[!NOTE]
>
>La pubblicazione immediata non viene automaticamente pubblicata in YouTube. Quando si imposta Dynamic Media, è possibile scegliere tra due opzioni di pubblicazione: **[!UICONTROL Immediatamente]** o **[!UICONTROL All’attivazione]**.
>
>**[!UICONTROL Pubblica immediatamente]** significa che la risorsa caricata, dopo essere stata sincronizzata con IPS, viene pubblicata automaticamente nel sistema di consegna. Anche se questo è vero per Dynamic Media, non lo è per YouTube. Per pubblicare in YouTube, devi utilizzare l’Autore Experience Manager.

>[!NOTE]
Per pubblicare contenuti da YouTube, Experience Manager utilizza **[!UICONTROL Pubblica su YouTube]** che consente di monitorare l’avanzamento e visualizzare eventuali informazioni sull’errore.
Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
Per informazioni più dettagliate sullo stato di avanzamento, puoi monitorare il registro di YouTube in replica. Tenere presente, tuttavia, che tale monitoraggio richiede l&#39;accesso dell&#39;amministratore.

**Per pubblicare video sul canale YouTube:**

1. Ad Experience Manager, individua la risorsa video da pubblicare sul tuo canale YouTube.
1. Seleziona la risorsa video (il set di video adattivi).
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda Base, seleziona l’intestazione Metadati **[!UICONTROL Apri finestra di dialogo per selezione]** a destra del campo Tag.
1. Nella pagina Seleziona tag passare ai tag che si desidera utilizzare e quindi selezionare uno o più tag.

   Ricorda che i tag devono essere associati al canale YouTube.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.
1. Nell’angolo superiore destro della pagina delle proprietà del video, seleziona **[!UICONTROL Salva e chiudi]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   Vedi anche [Utilizzare Gestione delle pubblicazioni con Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Facoltativamente, puoi verificare il video pubblicato sul tuo canale YouTube.

### (Facoltativo) Verifica il video pubblicato su YouTube {#optional-verifying-the-published-video-on-youtube}

Facoltativamente, puoi monitorare lo stato della pubblicazione (o dell’annullamento della pubblicazione) in YouTube.

Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

I tempi di pubblicazione possono variare notevolmente a seconda di numerosi fattori, tra cui il formato del video sorgente principale, la dimensione del file e il traffico di caricamento. Il processo di pubblicazione può richiedere da pochi minuti a diverse ore. Inoltre, i formati a risoluzione più elevata vengono riprodotti molto più lentamente. Ad esempio, le modalità 720p e 1080p richiedono più tempo rispetto alla modalità 480p.

Dopo otto ore, se ricevi ancora un messaggio di stato che indica **[!UICONTROL Caricato (elaborazione, attendere)]**, prova a rimuovere il video dal sito e a caricarlo di nuovo.

### Collegare gli URL di YouTube all’applicazione web {#linking-youtube-urls-to-your-web-application}

Dopo la pubblicazione del video, puoi ottenere una stringa URL di YouTube generata da Dynamic Media. Quando copi l’URL di YouTube, questo viene inserito negli Appunti, in modo da poterlo incollare nelle pagine del sito web o dell’applicazione.

>[!NOTE]
L’URL di YouTube non è disponibile per la copia finché non hai pubblicato la risorsa video in YouTube.

Per collegare gli URL di YouTube alla tua applicazione web:

1. Accedi a *YouTube pubblicato* risorsa video di cui desideri copiare l’URL, quindi selezionala.

   Gli URL di YouTube sono disponibili solo per la copia *dopo* hai prima *pubblicato* le risorse video in YouTube.

1. Sulla barra degli strumenti, seleziona **[!UICONTROL Proprietà]**.
1. Seleziona la **[!UICONTROL Avanzate]** scheda.
1. Nell’elenco URL di YouTube Publishing, seleziona e copia il testo dell’URL nel browser Web per visualizzare in anteprima la risorsa o aggiungerlo alla pagina di contenuto Web, sotto l’intestazione Pubblicazione di YouTube.

### Annullare la pubblicazione dei video per rimuoverli da YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Quando annulli la pubblicazione di una risorsa video in Experience Manager, il video viene rimosso da YouTube.

>[!CAUTION]
Se rimuovi un video direttamente da YouTube, Experience Manager non ne è a conoscenza e continua a comportarsi come se il video fosse ancora pubblicato in YouTube. Per Experience Manager, annulla sempre la pubblicazione di una risorsa video da YouTube.

>[!NOTE]
Per rimuovere il contenuto da YouTube, Experience Manager utilizza **[!UICONTROL Annulla pubblicazione da YouTube]** che consente di monitorare l’avanzamento e visualizzare eventuali informazioni sull’errore.
Consulta [Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Per annullare la pubblicazione dei video e rimuoverli da YouTube:**

1. Passa alle risorse video di cui vuoi annullare la pubblicazione dal tuo canale YouTube.
1. In modalità di selezione delle risorse, seleziona una o più risorse video pubblicate.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Se necessario, seleziona l’icona dei tre punti (`. . .`) sulla barra degli strumenti per visualizzare **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina Gestisci pubblicazione, seleziona **[!UICONTROL Annulla pubblicazione]**.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Successivo]**.
1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Annulla pubblicazione]**.

## Monitorare la codifica video e l’avanzamento della pubblicazione in YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Quando carichi un nuovo video in una cartella a cui è applicata la codifica video o, pubblichi il video in YouTube, monitori l’avanzamento (o l’errore) della codifica video/pubblicazione su Youtube. L’avanzamento effettivo della pubblicazione in YouTube è disponibile solo tramite i registri. Ma se fallisce o ha successo, viene elencato in altri modi descritti nella procedura seguente. Inoltre, ricevi notifiche e-mail quando un flusso di lavoro o una codifica video di YouTube Publish viene completato o interrotto.

### Monitorare l’avanzamento {#monitoring-progress}

Puoi monitorare l’avanzamento, inclusa la codifica non riuscita/pubblicazione YouTube.

1. Visualizza l’avanzamento della codifica video nella cartella delle risorse:

   * Nella vista a schede, l’avanzamento della codifica video viene visualizzato sulla risorsa in percentuale. In caso di errore, queste informazioni vengono visualizzate anche sulla risorsa.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * Nella vista a elenco, l’avanzamento della codifica video viene visualizzato nel **[!UICONTROL Stato elaborazione]** colonna. In caso di errore, il messaggio viene visualizzato nella stessa colonna.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Questa colonna non viene visualizzata per impostazione predefinita. Per abilitare la colonna, seleziona **[!UICONTROL Impostazioni vista]** dal menu a discesa viste e aggiungi **[!UICONTROL Stato elaborazione]** e seleziona **[!UICONTROL Aggiorna]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visualizza l’avanzamento nei dettagli della risorsa. Quando selezioni una risorsa, apri il menu a discesa e seleziona **[!UICONTROL Timeline]**. Per limitarla alle attività del flusso di lavoro come la codifica o la pubblicazione YouTube, seleziona **[!UICONTROL Flussi di lavoro]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   Tutte le informazioni sul flusso di lavoro, ad esempio la codifica, vengono visualizzate nella timeline. Per YouTube Publish, la timeline del flusso di lavoro include anche il nome del canale YouTube e l’URL del video YouTube. Inoltre, una volta completata la pubblicazione, nella timeline del flusso di lavoro vengono visualizzate tutte le notifiche di errore.

   >[!NOTE]
   Potrebbero essere necessari tempi lunghi per la registrazione dei messaggi di errore/guasto, a causa della presenza di più configurazioni di workflow **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), ad esempio:
   * Configurazione coda processi Apache Sling
   * Adobe Granite Workflow External Process Job Handler
   * Coda di timeout del flusso di lavoro Granite

   È possibile regolare **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** proprietà in queste configurazioni.

1. Per i flussi di lavoro in corso, vedi l’opzione Istanze flusso di lavoro accedendo a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Istanze]**.

   >[!NOTE]
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Seleziona l’istanza e seleziona **[!UICONTROL Cronologia elementi aperti]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Dall’area Istanze flusso di lavoro, puoi anche sospendere, terminare o rinominare i flussi di lavoro. Consulta [Amministrare i flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md) per ulteriori informazioni.

1. Per i processi non riusciti, consulta l’opzione Errori di flusso di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Errori]**. In **[!UICONTROL Errore flusso di lavoro]** sono elencate tutte le attività del flusso di lavoro che hanno generato errori.

   >[!NOTE]
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   Potrebbero essere necessari tempi lunghi per la registrazione del messaggio di errore, a causa della presenza di più configurazioni di workflow in **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** da [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), ad esempio:
   * Configurazione coda processi Apache Sling
   * Adobe Granite Workflow External Process Job Handler
   * Coda di timeout del flusso di lavoro Granite

   È possibile regolare **[!UICONTROL nuovi tentativi]**, **[!UICONTROL ritarda nuovo tentativo]**, e **[!UICONTROL timeout]** proprietà in queste configurazioni.

1. Per i flussi di lavoro completati, consulta Archivio flussi di lavoro, accessibile da **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Archivio]**. **[!UICONTROL Archivio flussi di lavoro]** elenca tutte le attività del flusso di lavoro che sono state completate.

   >[!NOTE]
   Sono necessari diritti di amministratore per accedere a **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Ricevi notifiche e-mail sui processi del flusso di lavoro interrotti o non riusciti. Queste notifiche e-mail possono essere configurate da un amministratore. Consulta [Configurare le notifiche e-mail](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## Visualizzare rapporti video {#viewing-video-reports}

>[!NOTE]
I rapporti video sono disponibili solo quando si esegue Dynamic Media in modalità ibrida.

I rapporti video visualizzano diverse metriche aggregate in un determinato periodo per aiutarti a monitorare che *pubblicato* i singoli video e i video aggregati funzionano come previsto. I seguenti dati sulle metriche principali sono aggregati per tutti i video pubblicati sull’intero sito web:

* Inizio video
* Percentuale completata
* Tempo medio sul video
* Tempo totale su video
* Video per visita

Una tabella di tutti *pubblicato* Sono elencati anche i video, in modo da poter tenere traccia dei video più visualizzati sul sito web in base al totale degli avvii dei video.

Quando selezioni un nome video nell’elenco, viene visualizzato il rapporto di conservazione del pubblico (a discesa) del video sotto forma di un grafico a linee. Il grafico mostra il numero di visualizzazioni per un dato momento della riproduzione video. Quando si riproduce il video, la barra verticale viene sincronizzata con l&#39;indicatore di tempo nel lettore. Le cadute nei dati del grafico a linee indicano dove il pubblico abbandona il disinteresse.

Se il video è stato codificato al di fuori di Adobe Experience Manager Dynamic Media, il grafico di conservazione del pubblico (a discesa) e i dati della percentuale di riproduzione nella tabella non sono disponibili.

>[!NOTE]
I dati di tracciamento e reporting si basano esclusivamente sull’utilizzo del lettore video di Dynamic Media e del relativo predefinito per lettore video. Di conseguenza, non è possibile tracciare e creare rapporti sui video riprodotti da altri lettori video.

Per impostazione predefinita, la prima volta che si immettono i rapporti video, il rapporto visualizza i dati video a partire dal primo del mese corrente e termina con la data del mese corrente. Tuttavia, puoi sovrascrivere l’intervallo di date predefinito specificando un intervallo di date personalizzato. Alla successiva immissione di Report video, viene utilizzato l&#39;intervallo di date specificato.

Affinché i rapporti video funzionino correttamente, viene creato automaticamente un ID suite di rapporti quando vengono configurati i Cloud Services Dynamic Media. Allo stesso tempo, l’ID suite di rapporti viene inviato al server di pubblicazione, in modo che sia disponibile per la funzione Copia URL quando visualizzi l’anteprima delle risorse. Tuttavia, questa funzionalità richiede che il server di pubblicazione sia già configurato. Se il server di pubblicazione non è configurato, puoi comunque eseguire la pubblicazione per visualizzare il rapporto video. Tuttavia, devi tornare alla configurazione cloud di Dynamic Media e selezionare **[!UICONTROL OK]**.

**Per visualizzare i rapporti video:**

1. Nell’angolo in alto a sinistra dell’Experience Manager, seleziona il logo dell’Experience Manager, quindi nella barra a sinistra passa a **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti video]**.
1. Nella pagina Rapporti video eseguire una delle operazioni seguenti:

   * Nell&#39;angolo superiore destro, selezionare **[!UICONTROL Aggiorna rapporto video]** icona.
Utilizzare Aggiorna solo se la data di fine del rapporto è il giorno corrente. Questa funzione ti assicura di visualizzare il tracciamento video che si è verificato dall’ultima volta che hai eseguito il rapporto.

   * Nell&#39;angolo superiore destro, selezionare **[!UICONTROL Selettore data]** icona.
Specifica l’intervallo di date iniziale e finale per il quale desideri visualizzare i dati video, quindi seleziona **[!UICONTROL Esegui rapporto]**.

   La casella di gruppo Metriche principali identifica varie misurazioni aggregate per tutti *pubblicato* video nel sito.

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

## Aggiungere sottotitoli codificati o sottotitoli al video {#adding-captions-to-video}

Puoi estendere la portata dei tuoi video ai mercati globali aggiungendo sottotitoli ai singoli video o ai set di video adattivi. Aggiungendo i sottotitoli, si evita di duplicare l&#39;audio o di utilizzare madrelingua per registrare nuovamente l&#39;audio per ogni lingua. Il video viene riprodotto nella lingua in cui è stato registrato. I sottotitoli delle lingue straniere vengono visualizzati in modo che persone di lingue diverse possano ancora comprendere la porzione audio.

I sottotitoli codificati consentono inoltre una maggiore accessibilità per le persone non udenti o ipoudenti.

>[!NOTE]
Il lettore video utilizzato deve supportare la visualizzazione di sottotitoli codificati.

Vedi anche [Accessibilità in Dynamic Media](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media può convertire i file di didascalia in formato JSON (JavaScript Object Notation). Questa conversione ti consente di incorporare il testo JSON in una pagina web come trascrizione nascosta ma completa del video. I motori di ricerca possono quindi eseguire la ricerca per indicizzazione/indicizzare il contenuto per rendere i video più facilmente individuabili e fornire ai clienti maggiori dettagli sul contenuto video.

Consulta [Distribuzione di contenuti statici (non di immagine)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) per ulteriori informazioni sull’utilizzo della funzione JSON in un URL.

**Per aggiungere sottotitoli o sottotitoli al video:**

1. Utilizza un’applicazione o un servizio di terze parti per creare il file di sottotitoli/sottotitoli video.

   Assicurati che il file creato segua lo standard WebVTT (Web Video Text Tracks). L&#39;estensione del nome file dei sottotitoli è .VTT. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

   Consulta [WebVTT: formato per tracce di testo video Web](https://w3c.github.io/webvtt/).

   Esistono strumenti e servizi gratuiti e premium che puoi utilizzare per creare file di sottotitoli/sottotitoli al di fuori di Dynamic Media. Ad esempio, per creare un file di sottotitoli video semplice senza stile, potete utilizzare il seguente strumento di creazione e modifica di sottotitoli online gratuito:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Per ottenere risultati ottimali, utilizza lo strumento in Internet Explorer 9 o versioni successive, Google Chrome o Safari.

   Nello strumento, nella sezione **[!UICONTROL Inserisci l’URL del file video]** , incolla l’URL copiato del file video e seleziona **[!UICONTROL Carica]**. Consulta [Ottenere un URL per una risorsa](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) per ottenere l’URL del file video stesso che puoi incollare nel file **[!UICONTROL Immetti l’URL del campo del file video]**. A quel punto, Internet Explorer, Chrome o Safari possono riprodurre il video in modalità nativa.

   Ora segui le istruzioni visualizzate sul sito per creare e salvare il file WebVTT. Al termine, copiate il contenuto del file di didascalia e incollatelo in un editor di testo normale e salvatelo con un&#39;estensione VTT.

   >[!NOTE]
   Per il supporto globale dei sottotitoli video in più lingue, lo standard WebVTT richiede la creazione di file .vtt e chiamate separati per ogni lingua che si desidera supportare.

   In genere, si desidera assegnare al file VTT della didascalia lo stesso nome del file video e aggiungerlo alla lingua locale, ad esempio -EN, -FR o -DE. In questo modo, è possibile automatizzare la generazione degli URL video utilizzando il sistema di gestione dei contenuti web esistente.

1. Ad Experience Manager, carica il file di didascalia WebVTT in DAM.
1. Accedi a *pubblicato* risorsa video da associare al file di didascalia caricato.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse.

   Consulta [Pubblicare le risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Effettua una delle operazioni seguenti:

   * Per visualizzare un video a comparsa, seleziona **[!UICONTROL URL]**. Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo. Aggiungi all’URL copiato del video la seguente sintassi:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Osserva `,1` alla fine del percorso della didascalia. Subito dopo l’estensione del nome file VTT nel percorso, puoi facoltativamente abilitare (attivare) o disabilitare (disattivare) il pulsante dei sottotitoli codificati sulla barra del lettore video impostando su `,1` o `,0`, rispettivamente.

   * Per un’esperienza di visualizzazione video incorporata, seleziona **[!UICONTROL Codice di incorporamento]**. Nella finestra di dialogo Incorpora codice, seleziona e copia il codice da incorporare negli Appunti, quindi incolla il codice in un semplice editor di testo. Aggiungi il codice da incorporare copiato con la seguente sintassi:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Osserva `,1` alla fine del percorso della didascalia. Subito dopo l’estensione del nome file VTT nel percorso, puoi facoltativamente abilitare (attivare) o disabilitare (disattivare) il pulsante dei sottotitoli codificati sulla barra del lettore video impostando su `,1` o `,0`, rispettivamente.

## Aggiungere marcatori capitolo al video {#adding-chapter-markers-to-video}

Per semplificare la visualizzazione e la navigazione dei video lunghi, aggiungi marcatori capitolo ai singoli video o ai set di video adattivi. Quando un utente riproduce il video, può selezionare i contrassegni dei capitoli sulla timeline del video (noti anche come scorrimento video). Possono facilmente spostarsi nel punto di interesse o passare immediatamente a nuovi contenuti, corsi di formazione e dimostrazioni.

>[!NOTE]
Il lettore video utilizzato deve supportare l’uso dei marcatori capitolo. I lettori video Dynamic Media supportano i contrassegni dei capitoli, ma non i lettori video di terze parti.

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

Nell’esempio precedente, `Chapter 1` è l’identificatore del cue ed è facoltativo. Il tempo di cue di `00:00:000 --> 01:04:364` specifica l&#39;ora di inizio e di fine del capitolo, in `00:00:000` formato. Le ultime tre cifre sono millisecondi e possono essere lasciate come `000`, se preferita. Titolo del capitolo di `The bicycle store behind it all` è la descrizione effettiva del contenuto del capitolo. L’identificatore del cue, l’ora di inizio del cue e il titolo del capitolo vengono visualizzati in un pop-up nel lettore video quando un utente passa il puntatore del mouse su un punto di cue visivo nella timeline.

Poiché si utilizza un visualizzatore video di HTML5, assicurarsi che il file del capitolo creato segua lo standard WebVTT (Web Video Text Tracks). L&#39;estensione del nome file del capitolo è .VTT. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

Consulta [WebVTT: formato per tracce di testo video Web](https://w3c.github.io/webvtt/).

**Per aggiungere marcatori capitolo al video:**

1. Salvare il file VTT con codifica UTF8 in modo da evitare problemi con la rappresentazione dei caratteri nel testo del titolo del capitolo.

   In genere, si desidera assegnare al file VTT del capitolo lo stesso nome del file video e aggiungerlo ai capitoli. In questo modo, è possibile automatizzare la generazione degli URL video utilizzando il sistema di gestione dei contenuti web esistente.
1. Ad Experience Manager, carica il file del capitolo WebVTT.

   Consulta [Caricare le risorse](/help/assets/manage-digital-assets.md#uploading-assets).

1. Effettua una delle operazioni seguenti:

   <table>
     <tbody>
      <tr>
       <td>Per un'esperienza di visualizzazione video popup</td>
       <td>
       <ol>
       <li>Accedi a <i>pubblicato </i>risorsa video da associare al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Consulta <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Pubblicazione delle risorse.</a></li>
       <li>Dal menu a discesa, seleziona quindi <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, seleziona il nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, seleziona <strong>URL</strong>.</li>
       <li>Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo.</li>
       <li>Aggiungi l’URL copiato del video con la seguente sintassi per associarlo all’URL copiato nel file del capitolo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Per un’esperienza di visualizzazione video incorporata<br /> </td>
       <td>
       <ol>
       <li>Accedi a <i>pubblicato </i>risorsa video da associare al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Consulta <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Pubblicazione delle risorse.</a></li>
       <li>Dal menu a discesa, seleziona quindi <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, seleziona il nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, seleziona <strong>Incorpora</strong>.</li>
       <li>Nella finestra di dialogo Incorpora codice, seleziona e copia l’intero codice negli Appunti, quindi incollalo in un semplice editor di testo.</li>
       <li>Aggiungi il codice di incorporamento del video con la seguente sintassi per associarlo all’URL copiato nel file del capitolo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to select the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, select the video asset.
1. On the toolbar, select the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Frame from video]**.
        * Select the Play button, then select the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, select **[!UICONTROL Select Thumbnail from Assets]**.
        * Select **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then select **[!UICONTROL Select]**.

1. On the Change Thumbnail page, select **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, select **[!UICONTROL Save & Close]**.

-->

<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

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

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

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

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
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

I video elaborati in Dynamic Media possono essere utilizzati tramite visualizzatori predefiniti e anche accedendo direttamente agli URL del manifesto e riproducendoli attraverso visualizzatori personalizzati. Di seguito è riportata l’API per recuperare gli URL del manifesto di un video.

### Informazioni sull’API getVideoManifestURI

Il `getVideoManifestURI`L’API è esposta tramite c`q-scene7-api:com.day.cq.dam.scene7.api` e possono essere utilizzati per generare i seguenti URL manifesto:

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

Per recuperare gli URL del manifesto per i video utilizzando il metodo precedente, aggiungi un [profilo di codifica video](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) in una cartella &quot;carica video&quot;. Dynamic Media elabora questi video in base alle codifiche trovate nel file di codifica video assegnato alla cartella. Ora puoi richiamare la precedente API per recuperare gli URL del manifesto per i video caricati.

### Scenari di errore

L’API restituisce null in caso di errori. Le eccezioni vengono registrate nei log degli errori di Experience Manager. Tutti gli errori registrati iniziano con `Could not generate Video Manifest URI`. Gli errori possono verificarsi nei seguenti scenari:

* Un `IllegalArgumentException` viene registrato per uno dei seguenti elementi:

   * Il `resource` il parametro passato è nullo.
   * Il `resource` Il parametro passato non è un video.
   * Il `manifestType` il parametro passato è nullo.
   * Il `onlyIfPublished` Il parametro viene passato come true, ma il video non viene pubblicato.
   * Il video non è stato acquisito utilizzando un set video adattivo di Dynamic Media.

* `IOException` viene registrato quando si verifica un problema di connessione a Dynamic Media.
* `UnsupportedOperationException` viene registrato quando `manifestType` il parametro passato è `ManifestType.DASH`, mentre il video non è stato elaborato utilizzando il formato DASH.

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





