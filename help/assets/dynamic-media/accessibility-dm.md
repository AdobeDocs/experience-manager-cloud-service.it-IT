---
title: Accessibilità in Dynamic Media
description: Scopri come utilizzare i video in Dynamic Medie, ad esempio come best practice per codificare i video, pubblicare video in YouTube e visualizzare rapporti video. Scopri anche come aggiungere sottotitoli, sottotitoli o marcatori capitolo ai video.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 6ad46350906c3b8a36a8e361714fa5fffdbf8e82
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# Accessibilità in Dynamic Media {#accessibility-in-dm}

{{work-with-dynamic-media}}

Dynamic Medie supporta il controllo da tastiera e tecnologie per l’accessibilità, come le utilità di lettura dello schermo JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto dell’accessibilità della tastiera in Dynamic Medie {#keyboard-support-in-dm}

Poiché Dynamic Medie è un plug-in di [!DNL Experience Manager Assets], la maggior parte del comportamento del controllo da tastiera è identico a quello di [!DNL Experience Manager Assets]. Il pulsante `Cancel` in Dynamic Medie, ad esempio, ha la stessa evidenziazione di attivazione di [!DNL Experience Manager Assets]. Reagisce anche alla chiave `Spacebar` come in [!DNL Experience Manager Assets]. Consulta [scelte rapide da tastiera in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Le sequenze di tasti supportate dai singoli elementi dell’interfaccia utente in Dynamic Medie sono, nella maggior parte dei casi, ovvie e facili da trovare. Il controllo tramite tastiera in Dynamic Medie riguarda i seguenti aspetti:

* Possibilità di utilizzare le pressioni dei tasti `Tab` e `Shift+Tab` per spostarsi tra gli elementi interattivi della pagina.
L&#39;utilizzo di `Tab` fa avanzare lo stato attivo dell&#39;input all&#39;elemento successivo dell&#39;interfaccia utente nell&#39;ordine di tabulazione; l&#39;utilizzo di `Shift+Tab` riporta lo stato attivo dell&#39;input all&#39;elemento precedente dell&#39;interfaccia utente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale degli elementi dell&#39;interfaccia sullo schermo e si sposta da sinistra a destra e quindi dall&#39;alto al basso. Inoltre, se un campo presenta un errore, è possibile premere `Tab` per spostare lo stato attivo su di esso.
* Possibilità di utilizzare i tasti `Spacebar` e `Enter` per attivare gli elementi standard dell&#39;interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l&#39;evidenziazione di tastiera sull&#39;elemento attivo. L’elemento dell’interfaccia utente che ha lo stato attivo sull’input ha ricevuto un’indicazione di stato attivo visivo come bordo rappresentato intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare la pressione di alcuni tasti personalizzati, ad esempio i tasti di direzione, per interagire con elementi complessi dell’interfaccia utente e riposizionare i punti attivi.
* Nell&#39;editor video interattivo è possibile utilizzare `Spacebar` per selezionare un&#39;immagine e aggiungerla a un segmento. È inoltre possibile utilizzare la chiave `Backspace` per eliminare l&#39;elemento selezionato dalla scheda **[!UICONTROL Contenuto]**. Inoltre, premendo `Tab` è possibile spostarsi tra gli elementi interattivi della pagina.
* Nell’editor di ritaglio immagine/ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni del fotogramma, o riposizionare l&#39;immagine, o entrambi.
   * La prima interruzione di `Tab` evidenzia l&#39;intero frame dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le prossime quattro `Tab` interruzioni sono i quattro angoli del frame. Quando lo stato attivo viene posizionato su un angolo del fotogramma, l&#39;angolo viene evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Vedi [Modifica del ritaglio o del campione avanzato di una singola immagine](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto per la tecnologia di supporto in Dynamic Medie {#assistive-technology=support-for-dm}

Gli elementi dell’interfaccia utente di Dynamic Medie funzionano con tecnologie per l’accessibilità, come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga tra i punti di riferimento utilizzando la scelta rapida da tastiera `D` o le aree utilizzando la scelta rapida da tastiera `R`. Inoltre, legge l&#39;intestazione quando si naviga utilizzando la scelta rapida da tastiera per l&#39;intestazione `H`.

## Supporto dell’accessibilità della tastiera nei visualizzatori Dynamic Medie {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti predefiniti per visualizzatori Dynamic Medie supportano l’accessibilità da tastiera per i clienti.

Consulta [Accesso facilitato alla tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento dei visualizzatori di Dynamic Medie.

## Supporto per la tecnologia di supporto nei visualizzatori Dynamic Medie {#assistive-technology=support-for-dm-viewers}

Tutti i componenti visualizzatore Dynamic Medie supportano i ruoli e gli attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie per l’accessibilità, come gli assistenti vocali.
Vedere l&#39;argomento della Guida relativo al supporto tecnico **Assistive Technology** in qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento dei visualizzatori di Dynamic Medie. Ad esempio, consulta [Supporto per la tecnologia per l&#39;accesso facilitato](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore di video o [Supporto per la tecnologia per l&#39;accesso facilitato](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattivo.

## Supporto per sottotitoli codificati in [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Medie supporta la distribuzione di video e set di video adattivi con sottotitoli. I sottotitoli devono essere visualizzati sopra il contenuto video.

Vedi [Video in Dynamic Medie - Aggiungi sottotitoli al video](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Accessibilità per le soluzioni Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)
