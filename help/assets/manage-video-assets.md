---
title: Gestire le risorse video
description: Caricare, visualizzare in anteprima, annotare e pubblicare risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 038dbc4b0febfa58f69e05f837760162210f8689
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 6%

---

# Gestire le risorse video {#manage-video-assets}

Il formato video è una parte fondamentale delle risorse digitali di un’organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzioni mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, sono possibili utilizzando Profili di elaborazione e utilizzando [!DNL Dynamic Media] integrazione. Senza [!DNL Dynamic Media] licenza, [!DNL Experience Manager] fornisce supporto di base per i video, ad esempio per la transcodifica tramite FFmpeg, l’estrazione delle miniature di anteprima per i formati di file supportati e l’anteprima nell’interfaccia utente per i formati supportati per la riproduzione diretta nel browser.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera anteprime per le risorse video con estensione MP4. Puoi visualizzare in anteprima le rappresentazioni in [!DNL Assets] dell&#39;utente.

1. Nella cartella o nelle sottocartelle delle risorse digitali, individua il percorso in cui desideri aggiungere le risorse digitali.
1. Per caricare la risorsa, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti e scegli **[!UICONTROL File]**. In alternativa, trascina un file sull’interfaccia utente. Consulta [caricare le risorse](manage-digital-assets.md#uploading-assets) per i dettagli.
1. Per visualizzare l’anteprima di un video nella vista a schede, fai clic su **[!UICONTROL Play]** ![opzione di riproduzione](assets/do-not-localize/play.png) sulla risorsa video. È possibile mettere in pausa o riprodurre il video solo nella vista a schede. Il [!UICONTROL Play] e [!UICONTROL Pausa] non sono disponibili nella vista a elenco.
1. Per visualizzare l’anteprima del video nella pagina dei dettagli della risorsa, seleziona **[!UICONTROL Modifica]** sulla scheda. Il video viene riprodotto nel lettore video nativo del browser. È possibile riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, puoi includere le risorse video in una pagina web come URL o incorporarle direttamente. Per ulteriori informazioni, consulta [pubblicare [!DNL Dynamic Media] risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Trascodifica tramite profilo di elaborazione {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] consente di eseguire la transcodifica di base dei file video MP4 utilizzando Profili di elaborazione. Questa funzionalità consente non solo di caricare ma anche di visualizzare in anteprima e ridimensionare un file video MP4.

![Creare un profilo di elaborazione per la transcodifica video in [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Profilo di elaborazione per la transcodifica video in [!DNL Experience Manager].*

Se fornisci solo la larghezza o solo l’altezza e lasci vuoto l’altro campo, le rappresentazioni manterranno le proporzioni. È disponibile il codec video H.264 per la transcodifica.

Per elaborare le risorse utilizzando un profilo di elaborazione, aggiungi un profilo a una cartella. Consulta [utilizzare i profili di elaborazione per elaborare le risorse](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Annotare risorse video {#annotate-video-assets}

Puoi aggiungere annotazioni alle risorse video. Durante l’annotazione dei video, il lettore si interrompe per consentire l’annotazione su un fotogramma. Per ulteriori informazioni, consulta [gestione delle risorse video](manage-video-assets.md).

>[!NOTE]
>
>Il formato video MXF non è ancora supportato con le annotazioni delle risorse video.

1. Dalla sezione [!DNL Assets] console, seleziona **[!UICONTROL Modifica]** nella scheda delle risorse per visualizzare la pagina dettagli risorsa.
1. Per riprodurre il video, fai clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fai clic su **[!UICONTROL Annota]**. Nel video viene aggiunta un’annotazione in corrispondenza del momento specifico (fotogramma). Durante l&#39;annotazione, è possibile disegnare sull&#39;area di lavoro e includere un commento con il disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata di annotazione, fare clic su **[!UICONTROL Chiudi]**.
1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.
1. Per visualizzarlo nella timeline, fai clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fai clic su **[!UICONTROL Elimina]**.

## Best practice e limitazioni {#tips-limitations}

* Senza [!DNL Dynamic Media] licenza, è possibile elaborare solo file MP4 utilizzando profili di elaborazione.
* Quando si transcodificano file MP4 utilizzando Profili di elaborazione, si applicano le seguenti linee guida e limitazioni:

   * I file Apple ProRes possono essere transcodificati solo con una risoluzione massima di 1080p.
   * Se il file di origine ha un bitrate > 200 Mbps, è possibile eseguire la trascodifica solo con una risoluzione massima di 1080p.
   * Se la frequenza di fotogrammi di origine è >=60 fps, la dimensione massima del file di origine utilizzabile è,

      * 400 MB per la transcodifica 4k.
      * 800 MB per la transcodifica 1080p.
      * 8 GB per transcodifica 720p.
   * La dimensione massima del file trascodificabile a una risoluzione 4k è di 2,55 GB di file MP4 con risoluzione 4k, bitrate di 12 Mbps e 23 fps.


>[!MORELIKETHIS]
>
>* [Documentazione video di Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Ulteriori informazioni su utilizzo, tipi e configurazione dei profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).

