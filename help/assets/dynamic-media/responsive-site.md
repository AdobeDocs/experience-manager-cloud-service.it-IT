---
title: Distribuzione di immagini ottimizzate per un sito reattivo
description: Scopri come utilizzare la funzione del codice reattivo per distribuire immagini ottimizzate da Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 15%

---

# Distribuzione di immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizza la funzione Codice reattivo per condividere il codice per il servizio reattivo con il tuo sviluppatore web. Il codice responsive (**[!UICONTROL RESS]**) viene copiato negli Appunti in modo da poterlo condividere con lo sviluppatore Web.

Questa funzione è utile se il sito web si trova su un WCM di terze parti. Tuttavia, se il tuo sito web si trova su Adobe Experience Manager, un server di immagini fuori sede esegue il rendering dell’immagine e la fornisce alla pagina web.

Vedi anche [Incorporare il Visualizzatore video in una pagina Web](embed-code.md).

Consulta anche [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

**Per distribuire immagini ottimizzate per un sito reattivo:**

1. Passa all&#39;immagine per la quale vuoi fornire il codice reattivo e seleziona **[!UICONTROL Rappresentazioni]** nel menu a discesa.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >I predefiniti per immagini vengono pubblicati automaticamente.

1. Selezionare **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Nella finestra di dialogo **[!UICONTROL Incorpora immagine reattiva]**, seleziona e copia il testo del codice reattivo e incollalo nel sito Web per accedere alla risorsa reattiva.
1. Modifica i punti di interruzione predefiniti nel codice di incorporamento in modo che corrispondano a quelli trovati nel sito web dinamico, direttamente nel codice. Inoltre, verifica le diverse risoluzioni dell’immagine distribuite in diversi punti di interruzione della pagina.

## Utilizzo di HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media è supportata tramite HTTP/2, che fornisce tempi di risposta e caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2faq.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con l&#39;account Dynamic Media.
