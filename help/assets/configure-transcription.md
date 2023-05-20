---
title: Configurare il servizio di trascrizione
seo-title: Configure transcription service
description: Adobe Experience Manager Assets è configurato con [!DNL Azure Media Services] che genera automaticamente la trascrizione testuale della lingua parlata in un file audio o video supportato in formato WebVTT (Vtt).
seo-description: When an audio or video asset is processed in Experience Manager Assets, the AI-based transcription service automatically generates the text transcript rendition of the audio or video asset and stores it at the same location within your Assets repository where the original asset resides. The Experience Manager Assets transcription service allows marketers to effectively manage their audio and video content with added discoverability of the text content as well as increase the ROI of these assets by supporting accessibility and localization.
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
exl-id: e96c8d68-74a6-4d61-82dc-20e619338d4b
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 95%

---

# Configurare la trascrizione in [!DNL Experience Manager Assets] {#configure-transcription-service}

La trascrizione è il processo di traduzione dell’audio da un file audio o video in testo (da un discorso al testo) utilizzando la tecnologia di riconoscimento vocale.
[!DNL Adobe Experience Manager Assets] è configurato con [!DNL Azure Media Services] che genera automaticamente la trascrizione testuale della lingua parlata in un file audio o video supportato in formato WebVTT (.vtt). Quando una risorsa audio o video viene elaborata in [!DNL Experience Manager Assets], il servizio di trascrizione genera automaticamente la rappresentazione trascritta della risorsa audio o video e la memorizza nella stessa posizione all’interno dell’archivio dell risorse in cui risiede la risorsa originale. Il servizio di trascrizione di [!DNL Experience Manager Assets] consente agli addetti al marketing di gestire in modo efficace i contenuti audio e video con in più la possibilità di individuare i contenuti testuali e di aumentare il ritorno sull’investimento di tali risorse, sostenendo l’accessibilità e la localizzazione.

Le trascrizioni sono versioni testuali del contenuto parlato; un esempio è un filmato che visualizzi su qualsiasi piattaforma OTT e che spesso include didascalie o sottotitoli per facilitarne l’accessibilità o per consumarne il contenuto in altre lingue. Oppure qualsiasi file audio o video utilizzato per scopi di marketing, apprendimento o intrattenimento. Queste esperienze iniziano con una trascrizione che viene poi formattata o tradotta come appropriato. La trascrizione di audio o video è un processo che richiede molto tempo ed è soggetto a errori quando viene eseguito manualmente. Il processo manuale rende difficile anche la scalabilità, necessaria data la crescente necessità di contenuti audio-video. [!DNL Experience Manager Assets] utilizza la trascrizione basata sull’intelligenza artificiale di Azure che consente l’elaborazione su larga scala delle risorse audio e video e genera le trascrizioni di testo (file .vtt) insieme ai dettagli delle marche temporali. Oltre ad Assets, la funzione di trascrizione è supportata anche da Dynamic Media.

La funzione di trascrizione è disponibile senza alcun costo in [!DNL Experience Manager Assets]. Tuttavia, per configurare il servizio di trascrizione in gli amministratori hanno bisogno delle credenziali di Azure dell’utente [!DNL Experience Manager Assets]. È inoltre possibile [ottenere le credenziali di prova](https://azure.microsoft.com/en-us/pricing/details/media-services/) direttamente da Microsoft® per scoprire la funzione di trascrizione audio o video in Assets.

## Prerequisiti per la trascrizione {#prerequisites}

1. Istanza [!DNL Experience Manager Assets as a Cloud Service] subito operativa.
1. Le seguenti credenziali di Azure sono necessarie per la configurazione in [!DNL Experience Manager Assets]:

   * ID client (chiave API)
   * Chiave segreto client
   * Endpoint tenant (dominio)
   * Account multimediale
   * Gruppo di risorse
   * ID abbonamento

   Vedi [Documentazione di Azure](https://docs.microsoft.com/it-it/azure/media-services/latest/access-api-howto?tabs=portal) per ottenere le credenziali di accesso all’API di Azure Media Services.

1. Assicurati che l’account Azure disponga di crediti sufficienti per elaborare le nuove richieste.

## Configurare la trascrizione in [!DNL Experience Manager Assets] {#configure-transcription}

Di seguito sono riportate le configurazioni necessarie per abilitare la funzione di trascrizione in [!DNL Experience Manager Assets]:

1. [Configurare Azure Media Services](#configure-azure-media-service)
1. [Configurare il profilo di elaborazione per la trascrizione audio/video](#configure-processing-profile-for-transcription)


### Configurare Azure Media Services {#configure-azure-media-services}

[!DNL Experience Manager Assets] utilizza [!DNL Azure Media Services] che genera automaticamente le trascrizioni testuali della lingua parlata in un [file audio o video supportato](#supported-file-formats-for-transcription) nel formato WebVTT (.vtt). Gli amministratori possono configurare [!DNL Azure Media Services] in [!DNL Experience Manager Assets] utilizzando le credenziali di Azure. I [prerequisiti per la trascrizione](#transcription-prerequisites) elencano le credenziali [!DNL Azure] necessarie per la configurazione. Se non hai account e credenziali [!DNL Azure], consulta la [Documentazione di Azure Media Services](https://azure.microsoft.com/en-us/pricing/details/media-services/) per ottenere le credenziali di prova.

![configure-transcription-service](assets/configure-transcription-service.png)

Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione di Azure Media Services]**. Seleziona una cartella (posizione) dalla barra a sinistra e fai clic sul pulsante [!UICONTROL Crea] per configurare la connessione con l’account [!DNL Azure]. Questa cartella è il percorso in cui è memorizzata la configurazione cloud [!DNL Azure] in Experience Manager Assets. Inserisci le credenziali [!DNL Azure] e fai clic su **[!UICONTROL Salva e chiudi]**.

### Configurare il profilo di elaborazione per la trascrizione {#configure-processing-profile}

Una volta che [!DNL Azure Media Services] è configurato in Experience Manager Assets, il passaggio successivo consiste nel creare un profilo di elaborazione delle risorse per generare la trascrizione delle risorse audio e video basate sull’intelligenza artificiale. Il profilo di elaborazione basato sull’intelligenza artificiale genera le trascrizioni della [risorsa audio o video supportata](#supported-file-formats-for-transcription) come rappresentazione in Experience Manager Assets e memorizza la trascrizione (file .vtt) nella stessa cartella in cui si trova la risorsa originale. In questo modo, è più facile per gli utenti cercare e individuare la risorsa e la relativa rappresentazione trascritta.

Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]** e fai clic sul pulsante **[!UICONTROL Crea]** per creare un profilo di elaborazione basato sull’intelligenza artificiale per generare la trascrizione dei file audio e video. Per impostazione predefinita, la pagina del profilo di elaborazione presenta solo tre schede (Immagine, Video e Personalizzato). Tuttavia, se hai configurato [!DNL Azure Media Services] nella tua istanza [!DNL Experience Manager Assets], è visibile una scheda **[!UICONTROL IA per la gestione dei contenuti]**. Verifica le credenziali [!DNL Azure] se non visualizzi la scheda **[!UICONTROL IA per la gestione dei contenuti]** durante la creazione di un profilo di elaborazione.

Nella scheda **[!UICONTROL IA per la gestione dei contenuti]**, fai clic sul pulsante **[!UICONTROL Aggiungi nuovo]** per configurare la trascrizione. In questo caso è possibile includere ed escludere i formati di file (tipi MIME) per la generazione delle trascrizioni selezionandoli dall’elenco a discesa. Nell’illustrazione seguente, tutti i file audio e video supportati sono inclusi e i file di testo sono esclusi.

Abilita **[!UICONTROL Creare una trascrizione VTT nella stessa directory]** per creare e memorizzare la rappresentazione della trascrizione (file .vtt) nella stessa cartella in cui si trova la risorsa originale. Le altre rappresentazioni vengono generate anche dal flusso di lavoro di elaborazione delle risorse DAM predefinito, indipendentemente da questa impostazione.

![configure-transcription-service](assets/configure-transcription-profile.png)

La figura seguente descrive un profilo video personalizzato creato in Experience Manager Assets.

![configure-transcription-service](assets/video-processing-profile.png)

Il profilo video contiene anche le seguenti configurazioni personalizzate. Consulta la [documentazione del profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md) per informazioni dettagliate su come creare un profilo di elaborazione personalizzato.

![configure-transcription-service](assets/video-processing-profile2.png)

Ora configuriamo la trascrizione in questo profilo video. Passa alla scheda **[!UICONTROL IA per la gestione dei contenuti]** e fai clic sul pulsante **[!UICONTROL Aggiungi nuovo]**. Includi tutti i file audio e video ed escludi i file di immagine e di applicazione. Abilita **[!UICONTROL Creare una trascrizione VTT nella stessa directory]** e salva la configurazione.

![configure-transcription-service](assets/video-processing-profile1.png)

Una volta configurato il profilo di elaborazione per la trascrizione di file audio e video, puoi applicarlo alle cartelle utilizzando uno dei seguenti metodi:

* Seleziona una definizione di profilo di elaborazione in **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]** e utilizza l’azione **[!UICONTROL Applica profilo a cartelle]**. Il browser del contenuto ti consente di passare a una cartella specifica, selezionarla e confermare l’applicazione del profilo.
* Seleziona una cartella nell’interfaccia utente di Assets e fai clic su **[!UICONTROL Proprietà]** per aprire le proprietà della cartella. Fai clic sulla scheda **[!UICONTROL Elaborazione delle risorse]** e seleziona il profilo di elaborazione appropriato per la cartella dall’elenco **[!UICONTROL Profilo di elaborazione]**. Per salvare le modifiche, fai clic su **[!UICONTROL Salva e chiudi]**.

   ![configure-transcription-service](assets/video-processing-profile3.png)

* Per applicare un profilo di elaborazione, gli utenti possono selezionare cartelle o risorse specifiche nell’interfaccia utente di Assets, quindi selezionare **[!UICONTROL Rielabora risorse]** tra le opzioni disponibili nella parte superiore.

>[!TIP]
>A una cartella può essere applicato un solo profilo di elaborazione.
>
>Dopo aver applicato un profilo di elaborazione a una cartella, tutte le nuove risorse caricate (o aggiornate) in questa cartella o in una delle sue sottocartelle vengono elaborate utilizzando il profilo di elaborazione aggiuntivo configurato. Questa elaborazione si aggiunge al profilo predefinito standard.

>[!NOTE]
>
>Un profilo di elaborazione applicato a una cartella funziona per l’intera struttura, tuttavia, può essere sostituito con un altro profilo applicato a una sottocartella.
>
>Quando le risorse vengono caricate in una cartella, Experience Manager comunica con le proprietà della cartella contenitore per identificare il profilo di elaborazione. Se nessun profilo è applicato, viene selezionata una cartella principale nella gerarchia per un profilo di elaborazione da applicare.


## Generare la trascrizione delle risorse audio o video {#generate-transcription}

Quando si elabora una risorsa video, il [Profilo di elaborazione basato sull’intelligenza artificiale](#configure-processing-profile-for-transcription) genera automaticamente la trascrizione (file .vtt) come rappresentazione insieme alla risorsa originale nella stessa cartella.

![configure-transcription-service](assets/transcript1.png)

Puoi anche vedere la rappresentazione della trascrizione accedendo alle rappresentazioni della risorsa video originale. Per accedere al pannello **[!UICONTROL Rappresentazioni]** seleziona la risorsa video originale e apri la barra a sinistra. È possibile vedere che la rappresentazione della trascrizione (file .vtt) è visibile sotto l’intestazione **[!UICONTROL TRANSCRIPTVTT]**.

![configure-transcription-service](assets/transcript.png)

Puoi scaricare la trascrizione (file di testo .vtt) direttamente dalla cartella come una rappresentazione separata della risorsa o dall’interno del pannello **[!UICONTROL Rappresentazioni]** della risorsa originale scaricando tutte le rappresentazioni della risorsa.

Attualmente, Experience Manager non supporta l’anteprima full-text o la modifica nativa di file VTT. Tuttavia, puoi scaricare la rappresentazione della trascrizione e utilizzare qualsiasi editor di testo per modificarla o verificarla. La trascrizione riflette la lingua parlata come un testo in una marca temporale determinata nel video con il punteggio di affidabilità (precisione) della trascrizione.

![configure-transcription-service](assets/transcript-text.png)

## Utilizzo della trascrizione in Dynamic Media {#using-transcription-in-dynamic-media}

Se hai [configurato Dynamic Media](/help/assets/dynamic-media/config-dm.md) nell’istanza di Experience Manager Assets, puoi pubblicare la risorsa (file audio o video) e la relativa trascrizione (file .vtt) in Dynamic Media. In questo modo, la risorsa originale (file audio o video) e la relativa rappresentazione trascritta (file .vtt) vengono pubblicati in Dynamic Media nella stessa cartella. L’amministratore di Dynamic Media può [abilitare l’esperienza con CC Closed Caption](/help/assets/dynamic-media/video.md#adding-captions-to-video) per il file audio o video che utilizza la rappresentazione della trascrizione (file .vtt).

Consulta anche:

* [Video tutorial su come aggiungere CC Closed Caption a un video Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=it#add-cc-closed-captioning-to-dynamic-media-video)
* [Pubblicare video Dynamic Media su YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

Nell’illustrazione seguente, la parte “caption” nell’URL fa riferimento alla trascrizione (file .vtt). Nel video, il testo parlato (testo trascritto) compare come **[!UICONTROL sottotitolo codificato]** in corrispondenza del tempo appropriato nel video. L’utente può abilitare o disabilitare i sottotitoli mediante il pulsante **[!UICONTROL CC]**.

![configure-transcription-service](assets/transcript-example.png)

## Formati di file supportati per la trascrizione {#supported-file-format}

La trascrizione supporta i seguenti formati di file audio e video:

| Formati audio/video supportati | Estensioni |
|----|----|
| FLV (con codec H.264 e AAC) | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS, MPEG2-TS, 3GP | (.ts, .ps, .3gp, .3gpp, .mpg) |
| Windows Media Video (WMV)/ASF | (.wmv, .asf) |
| AVI (non compresso 8 bit/10 bit) | (.avi) |
| MP4 | (.mp4, .m4a, .m4v) |
| Microsoft® Digital Video Recording (DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| QuickTime | (.mov) |


>[!NOTE]
>
>Le risorse (file audio o video) di tipo applicazione non sono supportate per la trascrizione.

## Limitazioni note {#known-limitations}

* La funzione di trascrizione è supportata per video di durata fino a 10 minuti.
* La lunghezza del titolo del video deve essere inferiore a 80 caratteri.
* Sono supportati file di dimensione fino a 15 GB.
* La durata massima di elaborazione supportata è di 60 minuti.
* In un account [!DNL Azure] a pagamento, puoi caricare fino a 50 filmati al minuto. Tuttavia, in un account di prova puoi caricare fino a cinque filmati al minuto.

## Suggerimenti per la risoluzione dei problemi {#troubleshooting}

Accedi al tuo account [!DNL Azure Media Services] con le stesse credenziali (quelle utilizzate per la configurazione) per verificare lo stato della richiesta. Contatta il supporto [!DNL Azure] se la richiesta non viene elaborata correttamente.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati da Assets](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
