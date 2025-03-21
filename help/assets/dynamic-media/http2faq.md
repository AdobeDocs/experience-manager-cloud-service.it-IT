---
title: Domande frequenti sulla distribuzione dei contenuti HTTP2
description: Scopri la distribuzione di contenuti HTTP2 e come migliora la comunicazione tra browser e server per un trasferimento più rapido delle informazioni.
contentOwner: Rick Brough
feature: Dynamic Media,Configuration,FAQ
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 3%

---

# Domande frequenti sulla distribuzione dei contenuti HTTP2{#http-delivery-of-content-faq}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Adobe è entusiasta di annunciare la disponibilità della distribuzione HTTP/2 dei contenuti. Quando si utilizza HTTP/2, si verifica un aumento complessivo delle prestazioni.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete per la distribuzione dei contenuti standard, inclusa in Adobe Experience Manager - Dynamic Media. Con questa funzione non è supportata alcuna rete di distribuzione di contenuti personalizzata.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui browser e server comunicano, consentendo un trasferimento più rapido delle informazioni e riducendo la quantità di potenza di elaborazione necessaria.

L&#39;articolo del sito Web [Informazioni su HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html) descrive HTTP/2 e i relativi vantaggi in modo breve e semplice.

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Il miglioramento delle prestazioni varia notevolmente perché si basa su vari fattori. Ad esempio, il codice del tuo sito web, come utilizzi Dynamic Media, il dispositivo del consumatore, lo schermo e la posizione.

I test eseguiti da Adobe hanno prodotto i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I miglioramenti delle prestazioni più importanti si sono verificati sui dispositivi iOS.
* Per i visualizzatori, il tempo di caricamento è aumentato del 15%.

La dimostrazione seguente illustra la differenza tra il caricamento di HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Utilizza HTTPS sicuro per le richieste rich media.
* Utilizza la rete CDN (Content Delivery Network) inclusa in Adobe come parte della licenza Dynamic Media Classic.
* Utilizza un dominio dedicato (ovvero `images.company.com` o `mycompany.scene7.com`), non un dominio Dynamic Media generico (ovvero `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

  Per trovare i domini, apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

  Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cercare il campo con etichetta **Nome server pubblicato**. Se attualmente utilizzi un dominio Dynamic Media generico, puoi richiedere di passare al dominio personalizzato come parte di questa transizione.

## Qual è il processo per abilitare HTTP/2 per il mio account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Utilizzare Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) e richiedere il passaggio a HTTP/2. Questa operazione non viene eseguita automaticamente.

1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Nome del contatto principale, e-mail e numero di telefono.
   * Tutti i domini da trasferire su HTTP2. ovvero `images.company.com` o `mycompany.scene7.com`.

   Per trovare i domini, apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cercare il campo con etichetta **[!UICONTROL Nome server pubblicato]**.

   * Verifica di utilizzare HTTPS sicuro per le richieste rich media.
   * Verifica di utilizzare la rete CDN tramite Adobe e non gestita con una relazione diretta.
   * Verifica di utilizzare un dominio dedicato. `images.company.com` o `mycompany.scene7.com`, non è un dominio Dynamic Media generico come `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Per trovare i domini, apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cercare il campo con etichetta **[!UICONTROL Nome server pubblicato]**. Se attualmente utilizzi un dominio Dynamic Media generico, puoi richiedere di passare al dominio personalizzato come parte di questa transizione.

   1. L’Assistenza clienti ti aggiunge alla lista di attesa dei clienti HTTP/2 in base all’ordine in cui sono state inviate le richieste.
   1. Quando Adobe è pronto a gestire la richiesta, l’Assistenza clienti ti contatta per coordinare la transizione e impostare una data di scadenza.
   1. Ricevi una notifica dopo il completamento e puoi verificare che la transizione su HTTP2 sia andata a buon fine.

## Quando è prevista la transizione a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti.

>[!NOTE]
>
>Il lead time è lungo perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo poche transizioni cliente alla volta.

## Quali sono i rischi associati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta lo spostamento a una nuova configurazione della rete CDN.

Il contenuto non memorizzato in cache colpisce direttamente i server di origine di Adobe fino a quando la cache non viene nuovamente generata. A causa di questa azione, Adobe prevede di gestire alcune transizioni cliente alla volta. Questo metodo garantisce il mantenimento di prestazioni accettabili durante il richiamo delle richieste dall’origine.

## Come verificare se un URL o un sito web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Scarica un’estensione da utilizzare con il browser web. Per Firefox e Chrome, esiste un&#39;estensione denominata **[!UICONTROL HTTP/2 e SPDY Indicator]**. I browser supportano solo HTTP/2 in modo sicuro, pertanto è necessario chiamare un URL con HTTPS per verificare. Se HTTP/2 è supportato, è indicato dall’estensione sotto forma di un simbolo Flash blu e di un’intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
