---
title: Aggiungere risorse Dynamic Media alle pagine
description: Scopri come aggiungere componenti Dynamic Media a una pagina in Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: da4174929e1eb8e15447f936dc89a67391c72209
workflow-type: tm+mt
source-wordcount: '3216'
ht-degree: 19%

---

# Aggiungere risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi inserire direttamente nella pagina il componente **Dynamic Media**, **File multimediali interattivi**, **Elemento multimediale panoramico** o **File multimediali video 360**. Si entra in modalità Layout e si attivano i componenti Dynamic Media. Quindi aggiungi questi componenti alla pagina e le risorse al componente. I componenti Dynamic Media sono intelligenti: rilevano l’aggiunta di un’immagine o di un video, dunque le opzioni di configurazione disponibili cambiano di conseguenza.

Se utilizzi, puoi aggiungere direttamente alla pagina le risorse Dynamic Media [!DNL Adobe Experience Manager] come WCM. Se si utilizza una terza parte per WCM, [link](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [incorporare](/help/assets/dynamic-media/embed-code.md) risorse. Per un sito web dinamico di terze parti, consulta [distribuzione di immagini ottimizzate a un sito reattivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Accertati di pubblicare le risorse prima di aggiungerle alle pagine di [!DNL Experience Manager]. Consulta [Pubblicazione di risorse Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Aggiungere un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

L’aggiunta di un componente 3D Media, Dynamic Media, File multimediali interattivi, Elemento multimediale panoramico, Ritaglio video avanzato o File multimediali video 360 a una pagina è identica all’aggiunta di un componente a qualsiasi pagina.

**Per aggiungere un componente Dynamic Media a una pagina:**

1. In entrata [!DNL Experience Manager], apri la pagina in cui desideri aggiungere il componente Dynamic Media.
1. Nel riquadro a sinistra, selezionare **[!UICONTROL Componenti]** , quindi applica il filtro per Dynamic Media.

   Se non è disponibile alcun elenco di componenti di Dynamic Media, è probabile che sia necessario abilitare i componenti di Dynamic Media che si desidera utilizzare. Consulta [Abilita componenti Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Trascina un **[!UICONTROL Dynamic Media]** e rilasciarlo nella posizione desiderata sulla pagina.

1. Passa il puntatore direttamente sul componente. Quando il componente è circondato da una casella blu, seleziona una volta per visualizzare la barra degli strumenti del componente. Seleziona la **[!UICONTROL Configurazione (chiave inglese)]** icona.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. A seconda del componente Dynamic Media rilasciato sulla pagina, viene visualizzata una finestra di dialogo di configurazione. [Impostare le opzioni del componente](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) secondo necessità.

   L’esempio seguente mostra il Dynamic Media **[!UICONTROL Contenuti video 360]** e le opzioni disponibili dall&#39;elenco a discesa Predefinito visualizzatore.

   ![Componente per contenuti video 360](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Il componente multimediale Dynamic Media Video 360.

1. Al termine, nell&#39;angolo superiore destro della finestra di dialogo, selezionare il segno di spunta per salvare le modifiche.

### Abilita componenti Dynamic Media {#enabling-dynamic-media-components}

Se non è disponibile alcun componente di Dynamic Media da aggiungere a una pagina, probabilmente dovrai abilitare i componenti da utilizzare.

1. In entrata [!DNL Experience Manager], apri la pagina in cui desideri aggiungere il componente Dynamic Media.
1. A sinistra della barra degli strumenti, nella parte superiore della pagina, seleziona l’icona Informazioni pagina, quindi fai clic su **[!UICONTROL Modifica modello]** dall’elenco a discesa.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. Dal lato destro della barra degli strumenti nella parte superiore della pagina, seleziona dall’elenco a discesa **[!UICONTROL Struttura]**.

   ![Criterio](/help/assets/assets-dm/structure-mode.png)

1. Nella parte inferiore della pagina, seleziona **[!UICONTROL Contenitore di layout]** per aprire la relativa barra degli strumenti, seleziona l’icona Criterio.
1. Il giorno **[!UICONTROL Contenitore di layout]** pagina, sotto **[!UICONTROL Proprietà]** , assicurati che il **[!UICONTROL Componenti consentiti]** è selezionata.

   ![Componenti consentiti](/help/assets/assets-dm/allowed-components.png)

1. Scorri fino a visualizzare **[!UICONTROL Dynamic Media]**.
1. Seleziona l’icona > a sinistra di **[!UICONTROL Dynamic Media]**, quindi seleziona i componenti Dynamic Media che desideri abilitare.

   ![Elenco dei componenti di Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Vicino all&#39;angolo superiore destro del **[!UICONTROL Contenitore di layout]** , selezionare l&#39;icona Fine (segno di spunta).

1. Dal lato destro della barra degli strumenti nella parte superiore della pagina, seleziona dall’elenco a discesa **[!UICONTROL Contenuto iniziale]**.
1. [Aggiungere un componente Dynamic Media a una pagina](#adding-a-dynamic-media-component-to-a-page) come al solito.

## Localizzare i componenti Dynamic Media {#localizing-dynamic-media-components}

È possibile localizzare i componenti Dynamic Media in uno dei due modi seguenti:

* In una pagina web di Sites, apri **[!UICONTROL Proprietà]** e seleziona la scheda **[!UICONTROL Avanzate]**. Scegli la lingua desiderata per la localizzazione.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Dal selettore del sito, seleziona la pagina o il gruppo di pagine desiderato. Seleziona **[!UICONTROL Proprietà]** e seleziona la **[!UICONTROL Avanzate]** scheda. Scegli la lingua desiderata per la localizzazione.

   >[!NOTE]
   >
   >Non tutte le lingue disponibili nel **[!UICONTROL Lingua]** al momento sono assegnati dei token al menu.

## Componenti Dynamic Media disponibili {#dynamic-media-components}

I componenti Dynamic Media sono disponibili quando si seleziona **[!UICONTROL Componenti]** , quindi filtra per **[!UICONTROL Dynamic Media]**.

I componenti Dynamic Media disponibili includono:

* **[!UICONTROL Dynamic Media]**: da utilizzare per risorse quali immagini, video, eCatalog e set 360 gradi.
* **[!UICONTROL File multimediali interattivi]** : utilizza per qualsiasi risorsa interattiva come video interattivo, immagini interattive o set carosello.
* **[!UICONTROL Elemento multimediale panoramico]** - Usare per immagini panoramiche o immagini panoramiche VR.
* **[!UICONTROL Contenuti video 360]** : da utilizzare per risorse video 360 e 360 VR.

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere resi disponibili tramite l’editor di modelli prima di utilizzare. Dopo essere stati resi disponibili nell’editor modelli, puoi aggiungere i componenti alla pagina come faresti con qualsiasi altro [!DNL Experience Manager] componente.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

Il componente Dynamic Media è intelligente. Sia che si aggiunga un&#39;immagine o un video, sono disponibili varie opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina web presenta le seguenti caratteristiche:
>
>* Più istanze del componente Dynamic Media in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.
>
>L’assegnazione di un predefinito visualizzatore diverso a ciascun componente Dynamic Media di quella pagina non è supportata.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti Dynamic Media che utilizzano risorse dello stesso tipo, all’interno della pagina.

Quando aggiungi il Componente elementi multimediali dinamici e le **[!UICONTROL Impostazioni elemento multimediale dinamico]** sono vuote o non è possibile aggiungere correttamente una risorsa, controlla quanto segue:

* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell&#39;attivazione di Dynamic Media non dispongono di un file tiff piramidale.

#### Quando si lavora con le immagini {#when-working-with-images}

Il componente elementi multimediali dinamici consente di aggiungere immagini dinamiche, compresi set di immagini, set di rotazione e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere reattiva un’immagine, puoi impostare i punti di interruzione o applicare un predefinito per immagine reattiva.

È possibile modificare le seguenti impostazioni di Dynamic Media selezionando **[!UICONTROL Modifica]** nel componente e quindi **[!UICONTROL Impostazioni Dynamic Media]**.

![Impostazioni predefinito immagine Dynamic Media](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]**.

* **[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore esistente dall’elenco a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

   Questa opzione è l&#39;unica disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi. I predefiniti visualizzatore visualizzati sono anche predefiniti visualizzatore rilevanti solo per il visualizzatore.

* **[!UICONTROL Modificatori visualizzatore]** - I modificatori visualizzatore si presentano come coppia nome=valore con delimitatore &amp; e consentono di modificare i visualizzatori come descritto nella Guida di riferimento visualizzatori. Un esempio di modificatore di visualizzatore è `posterimage=img.jpg&caption=text.vtt,1` che imposta un&#39;immagine diversa per la miniatura del video e associa al video un file di sottotitoli/sottotitoli codificati.

* **[!UICONTROL Predefinito immagine]** - Selezionate un predefinito immagine esistente dall&#39;elenco a discesa. Se il predefinito immagine che state cercando non è visibile, dovete renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Modificatori immagine]** - È possibile applicare effetti immagine fornendo più comandi per l&#39;immagine. Questi comandi sono descritti in Predefiniti immagine e nella Guida di riferimento per i comandi Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Punti di interruzione]** - Se utilizzi questa risorsa su un sito reattivo, devi aggiungere i punti di interruzione immagine. I punti di interruzione delle immagini devono essere separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Puoi modificare le seguenti Impostazioni avanzate selezionando **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Ottimizza per dispositivi ad alta risoluzione]** - Selezionare (impostazione predefinita) la casella di controllo per consentire l&#39;ottimizzazione DPR (Device Pixel Ratio).

   Il **[!UICONTROL Ottimizza per dispositivi ad alta risoluzione]** L&#39;opzione viene visualizzata solo quando è vero quanto segue:
   * In Tipo di predefinito, **[!UICONTROL Predefinito immagine]** è selezionato, e **[!UICONTROL RESS_IP]** è selezionato da **[!UICONTROL Predefinito immagine]** elenco a discesa.

   ![impostazione delle proporzioni pixel del dispositivo per predefinito immagine](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

   Vedi anche [Informazioni sull&#39;ottimizzazione delle proporzioni pixel del dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

   Qualsiasi [!DNL Experience Manager] I valori DPR di Dynamic Media Smart Imaging vengono ignorati.

* **[!UICONTROL Titolo]** - Modifica il titolo dell&#39;immagine.

* **[!UICONTROL Testo alternativo]** : aggiungi un titolo all&#39;immagine per gli utenti che hanno la grafica disattivata.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** - È possibile impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

#### Quando esegui operazioni con i Video {#when-working-with-video}

Utilizza il componente Dynamic Media per aggiungere video dinamici alle pagine web. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video predefinito per riprodurre il video sulla pagina.

![chlimage_1-173](assets/chlimage_1-540.png)

Puoi modificare le seguenti impostazioni di Dynamic Media selezionando **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nel componente con **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nel **[!UICONTROL Avanzate]** scheda.

* **[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore video esistente dall’elenco a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Modificatori visualizzatore]** - Modificatori per visualizzatori: `name=value` coppia con un `&` delimitatore. Consentono di modificare i visualizzatori come descritto nella Guida di riferimento dei visualizzatori di Adobe. Un esempio di modificatore di visualizzatore è `posterimage=img.jpg&caption=text.vtt,1`

   Con i modificatori del visualizzatore è possibile, ad esempio, effettuare le seguenti operazioni:

   * Associa un file di didascalia a un video: [didascalia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associa un file di navigazione a un video: [navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Puoi modificare le seguenti Impostazioni avanzate selezionando **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Titolo]** - Modifica il titolo del video.

* **[!UICONTROL Larghezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

#### Quando si lavora con Ritaglio avanzato {#when-working-with-smart-crop}

Utilizza il componente Dynamic Media per aggiungere alle pagine web risorse immagine di ritaglio avanzato. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video predefinito per riprodurre il video sulla pagina.

Consulta [Utilizzare il ritaglio avanzato con Experience Manager Assets Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

Vedi anche [Profili immagine](/help/assets/dynamic-media/image-profiles.md).

![Impostazioni ritaglio avanzato Dynamic Media](assets/dm-settings-smart-crop.png)

Puoi modificare le seguenti impostazioni di Dynamic Media selezionando **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]**.

* **[!UICONTROL Modificatori immagine]** - È possibile applicare effetti immagine fornendo più comandi per l&#39;immagine. Questi comandi sono descritti in Predefiniti immagine e nella Guida di riferimento per i comandi Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Puoi modificare le seguenti Impostazioni avanzate selezionando **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Abilita corrispondenza proporzioni]** : seleziona questa opzione per consentire a Dynamic Media di scegliere un rendering di ritaglio avanzato con proporzioni che corrispondano al meglio alle proporzioni dell’immagine originale.

* **[!UICONTROL Ottimizza per dispositivi ad alta risoluzione]** - Selezionare (impostazione predefinita) la casella di controllo per consentire l&#39;ottimizzazione DPR (Device Pixel Ratio).

   Il **[!UICONTROL Ottimizza per dispositivi ad alta risoluzione]** L&#39;opzione viene visualizzata solo quando è vero quanto segue:

   * In Tipo di predefinito, **[!UICONTROL Ritaglio avanzato]** è selezionata.

   ![impostazione delle proporzioni pixel del dispositivo per il ritaglio avanzato](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

   Vedi anche [Informazioni sull&#39;ottimizzazione delle proporzioni pixel del dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

   Qualsiasi [!DNL Experience Manager] I valori DPR di Dynamic Media Smart Imaging vengono ignorati.

* **[!UICONTROL Titolo]** - Modifica il titolo dell&#39;immagine di ritaglio avanzato.

* **[!UICONTROL Testo alternativo]** : aggiungi un titolo all’immagine di ritaglio avanzato per gli utenti che hanno la grafica disattivata.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** - È possibile impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

### Componente: File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente File multimediali interattivi è intelligente. Sia che si aggiunga un&#39;immagine o un video, sono disponibili varie opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina web presenta le seguenti caratteristiche:
>
>* Più istanze del componente File multimediali interattivi utilizzate nella stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.
>
>L’assegnazione di un predefinito visualizzatore diverso a ciascun componente File multimediali interattivi di quella pagina non è supportata.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti di Interactive Media che utilizzano risorse dello stesso tipo, all’interno della pagina.

![chlimage_1-174](assets/chlimage_1-541.png)

È possibile modificare quanto segue **[!UICONTROL Generale]** impostazioni selezionando **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore esistente dall’elenco a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Titolo]** - Modifica il titolo del video.

* **[!UICONTROL Larghezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

   È possibile modificare quanto segue **[!UICONTROL Aggiungi al carrello]** impostazioni selezionando **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Mostra risorsa prodotto]** - Per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

* **[!UICONTROL Mostra prezzo prodotto]** - Per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

* **[!UICONTROL Mostra modulo prodotto]** - Per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.

### Componente: elemento multimediale panoramico {#panoramic-media-component}

Il componente Elemento multimediale panoramico è destinato alle risorse che sono immagini panoramiche sferiche. Tali immagini forniscono un’esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio. Affinché un&#39;immagine possa essere considerata un panorama sferico, è necessario che disponga di uno o entrambi i seguenti elementi:

* Rapporto di formato 2:1.
* Contrassegnato con le parole chiave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Consulta [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dettagli risorsa e al componente WCM per **[!UICONTROL elementi multimediali panoramici]**.

>[!NOTE]
>
>Se la pagina web presenta le seguenti caratteristiche:
>
>* Più istanze di **[!UICONTROL Elemento multimediale panoramico]** componente utilizzato sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.
>
>Assegnazione di un predefinito visualizzatore diverso a ciascun **[!UICONTROL Elemento multimediale panoramico]** il componente in quella pagina non è supportato.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti Elemento multimediale panoramico che utilizzano risorse dello stesso tipo, all’interno della pagina.

![Predefinito visualizzatore elementi multimediali panoramici](assets/panoramic-media-viewer-preset.png)

Puoi modificare la seguente impostazione selezionando **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** - Selezionare un visualizzatore esistente dall&#39;elenco a discesa Predefinito visualizzatore.

Se il predefinito visualizzatore che stai cercando non è visibile, controlla che sia pubblicato. Pubblica i predefiniti visualizzatore prima di utilizzarli. Consulta [Gestisci predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md).

### Component: video 360 media {#video-media-component}

Utilizza il **[!UICONTROL Contenuti video 360]** per riprodurre video equirettangolari sulla pagina web. In questo modo si garantisce un&#39;esperienza visiva coinvolgente di una stanza, una proprietà, una posizione, un paesaggio o una procedura medica.

Durante la riproduzione su uno schermo piatto, l&#39;utente ha il controllo dell&#39;angolo di visualizzazione; la riproduzione su dispositivi mobili utilizza in genere i controlli giroscopici incorporati.

Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Puoi distribuire video 360 utilizzando le estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Puoi modificare la seguente impostazione selezionando **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** - Selezionare un visualizzatore esistente dall&#39;elenco a discesa Predefinito visualizzatore. Utilizzare Video360VR per gli utenti finali che utilizzano occhiali di realtà virtuale. Include controlli di riproduzione video di base e funzioni per social media. Utilizza Video360_social, che include controlli di base per la riproduzione di video. Il rendering video viene eseguito in modalità stereo. Il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato. Non sono presenti funzioni per social media.

Se il predefinito visualizzatore che stai cercando non è visibile, controlla che sia pubblicato. Pubblica i predefiniti visualizzatore prima di utilizzarli. Consulta [Gestisci predefiniti visualizzatore](/help/assets/dynamic-media/managing-viewer-presets.md).

### Usa HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, il che fornisce tempi di risposta e di caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](/help/assets/dynamic-media/http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media.

>[!MORELIKETHIS]
>
>* [Utilizzare il lettore video in Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [Utilizzare il video interattivo con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [Comprendere il Visualizzatore risorse con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [Usa miniatura video personalizzata con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [Comprendere la gestione del colore con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Utilizzare la nitidezza delle immagini con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

