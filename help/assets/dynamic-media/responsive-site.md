---
title: Distribuzione di immagini ottimizzate per un sito reattivo
description: Scopri come utilizzare la funzione di codice reattivo per distribuire immagini ottimizzate da Dynamic Media.
feature: Gestione risorse
role: Business Practitioner
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 13%

---

# Distribuzione di immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizza la funzione Codice reattivo quando desideri condividere il codice per il servizio reattivo con il tuo sviluppatore web. Puoi copiare il codice reattivo (**[!UICONTROL RESS]**) negli appunti per condividerlo con lo sviluppatore web.

Questa funzione ha senso utilizzare se il sito web si trova su un sito web WCM di terze parti. Tuttavia, se il sito web si trova in Adobe Experience Manager, un server di immagini offsite esegue il rendering dell&#39;immagine e la fornisce alla pagina web.

Vedere anche [Incorporamento del visualizzatore video in una pagina Web](embed-code.md).

Consulta anche [Collegamento di URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

**Per fornire immagini ottimizzate per un sito reattivo:**

1. Passa all’immagine per la quale desideri fornire codice reattivo e, nel menu a discesa, tocca **[!UICONTROL Rendering]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >I predefiniti immagine vengono pubblicati automaticamente.

1. Toccare **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Nella finestra di dialogo **[!UICONTROL Incorpora immagine reattiva]** , seleziona e copia il testo del codice reattivo e incollalo nel sito Web per accedere alla risorsa reattiva.
1. Modifica i punti di interruzione predefiniti nel codice di incorporamento per trovare la corrispondenza con ciò che si trova nel sito web reattivo, direttamente nel codice. Inoltre, prova le diverse risoluzioni immagine fornite in diversi punti di interruzione della pagina.

## Utilizzo di HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media è supportata tramite HTTP/2, che fornisce tempi di risposta e caricamento migliori.

Per informazioni dettagliate su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media, consulta [Distribuzione di contenuti HTTP2](http2faq.md) .
