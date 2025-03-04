---
title: Scaricare risorse da Content Hub
description: Scopri come scaricare le risorse dal portale Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 07d533962ae2922c8a467924361fdfefc5c594eb
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 9%

---

# Scaricare risorse da Content Hub {#download-assets}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Scaricare le risorse](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub ti consente di scaricare e condividere le risorse. Nell&#39;interfaccia utente di Content Hub vengono visualizzate solo le risorse approvate. Queste risorse possono includere immagini, video o qualsiasi altro contenuto digitale. Content Hub migliora l’accessibilità e l’adattabilità per una distribuzione efficace delle risorse.

Puoi scaricare una o più risorse e i relativi rendering disponibili tramite Content Hub.

Vedi [tipi di rendering disponibili in Content Hub](#types-of-renditions).

## Scaricare una risorsa e le relative rappresentazioni {#download-asset-renditions}

Per scaricare una risorsa e le relative rappresentazioni, esegui i seguenti passaggi:

1. Fai clic sulla risorsa per visualizzarne le proprietà.

1. Fai clic su ![scarica](/help/assets/assets/download-icon.svg) per avviare il processo di download. Il pannello Scarica elenca tutte le rappresentazioni di risorse disponibili.

   >[!NOTE]
   >
   * Le rappresentazioni vengono visualizzate solo se la loro visibilità è abilitata mediante l&#39;interfaccia utente [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
   * È possibile scaricare tutte le [rappresentazioni statiche, dinamiche e di ritaglio avanzato](#types-of-renditions) durante il download di una risorsa.

1. Selezionare una o più copie trasformate e fare clic su **[!UICONTROL Scarica]**.

   ![Scarica rappresentazioni di risorse singole](/help/assets/assets/download-single-asset-renditions.png)


Se stai scaricando una risorsa con licenza, seleziona **[!UICONTROL Ho letto e accettato i termini e le condizioni di cui sopra]**, quindi fai clic su **[!UICONTROL Scarica]**. Puoi anche fare clic su **[!UICONTROL termini e condizioni]** per visualizzare la licenza della risorsa. L’anteprima della licenza viene visualizzata solo se la risorsa viene approvata con l’ambiente di authoring Assets as a Cloud Service. Per ulteriori informazioni, consulta [Gestire le risorse con licenza nell’hub di contenuti](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
Gli utenti con accesso a [Dynamic Media con funzionalità Open API](/help/assets/dynamic-media-open-apis-overview.md) possono visualizzare e scaricare rappresentazioni dinamiche e con ritaglio avanzato.

## Scaricare più risorse e le relative rappresentazioni {#download-multiple-assets-renditions}

Per scaricare più risorse e le relative rappresentazioni, esegui i seguenti passaggi:

1. Seleziona le risorse e fai clic su ![scarica](/help/assets/assets/download-icon.svg) **[!UICONTROL Scarica]**. Nella schermata [!UICONTROL Scarica risorse] sono elencate tutte le risorse selezionate.
1. Fai clic su **[!UICONTROL Scarica]** per selezionare tra le varie opzioni di download per iniziare il download:

   * **Scarica [!UICONTROL Originali]**: seleziona questa opzione per scaricare le risorse selezionate nel modulo originale.
   * **Scarica [!UICONTROL Solo rappresentazioni statiche]**: seleziona questa opzione per scaricare tutte le rappresentazioni statiche disponibili delle risorse, ad eccezione delle risorse originali.
   * **Scarica [!UICONTROL Originali e rappresentazioni statiche]**: seleziona questa opzione per scaricare le rappresentazioni originali e statiche delle risorse selezionate.

     ![Scarica più rappresentazioni](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     * Le rappresentazioni vengono visualizzate solo se la loro visibilità è abilitata mediante l&#39;interfaccia utente [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
     * È possibile scaricare solo [rappresentazioni statiche](#types-of-renditions) durante il download di più risorse.

   Se una delle risorse selezionate è una risorsa con licenza, fai clic sulla licenza della risorsa nel riquadro a sinistra per visualizzarne l&#39;anteprima. In questo modo potrai selezionare **[!UICONTROL Ho letto e accettato i termini e le condizioni di cui sopra]**, quindi fai clic su **[!UICONTROL Scarica]**. L’anteprima della licenza viene visualizzata solo se la risorsa viene approvata con l’ambiente di authoring Assets as a Cloud Service. Per ulteriori informazioni, consulta [Gestire le risorse con licenza nell’hub di contenuti](/help/assets/manage-licensed-assets-on-content-hub.md).

   <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->


## Tipi di rappresentazioni {#types-of-renditions}

Le rappresentazioni delle risorse sono rappresentazioni diverse del file originale di una risorsa. Questi possono includere miniature, versioni ottimizzate per file web o mobili, con filigrana o protetti da DRM, o anche elementi dinamici come ritagli avanzati. Non devono corrispondere al tipo di file originale, ma servono a rappresentare la risorsa in vari casi d’uso.

Ulteriori informazioni su [visualizzare e gestire le copie trasformate in Experience Manager Assets](/help/assets/renditions.md).

[!DNL Experience Manager Assets] supporta i seguenti tipi di rendering:

* [Rappresentazioni statiche](/help/assets/renditions.md#static-renditions): le rappresentazioni statiche sono versioni precreate delle risorse digitali, in genere generate durante l&#39;inserimento o la modifica delle risorse. Sono ottimizzati per utilizzi e piattaforme specifici, ad esempio miniature web, formati facili da usare sui dispositivi mobili per progetti reattivi o file ad alta risoluzione per la stampa, per fornire un’esperienza semplificata e coerente.

* [Rappresentazioni dinamiche](/help/assets/renditions.md#dynamic-renditions): le rappresentazioni dinamiche sono versioni personalizzate in tempo reale delle risorse per eseguire varie azioni, ad esempio ridimensionare le immagini per diverse risoluzioni del dispositivo o ritagliarle per adattarle a varie proporzioni. Questi rendering ti consentono di offrire esperienze personalizzate e ottimizzate per requisiti più ampi. Vengono creati rendering dinamici delle risorse nell&#39;ambiente di authoring [!DNL Adobe Experience Manager Assets].

* [Ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): il ritaglio avanzato si concentra esclusivamente sulla parte essenziale di una risorsa durante il processo di ritaglio. Dynamic Media Smart Crop per sfrutta l’intelligenza artificiale fornita da Adobe Sensei per monitorare il punto di interesse, assicurando che le nostre risorse abbiano l’aspetto migliore su tutti gli schermi. Con lo smart crop di [!DNL Adobe Experience Manager] vengono visualizzate la larghezza e l&#39;altezza delle rappresentazioni di una risorsa e il titolo. Per saperne di più, visita il sito [Utilizzo di Smart Crop con AEM Assets Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  ![Tipi di rendering](/help/assets/assets/renditions-types.png)


>[!NOTE]
> 
* Per accedere in anteprima all&#39;account Dynamic Media, [crea e invia un caso di assistenza clienti Adobe](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
* I nuovi clienti onboarded nei [servizi API Dynamic Media Open](/help/assets/dynamic-media-open-apis-overview.md) devono rivedere i loro predefiniti immagine esistenti per l&#39;approvazione.



