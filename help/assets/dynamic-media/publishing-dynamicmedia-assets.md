---
title: Pubblicare risorse Dynamic Media
description: Scopri come pubblicare risorse di immagini e video Dynamic Medie in modo da poterle includere in una pagina web tramite un URL o incorporando codice in una pagina web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 4%

---

# Pubblicare risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Medie, seleziona le risorse già caricate e fai clic su **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Una volta pubblicate, le risorse Dynamic Medie possono essere incluse in una pagina web tramite URL o tramite l’incorporamento di codice nella pagina.

Puoi anche pubblicare immediatamente le risorse caricate, senza alcun intervento da parte dell’utente. In alternativa, puoi pubblicare tali risorse in modo selettivo. Consulta [Configurare Dynamic Medie](config-dm.md). In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Medie o Adobe Experience Manager, escludendovi a vicenda, utilizzando **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Consulta [Utilizzare la pubblicazione selettiva in Dynamic Medie](/help/assets/dynamic-media/selective-publishing.md).

In **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa e a sinistra della data e dell’ora viene visualizzata una piccola icona a forma di globo, per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già stata pubblicata, la risorsa viene spostata in un’altra cartella e ripubblicata dalla nuova posizione, la posizione originale della risorsa pubblicata rimane disponibile insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, viene persa per Experience Manager e non può essere annullata. Di conseguenza, come best practice, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, assicurati che sia eseguita la codifica. Quando i video vengono codificati, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, puoi pubblicare i video senza incorrere in errori di pubblicazione.

Vedi anche [Collegare gli URL all’applicazione web](linking-urls-to-yourwebapplication.md).

Vedi anche [Incorporare il visualizzatore di video Dynamic Medie o il visualizzatore di immagini in una pagina web](embed-code.md).

>[!NOTE]
>
>* Per utilizzare l&#39;URL, le risorse devono essere pubblicate. Se le risorse non sono pubblicate, non è possibile copiare e incollare l’URL in un browser web.
>* Per la distribuzione live, è necessario attivare e pubblicare i predefiniti immagine e i predefiniti visualizzatore.
>

Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicazione delle risorse](/help/assets/manage-digital-assets.md).

## Distribuzione HTTP/2 delle risorse Dynamic Medie {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Medie (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori per tutte le risorse Dynamic Medie.

Consulta [Domande frequenti sulla distribuzione HTTP/2 dei contenuti](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
