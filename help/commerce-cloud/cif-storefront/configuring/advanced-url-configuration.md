---
title: Configurazioni URL avanzate
description: Scopri come personalizzare gli URL per le pagine di prodotti e categorie. La personalizzazione consente alle implementazioni di ottimizzare gli URL per i motori di ricerca e promuovere l’individuazione.
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 9%

---


# Configurazioni URL avanzate {#url}

>[!NOTE]
>
> L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. Di conseguenza, i problemi relativi all’ottimizzazione SEO devono essere affrontati in molti progetti su Adobe Experience Manager (AEM) as a Cloud Service. Per ulteriori informazioni, vedere [Best practice per la gestione SEO e URL](/help/overview/seo-and-url-management.md).

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Molte implementazioni personalizzano questi URL a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare il servizio `UrlProvider` in base ai requisiti e alle esigenze SEO (Search Engine Optimization), un progetto deve fornire una configurazione OSGi per la _configurazione del provider URL di CIF_.

>[!NOTE]
>
> A partire dalla versione 2.0.0 dei Componenti core di AEM CIF, la configurazione del provider URL fornisce solo formati URL predefiniti, invece dei formati configurabili a testo libero noti dalle versioni 1.x. Inoltre, l’utilizzo dei selettori per trasmettere i dati negli URL è stato sostituito dai suffissi.

### Formato URL pagina prodotto {#product}

Configura gli URL delle pagine dei prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (impostazione predefinita)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Se è presente [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/product-page`
* `{{sku}}` è sostituito dallo SKU del prodotto, ad esempio `VP09`
* `{{url_key}}` è sostituito dalla proprietà `url_key` del prodotto, ad esempio `lenora-crochet-shorts`
* `{{url_path}}` è sostituito da `url_path` del prodotto, ad esempio `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` è sostituito dalla variante attualmente selezionata, ad esempio `VP09-KH-S`

Poiché `url_path` è diventato obsoleto, i formati URL del prodotto predefiniti utilizzano `url_rewrites` di un prodotto e selezionano quello con il maggior numero di segmenti di percorso in alternativa, se `url_path` non è disponibile.

Con i dati dell&#39;esempio precedente, l&#39;URL di una variante di prodotto formattato con il formato URL predefinito è simile a `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato URL pagina categoria {#product-list}

Configura gli URL delle pagine contenenti le categorie o gli elenchi di prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{url_path}}.html` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html`

Se è presente [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/category-page`
* `{{url_key}}` è sostituito dalla proprietà `url_key` della categoria
* `{{url_path}}` è sostituito da `url_path` della categoria

Con i dati dell&#39;esempio precedente, l&#39;URL di una pagina categoria formattato con il formato URL predefinito è simile a `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> `url_path` è una concatenazione di `url_keys` dei predecessori di un prodotto o di una categoria e `url_key` del prodotto o della categoria separati da `/` barra. Ogni `url_key` è considerato univoco all&#39;interno di un determinato archivio.

### Configurazione specifica per lo store {#store-specific-urlformats}

I formati degli URL delle categorie e delle pagine dei prodotti a livello di sistema impostati dalla _configurazione del provider URL di CIF_ possono essere modificati per ogni archivio.

In Configurazione CIF, un editor può selezionare un formato URL alternativo per la pagina di un prodotto o di una categoria. Se non viene selezionato nulla, l’implementazione torna alla configurazione a livello di sistema.

La modifica del formato URL di un sito web live potrebbe avere un impatto negativo sul traffico organico del sito. Consulta [Best practice](#best-practices) di seguito e pianifica attentamente la modifica del formato dell&#39;URL in anticipo.

![Formati URL nella configurazione CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> La configurazione specifica dell&#39;archivio dei formati URL richiede [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) e la versione più recente del componente aggiuntivo Adobe Experience Manager Content and Commerce.

## URL delle pagine dei prodotti in base alla categoria {#context-aware-pdps}

Poiché è possibile codificare le informazioni di categoria in un URL di prodotto, i prodotti che si trovano in più categorie possono essere indirizzati anche con più URL di prodotto.

I formati URL predefiniti selezionano una delle possibili alternative utilizzando lo schema seguente:

* se `url_path` è definito dal back-end di e-commerce, utilizzarlo (obsoleto)
* da `url_rewrites` utilizzare gli URL che terminano con `url_key` del prodotto come alternative
* da queste alternative utilizza quella con il maggior numero di segmenti di percorso
* se esistono più, prendi il primo nell’ordine dato dal backend di e-commerce

Questo schema seleziona `url_path` con il maggior numero di elementi precedenti, partendo dal presupposto che una categoria figlio sia più specifica della categoria padre. Il `url_path` selezionato è considerato _canonico_ ed è sempre utilizzato come collegamento canonico nelle pagine dei prodotti o nella mappa del sito del prodotto.

Tuttavia, quando un acquirente passa da una pagina di categoria a una pagina di prodotto o da una pagina di prodotto a un’altra pagina di prodotto correlata nella stessa categoria, vale la pena mantenere il contesto di categoria corrente. In questo caso, la selezione `url_path` deve preferire alternative che si trovano nel contesto della categoria corrente rispetto alla selezione _canonical_ descritta sopra.

Questa funzionalità deve essere abilitata nella _configurazione del provider URL di CIF_. Se l’opzione è abilitata, le alternative per i punteggi di selezione saranno più elevate quando

* corrispondono a parti di `url_path` di una determinata categoria dall&#39;inizio (corrispondenza del prefisso fuzzy)
* oppure corrispondono a `url_key` di una determinata categoria ovunque (corrispondenza parziale esatta)

Ad esempio, considera la risposta per una query [products](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) di seguito. Considerato quanto segue:

* l’utente si trova sulla pagina della categoria &quot;Nuovi prodotti/Novità dell’estate 2022&quot;
* lo store utilizza il formato URL predefinito per la pagina della categoria

L’alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corrisponde a due dei segmenti di percorso del contesto dall’inizio. Ovvero, &quot;new-products&quot; e &quot;new-in-summer-2022&quot;. Se l&#39;archivio utilizza un formato di URL per la pagina delle categorie che contiene solo la categoria `url_key`, la stessa alternativa verrà comunque selezionata in quanto corrisponde all&#39;elemento `url_key` del contesto in qualsiasi punto. In entrambi i casi, l&#39;URL della pagina del prodotto viene creato per &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> Gli URL dei prodotti in base alla categoria richiedono [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o versioni successive.

## Categorie specifiche e pagine di prodotti {#specific-pages}

È possibile creare [pagine di prodotti e categorie](/help/commerce-cloud/cif-storefront/authoring/multi-template-usage.md) per un sottoinsieme specifico di categorie o prodotti di un catalogo.

### Criteri di selezione {#specific-pages-selection}

La selezione di una pagina categoria specifica è diretta, in base al `url_path` o al `url_key` della categoria. La corrispondenza delle sottocategorie è supportata solo per i formati URL che contengono la categoria completa `url_path`. Altrimenti è possibile solo una corrispondenza esatta di `url_key`.

Le pagine di prodotto specifiche vengono selezionate in base alla SKU o alla categoria del prodotto. Quest’ultimo richiede che alcune informazioni sulla categoria siano codificate nell’URL del prodotto. Questa funzionalità è disponibile solo per alcuni dei formati URL predefiniti. Vedi la tabella seguente per un confronto tra i formati URL che supportano la selezione di pagine specifiche per SKU o categoria.


| Formato URL | da SKU | per categoria |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | no | no |
| `{{page}}.html/{{category}}/{{url_key}}.html` | no | solo corrispondenza esatta |
| `{{page}}.html/{{url_path}}.html` | no | sì |
| `{{page}}.html/{{sku}}.html` | sì | no |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | sì | no |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | sì | solo corrispondenza esatta |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | sì | sì |

{style="table-layout:auto"}

>[!NOTE]
>
> La selezione di pagine di prodotti specifiche per categoria richiede [CIF Core Components 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o versione successiva.

### Collegamenti profondi {#specific-pages-deep-linking}

`UrlProvider` è preconfigurato per generare collegamenti profondi a specifiche pagine di prodotti e categorie nelle istanze del livello di authoring. Questa funzionalità è utile per gli editor che navigano in un sito utilizzando la modalità Anteprima, che visitano una pagina di prodotto o categoria specifica e che tornano alla modalità Modifica per modificare la pagina.

Nelle istanze a livello di pubblicazione, invece, gli URL delle pagine del catalogo devono essere mantenuti stabili per non perdere i guadagni, ad esempio, nella classificazione dei motori di ricerca. A causa di questo livello di pubblicazione, per impostazione predefinita le istanze non eseguono il rendering dei collegamenti profondi a pagine di catalogo specifiche. Per modificare questo comportamento, è possibile configurare la _strategia di pagina specifica per il provider URL di CIF_ per generare sempre URL di pagina specifici.

### Più pagine catalogo {#multiple-product-pages}

Quando gli editor desiderano avere il controllo completo della navigazione di livello superiore di un sito, l’utilizzo di una singola pagina di catalogo per il rendering delle categorie di livello superiore di un catalogo potrebbe non essere desiderato. Gli editor possono invece creare più pagine di catalogo, una per ogni categoria del catalogo che desiderano includere nella navigazione di livello superiore.

Per questo caso d’uso, ogni pagina di catalogo può avere un riferimento a una pagina di prodotto e di categoria specifica per la categoria configurata per la pagina di catalogo. `UrlProvider` utilizza queste connessioni per creare collegamenti per le pagine e le categorie nella categoria configurata. Tuttavia, per motivi di prestazioni, vengono considerati solo gli elementi secondari della pagina di catalogo diretto della directory principale di navigazione/pagina di destinazione di un sito.

È consigliabile che le pagine di prodotti e categorie di una pagina di catalogo siano discendenti di tale pagina, altrimenti i componenti come Navigazione o Breadcrumb potrebbero non funzionare correttamente.

>[!NOTE]
>
> Il supporto completo per più pagine di catalogo richiede [CIF Core Components 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) o versione successiva.

## Personalizzazioni {#customization}

### Formati URL personalizzati {#custom-url-format}

Per fornire un formato URL personalizzato, un progetto può implementare l&#39;interfaccia di servizio [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registrare l&#39;implementazione come servizio OSGI. Queste implementazioni, se disponibili, sostituiscono il formato configurato e predefinito. Se sono registrate più implementazioni, quella con la classificazione di servizio più alta sostituisce quelle con la classificazione di servizio più bassa.

Le implementazioni del formato URL personalizzato devono implementare una coppia di metodi per generare un URL dai parametri forniti e per analizzare un URL rispettivamente per restituire gli stessi parametri.

### Combinare con mappature Sling {#sling-mapping}

Oltre a `UrlProvider`, è anche possibile configurare [mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto Archetipo AEM fornisce anche [una configurazione di esempio](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare mappature Sling per le porte 4503 (pubblicazione) e 80 (Dispatcher).

### Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando il server HTTP di AEM Dispatcher con il modulo `mod_rewrite`. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Best practice {#best-practices}

### Scegli il formato URL migliore {#choose-url-format}

Come accennato prima di selezionare uno dei formati predefiniti disponibili, o anche l&#39;implementazione di un formato personalizzato, altamente dipende dalle esigenze e requisiti di un negozio. I seguenti suggerimenti possono essere utili per prendere una decisione ponderata.

#### Utilizza un formato URL per pagina di prodotto contenente lo SKU. {#use-sku}

I Componenti core di CIF utilizzano lo SKU come identificatore primario in tutti i componenti. Se il formato dell’URL della pagina di prodotto non contiene lo SKU, è necessaria una query GraphQL per risolverlo. Questa risoluzione può influire sul tempo al primo byte. Inoltre, può essere necessario che gli acquirenti possano trovare i prodotti per SKU utilizzando i motori di ricerca.

#### Utilizza un formato URL per pagina di prodotto che contenga il contesto della categoria. {#use-url}

Alcune funzionalità del provider URL di CIF sono disponibili solo quando si utilizzano formati URL di prodotto che codificano il contesto della categoria, come la categoria `url_key` o la categoria `url_path`. Anche se queste funzioni non sono necessarie per un nuovo archivio, l’utilizzo iniziale di uno di questi formati URL contribuisce a ridurre le attività di migrazione in futuro.

#### Equilibrio tra la lunghezza dell’URL e le informazioni codificate. {#balance-url}

A seconda della dimensione del catalogo, in particolare la dimensione e la profondità della struttura delle categorie, potrebbe non essere ragionevole codificare l’`url_path` completo delle categorie nell’URL. In tal caso, la lunghezza dell&#39;URL può essere ridotta includendo solo il `url_key` della categoria. Questo metodo supporta la maggior parte delle funzionalità disponibili quando si utilizza la categoria `url_path`.

Utilizza inoltre [mappature Sling](#sling-mapping) per combinare lo SKU con il prodotto `url_key`. Nella maggior parte dei sistemi di e-commerce, lo SKU segue un formato particolare e dovrebbe essere possibile separare facilmente lo SKU da `url_key` per le richieste in arrivo. Tenendo presente questo aspetto, dovrebbe essere possibile riscrivere rispettivamente l&#39;URL di una pagina di prodotto in `/p/{{category}}/{{sku}}-{{url_key}}.html` e l&#39;URL di una categoria in `/c/{{url_key}}.html`. Il prefisso `/p` e `/c` sono ancora necessari per distinguere le pagine di prodotti e categorie da altre pagine di contenuti.

### Migrazione a un nuovo formato URL {#migrate-url-formats}

Molti dei formati URL predefiniti sono in qualche modo compatibili tra loro, il che significa che gli URL formattati da un utente possono essere analizzati da un altro. Questo facilita la migrazione tra i formati URL.

D’altra parte, i motori di ricerca hanno bisogno di tempo per eseguire nuovamente la ricerca per indicizzazione di tutte le pagine del catalogo con il nuovo formato URL. Per supportare questo processo e anche per migliorare l’esperienza dell’utente finale, si consiglia di fornire reindirizzamenti che inoltrino l’utente dai vecchi URL a quelli nuovi.

Un approccio per farlo potrebbe essere quello di collegare un ambiente di staging al backend di e-commerce di produzione e configurarlo per utilizzare il nuovo formato URL. In seguito, ottieni la [mappa del sito del prodotto generata dal generatore di sitemap dei prodotti CIF](/help/overview/seo-and-url-management.md) sia per stage che per l&#39;ambiente di produzione e utilizzali per creare una [mappa di riscrittura httpd Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Questa mappa di riscrittura può quindi essere distribuita in Dispatcher insieme al rollout del nuovo formato URL.

## Esempio {#example}

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questa configurazione consente a ciascun progetto di impostare pattern di URL individuali per le pagine di prodotti e categorie in base alle proprie esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella di mappatura Sling `hostname.adobeaemcloud.com` in `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/configuring/resource-mapping)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
