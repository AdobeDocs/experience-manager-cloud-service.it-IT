---
title: Incorporare il visualizzatore di video o immagini Dynamic Media in una pagina web
description: Scopri come incorporare risorse video o immagini Dynamic Media in una pagina web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 21%

---

# Incorpora il visualizzatore Dynamic Media Video, Immagine o Dimensionale in una pagina web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Gli URL vengono incorporati solo se _non_ utilizza Adobe Experience Manager come WCM. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente nella pagina](adding-dynamic-media-assets-to-pages.md).

Consulta [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consulta [Distribuire immagini ottimizzate per un sito reattivo](responsive-site.md).

>[!NOTE]
>
>Il codice da incorporare è disponibile per la copia solo dopo la pubblicazione della risorsa selezionata. Inoltre, devi pubblicare anche il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicare Assets](publishing-dynamicmedia-assets.md).
>
>Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

**Per incorporare il visualizzatore di video o immagini Dynamic Media in una pagina Web:**

1. Passa alla risorsa video o immagine *pubblicata* di cui desideri copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consulta [Pubblicare Assets](publishing-dynamicmedia-assets.md).

   Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, seleziona l&#39;elenco a discesa e seleziona **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, seleziona un nome per il predefinito visualizzatore. Il predefinito visualizzatore viene applicato alla risorsa.
1. Seleziona **[!UICONTROL Incorpora]**.
1. Nella finestra di dialogo **[!UICONTROL Incorpora codice]**, copiare l&#39;intero codice negli Appunti, quindi selezionare **[!UICONTROL Chiudi]**.
1. Incolla il codice da incorporare nelle pagine web.

## Utilizza HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, il che offre tempi di risposta e caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con l&#39;account Dynamic Media.
