---
title: Distribuzione di immagini ottimizzate per un sito reattivo
description: Scopri come utilizzare la funzione di codice reattivo per distribuire immagini ottimizzate da Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 15%

---

# Distribuzione di immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizza la funzione Codice reattivo quando desideri condividere il codice per il servizio reattivo con il tuo sviluppatore web. Copia la risposta (**[!UICONTROL RESS]**) negli Appunti in modo da poterlo condividere con lo sviluppatore web.

Questa funzione ha senso utilizzare se il sito web si trova su un sito web WCM di terze parti. Tuttavia, se il sito web si trova in Adobe Experience Manager, un server di immagini offsite esegue il rendering dell&#39;immagine e la fornisce alla pagina web.

Vedi anche [Incorporare il visualizzatore video in una pagina web](embed-code.md).

Vedi anche [Collegare gli URL all’applicazione web](linking-urls-to-yourwebapplication.md).

**Per fornire immagini ottimizzate per un sito reattivo:**

1. Passa all’immagine per la quale desideri fornire codice reattivo e, nel menu a discesa, seleziona **[!UICONTROL Rendering]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >I predefiniti immagine vengono pubblicati automaticamente.

1. Seleziona **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. In **[!UICONTROL Incorpora immagine reattiva]** seleziona e copia il testo del codice reattivo e incollalo nel sito web per accedere alla risorsa reattiva.
1. Modifica i punti di interruzione predefiniti nel codice di incorporamento per trovare la corrispondenza con ciò che si trova nel sito web reattivo, direttamente nel codice. Inoltre, prova le diverse risoluzioni immagine fornite in diversi punti di interruzione della pagina.

## Utilizzo di HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media è supportata tramite HTTP/2, che fornisce tempi di risposta e caricamento migliori.

Vedi [Distribuzione di contenuti HTTP2](http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media.
