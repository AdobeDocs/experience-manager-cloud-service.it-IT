---
title: Pubblicazione rapida su AEM e Dynamic Medie
description: La pubblicazione rapida nella vista Assets consente di pubblicare le risorse in AEM e Dynamic Media simultaneamente o separatamente. Puoi selezionare risorse e cartelle e scegliere di pubblicarle in Dynamic Medie o AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: 1da11f59f891654f04305d2a6a3e536a6beb5e6e
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Pubblicare risorse in AEM e Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

Experience Manager Assets consente di pubblicare rapidamente le risorse su Experience Manager e Dynamic Medie utilizzando la vista Risorse. In questo modo puoi gestire le risorse e quindi pubblicarle utilizzando [Visualizzazione risorse senza passare alla visualizzazione Amministratore](/help/assets/overview.md##persona-based-experiences).

La vista Experience Manager Assets offre la flessibilità di pubblicare le risorse in AEM o Dynamic Medie, o in entrambi i casi contemporaneamente. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca. Tutte queste opzioni per la pubblicazione delle risorse sono spiegate in dettaglio all’interno di questo articolo.

## Prima di iniziare {#before-you-begin}

Configura queste impostazioni per visualizzare le opzioni di pubblicazione per AEM e Dynamic Medie:

* Per visualizzare le opzioni di pubblicazione per Dynamic Medie, configura le seguenti impostazioni utilizzando la visualizzazione Amministratore:

   * [Creare una configurazione cloud di Dynamic Medie](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Imposta la modalità di pubblicazione Dynamic Medie a livello di cartella. Puoi configurare queste impostazioni anche durante la creazione della configurazione cloud di Dynamic Medie. Per sovrascrivere tali impostazioni a livello di cartella, vedi [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Medie](/help/assets/dynamic-media/selective-publishing.md).

* Per visualizzare le opzioni di pubblicazione per AEM, devi configurare l’endpoint di pubblicazione AEM per il tuo ambiente.

## Pubblicare le risorse durante il caricamento {#piblish-assets-during-upload}

Puoi pubblicare le risorse in AEM e Dynamic Medie durante il caricamento delle risorse in una cartella. Le opzioni di pubblicazione visualizzate dipendono dalla modalità di pubblicazione di Dynamic Medie impostata sulla cartella in cui vengono caricate le risorse. La modalità di pubblicazione di Dynamic Medie può essere impostata su:

* **All&#39;attivazione:** Quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento.

* **Immediata:** Quando le risorse vengono caricate in questa cartella, il sistema acquisisce le risorse in Experience Manager e fornisce immediatamente l’URL/Incorpora.
* **Pubblicazione selettiva:** Le risorse vengono pubblicate a scelta tra Experience Manager e Dynamic Medie per la distribuzione nel dominio pubblico.

### Modalità di pubblicazione Dynamic Medie impostata su All’attivazione {#dynamic-media-publish-mode-set-to-upon-activation}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità di pubblicazione Dynamic Medie impostata su **All&#39;attivazione**:

1. Clic **Aggiungi risorse** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Il **Opzioni di pubblicazione** mostra la sezione **Modalità pubblicazione DM** as **All&#39;attivazione**.
   ![Carica immagine all&#39;attivazione](/help/assets/assets/upload-upon-activation1.png)
2. Seleziona **Pubblica su AEM e Dynamic Medie** e fai clic su **Carica**. Le risorse vengono pubblicate contemporaneamente in AEM e Dynamic Medie. Per visualizzare lo stato di pubblicazione aggiornato di queste risorse, consulta [Verifica stato pubblicazione](#check-publish-status).

### Modalità di pubblicazione Dynamic Medie impostata su Immediata {#dynamic-media-publish-mode-set-to-immediate}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità di pubblicazione Dynamic Medie impostata su **Immediato**:

1. Clic **Aggiungi risorse** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. La sezione Opzioni di pubblicazione mostra **Modalità pubblicazione DM** as **Immediato**.
   ![immagine caricamento file - modalità immediata](/help/assets/assets/upload-immediate-mode.png)
Come la modalità di pubblicazione Dynamic Medie è **Immediato**, le risorse caricate vengono pubblicate automaticamente in Dynamic Medie quando fai clic su **Carica**.

2. Seleziona Pubblica in **Pubblicazione AEM** le risorse caricate in AEM e fai clic su Carica.

   Se si seleziona **Pubblica su AEM**, le risorse vengono pubblicate in AEM e Dynamic Medie, altrimenti vengono pubblicate in Dynamic Medie.

   Per visualizzare lo stato di pubblicazione aggiornato di queste risorse, consulta [Verifica stato pubblicazione](#check-publish-status).

### Modalità di pubblicazione Dynamic Medie impostata su Pubblicazione selettiva {#dynamic-media-publish-mode-set-to-selective-publish}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità di pubblicazione Dynamic Medie impostata su **Pubblicazione selettiva**:

1. Clic **Aggiungi risorse** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. La sezione Opzioni di pubblicazione mostra **Modalità pubblicazione DM** as **Pubblicazione selettiva**.
   ![carica modalità di pubblicazione selettiva per immagini](/help/assets/assets/upload-image-selective-publish-mode.png)

2. Seleziona **Pubblica su AEM**, **Pubblica su Dynamic Medie**, o entrambi in base alle tue esigenze, e fai clic su **Carica**.

   Le risorse vengono pubblicate in AEM e Dynamic Medie in base alla selezione.

   Per visualizzare lo stato di pubblicazione aggiornato di queste risorse, consulta [Verifica stato pubblicazione](#check-publish-status).

## Pubblicare le risorse utilizzando la pagina Sfoglia risorse {#publish-assets-using-asset-browse-page}

Per pubblicare le risorse tramite la pagina Sfoglia risorse:

1. Clic **Risorse** nel **Gestione risorse** disponibile nel riquadro a sinistra.
2. Seleziona le risorse o le cartelle da pubblicare e fai clic su **Pubblica**.
3. Seleziona **AEM** e fai clic su **Pubblica** per pubblicare risorse su AEM e Dynamic Medie.
   ![navigazione risorse](/help/assets/assets/assets-browse-1.png)
Non è possibile pubblicare una cartella con la modalità di pubblicazione Dynamic Medie impostata su **Pubblicazione selettiva.** Tutte le altre cartelle o risorse selezionate vengono pubblicate in AEM e Dynamic Medie dopo aver selezionato AEM.
   ![navigazione risorse](/help/assets/assets/assets-browse-2.png)

## Pubblicare le risorse utilizzando la pagina dei risultati di ricerca {#publish-assets-using-search-results-page}

Per pubblicare le risorse utilizzando la pagina dei risultati di ricerca delle risorse:

1. Specifica i criteri nella barra di ricerca e fai clic sull’icona Ricerca per visualizzare i risultati.
2. Seleziona le risorse da pubblicare e fai clic su **Pubblica.**
3. Seleziona AEM, Dynamic Medie o entrambi in base alle tue esigenze e fai clic su **Pubblica.**
   ![cerca immagine](/help/assets/assets/search-image1.png)
L’opzione per pubblicare su Dynamic Medie nella pagina dei risultati della ricerca dipende dalla modalità di pubblicazione Dynamic Medie impostata nella cartella in cui la risorsa è disponibile nell’archivio.

   >[!NOTE]
   >
   >Se si seleziona una cartella e si fa clic su **Pubblica** dalla pagina dei risultati della ricerca, Experience Manager Assets visualizza un’opzione per pubblicare le risorse su AEM e non su Dynamic Medie, indipendentemente dalle impostazioni della modalità di pubblicazione Dynamic Medie per la cartella.

## Verifica stato pubblicazione {#check-publish-status}

Per verificare lo stato di pubblicazione di una risorsa o di una cartella:

1. Clic **[!UICONTROL Risorse]** nel **[!UICONTROL Gestione risorse]** disponibile nel riquadro a sinistra.
2. Passa alla vista a elenco utilizzando il commutatore di vista. Puoi visualizzare le proprietà delle risorse, ad esempio Pubblicazione AEM, Pubblicazione Dynamic Medie, Titolo, dimensione, dimensioni e così via.\
   Se una risorsa o una cartella non è pubblicata, lo stato di **Pubblicazione AEM** e **Pubblicazione Dynamic Medie** le colonne vengono visualizzate come **N/D.**
   ![controllare lo stato di pubblicazione1](/help/assets/assets/check-publish-status1.png)
Se non è possibile visualizzare le colonne Pubblicazione AEM e Pubblicazione Dynamic Medie nella vista a elenco:
   1. Clic ![impostazioni](/help/assets/assets/settings-icon.svg) e seleziona **Pubblicazione AEM** e **Pubblicazione Dynamic Medie** colonne da **Colonne configurabili** .
   2. Clic **Conferma.** Experience Manager Assets aggiunge le colonne selezionate alla vista Elenco.

      ![controllare lo stato di pubblicazione2](/help/assets/assets/check-publish-status2.png)

Per controllare lo stato di pubblicazione di una risorsa, seleziona una risorsa e fai clic su **Dettagli.** I dettagli sono disponibili nella **Pubblica** disponibile nel riquadro a destra. Il **Pubblica** In questa sezione viene elencata la data di pubblicazione delle risorse in Dynamic Medie e AEM. Per visualizzare l’ora di pubblicazione delle risorse, passa alla vista a elenco e visualizza i relativi dettagli.

![controllare lo stato di pubblicazione 3](/help/assets/assets/check-publish-status3.png)

## Limitazioni {#limitations}

Al momento, quando si pubblicano risorse su AEM e Dynamic Medie, le seguenti funzionalità non sono più disponibili:

* Pubblica le risorse su AEM e Dynamic Medie dalla pagina dei dettagli delle risorse.
* Visualizza gli endpoint in cui le risorse vengono pubblicate utilizzando la Pubblicazione rapida guidata.
* Aggiungi o elimina altre risorse nella Pubblicazione guidata rapida.
* Una pagina per visualizzare le risorse pubblicate.
* Possibilità di copiare o incollare l’URL di Dynamic Medie a livello di risorsa (se le risorse vengono pubblicate in Dynamic Medie).
* Possibilità di pubblicare riferimenti (risorse, tag e così via) durante la pubblicazione in AEM.
* Possibilità di sovrascrivere lo stato di sincronizzazione di Dynamic Medie a livello di cartella.
* Possibilità di sovrascrivere la modalità di pubblicazione Dynamic Medie a livello di cartella
* Gestisci pubblicazione non ancora supportato.
