---
title: Configurazioni URL avanzate
description: Scopri come personalizzare gli URL per le pagine di prodotti e categorie. Questo consente alle implementazioni di ottimizzare gli URL per i motori di ricerca e promuovere l’individuazione.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 9c25d9991b41a5a714df3f07e84946162e5495c0
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 15%

---

# Configurazioni URL avanzate {#url}

>[!NOTE]
>
> L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. È quindi necessario affrontare questo tipo di ottimizzazione in numerosi progetti Adobe Experience Manager (AEM) as a Cloud Service. Leggi [Best practice per la gestione di SEO (Search Engine Optimization) e URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) per ulteriori informazioni.

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Per molte implementazioni questi URL devono essere personalizzati a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare le `UrlProvider` servizio in base ai requisiti e alle esigenze SEO, un progetto deve fornire una configurazione OSGI per _Configurazione del provider URL CIF_.

>[!NOTE]
>
> A partire dalla versione 2.0.0 dei componenti core CIF di AEM, la configurazione del provider URL fornisce solo formati URL predefiniti, invece dei formati configurabili in testo libero noti dalle versioni 1.x. Inoltre, l’uso dei selettori per trasmettere dati negli URL è stato sostituito con suffissi.

### Formato URL pagina di prodotto {#product}

Consente di configurare gli URL delle pagine dei prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (impostazione predefinita)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Nel caso di [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/product-page`
* `{{sku}}` saranno sostituite, ad esempio, dallo SKU del prodotto, `VP09`
* `{{url_key}}` saranno sostituiti dal `url_key` ad esempio, `lenora-crochet-shorts`
* `{{url_path}}` saranno sostituiti dal `url_path`ad esempio, `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` viene sostituito dalla variante attualmente selezionata, ad esempio `VP09-KH-S`

Dal momento che `url_path` obsoleti, i formati URL di prodotto predefiniti utilizzano i `url_rewrites` e scegli quello con il maggior numero di segmenti di percorso come alternativa se il `url_path` non è disponibile.

Con i dati di esempio di cui sopra, un URL di variante del prodotto formattato utilizzando il formato URL predefinito sarà simile a `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato URL pagina categoria {#product-list}

Consente di configurare gli URL delle pagine di elenchi di prodotti o categorie e supporta le seguenti opzioni:

* `{{page}}.html/{{url_path}}.html` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html`

Nel caso di [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/category-page`
* `{{url_key}}` sarà sostituito dal `url_key` property
* `{{url_path}}` sarà sostituito dal `url_path`

Con i dati di esempio di cui sopra, un URL di pagina di categoria formattato utilizzando il formato URL predefinito sarà simile a `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> La `url_path` è una concatenazione di `url_keys` di un prodotto o di una categoria e del prodotto o della categoria `url_key` separato da `/` slash. Ogni `url_key` è considerato univoco all&#39;interno di un determinato archivio.

### Configurazione specifica archivio {#store-specific-urlformats}

I formati di URL per le pagine di prodotti e le categorie di sistema impostati da _Configurazione del provider URL CIF_ può essere modificato per ogni negozio.

Nella configurazione CIF, un editor può selezionare un formato URL di pagina di prodotto o categoria alternativo. Se non viene selezionato nulla, l&#39;implementazione si basa sulla configurazione a livello di sistema.

La modifica del formato URL di un sito web live può avere un impatto negativo sul traffico organico del sito. Fai riferimento alla [Best practice](#best-practices) di seguito e pianifica attentamente la modifica del formato dell’URL in anticipo.

![Formati URL nella configurazione CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> La configurazione specifica dell’archivio dei formati URL richiede [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) e la versione più recente del componente aggiuntivo Contenuto e Commerce di Adobe Experience Manager.

## URL delle pagine di prodotto in base alle categorie {#context-aware-pdps}

Poiché è possibile codificare le informazioni sulle categorie in un URL di prodotto, i prodotti che si trovano in più categorie possono essere gestiti anche con più URL di prodotto.

I formati URL predefiniti selezioneranno una delle possibili alternative utilizzando il seguente schema:

* se `url_path` è definito dal backend e-commerce use (obsoleto)
* dal `url_rewrites` utilizza gli URL che terminano con i `url_key` come alternative
* in questo modulo le alternative utilizzano quella con il maggior numero di segmenti di percorso
* se sono presenti più elementi, inserisci il primo nell’ordine indicato dal backend e-commerce

Questo schema selezionerà `url_path` con il maggior numero di predecessori, partendo dal presupposto che una categoria figlio sia più specifica della categoria padre. I così selezionati `url_path` è considerato _canonico_ e sarà sempre utilizzato come collegamento canonico nelle pagine di prodotto o nella mappa del sito del prodotto.

Tuttavia, quando un acquirente passa da una pagina di categoria a una pagina di prodotto, o da una pagina di prodotto a un&#39;altra pagina di prodotto correlata nella stessa categoria, vale la pena mantenere il contesto di categoria corrente. In questo caso, `url_path` la selezione dovrebbe preferire le alternative che si trovano nel contesto della categoria corrente rispetto al _canonico_ selezione sopra descritta.

Questa funzione deve essere abilitata nella _Configurazione del provider URL CIF_. Se abilitata, la selezione avrà un punteggio alternativo più elevato, quando

* corrispondono a parti di una determinata categoria `url_path` dall’inizio (corrispondenza con prefisso fuzzy)
* o corrispondono a una determinata categoria `url_key` ovunque (corrispondenza parziale esatta)

Ad esempio, considera la risposta per un [query sui prodotti](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) sotto. Dato che l&#39;utente si trova nella pagina della categoria &quot;Nuovi prodotti / Novità nell&#39;estate 2022&quot; e che lo store utilizza il formato di URL della pagina della categoria predefinito, l&#39;alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corrisponderebbe a 2 segmenti del percorso del contesto dall&#39;inizio: &quot;new-products&quot; e &quot;new-in-estate-2022&quot;. Se lo store utilizza un formato URL di pagina di categoria che contiene solo la categoria `url_key`, la stessa alternativa verrebbe comunque selezionata in quanto corrisponde al `url_key` ovunque. In entrambi i casi, l’URL della pagina del prodotto verrebbe creato per &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

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
> Gli URL di prodotti in base alle categorie richiedono [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o più recente.

## Categorie specifiche e pagine di prodotti {#specific-pages}

È possibile creare [più pagine di categorie e prodotti](../authoring/multi-template-usage.md) solo per un sottoinsieme specifico di categorie o prodotti di un catalogo.

### Criteri di selezione {#specific-pages-selection}

La selezione di una pagina di categoria specifica è diretta in avanti, in base alle `url_path` o `url_key`. Le sottocategorie corrispondenti sono supportate solo per i formati URL che contengono la categoria completa `url_path`. Altrimenti solo una corrispondenza esatta del `url_key` è possibile.

Le pagine di prodotto specifiche vengono selezionate in base allo SKU o alla categoria del prodotto. In seguito, alcune informazioni sulla categoria devono essere codificate nell’URL del prodotto. Questa funzione è disponibile solo per alcuni dei formati URL predefiniti. Fai riferimento alla tabella seguente per un confronto tra il formato URL che supporta una selezione specifica di pagina per SKU o categoria.


| Formato URL | da sku | per categoria |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | no | no |
| `{{page}}.html/{{category}}/{{url_key}}.html` | no | solo corrispondenza esatta |
| `{{page}}.html/{{url_path}}.html` | no | sì |
| `{{page}}.html/{{sku}}.html` | sì | no |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | sì | no |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | sì | solo corrispondenza esatta |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | sì | sì |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> La selezione di specifiche pagine di prodotto per categoria richiede [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o più recente.

### Collegamenti profondi {#specific-pages-deep-linking}

La `UrlProvider` è preconfigurato per generare collegamenti profondi a specifiche pagine di prodotti e categorie nelle istanze del livello di authoring. È utile per gli editor che navigano su un sito utilizzando la modalità Anteprima, accedono a una pagina di prodotto o categoria specifica e tornano alla modalità Modifica per modificare la pagina.

Sulle istanze del livello di pubblicazione, invece, gli URL delle pagine di catalogo devono essere mantenuti stabili in modo da non perdere, ad esempio, guadagni nella classificazione dei motori di ricerca. Per impostazione predefinita, le istanze del livello di pubblicazione non eseguono il rendering dei collegamenti profondi a pagine di catalogo specifiche. Per modificare questo comportamento, _Strategia di pagina specifica per provider URL CIF_ può essere configurato per generare sempre URL di pagina specifici.

### Pagine catalogo multiple {#multiple-product-pages}

Quando gli editor desiderano avere il controllo completo della navigazione di primo livello di un sito, potrebbe non essere opportuno utilizzare una singola pagina di catalogo per eseguire il rendering delle categorie di primo livello di un catalogo. Gli editor possono invece creare più pagine di catalogo, una per ogni categoria del catalogo che desiderano includere nella navigazione di livello superiore.

In tal caso d’uso, ciascuna pagina del catalogo può avere un riferimento a una pagina di prodotto e di categoria specifica per la categoria configurata per la pagina del catalogo. La `UrlProvider` utilizzeranno questi per creare collegamenti per le pagine e le categorie della categoria configurata. Tuttavia, per motivi di prestazioni, vengono considerati solo gli elementi secondari della pagina di catalogo diretta della pagina principale o della pagina di destinazione di un sito.

È consigliabile che le pagine di prodotti e categorie di una pagina di catalogo siano discendenti di tale pagina di catalogo, altrimenti i componenti come Navigazione o Breadcrumb potrebbero non funzionare correttamente.

>[!NOTE]
>
> Il supporto completo per più pagine di catalogo richiede [Componenti core CIF 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) o più recente.

## Personalizzazioni {#customization}

### Formati URL personalizzati {#custom-url-format}

Per fornire un formato URL personalizzato, un progetto può implementare [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) interfaccia del servizio e registra l&#39;implementazione come servizio OSGI. Tali implementazioni, se disponibili, sostituiranno il formato predefinito configurato. Se sono registrate più implementazioni, quella con la classificazione di servizio superiore sostituisce quella con la classificazione di servizio inferiore.

Le implementazioni del formato URL personalizzato devono implementare una coppia di metodi per creare un URL a partire da determinati parametri e per analizzare un URL per restituire gli stessi parametri rispettivamente.

### Combinare con mappature Sling {#sling-mapping}

Oltre a `UrlProvider`, è anche possibile configurare [mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto AEM Archetype fornisce anche una [configurazione esemplificativa](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare mappature Sling per le porte 4503 (pubblicazione) e 80 (dispatcher).

### Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando AEM server HTTP Dispatcher con `mod_rewrite` modulo . [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Best practice   {#best-practices}

### Scegli il formato URL migliore {#choose-url-format}

Come accennato prima di selezionare uno dei formati predefiniti disponibili, o anche di implementare un formato personalizzato, dipende fortemente dalle esigenze e dai requisiti di un negozio. I seguenti suggerimenti possono aiutare a fare una descrizione educata.

_**Utilizza un formato URL della pagina di un prodotto contenente lo SKU.**_

I componenti core CIF utilizzano lo SKU come identificatore principale in tutti i componenti. Se il formato dell’URL della pagina del prodotto non contiene lo SKU, è necessaria una query GraphQL per risolverlo. Questo può influire sul time-to-first-byte. Inoltre, può essere desiderato, che i consumatori possono trovare prodotti da sku utilizzando motori di ricerca.

_**Utilizza un formato URL della pagina del prodotto che contiene il contesto della categoria.**_

Alcune funzioni del provider URL CIF sono disponibili solo quando si utilizzano i formati URL del prodotto, che codificano il contesto della categoria, come la categoria `url_key` o la categoria `url_path`. Anche se queste funzioni potrebbero non essere necessarie per un nuovo archivio, l&#39;utilizzo di uno di questi formati URL all&#39;inizio contribuisce a ridurre le operazioni di migrazione in futuro.

_**Equilibrio tra la lunghezza dell’URL e le informazioni codificate.**_

A seconda delle dimensioni del catalogo, in particolare delle dimensioni e della profondità dell&#39;albero della categoria, potrebbe non essere ragionevole codificare l&#39;intero `url_path` di categorie nell’URL. In tal caso, la lunghezza dell’URL potrebbe essere ridotta includendo solo l’ `url_key` invece. Questo supporterà la maggior parte delle funzioni disponibili quando si utilizza la categoria `url_path`.

Inoltre, utilizza [Mappature Sling](#sling-mapping) per combinare lo sku con il prodotto `url_key`. Nella maggior parte dei sistemi di e-commerce lo sku segue un particolare formato e separa lo sku dal `url_key` le richieste in arrivo dovrebbero essere facilmente possibili. Tenendo presente ciò, dovrebbe essere possibile riscrivere l’URL di una pagina di prodotto in `/p/{{category}}/{{sku}}-{{url_key}}.html`e un URL di categoria per `/c/{{url_key}}.html` rispettivamente. La `/p` e `/c` Il prefisso è ancora necessario per distinguere le pagine di prodotti e categorie da altre pagine di contenuto.

### Migrazione a un nuovo formato URL {#migrate-url-formats}

Molti dei formati URL predefiniti sono in qualche modo compatibili tra loro, il che significa che gli URL formattati da uno possono essere analizzati da un altro. Consente la migrazione tra i formati URL.

D’altro canto, i motori di ricerca avranno bisogno di un po’ di tempo per ri-crawling tutte le pagine di catalogo con il nuovo formato URL. Per supportare questo processo e anche per migliorare l’esperienza dell’utente finale, si consiglia di fornire reindirizzamenti che inoltrano l’utente dai vecchi URL a quelli nuovi.

Un approccio potrebbe essere quello di collegare un ambiente stage al back-end di produzione e-commerce e configurarlo per utilizzare il nuovo formato URL. In seguito, ottieni il [mappa del sito del prodotto generata dal generatore di mappa del sito dei prodotti CIF](../../overview/seo-and-url-management.md) sia per l’area di visualizzazione che per l’ambiente di produzione, e utilizzarli per creare un [Mappa di riscrittura di Apache httpd](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Questa mappa di riscrittura può essere distribuita al dispatcher insieme al rollout del nuovo formato URL.

## Esempio {#example}

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questo consente a ogni progetto di impostare singoli pattern URL per le pagine di prodotti e categorie in base alle proprie esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella delle mappature Sling da `hostname.adobeaemcloud.com` a `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
