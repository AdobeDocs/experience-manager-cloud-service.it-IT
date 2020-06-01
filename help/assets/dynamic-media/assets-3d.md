---
title: Utilizzo di risorse 3D in elementi multimediali dinamici
seo-title: Utilizzo di risorse 3D in elementi multimediali dinamici
description: Scopri come lavorare con risorse 3D in Dynamic Media
seo-description: Scopri come lavorare con risorse 3D in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: bc0852120580065a93923e7fe730485012afba6e
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 4%

---


# Utilizzo di risorse 3D in elementi multimediali dinamici {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze coinvolgenti.

* Pubblicazione con un solo clic (tramite Pubblicazione **** rapida sulla barra degli strumenti) di immagini 3D per generare il relativo URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il predefinito per visualizzatori dimensionali interattivi di alta qualità basato su Adobe Dimension. Il predefinito per visualizzatori include, tra l’altro, una serie di controlli per le videocamere interattive che consentono di effettuare operazioni di orbita, zoom e scorrimento.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D alle pagine AEM Sites.

Non è disponibile alcuna installazione o configurazione per l’utilizzo di risorse 3D in Contenuti multimediali dinamici.

![scarpa in 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati di file 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati di file 3D:

| Estensione dei file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binario | model/gltf-binary | Include le texture con la risorsa invece di farvi riferimento come immagini esterne. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Archivio ZIP con descrizione universale di Scene7 | model/vnd.usdz+zip | *Sostegno solo all&#39;ingestione; non è disponibile alcuna visualizzazione o interazione.* USDZ è il formato 3D proprietario di Apple che può essere visualizzato solo da Safari o iOS. |

## Avvio rapido: Risorse 3D per contenuti multimediali dinamici {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le risorse 3D in Contenuti multimediali dinamici.

Prima di usare risorse 3D in Contenuti multimediali dinamici, accertati che il tuo amministratore AEM abbia già attivato e configurato i Servizi Dynamic Media Cloud.

Consultate [Configurazione dei servizi](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)Dynamic Media Cloud.

1. **Caricare risorse 3D**

   * [Caricamento delle risorse 3D per l’utilizzo in Contenuti multimediali](/help/assets/add-assets.md#upload-assets)dinamici.
   * [Formati di file 3D supportati per il caricamento in elementi multimediali](#supported-three-d-file-formats-in-dm)dinamici.

1. **Gestione delle risorse 3D**

   * Organizzare ed effettuare ricerche in risorse 3D

      * [Organizzazione delle risorse](/help/assets/organize-assets.md)digitali.
      * [Ricerca di risorse](/help/assets/search-assets.md)3D.
   * Visualizzare risorse 3D

      * [Visualizzazione e interazione con risorse](#viewing-three-d-assets)3D.
      * [Gestione del predefinito](/help/assets/dynamic-media/managing-viewer-presets.md)per visualizzatori dimensionali.
   * Operazioni con i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse](/help/assets/manage-digital-assets.md#editing-properties)digitali.
      * [Schemi metadati](/help/assets/metadata-schemas.md).



1. **Pubblicare risorse 3D**

   * [Pubblicazione di risorse 3D per elementi multimediali dinamici](#publishing-three-d-assets)

## Visualizzazione e interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dalla pagina dei dettagli della risorsa e dal componente File multimediali 3D in Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli per telecamere interattive che consentono di orbitare, ingrandire e scorrere la risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione pagina Dettagli risorsa dipende da diversi fattori. quali:

* Larghezza di banda al server.
* Latenze al server
* Complessità dell’immagine.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo mobile touch, sono importanti anche quando si modifica la telecamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

>[!TIP]
>
>Potete aprire il predefinito per visualizzatori dimensionali nell’Editor predefinito per visualizzatori per esercitarvi a navigare in una risorsa 3D senza dover prima caricare i file 3D. Il predefinito per visualizzatori dimensionali dispone di una risorsa 3D integrata con cui potete interagire.
>
>See [Managing viewer presets](/help/assets/dynamic-media/managing-viewer-presets.md).

## Visualizzazione e interazione con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Consultate anche [Anteprima delle risorse tramite l’interfaccia](/help/assets/dynamic-media/previewing-assets.md)software.

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa**

1. Assicurati di aver caricato le risorse 3D in AEM.

   Consultate [Caricamento delle risorse 3D per l’utilizzo in Contenuti multimediali](/help/assets/add-assets.md#upload-assets)dinamici.

1. Da AEM, nella pagina **[!UICONTROL di navigazione]** , toccate **[!UICONTROL Risorse > File]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Accedi alla risorsa 3D da visualizzare.
1. Tocca la scheda della risorsa 3D per aprirla nella pagina dei dettagli della risorsa.
1. Nella pagina di visualizzazione Dettagli della risorsa 3D, effettuate una delle seguenti operazioni:

   * **Girare la fotocamera** - Orbire la vista intorno alla scena e agli oggetti 3D.
      * _Mouse_: Fare clic con il pulsante sinistro del mouse e trascinare.
      * _Touch screen_: Premere un dito singolo e trascinare.
   * **Scorrimento della telecamera** - Scorrimento della vista verso sinistra, destra, verso l&#39;alto o verso il basso.
      * _Mouse_: Fare clic con il pulsante destro del mouse e trascinare.
      * _Touch screen_: Premere due dita e trascinare.
   * **Zoom della fotocamera** - Zoom della fotocamera per spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Touch screen_: Pizzicotto a due dita.
   * **Rientra la fotocamera** - Ricentra la fotocamera in un punto della scena 3D.
      * _Mouse_: Fate doppio clic.
      * _Touch screen_: Doppio tocco.
   * **Ripristina** - Nell’angolo inferiore destro della pagina, toccate l’icona Ripristina per ripristinare il punto di destinazione della vista al centro della risorsa 3D. La funzione Reset (Reimposta) consente di spostare la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità** Schermo intero - Per passare alla modalità Schermo intero, nell’angolo inferiore destro della pagina toccate l’icona Schermo intero.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Chiudi]** per tornare alla schermata Risorse.

## Visualizzazione e interazione con una risorsa 3D all’interno di un componente Media 3D {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina Web è in modalità **[!UICONTROL Modifica]** , non è possibile interagire con una risorsa 3D. Per rendere la risorsa interattiva, potete usare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell’editor pagina e accedere pienamente alle funzionalità del componente File multimediali 3D.

>[!IMPORTANT]
>
>Potete eseguire questa operazione solo dopo aver aggiunto un componente File multimediali 3D a una pagina Web e assegnato una risorsa 3D al componente. Consultate [Aggiunta del componente File multimediali 3D a una pagina](#adding-the-three-d-media-component-to-a-web-page) Web e [Assegnazione di una risorsa 3D a un componente](#assigning-a-three-d-asset-to-the-component)File multimediali 3D.

Consultate anche [Anteprima delle risorse tramite l’interfaccia](/help/assets/dynamic-media/previewing-assets.md)software.

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente Media 3D**

1. Mentre una pagina Web è in modalità **[!UICONTROL Modifica]** , effettuate una delle seguenti operazioni:

   * Nella parte superiore destra della pagina, fate clic su **[!UICONTROL Anteprima]** per passare alla modalità **[!UICONTROL Anteprima]** .
   * Elimina `/editor.html` dall’URL della pagina nel browser.
   ![Risorsa 3D visualizzata all’interno del componente](/help/assets/dynamic-media/assets/3d-asset-in-3d-media.png)File multimediali 3D Una risorsa 3D completamente interattiva visualizzata in modalità **[!UICONTROL Anteprima]** .

1. In modalità **[!UICONTROL Anteprima]** , effettuate una delle seguenti operazioni:

   * **Girare la fotocamera** - Orbire la vista intorno alla scena e agli oggetti 3D.
      * _Mouse_: Fare clic con il pulsante sinistro del mouse e trascinare.
      * _Touch screen_: Premere un dito singolo e trascinare.
   * **Scorrimento della telecamera** - Scorrimento della vista verso sinistra, destra, verso l&#39;alto o verso il basso.
      * _Mouse_: Fare clic con il pulsante destro del mouse e trascinare.
      * _Touch screen_: Premere due dita e trascinare.
   * **Zoom della fotocamera** - Zoom della fotocamera per spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Touch screen_: Pizzicotto a due dita.
   * **Rientra la fotocamera** - Ricentra la fotocamera in un punto della scena 3D.
      * _Mouse_: Fate doppio clic.
      * _Touch screen_: Doppio tocco.
   * **Ripristina** - Nell’angolo inferiore destro della pagina, toccate l’icona Ripristina per ripristinare il punto di destinazione della vista al centro della risorsa 3D. La funzione Reset (Reimposta) consente di spostare la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità** Schermo intero - Per passare alla modalità Schermo intero, nell’angolo inferiore destro della pagina toccate l’icona Schermo intero.

## Utilizzo del componente File multimediali 3D {#working-with-three-d-media-component}

Contenuti multimediali dinamici include un componente Contenuti multimediali 3D dinamici che potete utilizzare in AEM Sites per abilitare la visualizzazione interattiva di modelli 3D nelle pagine Web.

* [Aggiunta del componente File multimediali 3D al modello di pagina](#adding-three-d-media-component-to-page-template)
* [Aggiunta del componente File multimediali 3D a una pagina Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurazione del componente File multimediali 3D](#configuring-the-three-d-component)
* [Assegnazione di una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)


## Aggiunta del componente File multimediali 3D al modello di pagina {#adding-three-d-media-component-to-page-template}

1. Selezionare **[!UICONTROL Strumenti > Generale > Modelli]**.
1. Individuate il modello di pagina in cui desiderate abilitare il componente 3D e selezionatelo.
1. Toccate **[!UICONTROL Modifica]** per aprire il modello.
1. Vicino alla parte superiore destra della pagina, nel menu a discesa, selezionate **[!UICONTROL Struttura]** , se non è già attiva.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structure.png)

1. Toccate un&#39;area vuota nell&#39;area Contenitore **[!UICONTROL di]** layout per selezionarla e aprire la barra degli strumenti associata.
1. Sulla barra degli strumenti, toccate l&#39;icona **[!UICONTROL Criterio]** per aprire l&#39;Editor **** criteri.
1. Nella sezione **[!UICONTROL Proprietà]** , nella scheda Componenti **** consentiti, scorri fino a Contenuti multimediali **** dinamici, espandi l’elenco e seleziona Contenuti multimediali **** 3D.
1. Toccate **[!UICONTROL Fine]** per salvare le modifiche e chiudere l&#39;Editor **** criteri.

   Ora puoi posizionare il componente Contenuti multimediali 3D dinamici su tutte le pagine che utilizzano questo modello.

## Aggiunta del componente File multimediali 3D a una pagina Web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzate Adobe Experience Manager come sistema di gestione dei contenuti Web, potete aggiungere risorse 3D alle pagine Web tramite il componente File multimediali 3D.

See also [Adding Dynamic Media assets to pages](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Aprite AEM Sites e selezionate la pagina Web alla quale desiderate aggiungere il componente Contenuti multimediali 3D dinamici.
1. Toccate l’icona **[!UICONTROL Modifica]** (matita) per aprire la pagina nell’editor pagina. Verificate che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra nella pagina.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edit.png)

1. Sulla barra degli strumenti, toccate l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, toccate l&#39;icona del segno più per aprire l&#39;elenco **[!UICONTROL Componenti]** .

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filter.png)

1. Trascinate il componente **[!UICONTROL 3D Media]** dall’elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui desiderate visualizzare il visualizzatore 3D.

È ora possibile assegnare una risorsa 3D al componente.

Consultate [Assegnazione di una risorsa 3D a un componente](#assigning-a-three-d-asset-to-the-component)File multimediali 3D.

### Facoltativo - Configurazione del componente File multimediali 3D {#configuring-the-three-d-component}

1. Nell’editor pagina AEM Sites, seleziona il componente Visualizzatore **[!UICONTROL multimediale]** 3D che hai aggiunto in precedenza alla pagina.
1. Toccate l&#39;icona **[!UICONTROL Configurazione]** (chiave inglese) per aprire la finestra di dialogo di configurazione del componente.

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-config.png)

1. Nella finestra di dialogo File multimediali 3D, dall’elenco a discesa Predefinito visualizzatore, selezionate **[!UICONTROL Dimensionale]** per assegnare al componente il predefinito per visualizzatori dimensionali.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-config.png)

1. Nell&#39;angolo superiore destro, toccate il segno di spunta per salvare le modifiche.

## Assegnazione di una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente File multimediali 3D a una pagina Web, potete assegnarvi una risorsa 3D.

Consultate [Aggiunta del componente File multimediali 3D a una pagina](#adding-the-three-d-media-component-to-a-web-page)Web.

1. Nell’editor pagina AEM Sites, fai clic sull’icona **[!UICONTROL Risorse]** per aprire **[!UICONTROL Risorse]** nel pannello laterale.
1. Nell’elenco a discesa, selezionate **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cercate o scorrete fino alla risorsa 3D che desiderate visualizzare sulla pagina da modificare.
1. Trascinate la risorsa 3D dal pannello laterale Risorse e rilasciatela sul componente File multimediali **** 3D precedentemente aggiunto alla pagina.

   ![Assegnare risorse 3d al componente File multimediali 3d](/help/assets/dynamic-media/assets/3d-asset-add.png)

>[!NOTE]
>
>Mentre una pagina Web è in modalità di **[!UICONTROL modifica]** di AEM Sites, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, potete usare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell’editor pagina e accedere pienamente alle funzionalità del componente File multimediali 3D.

## Publishing Dynamic Media 3D assets {#publishing-three-d-assets}

Dynamic Media accetta una serie di formati di file 3D supportati come contenuto ** statico in Dynamic Media. I contenuti statici consentono di caricare e pubblicare risorse 3D, ma non è supportato il riversamento *dinamico* di immagini o immagini associato alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Contenuti multimediali dinamici, potete copiare un URL immediato. L’URL per la risorsa 3D segue la consueta struttura URL per file multimediali dinamici. Tuttavia, non potete modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagine tradizionali negli elementi multimediali dinamici.

Nella vista **[!UICONTROL a]** schede, una piccola icona a forma di globo appare direttamente sotto il nome di una risorsa e a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Consultate anche [Pubblicazione di risorse](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)per file multimediali dinamici.

Consultate anche [Pubblicazione di pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

>[!MORELIKETHIS]
>
>Se utilizzate un sistema di gestione dei contenuti Web di terze parti, potete collegare o incorporare risorse 3D alle pagine Web.
>
>See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

**Per pubblicare risorse 3D per elementi multimediali dinamici**

1. Aprite una risorsa 3D (formato di file GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.
1. Nella barra degli strumenti, toccate Pubblicazione **** rapida.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publish.png)

1. Toccate **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall’elenco a discesa a sinistra del nome del file della risorsa 3D, toccate **[!UICONTROL Rendering]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditions.png)

1. Toccate **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), il pulsante URL viene visualizzato accanto all’angolo in basso a sinistra della pagina, se vengono soddisfatte tutte le seguenti condizioni per la risorsa 3D:
   * La risorsa 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.
   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-url.png)

1. Toccate **[!UICONTROL URL]** per visualizzare l&#39;URL di produzione della risorsa 3D.
