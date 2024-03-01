---
title: Personalizzare i componenti core CIF
description: Scopri come personalizzare AEM componenti CIF di base. Il esercitazione spiega come estendere in modo sicuro un componente CIF di base per soddisfare i requisiti specifici dell'azienda. Scopri come estendere una query GraphQL per restituire un attributo personalizzato e visualizzare il nuovo attributo in un componente CIF di base.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 9%

---

# Personalizzare AEM componenti CIF di base {#customize-cif-components}

Il [progetto](https://github.com/adobe/aem-cif-guides-venia) CIF Venia è una base di codice di riferimento per l&#39;utilizzo dei [componenti](https://github.com/adobe/aem-core-cif-components) CIF di base. In questo esercitazione, si estende ulteriormente il [componente Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) prodotto per visualizzare un attributo personalizzato da Adobe Systems Commerce. Ulteriori informazioni sull&#39;integrazione di GraphQL tra AEM e Adobe Systems Commerce e sugli hook di estensione forniti dai componenti CIF di base.

>[!TIP]
>
> Utilizza l&#39;archetipo](https://github.com/adobe/aem-project-archetype) AEM [Project quando avvii la tua implementazione di commerce.

## Cosa costruirai

La Venia marchio recentemente ha iniziato a produrre alcuni prodotti utilizzando materiali sostenibili e l&#39;azienda avrebbe like di mostrare un **badge Eco Friendly** come parte del teaser del prodotto. In Adobe Systems Commerce viene creato un nuovo attributo personalizzato per indicare se un prodotto utilizza il **materiale ecologico** . Questo attributo personalizzato viene aggiunto come parte della query GraphQL e visualizzato nel teaser del prodotto per i prodotti specificati.

![Implementazione finale del badge ecologico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Prerequisiti {#prerequisites}

Per completare questo esercitazione è necessario un ambiente di sviluppo locale. Questo ambiente include un istanza in esecuzione di AEM configurato e connesso a un istanza di Adobe Systems Commerce. Esamina i requisiti e i passaggi per [la configurazione di uno sviluppo locale con AEM come SDK](../develop.md) Cloud Service. Per seguire completamente il esercitazione, è necessario autorizzazione aggiungere [attributi a un prodotto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) in Adobe Systems Commerce.

È inoltre necessario un IDE GraphQL come [GraphiQL](https://github.com/graphql/graphiql) o un&#39;estensione browser per eseguire gli esempi di codice e le esercitazioni. Se installi un&#39;estensione browser, assicurati che possa impostare intestazioni richiesta. Su Google Effetto cromatura, _Altair GraphQL Client_ è un&#39;estensione che può fare il lavoro.

## Clona Progetto Venia {#clone-venia-project}

Clona il [progetto](https://github.com/adobe/aem-cif-guides-venia) Venia, quindi eseguire l&#39;override degli stili predefiniti.

>[!NOTE]
>
> **Sentiti gratuito di utilizzare un progetto** esistente (basato sul AEM Project Archetype con CIF incluso) e salta questa sezione.

1. Esegui il seguente comando git in modo da poter clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie in modo da connettere il tuo AEM istanza a un istanza di Adobe Systems Commerce o aggiungi le configurazioni al progetto creato.

1. A questo punto, dovresti avere una versione funzionante di una vetrina collegata a un istanza Adobe Systems Commerce. Vai alla `US` pagina > `Home` all&#39;indirizzo: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandendo il menu principale del negozio, dovresti vedere varie categorie, indicando che la connessione a Adobe Systems Commerce funziona.

   ![Vetrina configurata con il tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Autore il teaser del prodotto {#author-product-teaser}

Il componente teaser del prodotto è stato esteso per tutta la esercitazione. Come primo passaggio, aggiungi una istanza del teaser del prodotto alla home page per comprendere la funzionalità di base.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. Espandi il pannello laterale (se non è già attivato) e sposta l&#39;elenco a discesa risorsa Finder su **Prodotti**. In questo elenco dovrebbe essere visualizzato un elenco dei prodotti disponibili da un istanza commerciale Adobe Systems connesso. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di _chiave inglese_).

4. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](../assets/customize-cif-components/product-teaser-default-style.png)

## Aggiungere un attributo personalizzato in Adobe Systems Commerce {#add-custom-attribute}

I prodotti e i dati di prodotto visualizzati in AEM sono memorizzati in Adobe Systems Commerce. Successivo aggiungere un attributo per **Eco Friendly** come parte del set di attributi prodotto utilizzando il interfaccia Adobe Systems Commerce.

>[!TIP]
>
> Hai già un attributo Sì/No **personalizzato** come parte del set di attributi del prodotto? Sentiti gratuito di usarlo e salta questa sezione.

1. Accedi al tuo istanza Commerce di Adobe Systems.
1. Passa al **Catalogo** > **prodotti**.
1. Aggiornare il filtro ricerca in modo da poter trovare il **Prodotto** configurabile utilizzato quando aggiunto al componente Teaser nell&#39;esercizio precedente. Apri il prodotto in modalità di modifica.

   ![Search per Valeria Prodotto](../assets/customize-cif-components/search-valeria-product.png)

1. Dalla vista del prodotto, fai clic su Aggiungi attributo **>** su **Crea Nuovo Attributo**.
1. Compila il **modulo Attributo Nuovo** con i seguenti valori (lascia le impostazioni predefinite per gli altri valori)

   | Set di campi | Etichetta campo | Valore |
   | ----------------------------- | ------------------ | ---------------- |
   | Attributo Proprietà | Attribute Etichetta | **Ecologico** |
   | Attributo Proprietà | Tipo di input catalogo | **Sì/No** |
   | Proprietà attributi Avanzate | Attributo Code | **eco_friendly** |

   ![Nuovo Modulo attributi](../assets/customize-cif-components/attribute-new-form.png)

   Al termine fate clic su **Salva Attributo** .

1. Scorri fino alla fine del prodotto ed espandi l&#39;intestazione **Attributi** . Dovresti vedere il nuovo **campo Eco Friendly** . Imposta l&#39;interruttore su **Sì**.

   ![Passa a Sì](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** Salva le modifiche apportate al prodotto.

   >[!TIP]
   >
   > Ulteriori dettagli sulla gestione degli [attributi del prodotto sono disponibili nella guida](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html) utente di Adobe Systems Commerce.

1. Accedi a **System > Strumenti** > **** Cache Management ****. Poiché è stato effettuato un aggiornamento allo schema dei dati, è necessario invalidare alcuni tipi di cache in Adobe Systems Commerce.
1. Seleziona la casella accanto a Configurazione **** e invia il tipo di cache per **Aggiorna**

   ![Tipo di cache di configurazione Aggiorna](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Ulteriori dettagli sulla [gestione della cache sono disponibili nella guida](https://docs.magento.com/user-guide/system/cache-management.html) utente di Adobe Systems Commerce.

## Utilizzare un IDE GraphQL per verificare l&#39;attributo {#use-graphql-ide}

Prima di passare al codice AEM, è utile esplorare la panoramica](https://devdocs.magento.com/guides/v2.4/graphql/) di [GraphQL utilizzando un IDE GraphQL. L&#39;integrazione di Adobe Systems Commerce con AEM avviene principalmente tramite una serie di query GraphQL. La comprensione e la modifica delle query GraphQL è uno dei modi principali in cui i componenti CIF Core possono essere estesi.

Successivo, utilizzare un IDE GraphQL per verificare che l&#39;attributo `eco_friendly` sia stato aggiunto al set di attributi del prodotto. Le schermate in questo esercitazione utilizzano l&#39;estensione _Altair GraphQL Client_ Google Effetto cromatura extension.

1. Apri l&#39;IDE GraphQL e inserisci il URL `http://<commerce-server>/graphql` nella barra URL dell&#39;IDE o dell&#39;estensione.
2. Aggiungi i seguenti [prodotti Chiedi](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) dove `YOUR_SKU` è il **referenza di magazzino** del prodotto utilizzato nell&#39;esercizio precedente:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Esegui la query e otterrai una risposta like quanto segue:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Risposta GraphQL di esempio](../assets/customize-cif-components/sample-graphql-query.png)

   Il valore di **Sì** è un numero intero pari a **1**. Questo valore è utile quando si scrive la query GraphQL in Java™.

   >[!TIP]
   >
   > Leggi una documentazione più dettagliata su [Adobe Systems Commerce GraphQL qui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Aggiornare il modello Sling per il teaser del prodotto {#updating-sling-model-product-teaser}

Successivo, estendete la logica di business del teaser di prodotto implementando un modello Sling. [Gli Sling Model](https://sling.apache.org/documentation/bundles/models.html) sono &quot;POJO&quot; (Plain Old Java™ Objects) guidati da annotazione che implementare logica di business necessari al componente. I modelli Sling vengono utilizzati con gli script HTL come parte del componente. Seguire il [modello di delega per i modelli](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling in modo da poter estendere parti del modello Teaser prodotto esistente.

I modelli Sling sono implementati come Java™ e possono essere trovati nel **modulo principale** del progetto generato.

Utilizza [l&#39;IDE di tua scelta](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) per importare il progetto Venia. Le schermate utilizzate provengono dall&#39;IDE di [Visual Studio Code](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. Nell&#39;IDE, passa sotto il **modulo core** per: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE posizione principale](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` è un&#39;interfaccia Java™ che estende l&#39;interfaccia CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) .

   È già stato aggiunto un nuovo metodo denominato `isShowBadge()` per visualizzare un badge se il prodotto è considerato &quot;Nuovo&quot;.

1. Aggiungi `isEcoFriendly()` all&#39;interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Questo nuovo metodo è stato introdotto per incapsulare la logica per indicare se il prodotto ha l&#39;attributo `eco_friendly` impostato su **Sì** o **No**.

1. Successivo, ispezionare l&#39;at `MyProductTeaserImpl.java` `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   Il [pattern di delega per i modelli](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling consente `MyProductTeaserImpl` di fare riferimento `ProductTeaser` al modello tramite la `sling:resourceSuperType` proprietà:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per i metodi che non si desidera ignorare o modificare, è possibile restituire il valore restituito `ProductTeaser` . Ad esempio:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Questo metodo riduce al minimo la quantità di codice Java™ che un implementazione deve scrivere.

1. Uno dei punti di estensione aggiuntivi forniti da AEM CIF Core Components è il `AbstractProductRetriever` che fornisce accesso a specifici attributi del prodotto. Inspect il `initModel()` metodo:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to initialize the productRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   Il `@PostConstruct` annotazione garantisce che questo metodo venga chiamato quando viene inizializzato il modello Sling.

   Si noti che la query GraphQL del prodotto è già stata estesa utilizzando il `extendProductQueryWith` metodo per recuperare l&#39;attributo aggiuntivo `created_at` . Questo attributo viene successivamente utilizzato come parte del `isShowBadge()` metodo.

1. Aggiornare la query GraphQL per includere l&#39;attributo `eco_friendly` nella query parziale:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   L&#39;aggiunta `extendProductQueryWith` al metodo è un modo efficace per garantire che attributi di prodotto aggiuntivi siano disponibili per il resto del modello. Inoltre si riduce la quantità di query eseguite.

   Nel codice sopra riportato, viene`addCustomSimpleField` utilizzato per recuperare l&#39;attributo `eco_friendly` . Questo attributo illustra come eseguire query per qualsiasi attributo personalizzato che fa parte dello schema di Adobe Systems Commerce.

   >[!NOTE]
   >
   > Il `createdAt()` metodo è stato implementato come parte dell&#39;interfaccia [](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)prodotto. La maggior parte degli attributi dello schema comunemente trovati è già stata implementata, quindi utilizza solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Aggiungi un logger in modo da poter debug il codice Java™:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Successivo, implementare il `isEcoFriendly()` metodo:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   Nel metodo precedente, viene utilizzato per recuperare il prodotto e il metodo viene `productRetriever` utilizzato per ottenere il `getAsInteger()` valore dell&#39;attributo `eco_friendly` . Sulla base delle query GraphQL eseguite in precedenza, si sa che il valore previsto quando l&#39;attributo `eco_friendly` è impostato su &quot;Sì&#x200B;**&quot;** è in realtà un numero intero di **1**.

   Ora che il modello Sling è stato aggiornato, il markup del componente deve essere aggiornato per visualizzare effettivamente un indicatore di **Eco Friendly** basato sul modello Sling.

## Personalizzazione del markup del teaser prodotto {#customize-markup-product-teaser}

I componenti AEM vengono spesso estesi per modificare il markup generato dal componente. Questa modifica viene eseguita sovrascrivendo lo [script](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) HTL utilizzato dal componente per eseguire il rendering del markup. HTML Template Lingua (HTL) è un linguaggio di template leggero che i componenti AEM utilizzano per eseguire dinamicamente il rendering del markup in base ai contenuto creati, consentendo il riutilizzo dei componenti. Il teaser del prodotto, ad esempio, può essere riutilizzato più e più volte per visualizzare prodotti diversi.

In questo caso, desideri eseguire il rendering di un banner sopra il teaser per indicare che il prodotto è &quot;Eco Friendly&quot; in base a un attributo personalizzato. Il modello di progettazione per la personalizzazione del markup](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è standard per tutti i componenti AEM, non solo per [i componenti CIF Core AEM.

>[!NOTE]
>
> Se personalizzi un componente utilizzando i prodotti CIF e i selettori di categorie, like questo teaser di prodotto o il componente della pagina CIF, assicurati di includere la clientlib richiesta `cif.shell.picker` per le finestre di dialogo dei componenti. Per i dettagli, vedere [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md) .

1. Nell&#39;IDE, esplorare ed espandere il modulo ed espandere la gerarchia di cartelle per: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` ed esaminare il `.content.xml` `ui.apps` file.

   ![Teaser prodotto ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   La definizione del componente riportata sopra si riferisce al componente teaser del prodotto nel progetto. Osserva la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questa proprietà è un esempio di creazione di un [componente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components) proxy. Anziché copiare e incollare gli script HTL del teaser del prodotto dai componenti CIF Core di AEM, è possibile utilizzare il `sling:resourceSuperType` comando per ereditare tutte le funzionalità.

1. Aprire il file `productteaser.html`. Questo file è una copia del `productteaser.html` file dal [teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) del prodotto CIF.

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Si noti che il modello Sling per `MyProductTeaser` viene utilizzato e assegnato alla `product` variabile.

1. Modificare `productteaser.html` in modo da poter chiamare il `isEcoFriendly` metodo implementato nell&#39;esercizio precedente:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Quando si chiama un metodo Sling Model in HTL, la parte and `is` del metodo viene eliminata e la `get` prima lettera viene minuscola. Così `isShowBadge()` diventa e `isEcoFriendly` diventa `.ecoFriendly``.showBadge` . In base al valore booleano restituito da `.isEcoFriendly()` determina se l&#39;elemento `<span>Eco Friendly</span>` viene visualizzato.

   Ulteriori informazioni su `data-sly-test` e altre [istruzioni di blocco HTL sono disponibili qui](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. Salva le modifiche e distribuire aggiornamenti per AEM usando le tue abilità Maven, da un terminale a riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Apri una nuova finestra di browser e vai alla AEM e alla **console** OSGi > Stato **>****modelli Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Search per `MyProductTeaserImpl` e dovresti vedere una riga like seguente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Questa riga indica che il modello Sling è correttamente distribuito e mappato sul componente corretto.

1. Aggiorna al Pagina **Venia Home in [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) dove è stato aggiunto il** teaser del prodotto.

   ![Messaggio ecologico visualizzato](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se il prodotto ha l&#39;attributo `eco_friendly` impostato su **Sì**, dovresti vedere il testo &quot;Eco Friendly&quot; nella pagina. Prova a passare a prodotti diversi per vedere il cambiamento di comportamento.

1. Successivo aprire il AEM `error.log` per visualizzare le istruzioni di registro aggiunte. Il `error.log` è a `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Search i registri AEM per visualizzare le istruzioni di registro aggiunte nel modello Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > È inoltre possibile visualizzare alcune tracce dello stack se il prodotto utilizzato nel teaser non dispone dell&#39;attributo `eco_friendly` come parte del set di attributi.

## Aggiungi stili per il badge ecologico {#add-styles}

A questo punto la logica per quando visualizzare il badge Eco Friendly **sta funzionando, tuttavia il** testo normale potrebbe utilizzare alcuni stili. Successivo aggiungere un&#39;icona `ui.frontend` e degli stili al modulo per completare il implementazione.

1. Scarica il [file eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) . Questo file viene utilizzato come **badge Eco Friendly** .
1. Tornare all&#39;IDE e passare alla `ui.frontend` cartella.
1. Aggiungere il `eco_friendly.svg` file alla `ui.frontend/src/main/resources/images` cartella:

   ![SVG ecologico aggiunto](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Aprire il file `productteaser.scss` in `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Aggiungi le seguenti regole Sass all&#39;interno della `.productteaser` classe:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > Consulta [Styling CIF Core Components](./style-cif-component.md) per altri dettagli sui flussi di lavoro front-end.

1. Salva le modifiche e distribuire aggiornamenti per AEM usando le tue abilità Maven, da un terminale a riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiorna al Pagina **Venia Home in [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) dove è stato aggiunto il** teaser del prodotto.

   ![Implementazione finale del badge ecologico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Congratulazioni {#congratulations}

Hai personalizzato il tuo primo componente CIF AEM! Scarica qui i file](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip) della [soluzione finita.

## Sfida bonus {#bonus-challenge}

Esamina la funzionalità del badge Nuovo **già implementato nel teaser del** prodotto. Prova ad aggiungere una casella di controllo aggiuntiva per consentire agli autori di controllare quando deve essere visualizzato il **badge Eco Friendly** . Aggiornare la finestra di dialogo del componente in `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuovo Sfida di implementazione badge](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Risorse aggiuntive {#additional-resources}

- [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
- [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizzazione dei componenti core CIF di AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/customize-cif-components.html)
- [Personalizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=it)
- [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)
- [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md)
