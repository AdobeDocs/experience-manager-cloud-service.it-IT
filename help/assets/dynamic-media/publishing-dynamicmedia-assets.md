---
title: Pubblicazione delle risorse Dynamic Media
description: Scopri come pubblicare risorse Dynamic Media.
contentOwner: Rick Brough
feature: Gestione risorse
topic: Professionista
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 5%

---


# Pubblicazione delle risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Media, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Dopo la pubblicazione delle risorse Dynamic Media, sono disponibili per l’inclusione in una pagina web tramite un URL o tramite l’incorporamento di codice nella pagina.

Puoi anche pubblicare istantaneamente le risorse caricate senza alcun intervento da parte dell’utente. In alternativa, puoi pubblicare selettivamente tali risorse. Consulta [Configurazione di Dynamic Media.](config-dm.md) In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Media o AEM, reciprocamente esclusive, utilizzando  **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Consulta [Utilizzo della pubblicazione selettiva in Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già stata pubblicata, utilizza AEM per spostarla in un’altra cartella e ripubblicarla dalla nuova posizione, la posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in AEM e non può essere annullata. Pertanto, come best practice, annulla la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, accertati che la codifica sia completa. Quando i video vengono ancora codificati, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, dovresti essere in grado di visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro per te pubblicare i video senza che si verifichino errori di pubblicazione.

Vedere anche [Collegamento di URL all&#39;applicazione Web.](linking-urls-to-yourwebapplication.md)

Consulta anche [Incorporare il visualizzatore video o immagine Dynamic Media in una pagina web.](embed-code.md)

>[!NOTE]
>
>* Per utilizzare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, non sarà possibile copiare e incollare l’URL in un browser web.
>* I predefiniti per immagini e visualizzatori devono essere attivati e pubblicati per la distribuzione in diretta.

>



Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicazione di risorse.](/help/assets/manage-digital-assets.md)

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Distribuzione HTTP/2 dei contenuti con domande frequenti](/help/assets/dynamic-media/http2faq.md) .
<!--this md file used to reside under sites-administering-->
