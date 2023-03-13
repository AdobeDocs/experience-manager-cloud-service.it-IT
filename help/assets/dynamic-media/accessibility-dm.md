---
title: Accessibilità in Dynamic Media
description: Scopri come utilizzare i video in Dynamic Media, ad esempio come best practice per codificare i video, pubblicare video in YouTube e visualizzare rapporti video. Scopri anche come aggiungere sottotitoli, sottotitoli o marcatori capitolo ai video.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 0d3262a3182063e69f764339e7937e2f83ad7bbb
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Accessibilità in Dynamic Media {#accessibility-in-dm}

Dynamic Media supporta il controllo da tastiera e tecnologie per l’accessibilità, come le utilità di lettura dello schermo JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto dell’accessibilità della tastiera in Dynamic Media {#keyboard-support-in-dm}

Perché Dynamic Media è un plug-in per [!DNL Experience Manager Assets], la maggior parte del comportamento di controllo della tastiera è uguale a quello [!DNL Experience Manager Assets]. Ad esempio, il `Cancel` in Dynamic Media ha la stessa evidenziazione di messa a fuoco come in [!DNL Experience Manager Assets]. Essa reagisce inoltre alla `Spacebar` chiave come in [!DNL Experience Manager Assets]. Consulta [scelte rapide da tastiera in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Le sequenze di tasti supportate dai singoli elementi dell’interfaccia utente in Dynamic Media sono, nella maggior parte dei casi, ovvie e facili da trovare. Il controllo tramite tastiera in Dynamic Media riguarda i seguenti aspetti:

* Capacità di utilizzare `Tab` e `Shift+Tab` tasti per spostarsi tra gli elementi interattivi della pagina.
Utilizzo di `Tab` sposta lo stato attivo dell&#39;input sull&#39;elemento dell&#39;interfaccia utente successivo nell&#39;ordine di tabulazione; utilizzando `Shift+Tab` riporta lo stato attivo sull’elemento dell’interfaccia utente precedente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale degli elementi dell&#39;interfaccia sullo schermo e si sposta da sinistra a destra e quindi dall&#39;alto al basso. Inoltre, se un campo presenta un errore, è possibile premere `Tab` per spostare lo stato attivo su di esso.
* Possibilità di utilizzare `Spacebar` e `Enter` per attivare gli elementi standard dell’interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l&#39;evidenziazione di tastiera sull&#39;elemento attivo. L’elemento dell’interfaccia utente che ha lo stato attivo sull’input ha ricevuto un’indicazione di stato attivo visivo come bordo rappresentato intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare la pressione di alcuni tasti personalizzati, ad esempio i tasti di direzione, per interagire con elementi complessi dell’interfaccia utente e riposizionare i punti attivi.
* Nell’editor video interattivo puoi utilizzare `Spacebar` per selezionare un’immagine e aggiungerla a un segmento. Inoltre, è possibile utilizzare `Backspace` chiave per eliminare l’elemento selezionato da **[!UICONTROL Contenuto]** scheda. Inoltre, premendo `Tab` funziona come desiderato per navigare tra gli elementi interattivi sulla pagina.
* Nell’editor di ritaglio immagine/ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni del fotogramma, o riposizionare l&#39;immagine, o entrambi.
   * Il primo `Tab` stop evidenzia l&#39;intero frame dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le prossime quattro `Tab` Le fermate sono i quattro angoli del frame. Quando lo stato attivo viene posizionato su un angolo del fotogramma, l&#39;angolo viene evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Consulta [Modifica del ritaglio o del campione avanzato di una singola immagine](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto per le tecnologie di supporto in Dynamic Media {#assistive-technology=support-for-dm}

Gli elementi dell’interfaccia utente di Dynamic Media funzionano con tecnologie per l’accessibilità, come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga tra i punti di riferimento utilizzando la scelta rapida da tastiera `D` o aree tramite scelta rapida da tastiera `R`. Vengono inoltre narrate le intestazioni durante la navigazione utilizzando la scelta rapida da tastiera per le intestazioni `H`.

## Supporto dell’accessibilità della tastiera nei visualizzatori Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti predefiniti per visualizzatori Dynamic Media supportano l’accessibilità da tastiera per i clienti.

Consulta [Accessibilità della tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento dei visualizzatori di Dynamic Media.

## Supporto per la tecnologia di supporto nei visualizzatori Dynamic Media {#assistive-technology=support-for-dm-viewers}

Tutti i componenti visualizzatore Dynamic Media supportano i ruoli e gli attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie per l’accessibilità, come gli assistenti vocali.
Consulta la **Supporto di tecnologie assistive** Argomento della Guida in linea di qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento dei visualizzatori di Dynamic Media. Ad esempio, consulta [Supporto di tecnologie assistive](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore Video, oppure [Supporto di tecnologie assistive](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

## Supporto per sottotitoli codificati in [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Media supporta la distribuzione di video e set di video adattivi con sottotitoli. I sottotitoli devono essere visualizzati sopra il contenuto video.

Consulta [Video in Dynamic Media: aggiungi sottotitoli o sottotitoli al video](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Accessibilità per soluzioni di Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)

