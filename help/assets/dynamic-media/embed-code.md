---
title: Incorporare il visualizzatore video o immagine Dynamic Media in una pagina web
description: Scopri come incorporare risorse video o immagini Dynamic Media in una pagina web.
feature: Gestione risorse
role: Business Practitioner
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 21%

---

# Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Incorpora gli URL solo se _non_ utilizzi AEM come WCM. Se utilizzi AEM come WCM, [aggiungi le risorse direttamente sulla pagina](adding-dynamic-media-assets-to-pages.md).

Consulta [Collegamento di URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consulta [Distribuzione di immagini ottimizzate per un sito reattivo](responsive-site.md).

>[!NOTE]
>
>Il codice di incorporamento non è disponibile per la copia finché non avrai pubblicato la risorsa selezionata. Inoltre, devi pubblicare il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).
>
>Consulta [Pubblicazione dei predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblicazione di predefiniti immagine](managing-image-presets.md#publishing-image-presets).

**Per incorporare il visualizzatore video o immagine Dynamic Media in una pagina web**

1. Passa al video o alla risorsa immagine *pubblicata* di cui desideri copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consulta [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).

   Consulta [Pubblicazione dei predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblicazione di predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, seleziona l’elenco a discesa e tocca **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, tocca un nome predefinito per visualizzatori. Il predefinito visualizzatore viene applicato alla risorsa.
1. Tocca **[!UICONTROL Incorpora]**.
1. Nella finestra di dialogo **[!UICONTROL Incorpora codice]**, copia l’intero codice negli Appunti, quindi tocca **[!UICONTROL Chiudi]**.
1. Incolla il codice di incorporamento nelle pagine web.

## Utilizzo di HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media può ora avvenire tramite HTTP/2, garantendo tempi di risposta e caricamento migliori.

Per informazioni dettagliate su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media, consulta [Distribuzione di contenuti HTTP2](http2faq.md) .
