---
title: Utilizzare risorse 3D in Dynamic Medie
description: Scopri come utilizzare le risorse 3D in Dynamic Medie.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 2%

---

# Utilizzare risorse 3D in Dynamic Medie {#working-with-three-d-assets-dm}

Dynamic Medie consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze coinvolgenti.

* Pubblicazione con un clic (utilizzando **[!UICONTROL Quick Publish]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il predefinito visualizzatore dimensionale interattivo di alta qualità basato su Adobe Dimension.
* Il componente WCM 3D Media consente di aggiungere facilmente risorse 3D alle pagine [!DNL Adobe Experience Manager Sites].

Non è necessaria alcuna installazione aggiuntiva per utilizzare risorse 3D in Dynamic Medie.

![Scarpa in 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Medie {#supported-three-d-file-formats-in-dm}

Dynamic Medie supporta i seguenti formati di file 3D.

Vedi anche [Formati 3D supportati in Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary | Include i materiali e le texture come un&#39;unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivio zip | model/vnd.usdz+zip | *Supporto solo per l&#39;acquisizione. Nessuna visualizzazione o interazione disponibile.* USDZ è un formato 3D proprietario che può essere visualizzato in modalità nativa da Safari o iOS. |

Il componente WCM per contenuti multimediali 3D e l’anteprima 3D nella pagina Dettagli di una risorsa non sono compatibili con la versione più recente di Chrome (97.x). Invece, per lavorare con risorse 3D, utilizza Firefox o Safari oppure una versione precedente di Chrome (96.x).

## Guida introduttiva: risorse 3D in Dynamic Medie {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a utilizzare risorse 3D in Dynamic Medie.

Prima di utilizzare risorse 3D in Dynamic Medie, assicurati che l&#39;amministratore di [!DNL Experience Manager] abbia già abilitato e configurato i Cloud Service Dynamic Medie.

Consulta [Configurare i Cloud Service Dynamic Medie](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Carica risorse 3D**

   * [Carica le risorse 3D da utilizzare in Dynamic Medie](/help/assets/add-assets.md#upload-assets)
   * [Formati di file 3D supportati per il caricamento in Dynamic Medie](#supported-three-d-file-formats-in-dm)

1. **Gestione risorse 3D**

   * Organizzare e cercare risorse 3D

      * [Organizzazione delle risorse digitali](/help/assets/organize-assets.md)
      * [Cercare risorse 3D](/help/assets/search-assets.md)

   * Visualizzare risorse 3D

      * [Visualizzare e interagire con le risorse 3D](#viewing-three-d-assets)
      * [Gestione del predefinito visualizzatore dimensionale](/help/assets/dynamic-media/managing-viewer-presets.md)

   * Utilizzare i metadati delle risorse 3D

      * [Gestire i metadati per le risorse digitali](/help/assets/manage-digital-assets.md#editing-properties)
      * [Schemi metadati](/help/assets/metadata-schemas.md)

1. **Risorse Publish 3D**

   * [Risorse Dynamic Medie 3D statiche di Publish](#publishing-three-d-assets)
   * [Metodi alternativi per la pubblicazione di risorse 3D di Dynamic Medie tramite il visualizzatore dimensionale](#alternate-publish-methods)

## Informazioni sulla visualizzazione e l’interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dall’interno della pagina dei dettagli delle risorse e dall’interno del componente 3D Media in Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli interattivi della fotocamera che consentono di ruotare, ingrandire ed eseguire la panoramica della risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione della pagina Dettagli risorsa dipende da diversi fattori. Questi fattori includono ad esempio:

* Larghezza di banda al server.
* Latenze al server
* Complessità dell’immagine.

Inoltre, le funzionalità del computer client, ad esempio una workstation, un notebook o un dispositivo touch mobile, sono anch&#39;esse importanti da considerare quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l&#39;esperienza di visualizzazione 3D interattiva più fluida e più favorevole.

>[!TIP]
>
>Potete aprire il predefinito visualizzatore dimensionale nell&#39;Editor predefiniti visualizzatore per esercitarvi a navigare in una risorsa 3D senza dover prima caricare alcun file 3D. Il predefinito visualizzatore dimensionale dispone di una risorsa 3D incorporata con cui interagire.
>
>Consulta [Gestire i predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md).

## Visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Vedi anche [Anteprima delle risorse tramite l&#39;interfaccia software](/help/assets/dynamic-media/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa:**

1. Assicurati di aver caricato risorse 3D in [!DNL Experience Manager].

   Consulta [Caricare le risorse 3D da utilizzare in Dynamic Medie](/help/assets/add-assets.md#upload-assets).

1. Da [!DNL Experience Manager], nella pagina **[!UICONTROL Navigazione]**, selezionare **[!UICONTROL Assets > File]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Visualizza]** nell&#39;angolo superiore destro della pagina selezionare **[!UICONTROL Vista a schede]**.
1. Passa a una risorsa 3D che desideri visualizzare.
1. Per aprire la risorsa nella pagina Dettagli, seleziona la scheda della risorsa 3D.
1. Nella pagina Dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Ruota fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fai clic con il pulsante destro del mouse e trascina con il mouse. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Reinserire la fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Doppia selezione. |
   | **Reimposta** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |   |   |

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Chiudi]** per tornare alla pagina Assets.

## Visualizzare e interagire con una risorsa 3D all’interno di un componente 3D Media {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina Web è in modalità **[!UICONTROL Modifica]**, non è possibile alcuna interazione con una risorsa 3D. Per rendere interattiva la risorsa, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell&#39;editor pagina con accesso completo alla funzionalità del componente multimediale 3D.

>[!IMPORTANT]
>
>Puoi eseguire questa attività solo dopo aver aggiunto un componente File multimediali 3D a una pagina web e aver assegnato una risorsa 3D al componente. Consulta [Aggiungere il componente 3D Media a una pagina Web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnare una risorsa 3D a un componente 3D Media](#assigning-a-three-d-asset-to-the-component).

Vedi anche [Anteprima delle risorse tramite l&#39;interfaccia software](/help/assets/dynamic-media/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D all&#39;interno di un componente multimediale 3D:**

1. Quando una pagina Web è in modalità **[!UICONTROL Modifica]**, eseguire una delle operazioni seguenti:

   * Nella parte superiore destra della pagina, fare clic su **[!UICONTROL Anteprima]** per accedere alla modalità **[!UICONTROL Anteprima]**.
   * Elimina `/editor.html` dall&#39;URL della pagina nel browser.

   ![risorsa 3D visualizzata nel componente 3D Media](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Una risorsa 3D completamente interattiva visualizzata in modalità **[!UICONTROL Anteprima]**.

1. In modalità **[!UICONTROL Anteprima]**, eseguire una delle operazioni seguenti:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Ruota fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fai clic con il pulsante destro del mouse e trascina con il mouse. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Reinserire la fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Doppia selezione. |
   | **Reimposta** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |   |   |

## Informazioni sull&#39;utilizzo del componente 3D Media {#working-with-three-d-media-component}

Dynamic Medie include un componente Dynamic Medie 3D Media che è possibile utilizzare in [!DNL Experience Manager Sites] per consentire la visualizzazione interattiva di modelli 3D nelle pagine Web.

* [Aggiungere il componente 3D Media al modello della pagina](#adding-three-d-media-component-to-page-template)
* [Aggiungere il componente 3D Media a una pagina web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurazione del componente 3D Media](#configuring-the-three-d-component)
* [Assegnare una risorsa 3D al componente File 3D](#assigning-a-three-d-asset-to-the-component)

## Aggiungere il componente 3D Media al modello della pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**.
1. Passa al modello della pagina in cui desideri abilitare il componente 3D e seleziona il modello.
1. Per aprire il modello, selezionare **[!UICONTROL Modifica]**.
1. Nella parte superiore destra della pagina, nel menu a discesa, selezionare la modalità **[!UICONTROL Struttura]**, se non è già attiva.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Per selezionare un&#39;area vuota e aprire la relativa barra degli strumenti, selezionare l&#39;area vuota nell&#39;area **[!UICONTROL Contenitore layout]**.
1. Sulla barra degli strumenti, selezionare l&#39;icona **[!UICONTROL Policy]** per aprire **[!UICONTROL Policy Editor]**.
1. Nella sezione **[!UICONTROL Proprietà]**, nella scheda **[!UICONTROL Componenti consentiti]**, scorri fino a **[!UICONTROL Dynamic Medie]**, quindi espandi l&#39;elenco e seleziona **[!UICONTROL File 3D]**.
1. Seleziona **[!UICONTROL Fine]** per salvare le modifiche e chiudere **[!UICONTROL Editor criteri]**.

   È ora possibile inserire il componente Dynamic Medie 3D Media in tutte le pagine che utilizzano questo modello.

## Aggiungere il componente 3D Media a una pagina web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzi [!DNL Experience Manager] come sistema di gestione dei contenuti Web, puoi aggiungere risorse 3D alle pagine Web tramite il componente 3D Media.

Vedi anche [Aggiungere risorse Dynamic Medie alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Aprire [!DNL Experience Manager Sites] e selezionare la pagina Web alla quale si desidera aggiungere il componente Dynamic Medie 3D Media.
1. Per aprire la pagina nell&#39;editor pagina, seleziona l&#39;icona **[!UICONTROL Modifica]** (matita). Assicurarsi che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra della pagina.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Sulla barra degli strumenti, seleziona l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, seleziona l&#39;icona del segno più per aprire l&#39;elenco **[!UICONTROL Componenti]**.

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Trascina il componente **[!UICONTROL File 3D]** dall&#39;elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui vuoi visualizzare il visualizzatore 3D.

Ora puoi assegnare una risorsa 3D al componente.

Consulta [Assegnare una risorsa 3D al componente 3D Media](#assigning-a-three-d-asset-to-the-component)

### Facoltativo - Configurazione del componente 3D Media {#configuring-the-three-d-component}

1. Nell&#39;editor pagina [!DNL Experience Manager Sites], selezionare il componente **[!UICONTROL Visualizzatore file multimediali 3D]** precedentemente aggiunto alla pagina.
1. Per aprire la finestra di dialogo di configurazione del componente, seleziona l&#39;icona **[!UICONTROL Configurazione]** (chiave inglese).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. Nella finestra di dialogo 3D Media, dall&#39;elenco a discesa Predefinito visualizzatore, selezionare **[!UICONTROL Dimensionale]** per assegnare il predefinito visualizzatore dimensionale al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. Nell&#39;angolo superiore destro selezionare il segno di spunta per salvare le modifiche.

## Assegnare una risorsa 3D al componente File 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente 3D Media a una pagina web, puoi assegnargli una risorsa 3D.

Consulta [Aggiungere il componente 3D Media a una pagina Web](#adding-the-three-d-media-component-to-a-web-page).

1. Nell&#39;editor di pagine [!DNL Experience Manager Sites], fai clic sull&#39;icona **[!UICONTROL Assets]** per aprire **[!UICONTROL Assets]** nel pannello laterale.
1. Nell&#39;elenco a discesa, selezionare **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cerca o scorri fino alla risorsa 3D che desideri visualizzare nella pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale di Assets e rilasciala sul componente **[!UICONTROL 3D Media]** precedentemente aggiunto alla pagina.

   ![Assegna risorsa 3d al componente 3d Media](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Quando una pagina Web è in modalità [!DNL Experience Manager Sites] **[!UICONTROL Modifica]**, il componente 3D Media visualizza la risorsa 3D ma non è possibile alcuna interazione con la risorsa. Per rendere interattiva la risorsa, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell&#39;editor pagina con accesso completo alla funzionalità del componente multimediale 3D.

## Risorse Dynamic Medie 3D statiche di Publish {#publishing-three-d-assets}

Dynamic Medie accetta vari formati di file 3D supportati come *contenuto statico* in Dynamic Medie. Contenuto statico significa che puoi caricare e pubblicare risorse 3D, ma non è disponibile il supporto per l&#39;imaging *dinamico* o la modifica delle immagini associato alla risorsa 3D. Il motivo è che Dynamic Medie Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Medie, disponi di un URL istantaneo da copiare. L’URL della risorsa 3D segue la consueta struttura URL di Dynamic Medie. Tuttavia, a differenza delle risorse di immagini tradizionali in Dynamic Medie, nell’URL della risorsa non è possibile modificare alcun parametro.

Vedi anche [Ottenere un URL per una risorsa statica](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa e a sinistra della sua data e ora viene visualizzata una piccola icona a forma di globo, per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se utilizzi [!DNL Experience Manager] come WCM, utilizza questo metodo di pubblicazione per aggiungere le risorse 3D di Dynamic Medie direttamente sulla pagina Web.

Vedi anche [risorse Publish Dynamic Medie](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Vedi anche [pagine Publish](/help/sites-cloud/authoring/sites-console/publishing-pages.md).

**Per pubblicare risorse 3D Dynamic Medie statiche:**

1. Apri una risorsa 3D (formato file GLB, OBJ o STL).
1. Nella pagina Dettagli, sulla barra degli strumenti, selezionare **[!UICONTROL Publish rapido]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Seleziona **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall&#39;elenco a discesa a sinistra del nome file della risorsa 3D, selezionare **[!UICONTROL Rappresentazioni]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Seleziona **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), il pulsante **[!UICONTROL URL]** viene visualizzato nell&#39;angolo inferiore sinistro della pagina se sono soddisfatte tutte le seguenti condizioni per le risorse 3D:
   * La risorsa 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata acquisita in Dynamic Medie Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Per visualizzare l&#39;URL di produzione diretto della risorsa 3D che puoi copiare e utilizzare nelle pagine Web, seleziona **[!UICONTROL URL]**.

### Metodi alternativi per la pubblicazione di risorse 3D di Dynamic Medie tramite il visualizzatore dimensionale {#alternate-publish-methods}

Utilizza i due metodi seguenti per pubblicare risorse Dynamic Medie 3D se *non* utilizzi [!DNL Experience Manager] come WCM.

* **[!UICONTROL URL]** - Utilizza **[!UICONTROL URL]** se utilizzi un sistema di gestione dei contenuti Web di terze parti e vuoi collegare risorse Dynamic Medie 3D alle tue pagine Web utilizzando il visualizzatore dimensionale.

  Consulta [Collegare gli URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorpora]** - Utilizza **[!UICONTROL Incorpora]** per visualizzare una risorsa 3D di Dynamic Medie incorporata in una pagina Web utilizzando il visualizzatore dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora]**.

  Vedere [Incorporare il video Dynamic Medie, il visualizzatore di immagini o il visualizzatore dimensionale in una pagina Web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
