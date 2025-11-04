---
title: Scaricare risorse da Content Hub
description: Scopri come scaricare una o più risorse e le relative rappresentazioni dal portale Content Hub.
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: f1d036b2e114730c4cce8df8848359e854943153
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 1%

---

# Scaricare risorse da Content Hub {#download-assets}

[!DNL Content Hub] ti consente di scaricare e condividere le risorse. L&#39;interfaccia utente di [!DNL Content Hub] visualizza solo le risorse approvate. Queste risorse possono includere immagini, video o qualsiasi altro contenuto digitale. [!DNL Content Hub] migliora l&#39;accessibilità e l&#39;adattabilità per una distribuzione efficace delle risorse.

È possibile scaricare una o più risorse e le relative rappresentazioni disponibili utilizzando [!DNL Content Hub].

Visualizza i [tipi di rendering disponibili in Content Hub](#types-of-renditions).

## Scaricare una o più risorse e le relative rappresentazioni {#download-asset-renditions}

Per scaricare una o più risorse e le relative rappresentazioni, esegui i seguenti passaggi:

* Per scaricare una singola risorsa e le relative rappresentazioni:
   1. Seleziona ![scarica](/help/assets/assets/download-icon.svg) disponibile nella scheda delle risorse per visualizzare in anteprima la risorsa e le relative rappresentazioni disponibili.
   1. Seleziona le rappresentazioni disponibili e fai clic sull&#39;opzione **[!UICONTROL Scarica]** nella finestra di dialogo per scaricare le rappresentazioni selezionate come file ZIP. Se nella finestra di dialogo viene visualizzata una licenza per risorse (per risorse con licenza), accettare i termini e le condizioni di licenza e fare clic su **[!UICONTROL Scarica]**.
      ![scarica una risorsa](/help/assets/assets/download-an-asset-CH-from-asset-card.png)
In alternativa, fai clic sulla miniatura della risorsa e quindi su ![scarica](/help/assets/assets/download-icon.svg) per selezionare e visualizzare le rappresentazioni disponibili nella finestra di dialogo prima di scaricarle.

* Per scaricare più risorse e relative rappresentazioni:
   1. Seleziona le risorse, fai clic su ![scarica](/help/assets/assets/download-icon.svg) **[!UICONTROL Scarica]** e controlla l&#39;elenco delle risorse selezionate nella finestra di dialogo **[!UICONTROL Scarica risorse]**. Fai clic su ![deseleziona](/help/assets/assets/Close.svg) accanto a una risorsa per deselezionarla dall&#39;elenco.
   1. Seleziona una o più copie trasformate per scaricarle come file ZIP. Selezionando **[!UICONTROL Ritaglio avanzato]** e **[!UICONTROL Rappresentazioni statiche]** vengono scaricate tutte le rappresentazioni statiche e di ritaglio avanzato disponibili per ogni risorsa selezionata.
   1. Facoltativo: deseleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]** per scaricare le risorse selezionate e le relative rappresentazioni come una gerarchia semplice all&#39;interno di una cartella nel file zip. Per impostazione predefinita, [!DNL Content Hub] scarica le risorse selezionate e le relative rappresentazioni in cartelle separate all&#39;interno di un file zip.

      >[!NOTE]
      >
      > * Content Hub salva la selezione (**[!UICONTROL Crea una cartella separata per ogni risorsa]**) come preferenza e la conserva per i download futuri.
      > * **[!UICONTROL Crea una cartella separata per ogni risorsa]** l&#39;opzione è disponibile solo per [!DNL Content Hub] utenti autenticati. [!DNL Content Hub] consente agli utenti pubblici di scaricare risorse come risorse singole.

   1. Fai clic su **[!UICONTROL Scarica]** per scaricare le risorse selezionate e le relative rappresentazioni.
      ![scarica più risorse](/help/assets/assets/bulk-asset-download-content-hub.png)

È possibile continuare a utilizzare [!DNL Content Hub] mentre il download è in corso. Content Hub non interrompe il flusso di lavoro durante il processo di download.
![scarica più risorse](/help/assets/assets/download-assets-notification-ch.png)
Se nella finestra di dialogo **[!UICONTROL Scarica risorse]** sono visualizzate le licenze delle risorse, selezionare ciascuna licenza dal riquadro di sinistra ([!UICONTROL Documenti T&amp;C]) per visualizzare l&#39;anteprima della licenza e le risorse selezionate associate alla licenza nel riquadro centrale della finestra di dialogo. Dopo aver esaminato ogni licenza, seleziona le rappresentazioni, fai clic su **[!UICONTROL Ho letto e accettato i termini e le condizioni di cui sopra]** e seleziona **[!UICONTROL Scarica]** per scaricarle.
![scarica più risorse](/help/assets/assets/download-multiple-licensed-assets-CH.png)

>[!NOTE]
>
>* Le rappresentazioni vengono visualizzate solo se la loro visibilità è abilitata mediante l&#39;interfaccia utente [[!UICONTROL Configuration]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
>* Gli utenti con accesso a [[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md) possono visualizzare e scaricare rappresentazioni dinamiche e con ritaglio avanzato.
>* L&#39;anteprima della licenza viene visualizzata solo se la risorsa è approvata con l&#39;ambiente di authoring [!DNL Assets as a Cloud Service]. Per ulteriori informazioni, consulta [Gestire le risorse con licenza nell’hub di contenuti](/help/assets/manage-licensed-assets-on-content-hub.md).

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

Le rappresentazioni delle risorse sono rappresentazioni diverse del file originale di una risorsa. Queste rappresentazioni possono includere miniature, versioni ottimizzate per file web o mobili, con filigrana o protetti da DRM, o anche elementi dinamici come ritagli avanzati. Non devono corrispondere al tipo di file originale, ma servono a rappresentare la risorsa in vari casi d’uso.

Ulteriori informazioni su [visualizzare e gestire le rappresentazioni in [!DNL Experience Manager Assets]](/help/assets/renditions.md).

[!DNL Experience Manager Assets] supporta i seguenti tipi di rendering:

* [Rappresentazioni statiche](/help/assets/renditions.md#static-renditions): le rappresentazioni statiche sono versioni precreate delle risorse digitali, in genere generate durante l&#39;inserimento o la modifica delle risorse. Sono ottimizzati per utilizzi e piattaforme specifici, ad esempio miniature web, formati facili da usare sui dispositivi mobili per progetti reattivi o file ad alta risoluzione per la stampa, per fornire un’esperienza semplificata e coerente.

* [Rappresentazioni dinamiche](/help/assets/renditions.md#dynamic-renditions): le rappresentazioni dinamiche sono versioni personalizzate in tempo reale delle risorse per eseguire varie azioni, ad esempio ridimensionare le immagini per diverse risoluzioni del dispositivo o ritagliarle per adattarle a varie proporzioni. Questi rendering ti consentono di offrire esperienze personalizzate e ottimizzate per requisiti più ampi. Vengono creati rendering dinamici delle risorse nell&#39;ambiente di authoring [!DNL Adobe Experience Manager Assets]. Per informazioni sui passaggi necessari per abilitare le rappresentazioni dinamiche, vedere [Abilitare le rappresentazioni dinamiche](#enable-dynamic-media-renditions).

* [Ritaglio avanzato](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): il ritaglio avanzato si concentra esclusivamente sulla parte essenziale di una risorsa durante il processo di ritaglio. Il ritaglio intelligente di Dynamic Media sfrutta l’intelligenza artificiale fornita da Adobe Sensei per monitorare il punto di interesse, assicurando che le nostre risorse abbiano un aspetto ottimale su tutte le dimensioni dello schermo. Con lo smart crop di [!DNL Adobe Experience Manager] vengono visualizzate la larghezza e l&#39;altezza delle rappresentazioni di una risorsa e il titolo. Per saperne di più, visita il sito [Utilizzo di Smart Crop con AEM Assets Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  Le rappresentazioni di ritaglio avanzato vengono visualizzate e sono disponibili per il download solo se hai accesso a [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). Le rappresentazioni con ritaglio avanzato sono disponibili solo per le risorse immagine.

  ![Tipi di rendering](/help/assets/assets/renditions-types.png)

  >[!NOTE]
  > 
  > Nel pannello Download vengono visualizzate solo le rappresentazioni statiche personalizzate. Le miniature predefinite di `cq5dam.*` non vengono visualizzate in Content Hub.

### Abilita rappresentazioni dinamiche {#enable-dynamic-media-renditions}

Per abilitare le rappresentazioni dinamiche:

1. Assicurati di avere accesso a [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

   Una volta che hai accesso a Dynamic Media con funzionalità OpenAPI, tutte le risorse contrassegnate come `Approved` sono disponibili per la distribuzione pubblica tramite Dynamic Media.

1. Imposta la destinazione di approvazione [ della risorsa](/help/assets/approve-assets-content-hub.md#set-approval-target) su Content Hub per approvare le risorse solo per Content Hub.

1. Abilita l&#39;opzione **[!UICONTROL Abilita disponibilità delle rappresentazioni]** nella scheda **[!UICONTROL Rappresentazioni]** dell&#39;interfaccia utente [Configurazione](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub).

1. Salvate nuovamente i predefiniti immagine esistenti per renderli disponibili su Content Hub. È applicabile solo se hai effettuato l’onboarding in Dynamic Media con OpenAPI.

   Per salvare nuovamente i predefiniti immagine esistenti, passa alla visualizzazione Amministratore e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti immagine]**. Selezionare un predefinito, fare clic su **[!UICONTROL Modifica]** e quindi su **[!UICONTROL Salva]**.



   >[!NOTE]
   > 
   > Le rappresentazioni dinamiche sono disponibili solo per le risorse di immagini.



