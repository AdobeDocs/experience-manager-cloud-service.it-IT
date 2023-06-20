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
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 15%

---

# Configurazioni URL avanzate {#url}

>[!NOTE]
>
> L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. È quindi necessario affrontare questo tipo di ottimizzazione in numerosi progetti Adobe Experience Manager (AEM) as a Cloud Service. Leggere [Best practice per la gestione di SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) per ulteriori informazioni.

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Per molte implementazioni questi URL devono essere personalizzati a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare `UrlProvider` secondo i requisiti e le esigenze SEO (Search Engine Optimization), un progetto deve fornire una configurazione OSGI per _Configurazione provider URL CIF_.

>[!NOTE]
>
> A partire dalla versione 2.0.0 dei componenti core CIF dell’AEM, la configurazione del provider URL fornisce solo formati URL predefiniti, invece dei formati configurabili a testo libero noti dalle versioni 1.x. Inoltre, l’utilizzo dei selettori per trasmettere i dati negli URL è stato sostituito dai suffissi.

### Formato URL pagina prodotto {#product}

Questo configura gli URL delle pagine dei prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (impostazione predefinita)
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

Nel caso di [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/product-page`
* `{{sku}}` è sostituito dallo SKU del prodotto, ad esempio `VP09`
* `{{url_key}}` è sostituito da `url_key` proprietà, ad esempio `lenora-crochet-shorts`
* `{{url_path}}` è sostituito da `url_path`ad esempio: `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` viene sostituito dalla variante attualmente selezionata, ad esempio, `VP09-KH-S`

Poiché il `url_path` diventati obsoleti, i formati URL di prodotto predefiniti utilizzano i `url_rewrites` e scegliete quello con il maggior numero di segmenti di tracciato come alternativa se `url_path` non è disponibile.

Con i dati dell’esempio precedente, l’URL di una variante di prodotto formattato con il formato URL predefinito avrà l’aspetto di `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato URL pagina categoria {#product-list}

In questo modo vengono configurati gli URL delle pagine delle categorie o degli elenchi di prodotti e sono supportate le seguenti opzioni:

* `{{page}}.html/{{url_path}}.html` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html`

Nel caso di [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/category-page`
* `{{url_key}}` è sostituito da quello della categoria `url_key` proprietà
* `{{url_path}}` è sostituito da quello della categoria `url_path`

Con i dati dell’esempio precedente, l’URL di una pagina categoria formattato con il formato URL predefinito avrà l’aspetto di `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> Il `url_path` è una concatenazione del `url_keys` dei predecessori di un prodotto o di una categoria e del prodotto o della categoria `url_key` separato da `/` barra. Ogni `url_key` è considerato univoco all’interno di un dato archivio.

### Configurazione specifica archivio {#store-specific-urlformats}

Formati URL per categoria e pagina di prodotto a livello di sistema impostati da _Configurazione provider URL CIF_ può essere modificato per ogni negozio.

Nella configurazione CIF, un editor può selezionare un formato URL alternativo per la pagina di un prodotto o di una categoria. Se non viene selezionato nulla, l’implementazione utilizzerà come fallback la configurazione a livello di sistema.

La modifica del formato URL di un sito web live potrebbe avere un impatto negativo sul traffico organico del sito. Consulta la sezione [Best practice](#best-practices) di seguito e pianifica attentamente la modifica del formato dell’URL in anticipo.

![Formati URL nella configurazione CIF](assets/store-specific-url-formats.png)

>[!NOTE]
>
> La configurazione specifica dell’archivio dei formati URL richiede [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) e la versione più recente del componente aggiuntivo Adobe Experience Manager Content and Commerce.

## URL delle pagine dei prodotti in base alla categoria {#context-aware-pdps}

Poiché è possibile codificare le informazioni di categoria in un URL di prodotto, i prodotti che si trovano in più categorie possono essere indirizzati anche con più URL di prodotto.

I formati URL predefiniti selezioneranno una delle possibili alternative utilizzando lo schema seguente:

* se `url_path` è definito dal back-end di e-commerce use it (obsoleto)
* dal `url_rewrites` utilizza gli URL che terminano con il `url_key` come alternative
* da queste alternative utilizza quella con il maggior numero di segmenti di percorso
* se esistono più, prendi il primo nell’ordine dato dal backend di e-commerce

Questo schema selezionerà il `url_path` con il maggior numero di predecessori, in base al presupposto che una categoria figlio sia più specifica della categoria padre. Il così selezionato `url_path` è considerato _canonico_ e verranno sempre utilizzati come collegamento canonico nelle pagine dei prodotti o nella sitemap del prodotto.

Tuttavia, quando un acquirente passa da una pagina di categoria a una pagina di prodotto o da una pagina di prodotto a un’altra pagina di prodotto correlata nella stessa categoria, vale la pena mantenere il contesto di categoria corrente. In questo caso, il `url_path` la selezione deve preferire alternative che si trovano nel contesto della categoria corrente rispetto alla _canonico_ selezione descritta in precedenza.

Questa funzione deve essere abilitata nella _Configurazione provider URL CIF_. Se abilitata, la selezione assegnerà un punteggio più alto alle alternative, quando

* corrispondono a parti di una determinata categoria `url_path` dall’inizio (corrispondenza del prefisso fuzzy)
* oppure corrispondono a quelli di una determinata categoria `url_key` ovunque (corrispondenza parziale esatta)

Ad esempio, considera la risposta per un [query prodotti](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) di seguito. Dato che l’utente si trova sulla pagina della categoria &quot;Nuovi prodotti/Novità dell’estate 2022&quot; e che lo store utilizza il formato URL predefinito per la pagina della categoria, l’alternativa &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; corrisponderebbe a 2 segmenti del percorso del contesto dall’inizio: &quot;nuovi prodotti&quot; e &quot;nuovi dell’estate 2022&quot;. Se lo store utilizza un formato URL per pagina categoria che contiene solo la categoria `url_key`, la stessa alternativa verrebbe comunque selezionata in quanto corrisponde a `url_key` ovunque. In entrambi i casi, l’URL della pagina del prodotto viene creato per &quot;new-products/new-in-summer-2022/gold-cirque-earrings.html&quot; `url_path`.

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
> Gli URL dei prodotti in base alla categoria richiedono [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o più recenti.

## Categorie specifiche e pagine di prodotti {#specific-pages}

È possibile creare [più pagine di prodotti e categorie](../authoring/multi-template-usage.md) solo per un sottoinsieme specifico di categorie o prodotti di un catalogo.

### Criteri di selezione {#specific-pages-selection}

La selezione di una pagina di categoria specifica è diretta, in base al `url_path` o `url_key`. La corrispondenza delle sottocategorie è supportata solo per i formati URL che contengono la categoria completa `url_path`. In caso contrario, solo una corrispondenza esatta `url_key` è possibile.

Le pagine di prodotto specifiche sono selezionate dallo SKU o dalla categoria del prodotto. Quest’ultimo richiede che alcune informazioni sulla categoria siano codificate nell’URL del prodotto. Questa opzione è disponibile solo per alcuni dei formati URL predefiniti. Consulta la tabella seguente per un confronto tra i formati URL che supportano la selezione di pagine specifiche per SKU o categoria.


| Formato URL | da sku | per categoria |
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
> La selezione di pagine di prodotti specifiche per categoria richiede [Componenti core CIF 2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) o più recenti.

### Collegamenti profondi {#specific-pages-deep-linking}

Il `UrlProvider` è preconfigurato per generare collegamenti profondi a specifiche pagine di prodotti e categorie sulle istanze del livello di authoring. Questa funzione è utile per gli editor che navigano in un sito utilizzando la modalità Anteprima, per passare a una pagina di prodotto o categoria specifica e tornare alla modalità Modifica per modificare la pagina.

Nelle istanze a livello di pubblicazione, invece, gli URL delle pagine del catalogo devono essere mantenuti stabili per non perdere i guadagni, ad esempio, nella classificazione dei motori di ricerca. Per questo motivo, per impostazione predefinita, le istanze del livello di pubblicazione non eseguiranno il rendering dei collegamenti profondi a pagine di catalogo specifiche. Per modificare questo comportamento, _Strategia pagina specifica del provider URL CIF_ può essere configurato in modo da generare sempre URL di pagina specifici.

### Più pagine catalogo {#multiple-product-pages}

Quando gli editor desiderano avere il controllo completo della navigazione di livello superiore di un sito, l’utilizzo di una singola pagina di catalogo per il rendering delle categorie di livello superiore di un catalogo potrebbe non essere desiderato. Gli editor possono invece creare più pagine di catalogo, una per ogni categoria del catalogo che desiderano includere nella navigazione di livello superiore.

Per questo caso d’uso, ogni pagina di catalogo può avere un riferimento a una pagina di prodotto e di categoria specifica per la categoria configurata per la pagina di catalogo. Il `UrlProvider` utilizzerà questi per creare collegamenti per le pagine e le categorie nella categoria configurata. Tuttavia, per motivi di prestazioni, vengono considerati solo gli elementi secondari della pagina di catalogo diretto della directory principale di navigazione/pagina di destinazione di un sito.

È consigliabile che le pagine di prodotti e categorie di una pagina di catalogo siano discendenti di tale pagina, altrimenti i componenti come Navigazione o Breadcrumb potrebbero non funzionare correttamente.

>[!NOTE]
>
> Il supporto completo per più pagine di catalogo richiede [Componenti core CIF 2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) o più recenti.

## Personalizzazioni {#customization}

### Formati URL personalizzati {#custom-url-format}

Per fornire un formato URL personalizzato, un progetto può implementare [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registra l’implementazione come servizio OSGI. Queste implementazioni, se disponibili, sostituiranno il formato configurato e predefinito. Se sono registrate più implementazioni, quella con la classificazione di servizio più alta sostituisce quella con la classificazione di servizio più bassa.

Le implementazioni del formato URL personalizzato devono implementare una coppia di metodi per generare un URL dai parametri forniti e per analizzare un URL rispettivamente per restituire gli stessi parametri.

### Combinare con mappature Sling {#sling-mapping}

Oltre al `UrlProvider`, è anche possibile configurare [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto AEM Archetype fornisce anche una [configurazione esemplificativa](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare mappature Sling per le porte 4503 (pubblicazione) e 80 (dispatcher).

### Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando il server HTTP di Dispatcher dell’AEM con `mod_rewrite` modulo. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Best practice {#best-practices}

### Scegli il formato URL migliore {#choose-url-format}

Come accennato prima di selezionare uno dei formati predefiniti disponibili, o anche l&#39;implementazione di un formato personalizzato, altamente dipende dalle esigenze e requisiti di un negozio. I seguenti suggerimenti possono essere utili per una descrizione accurata.

_**Utilizza un formato URL per pagina di prodotto contenente lo SKU.**_

I componenti core CIF utilizzano lo SKU come identificatore primario in tutti i componenti. Se il formato dell’URL della pagina di prodotto non contiene lo SKU, è necessaria una query GraphQL per risolverlo. Questo può influire sul tempo al primo byte. Inoltre, può essere desiderato, che gli acquirenti possono trovare i prodotti da sku utilizzando motori di ricerca.

_**Utilizza un formato URL per pagina di prodotto che contenga il contesto della categoria.**_

Alcune funzioni del provider URL CIF sono disponibili solo quando si utilizzano i formati URL del prodotto, che codificano il contesto della categoria, come la categoria `url_key` o la categoria `url_path`. Anche se queste funzioni non sono necessarie per un nuovo archivio, l’utilizzo iniziale di uno di questi formati URL contribuisce a ridurre le attività di migrazione in futuro.

_**Equilibrio tra la lunghezza dell’URL e le informazioni codificate.**_

A seconda delle dimensioni del catalogo, in particolare le dimensioni e la profondità dell&#39;albero delle categorie, potrebbe non essere ragionevole codificare l&#39;intero `url_path` delle categorie nell’URL. In tal caso, la lunghezza dell’URL può essere ridotta includendo solo i `url_key` invece. Questa opzione supporta la maggior parte delle funzioni disponibili quando si utilizza la categoria `url_path`.

Inoltre, utilizza [Mappature Sling](#sling-mapping) per combinare lo sku con il prodotto `url_key`. Nella maggior parte dei sistemi di e-commerce lo SKU segue un particolare formato e separa lo SKU dallo `url_key` per le richieste in arrivo dovrebbe essere facilmente possibile. In quest’ottica, dovrebbe essere possibile riscrivere l’URL di una pagina di prodotto in `/p/{{category}}/{{sku}}-{{url_key}}.html`e un URL di categoria a `/c/{{url_key}}.html` rispettivamente. Il `/p` e `/c` Il prefisso è ancora necessario per distinguere le pagine di prodotti e categorie da altre pagine di contenuti.

### Migrazione a un nuovo formato URL {#migrate-url-formats}

Molti dei formati URL predefiniti sono in qualche modo compatibili tra loro, il che significa che gli URL formattati da un possono essere analizzati da un altro. Questo facilita la migrazione tra i formati URL.

D’altra parte, i motori di ricerca avranno bisogno di un po’ di tempo per eseguire nuovamente la ricerca per indicizzazione di tutte le pagine del catalogo con il nuovo formato URL. Per supportare questo processo e anche per migliorare l’esperienza dell’utente finale, si consiglia di fornire reindirizzamenti che inoltrino l’utente dai vecchi URL a quelli nuovi.

Un approccio per farlo potrebbe essere quello di collegare un ambiente di staging al backend di e-commerce di produzione e configurarlo per utilizzare il nuovo formato URL. In seguito ottieni il [mappa del sito del prodotto generata dal generatore di sitemap di prodotti CIF](../../overview/seo-and-url-management.md) sia per l&#39;ambiente di stage che per quello di produzione, e utilizzarli per creare un [Mappa di riscrittura httpd Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). Questa mappa di riscrittura può invece essere distribuita a Dispatcher insieme al rollout del nuovo formato URL.

## Esempio {#example}

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questo consente a ciascun progetto di impostare pattern di URL individuali per le pagine di prodotti e categorie in base alle proprie esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella delle mappature Sling da `hostname.adobeaemcloud.com` a `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive {#additional}

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
