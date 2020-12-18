---
title: Accessibilità in [!DNL Dynamic Media]
description: Informazioni sull’accessibilità nei visualizzatori Dynamic Media e Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: c3ada59105cad7c2fc3b36b032d045b91f86b495
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Accessibilità in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media supporta le tecnologie di controllo della tastiera e di assistenza, come gli assistenti vocali JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto dell&#39;accessibilità da tastiera in Dynamic Media

Poiché Dynamic Media è un plug-in per  risorse di Experience Manager, la maggior parte dei controlli da tastiera si comportano esattamente come in  risorse Experience Manager. Ad esempio, il pulsante `Cancel` in Dynamic Media ha la stessa evidenziazione dello stato attivo di  risorse del Experience Manager e reagisce alla chiave `Spacebar` come in  risorse Experience Manager. Vedere [Scelte rapide da tastiera in Risorse](/help/assets/accessibility.md#keyboard-shortcuts).

I tasti supportati dai singoli elementi dell&#39;interfaccia utente in Dynamic Media sono, nella maggior parte dei casi, evidenti e facili da scoprire. Il controllo della tastiera in Dynamic Media è circa quanto segue:

* Possibilità di utilizzare i tasti `Tab` e `Shift+Tab` per spostarsi tra gli elementi interattivi sulla pagina.
L&#39;utilizzo di `Tab` rende più attivo il successivo elemento dell&#39;interfaccia utente nell&#39;ordine di tabulazione; l&#39;utilizzo di `Shift+Tab` riattiva l&#39;elemento dell&#39;interfaccia utente precedente.
La barra laterale di messa a fuoco segue la posizione naturale dell&#39;elemento dell&#39;interfaccia utente sullo schermo e si sposta in ordine da sinistra a destra, quindi dall&#39;alto verso il basso. Inoltre, se un campo ha un errore, è possibile premere `Tab` per attivarlo.
* Possibilità di utilizzare il tasto `Spacebar` e `Enter` per attivare gli elementi standard dell&#39;interfaccia utente, ad esempio pulsanti, elenco a discesa e così via.
* Possibilità di visualizzare l&#39;evidenziazione dello stato attivo. L&#39;elemento dell&#39;interfaccia utente attivo può ricevere un&#39;indicazione visiva come bordo intorno all&#39;elemento dell&#39;interfaccia utente.
* Nell&#39;editor dei punti di attivazione è possibile utilizzare alcuni tasti di scelta rapida personalizzati, ad esempio i tasti freccia, per interagire con elementi dell&#39;interfaccia utente complessi per riposizionare i punti di attivazione.
* Nell&#39;editor video interattivo, potete utilizzare il simbolo `Spacebar` per selezionare un&#39;immagine e aggiungerla a un segmento. Inoltre, è possibile utilizzare il tasto `Backspace` per eliminare l&#39;elemento selezionato dalla scheda **[!UICONTROL Content]**. Inoltre, premendo `Tab` è possibile navigare tra gli elementi interattivi della pagina.
* Nell’editor Ritaglio immagine/Ritaglio avanzato, potete effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni della cornice, riposizionare l’immagine o entrambi.
   * La prima `Tab` interruzione evidenzia l&#39;intera cornice dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le quattro `Tab` fermate successive sono i quattro angoli del telaio. Quando lo stato attivo è posizionato su un angolo cornice, l&#39;angolo è evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Vedere [Modifica del ritaglio avanzato o del campione avanzato di una singola immagine](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto della tecnologia di assistenza in Dynamic Media {#assistive-technology=support-for-dm}

Gli elementi dell&#39;interfaccia utente di Dynamic Media funzionano con tecnologie di assistenza come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si spostano i punti di riferimento utilizzando la scelta rapida da tastiera `D` o aree mediante la scelta rapida da tastiera `R`. Inoltre, viene riportata l&#39;intestazione durante la navigazione tramite la scelta rapida da tastiera del titolo `H`.

## Supporto per l&#39;accessibilità da tastiera nei visualizzatori Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti forniti dai visualizzatori Dynamic Media supportano l&#39;accessibilità da tastiera per i clienti.

Consultate [Accessibilità e navigazione da tastiera](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella guida di riferimento dei visualizzatori Dynamic Media.

## Supporto della tecnologia di assistenza nei visualizzatori Dynamic Media {#assistive-technology=support-for-dm-viewers}

Tutti i componenti del visualizzatore Dynamic Media supportano ruoli e attributi ARIA (Accessible Rich Internet Applications) per migliorare l&#39;integrazione con tecnologie di supporto come gli assistenti vocali.
Consultate l&#39;argomento della guida **Supporto per la tecnologia di assistenza** in qualsiasi argomento della personalizzazione del visualizzatore nella Guida di riferimento dei visualizzatori Dynamic Media. Ad esempio, consultate [Supporto per la tecnologia di assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore video, oppure [Supporto per la tecnologia di assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

>[!MORELIKETHIS]
>
>* [Accessibilità per soluzioni  Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in  risorse Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

