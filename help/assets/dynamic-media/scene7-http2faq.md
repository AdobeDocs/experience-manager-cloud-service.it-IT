---
title: HTTP2 Distribuzione dei contenuti - Domande frequenti
description: Informazioni sulla distribuzione dei contenuti HTTP2.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# HTTP2 Distribuzione dei contenuti - Domande frequenti{#http-delivery-of-content-faq}

Adobe è entusiasta di annunciare la disponibilità della distribuzione di contenuti HTTP/2. Con HTTP/2 noterete un aumento complessivo delle prestazioni.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni, riducendo al contempo la quantità di potenza di elaborazione necessaria.

Il seguente sito Web descrive HTTP/2 e i relativi vantaggi in modo semplice e breve:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

I miglioramenti in termini di prestazioni variano notevolmente in base a fattori quali il codice del sito Web, la modalità di utilizzo di Scene7, il dispositivo, lo schermo e la posizione del consumatore e così via.

I test eseguiti da Adobe hanno dato i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I vantaggi più notevoli in termini di prestazioni si sono registrati sui dispositivi iOS.
* Per i visualizzatori, i tempi di caricamento sono migliorati del 15%.

La dimostrazione seguente illustra la differenza tra il caricamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Usa HTTPS sicuro per le tue richieste rich media.
* Utilizzate la rete CDN (content delivery network, rete di distribuzione dei contenuti) fornita in Adobe nell&#39;ambito della licenza Dynamic Media Classic.
* Utilizzate un dominio dedicato ( `images.company.com` o `mycompany.scene7.com`), non un dominio Dynamic Media Classic generico (ovvero, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

   Per trovare i domini, [accedete all’istanza di Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) per ciascun account società.

   Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali. Cercate il campo con l’etichetta Nome **server** pubblicato. Se usate un dominio Scene7 generico, potete richiedere di passare al vostro dominio personalizzato come parte di questa transizione.

## Qual è la procedura per abilitare HTTP/2 per il mio account Dynamic Media Classic? {#what-is-the-process-for-enabling-http-for-my-scene-account}

È necessario avviare una richiesta di assistenza tecnica Adobe (`s7support@adobe.com`) per passare a HTTP/2; non viene eseguita automaticamente.

1. Nella richiesta di assistenza, fornite le seguenti informazioni:

   * Nome contatto principale, indirizzo e-mail e numero di telefono.
   * Tutti i domini da trasferire a HTTP2. Questo è, `images.company.com` o `mycompany.scene7.com`.
   Per trovare i domini, [accedete all’istanza di Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) per ciascun account società.

   Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali. Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato.

   * Verificate di utilizzare il protocollo HTTPS protetto per le richieste rich media.
   * Verifica di utilizzare la CDN tramite Adobe e di non essere gestito con una relazione diretta.
   * Verifica di utilizzare un dominio dedicato. ossia, `images.company.com` o `mycompany.scene7.com`, non un dominio Scene7 generico come `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.
   Per trovare i domini, [accedete all’istanza di Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) per ciascun account società.

   Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali. Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato. Se usate un dominio Scene7 generico, potete richiedere di passare al vostro dominio personalizzato come parte di questa transizione.

   1. Il supporto tecnico aggiunge all’elenco di attesa dei clienti HTTP/2 in base all’ordine in cui sono state inviate le richieste.
   1. Quando Adobe sarà pronta a gestire la richiesta, il supporto vi contatterà per coordinare la transizione e impostare una data di destinazione.
   1. Una volta completato il processo, riceverete una notifica e potrete verificare il corretto passaggio a HTTP2.



## Quando è possibile passare a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dal supporto tecnico.

>[!NOTE]
>
>Il tempo di attesa potrebbe essere lungo perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni cliente alla volta.

## Quali sono i rischi legati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta il passaggio a una nuova configurazione CDN.

Il contenuto non memorizzato nella cache arriva direttamente sui server di origine di Adobe fino alla ricostruzione della cache. Per questo motivo, Adobe pianifica di gestire alcune transizioni tra clienti alla volta, in modo da mantenere prestazioni accettabili quando si richiamano richieste dalla nostra origine.

## Come verificare se un URL o un sito Web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

È necessario scaricare un&#39;esternalizzazione da utilizzare con il browser Web. Per Firefox e Chrome esiste un&#39;estensione chiamata **[!UICONTROL HTTP/2 e SPDY Indicator]**. I browser supportano solo HTTP/2 in modo sicuro, pertanto è necessario chiamare un URL con HTTPS per la verifica. Se HTTP/2 è supportato, questo è indicato dall’estensione sotto forma di simbolo Flash blu e di intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
