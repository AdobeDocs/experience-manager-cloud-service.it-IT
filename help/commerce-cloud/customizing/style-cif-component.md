---
title: Personalizzare lo stile dei componenti core CIF di AEM
description: Personalizzare lo stile dei componenti core CIF di AEM
translation-type: ht
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: ht
source-wordcount: '2568'
ht-degree: 100%

---


# Personalizzare lo stile dei componenti core CIF di AEM {#style-aem-cif-core-components}

[CIF Project Archetype](https://github.com/adobe/aem-cif-project-archetype) crea un progetto Adobe Experience Manager (AEM) CIF minimale da usare come punto di partenza per i progetti dei clienti che utilizzano i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components). Al sito viene inizialmente applicato lo stile predefinito del marchio Venia. In questa esercitazione, analizzerai un nuovo progetto CIF di AEM generato dall’archetipo, e comprenderai come vengono organizzati e utilizzati CSS e JavaScript utilizzati dai componenti core CIF di AEM. Creerai inoltre un nuovo stile CSS con cui sostituire lo stile predefinito del componente Product Teaser.

![Cosa verrà creato](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> Verrà implementato un nuovo stile per il componente Product Teaser, che assomiglia a una scheda.

## Prerequisiti {#prerequisites}

Sono necessari i seguenti strumenti e tecnologie:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (solo AEM 6.5+)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
* Adobe Experience Manager (istanza locale)
   * [AEM 6.5](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/it-IT/experience-manager-64/release-notes/sp-release-notes.html)
* Magento con una [versione compatibile con l’archetipo](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Generare un progetto {#generate-project}

Verrà generato un nuovo progetto CIF di AEM utilizzando [CIF Project Archetype](https://github.com/adobe/aem-cif-project-archetype), quindi verranno sostituiti gli stili predefiniti.

**Puoi anche utilizzare un progetto esistente** (basato su CIF Project Archetype) e saltare questa sezione.

1. Determina la versione più recente di CIF Project Archetype visualizzandola [su GitHub](https://github.com/adobe/aem-cif-project-archetype/releases/latest). Nel passaggio successivo, sostituisci `x.y.z` con la versione più recente.

1. Esegui il seguente comando Maven per generare un nuovo progetto in [modalità batch](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html).

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

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina che sia collegata a un’istanza di Magento. Passa alla pagina `US` > `Home` in: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina: dovresti vedere diverse categorie, a indicare che la connessione a Magento funziona.

   ![Vetrina configurata con il tema Venia](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introduzione alle librerie client {#introduction-to-client-libraries}

I CSS e JavaScript responsabili del rendering del tema o degli stili della vetrina sono gestiti in AEM da una [libreria client](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/introduction/clientlibs.html), o clientlib. Le librerie client consentono di organizzare CSS e JavaScript nel codice di un progetto e quindi di distribuirli sulla pagina.

Per applicare gli stili di un particolare brand ai componenti core CIF di AEM, si devono aggiungere nuovi CSS con cui e sovrascrivere quelli gestiti da queste librerie client. È fondamentale comprendere in che modo le librerie client sono strutturate e incluse nella pagina.

### Librerie client di progetto {#project-client-libraries}

Ora esaminiamo le librerie client generate automaticamente dall’archetipo. Utilizza l’IDE che preferisci per [importare il progetto generato nell’esercizio precedente](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment).

1. Passa al modulo **ui.apps** ed espandilo, quindi espandi la gerarchia delle cartelle fino a `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![clientlibs di ui.apps](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Ci sono due cartelle secondarie: **clientlib-base** e **theme**.

1. **clientlib-base**: si tratta di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai [componenti core di AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html).

   ![clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   Di seguito è riportata la definizione XML di **clientlib-base** (il file `.content.xml`):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` è la categoria per questa libreria client. Considera una categoria come un tag. Questa verrà utilizzata per includere o incorporare la libreria nella pagina.

   Osserva la proprietà `embed` e l’array di altre categorie clientlib. Ciascuna di queste categorie rappresenta una libreria client. Ad esempio, `core.wcm.components.accordion.v1` include il codice JavaScript necessario per il funzionamento del [componente per pannello a soffietto](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/components/accordion.html).

   Utilizzando le proprietà `embed` e `categories` puoi gestire e includere le librerie client di diversi progetti.

   `allowProxy=true` assicura che le librerie client CSS e JavaScript vengano distribuite da un percorso con prefisso `/etc.clientlibs`. In questo modo il codice dell’applicazione in `/apps` rimane protetto dagli utenti finali, ma i CSS e JavaScript necessari per il funzionamento del sito Web possono essere serviti in modo anonimo. Ulteriori dettagli sulla [proprietà allowProxy sono disponibili qui](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **theme**: questa è la libreria client che contiene il tema e gli stili CSS iniziali per il progetto CIF. Questa libreria client è progettata per essere personalizzata da ogni implementazione. È utile iniziare con alcuni stili esistenti in modo che i componenti siano già funzionali.

   ![Libreria client theme](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   Di seguito è riportata la definizione XML di **theme**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` è la categoria per questa libreria client, ed è così che la libreria client verrà inclusa nella pagina.

1. Sotto alla libreria client **theme** dovresti trovare un file denominato **css.txt** che si trova in `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   Il file **css.txt** (e **js.txt**) agisce come manifesto e determina l’ordine in cui i singoli file vengono inclusi nel file CSS finale. L’ordine è importante sia per CSS che per JavaScript ed è utile creare più file per gestire meglio il codice. Osservando il file **css.txt**, puoi vedere che i file sono organizzati in base ai componenti a cui sono applicati gli stili.

1.  Ispeziona i file CSS sotto **theme/components** per avere un’idea degli stili dei componenti inclusi. Alcuni di questi file verranno aggiornati più avanti nell’esercitazione.

### Inclusione della libreria client con il componente Pagina base

Nella sezione che segue verranno analizzate le modalità di inclusione delle librerie client in una pagina utilizzando [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/introduction/clientlibs.html#using-htl) e il componente Pagina.

1. Nel modulo **ui.apps**, passa alla definizione del componente `page` in `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Questo componente **page**, generato dall’archetipo, è il punto di ingresso utilizzato per il rendering di tutte le pagine del progetto.

1. Se analizzi la definizione del componente **page** (`page/.content.xml`), noterai una proprietà `sling:resourceSuperType` che punta a `core/cif/components/structure/page/v1/page`. Questo significa che il componente **page** del nostro progetto (Acme) erediterà tutte le funzionalità del componente [core Pagina core di CIF](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) e ci consentirà di gestire meno codice.

1. Sotto il componente **page** si trovano due file: **customheaderlibs.html** e **customfooterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** è uno script HTL di cui sarà effettuato il rendering nella parte superiore della pagina. È uno script comune per ignorare e aggiungere logica specifica per il progetto. In questo caso lo usiamo per includere la libreria client con una categoria `acme.wcm.base`. Seguendo le best practice di sviluppo Web, includiamo solo il CSS nella parte superiore della pagina.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** è uno script HTL di cui sarà effettuato il rendering nella parte inferiore della pagina, subito prima del tag di chiusura `</body>`. Anche in questo caso viene utilizzata la categoria `acme.wcm.base`, ma questa volta verrà caricato solo il JavaScript della libreria client.

La modifica degli script HTL del componente **page** determina come `acme.wcm.base` viene incluso in tutte le pagine. E per quanto riguarda `acme.theme`? Nel prossimo esercizio esamineremo un’altra opzione per l’inclusione delle librerie client.

### Inclusione della libreria client con i modelli di pagina {#client-library-inclusion-pagetemplates}

Sono disponibili diverse opzioni per includere una libreria lato client. Ora esamineremo come il progetto generato include le librerie lato client del tema tramite [Modelli di pagina](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/platform/templates/page-templates-editable.html).

Apri un nuovo browser e accedi all’istanza AEM in cui è stato implementato il progetto all’inizio di questa esercitazione.

1. Dalla schermata iniziale di AEM, passa a **Strumenti** > **Generale** > **Modelli**.

   ![Passare ai modelli](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Passa alla cartella **Configurazione archivio Acme**. Apri il **modello per pagina categorie** selezionando l’icona a forma di *matita*.

   ![Scheda del modello per pagina categorie](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. Nell’angolo in alto a sinistra, seleziona l’icona **Informazioni pagina** e fai clic su **Criterio pagina**.

   ![Voce di menu Criterio pagina](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. Si aprirà il Criterio pagina per il modello Pagina di catalogo:

   ![Criterio pagina - pagina di catalogo](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   Sul lato destro è disponibile un elenco delle **categorie** di librerie client che verranno incluse in tutte le pagine che utilizzano questo modello.

   * **wcm.foundation.components.page.responsive** - Fornisce il CSS necessario per abilitare i controlli di [layout reattivo](https://docs.adobe.com/content/help/it-IT/experience-manager-65/authoring/siteandpage/responsive-layout.html) da parte degli autori.
   * **acme.theme** - Questo è il tema di partenza generato automaticamente dall’archetipo. Per impostazione predefinita, questo stile è simile al negozio demo di esempio Venia. Tuttavia, come puoi vedere dal nome, è destinato a essere personalizzato dall’implementazione del progetto. *Questo è ciò che modificheremo nella prossima sezione.*
   * **core.cif.components.react** - Si tratta di una libreria client compilata con diversi componenti React utilizzati per funzioni dinamiche come il carrello acquisti. Ulteriori [informazioni sono disponibili qui](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Altri modelli utilizzano lo stesso criterio: **Pagina di contenuto**, **Pagina di destinazione** e così via. Riutilizzando lo stesso criterio, possiamo essere certi che le stesse librerie client verranno incluse in tutte le pagine.

   Quando si gestisce l’inclusione delle librerie client mediante l’uso di modelli e criteri di pagina, si può modificare il criterio a livello di modello. Ad esempio, supponiamo di dover gestire due marchi diversi nella stessa istanza di AEM. Ogni marchio avrà un proprio stile o un proprio *tema*, ma le librerie e il codice di base saranno gli stessi. Un altro esempio, nel caso di una libreria client più grande che si voglia visualizzare solo su determinate pagine, si può creare un criterio di pagina univoco solo per quel modello. L’altro vantaggio

### Verificare le librerie client sulla pagina {#verify-client-libraries}

A questo punto abbiamo esaminato come includere le librerie client utilizzando HTL con gli script **custom headerlibs.html** e **customfooterlibs.html** e come utilizzare i criteri di pagina di un modello per includere librerie client aggiuntive. Ora verificheremo l’inclusione delle librerie client sul sito.

1. Dalla schermata iniziale di AEM, passa a **Sites** > **Acme Store** > **Stati Uniti** > **Inglese** e apri la pagina per la modifica: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Seleziona il menu **Informazioni pagina** e fai clic su **Visualizza come pubblicato**:

   ![Visualizza come pubblicato](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   La pagina viene aperta senza caricare alcun JavaScript di authoring di AEM, come apparirebbe sul sito pubblicato. All’URL è stato aggiunto il parametro di query `?wcmmode=disabled`. Quando si sviluppano CSS e JavaScript, è buona norma utilizzare questo parametro per semplificare la pagina, rimuovendo elementi dell’istanza di authoring di AEM.

1. Visualizza il codice sorgente della pagina e individua le seguenti librerie client incluse: **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.theme**, **core.cif.components.react**

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

## Personalizzare lo stile del Product Teaser {#style-product-teaser}

Ora che comprendiamo la struttura delle librerie client generata dall’archetipo, possiamo iniziare a personalizzare i componenti core CIF di AEM. Modificheremo gli stili del componente Product Teaser per dargli l’aspetto di una “scheda”.

### Creare il Product Teaser {#author-product-teaser}

Come prima cosa, aggiungeremo una nuova istanza del componente Product Teaser nella home page del sito, utilizzando gli strumenti di authoring di AEM.

1. Apri una nuova scheda del browser e passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**. Dovrebbe essere visualizzato un elenco di prodotti disponibili da un’istanza di Magento connessa. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di *chiave inglese*).

1. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Aggiornare il CSS per il Product Teaser {#update-css-product-teaser}

Ora modificheremo il CSS nella libreria client **theme** per applicare al Product Teaser uno stile di tipo scheda.

Torna all’IDE e al progetto generato.

1. Nel modulo **ui.apps**, passa alla cartella `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. Qui sono definiti tutti gli stili per il Product Teaser.

1. Apri il file **teaser.css** e aggiorna le regole CSS corrispondenti (oppure scarica il [file teaser.css della soluzione](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) e sostituiscilo).

   Aggiungi un’ombra esterna e includi angoli arrotondati al Product Teaser.

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

   Modifica il bordo dell’immagine nel Product Teaser.

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

   Aggiorna il nome del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

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

   Aggiorna il prezzo del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

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

   Aggiorna la query “media” nella parte inferiore in modo che, su schermi più piccoli di 992 px, il nome e il prezzo vengano sovrapposti.

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

   Salva le modifiche in **teaser.css**. Puoi scaricare il [file teaser.css della soluzione qui](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Implementa in AEM gli aggiornamenti del modulo **ui.apps** mediante Maven, da un terminale di riga di comando:

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
   >Sono disponibili [strumenti e configurazione IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) aggiuntivi per sincronizzare i file di progetto direttamente con un’istanza AEM locale senza dover eseguire una generazione Maven completa.

### Visualizzare il Product Teaser aggiornato {#view-updated-product-teaser}

Una volta implementato in AEM il codice per il progetto, dovrebbe essere possibile vedere le modifiche apportate al Product Teaser.

1. Torna nel browser e aggiorna la home page: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). Dovresti vedere gli stili del product teaser aggiornati.

   ![Stile del Product Teaser aggiornato](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Prova ad aggiungere altri Product Teaser. Utilizza la modalità Layout per modificare la larghezza e l’offset dei componenti in modo da visualizzare più teaser su una riga.

   ![Product Teaser multipli](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Ciascun teaser di prodotto contiene lo stesso stile.

### Risoluzione dei problemi {#troubleshooting}

In [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) puoi verificare che il file CSS aggiornato sia stato distribuito: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

Quando si distribuiscono nuovi file CSS e/o JavaScript, è importante anche assicurarsi che il browser non distribuisca file non aggiornati. A tale scopo, cancella la cache del browser o avvia una nuova sessione del browser.

AEM inoltre tenta di memorizzare nella cache le librerie client per migliorare le prestazioni. A volte, dopo la distribuzione del codice, vengono distribuiti i file meno recenti. Puoi annullare manualmente la validità della cache della libreria client di AEM utilizzando lo strumento [Rigenera librerie client](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Se si sospetta che AEM abbia memorizzato nella cache una versione precedente di una libreria client, è meglio annullare la validità della cache. La rigenerazione delle librerie è infatti inefficiente e richiede molto tempo.*

### Congratulazioni {#congratulations}

Hai appena personalizzato il primo componente core CIF di AEM.

### Sfida bonus {#bonus-challenge}

Usa il [Sistema di stili di AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/components/style-system.html) per creare due stili che possono essere attivati/disattivati da un autore di contenuti. La sezione su come [sviluppare con il sistema di stili](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) include passaggi dettagliati e informazioni su come eseguire questa operazione.

![Sfida bonus - Sistema di stili](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)

* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)

* [Configurare un ambiente di sviluppo AEM locale](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Librerie lato client](https://docs.adobe.com/content/help/it-IT/experience-manager-65/developing/introduction/clientlibs.html)
* [Guida introduttiva di AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Sviluppo con il sistema di stili](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
