---
title: Personalizzare lo stile dei componenti core CIF di AEM
description: Scopri come assegnare uno stile AEM componenti core CIF. L’esercitazione illustra come le librerie lato client o le librerie client vengono utilizzate per distribuire e gestire CSS e JavaScript per un’implementazione Commerce di Adobe Experience Manager (AEM). Questa esercitazione riguarderà anche il modo in cui il modulo ui.frontend e un progetto webpack sono integrati nel processo di compilazione end-to-end.
sub-product: Commerce
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 521c1bb8-7326-4ee8-aba3-f386727e2b34,75df606f-b22f-4f7e-bd8a-576d215f72bc
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 29%

---

# Personalizzare lo stile dei componenti core CIF di AEM {#style-aem-cif-core-components}

La [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) è una base di codice di riferimento per l&#39;utilizzo di [Componenti core CIF](https://github.com/adobe/aem-core-cif-components). In questa esercitazione esaminerai il progetto di riferimento Venia e comprenderai come sono organizzati i CSS e JavaScript utilizzati dai componenti core CIF di AEM. Verrà inoltre creato un nuovo stile utilizzando CSS per aggiornare lo stile predefinito del **Product Teaser** componente.

>[!TIP]
>
> Utilizza la [Archetipo AEM progetto](https://github.com/adobe/aem-project-archetype) all’avvio dell’implementazione Commerce personalizzata.

## Cosa Verrà Generato

In questa esercitazione verrà implementato un nuovo stile per il componente Product Teaser che assomiglia a una scheda. Le lezioni apprese nell’esercitazione possono essere applicate ad altri componenti core CIF.

![Cosa verrà creato](../assets/style-cif-component/what-you-will-build.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Questo include un&#39;istanza in esecuzione di AEM configurata e connessa a un&#39;istanza Adobe Commerce. Rivedi i requisiti e le fasi per [configurazione di uno sviluppo locale con AEM SDK as a Cloud Service](../develop.md).

## Clona il progetto Venia {#clone-venia-project}

Cloneremo il [Progetto Venia](https://github.com/adobe/aem-cif-guides-venia) quindi sovrascrivi gli stili predefiniti.

>[!NOTE]
>
> **Sentitevi liberi di utilizzare un progetto esistente** (in base al AEM Project Archetype con CIF incluso) e salta questa sezione.

1. Esegui il seguente comando git per clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza Adobe Commerce o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina connessa a un&#39;istanza di Adobe Commerce. Passa a `US` > `Home` pagina in: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina, dovresti vedere diverse categorie, a indicare che la connessione ad Adobe Commerce funziona.

   ![Storefront configurato con il tema Venia](../assets/style-cif-component/venia-store-configured.png)

## Librerie client e modulo ui.frontend {#introduction-to-client-libraries}

I CSS e JavaScript responsabili del rendering del tema o degli stili della vetrina sono gestiti in AEM da una [libreria client](/help/implementing/developing/introduction/clientlibs.md), o clientlib. Le librerie client consentono di organizzare CSS e JavaScript nel codice di un progetto e quindi di distribuirli sulla pagina.

Gli stili specifici per il marchio possono essere applicati AEM componenti core CIF aggiungendo ed ignorando i CSS gestiti da queste librerie client. È fondamentale comprendere in che modo le librerie client sono strutturate e incluse nella pagina.

La [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) è dedicato [webpack](https://webpack.js.org/) per gestire tutte le risorse front-end di un progetto. Questo consente agli sviluppatori front-end di utilizzare un numero qualsiasi di lingue e tecnologie, come [TypeScript](https://www.typescriptlang.org/), [Squalo](https://sass-lang.com/) e molto altro.

La `ui.frontend` Il modulo è anche un modulo Maven e integrato con il progetto più ampio attraverso l&#39;uso di un modulo NPM il [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). Durante una build, il `aem-clientlib-generator` copia i file CSS e JavaScript compilati in una libreria client nel `ui.apps` modulo .

![architettura ui.frontend a ui.apps](../assets/style-cif-component/ui-frontend-architecture.png)

*I CSS e JavaScript compilati vengono copiati dal `ui.frontend` nel modulo `ui.apps` modulo come libreria client durante una build Maven*

## Aggiornare lo stile del teaser {#ui-frontend-module}

Quindi, apporta una piccola modifica allo stile Teaser per vedere come `ui.frontend` funzionano le librerie client e dei moduli. Utilizzo [l&#39;IDE che preferisci](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) importare il progetto Venia. Le schermate utilizzate sono [IDE codice di Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. Naviga ed espandi **ui.frontend** modulo ed espandi la gerarchia delle cartelle per: `ui.frontend/src/main/styles/commerce`:

   ![cartella di e-commerce ui.frontend](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   Tieni presente che sono presenti più istanze (`.scss`) sotto la cartella. Si tratta degli stili specifici Commerce per ciascuno dei componenti Commerce .

1. Aprire il file `_productteaser.scss`.

1. Aggiorna `.item__image` regola e modifica la regola del bordo:

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
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

   La regola di cui sopra deve aggiungere un bordo rosa molto grassetto al componente Product Teaser.

1. Apri una nuova finestra terminale e passa alla `ui.frontend` cartella:

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. Esegui il seguente comando Maven:

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect l&#39;uscita terminale. Il comando Maven esegue diversi script NPM, tra cui `npm run build`. La `npm run build` è definito nel `package.json` e ha l&#39;effetto di compilare il progetto webpack e attivare la generazione della libreria client.

1. Inspect il file `ui.frontend/dist/clientlib-site/site.css`:

   ![CSS del sito compilato](../assets/style-cif-component/comiled-site-css.png)

   Il file è la versione compilata e minimizzata di tutti i file Sass nel progetto.

   >[!NOTE]
   >
   > File come questo vengono ignorati dal controllo del codice sorgente poiché dovrebbero essere generati durante il tempo di creazione.

1. Inspect il file `ui.frontend/clientlib.config.js`.

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   Questo è il file di configurazione per [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) e determina dove e come i CSS e JavaScript compilati verranno trasformati in una libreria client AEM.

1. In `ui.apps` il modulo esamina il file: `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![CSS del sito compilato in ui.apps](../assets/style-cif-component/comiled-css-ui-apps.png)

   Questo viene copiato `site.css` in `ui.apps` progetto. Ora fa parte di una libreria client denominata `clientlib-site` con una categoria di `venia.site`. Una volta che il file fa parte del `ui.apps` modulo che può essere distribuito a AEM.

   >[!NOTE]
   >
   > File come questo vengono anche ignorati dal controllo del codice sorgente, in quanto dovrebbero essere generati durante il tempo di creazione.

1. Ispeziona quindi le altre librerie client generate dal progetto:

   ![Altre librerie client](../assets/style-cif-component/other-clientlibs.png)

   Queste librerie client non sono gestite dalla `ui.frontend` modulo . Queste librerie client includono invece dipendenze CSS e JavaScript fornite da Adobe. La definizione di queste librerie client è `.content.xml` sotto ogni cartella.

   **clientlib-base**: si tratta di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai [componenti core di AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it). La categoria è `venia.base`.

   **clientlib-cif** - Questa è anche una libreria client vuota che incorpora semplicemente le dipendenze necessarie da [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components). La categoria è `venia.cif`.

   **clientlib-grid** - Questo include il CSS necessario per abilitare AEM funzione Griglia reattiva. L&#39;utilizzo della griglia AEM abilita [Modalità Layout](/help/sites-cloud/authoring/features/responsive-layout.md) nell’editor di AEM e consente agli autori di contenuti di ridimensionare i componenti. La categoria è `venia.grid` e è incorporato nel `venia.base` libreria.

1. Inspect i file `customheaderlibs.html` e `customfooterlibs.html` sotto `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![Script personalizzati di intestazione e piè di pagina](../assets/style-cif-component/custom-header-footer-script.png)

   Questi script includono: **venia.base** e **venia.cif** come parte di tutte le pagine.

   >[!NOTE]
   >
   > Solo le librerie di base sono &quot;hard-coded&quot; come parte degli script di pagina. `venia.site` non è incluso in questi file, ma è incluso come parte del modello di pagina per una maggiore flessibilità. Questo verrà esaminato successivamente.

1. Dal terminale, crea e implementa l’intero progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## Creare un Product Teaser {#author-product-teaser}

Dopo aver distribuito gli aggiornamenti di codice, aggiungi una nuova istanza del componente Product Teaser nella home page del sito utilizzando gli strumenti di authoring AEM. Questo ci consentirà di visualizzare gli stili aggiornati.

1. Apri una nuova scheda del browser e passa alla **Home page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Espandi Asset Finder (la barra laterale) in **Modifica** modalità. Passa al filtro Risorsa in **Prodotti**.

   ![Espandi Asset Finder e filtra per prodotti](../assets/style-cif-component/drag-drop-product-page.png)

1. Trascina un nuovo prodotto nella home page del contenitore di layout principale:

   ![Product Teaser con bordo rosa](../assets/style-cif-component/pink-border-product-teaser.png)

   Dovresti vedere che Product Teaser ora ha un bordo rosa brillante in base alla modifica della regola CSS creata in precedenza.

## Verificare le librerie client sulla pagina {#verify-client-libraries}

Quindi verifica l’inclusione delle librerie client nella pagina.

1. Passa a **Home page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona il menu **Informazioni pagina** e fai clic su **Visualizza come pubblicato**:

   ![Visualizza come pubblicato](../assets/style-cif-component/view-as-published.png)

   La pagina viene aperta senza caricare alcun JavaScript di authoring di AEM, come apparirebbe sul sito pubblicato. Osserva che l’url ha il parametro di query `?wcmmode=disabled` aggiunto. Quando si sviluppano CSS e JavaScript, è buona norma utilizzare questo parametro per semplificare la pagina, rimuovendo elementi dell’istanza di authoring di AEM.

1. Visualizza l’origine della pagina e individua diverse librerie client incluse:

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   Le librerie client distribuite alla pagina hanno il prefisso `/etc.clientlibs` e vengono serviti tramite un [proxy](/help/implementing/developing/introduction/clientlibs.md) per evitare di esporre qualsiasi elemento sensibile in `/apps` o `/libs`.

   Avviso `venia/clientlibs/clientlib-site.min.css` e `venia/clientlibs/clientlib-site.min.js`. Si tratta dei file CSS e JavaScript compilati derivati da `ui.frontend` modulo .

## Inclusione della libreria client con i modelli di pagina {#client-library-inclusion-pagetemplates}

Sono disponibili diverse opzioni per includere una libreria lato client. Controlla come il progetto generato include `clientlib-site` librerie tramite [Modelli di pagina](/help/implementing/developing/components/templates.md).

1. Passa a **Home page** del sito nell’editor AEM: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona la **Informazioni pagina** menu e fai clic su **Modifica modello**:

   ![Modificare il modello](../assets/style-cif-component/edit-template.png)

   Verrà aperto il **Pagina di destinazione** modello **Pagina principale** La pagina è basata su.

   >[!NOTE]
   >
   > Per visualizzare tutti i modelli disponibili dalla schermata iniziale AEM, passa a **Strumenti** > **Generale** > **Modelli**.

1. Nell’angolo in alto a sinistra, seleziona l’icona **Informazioni pagina** e fai clic su **Criterio pagina**.

   ![Voce di menu Criterio pagina](../assets/style-cif-component/page-policy-menu.png)

1. Verrà aperto il Criterio pagina per il modello Pagina di destinazione:

   ![Criterio pagina : pagina di destinazione](../assets/style-cif-component/page-policy-properties.png)

   Sul lato destro è disponibile un elenco delle **categorie** di librerie client che verranno incluse in tutte le pagine che utilizzano questo modello.

   * `venia.dependencies` - Fornisce tutte le librerie di fornitori `venia.site` dipende da.
   * `venia.site` - Questa è la categoria `clientlib-site` che `ui.frontend` viene generato dal modulo.

   Altri modelli utilizzano lo stesso criterio: **Pagina di contenuto**, **Pagina di destinazione** e così via. Riutilizzando lo stesso criterio, possiamo essere certi che le stesse librerie client verranno incluse in tutte le pagine.

   Quando si gestisce l’inclusione delle librerie client mediante l’uso di modelli e criteri di pagina, si può modificare il criterio a livello di modello. Ad esempio, supponiamo di dover gestire due marchi diversi nella stessa istanza di AEM. Ogni marchio avrà un proprio stile o un proprio *tema*, ma le librerie e il codice di base saranno gli stessi. Un altro esempio, nel caso di una libreria client più grande che si voglia visualizzare solo su determinate pagine, si può creare un criterio di pagina univoco solo per quel modello.

## Sviluppo Webpack locale {#local-webpack-development}

Nell’esercizio precedente, è stato effettuato un aggiornamento a un file Sass nel `ui.frontend` e dopo aver eseguito una build Maven, le modifiche vengono distribuite in AEM. Ora cercheremo di sfruttare un webpack-dev-server per sviluppare rapidamente gli stili front-end.

Il webpack-dev-server proxy immagini e alcuni dei CSS/JavaScript dell&#39;istanza locale di AEM, ma consente allo sviluppatore di modificare gli stili e JavaScript nel `ui.frontend` modulo .

1. Nel browser passa alla **Pagina principale** pagina e **Visualizza come pubblicato**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. Visualizza l’origine della pagina e la **copia** il HTML non elaborato della pagina.

1. Torna all’IDE che preferisci sotto la `ui.frontend` il modulo apre il file: `ui.frontend/src/main/static/index.html`

   ![File HTML statico](../assets/style-cif-component/static-index-html.png)

1. Sovrascrivi il contenuto di `index.html` e **incolla** il HTML copiato nel passaggio precedente.

1. Trova gli &quot;include&quot; per `clientlib-site.min.css`, `clientlib-site.min.js` e **remove** loro.

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   Questi vengono rimossi perché rappresentano la versione compilata del CSS e JavaScript generato dal `ui.frontend` modulo . Lascia le altre librerie client così come verranno proxy dall&#39;istanza AEM in esecuzione.

1. Apri una nuova finestra terminale e passa alla `ui.frontend` cartella. Esegui il comando `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   Verrà avviato il webpack-dev-server su [http://localhost:8080/](Http://localhost:8080/)

   >[!CAUTION]
   >
   > Se ricevi un errore relativo a Sass, interrompi il server ed esegui il comando `npm rebuild node-sass` e ripeti i passaggi precedenti. Ciò può verificarsi se una versione diversa di `npm` e `node` quindi specificato nel progetto `aem-cif-guides-venia/pom.xml`.

1. Passa a [http://localhost:8080/](Http://localhost:8080/) in una nuova scheda con lo stesso browser di un’istanza di AEM registrata. Dovresti vedere la home page di Venia tramite il webpack-dev-server:

   ![Server di sviluppo Webpack sulla porta 80](../assets/style-cif-component/webpack-dev-server-port80.png)

   Lasciare in esecuzione il webpack-dev-server. Sarà utilizzato nel prossimo esercizio.

## Implementare lo stile della scheda per Product Teaser {#update-css-product-teaser}

Quindi modifica i file Sass nel `ui.frontend` modulo per implementare uno stile simile a una scheda per Product Teaser. Il webpack-dev-server verrà utilizzato per vedere rapidamente le modifiche.

Torna all’IDE e al progetto generato.

1. In **ui.frontend** riaprire il file `_productteaser.scss` a `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

1. Apporta le seguenti modifiche al bordo del Product Teaser:

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
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

   Salvare le modifiche e il webpack-dev-server dovrebbe aggiornarsi automaticamente con i nuovi stili.

1. Aggiungi un’ombra esterna e includi angoli arrotondati al Product Teaser.

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. Aggiorna il nome del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

   ```css
   .item__name {
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

1. Aggiorna il prezzo del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. Aggiorna la query multimediale in basso per impilare il nome e il prezzo in schermate più piccole di **992 px**.

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

   Ora dovresti vedere lo stile della scheda riflesso nel webpack-dev-server:

   ![Modifiche al teaser di Webpack Dev Server](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   Tuttavia, le modifiche non sono state ancora distribuite AEM. Puoi scaricare il [file della soluzione qui](../assets/style-cif-component/_productteaser.scss).

1. Distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale a riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >Sono disponibili [strumenti e configurazione IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) aggiuntivi per sincronizzare i file di progetto direttamente con un’istanza AEM locale senza dover eseguire una generazione Maven completa.

## Visualizzare il Product Teaser aggiornato {#view-updated-product-teaser}

Una volta implementato in AEM il codice per il progetto, dovrebbe essere possibile vedere le modifiche apportate al Product Teaser.

1. Torna al browser e aggiorna la home page: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). Dovresti vedere gli stili del product teaser aggiornati.

   ![Stile del Product Teaser aggiornato](../assets/style-cif-component/product-teaser-new-style.png)

1. Prova ad aggiungere altri Product Teaser. Utilizza la modalità Layout per modificare la larghezza e l’offset dei componenti in modo da visualizzare più teaser su una riga.

   ![Product Teaser multipli](../assets/style-cif-component/multiple-teasers-final.png)

## Risoluzione dei problemi {#troubleshooting}

Puoi verificare in [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) che il file CSS aggiornato sia stato distribuito: [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

Quando si distribuiscono nuovi file CSS e/o JavaScript, è importante anche assicurarsi che il browser non distribuisca file non aggiornati. A tale scopo, cancella la cache del browser o avvia una nuova sessione del browser.

AEM inoltre tenta di memorizzare nella cache le librerie client per migliorare le prestazioni. A volte, dopo la distribuzione del codice, vengono distribuiti i file meno recenti. Puoi annullare manualmente la validità della cache della libreria client di AEM utilizzando lo strumento [Rigenera librerie client](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Se si sospetta che AEM abbia memorizzato nella cache una versione precedente di una libreria client, è meglio annullare la validità della cache. La rigenerazione delle librerie è infatti inefficiente e richiede molto tempo.*

## Congratulazioni {#congratulations}

Hai appena formattato il tuo primo componente core CIF AEM e hai utilizzato un server di sviluppo webpack!

## Sfida bonus {#bonus-challenge}

Usa il [Sistema di stili di AEM](/help/sites-cloud/authoring/features/style-system.md) per creare due stili che possono essere attivati/disattivati da un autore di contenuti. La sezione su come [sviluppare con il sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html?lang=it) include passaggi dettagliati e informazioni su come eseguire questa operazione.

![Sfida bonus - Sistema di stili](../assets/style-cif-component/bonus-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
* [Configurare un ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [Librerie lato client](/help/implementing/developing/introduction/clientlibs.md)
* [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)
* [Sviluppo con il sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
