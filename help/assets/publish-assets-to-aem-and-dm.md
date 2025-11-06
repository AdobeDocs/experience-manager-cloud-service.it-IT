---
title: Pubblicazione rapida in [!DNL AEM and Dynamic Media]
description: Pubblicazione rapida in [!DNL Assets view] consente di pubblicare risorse in [!DNL AEM and Dynamic Media] contemporaneamente o separatamente. Puoi selezionare risorse e cartelle e scegliere di pubblicare in [!DNL Dynamic Media] o [!DNL AEM].
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Pubblica Assets in [!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

[!DNL Experience Manager Assets] consente di pubblicare rapidamente le risorse in [!DNL Experience Manager] e [!DNL Dynamic Media] utilizzando [!DNL Assets view]. In questo modo potrai gestire le risorse e quindi pubblicarle utilizzando [[!DNL Assets view] senza passare a  [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences).

[!DNL Experience Manager Assets view] offre la flessibilità necessaria per pubblicare le risorse in [!DNL AEM] o [!DNL Dynamic Media], o entrambi contemporaneamente. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca. Tutte queste opzioni per la pubblicazione delle risorse sono spiegate in dettaglio all’interno di questo articolo.

## Prima di iniziare {#before-you-begin}

Configurare le impostazioni seguenti per visualizzare le opzioni di pubblicazione per [!DNL AEM and Dynamic Media]:

* Per visualizzare le opzioni di pubblicazione per [!DNL Dynamic Media], configurare le impostazioni seguenti utilizzando la visualizzazione Amministratore:

   * [Crea una [!DNL Dynamic Media] configurazione cloud](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Imposta la modalità di pubblicazione [!DNL Dynamic Media] a livello di cartella. Puoi configurare queste impostazioni anche durante la creazione della configurazione cloud di [!DNL Dynamic Media]. Per sovrascrivere le impostazioni a livello di cartella, vedere [Configurare la pubblicazione selettiva a livello di cartella in [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md).

* Per visualizzare le opzioni di pubblicazione per [!DNL AEM], è necessario configurare l&#39;endpoint di pubblicazione [!DNL AEM] per l&#39;ambiente.

## Pubblica Assets durante il caricamento {#piblish-assets-during-upload}

È possibile pubblicare le risorse in [!DNL AEM and Dynamic Media] durante il caricamento delle risorse in una cartella. Le opzioni di pubblicazione visualizzate dipendono dalle impostazioni della modalità di pubblicazione [!DNL Dynamic Media] della cartella in cui vengono caricate le risorse. La modalità di pubblicazione di [!DNL Dynamic Media] può essere impostata su:

* **[!UICONTROL All&#39;attivazione]:** Quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento.

* **[!UICONTROL Immediato]:** Quando le risorse vengono caricate in questa cartella, il sistema le acquisisce in Experience Manager e fornisce l&#39;URL/Incorpora immediatamente.
* **[!UICONTROL Pubblicazione selettiva]:** Assets sono pubblicati in [!DNL Experience Manager] o [!DNL Dynamic Media] a tua scelta per la distribuzione nel dominio pubblico.

### [!UICONTROL Modalità di pubblicazione Dynamic Media] impostata su [!UICONTROL All&#39;attivazione] {#dynamic-media-publish-mode-set-to-upon-activation}

Per pubblicare le risorse durante il caricamento in una cartella con [!DNL Dynamic Media Publish Mode] impostato su **[!UICONTROL All&#39;attivazione]**:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** > **[!UICONTROL Sfoglia]** > **[!UICONTROL Sfoglia file]** per passare alla cartella appropriata per caricare le risorse. Nella sezione **[!UICONTROL Opzioni di pubblicazione]** viene visualizzata la **[!UICONTROL Modalità di pubblicazione DM]** come **[!UICONTROL All&#39;attivazione]**.

   ![Carica immagine all&#39;attivazione](/help/assets/assets/upload-uactivation.svg)

1. Seleziona **[!UICONTROL Pubblica su AEM e Dynamic Media]** e fai clic su **[!UICONTROL Carica]**. Le risorse vengono pubblicate contemporaneamente in [!DNL AEM and Dynamic Media]. Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

### [!UICONTROL Modalità di pubblicazione Dynamic Media] impostata su [!UICONTROL Immediata] {#dynamic-media-publish-mode-set-to-immediate}

Per pubblicare le risorse durante il loro caricamento in una cartella la cui [!UICONTROL Modalità di pubblicazione Dynamic Media] è impostata su **[!UICONTROL Immediata]**:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** > **[!UICONTROL Sfoglia]** > **[!UICONTROL Sfoglia file]** per passare alla cartella appropriata per caricare le risorse. Nella sezione **[!UICONTROL Opzioni di pubblicazione]** viene visualizzata la **[!UICONTROL Modalità di pubblicazione DM]** come **[!UICONTROL Immediata]**.

   ![immagine di caricamento file - modalità immediata](/help/assets/assets/resized-image-pdf-svg-new.svg)

   Poiché la [!UICONTROL modalità di pubblicazione Dynamic Media] è **[!UICONTROL immediata]**, le risorse caricate vengono pubblicate automaticamente in [!DNL Dynamic Media] quando si fa clic su **[!UICONTROL Carica]**.

1. Seleziona **Pubblica in AEM** per pubblicare le risorse caricate in [!DNL AEM] e fai clic su **[!UICONTROL Carica]**.

   Se si seleziona **Pubblica in AEM**, le risorse verranno pubblicate in [!DNL AEM and Dynamic Media], altrimenti verranno pubblicate in [!DNL Dynamic Media].

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

### [!UICONTROL Modalità di pubblicazione Dynamic Media] impostata su [!UICONTROL Pubblicazione selettiva] {#dynamic-media-publish-mode-set-to-selective-publish}

Per pubblicare le risorse durante il caricamento in una cartella con [!UICONTROL Modalità di pubblicazione Dynamic Media] impostata su **[!UICONTROL Pubblicazione selettiva]**:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** > **[!UICONTROL Sfoglia]** > **[!UICONTROL Sfoglia file]** per passare alla cartella appropriata per caricare le risorse. Nella sezione **[!UICONTROL Opzioni di pubblicazione]** viene visualizzata la **[!UICONTROL Modalità di pubblicazione DM]** come **[!UICONTROL Pubblicazione selettiva]**.

![carica modalità pubblicazione selettiva per immagini](/help/assets/assets/upload-selective.svg)

1. Seleziona **[!UICONTROL Pubblica in AEM]**, **[!UICONTROL Pubblica in Dynamic Media]** o entrambi in base alle tue esigenze e fai clic su **Carica**.

   Le risorse vengono pubblicate in [!DNL AEM and Dynamic Media] in base alla selezione.

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

## Pubblicare le risorse utilizzando la pagina Sfoglia risorse {#publish-assets-using-asset-browse-page}

Per pubblicare le risorse tramite la pagina Sfoglia risorse:

1. Fai clic su **[!UICONTROL Assets]** nella sezione **[!UICONTROL Assets Management]** disponibile nel riquadro a sinistra.
1. Seleziona una o più risorse o cartelle da pubblicare e fai clic su **[!UICONTROL Pubblica]**.
1. Seleziona **[!UICONTROL AEM]** e fai clic su **[!UICONTROL Pubblica]** per pubblicare le risorse in [!DNL AEM and Dynamic Media].

   ![navigazione risorse](/help/assets/assets/browse-uactivation-immediate.svg)

   Impossibile pubblicare una cartella con la modalità di pubblicazione [!DNL Dynamic Media] impostata su **[!UICONTROL Pubblicazione selettiva]**. Tutte le altre cartelle o risorse selezionate vengono pubblicate in [!DNL AEM and Dynamic Media] dopo la selezione di [!DNL AEM].

   ![navigazione risorse](/help/assets/assets/browse-selective123.svg)

## Pubblicare le risorse utilizzando la pagina dei risultati di ricerca {#publish-assets-using-search-results-page}

Per pubblicare le risorse utilizzando la pagina dei risultati di ricerca delle risorse:

1. Specifica i criteri nella barra di ricerca e fai clic sull’icona di ricerca per visualizzare i risultati.
1. Seleziona le risorse da pubblicare e fai clic su **[!UICONTROL Pubblica].**
1. Seleziona [!DNL AEM, Dynamic Media] o entrambi in base alle tue esigenze e fai clic su **[!UICONTROL Pubblica]**.

   ![cerca immagine](/help/assets/assets/search-mode.svg)

   L&#39;opzione per la pubblicazione in [!DNL Dynamic Media] nella pagina dei risultati di ricerca dipende dalla modalità di pubblicazione di [!DNL Dynamic Media] impostata nella cartella in cui la risorsa è disponibile nell&#39;archivio.

   >[!NOTE]
   >
   >Se selezioni una cartella e fai clic su **[!UICONTROL Pubblica]** dalla pagina dei risultati della ricerca, [!DNL Experience Manager Assets] visualizza un&#39;opzione per pubblicare le risorse in [!DNL AEM] e non in [!DNL Dynamic Media] indipendentemente dalle impostazioni della modalità di pubblicazione di [!DNL Dynamic Media] per la cartella.

## Verifica stato pubblicazione {#check-publish-status}

Per verificare lo stato di pubblicazione di una risorsa o di una cartella:

1. Fai clic su **[!UICONTROL Assets]** nella sezione **[!UICONTROL Assets Management]** disponibile nel riquadro a sinistra.
1. Passare alla vista a elenco utilizzando il commutatore vista. Puoi visualizzare le proprietà delle risorse, ad esempio [!UICONTROL AEM publish], [!UICONTROL Dynamic Media publish], [!UICONTROL title], [!UICONTROL size], [!UICONTROL dimensioni] e così via.

   Se una risorsa o una cartella non è pubblicata, lo stato delle colonne **[!UICONTROL Pubblicazione AEM]** e **[!UICONTROL Pubblicazione Dynamic Media]** viene visualizzato come **[!UICONTROL N/A]**.

   ![controllare lo stato di pubblicazione1](/help/assets/assets/check-publish-status1.png)

   Se non è possibile visualizzare le colonne Pubblicazione [!DNL AEM] e Pubblicazione [!DNL Dynamic Media] nella visualizzazione Elenco:

   1. Fai clic su ![impostazioni](/help/assets/assets/settings-icon.svg) e seleziona **[!UICONTROL Pubblicazione AEM]** e **[!UICONTROL Pubblicazione Dynamic Media]** colonne dalla finestra di dialogo **[!UICONTROL Colonne configurabili]**.
   1. Fai clic su **[!UICONTROL Conferma]**. [!DNL Experience Manager Assets] aggiunge le colonne selezionate alla visualizzazione Elenco.

      ![verifica stato pubblicazione2](/help/assets/assets/check-publish-status2.png)

Puoi anche controllare lo stato di pubblicazione di una risorsa selezionando una risorsa e facendo clic su **[!UICONTROL Dettagli]**. I dettagli sono disponibili nella sezione **[!UICONTROL Pubblica]** disponibile nel riquadro di destra. Nella sezione **[!UICONTROL Pubblica]** è indicata la data di pubblicazione delle risorse in [!DNL Dynamic Media] e [!DNL AEM]. Per visualizzare l’ora di pubblicazione delle risorse, passa alla vista a elenco e visualizza i relativi dettagli.

![verifica stato pubblicazione 3](/help/assets/assets/check-publish-status3.png)

## Limitazioni {#limitations}

Al momento, le seguenti funzionalità non sono incluse nell&#39;ambito durante la pubblicazione di risorse in [!DNL AEM and Dynamic Media]:

* Pubblica risorse in [!DNL AEM and Dynamic Media] da [!DNL Asset details page].
* Visualizza gli endpoint in cui le risorse vengono pubblicate utilizzando la Pubblicazione rapida guidata.
* Aggiungi o elimina altre risorse nella Pubblicazione guidata rapida.
* Una pagina per visualizzare le risorse pubblicate.
* Possibilità di copiare o incollare l&#39;URL [!DNL Dynamic Media] a livello di risorsa (se le risorse sono pubblicate in [!DNL Dynamic Media]).
* Possibilità di pubblicare riferimenti (risorse, tag e così via) durante la pubblicazione in [!DNL AEM].
* Possibilità di sovrascrivere lo stato di sincronizzazione di [!DNL Dynamic Media] a livello di cartella.
* Possibilità di sovrascrivere la modalità di pubblicazione [!DNL Dynamic Media] a livello di cartella
* Gestisci pubblicazione non ancora supportato.
