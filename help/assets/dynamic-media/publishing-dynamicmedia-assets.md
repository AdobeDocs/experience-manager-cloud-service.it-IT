---
title: Pubblicazione delle risorse Dynamic Media
description: Scopri come pubblicare risorse Dynamic Media.
contentOwner: Rick Brough
feature: Gestione risorse
role: Business Practitioner
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 5%

---

# Pubblicazione delle risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Media, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Dopo la pubblicazione delle risorse Dynamic Media, sono disponibili per l’inclusione in una pagina web tramite un URL o tramite l’incorporamento di codice nella pagina.

Puoi anche pubblicare istantaneamente le risorse caricate senza alcun intervento da parte dell’utente. In alternativa, puoi pubblicare selettivamente tali risorse. Consulta [Configurazione di Dynamic Media](config-dm.md). In alternativa, puoi pubblicare in modo selettivo le risorse su Dynamic Media o Adobe Experience Manager, escludendole a vicenda, utilizzando **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Consulta [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già pubblicata, sposta la risorsa in un’altra cartella e ripubblica dalla sua nuova posizione, la posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa ripubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in Experience Manager e non può essere annullata. Pertanto, come best practice, annulla la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, accertati di effettuare la codifica. Quando i video vengono codificati, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro per te pubblicare i video senza che si verifichino errori di pubblicazione.

Consulta anche [Collegamento di URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consulta anche [Incorporare il visualizzatore video o immagine Dynamic Media in una pagina web](embed-code.md).

>[!NOTE]
>
>* Per utilizzare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, la copia e l’incolla dell’URL in un browser web non funziona.
>* I predefiniti per immagini e visualizzatori devono essere attivati e pubblicati per la distribuzione in diretta.

>



Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicazione di risorse](/help/assets/manage-digital-assets.md).

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Consulta [Distribuzione HTTP/2 del contenuto delle domande frequenti](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
