---
title: Utilizzo di risorse 3D in Dynamic Media
seo-title: Utilizzo di risorse 3D in Dynamic Media
description: Scopri come lavorare con risorse 3D in Dynamic Media
seo-description: Scopri come lavorare con risorse 3D in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 76cd37ae35360e68cca676de8eda53dff4819b41
workflow-type: tm+mt
source-wordcount: '2264'
ht-degree: 5%

---


# Utilizzo di risorse 3D in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze coinvolgenti.

* Pubblicazione con un solo clic (tramite Pubblicazione **** rapida sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il predefinito per visualizzatori dimensionali interattivi di alta qualità basato su Adobe Dimension.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D alle pagine dei AEM Sites.

Non è necessaria alcuna installazione aggiuntiva per utilizzare risorse 3D in Dynamic Media.

![scarpa in 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes.](/help/release-notes/aem3d-release-notes.md) -->

## Formati di file 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati di file 3D:

| Estensione dei file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binario | model/gltf-binary | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Archivio ZIP con descrizione universale di Scene7 | model/vnd.usdz+zip | *Sostegno solo all&#39;ingestione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modo nativo da Safari o iOS. |

## Avvio rapido: Risorse 3D in Dynamic Media {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le risorse 3D in Dynamic Media.

Prima di lavorare con risorse 3D in Dynamic Media, accertati che il tuo amministratore AEM abbia già attivato e configurato i servizi Dynamic Media Cloud.

Consultate [Configurazione dei servizi Dynamic Media Cloud.](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

1. **Caricare risorse 3D**

   * [Caricamento delle risorse 3D per l’uso in Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formati di file 3D supportati per il caricamento in Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gestione delle risorse 3D**

   * Organizzare ed effettuare ricerche in risorse 3D

      * [Organizzazione delle risorse digitali](/help/assets/organize-assets.md)
      * [Ricerca di risorse 3D](/help/assets/search-assets.md)
   * Visualizzare risorse 3D

      * [Visualizzazione e interazione con risorse 3D](#viewing-three-d-assets)
      * [Gestione del predefinito per visualizzatori dimensionali](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Operazioni con i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse digitali](/help/assets/manage-digital-assets.md#editing-properties)
      * [Schemi metadati](/help/assets/metadata-schemas.md)



1. **Pubblicare risorse 3D**

   * [Pubblicazione di risorse statiche Dynamic Media 3D](#publishing-three-d-assets)
   * [Metodi alternativi per pubblicare risorse Dynamic Media 3D mediante il visualizzatore dimensionale](#alternate-publish-methods)

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
>See [Managing viewer presets.](/help/assets/dynamic-media/managing-viewer-presets.md)

## Visualizzazione e interazione con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Consultate anche [Anteprima delle risorse tramite l’interfaccia software.](/help/assets/dynamic-media/previewing-assets.md)

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa**

1. Assicurati di aver caricato le risorse 3D in AEM.

   Consultate [Caricamento delle risorse 3D per l’uso in Dynamic Media.](/help/assets/add-assets.md#upload-assets)

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
>Potete eseguire questa operazione solo dopo aver aggiunto un componente File multimediali 3D a una pagina Web e assegnato una risorsa 3D al componente. Consultate [Aggiunta del componente File multimediali 3D a una pagina](#adding-the-three-d-media-component-to-a-web-page) Web e [Assegnazione di una risorsa 3D a un componente File multimediali 3D.](#assigning-a-three-d-asset-to-the-component)

Consultate anche [Anteprima delle risorse tramite l’interfaccia software.](/help/assets/dynamic-media/previewing-assets.md)

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente Media 3D**

1. Mentre una pagina Web è in modalità **[!UICONTROL Modifica]** , effettuate una delle seguenti operazioni:

   * Nella parte superiore destra della pagina, fate clic su **[!UICONTROL Anteprima]** per passare alla modalità **[!UICONTROL Anteprima]** .
   * Elimina `/editor.html` dall’URL della pagina nel browser.
![Risorsa 3D visualizzata all’interno del componente](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)File multimediali 3D Una risorsa 3D completamente interattiva visualizzata in modalità **[!UICONTROL Anteprima]** .   In modalità **[!UICONTROL Anteprima]** , effettuate una delle seguenti operazioni:](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)]**

1. **Girare la fotocamera** - Orbire la vista intorno alla scena e agli oggetti 3D.]**

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
   * Utilizzo del componente File multimediali 3D {#working-with-three-d-media-component}**

## Dynamic Media include un componente Dynamic Media 3D Media che potete usare nei AEM Sites per abilitare la visualizzazione interattiva dei modelli 3D sulle pagine Web.{#working-with-three-d-media-component}

[Aggiunta del componente File multimediali 3D al modello di pagina](#adding-three-d-media-component-to-page-template)

* [Aggiunta del componente File multimediali 3D a una pagina Web](#adding-the-three-d-media-component-to-a-web-page)
* [Facoltativo - Configurazione del componente File multimediali 3D](#configuring-the-three-d-component)
   * [Assegnazione di una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)
* Aggiunta del componente File multimediali 3D al modello di pagina {#adding-three-d-media-component-to-page-template}](#assigning-a-three-d-asset-to-the-component)


## Selezionare **[!UICONTROL Strumenti > Generale > Modelli]**.

1. Individuate il modello di pagina in cui desiderate abilitare il componente 3D e selezionatelo.****
1. Toccate **[!UICONTROL Modifica]** per aprire il modello.
1. Vicino alla parte superiore destra della pagina, nel menu a discesa, selezionate **[!UICONTROL Struttura]** , se non è già attiva.
1. ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)]**

   Toccate un&#39;area vuota nell&#39;area Contenitore **[!UICONTROL di]** layout per selezionarla e aprire la barra degli strumenti associata.](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Sulla barra degli strumenti, toccate l&#39;icona **[!UICONTROL Criterio]** per aprire l&#39;Editor **** criteri.
1. Nella sezione **[!UICONTROL Proprietà]** , nella scheda Componenti **** consentiti, scorrete fino ad **[!UICONTROL Dynamic Media]**, quindi espandete l’elenco e selezionate File multimediali **** 3D.
1. Toccate **[!UICONTROL Fine]** per salvare le modifiche e chiudere l&#39;Editor **** criteri.********
1. Ora è possibile posizionare il componente Dynamic Media 3D Media su tutte le pagine che utilizzano questo modello.********

   Aggiunta del componente File multimediali 3D a una pagina Web {#adding-the-three-d-media-component-to-a-web-page}

## Se utilizzate  Adobe Experience Manager come sistema di gestione dei contenuti Web, potete aggiungere risorse 3D alle pagine Web mediante il componente File multimediali 3D.{#adding-the-three-d-media-component-to-a-web-page}

See also [Adding Dynamic Media assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Aprite i AEM Sites e selezionate la pagina Web alla quale desiderate aggiungere il componente Dynamic Media 3D Media.[](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

1. Toccate l’icona **[!UICONTROL Modifica]** (matita) per aprire la pagina nell’editor pagina. Verificate che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra nella pagina.
1. ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)]******

   ![Sulla barra degli strumenti, toccate l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Nel pannello laterale, toccate l&#39;icona del segno più per aprire l&#39;elenco **[!UICONTROL Componenti]** .

1. ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)]**

   Trascinate il componente **[!UICONTROL 3D Media]** dall’elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui desiderate visualizzare il visualizzatore 3D.](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. È ora possibile assegnare una risorsa 3D al componente.********

Consultate [Assegnazione di una risorsa 3D a un componente File multimediali 3D.](#assigning-a-three-d-asset-to-the-component)

Facoltativo - Configurazione del componente File multimediali 3D {#configuring-the-three-d-component}](#assigning-a-three-d-asset-to-the-component)

### Nell’editor della pagina AEM Sites, selezionate il componente Visualizzatore **[!UICONTROL file multimediali]** 3D che avete aggiunto in precedenza alla pagina.

1. Toccate l&#39;icona **[!UICONTROL Configurazione]** (chiave inglese) per aprire la finestra di dialogo di configurazione del componente.
1. ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)]**

   Nella finestra di dialogo File multimediali 3D, dall’elenco a discesa Predefinito visualizzatore, selezionate **[!UICONTROL Dimensionale]** per assegnare al componente il predefinito per visualizzatori dimensionali.](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)]**

   ![Nell&#39;angolo superiore destro, toccate il segno di spunta per salvare le modifiche.](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. Assegnazione di una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

## Dopo aver aggiunto un componente File multimediali 3D a una pagina Web, potete assegnarvi una risorsa 3D.{#assigning-a-three-d-asset-to-the-component}

Consultate [Aggiunta del componente File multimediali 3D a una pagina Web.](#adding-the-three-d-media-component-to-a-web-page)

Nell’Editor pagina AEM Sites, fai clic sull’icona **[!UICONTROL Risorse]** per aprire **[!UICONTROL Risorse]** nel pannello laterale.](#adding-the-three-d-media-component-to-a-web-page)

1. Nell’elenco a discesa, selezionate **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.****
1. Nel pannello laterale, cercate o scorrete fino alla risorsa 3D che desiderate visualizzare sulla pagina da modificare.****
1. Trascinate la risorsa 3D dal pannello laterale Risorse e rilasciatela sul componente File multimediali **** 3D precedentemente aggiunto alla pagina.
1. ![Assegnare risorse 3d al componente File multimediali 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)]**

   [!NOTE]](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>Mentre una pagina Web è in modalità **[!UICONTROL Modifica]** AEM Sites, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, potete usare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell’editor pagina e accedere pienamente alle funzionalità del componente File multimediali 3D.
>
>Pubblicazione di risorse statiche Dynamic Media 3D {#publishing-three-d-assets}]******

## Dynamic Media accetta una varietà di formati di file 3D supportati come contenuto ** statico in Dynamic Media. I contenuti statici consentono di caricare e pubblicare risorse 3D, ma non è supportato il riversamento *dinamico* di immagini o immagini associato alla risorsa 3D. Questo perché Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Media, potete copiare un URL immediato. L’URL per la risorsa 3D segue la consueta struttura URL di Dynamic Media. Tuttavia, non potete modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagine tradizionali in Dynamic Media.

Consultate anche [Ottenimento di un URL per una risorsa statica.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)**

Nella vista **[!UICONTROL a]** schede, una piccola icona a forma di globo appare direttamente sotto il nome di una risorsa e a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

Se utilizzate AEM come WCM, usate questo metodo di pubblicazione per aggiungere le risorse Dynamic Media 3D direttamente sulla pagina Web.************

Consultate anche [Pubblicazione di risorse Dynamic Media.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

Consultate anche [Pubblicazione di pagine.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

**Per pubblicare risorse statiche Dynamic Media 3D**

**Aprite una risorsa 3D (formato di file GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.**

1. Nella barra degli strumenti, toccate Pubblicazione **** rapida.
1. ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)]**

   Toccate **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Dall’elenco a discesa a sinistra del nome del file della risorsa 3D, toccate **[!UICONTROL Rendering]**.
1. ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)]**

   Toccate **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), il pulsante **[!UICONTROL URL]** viene visualizzato accanto all’angolo in basso a sinistra della pagina, se sono soddisfatte tutte le seguenti condizioni per la risorsa 3D:](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. La risorsa 3D è un formato supportato (GLB, OBJ, STL e USDZ).********
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.
   * ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

   Toccate **[!UICONTROL URL]** per visualizzare l&#39;URLdi produzione diretto della risorsa 3D, che potete copiare e usare sulle pagine Web.](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Metodi alternativi per pubblicare risorse Dynamic Media 3D mediante il visualizzatore dimensionale {#alternate-publish-methods}]**

### Utilizzate i due metodi seguenti per pubblicare risorse Dynamic Media 3D se *non* utilizzate AEM come WCM.

**[!UICONTROL URL]** - Utilizzate **[!UICONTROL URL]** se utilizzate un sistema di gestione dei contenuti Web di terze parti e desiderate collegare le risorse Dynamic Media 3D alle pagine Web mediante il visualizzatore dimensionale.*

* See [Linking URLs to your web application.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)]******

   **[!UICONTROL Incorpora]** - Utilizzate **[!UICONTROL Incorpora]** per visualizzare una risorsa Dynamic Media 3D incorporata in una pagina Web mediante il visualizzatore Dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. Editing of the code is not permitted in the **[!UICONTROL Embed]** dialog box.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* Consultate [Incorporamento di video, visualizzatori immagini o visualizzatori dimensionali Dynamic Media in una pagina Web.](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)]**********

   See [Embedding the Dynamic Media Video, Image viewer, or Dimensional viewer on a web page.](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)
