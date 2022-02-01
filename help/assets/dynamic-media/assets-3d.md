---
title: Utilizzare le risorse 3D in Dynamic Media
description: Scopri come utilizzare le risorse 3D in Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 446edfd83affb062585dca81052575b73c2e796f
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 5%

---

# Utilizzare le risorse 3D in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze immersive.

* Pubblicazione con un solo clic (utilizzando **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il visualizzatore Dimensionale interattivo di alta qualità basato su Adobe Dimension.
* Il componente 3D Media WCM consente di aggiungere facilmente risorse 3D al [!DNL Adobe Experience Manager Sites] pagine.

Non è necessaria alcuna installazione aggiuntiva per utilizzare risorse 3D in Dynamic Media.

![Scarpa in 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati di file 3D.

Vedi anche [Formati 3D supportati in Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario | Include i materiali e le texture come un’unica risorsa. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | *Sostegno solo all&#39;acquisizione; non è disponibile alcuna visualizzazione o interazione.* USDZ è un formato 3D proprietario che può essere visualizzato in modalità nativa da Safari o iOS. |

<!-- >[!NOTE]
>
>The 3D Media WCM component and 3D preview on an asset's Details page is not compatible with the latest version of Chrome (97.x). Instead, to work with 3D assets, use Firefox or Safari, or use an earlier version of Chrome (96.x). UNHIDE 2/3/22 CQDOC-18921-->

## Avvio rapido: Risorse 3D in Dynamic Media {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le risorse 3D in Dynamic Media.

Prima di lavorare con risorse 3D in Dynamic Media, assicurati che le [!DNL Experience Manager] L&#39;amministratore ha già abilitato e configurato Cloud Services Dynamic Media.

Vedi [Configurare Cloud Services Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Caricare risorse 3D**

   * [Caricare le risorse 3D da utilizzare in Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formati di file 3D supportati per il caricamento in Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gestione delle risorse 3D**

   * Organizzare e cercare risorse 3D

      * [Organizzazione delle risorse digitali](/help/assets/organize-assets.md)
      * [Cercare risorse 3D](/help/assets/search-assets.md)
   * Visualizzare risorse 3D

      * [Visualizzare e interagire con le risorse 3D](#viewing-three-d-assets)
      * [Gestire il predefinito visualizzatore dimensionale](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Utilizzare i metadati delle risorse 3D

      * [Gestione dei metadati per le risorse digitali](/help/assets/manage-digital-assets.md#editing-properties)
      * [Schemi metadati](/help/assets/metadata-schemas.md)



1. **Pubblicare risorse 3D**

   * [Pubblicare risorse statiche Dynamic Media 3D](#publishing-three-d-assets)
   * [Metodi alternativi per la pubblicazione di risorse 3D Dynamic Media utilizzando il visualizzatore dimensionale](#alternate-publish-methods)

## Informazioni sulla visualizzazione e sull’interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dalla pagina dei dettagli della risorsa e dal componente Media 3D in Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli interattivi per le telecamere che consentono di orbitare, ingrandire e scorrere la risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione pagina Dettagli risorsa dipende da diversi fattori. quali:

* Larghezza di banda per il server.
* Latenze al server
* Complessità dell&#39;immagine.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo touch mobile, sono importanti anche quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

>[!TIP]
>
>Puoi aprire il predefinito visualizzatore dimensionale nell’Editor predefiniti per visualizzatori per esercitarti a navigare su una risorsa 3D senza dover prima caricare alcun file 3D. Il predefinito visualizzatore dimensionale dispone di una risorsa 3D incorporata con cui è possibile interagire.
>
>Vedi [Gestire i predefiniti per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md).

## Visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Vedi anche [Anteprima delle risorse tramite l’interfaccia software](/help/assets/dynamic-media/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa:**

1. Assicurati di aver caricato le risorse 3D in [!DNL Experience Manager].

   Vedi [Caricare le risorse 3D da utilizzare in Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. Da [!DNL Experience Manager], sul **[!UICONTROL Navigazione]** pagina, seleziona **[!UICONTROL Risorse > File]**.
1. Vicino all’angolo superiore destro della pagina, dal **[!UICONTROL Visualizza]** elenco a discesa, seleziona **[!UICONTROL Vista a schede]**.
1. Accedi alla risorsa 3D da visualizzare.
1. Per aprire la risorsa nella pagina Dettagli, seleziona la scheda della risorsa 3D.
1. Nella pagina Dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione touch screen |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Clic a sinistra + trascinamento. | Premere un dito singolo + trascinare. |
   | **Panning della fotocamera** | Consente di scorrere la visualizzazione a sinistra, a destra, in alto o in basso. | Fai clic con il pulsante destro del mouse e trascina. | Premere due dita + trascinare. |
   | **Zoom della fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Ruota di scorrimento. | Pizzico a due dita. |
   | **Ricollegare la fotocamera** | Rientra la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole. |  |  |
   | **Modalità a tutto schermo** | Per passare alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |  |  |

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Chiudi]** per tornare alla pagina Risorse .

## Visualizzare e interagire con una risorsa 3D all’interno di un componente Media 3D {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina web si trova in **[!UICONTROL Modifica]** con una risorsa 3D non è possibile interagire. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente Media 3D.

>[!IMPORTANT]
>
>Puoi eseguire questa operazione solo dopo aver aggiunto un componente Media 3D a una pagina web e assegnato una risorsa 3D al componente. Vedi [Aggiungere il componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnare una risorsa 3D a un componente Media 3D](#assigning-a-three-d-asset-to-the-component).

Vedi anche [Anteprima delle risorse tramite l’interfaccia software](/help/assets/dynamic-media/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D all’interno di un componente File multimediali 3D:**

1. Mentre una pagina web si trova in **[!UICONTROL Modifica]** eseguire una delle operazioni seguenti:

   * Fai clic su in alto a destra nella pagina **[!UICONTROL Anteprima]** per immettere **[!UICONTROL Anteprima]** modalità.
   * Elimina `/editor.html` dall’URL della pagina nel browser.

Una risorsa 3D completamente interattiva come visualizzata in    ![Risorsa 3D visualizzata all’interno del componente Media 3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Una risorsa 3D completamente interattiva come visualizzata in **[!UICONTROL Anteprima]** modalità.

1. Quando **[!UICONTROL Anteprima]** eseguire una delle operazioni seguenti:

   | Visualizzazione | Descrizione | Azione del mouse | Azione touch screen |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Clic a sinistra + trascinamento. | Premere un dito singolo + trascinare. |
   | **Panning della fotocamera** | Consente di scorrere la visualizzazione a sinistra, a destra, in alto o in basso. | Fai clic con il pulsante destro del mouse e trascina. | Premere due dita + trascinare. |
   | **Zoom della fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Ruota di scorrimento. | Pizzico a due dita. |
   | **Ricollegare la fotocamera** | Rientra la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole. |  |  |
   | **Modalità a tutto schermo** | Per passare alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |  |  |

## Utilizzo del componente File multimediali 3D {#working-with-three-d-media-component}

Dynamic Media include un componente Media 3D di Dynamic Media che può essere utilizzato in [!DNL Experience Manager Sites] per abilitare la visualizzazione interattiva dei modelli 3D nelle pagine web.

* [Aggiungi il componente Media 3D al modello di pagina](#adding-three-d-media-component-to-page-template)
* [Aggiungere il componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurazione del componente File multimediali 3D](#configuring-the-three-d-component)
* [Assegnare una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)

## Aggiungi il componente Media 3D al modello di pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**.
1. Passa al modello di pagina in cui desideri abilitare il componente 3D e seleziona il modello.
1. Per aprire il modello, seleziona **[!UICONTROL Modifica]**.
1. Nel menu a discesa visualizzato in alto a destra della pagina, seleziona **[!UICONTROL Struttura]** se non è già attiva.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Per selezionare un’area vuota e aprire la relativa barra degli strumenti associata, selezionare l’area vuota **[!UICONTROL Contenitore di layout]** regione.
1. Nella barra degli strumenti, seleziona la **[!UICONTROL Criterio]** per aprire **[!UICONTROL Editor criteri]**.
1. In **[!UICONTROL Proprietà]** nella sezione **[!UICONTROL Componenti consentiti]** scheda , scorri fino a **[!UICONTROL Dynamic Media]**, quindi espandi l’elenco e controlla **[!UICONTROL Supporti 3D]**.
1. Tocca **[!UICONTROL Fine]** per salvare le modifiche e chiudere il **[!UICONTROL Editor criteri]**.

   Ora puoi posizionare il componente Media 3D di Dynamic Media su tutte le pagine che utilizzano questo modello.

## Aggiungere il componente Media 3D a una pagina web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzi [!DNL Experience Manager] come sistema di gestione dei contenuti web, puoi aggiungere risorse 3D alle pagine web tramite il componente Media 3D.

Vedi anche [Aggiungere risorse Dynamic Media alle pagine](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Apri [!DNL Experience Manager Sites] e seleziona la pagina web a cui desideri aggiungere il componente Dynamic Media 3D Media.
1. Per aprire la pagina nell’editor di pagine, seleziona la **[!UICONTROL Modifica]** Icona (matita). Assicurati che **[!UICONTROL Modifica]** viene selezionata vicino alla parte superiore destra della pagina.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Nella barra degli strumenti, seleziona l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, seleziona l’icona del segno più per aprire il **[!UICONTROL Componenti]** elenco.

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Trascina **[!UICONTROL Supporti 3D]** dal **[!UICONTROL Componenti]** nella posizione della pagina in cui si desidera visualizzare il visualizzatore 3D.

Ora puoi assegnare una risorsa 3D al componente.

Vedi [Assegnare una risorsa 3D al componente File multimediali 3D](#assigning-a-three-d-asset-to-the-component)

### Facoltativo - Configurazione del componente File multimediali 3D {#configuring-the-three-d-component}

1. In [!DNL Experience Manager Sites] editor di pagine, seleziona **[!UICONTROL Visualizzatore multimediale 3D]** componente precedentemente aggiunto alla pagina.
1. Per aprire la finestra di dialogo di configurazione del componente, seleziona la **[!UICONTROL Configurazione]** icona (chiave inglese).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. Nella finestra di dialogo File multimediali 3D, dall’elenco a discesa Predefinito visualizzatore , seleziona **[!UICONTROL Dimensionale]** per assegnare il predefinito visualizzatore dimensionale al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. Nell’angolo in alto a destra, seleziona il segno di spunta per salvare le modifiche.

## Assegnare una risorsa 3D al componente File multimediali 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente Media 3D a una pagina web, puoi assegnargli una risorsa 3D.

Vedi [Aggiungere il componente Media 3D a una pagina web](#adding-the-three-d-media-component-to-a-web-page).

1. In [!DNL Experience Manager Sites] editor di pagine, fai clic su **[!UICONTROL Risorse]** icona per aprire **[!UICONTROL Risorse]** nel pannello laterale.
1. Nell’elenco a discesa , seleziona **[!UICONTROL 3D]** per mostrare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cerca o scorri fino alla risorsa 3D che desideri visualizzare sulla pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale Risorse e rilasciala sul pannello **[!UICONTROL Supporti 3D]** componente precedentemente aggiunto alla pagina.

   ![Assegnare risorse 3d al componente Media 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Mentre una pagina web si trova nella [!DNL Experience Manager Sites] **[!UICONTROL Modifica]** In modalità 3D Media, il componente File multimediali 3D visualizza la risorsa 3D ma non è possibile interagire con essa. Per rendere la risorsa interattiva, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina web nell’editor di pagine con accesso completo alle funzionalità del componente Media 3D.

## Pubblicare risorse statiche Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media accetta vari formati di file 3D supportati come *contenuto statico* in Dynamic Media. Il contenuto statico consente di caricare e pubblicare risorse 3D, ma non è disponibile il supporto per *dinamico* riproduzione di immagini o immagini associate alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Media, disponi di un URL istantaneo che puoi copiare. L’URL della risorsa 3D segue la consueta struttura URL di Dynamic Media. Tuttavia, non puoi modificare alcun parametro nell’URL della risorsa, a differenza delle risorse di immagini tradizionali in Dynamic Media.

Vedi anche [Ottenere un URL per una risorsa statica](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

In **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se utilizzi [!DNL Experience Manager] come WCM, utilizza questo metodo di pubblicazione per aggiungere le risorse Dynamic Media 3D direttamente sulla tua pagina web.

Vedi anche [Pubblicare risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Vedi anche [Pubblicare pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**Per pubblicare risorse 3D statiche di Dynamic Media:**

1. Apri una risorsa 3D (formato di file GLB, OBJ o STL).
1. Nella pagina Dettagli, sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Tocca **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall’elenco a discesa a sinistra del nome del file della risorsa 3D, seleziona **[!UICONTROL Rendering]**.

   ![3d-asset-rendering](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Tocca **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), la **[!UICONTROL URL]** viene visualizzato vicino all’angolo in basso a sinistra della pagina se sono soddisfatte tutte le seguenti condizioni della risorsa 3D:
   * Il asset 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata assimilata in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Per visualizzare l’URL di produzione diretta della risorsa 3D che puoi copiare e utilizzare nelle pagine web, seleziona **[!UICONTROL URL]**.

### Metodi alternativi per la pubblicazione di risorse 3D Dynamic Media utilizzando il visualizzatore dimensionale {#alternate-publish-methods}

Utilizza i due metodi seguenti per pubblicare le risorse 3D di Dynamic Media se sei *not* utilizzo [!DNL Experience Manager] come WCM.

* **[!UICONTROL URL]** - Utilizzo **[!UICONTROL URL]** se utilizzi un sistema di gestione dei contenuti web di terze parti e desideri collegare risorse Dynamic Media 3D alle tue pagine web utilizzando il visualizzatore dimensionale.

   Vedi [Collegare gli URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorpora]** - Utilizzo **[!UICONTROL Incorpora]** per visualizzare una risorsa Dynamic Media 3D incorporata in una pagina web utilizzando il visualizzatore dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nel **[!UICONTROL Incorpora]** finestra di dialogo.

   Vedi [Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
