---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Come aggiungere componenti Dynamic Media a una pagina in Adobe Experience Manager come Cloud Service.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: cf607bd27463f23de29d0d6770940a01f3e36c87
workflow-type: tm+mt
source-wordcount: '3082'
ht-degree: 21%

---


# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi inserire direttamente nella pagina il componente **Dynamic Media**, **File multimediali interattivi**, **Elemento multimediale panoramico** o **File multimediali video 360**. Accedete alla modalità Layout e attivate i componenti Dynamic Media. Quindi aggiungete questi componenti alla pagina e aggiungete le risorse al componente. I componenti Dynamic Media sono intelligenti: rilevano l’aggiunta di un’immagine o di un video, dunque le opzioni di configurazione disponibili cambiano di conseguenza.

Potete aggiungere risorse Dynamic Media direttamente alla pagina se utilizzate  Experience Manager come WCM. Se utilizzate una terza parte per WCM, [collegare](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [incorporare](/help/assets/dynamic-media/embed-code.md) le risorse. Per un sito Web reattivo di terze parti, consultate [Distribuzione di immagini ottimizzate in un sito reattivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Assicuratevi di pubblicare le risorse prima di aggiungerle alle pagine  Experience Manager. Consultate [Pubblicazione di Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Aggiunta di un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

L’aggiunta a una pagina di un componente di supporto 3D, Dynamic Media, Interactive Media, Panoramic Media, Smart Crop Video o Video 360 equivale all’aggiunta di un componente a qualsiasi pagina.

**Aggiunta di un componente Dynamic Media a una pagina**

1. In  Experience Manager, aprite la pagina in cui desiderate aggiungere il componente Dynamic Media.
1. Nel riquadro a sinistra, toccare l&#39;icona **[!UICONTROL Componenti]**, quindi filtrare per Dynamic Media.

   Se non è disponibile alcun elenco di componenti Dynamic Media, è probabile che sia necessario abilitare i componenti Dynamic Media da utilizzare. Vedere [Abilitazione di componenti Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Trascinate un componente **[!UICONTROL Dynamic Media]** e rilasciatelo nella posizione desiderata sulla pagina.

1. Passate il puntatore direttamente sul componente. Quando il componente è circondato da una casella blu, toccate una volta per visualizzare la barra degli strumenti del componente. Toccate l&#39;icona **[!UICONTROL Configurazione (chiave inglese)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. A seconda del componente Dynamic Media rilasciato sulla pagina, si apre una finestra di dialogo di configurazione. [Impostate le ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) opzioni del componente secondo necessità.

   L&#39;esempio seguente mostra la finestra di dialogo del componente Dynamic Media **[!UICONTROL Video 360 Media]** e le opzioni disponibili nell&#39;elenco a discesa Predefinito visualizzatore.

   ![Video 360 Media component](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Il componente Dynamic Media Video 360 Media.

1. Al termine, nell’angolo superiore destro della finestra di dialogo toccate il segno di spunta per salvare le modifiche.

### Abilitazione dei componenti Dynamic Media {#enabling-dynamic-media-components}

Se non è disponibile alcun componente Dynamic Media da aggiungere a una pagina, è probabile che sia necessario abilitare i componenti che si desidera utilizzare.

1. In  Experience Manager, aprite la pagina in cui desiderate aggiungere il componente Dynamic Media.
1. A sinistra della barra degli strumenti accanto alla parte superiore della pagina, toccate l&#39;icona Informazioni pagina, quindi toccate **[!UICONTROL Modifica modello]** dall&#39;elenco a discesa.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. Sul lato destro della barra degli strumenti accanto alla parte superiore della pagina, toccate **[!UICONTROL Struttura]** dall&#39;elenco a discesa.

   ![Criterio](/help/assets/assets-dm/structure-mode.png)

1. Nella parte inferiore della pagina, toccare **[!UICONTROL Contenitore di layout]** per aprire la barra degli strumenti, quindi toccare l&#39;icona Criterio.
1. Nella pagina **[!UICONTROL Contenitore di layout]**, sotto l&#39;intestazione **[!UICONTROL Proprietà]**, assicurarsi che la scheda **[!UICONTROL Componenti consentiti]** sia selezionata.

   ![Componenti consentiti](/help/assets/assets-dm/allowed-components.png)

1. Scorrete fino a visualizzare **[!UICONTROL Dynamic Media]**.
1. Toccate l&#39;icona > a sinistra di **[!UICONTROL Dynamic Media]**, quindi selezionate i componenti Dynamic Media da abilitare.

   ![Elenco dei componenti Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Contenitore di layout]**, toccate l&#39;icona Fine (segno di spunta).

1. Sul lato destro della barra degli strumenti accanto alla parte superiore della pagina, toccate **[!UICONTROL Contenuto iniziale]** dall&#39;elenco a discesa.
1. [Aggiungere un componente Dynamic Media a una ](#adding-a-dynamic-media-component-to-a-page) pagina come al solito.

## Localizzazione dei componenti Dynamic Media {#localizing-dynamic-media-components}

Potete localizzare i componenti Dynamic Media in uno dei due modi seguenti:

* In una pagina web di Sites, apri **[!UICONTROL Proprietà]** e seleziona la scheda **[!UICONTROL Avanzate]**. Scegli la lingua desiderata per la localizzazione.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Dal selettore del sito, selezionate la pagina o il gruppo di pagine desiderato. Toccare **[!UICONTROL Properties]** e selezionare la scheda **[!UICONTROL Advanced]**. Scegli la lingua desiderata per la localizzazione.

   >[!NOTE]
   >
   >Non tutte le lingue disponibili nel menu **[!UICONTROL Lingua]** dispongono attualmente di token.

## Componenti Dynamic Media disponibili {#dynamic-media-components}

I componenti Dynamic Media sono disponibili quando si tocca l&#39;icona **[!UICONTROL Componenti]**, quindi si applica il filtro su **[!UICONTROL Dynamic Media]**.

I componenti Dynamic Media disponibili includono:

* **[!UICONTROL Dynamic Media]**: da utilizzare per risorse quali immagini, video, eCatalog e set 360 gradi.
* **[!UICONTROL Contenuti multimediali]**  interattivi: da usare per qualsiasi risorsa interattiva, ad esempio video interattivi, immagini interattive o set di caroselli.
* **[!UICONTROL Supporti]**  panoramici - Utilizzati per immagini panoramiche o risorse di immagini VR panoramiche.
* **[!UICONTROL Video 360 Media]**  - Utilizzate per risorse video 360 e 360 VR.

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere resi disponibili dall’editor modelli prima di utilizzarli. Una volta resi disponibili nell’editor modelli, potete aggiungere i componenti alla pagina come qualsiasi altro componente di Experience Manager .

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

Il componente Dynamic Media è avanzato. A seconda se aggiungete un’immagine o un video, avete a disposizione diverse opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Più istanze del componente Dynamic Media in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito per visualizzatori diverso a ciascun componente Dynamic Media in quella pagina non è supportata.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti Dynamic Media che utilizzano risorse dello stesso tipo, all’interno della pagina.

Quando aggiungi il Componente elementi multimediali dinamici e le **[!UICONTROL Impostazioni elemento multimediale dinamico]** sono vuote o non è possibile aggiungere correttamente una risorsa, controlla quanto segue:

* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell&#39;abilitazione di Dynamic Media non dispongono di un file TIFF piramidale.

#### Quando si lavora con le immagini {#when-working-with-images}

Il componente elementi multimediali dinamici consente di aggiungere immagini dinamiche, compresi set di immagini, set di rotazione e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere l’immagine reattiva, potete impostare i punti di interruzione o applicare un predefinito per immagini reattivo.

Per modificare le seguenti impostazioni Dynamic Media, toccate l&#39;icona **[!UICONTROL Modifica]** nel componente, quindi **[!UICONTROL Dynamic Media Settings]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]**.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un predefinito esistente dall’elenco a discesa. Se il predefinito per visualizzatori ricercato non è visibile, dovete renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. Non potete selezionare un predefinito per visualizzatori se usate un predefinito per immagini e viceversa.

   Questa opzione è l’unica disponibile per la visualizzazione di set di immagini, set 360 gradi o set di file multimediali diversi. I predefiniti per visualizzatori visualizzati sono anche predefiniti per visualizzatori rilevanti solo per gli elementi avanzati.

* **[!UICONTROL Modificatori]** visualizzatore - I modificatori visualizzatore assumono la forma di coppia nome=valore con un carattere di delimitazione &amp; e consentono di modificare i visualizzatori come indicato nella guida di riferimento dei visualizzatori. Un esempio di modificatore di visualizzatore è `posterimage=img.jpg&caption=text.vtt,1` che imposta un’immagine diversa per la miniatura del video e associa un file di sottotitoli/sottotitoli codificati al video.

* **[!UICONTROL Predefinito]** immagine - Selezionate un predefinito per immagini esistente dall’elenco a discesa. Se il predefinito per immagini ricercato non è visibile, dovete renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non potete selezionare un predefinito per visualizzatori se usate un predefinito per immagini e viceversa.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Modificatori]** immagini - Potete applicare effetti immagine fornendo ulteriori comandi immagine. Questi comandi sono descritti nei predefiniti per immagini e nel riferimento al comando Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Punti di interruzione]**: se utilizzi questa risorsa in un sito reattivo, devi aggiungere i punti di interruzione immagine. I punti di interruzione delle immagini devono essere separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Per modificare le seguenti impostazioni avanzate, tocca **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Titolo]** (Title) - Consente di modificare il titolo dell&#39;immagine.

* **[!UICONTROL Testo]** Alt (Alt Text) - Aggiungete un titolo all&#39;immagine per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** (Open in) - Potete impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** (Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** (Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.


#### Quando esegui operazioni con i Video {#when-working-with-video}

Usate il componente Dynamic Media per aggiungere video dinamici alle pagine Web. Quando modificate il componente, potete scegliere di usare un predefinito per visualizzatori video predefinito per riprodurre il video sulla pagina.

![chlimage_1-173](assets/chlimage_1-540.png)

Per modificare le seguenti impostazioni Dynamic Media, fai clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se si desidera impostarne una dimensione fissa, impostarla nel componente con la scheda **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nella scheda **[!UICONTROL Avanzate]**.

* **[!UICONTROL Predefinito]** visualizzatore: selezionate un predefinito per visualizzatori video esistente dall’elenco a discesa. Se il predefinito per visualizzatori ricercato non è visibile, dovete renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Modificatori]** visualizzatore - I modificatori del visualizzatore hanno la forma di una  `name=value` coppia di  `&` delimitatori. Consentono di modificare i visualizzatori come indicato nella guida di riferimento visualizzatori di Adobi . Un esempio di modificatore visualizzatore è `posterimage=img.jpg&caption=text.vtt,1`

   I modificatori del visualizzatore consentono, ad esempio, di effettuare le seguenti operazioni:

   * Associare un file di sottotitoli a un video: [caption](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associare un file di navigazione a un video: [navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Per modificare le seguenti impostazioni avanzate, fai clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Titolo]** (Title) - Consente di modificare il titolo del video.

* **[!UICONTROL Larghezza]** (Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** (Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

#### Durante l&#39;utilizzo di SmartCrop {#when-working-with-smart-crop}

Usate il componente Dynamic Media per aggiungere le risorse di immagine SmartCrop alle pagine Web. Quando modificate il componente, potete scegliere di usare un predefinito per visualizzatori video predefinito per riprodurre il video sulla pagina.

Vedere [Utilizzo di Smart Crop con risorse di Experience Manager  Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

Vedere anche [Profili immagine](/help/assets/dynamic-media/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

Per modificare la seguente impostazione Dynamic Media, fai clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]**.

* **[!UICONTROL Modificatori]** immagini - Potete applicare effetti immagine fornendo ulteriori comandi immagine. Questi comandi sono descritti nei predefiniti per immagini e nel riferimento al comando Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Per modificare le seguenti impostazioni avanzate, fai clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Abilita corrispondenza]** proporzioni: per consentire ad Dynamic Media di selezionare una rappresentazione di ritaglio avanzato con proporzioni che meglio corrispondono alle proporzioni dell&#39;immagine originale, selezionate questa opzione.

* **[!UICONTROL Titolo]** (Title) - Consente di modificare il titolo dell&#39;immagine SmartCrop.

* **[!UICONTROL Testo]** Alt (Alt Text) - Aggiungete un titolo all&#39;immagine di ritaglio avanzato per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** (Open in) - Potete impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** (Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** (Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

### Componente: Supporto interattivo {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente Contenuti multimediali interattivi è avanzato. A seconda se aggiungete un’immagine o un video, avete a disposizione diverse opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Più istanze del componente Supporto interattivo in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito per visualizzatori diverso a ciascun componente per contenuti multimediali interattivi in quella pagina non è supportata.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti per contenuti multimediali interattivi che utilizzano risorse dello stesso tipo, all’interno della pagina.

![chlimage_1-174](assets/chlimage_1-541.png)

Per modificare le seguenti impostazioni **[!UICONTROL Generale]**, toccate **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un predefinito esistente dall’elenco a discesa. Se il predefinito per visualizzatori ricercato non è visibile, dovete renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Titolo]** (Title) - Consente di modificare il titolo del video.

* **[!UICONTROL Larghezza]** (Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** (Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

   È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Mostra risorsa]** prodotto: per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

* **[!UICONTROL Mostra prezzo]** prodotto: per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

* **[!UICONTROL Mostra modulo]** prodotto - Per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.

### Componente: Supporti panoramici {#panoramic-media-component}

Il componente Contenuti multimediali panoramici è destinato alle risorse che sono immagini panoramiche sferiche. Tali immagini forniscono un&#39;esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio. Affinché un’immagine possa essere definita come panorama sferico, deve avere una O entrambe le caratteristiche seguenti:

* Proporzioni di 2:1.
* Tag con le parole chiave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Vedere [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dettagli risorsa e al componente WCM per **[!UICONTROL elementi multimediali panoramici]**.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Nella stessa pagina vengono utilizzate più istanze del componente **[!UICONTROL File multimediali panoramici]**.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L&#39;assegnazione di un predefinito per visualizzatori diverso a ciascun componente **[!UICONTROL Supporto panoramico]** in quella pagina non è supportata.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti per file multimediali panoramici che utilizzano risorse dello stesso tipo, all’interno della pagina.

![panoramica-media-predefinito per visualizzatori](assets/panoramic-media-viewer-preset.png)

Per modificare la seguente impostazione, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un visualizzatore esistente dall’elenco a discesa Predefinito visualizzatore.

Se il predefinito per visualizzatori ricercato non è visibile, accertatevi che sia pubblicato. Pubblicate i predefiniti per visualizzatori prima di utilizzarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Componente: Video 360 Media {#video-media-component}

Utilizzate il componente **[!UICONTROL Video 360 Media]** per eseguire il rendering di video equirettangolari sulla pagina Web. In questo modo si assicura un&#39;esperienza di visualizzazione coinvolgente di una stanza, una proprietà, un luogo, un paesaggio o una procedura medica.

Durante la riproduzione su uno schermo piatto, l&#39;utente ha il controllo dell&#39;angolo di visione; la riproduzione su dispositivi mobili utilizza generalmente i controlli giroscopici incorporati.

Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Potete distribuire video a 360 gradi utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Per modificare la seguente impostazione, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un visualizzatore esistente dall’elenco a discesa Predefinito visualizzatore. Utilizzate Video360VR per gli utenti finali che utilizzano occhiali di realtà virtuale. Include controlli di riproduzione video di base e funzioni per social media. Utilizzate Video360_social che include controlli di riproduzione video di base. Il rendering video viene eseguito in modalità stereo. Il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato. Non esistono funzioni per social media.

Se il predefinito per visualizzatori ricercato non è visibile, accertatevi che sia pubblicato. Pubblicate i predefiniti per visualizzatori prima di utilizzarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Utilizzo di HTTP/2 per la distribuzione di risorse Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, migliorando la risposta e i tempi di caricamento.

Per informazioni dettagliate sull&#39;utilizzo di HTTP/2 con l&#39;account Dynamic Media, vedere [HTTP2 Delivery of Content](/help/assets/dynamic-media/http2faq.md).

>[!MORELIKETHIS]
>
>* [Utilizzo del lettore video in Dynamic Media  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [Utilizzo di video interattivi con Dynamic Media  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [Il visualizzatore delle risorse con  Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [Utilizzo della miniatura video personalizzata con  Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [Gestione del colore con Dynamic Media  Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Utilizzo della nitidezza immagine con  Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

