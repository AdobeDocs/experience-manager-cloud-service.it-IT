---
title: Pubblicare risorse Dynamic Media
description: Scopri come pubblicare risorse video e immagini Dynamic Media in modo da poterle includere in una pagina web tramite un URL o incorporando codice in una pagina web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# Pubblicare risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Media, seleziona le risorse già caricate e seleziona **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Dopo la pubblicazione delle risorse Dynamic Media, queste sono disponibili per l’inclusione in una pagina web tramite un URL o tramite l’incorporamento di codice nella pagina.

Puoi anche pubblicare immediatamente le risorse caricate, senza alcun intervento da parte dell’utente. In alternativa, puoi pubblicare tali risorse in modo selettivo. Consulta [Configurare Dynamic Media](config-dm.md). In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Media o Adobe Experience Manager, escludendole a vicenda, utilizzando **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Vedi [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell&#39;ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già stata pubblicata, la risorsa viene spostata in un’altra cartella e ripubblicata dalla nuova posizione, la posizione originale della risorsa pubblicata rimane disponibile insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, viene persa in Experience Manager e non può essere annullata. Di conseguenza, come best practice, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, assicurati che sia eseguita la codifica. Quando i video vengono codificati, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, puoi pubblicare i video senza incorrere in errori di pubblicazione.

Consulta anche [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Vedi anche [Incorporare il visualizzatore di video Dynamic Media o il visualizzatore di immagini in una pagina Web](embed-code.md).

>[!NOTE]
>
>* Per utilizzare l’URL, è necessario pubblicare Assets. Se le risorse non sono pubblicate, non è possibile copiare e incollare l’URL in un browser web.
>* Per la distribuzione live, è necessario attivare e pubblicare i predefiniti immagine e i predefiniti visualizzatore.
>

Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, vedi [Pubblicazione di Assets](/help/assets/manage-digital-assets.md).

## Distribuzione HTTP/2 delle risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori di tutte le risorse Dynamic Media.

Consulta [Domande frequenti sulla distribuzione HTTP/2 del contenuto](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
