---
title: Pubblicazione rapida in AEM e Dynamic Media
description: La pubblicazione rapida nella vista Assets consente di pubblicare le risorse in AEM e Dynamic Media simultaneamente o separatamente. Puoi selezionare risorse e cartelle e scegliere di pubblicarle in Dynamic Media o AEM.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 2%

---

# Pubblicare risorse in AEM e Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Experience Manager Assets consente di pubblicare rapidamente le risorse in Experience Manager e Dynamic Media utilizzando la vista Assets. In questo modo puoi gestire le risorse e pubblicarle utilizzando la [visualizzazione Assets senza passare alla visualizzazione Amministratore](/help/assets/overview.md##persona-based-experiences).

La vista Experience Manager Assets offre la flessibilità necessaria per pubblicare le risorse in AEM, Dynamic Media o in entrambi allo stesso tempo. Puoi pubblicare le risorse durante il caricamento, la navigazione e la ricerca. Tutte queste opzioni per la pubblicazione delle risorse sono spiegate in dettaglio all’interno di questo articolo.

## Prima di iniziare {#before-you-begin}

Configura queste impostazioni per visualizzare le opzioni di pubblicazione per AEM e Dynamic Media:

* Per visualizzare le opzioni di pubblicazione per Dynamic Media, configura le seguenti impostazioni utilizzando la visualizzazione Amministratore:

   * [Crea una configurazione cloud Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Imposta la modalità di pubblicazione Dynamic Media a livello di cartella. Puoi configurare queste impostazioni anche durante la creazione della configurazione di Dynamic Media Cloud. Per sovrascrivere le impostazioni a livello di cartella, vedere [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* Per visualizzare le opzioni di pubblicazione di AEM, devi configurare l’endpoint di pubblicazione di AEM per il tuo ambiente.

## Pubblica Assets durante il caricamento {#piblish-assets-during-upload}

Puoi pubblicare le risorse in AEM e Dynamic Media durante il caricamento delle risorse in una cartella. Le opzioni di pubblicazione visualizzate dipendono dalle impostazioni della modalità di pubblicazione Dynamic Media della cartella in cui vengono caricate le risorse. La modalità di pubblicazione in Dynamic Media può essere impostata su:

* **All&#39;attivazione:** quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento.

* **Immediato:** Quando le risorse vengono caricate in questa cartella, il sistema le acquisisce in Experience Manager e fornisce immediatamente l&#39;URL/Incorpora.
* **Pubblicazione selettiva:** Assets sono pubblicati in Experience Manager o Dynamic Media a scelta per la distribuzione nel dominio pubblico.

### Modalità di pubblicazione Dynamic Media impostata su All’attivazione {#dynamic-media-publish-mode-set-to-upon-activation}

Per pubblicare le risorse durante il loro caricamento in una cartella la cui modalità di pubblicazione Dynamic Media è impostata su **All&#39;attivazione**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni di pubblicazione** viene visualizzata la **Modalità di pubblicazione DM** come **All&#39;attivazione**.
   ![Carica immagine all&#39;attivazione](/help/assets/assets/upload-uactivation.svg)
2. Seleziona **Pubblica su AEM e Dynamic Media** e fai clic su **Carica**. Le risorse vengono pubblicate contemporaneamente in AEM e Dynamic Media. Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

### Modalità di pubblicazione Dynamic Media impostata su Immediata {#dynamic-media-publish-mode-set-to-immediate}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità di pubblicazione Dynamic Media impostata su **Immediata**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni di pubblicazione** viene visualizzata la **Modalità di pubblicazione DM** come **Immediata**.
   ![immagine di caricamento file - modalità immediata](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Poiché la modalità di pubblicazione Dynamic Media è **Immediata**, le risorse caricate vengono pubblicate automaticamente in Dynamic Media quando si fa clic su **Carica**.

2. Seleziona **Pubblica su AEM** per pubblicare le risorse caricate su AEM, quindi fai clic su Carica.

   Se si seleziona **Pubblica in AEM**, le risorse vengono pubblicate in AEM e Dynamic Media, altrimenti vengono pubblicate in Dynamic Media.

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

### Modalità di pubblicazione Dynamic Media impostata su Pubblicazione selettiva {#dynamic-media-publish-mode-set-to-selective-publish}

Per pubblicare le risorse durante il caricamento in una cartella con la modalità di pubblicazione Dynamic Media impostata su **Pubblicazione selettiva**:

1. Fai clic su **Aggiungi Assets** > **Sfoglia** > **Sfoglia file** per passare alla cartella appropriata per caricare le risorse. Nella sezione **Opzioni di pubblicazione** viene visualizzata la **Modalità di pubblicazione DM** come **Pubblicazione selettiva**.
   ![carica modalità pubblicazione selettiva per immagini](/help/assets/assets/upload-selective.svg)

2. Seleziona **Pubblica in AEM**, **Pubblica in Dynamic Media** o entrambi in base alle tue esigenze e fai clic su **Carica**.

   Le risorse vengono pubblicate in AEM e Dynamic Media in base alla selezione.

   Per visualizzare lo stato di pubblicazione aggiornato per queste risorse, vedi [Verifica stato pubblicazione](#check-publish-status).

## Pubblicare le risorse utilizzando la pagina Sfoglia risorse {#publish-assets-using-asset-browse-page}

Per pubblicare le risorse tramite la pagina Sfoglia risorse:

1. Fai clic su **Assets** nella sezione **Assets Management** disponibile nel riquadro a sinistra.
2. Seleziona una o più risorse o cartelle da pubblicare e fai clic su **Pubblica**.
3. Seleziona **AEM** e fai clic su **Pubblica** per pubblicare le risorse in AEM e Dynamic Media.
   ![navigazione risorse](/help/assets/assets/browse-uactivation-immediate.svg)
Impossibile pubblicare una cartella con la modalità di pubblicazione Dynamic Media impostata su **Pubblicazione selettiva.** Tutte le altre cartelle o risorse selezionate vengono pubblicate in AEM e Dynamic Media dopo la selezione di AEM.
   ![navigazione risorse](/help/assets/assets/browse-selective123.svg)

## Pubblicare le risorse utilizzando la pagina dei risultati di ricerca {#publish-assets-using-search-results-page}

Per pubblicare le risorse utilizzando la pagina dei risultati di ricerca delle risorse:

1. Specifica i criteri nella barra di ricerca e fai clic sull’icona di ricerca per visualizzare i risultati.
2. Seleziona le risorse da pubblicare e fai clic su **Pubblica.**
3. Seleziona AEM, Dynamic Media o entrambi in base alle tue esigenze e fai clic su **Pubblica.**
   ![cerca immagine](/help/assets/assets/search-mode.svg)
L’opzione per pubblicare in Dynamic Media nella pagina dei risultati della ricerca dipende dalla modalità di pubblicazione Dynamic Media impostata sulla cartella in cui la risorsa è disponibile nell’archivio.

   >[!NOTE]
   >
   >Se selezioni una cartella e fai clic su **Pubblica** dalla pagina dei risultati della ricerca, Experience Manager Assets visualizza un&#39;opzione per pubblicare le risorse in AEM e non in Dynamic Media, indipendentemente dalle impostazioni della modalità di pubblicazione Dynamic Media per la cartella.

## Verifica stato pubblicazione {#check-publish-status}

Per verificare lo stato di pubblicazione di una risorsa o di una cartella:

1. Fai clic su **[!UICONTROL Assets]** nella sezione **[!UICONTROL Assets Management]** disponibile nel riquadro a sinistra.
2. Passare alla vista a elenco utilizzando il commutatore vista. Puoi visualizzare le proprietà delle risorse, ad esempio AEM Publish, Dynamic Media Publish, titolo, dimensione, dimensioni e così via.\
   Se una risorsa o una cartella non è pubblicata, lo stato delle colonne **Pubblicazione AEM** e **Pubblicazione Dynamic Media** viene visualizzato come **N/D.**
   ![verifica stato pubblicazione1](/help/assets/assets/check-publish-status1.png)
Se non è possibile visualizzare le colonne Pubblicazione AEM e Pubblicazione Dynamic Media nella vista a elenco:
   1. Fai clic su ![impostazioni](/help/assets/assets/settings-icon.svg) e seleziona **Pubblicazione AEM** e **Pubblicazione Dynamic Media** colonne dalla finestra di dialogo **Colonne configurabili**.
   2. Fare clic su **Conferma.** Experience Manager Assets aggiunge le colonne selezionate alla visualizzazione Elenco.

      ![verifica stato pubblicazione2](/help/assets/assets/check-publish-status2.png)

Puoi anche controllare lo stato di pubblicazione di una risorsa selezionando una risorsa e facendo clic su **Dettagli.** I dettagli sono disponibili nella sezione **Pubblica** disponibile nel riquadro di destra. La sezione **Pubblica** elenca la data in cui le risorse vengono pubblicate in Dynamic Media e AEM. Per visualizzare l’ora di pubblicazione delle risorse, passa alla vista a elenco e visualizza i relativi dettagli.

![verifica stato pubblicazione 3](/help/assets/assets/check-publish-status3.png)

## Limitazioni {#limitations}

Al momento, durante la pubblicazione di risorse in AEM e Dynamic Media, le seguenti funzionalità non sono più disponibili:

* Pubblica le risorse in AEM e Dynamic Media dalla pagina dei dettagli delle risorse.
* Visualizza gli endpoint in cui le risorse vengono pubblicate utilizzando la Pubblicazione rapida guidata.
* Aggiungi o elimina altre risorse nella Pubblicazione guidata rapida.
* Una pagina per visualizzare le risorse pubblicate.
* Possibilità di copiare o incollare l’URL di Dynamic Media a livello di risorsa (se le risorse vengono pubblicate in Dynamic Media).
* Possibilità di pubblicare riferimenti (risorse, tag e così via) durante la pubblicazione in AEM.
* Possibilità di sovrascrivere lo stato di sincronizzazione di Dynamic Media a livello di cartella.
* Possibilità di sovrascrivere la modalità di pubblicazione Dynamic Media a livello di cartella
* Gestisci pubblicazione non ancora supportato.
