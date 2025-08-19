---
title: Metadati JSON+LD
description: Scopri come abilitare e verificare la funzione JSON+LD in AEM CIF.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 2%

---


# Metadati JSON+LD {#json-ld}

Questa guida spiega come abilitare e verificare la funzione JSON+LD in AEM CIF.

>[!NOTE]
>
> Questa funzione è sperimentale.

## Abilitazione di JSON+LD nella configurazione del CIF {#enabling}

Per impostazione predefinita, la casella di controllo **Abilita JSON+LD** non è visibile nella configurazione di CIF. Per abilitare questa funzione, il progetto deve includere la configurazione OSGi necessaria, che consente di visualizzare la casella di controllo. Questa configurazione consente agli utenti di attivare o disattivare il supporto per script JSON+LD nelle pagine dei prodotti.

Per rendere disponibile la casella di controllo **Abilita JSON+LD** nella configurazione di CIF, aggiungi la seguente configurazione OSGi al progetto:

`com.adobe.cq.cif.components.models.JsonLdFeatureEnable`.

Per ulteriori dettagli sull&#39;aggiunta di questa configurazione, fai riferimento a [Aggiunge la configurazione per Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json) nell&#39;archivio pubblico aem-cif-guides-venia.

Dopo aver aggiunto e distribuito questa configurazione, la casella di controllo diventa visibile nelle impostazioni di configurazione di CIF. Di seguito sono riportati i passaggi per abilitare **JSON+LD**:

1. Passa alla configurazione CIF in AEM.
1. Annulla ereditarietà.
1. Selezionare la casella di controllo **Abilita JSON+LD**.
1. Salva la configurazione.

## Verifica di JSON+LD in una pagina di dettagli del prodotto (PDP) {#verify}

Per illustrare i passaggi per verificare JSON+LD, si utilizza il progetto Venia come esempio, in cui la configurazione JSON+LD richiesta è già stata aggiunta per abilitare la funzione. Di seguito sono riportati i passaggi da seguire:

1. Passa all&#39;istanza AEM locale e apri la pagina dettagli prodotto (PDP): `http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html`
1. Creare un prodotto nella pagina dettagli prodotto (PDP).
1. Passa alla modalità **Visualizza come pubblicazione**.
1. Apri **Visualizza pagina Source** nel browser.
1. Cerca JSON+LD nell’origine della pagina.

Se configurato correttamente, troverai lo script JSON+LD associato al prodotto inserito nella pagina.

## Esempio di struttura JSON+LD per un prodotto {#sample}

Di seguito è riportata una struttura di esempio **JSON+LD** per la gonna Agatha, creata sulla pagina PDP nel progetto Venia:

```html
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## Mappatura di attributi JSON+LD a GraphQL {#mapping}

Gli attributi JSON+LD possono essere mappati su query GraphQL in AEM CIF, garantendo che i dati strutturati riflettano dinamicamente le informazioni di prodotto recuperate tramite GraphQL.

### Esempio di mappatura del prodotto {#example}

| Attributo JSON+LD | Attributo GraphQL Magento | Obbligatorio (S/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | Logica personalizzata | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | valuta | Y |
| offers.priceSpecification.price | prezzo_regolare | N |
| offers.priceCurrency | valuta | Y |
| offers.price | prezzo_speciale | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| nome | nome | Y |
| immagine | media_gallery.url | Y |
| descrizione | descrizione | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | riepilogo_valutazione | N |
| @id | id | N |

Questa mappatura assicura che lo script JSON+LD sia popolato dinamicamente in base ai dati del prodotto recuperati tramite query GraphQL.

Per verificare la struttura JSON+LD, puoi utilizzare il test dei risultati avanzati di [ nella console di ricerca di Google.](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw) Questo strumento fornisce un feedback dettagliato, indicando se gli attributi richiesti sono presenti o mancanti, e aiuta a garantire che i dati strutturati siano correttamente implementati.
