---
title: Configurazioni URL avanzate
description: Configurazioni URL avanzate
translation-type: tm+mt
source-git-commit: 3a235e3d8e2d97e413f445df1f0bfe52e97024b3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Configurazioni URL avanzate {#url}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) fornisce configurazioni avanzate per personalizzare gli URL per le pagine prodotto e categoria. Molte implementazioni personalizzeranno questi URL a scopo di ottimizzazione SEO (Search Engine Optimization).  Nei seguenti video viene descritto come configurare il `UrlProvider` servizio e le funzioni di Mappatura [](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) Sling per personalizzare gli URL per le pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare il `UrlProvider` servizio in base ai requisiti SEO e necessita di un progetto, è necessario fornire una configurazione OSGI per la configurazione &quot;CIF URL Provider configuration&quot; e configurare il servizio come descritto di seguito.

>[!NOTE]
>
> Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) , riportato di seguito, include configurazioni di esempio per dimostrare l&#39;utilizzo di URL personalizzati per le pagine di prodotti e categorie.

### Modello URL pagina prodotto {#product}

Questo consente di configurare gli URL delle pagine di prodotto con le seguenti proprietà:

* **Modello** URL prodotto: definisce il formato degli URL con un set di segnaposto. Il valore predefinito è `{{page}}.{{url_key}}.html#{{variant_sku}}`, che termina con la generazione di URL, ad esempio `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`
   * `{{page}}` è stato sostituito da `/content/venia/us/en/products/product-page`
   * `{{url_key}}` è stato sostituito da Magento  `url_key` proprietà del prodotto, qui `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` è stato sostituito dalla variante attualmente selezionata, qui `MH01-M-Orange`
* **Posizione** identificatore prodotto: definisce la posizione dell&#39;identificatore che verrà utilizzato per recuperare i dati del prodotto. Il valore predefinito è `SELECTOR`, l&#39;altro possibile è `SUFFIX`. Con l&#39;URL di esempio precedente, questo significa che l&#39;identificatore `chaz-kangeroo-hoodie` verrà utilizzato per recuperare i dati del prodotto.
* **Tipo** identificatore prodotto: definisce il tipo di identificatore da utilizzare per il recupero dei dati del prodotto. Il valore predefinito è `URL_KEY`, l&#39;altro possibile è `SKU`. Con l&#39;URL di esempio precedente, ciò significa che i dati del prodotto verranno recuperati con un filtro GraphQL di Magento come `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Modello URL pagina elenco prodotti {#product-list}

Questo consente di configurare gli URL delle pagine delle categorie o degli elenchi di prodotti con le seguenti proprietà:

* **Modello** URL categoria: definisce il formato degli URL con un set di segnaposto. Il valore predefinito è `{{page}}.{{id}}.html`, che termina con la generazione di URL, ad esempio `/content/venia/us/en/products/category-page.3.html`
   * `{{page}}` è stato sostituito da `/content/venia/us/en/products/category-page`
   * `{{id}}` è stato sostituito da Magento  `id` proprietà della categoria, qui `3`
* **Posizione** identificatore categoria: definisce la posizione dell&#39;identificatore che verrà utilizzato per recuperare i dati del prodotto. Il valore predefinito è `SELECTOR`, l&#39;altro possibile è `SUFFIX`. Con l&#39;URL di esempio precedente, questo significa che l&#39;identificatore `3` verrà utilizzato per recuperare i dati del prodotto.
* **Tipo** identificatore categoria: definisce il tipo di identificatore da utilizzare per il recupero dei dati del prodotto. Il valore predefinito e al momento solo il valore supportato è `ID`. Con l&#39;URL di esempio precedente, ciò significa che i dati della categoria verranno recuperati con un filtro GraphQL Magento come `category(id:3)`.

È possibile aggiungere proprietà personalizzate per ciascun modello, purché i dati corrispondenti vengano impostati dai componenti che utilizzano il modello `UrlProvider`. Controllate, ad esempio, il codice della `ProductListItemImpl` classe per sapere come viene implementato.

È inoltre possibile sostituire il `UrlProvider` servizio con un servizio OSGi completamente personalizzato. In questo caso, per sostituire l&#39;implementazione predefinita è necessario implementare l&#39; `UrlProvider` interfaccia e registrarla con una classificazione superiore.

## Combinazione con le mappature di sling {#sling-mapping}

Oltre a `UrlProvider`, è anche possibile configurare [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto AEM Archetype fornisce anche [una configurazione](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) di esempio per configurare alcune Mappature Sling per le porte 4503 (pubblicazione) e 80 (dispatcher).

## Combinazione con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando AEM server Dispatcher HTTP con `mod_rewrite` modulo. Il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce un riferimento AEM configurazione Dispatcher che già include regole [di](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) riscrittura di base per la dimensione generata.

## Esempio

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni di esempio per dimostrare l&#39;utilizzo di URL personalizzati per le pagine prodotto e categoria. Questo consente a ciascun progetto di impostare singoli pattern URL per le pagine di prodotti e categorie in base alle esigenze SEO. Si utilizza una combinazione di Mappature CIF `UrlProvider` e Sling come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le Mappature Sling funzionano in base al nome host e al dominio. Questa configurazione è pertanto disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinominare la `hostname.adobeaemcloud.com` cartella Sling Mapping in `ui.content/src/main/content/jcr_root/etc/map.publish/https` base al nome di dominio utilizzato e abilitare questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla `JcrResourceResolver` configurazione del progetto.

## Risorse aggiuntive

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappatura risorse AEM](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
