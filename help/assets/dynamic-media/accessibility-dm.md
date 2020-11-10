---
title: Accessibilità in [!DNL Dynamic Media]
description: Scopri come lavorare con risorse 3D in Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 7af8ddda4aee093b22147db9be9f65cd0c131c04
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Accessibilità in elementi multimediali dinamici {#working-with-three-d-assets-dm}

Dynamic Media supporta il controllo da tastiera e tecnologie di supporto, come gli assistenti vocali JAWS e NVDA, nell’interfaccia utente di authoring.



## Supporto per l&#39;accessibilità da tastiera in Contenuti multimediali dinamici

I tasti supportati da singoli elementi dell&#39;interfaccia utente sono, nella maggior parte dei casi, evidenti e facili da scoprire. Il controllo della tastiera in Contenuti multimediali dinamici è il seguente:

* Possibilità di utilizzare `Tab` e `Shift+Tab` tasti per spostarsi tra gli elementi interattivi sulla pagina.
L&#39;utilizzo di `Tab` rende più attivo il successivo elemento dell&#39;interfaccia utente nell&#39;ordine di tabulazione; l&#39;utilizzo `Shift+Tab` ripristina l&#39;input dell&#39;elemento dell&#39;interfaccia utente precedente.
La barra laterale di messa a fuoco segue la posizione naturale dell&#39;elemento dell&#39;interfaccia utente sullo schermo e si sposta in ordine da sinistra a destra, quindi dall&#39;alto verso il basso.
* Possibilità di utilizzare il tasto `Spacebar` e `Enter` per attivare gli elementi standard dell&#39;interfaccia utente, ad esempio pulsanti, elenchi a discesa e così via.
* Possibilità di visualizzare l&#39;evidenziazione dello stato attivo. L&#39;elemento dell&#39;interfaccia utente attivo può ricevere un&#39;indicazione visiva come bordo intorno all&#39;elemento dell&#39;interfaccia utente.
* Possibilità di usare alcuni tasti personalizzati per interagire con elementi dell’interfaccia utente complessi, ad esempio i tasti freccia nell’editor hot spot. Nell’editor Ritaglio immagine/Ritaglio avanzato è possibile utilizzare i tasti freccia per ritagliare le dimensioni del fotogramma, riposizionare l’immagine o entrambi.

Poiché Dynamic Media è un plug-in per  AEM Assets, la maggior parte del comportamento dei controlli da tastiera è esattamente uguale a  AEM Assets. Ad esempio, il `Cancel` pulsante in Contenuti multimediali dinamici ha la stessa evidenziazione dello stato attivo di  AEM Assets e reagisce alla `Spacebar` chiave come in  AEM Assets. Consultate Scelte rapide da [tastiera in Risorse](/help/assets/accessibility.md#keyboard-shortcuts). Eccezioni a questo sono l’editor dei punti attivi e gli editor di ritaglio immagini/ritaglio avanzato.

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

Nell’editor di punti sensibili, Dynamic Media consente di utilizzare i tasti freccia per controllare la posizione di un punto critico. Consultate [Carosello Banner](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) o Immagini [interattive](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

Nell’editor Ritaglio immagine/Ritaglio avanzato, utilizzate i tasti freccia per ritagliare le dimensioni del fotogramma, oppure riposizionate l’immagine o entrambi. Consultate [Modifica del ritaglio avanzato o del campione avanzato di una singola immagine](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto per l’accessibilità da tastiera per visualizzatori per contenuti multimediali dinamici {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti predefiniti per visualizzatori per contenuti multimediali dinamici supportano l’accessibilità da tastiera per i clienti.

Consultate Accessibilità [della tastiera e navigazione](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella guida di riferimento dei visualizzatori per contenuti multimediali dinamici.

## Supporto della tecnologia di supporto per visualizzatori per contenuti multimediali dinamici {#assistive-technology=support-for-dm-viewers}

Tutti i componenti del visualizzatore in Dynamic Media supportano ruoli e attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie di supporto come gli assistenti vocali.

Consultate l’argomento della guida del supporto **per la tecnologia di** assistenza in qualsiasi argomento del visualizzatore personalizzato nella guida di riferimento dei visualizzatori per contenuti multimediali dinamici. Ad esempio, consultate Supporto per la tecnologia [di assistenza](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore video o Supporto per la tecnologia di [assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

>[!MORELIKETHIS]
>
>* [Accessibilità per soluzioni  Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in  risorse Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

