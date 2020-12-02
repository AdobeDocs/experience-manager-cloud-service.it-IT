---
title: Pubblicazione di risorse multimediali dinamiche
description: Come pubblicare le risorse multimediali dinamiche
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: b65ce0af6281f60272322744f0e6f81b7eb6b96a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Pubblicazione di risorse multimediali dinamiche {#publishing-dynamic-media-assets}

Per pubblicare le risorse per contenuti multimediali dinamici, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Dopo la pubblicazione, le risorse Dynamic Media sono disponibili per l’inclusione in una pagina Web tramite un URL o mediante l’incorporazione di codice nella pagina.

Potete anche pubblicare istantaneamente le risorse caricate, senza alcun intervento da parte dell’utente. In alternativa, potete pubblicare le risorse in modo selettivo. Consultate [Configurazione di contenuti multimediali dinamici.](config-dm.md) In alternativa, potete pubblicare selettivamente le risorse su elementi multimediali dinamici o AEM, escludendovi vicendevolmente tra di loro, utilizzando  **[!UICONTROL Pubblicazione selettiva a]** livello di cartella. Consultate [Utilizzo della pubblicazione selettiva nei file multimediali dinamici.](/help/assets/dynamic-media/selective-publishing.md)

Nella **[!UICONTROL vista a schede]**, un&#39;icona a forma di globo viene visualizzata direttamente sotto il nome di una risorsa e a sinistra della data e dell&#39;ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già pubblicata, usate AEM per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione, il percorso originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;perduta&quot; in AEM e non può essere annullata la pubblicazione. Di conseguenza, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendete pubblicare le risorse video subito dopo la codifica, accertatevi che la codifica sia stata completata. Quando i video vengono ancora codificati, il sistema segnala che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, dovreste essere in grado di visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro pubblicare i video senza che si verifichino errori di pubblicazione.

Vedere anche [Collegamento di URL all&#39;applicazione Web.](linking-urls-to-yourwebapplication.md)

Consultate anche [Incorporazione del visualizzatore video o del visualizzatore immagini per file multimediali dinamici in una pagina Web.](embed-code.md)

>[!NOTE]
>
>* Per usare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, non sarà possibile copiare e incollare l’URL in un browser Web.
>* I predefiniti per immagini e per visualizzatori devono essere attivati e pubblicati per la distribuzione live.

>



Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consultate [Pubblicazione delle risorse.](/help/assets/manage-digital-assets.md)

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti multimediali dinamici (immagini e video) su HTTP/2. ossia un URL pubblicato o un codice da incorporare per l’immagine o il video può essere integrato con qualsiasi applicazione che accetta una risorsa ospitata. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, vedere [Distribuzione HTTP/2 del contenuto alle domande frequenti](/help/assets/dynamic-media/http2faq.md).
<!--this md file used to reside under sites-administering-->
