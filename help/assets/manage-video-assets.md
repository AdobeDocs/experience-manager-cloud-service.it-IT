---
title: Gestire le risorse video
description: Carica, visualizza in anteprima, annota e pubblica risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Gestione risorse, Pubblicazione, Collaborazione, Video
role: Professionista
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---


# Gestire le risorse video {#manage-video-assets}

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, è possibile utilizzando Profili di elaborazione e utilizzando l’integrazione [!DNL Dynamic Media] . Senza la licenza [!DNL Dynamic Media] , [!DNL Experience Manager] fornisce il supporto di base per i video, ad esempio la transcodifica tramite FFmpeg, l’estrazione di miniature di anteprima per i formati di file supportati e l’anteprima nell’interfaccia utente per i formati supportati per la riproduzione diretta nel browser.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera le anteprime per le risorse video con l’estensione MP4. Puoi visualizzare in anteprima le rappresentazioni nell’ interfaccia utente di [!DNL Assets] .

1. Nella cartella o nelle sottocartelle delle risorse digitali, individua il percorso in cui desideri aggiungere le risorse digitali.
1. Per caricare la risorsa, fai clic su **[!UICONTROL Crea]** nella barra degli strumenti e scegli **[!UICONTROL File]**. In alternativa, trascinare un file sull’interfaccia utente. Per ulteriori informazioni, consulta [caricare le risorse](manage-digital-assets.md#uploading-assets) .
1. Per visualizzare un video in anteprima nella vista a schede, fai clic sull&#39;opzione **[!UICONTROL Play]** ![play](assets/do-not-localize/play.png) sulla risorsa video. È possibile mettere in pausa o riprodurre video solo nella vista a schede. Le opzioni [!UICONTROL Play] e [!UICONTROL Pause] non sono disponibili nella vista a elenco.
1. Per visualizzare l’anteprima del video nella pagina dei dettagli della risorsa, seleziona **[!UICONTROL Modifica]** sulla scheda . Il video viene riprodotto nel lettore video nativo del browser. È possibile riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, puoi includere le risorse video in una pagina web come URL o incorporarle direttamente. Per informazioni dettagliate, consulta [pubblicare [!DNL Dynamic Media] risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodifica utilizzando il profilo di elaborazione {#transcode-video}

[!DNL Experience Manager] as a  [!DNL Cloud Service] consente di eseguire la transcodifica di base dei file video MP4 utilizzando Profili di elaborazione. La funzionalità ti consente non solo di caricare, ma anche di visualizzare in anteprima e scalare un file video MP4.

![Crea profilo di elaborazione per la transcodifica video in  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Un profilo di elaborazione per la transcodifica video in  [!DNL Experience Manager].*

Se specifichi solo larghezza o solo altezza e lasci vuoto l’altro campo, le rappresentazioni mantengono le proporzioni. Il codec video H.264 è disponibile per la transcodifica.

Per elaborare le risorse utilizzando un profilo di elaborazione, aggiungi un profilo a una cartella. Consulta [utilizzare i profili di elaborazione per elaborare le risorse](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Annotare risorse video {#annotate-video-assets}

1. Dalla console [!DNL Assets], seleziona **[!UICONTROL Modifica]** nella scheda delle risorse per visualizzare la pagina dei dettagli delle risorse.
1. Per riprodurre il video, fai clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fai clic su **[!UICONTROL Annota]**. Viene aggiunta un’annotazione alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, potete disegnare sull&#39;area di lavoro e includere un commento nel disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata di annotazione, fare clic su **[!UICONTROL Chiudi]**.
1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.
1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fai clic su **[!UICONTROL Elimina]**.

## Best practice e limitazioni {#tips-limitations}

* Senza la licenza [!DNL Dynamic Media] è possibile elaborare solo file MP4 utilizzando i profili di elaborazione.
* Quando si transcodificano file MP4 utilizzando i Profili di elaborazione, si applicano le seguenti linee guida e limitazioni:

   * I file Apple ProRes possono transcodificare solo a una risoluzione massima di 1080p.
   * Se il file di origine ha un bitrate >200 Mbps, è possibile eseguire la transcodifica solo a una risoluzione massima di 1080p.
   * Se il framerate di origine >=60 fps allora, la dimensione massima del file di origine che è possibile utilizzare è,

      * 400 MB per transcodifica 4k.
      * 800 MB per transcodifica 1080p.
      * 8 GB per transcodifica 720p.
   * La dimensione massima del file che è possibile transcodificare in risoluzione 4k è un file MP4 da 2,55 GB con risoluzione 4k, bitrate da 12 Mbps e 23 fps.


>[!MORELIKETHIS]
>
>* [Documentazione video su Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Scopri di più sull’utilizzo, i tipi e la configurazione dei profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.

