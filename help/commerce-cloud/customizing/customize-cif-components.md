---
title: Personalizzare i componenti core CIF
description: Personalizzare i componenti core CIF
translation-type: ht
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: ht
source-wordcount: '2520'
ht-degree: 100%

---


# Personalizzare i componenti core CIF di AEM {#customize-cif-components}

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono un set standard di componenti Commerce che possono essere utilizzati per accelerare un progetto che integra soluzioni Adobe Experience Manager (AEM) e Magento. Questi componenti sono pronti per la produzione e possono essere [facilmente formattati con CSS](style-cif-component.md). Per molte implementazioni può essere necessario estendere questi componenti in base a specifici requisiti di business.

In questa esercitazione verranno esaminati diversi punti di estensione forniti dai componenti core CIF di AEM e da AEM in generale. A tal fine, estenderemo le capacità del componente [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) per includere la capacità di eseguire il rendering di un banner “Nuovo”. Gli autori dei contenuti potranno attivare/disattivare questo banner e determinare per quanto tempo visualizzare il banner. L’“età” del prodotto sarà basata sulla data di creazione nel catalogo Magento. Quando un prodotto ha una certa quantità di giorni, il banner “Nuovo” deve scomparire automaticamente.

![Banner Nuovo esteso](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Prerequisiti {#prerequisites}

Sono necessari i seguenti strumenti e tecnologie:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
* [SDK di AEM Cloud con componente aggiuntivo CIF](../develop.md)
* Magento compatibile con componenti core CIF

Prima di procedere con questa esercitazione, è consigliabile consultare il contenuto seguente:

* [Introduzione di Commerce Integration Framework in AEM as a Cloud Service](/help/commerce-cloud/overview.md)
* [Personalizzare lo stile dei componenti core CIF di AEM - Esercitazione](style-cif-component.md)

## Progetto iniziale

Abbiamo fornito un progetto iniziale da utilizzare con questa esercitazione. Il progetto è stato generato utilizzando la [v0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) di CIF Project Archetype. come best practice, utilizza sempre l’[ultima versione](https://github.com/adobe/aem-cif-project-archetype/releases/latest) dell’archetipo all’avvio di un nuovo progetto.

1. Scarica il progetto iniziale [**acme-store.zip**](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip) sul desktop.

1. Decomprimi **acme-store.zip** per ottenere la seguente struttura di cartelle:

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

1. Apri una nuova finestra terminale, quindi genera e implementa il progetto in un’istanza locale di AEM;

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina che sia collegata a un’istanza di Magento. Passa alla pagina `US` > `Home` in: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina: dovresti vedere diverse categorie, a indicare che la connessione a Magento funziona.

   ![Vetrina configurata con il tema Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Creare il Product Teaser {#author-product-teaser}

In questa esercitazione verrà esteso il componente Product Teaser. Come prima cosa, aggiungeremo una nuova istanza del Product Teaser alla home page per comprenderne la funzionalità di base.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**. Dovrebbe essere visualizzato un elenco di prodotti disponibili da un’istanza di Magento connessa. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di *chiave inglese*).

1. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalizzazione del markup del Product Teaser {#customize-markup-product-teaser}

I componenti AEM vengono spesso estesi per modificare il markup generato dal componente. A tal fine, sovrascrivi lo [script HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) utilizzato dal componente per eseguire il rendering del relativo markup. HTML Template Language (HTL) è un linguaggio per modelli leggero usato dai componenti di AEM per eseguire il rendering dinamico del markup in base al contenuto creato, in modo che sia possibile riutilizzare i componenti. Il Product Teaser, ad esempio, può essere riutilizzato più volte per visualizzare prodotti diversi.

Nel nostro caso, vogliamo applicare un banner sopra il teaser per indicare che il prodotto è “Nuovo” ed è stato aggiunto di recente al catalogo. Il modello di progettazione per [personalizzare il markup](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è in realtà standard per tutti i componenti di AEM, non solo per i componenti core CIF di AEM.

Utilizza l’IDE che preferisci per [aprire il progetto iniziale scaricato](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) all’inizio dell’esercitazione.

1. Passa la modulo **ui.apps** ed espandilo, quindi espandi la gerarchia delle cartelle fino a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e ispeziona il file `.content.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Questa è la definizione del componente Product Teaser usato nel nostro progetto. Osserva la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questo è un esempio di creazione di un [componente Proxy](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Invece di copiare e incollare tutti gli script HTL di Product Teaser dai componenti core CIF di AEM, possiamo utilizzare `sling:resourceSuperType` per ereditare tutte le funzionalità.

1. Apri un nuovo browser e passa a [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) in AEM. Espandi la struttura ad albero per visualizzare il componente `productteaser` in `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![Product Teaser in CRXDE Lite](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Questa è la definizione completa del componente Product Teaser.

1. Torna all’IDE e al progetto Acme Store. Crea un nuovo file denominato `productteaser.html` sotto a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copia i contenuti di `productteaser.html` da [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) e incollali nel progetto Acme-Store nel file `productteaser.html` appena creato.

   ![Sovrascrittura di HTML di Product Teaser](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. Nel progetto Acme-Store, modifica il file `productteaser.html` e inserisci un nuovo div che rappresenti un badge sopra il markup dell’immagine del prodotto:

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

1. Distribuisci il codice aggiornato nell’istanza locale di AEM mediante Maven o [le funzioni dell’IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Nel browser, torna alla [homepage della vetrina](http://localhost:4502/editor.html/content/acme/us/en.html) in AEM. Aggiorna la pagina e nell’angolo in alto a destra del componente dovresti vedere un banner “Nuovo”.

   ![Banner Nuovo esteso](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   Al momento la visualizzazione del banner non è gestita da alcuna logica. Nei prossimi esercizi provvederemo a definirla.

   > Il CSS per il rendering del banner è stato fornito come parte del progetto iniziale e si trova in `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Per ulteriori informazioni, consulta l’[esercitazione su come personalizzare lo stile dei componenti core CIF](style-cif-component.md).

## Personalizzazione della finestra di dialogo del Product Teaser {#customize-dialog-product-teaser}

Ora personalizzeremo la finestra di dialogo del componente Product Teaser in modo che un autore possa specificare l’intervallo di date per il quale un prodotto dovrà essere considerato “nuovo” e dovrà quindi essere visualizzato il banner. A tal fine, [personalizzeremo la finestra di dialogo](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) del Product Teaser nell’ambito del progetto Acme Store.

1. Apri il progetto Acme Store nell’IDE che preferisci e passa a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Nella cartella `productteaser`, aggiungi una nuova cartella denominata `_cq_dialog`. Aggiungi alla cartella `_cq_dialog` un nuovo file denominato `.content.xml`. A questo punto la struttura di file si dovrebbe presentare così:

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

1. Aggiorna `_cq_dialog/.content.xml` con il seguente XML:

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

   Qui sopra abbiamo aggiunto 2 campi come parte di una nuova scheda e un singolo campo nascosto.

   1. Casella di controllo per visualizzare il badge “Nuovo”
   2. Campo Numero per definire l’età massima del prodotto
   3. Campo nascosto per garantire che l’età massima del prodotto sia salvata come valore Long (vedi [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) per ulteriori dettagli)

   Le finestre di dialogo definite come parte di un componente proxy ereditano tutti i campi di dialogo esistenti con una funzione nota come [Sling Resource Merger](https://docs.adobe.com/content/help/it-IT/experience-manager-64/developing/platform/sling-resource-merger.html). Pertanto, non è necessario ridefinire i campi esistenti che fanno parte del Product Teaser.

1. Aggiorna `productteaser.html` e aggiungi `data-sly-test` al `<div>` del badge. Questo sarà un semplice test per decidere di eseguire il rendering del badge se l’utente ha selezionato “true”.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Distribuisci il codice aggiornato nell’istanza locale di AEM utilizzando le funzioni dell’IDE o Maven:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Torna al componente Product Teaser e fai clic sull’icona a forma di *chiave inglese* per aprire la finestra di dialogo. A questo punto dovrebbe essere visualizzata una scheda per **Badge** con due campi aggiuntivi. L’aggiornamento di questi campi determinerà la persistenza dei valori da AEM. Dovresti essere in grado di attivare/disattivare il badge con la casella di controllo:

   ![Attiva/disattiva badge](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Ciò consente all’autore di controllare quando viene visualizzato il badge. Tuttavia, sarebbe utile se il badge potesse scomparire in automatico dopo alcuni giorni, quando il prodotto non sarà più considerato “nuovo”, in base al valore specificato come **Età massima del prodotto**. A tale scopo, dovremo implementare una logica di back-end.

## Aggiornamento del modello Sling per Product Teaser{#updating-sling-model-product-teaser}

Ora estenderemo la logica di business del Product Teaser implementando un modello Sling. I [modelli Sling](https://sling.apache.org/documentation/bundles/models.html) sono “POJO” (Plain Old Java Objects) basati su annotazioni che implementano la logica di business necessaria per il componente. I modelli Sling vengono utilizzati insieme agli script HTL come parte del componente. Seguiremo il [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) in modo da estendere solo parti del modello esistente di Product Teaser.

I modelli Sling sono implementati come Java e si trovano nel modulo **core** del progetto generato.

1. Apri il progetto Acme Store nell’IDE che preferisci e passa la modulo **core** fino a `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** è un’interfaccia Java precreata che estende l’interfaccia CIF di **ProductTeaser**.

1. Apri il file **MyProductTeaserImpl.java** che si trova in `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` è la classe di implementazione per l’interfaccia `MyProductTeaser`.

   Utilizzando il [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models), è possibile fare riferimento alla `ProductTeaser` classe tramite la proprietà `sling:resourceSuperType`:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per tutti i metodi che non dovranno essere ignorati o modificati, possiamo semplicemente restituire il valore che `ProductTeaser` restituisce:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. Uno dei punti di estensione aggiuntivi forniti dai componenti core CIF di AEM è `AbstractProductRetriever`, che ci permette di accedere ad attributi di prodotto specifici. Aggiungi il seguente metodo per inizializzare `AbstractProductRetriever` nel metodo `init()`:

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

1. Per verificare queste modifiche, modifichiamo il prezzo formattato e ignoriamo la logica in `getFormattedPrice()`. Effettua i seguenti aggiornamenti in modo che il prezzo venga formattato in modo esplicito in base alle impostazioni internazionali tedesche (o di un altro Paese).

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

   L’oggetto `productRetriever` consente di accedere all’oggetto `ProductInterface` mediante il metodo `fetchProduct()`. Puoi vedere tutti i [metodi disponibili qui](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Nota: qui modifichiamo le impostazioni internazionali in tedesco unicamente a titolo di esempio, per vedere come funziona l’override. In realtà, ProductTeaser [determina il formato in base alla lingua della pagina](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. Ora dobbiamo aggiornare **productteaser.html** nel modulo **ui.apps** in modo che faccia riferimento al nostro nuovo modello Sling in: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   Salva le modifiche apportate a `productteaser.html`.

1. Implementa la base di codice nell’istanza locale di AEM. Poiché sono state apportate modifiche ai moduli **ui.apps** e **core**, crea e implementa il progetto dalla radice:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Apri un browser e passa a: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Questa console mostra tutti i modelli Sling registrati nel sistema. Verifica che MyTeaserModelImpl sia stato implementato e mappato correttamente. Dovresti vedere qualcosa questo tipo:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Infine, passa alla posizione in cui è stato creato il componente Product Teaser: ora dovresti vedere il prezzo con il formato della valuta tedesca:

   ![Formato del prezzo aggiornato](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementare la logica isShowBadge {#implement-isshowbadge}

Ora che abbiamo avuto la possibilità di sperimentare con l’override dei metodi del modello Sling, possiamo implementare la logica che determina quando visualizzare il badge “Nuovo”.

1. Torna all’IDE e apri il file **MyProductTeaser.java** in `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Aggiungi il nuovo metodo `isShowBadge()` all’interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   Questo è un nuovo metodo che introdurremo per incapsulare la logica necessaria per determinare se mostrare o meno il badge.

1. Riapri **MyProductTeaserImpl.java** in `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. La logica che stabilisce per quanto tempo verrà visualizzato il bagde “Nuovo” sarà basata sull’attributo `created_at` del prodotto. Per poter accedere a tale attributo, è necessario estendere la query **GraphQL** eseguita da ProductTeaser. Possiamo farlo aggiornando il metodo `init()` in **MyProductTeaserImpl.java**:

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

   Con l’aggiunta al metodo `extendProductQueryWith`, gli attributi di prodotto aggiuntivi saranno disponibili per il resto del modello. Inoltre si riduce la quantità di query eseguite.

   >[!NOTE]
   >Nel codice riportato sopra utilizziamo `addCustomSimpleField` per recuperare la proprietà `created_at`. Questo illustra come eseguire una query per gli attributi personalizzati che fanno parte dello schema di Magento.
   >
   > Tuttavia, la proprietà `created_at` è stata effettivamente implementata come parte dell’[interfaccia di prodotto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) e sarebbe preferibile riutilizzare il metodo come segue: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. La maggior parte degli attributi dello schema comunemente trovati è già stata implementata, quindi utilizza solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Ora, implementeremo il metodo `isShowBadge()`:

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

   In questo metodo verifichiamo innanzitutto se l’autore ha abilitato la funzionalità di badge con la casella di controllo. Successivamente, leggiamo il valore della proprietà `age` impostata come parte della finestra di dialogo e che rappresenta il numero massimo di giorni, ossia l’età di un prodotto oltre la quale il banner non dovrà più essere visualizzato. Infine, calcoliamo l’età del prodotto in base alla data `created_at`. Dopo aver confrontato i due valori si restituisce `true` per mostrare il badge, `false` in tutti gli altri casi.

1. Infine, è necessario fare un’ulteriore aggiunta allo script `productteaser.html` per chiamare il metodo `isShowBadge()`. Apri il file in `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Apporta le seguenti modifiche:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Implementa la base di codice nell’istanza locale di AEM. Poiché sono state apportate modifiche ai moduli **ui.apps** e **core**, crea e implementa il progetto dalla radice:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Torna a AEM e al componente ProductTeaser e prova con numeri diversi per visualizzare l’età massima del prodotto. A seconda dell’età del prodotto, potrebbe essere necessario inserire alcuni numeri molto grandi per far apparire il badge.

   ![Età massima del prodotto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Infine, esegui una ricerca nei registri di AEM per visualizzare l’istruzione di registro inserita al punto 5. In questo modo verrà stampato il valore della proprietà `created_at` proveniente da Magento. Per visualizzare i registri di AEM, apri il file `error.log`. Questo file si trova sotto a `crx-quickstart/logs/error.log`, dove è stato installato il file jar di AEM. Dovresti trovare una riga di questo tipo:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Ora puoi verificare che la logica implementata sia corretta.

### Congratulazioni {#congratulations}

Hai appena personalizzato il tuo primo componente CIF di AEM. Scarica il [pacchetto completo qui](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Risorse aggiuntive {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalizzazione dei componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalizzazione dei componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/customizing.html)
