---
title: Distribuzione di risorse Dynamic Media
description: Scopri come distribuire risorse multimediali dinamiche
translation-type: tm+mt
source-git-commit: 5b55a339f466a7a0ffb4900c72e7d95995b28e83

---


# Distribuzione di risorse Dynamic Media{#delivering-dynamic-media-assets}

La modalità di distribuzione delle risorse multimediali dinamiche (video e immagini) dipende dall’implementazione del sito Web.

Con l’elemento multimediale dinamico hai a disposizione diverse opzioni:

* Se il sito web è ospitato su AEM, allora è necessario aggiungere le risorse dell’elemento multimediale dinamico direttamente sulla pagina.
* Se il sito Web non è su AEM, potete scegliere tra:

   * Incorporamento del video o dell’immagine nel sito Web.
   * Collegare gli URL all’applicazione Web. Usate il collegamento per distribuire un lettore video come finestra a comparsa o modale.
   * Se il sito è reattivo, potete [distribuire immagini ottimizzate.](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Per ulteriori informazioni, consultate [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) .

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiunta di risorse multimediali dinamiche alle pagine Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporazione di un visualizzatore video o di immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md)
* [Attivazione della protezione dei collegamenti ipertestuali in elementi multimediali dinamici](/help/assets/dynamic-media/hotlink-protection.md)
* [Collegamento di URL all&#39;applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/dynamic-media/responsive-site.md)
* [HTTP2 Distribuzione dei contenuti](/help/assets/dynamic-media/http2.md)
* [Invalidazione del contenuto cache CDN](/help/assets/dynamic-media/invalidate-cdn-cached-content.md)
* [Utilizzo dei set di regole per trasformare gli URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti multimediali dinamici (immagini e video) su HTTP/2. ossia un URL pubblicato o un codice da incorporare per l’immagine o il video può essere integrato con qualsiasi applicazione che accetta una risorsa ospitata. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [HTTP/2 Distribuzione di contenuti con domande](/help/assets/dynamic-media/scene7-http2faq.md) frequenti.
