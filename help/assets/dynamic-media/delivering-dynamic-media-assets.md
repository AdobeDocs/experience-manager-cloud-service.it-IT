---
title: Distribuire Dynamic Media Assets
description: Scopri come distribuire risorse Dynamic Media alle pagine web tramite video e immagini incorporati o collegamenti di URL all’applicazione web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 7%

---

# Distribuire Dynamic Media Assets{#delivering-dynamic-media-assets}

Il modo in cui distribuisci le risorse Dynamic Media, sia video che immagini, dipende da come viene implementato il sito web.

Dynamic Media offre diverse opzioni:

* Se il tuo sito web è ospitato su Adobe Experience Manager, vuoi aggiungere le risorse Dynamic Media direttamente alla pagina.
* Se il tuo sito web non è su Experience Manager, puoi scegliere:

   * Incorporare il video o l’immagine sul sito web.
   * Collega gli URL all’applicazione web. Utilizza i collegamenti quando desideri distribuire un lettore video come finestra popup o modale.
   * Se il tuo sito è reattivo, puoi [distribuire immagini ottimizzate](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>L&#39;imaging avanzato funziona con i predefiniti immagine esistenti. Utilizza l&#39;intelligenza all&#39;ultimo millisecondo di consegna per ridurre ulteriormente le dimensioni del file di immagine in base alla velocità del browser o della connessione di rete. Per ulteriori informazioni, vedere [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md).

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiungere Dynamic Media Assets alle pagine web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/dynamic-media/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Collegare gli URL all’applicazione web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/dynamic-media/responsive-site.md)
* [Distribuzione HTTP2 dei contenuti](/help/assets/dynamic-media/http2faq.md)
* [Invalidare la cache CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidare la cache CDN tramite Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Utilizzare i set di regole per trasformare gli URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Distribuzione HTTP/2 delle risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione dei contenuti HTTP/2](/help/assets/dynamic-media/http2faq.md).
