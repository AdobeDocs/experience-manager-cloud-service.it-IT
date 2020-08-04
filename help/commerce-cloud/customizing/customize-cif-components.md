---
title: Personalizza componenti CIF di base
description: Personalizza componenti CIF di base
translation-type: tm+mt
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 1%

---


# Personalizzare i componenti AEM CIF di base {#customize-cif-components}

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) fornisce un set standard di componenti Commerce che possono essere utilizzati per accelerare un progetto che integra soluzioni  Adobe Experience Manager (AEM) e Magento. Questi componenti sono pronti per la produzione e possono essere [facilmente formattati con i CSS](style-cif-component.md). Molte implementazioni vorranno anche estendere questi componenti per soddisfare requisiti aziendali specifici.

In questa esercitazione verranno esaminati diversi punti di estensione forniti da AEM CIF Core Components e AEM in generale. A tal fine, estenderemo le capacità del componente [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) per includere la capacità di eseguire il rendering di un banner &quot;Nuovo&quot;. Gli autori dei contenuti potranno attivare/disattivare questo banner e determinare per quanto tempo visualizzare il banner. La &quot;età&quot; del prodotto sarà basata sulla data di creazione nel catalogo del Magento. Quando un prodotto ha una certa quantità di giorni, il banner &quot;Nuovo&quot; deve scomparire automaticamente.

![Nuovo banner esteso](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Prerequisiti {#prerequisites}

Sono necessari i seguenti strumenti e tecnologie:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
* [AEM Cloud SKD con componente aggiuntivo CIF](../develop.md)
* Magento compatibile con componenti CIF di base

Prima di continuare con questa esercitazione, è consigliabile consultare il contenuto seguente:

* [Introduzione di Commerce Integration Framework in AEM come Cloud Service](/help/commerce-cloud/overview.md)
* [Stile AEM componenti CIF di base - Esercitazione](style-cif-component.md)

## Progetto iniziale

Abbiamo fornito un progetto iniziale da utilizzare con questa esercitazione. Il progetto è stato generato utilizzando la [v0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) del tipo di archivio del progetto CIF. È consigliabile utilizzare sempre l&#39; [ultima versione](https://github.com/adobe/aem-cif-project-archetype/releases/latest) di archetype all&#39;avvio di un nuovo progetto.

1. Scarica il progetto iniziale [**acme-store.zip **](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)sul desktop.

1. Decomprimete **acme-store.zip** e visualizzate la seguente struttura di cartelle:

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. Aprite una nuova finestra terminale e create e distribuite il progetto in un’istanza locale di AEM;

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Aggiungete le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungere le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di uno storefront che sia collegata a un&#39;istanza di Magento. Passa alla pagina `US` > `Home` in: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Dovresti vedere che il negozio al momento sta usando il tema Venia. Se si espande il menu principale dello storefront, dovrebbero essere visualizzate diverse categorie, a indicare che il Magento di connessione funziona.

   ![Storefront configurato con il tema Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Autore del teaser prodotto {#author-product-teaser}

In questa esercitazione verrà esteso il componente Product Teaser. Come primo passo, aggiungeremo una nuova istanza del Product Teaser alla home page per comprendere la funzionalità di base.

1. Passate alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Inserite un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserisci teaser prodotto](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Espandete il pannello laterale (se non è già attivato) e passate al menu a discesa di ricerca risorse su **Prodotti**. Deve essere visualizzato un elenco di prodotti disponibili da un&#39;istanza di Magento connessa. Selezionate un prodotto e **trascinatelo** sul componente **Product Teaser** nella pagina.

   ![Trascinamento + Rilascia teaser prodotto](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Nota, puoi anche configurare il prodotto visualizzato configurando il componente utilizzando la finestra di dialogo (facendo clic sull’icona della *chiave inglese* ).

1. È ora possibile visualizzare un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Teaser prodotto - stile predefinito](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalizzazione del markup del Product Teaser {#customize-markup-product-teaser}

Un’estensione comune di AEM componenti consiste nel modificare la marcatura generata dal componente. A tal fine, sovrascrivere lo script [](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) HTL utilizzato dal componente per eseguire il rendering del relativo markup. HTML Template Language (HTL) è un linguaggio di modellazione leggero che AEM componenti utilizzano per eseguire il rendering dinamico della marcatura in base al contenuto creato, consentendo il riutilizzo dei componenti. Il Product Teaser, ad esempio, può essere riutilizzato più volte per visualizzare prodotti diversi.

Nel nostro caso, vogliamo eseguire il rendering di un banner sopra al teaser per indicare che il prodotto è &quot;Nuovo&quot; ed è stato aggiunto di recente al catalogo. Il pattern di progettazione per [personalizzare la marcatura](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è in realtà standard per tutti i componenti AEM, non solo per i componenti AEM CIF di base.

Utilizzate l&#39;IDE di vostra scelta per [aprire il progetto iniziale scaricato](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) all&#39;inizio dell&#39;esercitazione.

1. Spostatevi ed espandete il modulo **ui.apps** ed espandete la gerarchia delle cartelle per: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e ispezionare il `.content.xml` file.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Questa è la definizione del componente per il componente Teaser prodotto nel nostro progetto. Osservate la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questo è un esempio di creazione di un componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)Proxy. Invece di copiare e incollare tutti gli script HTL Product Teaser dai componenti core CIF AEM, possiamo utilizzare il `sling:resourceSuperType` per ereditare tutte le funzionalità.

1. Apri un nuovo browser e passa a [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) in AEM. Espandete la struttura ad albero per visualizzare il `productteaser` componente in: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite Product Teaser](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Questa è la definizione completa del componente Teaser del prodotto.

1. Tornate all&#39;IDE e al progetto Acme Store. Create un nuovo file denominato `productteaser.html` sotto di `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copiate i contenuti di `productteaser.html` CRXDE-Lite [e incollateli nel progetto Acme-Store nel](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) `productteaser.html` file appena creato.

   ![Sovrascrivi HTML di Product Teaser](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. Nel progetto Acme-Store, modificate il `productteaser.html` file e inserite un nuovo div che rappresenti un contrassegno sopra la marcatura immagine del prodotto:

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. Distribuisci il codice aggiornato nell’istanza locale di AEM utilizzando le tue competenze mentali o utilizzando [le funzioni dell’IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Nel browser, tornate alla [homepage del negozio davanti](http://localhost:4502/editor.html/content/acme/us/en.html) a AEM. Aggiorna e nell’angolo superiore destro del componente viene visualizzato un &quot;nuovo&quot; banner.

   ![Nuovo banner esteso](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   Al momento non esiste alcuna logica dietro la visualizzazione del banner. Nei prossimi esercizi lo correggeremo.

   > Nota, il CSS per il rendering del banner è stato fornito come parte del progetto iniziale e si trova in: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Per ulteriori informazioni, consulta l’esercitazione [Styling CIF Core Components (](style-cif-component.md)Attribuzione stile CIF ai componenti core).

## Personalizzazione della finestra di dialogo del teaser prodotto {#customize-dialog-product-teaser}

Successivamente, personalizzeremo la finestra di dialogo del componente Product Teaser per consentire a un autore di determinare l’intervallo di date per il quale un prodotto viene considerato &quot;nuovo&quot; e se il banner deve essere visualizzato. A tal fine, [personalizzeremo il dialogo](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) del Product Teaser nell&#39;ambito del progetto Acme Store.

1. Apri il progetto Acme Store nell’IDE di tua scelta e passa a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Sotto la `productteaser` cartella, aggiungete una nuova cartella denominata `_cq_dialog`. Aggiungete un nuovo file alla `_cq_dialog` cartella denominata `.content.xml`. È ora necessario disporre della seguente struttura di file:

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. Aggiornamento `_cq_dialog/.content.xml` con il seguente XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   Sopra abbiamo aggiunto 2 campi aggiuntivi come parte di una nuova scheda e un singolo campo nascosto.

   1. Casella di controllo per visualizzare il contrassegno &#39;Nuovo&#39;
   2. Campo Numero per definire l&#39;età massima del prodotto
   3. Campo nascosto per garantire che l&#39;età massima per il prodotto sia salvata come lungo (vedere [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) per ulteriori dettagli)

   Le finestre di dialogo definite come parte di un componente proxy ereditano tutti i campi di dialogo esistenti con una funzione nota come [Sling Resource Merger](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)(Fusione risorse Sling). Pertanto non è necessario ridefinire i campi esistenti che fanno parte del Product Teaser.

1. Aggiornate `productteaser.html` e aggiungete un `data-sly-test` segno di spunta `<div>` per il contrassegno. Questo sarà un semplice test per decidere di eseguire il rendering del contrassegno se l&#39;utente ha selezionato &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Distribuisci il codice aggiornato nell’istanza locale di AEM utilizzando le funzioni dell’IDE o le tue competenze mentali:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Tornate al componente Product Teaser e fate clic sull’icona della *chiave inglese* per aprire la finestra di dialogo. A questo punto dovrebbe essere visualizzata una scheda per **Badge** con due campi aggiuntivi. L&#39;aggiornamento di questi campi determinerà la persistenza dei valori da AEM. È consigliabile attivare/disattivare il contrassegno con la casella di controllo:

   ![Attiva/disattiva contrassegno](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Questo consente all’autore di controllare quando viene visualizzato il contrassegno. Tuttavia sarebbe ideale che il contrassegno scomparisse automaticamente una volta che il prodotto ha raggiunto una certa età in giorno in base alla voce per **Max Product Age**. Per questo, dovremo implementare una logica di back-end.

## Aggiornamento del modello Sling per il teaser prodotto {#updating-sling-model-product-teaser}

Successivamente, estenderemo la logica di business del Product Teaser implementando un modello Sling. [Modelli](https://sling.apache.org/documentation/bundles/models.html)Sling, sono &quot;POJO&quot; basati su annotazioni (Plain Old Java Objects) che implementano qualsiasi logica aziendale necessaria per il componente. I modelli Sling vengono utilizzati insieme agli script HTL come parte del componente. Seguiremo il modello di [delega per Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) in modo da poter estendere solo parti del modello esistente Product Teaser.

I modelli Sling sono implementati come Java e si trovano nel modulo **core** del progetto generato.

1. Apri il progetto Acme Store nell’IDE di tua scelta e naviga sotto il modulo **principale** per: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** è un&#39;interfaccia Java precreata che estende l&#39;interfaccia CIF **ProductTeaser** .

1. Quindi, apri il file **MyProductTeaserImpl.java** che si trova in: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` è la classe di implementazione per l&#39;interfaccia `MyProductTeaser`.

   Utilizzando il pattern di [delega per Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) è possibile fare riferimento alla `ProductTeaser` classe tramite la `sling:resourceSuperType` proprietà:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per tutti i metodi che non vogliamo ignorare o modificare, possiamo semplicemente restituire il valore che `ProductTeaser` restituisce:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. Uno dei punti di estensione extra forniti da AEM CIF Core Components è il `AbstractProductRetriever` che ci permette di accedere ad attributi di prodotto specifici. Aggiungete il seguente metodo per inizializzare il `AbstractProductRetriever` metodo nel `init()` :

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
   
       }
   ...
   ```

1. Consente di verificare queste modifiche modificando il prezzo formattato e ignorando la logica in `getFormattedPrice()`. Effettuate i seguenti aggiornamenti in modo che il prezzo venga formattato in modo esplicito in base alle impostazioni internazionali tedesche. (o scegliete un altro paese!)

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   L&#39; `productRetriever` oggetto consente di accedere all&#39; `ProductInterface` oggetto mediante il `fetchProduct()` metodo. Puoi vedere tutti i metodi [disponibili qui](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Nota* la modifica delle impostazioni internazionali in tedesco è solo un esempio divertente per visualizzare l&#39;override. In realtà, ProductTeaser utilizza le impostazioni internazionali della [pagina per determinare il formato](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. Successivamente, dovremo aggiornare il **productteaser.html** nel modulo **ui.apps** per fare riferimento al nostro nuovo modello Sling a: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   Salvare le modifiche in `productteaser.html`.

1. Distribuire la base di codice nell&#39;istanza locale di AEM. Poiché sono state apportate modifiche ai moduli **ui.apps** e **core** , create e distribuite il progetto dalla radice:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Apri un browser e passa a: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Questa console mostra tutti i modelli Sling registrati nel sistema. Controllare due volte per assicurarsi che MyTeaserModelImpl sia stato distribuito ed è mappato correttamente. Dovresti riuscire a vedere qualcosa come:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Individuare infine il punto in cui è stato creato il componente Product Teaser e visualizzare il prezzo con il formato della valuta tedesca:

   ![Formato prezzo aggiornato](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementare la logica isShowBadge {#implement-isshowbadge}

Ora che abbiamo avuto la possibilità di sperimentare con sovrascrivere i metodi del modello Sling, è possibile implementare la logica per quando visualizzare il &quot;nuovo&quot; contrassegno.

1. Tornate all&#39;IDE e aprite il file **MyProductTeaser.java** all&#39;indirizzo: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Aggiungere un nuovo metodo `isShowBadge()` all&#39;interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   Questo è un nuovo metodo che introdurremo per incapsulare la logica di mostrare o meno il contrassegno.

1. Quindi, riapri **MyProductTeaserImpl.java** all&#39;indirizzo `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. La logica per quanto tempo verrà visualizzato il contrassegno &quot;nuovo&quot; sarà basata sull&#39; `created_at` attributo del Prodotto. Per poter accedere a tale attributo, è necessario estendere la query **GraphQL** eseguita da ProductTeaser. Possiamo farlo aggiornando il `init()` metodo in **MyProductTeaserImpl.java**:

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   L&#39;aggiunta al `extendProductQueryWith` metodo è un modo efficace per garantire che gli attributi di prodotto aggiuntivi siano disponibili per il resto del modello. Consente inoltre di ridurre il numero di query eseguite.

   >[!NOTE]
   >Nel codice riportato sopra stiamo utilizzando la`addCustomSimpleField` per recuperare la `created_at` proprietà. Questo illustra come eseguire una query per tutti gli attributi personalizzati che fanno parte dello schema di Magento.
   >
   > Tuttavia, la `created_at` proprietà è stata effettivamente implementata come parte dell&#39;interfaccia [](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) prodotto e una procedura migliore sarebbe quella di riutilizzare il metodo come il seguente: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. La maggior parte degli attributi dello schema comunemente trovati è stata implementata, quindi utilizzate solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Successivamente, implementeremo il `isShowBadge()` metodo:

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   Per verificare se l’autore ha attivato la funzionalità contrassegno con la casella di controllo, nel metodo precedente viene selezionato. Successivamente, viene letto il valore della proprietà `age` impostata come parte della finestra di dialogo e rappresenta il numero massimo di giorni in cui un prodotto deve avere inizio finché il banner non scompare. Infine calcoliamo l&#39;età del prodotto in base alla `created_at` data. Se dopo aver confrontato i due valori torniamo `true` a mostrare il contrassegno, `false` in tutti gli altri casi.

1. Infine, per chiamare il `productteaser.html` `isShowBadge()` metodo, è necessario aggiungere un&#39;ulteriore aggiunta allo script. Aprite il file in `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Effettuate il seguente aggiornamento:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Distribuire la base di codice nell&#39;istanza locale di AEM. Poiché sono state apportate modifiche ai moduli **ui.apps** e **core** , create e distribuite il progetto dalla radice:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Tornate a AEM e al componente ProductTeaser e provate con numeri diversi per visualizzare l&#39;età massima del prodotto. A seconda dell&#39;età del prodotto, potrebbe essere necessario inserire alcuni numeri molto grandi per ottenere il contrassegno da visualizzare.

   ![Max Età Prodotto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Infine, eseguite una ricerca nei registri di AEM per visualizzare l&#39;istruzione di registro inserita al punto 5. In questo modo verrà stampato il valore della `created_at` proprietà proveniente dall&#39;Magento. È possibile visualizzare i registri di AEM aprendo il `error.log` file. Questo file si trova sotto il `crx-quickstart/logs/error.log` punto in cui è stato installato il AEM. È possibile visualizzare un elemento di riga come segue:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Ora potete verificare che la logica che abbiamo implementato sia corretta!

### Congratulazioni {#congratulations}

Hai appena personalizzato il primo componente AEM CIF! Scarica il pacchetto della soluzione [finita qui](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Risorse aggiuntive {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componenti di base CIF AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalizzazione AEM componenti CIF di base](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalizzazione dei componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
