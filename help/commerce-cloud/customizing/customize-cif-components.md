---
title: Personalizzare i componenti core CIF
description: Scoprite come personalizzare AEM componenti CIF di base. L'esercitazione illustra come estendere in modo sicuro un componente CIF di base per soddisfare requisiti aziendali specifici. Scoprite come estendere una query GraphQL per restituire un attributo personalizzato e visualizzare il nuovo attributo in un componente CIF di base.
sub-product: commerce
topics: development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
kt: 4279
thumbnail: 4279-customize-cif.jpg
translation-type: tm+mt
source-git-commit: 34b4dc697d3fb8c3f81e16ee3cab5d768e42b99c
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 30%

---


# Personalizzare i componenti core CIF di AEM {#customize-cif-components}

Il progetto [](https://github.com/adobe/aem-cif-guides-venia) CIF Venia è una base di codice di riferimento per l&#39;utilizzo dei componenti [di base](https://github.com/adobe/aem-core-cif-components)CIF. In questa esercitazione, estenderete ulteriormente il componente [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) per visualizzare un attributo personalizzato dall’Magento. Scoprirete inoltre ulteriori informazioni sull&#39;integrazione GraphQL tra AEM e Magento e i ganci di estensione forniti dai componenti CIF di base.

>[!TIP]
>
> Utilizza il [AEM archetipo](https://github.com/adobe/aem-project-archetype) del progetto quando avvii la tua implementazione commerciale.

## Cosa verrà creato

Il marchio Venia ha recentemente iniziato a produrre alcuni prodotti utilizzando materiali sostenibili e l&#39;azienda desidera visualizzare un marchio **eco-compatibile** come parte del Product Teaser. Un nuovo attributo personalizzato verrà creato in Magento per indicare se un prodotto utilizza materiale **eco-compatibile** . Questo attributo personalizzato verrà quindi aggiunto come parte della query GraphQL e visualizzato sul Product Teaser per prodotti specifici.

![Implementazione finale del marchio di qualità ecologica](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Ciò include un&#39;istanza in esecuzione di AEM configurata e connessa a un&#39;istanza di Magento. Verifica i requisiti e i passaggi per [configurare uno sviluppo locale con AEM come SDK](../develop.md)di Cloud Service. Per seguire completamente l&#39;esercitazione, è necessario disporre delle autorizzazioni per aggiungere [attributi a un prodotto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) in un Magento.

È inoltre necessario GraphQL IDE, ad esempio [GraphiQL](https://github.com/graphql/graphiql) o un&#39;estensione del browser per eseguire gli esempi di codice e le esercitazioni. Se installate un&#39;estensione del browser, accertatevi che sia in grado di impostare le intestazioni della richiesta. In Google Chrome, [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) è un&#39;estensione che può eseguire il processo.

## Clona il progetto Venia {#clone-venia-project}

Cloneremo il Progetto [](https://github.com/adobe/aem-cif-guides-venia) Venia e quindi ignoreremo gli stili predefiniti.

>[!NOTE]
>
> **Sentitevi liberi di utilizzare un progetto** esistente (basato sul AEM Project Archetype con CIF incluso) e saltate questa sezione.

1. Eseguite il seguente comando git per duplicare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina che sia collegata a un’istanza di Magento. Navigate to the `US` > `Home` page at: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina: dovresti vedere diverse categorie, a indicare che la connessione a Magento funziona.

   ![Storefront configurato con il tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creare il Product Teaser {#author-product-teaser}

Il componente Product Teaser verrà esteso in questa esercitazione. Come primo passo, aggiungete una nuova istanza del Product Teaser alla pagina principale per comprendere la funzionalità di base.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**. Dovrebbe essere visualizzato un elenco di prodotti disponibili da un’istanza di Magento connessa. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di *chiave inglese*).

4. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](../assets/customize-cif-components/product-teaser-default-style.png)

## Aggiunta di un attributo personalizzato nel Magento {#add-custom-attribute}

I prodotti e i dati del prodotto visualizzati in AEM vengono memorizzati nel Magento. Quindi aggiungete un nuovo attributo per **Eco Friendly** come parte dell’attributo di prodotto impostato utilizzando l’interfaccia utente del Magento.

>[!TIP]
>
> Disponete già di un attributo **Sì/No** personalizzato come parte del set di attributi del prodotto? Sentitevi liberi di usarlo e saltare questa sezione.

1. Accedete all’istanza del Magento.
1. Passa a **Catalogo** > **Prodotti**.
1. Aggiornate il filtro di ricerca per trovare il Prodotto **** configurabile utilizzato quando aggiunto al componente Teaser nell’esercizio precedente. Aprite il prodotto in modalità di modifica.

   ![Cerca prodotto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. Dalla visualizzazione prodotto, fate clic su **Aggiungi attributo** > **Crea nuovo attributo**.
1. Compilare il modulo **Nuovo attributo** con i seguenti valori (lasciare le impostazioni predefinite per altri valori)

   | Set di campi | Etichetta campo | Valore |
   |-----------|-------------|---------|
   | Proprietà attributo | Etichetta attributo | **Ecologico** |
   | Proprietà attributo | Tipo di input catalogo | **Sì/No** |
   | Proprietà attributo avanzate | Codice attributo | **eco_friendly** |

   ![Nuovo modulo attributo](../assets/customize-cif-components/attribute-new-form.png)

   Al termine, fate clic su **Salva attributo** .

1. Scorrete fino in fondo al prodotto ed espandete l&#39;intestazione **Attributi** . Dovresti vedere il nuovo campo **Eco Friendly** . Passate l’interruttore a **Sì**.

   ![Passa a Sì](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salvare** le modifiche apportate al prodotto.

   >[!TIP]
   >
   > Ulteriori dettagli sulla gestione degli attributi [del prodotto sono disponibili nella guida](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)utente del Magento.

1. Andate a **Sistema** > **Strumenti** > Gestione **cache**. Poiché è stato effettuato un aggiornamento allo schema di dati, è necessario annullare alcuni dei tipi di cache nel Magento.
1. Selezionare la casella accanto a **Configurazione** e inviare il tipo di cache per **Aggiorna**

   ![Aggiorna tipo cache configurazione](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Maggiori dettagli sulla gestione della [cache sono disponibili nella guida](https://docs.magento.com/user-guide/system/cache-management.html)utente del Magento.

## Usare un IDE GraphQL per verificare l&#39;attributo {#use-graphql-ide}

Prima di passare AEM codice è utile esplorare il [Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) utilizzando un IDE GraphQL. L&#39;integrazione del Magento con AEM viene realizzata principalmente tramite una serie di query GraphQL. Comprendere e modificare le query GraphQL è uno dei modi principali in cui i componenti CIF di base possono essere estesi.

Quindi, utilizzate un IDE GraphQL per verificare che l&#39; `eco_friendly` attributo sia stato aggiunto al set di attributi del prodotto. Le schermate in questa esercitazione utilizzano il client [Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Aprite l’IDE GraphQL e immettete l’URL `http://<magento-server>/graphql` nella barra dell’URL dell’IDE o dell’estensione.
2. Aggiungete la seguente query [](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) sui prodotti in cui `YOUR_SKU` è **lo SKU** del prodotto utilizzato nell&#39;esercizio precedente:

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

3. Esegui la query e ottieni una risposta come segue:

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

   ![Esempio di risposta GraphlQL](../assets/customize-cif-components/sample-graphql-query.png)

   Il valore di **Yes** è un numero intero di **1**. Questo sarà utile quando scriveremo la query GraphQL in Java.

   >[!TIP]
   >
   > La documentazione più dettagliata sul [Magento GraphQL è disponibile qui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Update the Sling Model for the Product Teaser {#updating-sling-model-product-teaser}

Ora estenderemo la logica di business del Product Teaser implementando un modello Sling. I [modelli Sling](https://sling.apache.org/documentation/bundles/models.html) sono “POJO” (Plain Old Java Objects) basati su annotazioni che implementano la logica di business necessaria per il componente. I modelli Sling vengono utilizzati insieme agli script HTL come parte del componente. Seguiremo il [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) in modo da estendere solo parti del modello esistente di Product Teaser.

I modelli Sling sono implementati come Java e si trovano nel modulo **core** del progetto generato.

Utilizzate [l&#39;IDE di vostra scelta](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) per importare il progetto Venia. Gli screenshot utilizzati sono tratti dall&#39;IDE [di codice di](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)Visual Studio.

1. Nell’IDE, naviga sotto il modulo **principale** per: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE posizione chiave](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` è un&#39;interfaccia Java che estende l&#39;interfaccia CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) .

   È già stato aggiunto un nuovo metodo denominato `isShowBadge()` per visualizzare un contrassegno se il prodotto è considerato &quot;Nuovo&quot;.

1. Aggiungi il nuovo metodo `isEcoFriendly()` all’interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Questo è un nuovo metodo che introdurremo per incapsulare la logica per indicare se l&#39; `eco_friendly` attributo del prodotto è impostato su **Yes** o **No**.

1. Quindi, ispezionate la `MyProductTeaserImpl.java` pagina `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   Il pattern di [delega per Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) consente `MyProductTeaserImpl` di fare riferimento `ProductTeaser` al modello tramite la `sling:resourceSuperType` proprietà:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per tutti i metodi che non dovranno essere ignorati o modificati, possiamo semplicemente restituire il valore che `ProductTeaser` restituisce. Esempio:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Questo riduce al minimo la quantità di codice Java che l&#39;implementazione deve scrivere.

1. One of the extra extension points provided by AEM CIF Core Components is the `AbstractProductRetriever` which provides access to specific product attributes.  Inspect il `initModel()` metodo:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   L&#39; `@PostConstruct` annotazione assicura che questo metodo venga chiamato non appena viene inizializzato il modello Sling.

   Tenere presente che la query GraphQL del prodotto è già stata estesa utilizzando il `extendProductQueryWith` metodo per recuperare l&#39; `created_at` attributo aggiuntivo. Questo attributo viene utilizzato successivamente come parte del `isShowBadge()` metodo.

1. Aggiornate la query GraphQL per includere l&#39; `eco_friendly` attributo nella query parziale:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   Con l’aggiunta al metodo `extendProductQueryWith`, gli attributi di prodotto aggiuntivi saranno disponibili per il resto del modello. Inoltre si riduce la quantità di query eseguite.

   Nel codice riportato sopra,`addCustomSimpleField` viene utilizzato per recuperare l&#39; `eco_friendly` attributo. Questo illustra come eseguire una query per gli attributi personalizzati che fanno parte dello schema di Magento.

   >[!NOTE]
   >
   > Il `createdAt()` metodo è stato implementato nell&#39;ambito dell&#39;interfaccia [prodotto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). La maggior parte degli attributi dello schema comunemente trovati è già stata implementata, quindi utilizza solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Aggiungete un logger per eseguire il debug del codice Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Quindi, implementate il `isEcoFriendly()` metodo:

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

   Nel metodo precedente `productRetriever` viene utilizzato per recuperare il prodotto e il `getAsInteger()` metodo viene utilizzato per ottenere il valore dell&#39; `eco_friendly` attributo. In base alle query GraphQL eseguite in precedenza, sappiamo che il valore previsto quando l&#39; `eco_friendly` attributo è impostato su &quot;**Yes**&quot; è in realtà un numero intero di **1**.

   Ora che il modello Sling è stato aggiornato, la marcatura componente deve essere aggiornata per visualizzare un indicatore di **eco-compatibile** basato sul modello Sling.

## Personalizzazione del markup del Product Teaser {#customize-markup-product-teaser}

I componenti AEM vengono spesso estesi per modificare il markup generato dal componente. A tal fine, sovrascrivi lo [script HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) utilizzato dal componente per eseguire il rendering del relativo markup. HTML Template Language (HTL) è un linguaggio per modelli leggero usato dai componenti di AEM per eseguire il rendering dinamico del markup in base al contenuto creato, in modo che sia possibile riutilizzare i componenti. Il Product Teaser, ad esempio, può essere riutilizzato più volte per visualizzare prodotti diversi.

Nel nostro caso, vogliamo eseguire il rendering di un banner sopra al teaser per indicare che il prodotto è &quot;Eco Friendly&quot; basato su un attributo personalizzato. Il modello di progettazione per [personalizzare il markup](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è in realtà standard per tutti i componenti di AEM, non solo per i componenti core CIF di AEM.

1. In the IDE, navigate and expand the `ui.apps` module and expand the folder hierarchy to: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` and inspect the `.content.xml` file.

   ![App ui.apps per teaser prodotto](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Questa è la definizione del componente Product Teaser usato nel nostro progetto. Osserva la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questo è un esempio di creazione di un [componente Proxy](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Invece di copiare e incollare tutti gli script HTL di Product Teaser dai componenti core CIF di AEM, possiamo utilizzare `sling:resourceSuperType` per ereditare tutte le funzionalità.

1. Aprire il file `productteaser.html`. Questa è una copia del `productteaser.html` file da [CIF Product Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
       data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
       data-sly-use.actionsTpl="actions.html"
       data-sly-test.isConfigured="${properties.selection}"
       data-sly-test.hasProduct="${product.url}">
   ```

   Tenere presente che il modello Sling per `MyProductTeaser` viene utilizzato e assegnato alla `product` variabile.

1. Modificare `productteaser.html` per eseguire una chiamata al `isEcoFriendly` metodo implementato nell&#39;esercizio precedente:

   ```html
   ...
   <div data-sly-test="${isConfigured && hasProduct}" class="item__root" data-cmp-is="productteaser" data-virtual="${product.virtualProduct}">
       <div data-sly-test="${product.showBadge}" class="item__badge">
           <span>${properties.text || 'New'}</span>
       </div>
       <!--/* Insert call to Eco Friendly here */-->
       <div data-sly-test="${product.ecoFriendly}" class="item__eco">
           <span>Eco Friendly</span>
       </div>
   ...
   ```

   Quando si chiama un metodo Sling Model in HTL, la `get` parte e `is` la parte del metodo vengono ignorate e la prima lettera viene minuscola. Così `isShowBadge()` diventa `.showBadge` e `isEcoFriendly` diventa `.ecoFriendly`. In base al valore booleano restituito da `.isEcoFriendly()` , viene determinato se la visualizzazione `<span>Eco Friendly</span>` è attiva.

   Ulteriori informazioni su `data-sly-test` e altre istruzioni di blocco [HTL sono disponibili qui](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. Salva le modifiche e distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aprite una nuova finestra del browser e accedete a AEM e alla console **OSGi >** Stato **>** Modelli **** Sling: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Cerca `MyProductTeaserImpl` e dovresti visualizzare una riga come segue:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Indica che il modello Sling è stato distribuito correttamente e mappato sul componente corretto.

1. Aggiornate alla home page **di** Venia all&#39;indirizzo [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) in cui è stato aggiunto il teaser prodotto.

   ![Messaggio eco-compatibile visualizzato](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se l&#39; `eco_friendly` attributo del prodotto è impostato su **Sì**, sulla pagina verrà visualizzato il testo &quot;Eco Friendly&quot;. Provate a passare a prodotti diversi per vedere il cambiamento di comportamento.

1. Aprite quindi il AEM `error.log` per visualizzare le istruzioni di registro aggiunte. La `error.log` si trova a `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Cerca nei registri AEM per visualizzare le istruzioni di registro aggiunte nel modello Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > È anche possibile che vengano visualizzate delle tracce di stack se il prodotto utilizzato nel teaser non ha l&#39; `eco_friendly` attributo come parte del set di attributi.

## Aggiungere stili per il contrassegno eco-compatibile {#add-styles}

A questo punto la logica per quando visualizzare il contrassegno **Eco Friendly** funziona, ma il testo normale potrebbe usare alcuni stili. Quindi aggiungete un&#39;icona e degli stili al `ui.frontend` modulo per completare l&#39;implementazione.

1. Scaricate il file [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) . Questo verrà usato come **marchio amico** dell&#39;eco.
1. Tornate all’IDE e individuate la `ui.frontend` cartella.
1. Aggiungete il `eco_friendly.svg` file alla `ui.frontend/src/main/resources/images` cartella:

   ![SVG eco-compatibile aggiunto](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Open the file `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Aggiungete le seguenti regole Sass all&#39;interno della `.productteaser` classe:

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
   > Per ulteriori informazioni sui flussi di lavoro front-end, consulta [Styling CIF Core Components](./style-cif-component.md) .

1. Salva le modifiche e distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aggiornate alla home page **di** Venia all&#39;indirizzo [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) in cui è stato aggiunto il teaser prodotto.

   ![Implementazione finale del marchio di qualità ecologica](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Congratulazioni {#congratulations}

Hai appena personalizzato il tuo primo componente CIF di AEM. Download the [finished solution files here](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Sfida bonus {#bonus-challenge}

Rivedete la funzionalità del **nuovo** badge che è già stato implementato nel Product Teaser. Provate ad aggiungere una casella di controllo aggiuntiva per consentire agli autori di controllare quando deve essere visualizzato il contrassegno **eco-compatibile** . Sarà necessario aggiornare la finestra di dialogo del componente in `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuova sfida per l&#39;implementazione dei badge](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalizzazione dei componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalizzazione dei componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/customizing.html)
* [Guida introduttiva di AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)