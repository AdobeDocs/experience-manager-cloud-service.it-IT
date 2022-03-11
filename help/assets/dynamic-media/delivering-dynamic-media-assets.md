---
title: Fornire risorse Dynamic Media
description: Scopri come distribuire le risorse Dynamic Media.
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 11%

---

# Fornire risorse Dynamic Media{#delivering-dynamic-media-assets}

La modalità di distribuzione delle risorse Dynamic Media, sia video che immagini, dipende da come viene implementato il sito web.

Con Dynamic Media hai diverse opzioni:

* Se il sito web è ospitato su Adobe Experience Manager, è necessario aggiungere le risorse Dynamic Media direttamente alla pagina.
* Se il tuo sito web non è disponibile come Experience Manager, puoi scegliere tra:

   * Incorporare il video o l’immagine sul sito web.
   * Collegamento degli URL all’applicazione Web. Utilizza il collegamento quando desideri distribuire un lettore video come finestra a comparsa o modale.
   * Se il sito è reattivo, puoi [fornire immagini ottimizzate](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>La funzione Smart imaging funziona con i predefiniti per immagini esistenti. Utilizza l&#39;intelligenza nell&#39;ultimo millisecondo di consegna per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Vedi [Imaging avanzato](/help/assets/dynamic-media/imaging-faq.md) per ulteriori informazioni.

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiungere risorse Dynamic Media alle pagine Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/dynamic-media/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Collegare gli URL all’applicazione Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Fornire immagini ottimizzate per un sito reattivo](/help/assets/dynamic-media/responsive-site.md)
* [Distribuzione di contenuti HTTP2](/help/assets/dynamic-media/http2faq.md)
* [Invalidare la cache CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidare la cache CDN tramite Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Utilizzare i set di regole per trasformare gli URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Distribuzione di risorse Dynamic Media HTTP/2 {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione dei contenuti HTTP/2](/help/assets/dynamic-media/http2faq.md).
