---
title: Stile AEM componenti CIF di base
description: Stile AEM componenti CIF di base
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---


# Stile AEM componenti CIF di base {#style-aem-cif-core-components}

L&#39;archetipo [](https://github.com/adobe/aem-cif-project-archetype) CIF del progetto [crea un progetto CIF (AEM) di Adobe Experience Manager minimo come punto di partenza per i progetti dei clienti che utilizzano](https://github.com/adobe/aem-core-cif-components)AEM componentidi base CIF. Uno stile predefinito, noto come marchio Venia, viene applicato inizialmente al sito. In questa esercitazione verrà analizzato un nuovo progetto AEM CIF, generato dall&#39;archetype, e verrà illustrato in che modo i componenti CSS e JavaScript utilizzati dai componenti AEM CIF Core sono organizzati. Verrà inoltre creato un nuovo stile utilizzando CSS per sostituire lo stile predefinito del componente Product Teaser.

![Elementi da creare](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> Verrà implementato un nuovo stile per il componente Product Teaser che assomiglia a una scheda.

## Prerequisiti {#prerequisites}

Sono necessari i seguenti strumenti e tecnologie:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (solo AEM 6.5+)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
* Adobe Experience Manager  (istanza locale)
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* Magento che esegue una [versione compatibile con archetype](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Generazione di un progetto {#generate-project}

Genereremo un nuovo progetto AEM CIF utilizzando l&#39;archetipo [](https://github.com/adobe/aem-cif-project-archetype) CIF del progetto e quindi ignoreremo gli stili predefiniti.

**Sentitevi liberi di utilizzare un progetto** esistente (basato sul tipo di archivio del progetto CIF) e saltate questa sezione.

1. Determinate la versione più recente di CIF Project Archetype visualizzando [la versione più recente su GitHub](https://github.com/adobe/aem-cif-project-archetype/releases/latest). Nel passaggio successivo sostituisci `x.y.z` con la versione dell’ultima versione.

1. Eseguite il seguente comando Maven per generare un nuovo progetto in modalità [](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)batch.

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. Create e distribuite il progetto in un’istanza locale di AEM:

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Aggiungete le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungere le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di uno storefront che sia collegata a un&#39;istanza di Magento. Passa alla pagina `US` > `Home` in: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Dovresti vedere che il negozio al momento sta usando il tema Venia. Se si espande il menu principale dello storefront, dovrebbero essere visualizzate diverse categorie, a indicare che il Magento di connessione funziona.

   ![Storefront configurato con il tema Venia](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introduzione alle librerie client {#introduction-to-client-libraries}

I CSS e JavaScript responsabili per il rendering del tema/stili dello storefront sono gestiti in AEM da una libreria [o clientlibs](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) Client per farla breve. Le librerie client forniscono un meccanismo per organizzare CSS e Javascript nel codice di un progetto e quindi distribuirli sulla pagina.

Il modo in cui possiamo applicare stili specifici per il marchio AEM componenti CIF di base è aggiungendo e ignorando i CSS gestiti da queste librerie client. È fondamentale comprendere in che modo le librerie client sono strutturate e incluse nella pagina.

### Librerie client di progetto {#project-client-libraries}

In seguito verranno analizzate le librerie client generate automaticamente da archetype. Utilizzate l&#39;IDE di vostra scelta per [importare il progetto generato nell&#39;esercizio](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)precedente.

1. Spostatevi ed espandete il modulo **ui.apps** ed espandete la gerarchia delle cartelle per: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Ci sono due cartelle sotto, **clientlib-base** e **tema**.

1. **clientlib-base** - Si tratta di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai [AEM Componenti](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html)principali.

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   Di seguito è riportata la definizione XML di **clientlib-base** (il `.content.xml` file):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` è la categoria per questa libreria client. Considerate una categoria come un tag. Questo verrà utilizzato per includere o incorporare la libreria nella pagina.

   Osservare la `embed` proprietà e la matrice di altre categorie clientlib. Ciascuna di queste categorie rappresenta una libreria client. Ad esempio, `core.wcm.components.accordion.v1` include il codice JavaScript necessario per il funzionamento del componente [Accordion](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) .

   Utilizzando le proprietà `embed` e `categories` è possibile gestire e includere le librerie client di diversi progetti.

   `allowProxy=true` assicura che la libreria client CSS e JavaScript vengano serviti da un percorso con il prefisso: `/etc.clientlibs`. In questo modo il codice dell&#39;applicazione in `/apps` questione rimane protetto dagli utenti finali, ma i CSS e JavaScript necessari per il funzionamento del sito Web possono essere serviti in modo anonimo. Ulteriori dettagli sulla proprietà [allowProxy sono disponibili qui](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **tema** - È la libreria client che contiene il tema iniziale e CSS per il progetto CIF. Questa libreria client è progettata per essere personalizzata da ogni implementazione ed è utile iniziare con alcuni stili esistenti in modo che i componenti siano funzionali per iniziare.

   ![clientlibrary di temi](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   Di seguito è riportata la definizione XML del **tema**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` è la categoria per questa libreria client ed è così che la libreria client verrà inclusa nella pagina.

1. Sotto la libreria client **tema** dovrebbe essere visualizzato un file denominato **css.txt** che si trova in: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   Il file **css.txt** (e **js.txt**) agiscono come manifesti che stabiliscono l&#39;ordine in cui i singoli file vengono inclusi nel file CSS finale. L&#39;ordine è importante sia per CSS che per JavaScript ed è utile creare più file per gestire meglio il codice. Osservando il file **css.txt** potete vedere che i file sono organizzati in base ai componenti a cui sono applicati gli stili.

1.  i file CSS sotto il **tema o i componenti** per avere un&#39;idea degli stili dei componenti ootb. Alcuni di questi file verranno aggiornati più avanti nell&#39;esercitazione.

### Integrazione della libreria client con il componente Pagina base

Nella sezione che segue verranno analizzate le modalità di inclusione delle librerie client in una pagina utilizzando [HTL](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) e il componente Pagina.

1. Nel modulo **ui.apps** , andate alla definizione del `page` componente in: `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Questo componente **pagina** , generato dall’archetipo, è il punto di ingresso utilizzato per eseguire il rendering di tutte le pagine del progetto.

1. Se si analizza la definizione del componente **pagina** (`page/.content.xml`), si noterà una proprietà `sling:resourceSuperType` che punta a `core/cif/components/structure/page/v1/page`. Questo significa che il componente **pagina** Acme del nostro progetto erediterà tutte le funzionalità del componente Pagina [principale](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) CIF e ci consentirà di gestire meno codice.

1. Sotto il componente **pagina** si trovano due file: **customheaderlibs.html** e **customfooterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** è uno script HTL che verrà rappresentato nella parte superiore della pagina. È uno script comune per ignorare e aggiungere logica specifica per il progetto. In questo caso lo stiamo utilizzando per includere la libreria client con una categoria di `acme.wcm.base`. Seguendo le procedure ottimali per lo sviluppo Web, includiamo solo il CSS nella parte superiore della pagina.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** è uno script HTL che verrà visualizzato nella parte inferiore della pagina, subito prima del `</body>` tag di chiusura. Anche in questo caso la categoria di `acme.wcm.base` viene utilizzata, ma questa volta verrà caricato solo il JavaScript della libreria client.

La modifica degli script HTL del componente **pagina** determina come `acme.wcm.base` viene incluso in tutte le pagine. Ma che dire `acme.theme`? Nel prossimo esercizio esamineremo un&#39;altra opzione per l&#39;inclusione delle librerie client.

### Integrazione della libreria client con i modelli di pagina {#client-library-inclusion-pagetemplates}

Sono disponibili diverse opzioni per l&#39;inclusione di una libreria lato client. In seguito, controlleremo come il progetto generato include le librerie lato client del tema tramite Modelli [](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html)pagina.

Aprite un nuovo browser e accedete all&#39;istanza AEM in cui avete distribuito il progetto all&#39;inizio di questa esercitazione.

1. Dalla schermata iniziale AEM passare a **Strumenti** > **Generale** > **Modelli**.

   ![Navigazione modelli](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Andate nella cartella Configurazione **archivio** Acme. Aprite il Modello **pagina** categoria selezionando l&#39;icona *matita* .

   ![scheda modello pagina di categoria](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. Nell’angolo in alto a sinistra, selezionate l’icona Informazioni **** pagina e fate clic su Criterio **** pagina.

   ![Voce di menu del criterio della pagina](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. Viene aperto il Criterio pagina per il modello Pagina catalogo:

   ![Criteri pagina - pagina catalogo](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   Sul lato destro è disponibile un elenco delle **categorie** di librerie client che verranno incluse in tutte le pagine che utilizzano questo modello.

   * **wcm.foundation.components.page.responsive** - Fornisce il CSS necessario per abilitare i controlli di layout [](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) reattivi da parte degli autori.
   * **acme.tema** - Questo è il tema di partenza che archetype genera automaticamente. Per impostazione predefinita, questo stile è simile al negozio demo di esempio Venia. Tuttavia, come potete vedere dal nome, è destinato a essere personalizzato dall&#39;implementazione del progetto. *Questo è ciò che modificheremo nella prossima sezione!*
   * **core.cif.components.response** - Si tratta di una libreria client compilata con diversi componenti React utilizzati per funzioni dinamiche come il carrello acquisti. Ulteriori [informazioni sono disponibili qui](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Tenere presente che altri modelli utilizzano lo stesso criterio, **Pagina** contenuto, Pagina **di** destinazione e così via. Riutilizzando lo stesso criterio, possiamo garantire che le stesse librerie client siano incluse in tutte le pagine.

   Il vantaggio di utilizzare Modelli e criteri pagina per gestire l&#39;inclusione delle librerie client è che potete modificare il criterio per modello. Ad esempio, potete gestire due marchi diversi all&#39;interno della stessa istanza AEM. Ogni marchio avrà un proprio stile o un proprio *tema* , ma le librerie e il codice di base saranno gli stessi. Un altro esempio, se aveste una libreria client più grande che desiderate visualizzare solo su determinate pagine, potreste creare un criterio di pagina univoco solo per quel modello. L&#39;altro vantaggio

### Verificare le librerie client sulla pagina {#verify-client-libraries}

A questo punto abbiamo esaminato come includere le librerie client utilizzando HTL con gli script **custom headerlibs.html** e **customfooterlibs.html** e come utilizzare i criteri di pagina di un modello per includere librerie client aggiuntive. Quindi verificheremo l&#39;inclusione delle librerie client sul sito.

1. Dalla schermata iniziale AEM passare a **Siti** > **Acme Store** > Stati **Uniti >** Inglese **** e aprire la pagina per la modifica: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Selezionate il menu Informazioni **** pagina e fate clic su **Visualizza come pubblicato**:

   ![Visualizza come pubblicato](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   Viene aperta la pagina senza che sia stato caricato alcun javascript dell’autore AEM, come apparirebbe sul sito pubblicato. Tenere presente che all&#39;URL è `?wcmmode=disabled` stato aggiunto il parametro di query. Quando si sviluppano CSS e JavaScript, è buona norma utilizzare questo parametro per semplificare la pagina con informazioni AEM autore.

1. Visualizzare l’origine della pagina e identificare le seguenti librerie client incluse: **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.tema**, **core.cif.components.response**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## Stile del teaser prodotto {#style-product-teaser}

Ora che comprendiamo la struttura della libreria client generata dall&#39;archetipo, possiamo iniziare a personalizzare i componenti core CIF AEM. Verranno modificati gli stili del componente Product Teaser in modo che sembri più una &quot;scheda&quot;.

### Autore del teaser prodotto {#author-product-teaser}

Come primo passo, aggiungeremo una nuova istanza del componente Product Teaser nella home page del sito utilizzando gli strumenti di authoring AEM.

1. Aprite una nuova scheda del browser e passate alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Inserite un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserisci teaser prodotto](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Espandete il pannello laterale (se non è già attivato) e passate al menu a discesa di ricerca risorse su **Prodotti**. Deve essere visualizzato un elenco di prodotti disponibili da un&#39;istanza di Magento connessa. Selezionate un prodotto e **trascinatelo** sul componente **Product Teaser** nella pagina.

   ![Trascinamento + Rilascia teaser prodotto](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Nota, puoi anche configurare il prodotto visualizzato configurando il componente utilizzando la finestra di dialogo (facendo clic sull’icona della *chiave inglese* ).

1. È ora possibile visualizzare un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Teaser prodotto - stile predefinito](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Aggiornare il CSS per il teaser prodotto {#update-css-product-teaser}

Quindi, modificheremo il CSS nella libreria client **tema** per implementare uno stile tipo scheda per il Product Teaser.

Torna all’IDE e al progetto generato.

1. Nel modulo **ui.apps** andate alla cartella: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. Qui sono definiti tutti gli stili per il Product Teaser.

1. Aprite il file **teaser.css** e aggiornate le regole CSS corrispondenti (oppure scaricate il file [teaser.css della](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) soluzione e sostituite).

   Aggiungete un’ombra esterna e includete angoli arrotondati al teaser prodotto.

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   Modificate il bordo dell’immagine nel teaser prodotto.

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
    }
   ```

   Aggiornate il nome del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modificate il colore del testo.

   ```css
   .productteaser .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

   Aggiornate il prezzo del prodotto in modo che venga visualizzato anche nella parte inferiore del teaser e modificate il colore del testo.

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   Aggiornate la query multimediale nella parte inferiore, in modo da memorizzare il nome e il prezzo nelle schermate più piccole di 992 px.

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   Salvate le modifiche in **teaser.css**. È possibile scaricare il file teaser.css della [soluzione qui](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Distribuisci gli aggiornamenti del modulo **ui.apps** per AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >Sono disponibili strumenti [e configurazione](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) IDE aggiuntivi per sincronizzare i file di progetto direttamente a un&#39;istanza AEM locale senza dover eseguire una build Maven completa.

### Visualizza teaser prodotto aggiornato {#view-updated-product-teaser}

Dopo che il codice per il progetto è stato distribuito a AEM, ora dovremmo essere in grado di vedere le modifiche al Product Teaser.

1. Tornate nel browser e aggiornate nuovamente la home page: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). Vengono visualizzati gli stili teaser di prodotto aggiornati.

   ![Stile teaser prodotto aggiornato](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Provate aggiungendo altri teaser di prodotto. Utilizzare la modalità Layout per modificare la larghezza e l’offset dei componenti al fine di visualizzare più teaser in una riga.

   ![Teaser di prodotti multipli](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Ciascun teaser di prodotto contiene lo stesso stile.

### Risoluzione dei problemi {#troubleshooting}

In [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) potete verificare che il file CSS aggiornato sia stato distribuito: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

Quando si distribuiscono nuovi file CSS e/o JavaScript, è importante anche assicurarsi che il browser non distribuisca file non aggiornati. Potete eliminare questo problema cancellando la cache del browser o avviando una nuova sessione del browser.

AEM inoltre tenta di memorizzare nella cache le librerie client per migliorare le prestazioni. A volte, dopo la distribuzione del codice, i file meno recenti vengono serviti. È possibile annullare manualmente AEM cache della libreria client utilizzando lo strumento [Ricrea librerie client](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Annulla validità cache è il metodo preferito se si sospetta che AEM abbia memorizzato nella cache una versione precedente di una libreria client. La ricostruzione delle librerie è inefficiente e richiede molto tempo.*

### Congratulazioni {#congratulations}

Hai appena disegnato il tuo primo componente AEM CIF Core Component!

### Sfida Bonus {#bonus-challenge}

Usate il sistema [Stile](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) AEM per creare due stili che possono essere attivati/disattivati dall’autore di un contenuto. [Lo sviluppo con Style System](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) include passaggi dettagliati e informazioni su come eseguire questa operazione.

![Sfida bonus - sistema stile](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)

* [Componenti di base CIF AEM](https://github.com/adobe/aem-core-cif-components)

* [Configurare un ambiente di sviluppo AEM locale](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Librerie lato client](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [Guida introduttiva ai AEM Sites](https://docs.adobe.com/content/help/it-IT/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Sviluppo con il sistema di stile](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
