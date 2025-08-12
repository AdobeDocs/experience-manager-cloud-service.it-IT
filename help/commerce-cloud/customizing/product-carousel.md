---
title: Attributi personalizzati per il carosello dei prodotti CIF
description: Scopri come estendere il componente Carosello prodotto AEM CIF aggiornando il modello Sling e personalizzando il markup.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 758e0e13-c4d8-4d32-bcc9-91a36b3ffa98
index: false
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 4%

---

# Attributi personalizzati per il carosello dei prodotti CIF {#product-carousel}

## Introduzione {#intro}

Il componente Carosello prodotto viene esteso durante questa esercitazione. Come primo passo, aggiungi un’istanza del Carosello prodotto alla pagina Home per comprenderne le funzionalità di base:

1. Passa alla home page del sito, ad esempio [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. Inserisci un nuovo componente Carosello prodotto nel contenitore di layout principale della pagina.
   ![Componente Carosello prodotti](/help/commerce-cloud/assets/product-carousel-component.png)
1. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**.

   ![Prodotti carosello](/help/commerce-cloud/assets/carousel-products.png)

1. Dovrebbe essere visualizzato un elenco dei prodotti disponibili da un’istanza di Adobe Commerce connessa.

   ![Istanza connessa](/help/commerce-cloud/assets/connected-instance.png)

1. I prodotti verranno visualizzati come segue con le proprietà predefinite:

   ![Prodotto visualizzato con proprietà](/help/commerce-cloud/assets/discount.png)

## Aggiornare il modello Sling {#update-sling-model}

Puoi estendere la logica di business del carosello di prodotti implementando un modello Sling:

1. Nell&#39;IDE, passa al modulo core fino a `core/src/main/java/com/venia/core/models/commerce` e crea un&#39;interfaccia CustomCarousel che estende l&#39;interfaccia CIF ProductCarousel:

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```

1. Creare quindi una classe di implementazione `CustomCarouselImpl.java` in `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.
Il modello di delega per modelli Sling consente a `CustomCarouselImpl` di fare riferimento al modello `ProductCarousel` tramite la proprietà `sling:resourceSuperType`:

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. L’annotazione @PostConstruct assicura che questo metodo venga chiamato quando il modello Sling viene inizializzato. La query GraphQL del prodotto è già stata estesa utilizzando il metodo extendProductQueryWith per recuperare gli attributi. Aggiorna la query GraphQL per includere l’attributo nella query parziale:

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   Nel codice riportato sopra, `addCustomSimpleField` viene utilizzato per recuperare l&#39;attributo `accessory_gemstone_addon`.

## Personalizzazione del markup {#customize-markup}

Per personalizzare ulteriormente il markup:

1. Crea una copia di `productcard.html` da `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` (percorso crxde del componente core) al modulo ui.apps `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. Modificare `productcard.html` per chiamare l&#39;attributo personalizzato, indicato nella classe di implementazione:

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. Salva le modifiche e distribuisci gli aggiornamenti in AEM utilizzando il comando Maven, da un terminale della riga di comando. Nella pagina verrà visualizzato il valore dell&#39;attributo personalizzato `accessory_gemstone_addon` per i prodotti selezionati.
