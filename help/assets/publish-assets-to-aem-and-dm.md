---
title: Publish rapido a AEM e Dynamic Media
description: Quick Publish nella vista Assets consente di pubblicare le risorse su AEM e Dynamic Media in modo simultaneo o separato. Puoi selezionare risorse e cartelle e scegliere di pubblicarle in Dynamic Media o AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 991888d532b3396054bd04c11c7257b61c337725
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 2%

---

# Pubblicare risorse in AEM e Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets consente di pubblicare rapidamente le risorse su Experience Manager e Dynamic Media utilizzando la vista Assets. In questo modo puoi gestire le risorse e pubblicarle utilizzando la [visualizzazione Assets senza passare alla visualizzazione Amministratore](/help/assets/overview.md##persona-based-experiences).

La vista Experience Manager Assets offre la flessibilità di pubblicare le risorse in AEM o Dynamic Media, o in entrambi i casi contemporaneamente. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca. Tutte queste opzioni per la pubblicazione delle risorse sono spiegate in dettaglio all’interno di questo articolo.

## Prima di iniziare {#before-you-begin}

Configura queste impostazioni per visualizzare le opzioni di pubblicazione per AEM e Dynamic Media:

* Per visualizzare le opzioni di pubblicazione per Dynamic Media, configura le seguenti impostazioni utilizzando la visualizzazione Amministratore:

   * [Crea una configurazione di Dynamic Media Cloud](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Imposta la modalità Dynamic Media Publish a livello di cartella. Puoi configurare queste impostazioni anche durante la creazione della configurazione di Dynamic Media Cloud. Per sovrascrivere le impostazioni a livello di cartella, vedere [Configurare Publish selettivo a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Per visualizzare le opzioni di pubblicazione per l’AEM, devi configurare l’endpoint di pubblicazione AEM per il tuo ambiente.

## Publish Assets durante il caricamento {#piblish-assets-during-upload}

Puoi pubblicare le risorse in AEM e Dynamic Media durante il caricamento delle risorse in una cartella. Le opzioni di pubblicazione visualizzate dipendono dalle impostazioni della modalità di pubblicazione Dynamic Media della cartella in cui vengono caricate le risorse. La modalità di pubblicazione di Dynamic Media può essere impostata su:

* **All&#39;attivazione:** quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento.

* **Immediato:** Quando le risorse vengono caricate in questa cartella, il sistema acquisisce le risorse in Experience Manager e fornisce immediatamente l&#39;URL/Incorpora.
* **Publish selettivo:** Assets sono pubblicati su Experience Manager o Dynamic Media a scelta per la distribuzione nel dominio pubblico.

### Modalità Dynamic Media Publish impostata su All&#39;attivazione {#dynamic-media-publish-mode-set-to-upon-activation}

Per pubblicare le risorse durante il loro caricamento in una cartella con la modalità Publish di Dynamic Media impostata su **All&#39;attivazione**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni Publish** è visualizzata la **Modalità Publish DM** come **All&#39;attivazione**.
   ![Carica immagine all&#39;attivazione](/help/assets/assets/upload-uactivation.svg)
2. Seleziona **Publish per AEM e Dynamic Media** e fai clic su **Carica**. Le risorse vengono pubblicate contemporaneamente in AEM e Dynamic Media. Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato Publish](#check-publish-status).

### Modalità Dynamic Media Publish impostata su Immediata {#dynamic-media-publish-mode-set-to-immediate}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità Publish di Dynamic Media impostata su **Immediata**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni Publish** la **Modalità Publish DM** viene visualizzata come **Immediata**.
   ![immagine di caricamento file - modalità immediata](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Poiché la modalità Publish di Dynamic Media è **Immediata**, le risorse caricate vengono pubblicate automaticamente in Dynamic Media quando si fa clic su **Carica**.

2. Seleziona **Publish in AEM** per pubblicare le risorse caricate in AEM e fai clic su Carica.

   Se si seleziona **Publish in AEM**, le risorse verranno pubblicate in AEM e Dynamic Media, altrimenti verranno pubblicate in Dynamic Media.

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato Publish](#check-publish-status).

### Modalità Publish Dynamic Media impostata su Selective Publish {#dynamic-media-publish-mode-set-to-selective-publish}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità Publish di Dynamic Media impostata su **Publish selettivo**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni Publish** la **Modalità Publish DM** viene visualizzata come **Publish selettivo**.
   ![carica modalità pubblicazione selettiva per immagini](/help/assets/assets/upload-selective.svg)

2. Seleziona **da Publish a AEM**, **da Publish a Dynamic Media** o entrambi in base alle tue esigenze e fai clic su **Carica**.

   Le risorse vengono pubblicate in AEM e Dynamic Media in base alla selezione.

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato Publish](#check-publish-status).

## Publish Assets tramite la pagina Sfoglia risorse {#publish-assets-using-asset-browse-page}

Per pubblicare le risorse tramite la pagina Sfoglia risorse:

1. Fai clic su **Assets** nella sezione **Assets Management** disponibile nel riquadro a sinistra.
2. Seleziona una o più risorse o cartelle da pubblicare e fai clic su **Publish**.
3. Seleziona **AEM** e fai clic su **Publish** per pubblicare le risorse su AEM e Dynamic Media.
   ![navigazione risorse](/help/assets/assets/browse-uactivation-immediate.svg)
Impossibile pubblicare una cartella con la modalità Publish di Dynamic Media impostata su **Pubblicazione selettiva.** Tutte le altre cartelle o risorse selezionate vengono pubblicate in AEM e Dynamic Media dopo aver selezionato AEM.
   ![navigazione risorse](/help/assets/assets/browse-selective123.svg)

## pagina dei risultati della ricerca per l’utilizzo delle risorse di Publish {#publish-assets-using-search-results-page}

Per pubblicare le risorse utilizzando la pagina dei risultati di ricerca delle risorse:

1. Specifica i criteri nella barra di ricerca e fai clic sull’icona di ricerca per visualizzare i risultati.
2. Seleziona le risorse da pubblicare e fai clic su **Publish.**
3. Seleziona AEM, Dynamic Media o entrambi in base alle tue esigenze e fai clic su **Publish.**
   ![cerca immagine](/help/assets/assets/search-mode.svg)
L’opzione per pubblicare su Dynamic Media nella pagina dei risultati della ricerca dipende dalla modalità Dynamic Media Publish impostata sulla cartella in cui la risorsa è disponibile nell’archivio.

   >[!NOTE]
   >
   >Se si seleziona una cartella e si fa clic su **Publish** dalla pagina dei risultati della ricerca, in Experience Manager Assets viene visualizzata un&#39;opzione per pubblicare le risorse in AEM e non in Dynamic Media, indipendentemente dalle impostazioni della modalità Publish di Dynamic Media per la cartella.

## Verifica lo stato di Publish {#check-publish-status}

Per verificare lo stato di pubblicazione di una risorsa o di una cartella:

1. Fai clic su **[!UICONTROL Assets]** nella sezione **[!UICONTROL Assets Management]** disponibile nel riquadro a sinistra.
2. Passare alla vista a elenco utilizzando il commutatore vista. Puoi visualizzare le proprietà delle risorse, ad esempio pubblicazione AEM, Dynamic Media Publish, titolo, dimensione, dimensioni e così via.\
   Se una risorsa o una cartella non è pubblicata, lo stato delle colonne **AEM Publish** e **Dynamic Media Publish** viene visualizzato come **N/D.**
   ![verifica stato pubblicazione1](/help/assets/assets/check-publish-status1.png)
Se non è possibile visualizzare le colonne AEM Publish e Dynamic Media Publish nella vista a elenco:
   1. Fai clic su ![impostazioni](/help/assets/assets/settings-icon.svg) e seleziona **Publish** AEM e **Dynamic Media Publish** colonne dalla finestra di dialogo **Colonne configurabili**.
   2. Fare clic su **Conferma.** Experience Manager Assets aggiunge le colonne selezionate alla visualizzazione Elenco.

      ![verifica stato pubblicazione2](/help/assets/assets/check-publish-status2.png)

Puoi anche controllare lo stato di pubblicazione di una risorsa selezionando una risorsa e facendo clic su **Dettagli.** I dettagli sono disponibili nella sezione **Publish** disponibile nel riquadro di destra. La sezione **Publish** elenca la data in cui le risorse vengono pubblicate in Dynamic Media e AEM. Per visualizzare l’ora di pubblicazione delle risorse, passa alla vista a elenco e visualizza i relativi dettagli.

![verifica stato pubblicazione 3](/help/assets/assets/check-publish-status3.png)

## Limitazioni {#limitations}

Al momento, quando si pubblicano risorse su AEM e Dynamic Media, le seguenti funzionalità non sono più disponibili:

* da Publish a AEM e Dynamic Media dalla pagina dei dettagli delle risorse.
* Visualizza gli endpoint in cui le risorse vengono pubblicate utilizzando la procedura guidata Quick Publish.
* Aggiungi o elimina altre risorse nella procedura guidata Quick Publish.
* Una pagina per visualizzare le risorse pubblicate.
* Possibilità di copiare o incollare l’URL di Dynamic Media a livello di risorsa (se le risorse vengono pubblicate in Dynamic Media).
* Possibilità di pubblicare riferimenti (risorse, tag e così via) durante la pubblicazione in AEM.
* Possibilità di sovrascrivere lo stato di sincronizzazione di Dynamic Media a livello di cartella.
* Possibilità di sovrascrivere la modalità Dynamic Media Publish a livello di cartella
* Gestisci pubblicazione non ancora supportato.
