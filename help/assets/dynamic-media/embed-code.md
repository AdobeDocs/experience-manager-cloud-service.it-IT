---
title: Incorporare il visualizzatore di video o immagini Dynamic Media in una pagina web
description: Scopri come incorporare risorse video o immagini Dynamic Media in una pagina web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 21%

---

# Incorpora il visualizzatore Dynamic Media Video, Immagine o Dimensionale in una pagina web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Gli URL vengono incorporati solo se _non_ utilizzo di Adobe Experience Manager come WCM. Se si utilizza Experience Manager come WCM, [aggiungi le risorse direttamente sulla pagina](adding-dynamic-media-assets-to-pages.md).

Consulta [Collegare gli URL all’applicazione web](linking-urls-to-yourwebapplication.md).

Consulta [Distribuzione di immagini ottimizzate per un sito reattivo](responsive-site.md).

>[!NOTE]
>
>Il codice da incorporare è disponibile per la copia solo dopo la pubblicazione della risorsa selezionata. Inoltre, devi pubblicare anche il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicare le risorse](publishing-dynamicmedia-assets.md).
>
>Consulta [Pubblica predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

**Per incorporare il visualizzatore di video o immagini Dynamic Media in una pagina Web:**

1. Accedi a *pubblicato* risorsa video o immagine di cui desideri copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consulta [Pubblicare le risorse](publishing-dynamicmedia-assets.md).

   Consulta [Pubblica predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, seleziona l’elenco a discesa e seleziona **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, seleziona un nome per il predefinito visualizzatore. Il predefinito visualizzatore viene applicato alla risorsa.
1. Seleziona **[!UICONTROL Incorpora]**.
1. In **[!UICONTROL Codice di incorporamento]** , copiare l&#39;intero codice negli Appunti e quindi selezionare **[!UICONTROL Chiudi]**.
1. Incolla il codice da incorporare nelle pagine web.

## Utilizza HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, il che fornisce tempi di risposta e di caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media.
