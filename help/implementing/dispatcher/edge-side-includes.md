---
title: Il lato Edge include
description: Adobe Managed CDN ora supporta Edge Side Includes (ESI), un linguaggio di markup per l’assembly di contenuti web dinamici a livello di edge.
feature: Dispatcher
exl-id: 35093477-2788-4f69-80a9-899f43567cae
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 3%

---

# Il lato Edge include {#edge-side-includes}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, invia un messaggio e-mail a `aemcs-cdn-config-adopter@adobe.com` e descrivi il tuo caso d’uso.

La velocità di distribuzione dei contenuti deriva da un caching aggressivo delle pagine, ottenuto impostando intestazioni cache con valori TTL (High Time To Live) elevati. Questo può essere difficile quando le pagine includono contenuti dinamici, che devono essere aggiornati frequentemente o che potenzialmente non possono essere memorizzati nella cache. Fortunatamente, esistono strategie in cui la pagina HTML contenitore può essere memorizzata nella cache con un TTL elevato, posticipando il recupero dei frammenti di contenuto più dinamici a un momento successivo, tramite Javascript lato client o sulla rete CDN. Quest’ultimo approccio è uno standard denominato Edge Side Includes (ESI), supportato per i siti sottoposti a rendering con la pubblicazione AEM. Il HTML include tag ESI che indicano al CDN di rimandare la distribuzione della pagina al browser fino a quando non valuta tali tag, recuperando contenuto aggiuntivo più dinamico (TTL inferiore) dall’origine (o cache CDN se il relativo TTL non è scaduto).

Alcuni casi d’uso in cui l’opzione Edge Side Includes può essere utile:

* Visualizzazione del nome di un utente finale o di altre informazioni specifiche dell&#39;utente finale.
* Visualizzazione di un elenco di informazioni recenti, ad esempio articoli di notizie o quotazioni azionarie.

## Sintassi ESI {#esi-syntax}

La sintassi ESI è la seguente, se una pagina padre `/content/page.html` include uno snippet `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

Consulta la [Specifiche ESI](https://www.w3.org/TR/esi-lang/) per i dettagli.

### Considerazioni {#esi-syntax-considerations}

* Sono supportati i seguenti tag ESI: include, comment, remove.
* I tag ESI vengono elaborati in modo sequenziale anziché simultaneo alla rete CDN, pertanto molti tag ESI in una pagina con valori TTL bassi possono aggiungere latenza all’esperienza dell’utente finale.
* La profondità massima di ESI: elaborazione inclusa è 5.
* Il valore massimo totale ESI: include frammenti di elaborazione è 256.


## Configurazione Apache {#esi-apache}

Se disponi di pagine con tag ESI, è necessario dichiarare le seguenti proprietà nella configurazione di Apache:

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

Le proprietà configurate hanno il seguente comportamento:

| Proprietà | Comportamento |
|-----------|--------------------------|
| **no-gzip** | Se è impostato su 1, la pagina HTML viene trasmessa da Apache alla CDN non compressa. Ciò è necessario per ESI in quanto il contenuto deve essere inviato a CDN non compresso in modo che la CDN possa visualizzare e valutare i tag ESI.<br/><br/>Sia la pagina padre che i frammenti inclusi devono impostare no-gzip su 1.<br/><br/>Questa impostazione sostituisce qualsiasi impostazione di compressione Apache avrebbe potuto utilizzare altrimenti, in base al `Accept-Encoding` valori. |
| **x-aem-esi** | Se è impostata su &quot;on&quot;, la rete CDN valuterà i tag ESI della pagina HTML principale.  Per impostazione predefinita, l’intestazione non è impostata. |
| **x-aem-compress** | Se è impostata su &quot;on&quot;, la rete CDN comprimerà il contenuto dalla rete CDN al browser. Poiché la trasmissione della pagina padre da Apache a CDN deve essere non compressa affinché ESI funzioni (`no-gzip` impostato su 1), questo può ridurre la latenza.<br/><br/>Se questa intestazione non è impostata, quando la rete CDN recupera il contenuto dall’origine non compresso, distribuisce anche il contenuto al client non compresso. Pertanto, è necessario impostare questa intestazione se `no-gzip` è impostato su 1 (richiesto per ESI) e si desidera distribuire al browser il contenuto compresso dalla rete CDN. |

## Sling Dynamic Include {#esi-sdi}

Anche se non obbligatorio, [Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI) può essere utilizzato per generare snippet ESI interpretati sulla rete CDN.
