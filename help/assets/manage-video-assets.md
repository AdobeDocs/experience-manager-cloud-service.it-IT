---
title: Gestire le risorse video
description: Caricate, visualizzate in anteprima, annotate e pubblicate le risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 7%

---


# Gestire le risorse video {#manage-video-assets}

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, è possibile utilizzando Profili di elaborazione e utilizzando l&#39;integrazione [!DNL Dynamic Media]. Senza [!DNL Dynamic Media] licenza, [!DNL Experience Manager] fornisce il supporto di base per i video, ad esempio la transcodifica mediante FFmpeg, l&#39;estrazione di miniature di anteprima per i formati di file supportati e l&#39;anteprima nell&#39;interfaccia utente per i formati supportati per la riproduzione direttamente nel browser.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera anteprime per le risorse video con l’estensione MP4. Potete visualizzare l&#39;anteprima delle rappresentazioni nell&#39;interfaccia utente [!DNL Assets].

1. Nella cartella o nelle sottocartelle delle risorse digitali, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare la risorsa, fate clic su **[!UICONTROL Crea]** nella barra degli strumenti e scegliete **[!UICONTROL File]**. In alternativa, trascinare un file nell’interfaccia utente. Per informazioni, consultate [caricare risorse](manage-digital-assets.md#uploading-assets).
1. Per visualizzare l&#39;anteprima di un video nella vista a schede, fate clic sull&#39;opzione **[!UICONTROL Riproduci]** ![Riproduci](assets/do-not-localize/play.png) nella risorsa video. Potete mettere in pausa o riprodurre il video solo nella vista a schede. Le opzioni [!UICONTROL Riproduci] e [!UICONTROL Pausa] non sono disponibili nella vista a elenco.
1. Per visualizzare l&#39;anteprima del video nella pagina dei dettagli della risorsa, selezionate **[!UICONTROL Modifica]** nella scheda. Il video viene riprodotto nel lettore video nativo del browser. Potete riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, potete includere le risorse video in una pagina Web come URL o incorporarle direttamente. Per informazioni dettagliate, consultate [pubblicare risorse per file multimediali dinamici](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodifica tramite profilo di elaborazione {#transcode-video}

[!DNL Experience Manager] come  [!DNL Cloud Service] consente di eseguire la transcodifica di base dei file video MP4 utilizzando Profili di elaborazione. La funzionalità consente non solo di caricare, ma anche di visualizzare in anteprima e ridimensionare un file video MP4.

![Crea profilo di elaborazione per la transcodifica video in  Experience Manager](assets/video-processing-profile-for-mp4.png)

*Figura: Profilo di elaborazione per la transcodifica video in  [!DNL Experience Manager].*

Se specificate solo larghezza o altezza e lasciate vuoto l’altro campo, le rappresentazioni mantengono le proporzioni. Al momento, per la transcodifica è disponibile solo il codec h264.

Per elaborare le risorse mediante un profilo di elaborazione, aggiungete un profilo a una cartella. Consultate [Utilizzare i profili di elaborazione per elaborare le risorse](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Annotazione delle risorse video {#annotate-video-assets}

1. Dalla console [!DNL Assets], selezionate **[!UICONTROL Modifica]** nella scheda delle risorse per visualizzare la pagina dei dettagli delle risorse.
1. Per riprodurre il video, fare clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fare clic su **[!UICONTROL Annota]**. Un’annotazione viene aggiunta alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, è possibile disegnare sul quadro e inserire un commento con il disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata di annotazione, fare clic su **[!UICONTROL Chiudi]**.
1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.
1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l&#39;annotazione dalla cronologia, fare clic su **[!UICONTROL Elimina]**.

## Best practice e limitazioni {#tips-limitations}

* Senza la licenza per contenuti multimediali dinamici, potete elaborare solo i file MP4 utilizzando i profili di elaborazione.
* Per la transcodifica di base tramite

>[!MORELIKETHIS]
>
>* [Documentazione](/help/assets/dynamic-media/video.md) video per contenuti multimediali dinamici.
>* [Ulteriori informazioni sull&#39;uso, i tipi e la configurazione dei profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.

