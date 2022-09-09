---
title: Best practice relative alla gestione di SEO (Search Engine Optimization) e URL per Adobe Experience Manager as a Cloud Service
description: Best practice relative alla gestione di SEO (Search Engine Optimization) e URL per Adobe Experience Manager as a Cloud Service
exl-id: abe3f088-95ff-4093-95a1-cfc610d4b9e9
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '3714'
ht-degree: 75%

---

# Best practice relative alla gestione di SEO (Search Engine Optimization) e URL per Adobe Experience Manager as a Cloud Service {#seo-and-url-management-best-practices-for-aem}

L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. È quindi necessario affrontare questo tipo di ottimizzazione in numerosi progetti Adobe Experience Manager (AEM) as a Cloud Service.

Questo documento fornisce innanzitutto alcuni consigli e [best practice relativi all’ottimizzazione SEO (Search Engine Optimization)](#seo-best-practices), utili per affrontarla in un’implementazione di AEM as a Cloud Service. Vengono quindi approfonditi alcuni dei [passaggi di implementazione più complessi](#aem-configurations) illustrati nella prima sezione.

## Best practice per l’ottimizzazione SEO {#seo-best-practices}

Questa sezione descrive alcune best practice generali relative all’ottimizzazione SEO (Search Engine Optimization).

### URL {#urls}

Negli URL sono presenti alcune best practice accettate.

Durante la valutazione degli URL nel progetto AEM, considera le seguenti domande:

*&quot;Se un utente visualizza questo URL e nessuno dei contenuti della pagina, potrebbe descrivere la pagina?&quot;*

Se la risposta è sì, è probabile che l’URL funzioni correttamente per un motore di ricerca.

Ecco alcuni suggerimenti di carattere generale su come creare URL per l’ottimizzazione SEO (Search Engine Optimization):

* Separa le parole con un trattino.

   * Usa i trattini (-) come separatori nei nomi delle pagine.
   * Evita di usare la notazione camel, caratteri di sottolineatura e spazi.

* Se possibile, evita l’uso di parametri di query. In caso di necessità, limitali a un massimo di due.

   * Utilizza la struttura di directory per indicare l’architettura delle informazioni, se disponibile.
   * Se una struttura di directory non è un’opzione, utilizza i selettori Sling nell’URL anziché le stringhe di query. Oltre al valore SEO fornito, i selettori Sling rendono le pagine memorizzabili in cache per il Dispatcher.

* Più un URL è leggibile dall&#39;uomo, meglio è; se nell’URL sono presenti parole chiave, viene incrementato il valore.

   * Se utilizzi selettori in una pagina, scegli quelli che forniscono valori semantici.
   * Se un utente non riesce a interpretare l’URL, non può farlo nemmeno un motore di ricerca.
   * Ad esempio:
      `mybrand.com/products/product-detail.product-category.product-name.html`
è da preferirsi a 
`mybrand.com/products/product-detail.1234.html`

* Evita i sottodomini quando possibile, in quanto i motori di ricerca li considerano come entità diverse, frammentando il valore SEO del sito.

   * Utilizza invece percorsi secondari di primo livello. Ad esempio, usa `www.mybrand.com/es/home.html` invece di `es.mybrand.com/home.html`.

   * Pianifica la gerarchia dei contenuti in modo che corrisponda alla modalità di presentazione, in base a questa linea guida.

* Le parole chiave negli URL perdono efficacia se si trovano in URL lunghi e se non sono posizionate all’inizio. In altre parole, scegli URL brevi.

   * Utilizza le tecniche e le funzioni di abbreviazione degli URL fornite da AEM per rimuovere gli elementi superflui.
   * Ad esempio, `mybrand.com/en/myPage.html` è da preferirsi a `mybrand.com/content/my-brand/en/myPage.html`.

* Utilizza URL canonici.

   * Quando un URL può essere gestito da percorsi diversi o con parametri o selettori diversi, assicurati di usare un tag `rel=canonical` nella pagina.

   * Questo tag può essere incluso nel codice del modello AEM.

* Se possibile, fai in modo che l’URL corrisponda al titolo della pagina.

   * Invita gli autori dei contenuti a seguire questa pratica.

* Non richiedere il rispetto della distinzione tra maiuscole/minuscole nelle richieste URL.

   * Configura Dispatcher per riscrivere tutte le richieste in entrata come lettere minuscole.
   * Chiedi agli autori di contenuti di creare tutte le pagine utilizzando solo lettere minuscole.

* Assicurati che ogni pagina sia gestita da un solo protocollo.

   * A volte i siti vengono gestiti tramite `http` fino a quando l’utente non raggiunge una pagina contenente, ad esempio, un modulo di pagamento o di accesso, che viene gestito tramite `https`. Quando si effettua il collegamento da questa pagina, se l&#39;utente può tornare a `http` pagine e accedili tramite `https`, il motore di ricerca li tiene traccia come due pagine separate.

   * Google attualmente preferisce le pagine `https` a quelle `http`. Per questo motivo è spesso preferibile gestire l’intero sito tramite `https`.

### Configurazione del server {#server-configuration}

Dal punto di vista della configurazione del server, puoi adottare le seguenti misure per garantire che venga effettuata la ricerca per indicizzazione solo del contenuto corretto:

* Utilizza un file `robots.txt` per bloccare la ricerca per indicizzazione di qualsiasi contenuto che non deve essere indicizzato.

   * Blocca **tutte** le operazioni di ricerca per indicizzazione negli ambienti di test.

* Quando lanci un nuovo sito con URL aggiornati, implementa i reindirizzamenti 301 per non perdere il tuo ranking SEO esistente.
* Includi un favicon per il tuo sito.
* Implementa una mappa del sito XML per facilitare la ricerca per indicizzazione del contenuto da parte dei motori di ricerca. Assicurati di includere una mappa del sito mobile per i siti mobili e/o reattivi.

## Configurazioni AEM {#aem-configurations}

Questa sezione descrive i passaggi di implementazione necessari per configurare AEM in modo che segua queste raccomandazioni SEO (Search Engine Optimization).

### Utilizzo dei selettori Sling {#using-sling-selectors}

In precedenza, l’utilizzo dei parametri di query era la pratica accettata durante la creazione di un’applicazione web aziendale.

Negli ultimi anni la tendenza è stata quella di rimuoverli in modo che gli URL siano più leggibili. Su molte piattaforme, questo approccio comporta l’implementazione di reindirizzamenti sul server web o sulla rete CDN (Content Delivery Network), ma grazie a Sling questa operazione è estremamente semplice. I selettori Sling:

* Migliorano la leggibilità degli URL.
* Consente di memorizzare le pagine nella cache del Dispatcher, spesso migliorando la sicurezza.
* Consentono di gestire il contenuto direttamente, invece di utilizzare un servlet generico per il recupero del contenuto. Questo ti offre i vantaggi degli ACL applicati al tuo archivio e i filtri applicati al Dispatcher.

#### Utilizzo dei selettori per i servlet {#using-selectors-for-servlets}

AEM offre due opzioni per la scrittura di servlet:

* Servlet **bin**
* Servlet **Sling**

Gli esempi seguenti illustrano come registrare i servlet che seguono entrambi questi modelli e i vantaggi ottenuti utilizzando i servlet Sling.

#### Servlet Bin (un livello inferiore) {#bin-servlets-one-level-down}

I servlet **Bin** sono conformi al modello a cui molti sviluppatori sono abituati dalla programmazione J2EE. Il servlet viene registrato in un percorso specifico, che nel caso di AEM si trova in genere in `/bin`. I parametri di richiesta necessari vengono estratti dalla stringa di query.

L’annotazione SCR per questo tipo di servlet sarà simile al seguente:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Estrai quindi i parametri dalla stringa di query tramite l’oggetto `SlingHttpServletRequest` incluso nel metodo `doGet`; ad esempio:

```
String myParam = req.getParameter("myParam");
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Con questo approccio ci sono alcuni aspetti da considerare:

* L’URL stesso perde valore SEO. Gli utenti che accedono al sito, inclusi i motori di ricerca, non ricevono alcun valore semantico dall’URL, in quanto l’URL rappresenta un percorso programmatico e non la gerarchia dei contenuti.
* La presenza di parametri di query nell’URL impedisce a Dispatcher di memorizzare la risposta nella cache.
* Se vuoi proteggere questo servlet, devi implementare una logica di sicurezza personalizzata nel servlet.
* Il Dispatcher deve essere configurato con attenzione per esporre `/bin/myApp/myServlet`. La semplice esposizione di `/bin` consentirebbe l’accesso a determinati servlet che non dovrebbero essere aperti ai visitatori del sito.

#### Servlet Sling (un livello inferiore) {#sling-servlets-one-level-down}

I servlet **Sling** permettono di registrare il servlet in modo opposto. Invece di gestire un servlet e specificare il contenuto di cui vuoi eseguire il rendering in base ai parametri di query, devi indirizzare il contenuto desiderato e specificare il servlet che deve eseguire il rendering del contenuto in base ai selettori Sling.

L’annotazione SCR per questo tipo di servlet sarà simile al seguente:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

In questo caso, la risorsa gestita dall’URL (un’istanza della risorsa `myPageType`) è accessibile automaticamente nel servlet. Per accedervi, chiama:

```
Resource myPage = req.getResource();
```

L’URL risultante usato sarà simile al seguente:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

I vantaggi di questo approccio sono i seguenti:

* Puoi incorporare valore SEO (Search Engine Optimization), ottenuto dalla semantica presente nella gerarchia del sito e nel nome della pagina.
* Poiché non sono presenti parametri di query, Dispatcher può memorizzare la risposta nella cache. Inoltre, eventuali aggiornamenti apportati alla pagina gestita annullano la validità della cache quando la pagina viene attivata.
* Tutti gli ACL applicati a `/content/my-brand/my-page` entra in vigore quando un utente prova ad accedere a questo servlet.
* Dispatcher sarà già configurato per distribuire questo contenuto in funzione del servizio del sito web. Non è richiesta alcuna configurazione aggiuntiva.

### Riscrittura di URL {#url-rewriting}

In AEM, tutte le pagine web vengono memorizzate in `/content/my-brand/my-content`. Anche se questo approccio può essere utile dal punto di vista della gestione dati dell’archivio, non corrisponde necessariamente al modo in cui i clienti devono esplorare il sito e può entrare in conflitto con le indicazioni SEO che richiedono di utilizzare URL brevi. Inoltre, puoi servire più siti web dalla stessa istanza AEM e da nomi di dominio diversi.

Questa sezione esamina le opzioni disponibili in AEM per gestire questi URL e presentarli agli utenti in modo più leggibile e compatibile con SEO.

#### Gli URL personalizzati {#vanity-urls}

Se un autore vuole che una pagina sia accessibile da una seconda posizione a scopo promozionale, potrebbe essere utile utilizzare gli URL personalizzati di AEM, definiti pagina per pagina. Per aggiungere un URL personalizzato a una pagina, passa alla pagina nella console **Sites** e modifica le proprietà della pagina. Nella parte inferiore della scheda **Base**, è disponibile una sezione in cui è possibile aggiungere URL personalizzati. Tieni presente che l’accesso alla pagina tramite più URL comporterà la frammentazione del valore SEO della pagina. Per evitare questo problema è quindi necessario aggiungere alla pagina un tag di URL canonico.

#### Nomi di pagina localizzati {#localized-page-names}

Può essere necessario visualizzare i nomi delle pagine localizzate agli utenti del contenuto tradotto. Ad esempio:

* L’URL visualizzato da un utente di lingua spagnola non dovrebbe essere:
   `www.mydomain.com/es/home.html`

* Ma sarebbe meglio che fosse:
   `www.mydomain.com/es/casa.html`.

Il problema correlato alla localizzazione del nome della pagina è che molti degli strumenti di localizzazione disponibili sulla piattaforma AEM dipendono dalla corrispondenza dei nomi delle pagine tra diverse lingue per garantire la sincronizzazione del contenuto.

Per risolvere questo problema, puoi utilizzare la proprietà `sling:alias`. Puoi aggiungere `sling:alias` come proprietà a qualsiasi risorsa per consentire l’utilizzo di un nome di alias della risorsa. Nell’esempio precedente, avrai:

* Una pagina nel JCR in:
   `…/es/home`

* Una proprietà aggiunta a tale pagina:
   `sling:alias` = `casa`

In questo modo gli strumenti di traduzione di AEM, come l’utilità di gestione di più siti, continueranno a mantenere una relazione tra:

* `/en/home`

* `/es/home`

Allo stesso tempo gli utenti finali potranno interagire con il nome della pagina nelle rispettive lingue native.

>[!NOTE]
>
>È possibile impostare la proprietà `sling:alias` utilizzando la [proprietà Alias durante la modifica delle proprietà della pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced).

#### /etc/map {#etc-map}

In un’installazione standard di AEM:

* per la configurazione OSGi
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* la proprietà
   **Mapping Location** (Posizione mappatura) ( `resource.resolver.map.location`)

* viene impostata sul valore predefinito `/etc/map`.

È possibile aggiungere definizioni di mappatura in questa posizione per mappare le richieste in entrata, riscrivere gli URL nelle pagine in AEM o eseguire entrambe le operazioni.

Per creare una mappatura, crea una `sling:Mapping` nodo in questa posizione sotto `/http` o `/https`. In base alle proprietà `sling:match` e `sling:internalRedirect` impostate su questo nodo, AEM reindirizzerà tutto il traffico dell’URL corrispondente al valore specificato nella proprietà `internalRedirect`.

Anche se questo è l’approccio illustrato nella documentazione ufficiale di AEM e Sling, il supporto delle espressioni regolari fornito da questa implementazione ha un ambito limitato rispetto alle opzioni disponibili quando si utilizza direttamente `SlingResourceResolver`. Inoltre, l’implementazione delle mappature in questo modo può causare problemi con l’annullamento della validità della cache del Dispatcher.

Ecco un esempio di scenario in cui si verifica questo problema:

1. Un utente visita il sito web e richiede `https://www.mydomain.com/my-page.html`
1. Dispatcher inoltra questa richiesta al server di pubblicazione.
1. Con `/etc/map`, il server di pubblicazione risolve la richiesta in `/content/my-brand/my-page` ed esegue il rendering della pagina.

1. Il Dispatcher memorizza in cache la risposta in `/my-page.html` e restituisce la risposta all&#39;utente.
1. Un autore di contenuti modifica e attiva la pagina.
1. L’agente di flush del Dispatcher invia una richiesta di annullamento della validità per `/content/my-brand/my-page`**.** Poiché il Dispatcher non ha una pagina memorizzata nella cache in questo percorso, il contenuto precedente rimane memorizzato nella cache e non aggiornato.

Esistono modi per configurare regole di eliminazione dell’invio personalizzate che associano l’URL più breve all’URL più lungo a scopo di annullamento della validità della cache.

Esiste però anche una soluzione più semplice per gestire questo problema:

1. **Regole di SlingResourceResolver**

   Utilizzando la console web, ad esempio localhost:4502/system/console/configMgr, puoi configurare Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   È consigliabile creare le mappature necessarie per ridurre gli URL come espressioni regolari, quindi definire queste configurazioni in un nodo OsgiConfignode, `config.publish`, incluso nella build.

   Invece di definire le mappature in `/etc/map`, puoi assegnarle direttamente alla proprietà **URL Mappings** (Mappature URL) ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   In questo semplice esempio rimuoverai `/content/my-brand/` dall’inizio di tutti gli URL in cui è presente.

   In questo modo un URL viene convertito:

   * da `/content/my-brand/my-page.html`
   * a semplicemente `/my-page.html`

   Questo approccio è in linea con la pratica consigliata di ridurre la lunghezza degli URL.

1. **Mappatura dell’output degli URL nelle pagine**

   Dopo aver definito le mappature in Apache Sling Resource Resolver, devi utilizzarle nei componenti per garantire che gli URL generati nelle pagine siano brevi e leggibili. Per farlo, puoi utilizzare la funzione di mappatura di `ResourceResolver`.

   Se, ad esempio, stai implementando un componente di navigazione personalizzato che elenca gli elementi secondari della pagina corrente, puoi utilizzare il metodo di mappatura nel modo seguente:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### mod_rewrite di Apache HTTP Server {#apache-http-server-mod-rewrite}

Finora, hai implementato le mappature unitamente alla logica presente nei tuoi componenti per utilizzarle durante la creazione dell’output degli URL nelle pagine.

L’ultimo tassello del puzzle è la gestione di questi URL abbreviati quando arrivano al Dispatcher, che è dove `mod_rewrite` entra in gioco. Il più grande vantaggio dell&#39;utilizzo `mod_rewrite` è che gli URL sono mappati nuovamente sulla loro forma lunga *prima* vengono inviati al modulo Dispatcher. Ciò significa che Dispatcher richiede l’URL lungo dal server di pubblicazione e lo memorizza in cache di conseguenza. Pertanto, qualsiasi svuotamento del Dispatcher proveniente dal server di pubblicazione può annullare la validità di questo contenuto.

Per implementare queste regole, puoi aggiungere elementi `RewriteRule` nell’host virtuale della configurazione di Apache HTTP Server. Se vuoi espandere gli URL abbreviati dell’esempio precedente, puoi implementare una regola simile alla seguente:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Tag di URL canonici {#canonical-url-tags}

I tag URL canonici sono tag di collegamento inseriti nell’intestazione di un documento HTML che consentono di definire la modalità di gestione di una pagina nei motori di ricerca durante l’indicizzazione del contenuto. Il vantaggio offerto è quello di garantire che una pagina (versioni diverse di) sia indicizzata allo stesso modo anche quando l’URL della pagina può contenere differenze.

Se, ad esempio, un sito include una versione di una pagina adatta alla stampa, un motore di ricerca indicizza tale pagina separatamente dalla versione normale della stessa pagina. Il tag canonico indica al motore di ricerca che sono uguali.

Esempi:

* `<https://www.mydomain.com/my-brand/my-page.html>`
* `<https://www.mydomain.com/my-brand/my-page.print.html>`

Per entrambi viene applicato il seguente tag all’intestazione della pagina:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

Il valore `href` può essere relativo o assoluto. Per determinare l’URL canonico per la pagina e generare questo tag, il codice deve essere incluso nel markup della pagina.

### Configurazione di Dispatcher per la distinzione tra maiuscole e minuscole {#configuring-the-dispatcher-for-case-insensitivity}

Secondo la best practice, è consigliabile utilizzare solo lettere minuscole nei nomi di pagina. Se, però, non vuoi che un utente riceva un errore 404 quando accede al sito web utilizzando lettere maiuscole nell’URL, Adobe consiglia di aggiungere nella configurazione di Apache HTTP Server una regola di riscrittura per mappare tutti gli URL in arrivo utilizzando lettere minuscole. Inoltre, gli autori dei contenuti devono essere formati per creare le pagine con nomi in minuscolo.

Per configurare Apache in modo che per tutto il traffico in entrata vengano utilizzate lettere minuscole, aggiungi quanto segue alla configurazione di `vhost`:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Inoltre, aggiungi quanto segue nella parte superiore della `htaccess` file:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementazione di robots.txt per proteggere gli ambienti di sviluppo {#implementing-robots-txt-to-protect-development-environments}

I motori di ricerca *devono* verificare la presenza di un file `robots.txt` nella directory principale del sito prima di eseguire la ricerca per indicizzazione del sito. Mentre i principali motori di ricerca come Google, Yahoo o Bing lo rispettano tutti, alcuni motori di ricerca stranieri no.

Il modo più semplice per bloccare l’accesso all’intero sito consiste nell’inserire nella directory principale del sito un file denominato `robots.txt` con il seguente contenuto:

```xml
User-agent: *
Disallow: /
```

In alternativa, in un ambiente live, puoi scegliere di non consentire l’indicizzazione di determinati percorsi.

La avvertenza di posizionare il `robots.txt` nella directory principale del sito è possibile che le richieste di eliminazione del Dispatcher cancellino questo file e le mappature URL posizionano probabilmente la directory principale del sito in un punto diverso da quello del `DOCROOT` come definito nella configurazione di Apache HTTP Server. Per questo motivo, questo file viene in genere inserito nell’istanza di authoring nella directory principale del sito e replicato nell’istanza di pubblicazione.

### Creazione di una mappa del sito XML in AEM {#building-an-xml-sitemap-on-aem}

I crawler utilizzano le mappe del sito XML per comprendere meglio la struttura dei siti web. Sebbene non vi sia alcuna garanzia che la creazione di una mappa del sito porti a una migliore classificazione SEO, si tratta di una best practice concordata. Puoi gestire manualmente un file XML sul server web da utilizzare come mappa del sito, ma è consigliabile generarla a livello di programmazione, in modo che, quando gli autori creano contenuti, le modifiche apportate vengano applicate automaticamente alla mappa del sito.

AEM utilizza il [Modulo Sling Sitemap di Apache](https://github.com/apache/sling-org-apache-sling-sitemap) per generare sitemap XML. Questo fornisce un’ampia gamma di opzioni per gli sviluppatori e gli editor per mantenere aggiornata una sitemap XML dei siti.

Il modulo Sling Sitemap di Apache distingue tra una mappa del sito di primo livello e una mappa del sito nidificata, entrambe generate per qualsiasi risorsa con il `sling:sitemapRoot` proprietà impostata su `true`. In generale, le mappe del sito vengono sottoposte a rendering utilizzando i selettori nel percorso della mappa del sito di primo livello della struttura, che è la risorsa che non ha altri predecessori della radice della mappa del sito. Questa directory principale della mappa del sito espone anche l’indice della mappa del sito, che normalmente è ciò che un proprietario del sito configurerebbe nel portale di configurazione del motore di ricerca o aggiungerà al sito `robots.txt`.

Ad esempio, considera un sito che definisce una directory principale della mappa del sito principale in `my-page` e una radice di sitemap nidificata in `my-page/news`, per generare una mappa del sito dedicata alle pagine nella sottostruttura news. Gli url pertinenti risultanti sarebbero

* `<https://www.mydomain.com/my-brand/my-page.sitemap-index.xml>`
* `<https://www.mydomain.com/my-brand/my-page.sitemap.xml>`
* `<https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html>`

>[!NOTE]
>
> I selettori `sitemap` e `sitemap-index` possono interferire con le implementazioni personalizzate. Se non desideri utilizzare la funzione del prodotto, configura il tuo servlet che serve questi selettori con un `service.ranking` superiore a 0.

Nella configurazione predefinita, la finestra di dialogo Proprietà pagina consente di contrassegnare una pagina come radice di una sitemap e quindi, come descritto in precedenza, di generare una sitemap di se stessa e dei suoi discendenti. Questo comportamento è implementato dalle implementazioni dell’interfaccia `SitemapGenerator` e può essere esteso aggiungendo implementazioni alternative. Tuttavia, dato che la frequenza con cui rigenerare sitemap XML dipende fortemente dai flussi di lavoro e dai carichi di lavoro per l’authoring dei contenuti, il prodotto non presenta configurazioni `SitemapScheduler`. In questo modo la funzione può essere effettivamente opt-in.

Al fine di abilitare il processo in background che genera sitemap XML, `SitemapScheduler` deve essere configurato. Per farlo, crea una configurazione OSGI per il PID `org.apache.sling.sitemap.impl.SitemapScheduler`. Espressione di pianificazione `0 0 0 * * ?` può essere utilizzato come punto di partenza per rigenerare tutte le sitemap XML una volta al giorno a mezzanotte.

![Sitemap Apache Sling - Pianificazione](assets/sling-sitemap-scheduler.png)

Il processo di generazione della sitemap può essere eseguito su istanze di livello sia di authoring che di pubblicazione. Nella maggior parte dei casi, si consiglia di eseguire la generazione sulle istanze del livello di pubblicazione, in quanto gli URL canonici corretti possono essere generati solo lì (a causa delle regole di mappatura risorse Sling comunemente presenti solo sulle istanze del livello di pubblicazione). Tuttavia, è possibile collegare un’implementazione personalizzata del meccanismo di esternalizzazione utilizzato per generare gli URL canonici implementando l’interfaccia [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html). Se un’implementazione personalizzata è in grado di generare gli URL canonici di una sitemap sulle istanze del livello di authoring, `SitemapScheduler` può essere configurato per la modalità di esecuzione dell’autore e il carico di lavoro di generazione della sitemap XML può essere distribuito tra le istanze del cluster del servizio di authoring. In questo scenario, occorre prestare particolare attenzione alla gestione di contenuti non ancora pubblicati, modificati o visibili solo a un gruppo ristretto di utenti.

AEM Sites contiene un’implementazione predefinita di un `SitemapGenerator` che attraversa una struttura ad albero di pagine per generare una sitemap. È preconfigurato per generare solo gli URL canonici di un sito e qualsiasi alternativa linguistica, se disponibile. Può anche essere configurato in modo da includere l’ultima data modificata di una pagina, se necessario. Per questo, abilita l’opzione *Aggiungi ultima modificata* di *Adobe AEM SEO - Configurazione del generatore di sitemap nella struttura ad albero della pagina* e seleziona *Ultima origine modificata*. Quando le mappe del sito vengono generate sul livello di pubblicazione, si consiglia di utilizzare il `cq:lastModified` data.

![Adobe AEM SEO - Configurazione del generatore di sitemap nella struttura ad albero della pagina](assets/sling-sitemap-pagetreegenerator.png)

Per limitare il contenuto di una sitemap, è possibile implementare le seguenti interfacce di servizio quando necessario:

* [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) può essere implementato per nascondere le pagine da sitemap XML generate dal generatore di sitemap specifico di AEM Sites
* [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) o [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) può essere implementato per filtrare prodotti o categorie da sitemap XML generati dai generatori di sitemap specifici [Framework di integrazione Commerce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html)

Se le implementazioni predefinite non funzionano per un particolare caso d’uso o se i punti di estensione non sono abbastanza flessibili, un `SitemapGenerator` personalizzato può essere implementato per assumere il controllo completo del contenuto di una sitemap generata. Il seguente esempio mostra come eseguire questa operazione, utilizzando la logica di implementazione predefinita per AEM Sites. Utilizza il [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) come punto iniziale per scorrere la struttura ad albero delle pagine:

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, etc
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

Inoltre, la funzionalità implementata per le sitemap XML può essere utilizzata anche in casi d’uso diversi, ad esempio per aggiungere il collegamento canonico o la lingua nell’intestazione di una pagina. Fai riferimento all’interfaccia [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) per ulteriori informazioni.

### Creazione di reindirizzamenti 301 per gli URL legacy {#creating-redirects-for-legacy-urls}

Quando si lancia un sito con una nuova struttura, è fondamentale implementare e testare i reindirizzamenti 301 in Apache HTTP Server per due motivi:

* Gli URL legacy hanno accumulato valore SEO nel tempo. Implementando un reindirizzamento, il motore di ricerca può applicare questo valore al nuovo URL.
* Gli utenti del sito potrebbero aver creato segnalibri per queste pagine. Grazie ai reindirizzamenti, gli utenti verranno reindirizzati alla pagina del nuovo sito che corrisponde maggiormente alla pagina a cui erano interessati nel vecchio sito.

Controlla la sezione relativa alle risorse aggiuntive che segue per istruzioni sull’implementazione dei reindirizzamenti 301 e uno strumento per verificare che i reindirizzamenti funzionino come previsto.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta le seguenti risorse aggiuntive:

<!--
* [Resource Mapping](/help/sites-deploying/resource-mapping.md)
-->

* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
* [https://github.com/apache/sling-org-apache-sling-sitemap](https://github.com/apache/sling-org-apache-sling-sitemap)
